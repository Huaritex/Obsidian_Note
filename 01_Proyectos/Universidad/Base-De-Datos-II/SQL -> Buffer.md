---
tags: ['note', 'database', 'sql', project]
fecha_creacion: 2026-02-14
relaciones: []
---
[[SQL -> Indices]]
## Buffer

> Un bufer es una de 8kb en memoria(el mismo tamano que una pagina de indice o de datos).

> El grupo de buffers es un recurso global compartido por todas las bases de datos para sus paginas de datos en cache.
> Proporciona una Extension de memoria de acceso aleatorio volatil SSD al motor de base de datos, lo que mejora significativamente el rendimiento.

---

## Beneficios Grupo de Buffers

### Mejora de Rendimiento 

- Puede reducir la carga en los dispositivos de almacenamiento fisico, ya que minimiza la frecuencia con la que se accede directamente a ellos. Esto puede ser beneficioso para sistemas con altas carga de trabajo y limitaciones en la capacida de almacenamiento

### Mejora de Concurrencia

- Puede mejorar la concurrencia al permitir que varias transacciones accedan a los mismos datos

### Reduccion del trafico de E/S




---

## Pagina de Buffer

```SQL
SELECT ProductID, name, ListPrice
FROM Production.product p
WHERE exists(
	SELECT 1
	FROM Sales.SalesOrderDetail sod
	WHERE sod.ProductID = p.ProductID
);
```

## Limpiar Buffer

```SQL
DBCC DROPCLEANBUFFERS;
```

## Configurar Memoria Asignadas

```SQL
EXEC sp_configure 'show advanced options', 1;
RECONFIGURE;
EXEC sp_configure 'max server memory';
```

--- 










