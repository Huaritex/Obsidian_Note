---
tags: ['note', 'computer-science', 'algorithms', 'data-structures']
fecha_creacion: 2026-02-14
relaciones: []
---

# Árboles y Grafos

## Árboles (Trees)
> [!info] Estructura de datos jerárquica no lineal.

### Tipos Comunes
1.  **Árbol Binario**: Cada nodo tiene a lo sumo dos hijos (izquierdo y derecho).
2.  **Árbol de Búsqueda Binaria (BST)**:
    -   Hijo izquierdo < Padre.
    -   Hijo derecho > Padre.
    -   Búsqueda eficiente: O(log n).
3.  **Árbol AVL**: Árbol BST auto-balanceado.

### Recorridos
-   **In-Order (Izquierda-Raíz-Derecha)**: Visita los nodos en orden ascendente (en BST).
-   **Pre-Order (Raíz-Izquierda-Derecha)**: Útil para copiar árboles.
-   **Post-Order (Izquierda-Derecha-Raíz)**: Útil para eliminar árboles.

---

## Grafos (Graphs)
> [!info] Representación de relaciones entre objetos.

### Componentes
-   **Vértices (V)**: Nodos.
-   **Aristas (E)**: Conexiones entre nodos.

### Algoritmos de Búsqueda
1.  **BFS (Breadth-First Search)**:
    -   Búsqueda en anchura (por niveles).
    -   Usa una **Cola**.
    -   Encuentra el camino más corto en grafos no ponderados.

2.  **DFS (Depth-First Search)**:
    -   Búsqueda en profundidad.
    -   Usa una **Pila** (o recursión).
    -   Útil para detectar ciclos y componentes conectados.
