---
tags: ['note', 'database', 'sql']
fecha_creacion: 2026-02-14
relaciones: []
---
[[hashes-base-de-datos]]
# Indices 

> Imagina que tiene un libro de 1000 paginas sobre medicina. Si quieres buscar que dice sobre la 'Aspirina' y no existiera un indice al final, tendrias que leer hoja por hoja hasta encontrar la palabra. Eso, en base de datos, se llama **Table Scan** (Escaneo de Tabla), y muy lento.
> Un indice en SQL es una estructura de datos en el disco que permite al motor de la base de datos encontrar filas especificas de forma mucho mas rapida, sin tener que revisar toda la tabla



### Indices agrupados 
- `Ordenan y almacenan` las filas de los datos de la tabla o vista de acuerdo con los valores de la clave del indice. Estos valores son las columnas incluidas en la definicion del indice.
- Solo puede haber un indice cluster por cada tabla, porque las filas de datos solo pueden estar almacenadas de una forma
- La unica ocasion en la que las filas de datos de una tabla estan ordenadas es cuando la tabla contiene un indice cluster

```sql
CREATE CLUSTERED INDEX ix_SalesOrderID
ON Sales.SalesOrderHeader(SaleOrderID);
```

## Indices No Clusterizados

> Tiene una estructura seperada de las filas de datos. Un indice no cluster contiene los valores de clave de indice no cluster y cada entrada de valor de **clave tiene un puntero** a la fila de datos que contiene el valor clave.
> El puntero de una fila de indice no cluster hacia una fila de datos se denomina localizador de fila. La estructura del localizador de filas depende de si las paginas de datos estan almacenadas en un monton o en una tabla agrupada, el localizador de fila es la clave de indice cluster.

```sql
-- CREATE UNIQUE NONCLUSTERED INDEX [AK_Products_Name]
-- ON [Production].[Product] ([Name])

CREATE NONCLUSTERED INDEX [AK_Products_Name]
ON [Production].[Product] ([Name])
```


## Implementaciones Tipicas

>[!warning] Restricciones UNIQUE

-> `UNIQUE:` Se creara un indice no cluster unico para exigir una restriccion UNIQUE de forma predeterminada.
-> `Indice independiente de una restriccion:` 

```SQL
SELECT
	i.name As Indexname;
	i.type_desc AS Indextype;
	c.name AS Columname;
FROM sys.Indexes i
JOIN sys.Index_columns ic ON i.object_id = ic.object_id AND i.index_id = ic.index_id
JOIN sys.columns c ON ic.object_id = c.object_id AND ic.column_id = c.column_id
WHERE i.object_id = OBJECT_ID('Person.Person');
```

```SQL
SELECT SalesOrderID,OrderDate,TotalDue
FROM Sales.SalesOrderHeader
WHERE CustormerID = 11000
	AND OrderDate BETWEEN '2013-01-01' AND '2014-01-01';
	
CREATE NONCLUSTERED INDEX IX_SOH_Customer_OrderDate
ON sales.salesorderheader(customerID,OrderDate)
```