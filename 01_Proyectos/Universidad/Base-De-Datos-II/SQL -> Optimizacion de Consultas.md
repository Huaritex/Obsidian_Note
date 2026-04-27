---
tags: ['note', 'database', 'sql', project]
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

![[Pasted image 20260221203409.png]]


---

## Prioridad por Operador

> La prioridad de operador determina la secuencia en que se realizara las operaciones


| **Nivel** | **Operadores**                                                                                                                |
| --------- | ----------------------------------------------------------------------------------------------------------------------------- |
| **1**     | ~ (operador bit a bit NOT)                                                                                                    |
| **2**     | *(multiplicacion), /(division), %(modulo)                                                                                     |
| **3**     | +(Positivo), -(Negativo), +(suma), +(concatenacion), -(Resta), &(AND bit a bit), ^(OR exclusivo bit a bit), \| (OR bit a bit) |
| **4**     | =,>,<,>=,<=,<>,!=,!>,!< (Operadores de comparacion)                                                                           |
| **5**     | NOT                                                                                                                           |
| **6**     | Y                                                                                                                             |
| **7**     | ALL ,ANY ,BETWEEN ,IN ,LIKE ,OR ,SOME                                                                                         |

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
FROM Sales.SalesOrderHeader
GROUP BY SalesOrderID, CustomerID;
```

```SQL
SELECT CustomerID, SUM(TotalDue), AS TotalSprent
FROM Sales.SalesOrderHeader
GROUP BY CustomerID;
```


### Uso de Indices y Estadisticas

> Los Indices y las estadisticas juegan un papel crucial en la optimizacion de consultas.

```SQL
SELECT SalesOrderID, TotalDue
FROM Sales.SalesOrderHeader
WHERE CustomerID = 11000 AND OrderDate >= '2013-01-01';

CREATE INDEX idx_Customer_OrderDate ON Sales.SalesOrderHeader (CustomerID, OrderDate);
```

