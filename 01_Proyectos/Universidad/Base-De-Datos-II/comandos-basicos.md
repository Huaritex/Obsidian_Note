---
tags: ['note', 'database', 'sql']
fecha_creacion: 2026-02-14
relaciones: []
---

# Comandos Básicos de SQL

> [!info] Structured Query Language (SQL) es el lenguaje estándar para gestionar bases de datos relacionales.

## DDL (Data Definition Language)

> [!summary] Define la estructura de la base de datos (tablas, índices, etc.).

-   **CREATE TABLE**: Crea una nueva tabla.
-   **ALTER TABLE**: Modifica una tabla existente.
-   **DROP TABLE**: Elimina una tabla.
-   **TRUNCATE**: Elimina todos los datos de una tabla sin borrar la estructura.

```sql
CREATE TABLE Usuarios (
    ID INT PRIMARY KEY,
    Nombre VARCHAR(50) NOT NULL,
    Email VARCHAR(100) UNIQUE
);
```

## DML (Data Manipulation Language)

> [!summary] Manipula los datos dentro de las tablas.

-   **SELECT**: Recupera datos.
-   **INSERT**: Agrega nuevos registros.
-   **UPDATE**: Modifica registros existentes.
-   **DELETE**: Elimina registros.

```sql
SELECT * FROM Usuarios WHERE Nombre = 'Juan';
INSERT INTO Usuarios (Nombre) VALUES ('Maria');
UPDATE Usuarios SET Email = 'maria@mail.com' WHERE ID = 2;
```

## Avanzado: JOINs

> [!important] Combinar filas de dos o más tablas basándose en una columna relacionada.

-   **INNER JOIN**: Devuelve filas cuando hay coincidencia en ambas tablas.
-   **LEFT JOIN**: Devuelve todas las filas de la izquierda y las coincidentes de la derecha.
-   **RIGHT JOIN**: Devuelve todas las filas de la derecha y las coincidentes de la izquierda.
-   **FULL OUTER JOIN**: Devuelve todas las filas si hay coincidencia en cualquiera de las tablas.

```sql
SELECT Pedidos.ID, Clientes.Nombre
FROM Pedidos
INNER JOIN Clientes ON Pedidos.ClienteID = Clientes.ID;
```

## Normalización
> [!info] Proceso para organizar datos y reducir la redundancia.

1.  **1NF (Primera Forma Normal)**: Atomicidad (valores indivisibles).
2.  **2NF**: 1NF + Dependencia funcional completa (clave primaria).
3.  **3NF**: 2NF + No dependencias transitivas.

---
