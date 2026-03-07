---
tags:
  - note
  - database
  - sql
fecha_creacion: 2026-02-14
relaciones:
  - "[[SQL -> Indices]]"
---

>[!abstract] **Relacionado con:** [[SQL -> Indices]]

# Definición de Vistas

> Son consultas almacenadas que proporcionan una representación virtual de los datos, permitiendo a los usuarios acceder a datos específicos sin cambiar la estructura de las tablas subyacentes.

>[!note] Características principales
> Se basa en una consulta SQL y se almacena en la base de datos con un nombre específico.

---

## 🎯 Objetivo

- **Simplificar consultas complejas:** Si tienes una consulta larga con muchas uniones (`JOIN`), condiciones (`WHERE`), agrupaciones (`GROUP BY`), etc., puedes guardarla como una vista y luego consultarla como si fuera una tabla.
- **Seguridad y control de acceso:** Pueden restringir el acceso a ciertas columnas o filas sin exponer toda la tabla original.
- **Facilitar el mantenimiento:** Si el esquema cambia, puedes actualizar solo la vista sin afectar el código de las aplicaciones que la usan.
- **Reutilización:** Si varios usuarios necesitan la misma consulta, una vista evita que tengan que escribir la misma consulta una y otra vez.

---

## 🛠 Utilidad

- Para **centrar, simplificar y personalizar** la percepción de la base de datos para cada usuario.
- Como mecanismo de **seguridad**, permiten a los usuarios obtener acceso a los datos por medio de la vista, pero no les conceden el permiso de obtener acceso directo a las tablas subyacentes de la consulta.
- Para proporcionar una **interfaz compatible con versiones anteriores** con el fin de emular una tabla que existía pero cuyo esquema ha cambiado.

---

## 🗂 Tipos de Vistas 

- 👉 **Vistas Simples:** Se basan en una sola tabla.
- 👉 **Vistas Complejas:** Combinan datos de múltiples tablas, o bien de otras vistas de la base de datos actual u otras bases de datos.

---

## ⚙ Creación de Vistas en SQL

> Para crear una vista en SQL, se utiliza la instrucción `CREATE VIEW`, seguida del nombre de la vista y la consulta `SELECT` que define su contenido. Esto permite modularizar y reutilizar consultas.

### Sintaxis

```sql
CREATE VIEW nombre_vista AS
SELECT columna1, columna2
FROM tabla
WHERE condicion;
```

### Ejemplo de Consultas con Vistas

```sql
CREATE VIEW vm_ClientesOrdenes AS
SELECT
    p.businessentityid AS ClienteID,
    p.Firstname + ' ' + p.Lastname AS NombreCliente,
    soh.OrderDate AS ID_Orden,
    soh.SalesOrderID AS fechaOrden,
    soh.Totaldue AS MontoTotal 
FROM Sales.SalesOrderHeader AS soh
JOIN Sales.Customer AS c ON soh.CustomerID = c.CustomerID
JOIN Person.Person AS p ON c.PersonID = p.BusinessEntityID;
```

---

## ✨ Ventajas de Usar Vistas

- Simplifican las consultas complejas.
- Mejoran la seguridad al restringir el acceso a datos sensibles y permiten reutilizar código, lo que mejora la eficiencia del desarrollo de consultas.

```sql
CREATE VIEW vw_clientes_segura
WITH SCHEMABINDING
AS
SELECT BusinessEntityID, FirstName, LastName
FROM dbo.Person;
```

---

## 📌 Resumen

- Una vista **no almacena datos**, solo una consulta predefinida.
- Se pueden hacer consultas (`SELECT`) sobre una vista como si fuera una tabla normal.
- Algunas vistas permiten modificaciones (`INSERT`, `UPDATE`, `DELETE`), pero hay restricciones.
- En bases de datos grandes, las vistas pueden mejorar el rendimiento en ciertos casos, pero a veces pueden ser lentas si la consulta es muy compleja.
- Simplifican el acceso a datos, mejoran la seguridad y facilitan el desarrollo de aplicaciones al proporcionar una interfaz flexible y reutilizable para interactuar con la base de datos.