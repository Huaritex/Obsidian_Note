
![[Pasted image 20260214101033.png]]


```
set statistics XML ON

SELECT

c.CustomerID,

SUM(soh.TotalDue) AS TotalCompras

FROM

Sales.SalesOrderHeader AS soh

INNER JOIN

Sales.SalesOrderDetail AS od ON soh.SalesOrderID = od.SalesOrderID

INNER JOIN

Sales.Customer AS c ON soh.CustomerID = c.CustomerID

GROUP BY

c.CustomerID

HAVING

SUM(soh.TotalDue) > 500000

ORDER BY

TotalCompras DESC;

set statistics XML OFF
```



![[Pasted image 20260214103126.png]]


```
GO

set STATISTICS XML ON

SELECT

p.Name,

SUM(sod.OrderQty) AS TotalCantidad,

SUM(sod.LineTotal) AS TotalVenta

FROM Sales.SalesOrderDetail sod

JOIN Production.Product p

ON CAST(sod.ProductID AS VARCHAR(50)) = CAST(p.ProductID AS VARCHAR(50))

JOIN Sales.SalesOrderHeader soh

ON sod.SalesOrderID = soh.SalesOrderID

WHERE

YEAR(soh.OrderDate) = 2013

AND p.Name LIKE '%Bike%'

GROUP BY

p.Name

ORDER BY

TotalVenta DESC;

SET STATISTICS XML OFF

GO
```

