---
tags: ['note', 'database', 'security', 'hashing']
fecha_creacion: 2026-02-14
relaciones: []
---

# Hashes en Base de Datos

> [!info] Un hash es una función matemática que convierte una entrada de longitud variable en una salida de longitud fija (digest). Es irreversible (one-way).

## Uso Principal: Contraseñas
> [!danger] **NUNCA** almacenar contraseñas en texto plano.

### Algoritmos Comunes
1.  **MD5 / SHA-1**: Obsoletos e inseguros (colisiones rápidas).
2.  **SHA-256**: Estándar actual, pero rápido (susceptible a fuerza bruta con GPU).
3.  **Bcrypt / Argon2**: Diseñados para ser lentos ("Key Stretching"), ideales para contraseñas.

### Salt & Pepper

-   **Salt (Sal)**: Valor aleatorio único agregado a cada contraseña antes de hashear. Protege contra *Rainbow Tables*.
    ```
    Hash = SHA256(Password + Salt)
    ```
-   **Pepper (Pimienta)**: Valor secreto global agregado a todas las contraseñas, almacenado fuera de la base de datos (en código o variables de entorno).

## Índices Hash
> [!summary] Estructura de datos para búsquedas de igualdad rápida (O(1)).

-   Útil para búsquedas exactas: `WHERE email = '...'`
-   No sirve para rangos: `WHERE edad > 18` (Para esto usar B-Trees).
