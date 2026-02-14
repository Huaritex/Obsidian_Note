
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