---
tags: ['note', 'database', 'sql']
fecha_creacion: 2026-02-14
relaciones: []
---
[[SQL -> Indices]]
## Optimizacion de Consultas

> Proceso de mejorar el rendimiento de las consultas SQL

## Orden de Ejecucion de Consulta

```SQL
SELECT
FROM
JOIN 
ON
WHERE
GROUP BY
HAVING
ORDER BY
LIMIT --TOP

```

---

## Operadores Logicos




---

## Prioridad por Operador

> La prioridad de operador 


---

## Tecnicas de Reescritura de Consultas

### `Optimizacion de JOINS`

> Los JOINS son una parte integral de muchas consultas SQL, pero pueden ser una fuente de ineficiencia si no se manejan adeucadamente:

-> Utilizar JOINs explicitos en lugar de JOINs implicitos

>[!info] Explicito

```SQL
SELECT p.name as Product, sc.name as Subcategoria
FROM Production.Product p
INNER JOIN Production.ProductSubcategory sc
ON p.ProductSubcategoryID = sc.ProductSubcategoryID
```

>[!info] Implicito

```SQL
SELECT p.name as Product, sc.name as Subcategoria
FROM Production.Product p
,Production.ProductSubcategory sc
WHERE p.ProductSubcateogryID = sc.ProductSubcategoryID
```

-> Seleccionar solo las Consultas necesarias en la clausula SELECT en un lugar de seleccionar todas las columnas

-> Utilizar Indices en las columnas involucradas en los JOINs para mejorar el rendimiento

---
## `Subconsultas Correlacionadas vs Subconsultas Independiente`

> Las subconsultas independientes tienden a ser mas eficientes que las subconsultas correlacionadas

```SQL
SELECT firstname, lastname, rate AS salary
FROM humanresources.employee E
INNER JOIN person.person P ON E.businessentityID = P.businessentityID
INNER JOIN humanresources.employeepayhistory PH ON E.businessentityID = PH.businessentityID
WHERE rate > (
	SELECT avg(rate)
	FROM humanresources.employeepayhistory
);
```

### Correlacional

```SQL
select customerid
from sales.Customer C
where CustomerID in (
    select CustomerID FROM
    Sales.SalesOrderHeader H
    WHERE h.CustomerID = C.CustomerID
    AND TotalDue <= 1000)
```

### Uso de Clausulas de  Reescritura de Consultas

`Uso de Clausulas WHERE Y HAVING de manera eficiente:`

- Las clausulas de WHERE y HAVING son esenciales para filtrar los resultados de una consulta.
- Mover las condicionales de filtrado mas restrictivas hacia arriba en la clausula WHERE.
- Utilizar clausulas EXISTS en lugar de IN o JOINs cuando sea posible

```SQL
SELECT ProductID, name, ListPrice
FROM Production.product p
WHERE exists(
	SELECT 1
	FROM Sales.SalesOrderDetail sod
	WHERE sod.ProductID = p.ProductID
);
```

---

## Evitar Operaciones Costosas

> Algunas operaciones, como las funciones de agregacion y las operaciones de ordenamiento, pueden ser costosas en terminos de rendimiento

```SQL
SELECT SalesOrderID, custormerID, sum(TotalDUe)
```

### Uso de Indices y Estadisticas

> 