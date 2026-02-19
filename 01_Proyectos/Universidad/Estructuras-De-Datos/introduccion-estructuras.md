---
tags: ['note', 'computer-science', 'algorithms', 'data-structures']
fecha_creacion: 2026-02-14
relaciones: []
---

> [!info]
> Las **Estructuras de Datos** son formas de organizar y almacenar datos en una computadora para que puedan ser utilizados de manera eficiente.

## Clasificación General

### 1. Lineales
> [!summary] Los elementos se organizan de forma secuencial.

- **Arrays (Arreglos)**:
    - Colección de elementos del mismo tipo almacenados en memoria contigua.
    - Acceso rápido por índice (O(1)).
    - Tamaño fijo.

- **Linked Lists (Listas Enlazadas)**:
    - Elementos (nodos) dispersos en memoria, conectados por punteros.
    - Inserción/Eliminación eficiente (O(1)).
    - Acceso lento (O(n)).

- **Stacks (Pilas)**:
    - Estructura **LIFO** (Last In, First Out).
    - Operaciones: `push` (insertar), `pop` (sacar).
    - Usos: Llamadas a funciones, deshacer (undo).

- **Queues (Colas)**:
    - Estructura **FIFO** (First In, First Out).
    - Operaciones: `enqueue` (encolar), `dequeue` (desencolar).
    - Usos: Impresión, manejo de procesos.

### 2. No Lineales
> [!summary] Los elementos no siguen una secuencia única.

- **Trees (Árboles)**:
    - Estructura jerárquica con un nodo raíz y subárboles.
    - Tipos: Binarios, AVL, B-Trees.

- **Graphs (Grafos)**:
    - Conjunto de vértices (nodos) conectados por aristas.
    - Tipos: Dirigidos, No Dirigidos, Ponderados.
