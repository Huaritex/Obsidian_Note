---
tags: ['note', 'database', 'sql', project]
fecha_creacion: 2026-02-14
relaciones: []
---
[[SQL -> Indices]]
# Consultar las paginas en cache antes de ejecutar consultas grandes

```SQL
SELECT
COUNT(*) as paginas_en_buffer,
DB_NAME(database_id) as nombre_base_datos
FROM sys.dm_os_buffer_descriptors
GROUP BY database_id;
```

![[Pasted image 20260228090156.png]]

# Ejecutar una consulta grande para llenar el buffer pool

```SQL
SELECT * 
from Production.Product as P
full OUTER JOIN Sales.SalesOrderDetail as S
ON P.ProductID = S.ProductID
FULL OUTER JOIN Sales.SalesOrderHeader as H
ON S.SalesOrderID = H.SalesOrderID
FULL OUTER JOIN Sales.Customer as C
ON H.CustomerID = C.CustomerID
```

![[Pasted image 20260228090439.png]]

# Verificar el impacto en el buffer pool

```SQL
SELECT 
    COUNT(*) as paginas_en_buffer,
    DB_NAME(database_id) as nombre_base_datos
    FROM sys.dm_os_buffer_descriptors
    GROUP BY database_id;
```

![[Pasted image 20260228090810.png]]

# Limpiar el Buffer Pool

```SQL
    DBCC DROPCLEANBUFFERS;
```

![[Pasted image 20260228090958.png]]

# Repetir la consulta grande
```SQL
SELECT * 
from Production.Product as P
full OUTER JOIN Sales.SalesOrderDetail as S
ON P.ProductID = S.ProductID
FULL OUTER JOIN Sales.SalesOrderHeader as H
ON S.SalesOrderID = H.SalesOrderID
FULL OUTER JOIN Sales.Customer as C
ON H.CustomerID = C.CustomerID
```

![[Pasted image 20260228091214.png]]

---

## Preguntas

- `Que impacto tiene el buffer pool en la velocidad de las consultas?`

>Más datos en buffer pool = menos accesos a disco = consultas más rápidas. Es como tener los libros que más usas en tu escritorio en vez de ir cada vez a la biblioteca.

- `Como afecta la prelectura al rendimiento de SQL Server?`

> Sirve muchos para consultas pesadas como las tablas completas, si antes ejecute DBCC DROPCLEANBUFFERS, que esta arriba en el archivo, se limpia la RAM y la prelectur tiene que volver a cargar todo desde disco

- `Como puedes optimizar la memoria para mejorar la velocidad de las consultas?`

> Si tengo mas espacio y solo pongo lo que necesito trabajaria mas rapido. Si lleno el escritorio con cosas que no uso , se volveria mas lento

