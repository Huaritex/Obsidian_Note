---
tags: ['note', 'programming', 'csharp', 'oop']
fecha_creacion: 2026-02-14
relaciones: []
---

# Programación en C#

> [!info] Lenguaje de programación multiparadigma desarrollado por Microsoft, orientado a objetos y fuertemente tipado.

## Características Principales
-   **Orientado a Objetos (POO)**: Encapsulamiento, Herencia, Polimorfismo.
-   **Seguridad de Tipos**: Compilación estática que evita errores comunes.
-   **Garbage Collection**: Gestión automática de memoria.

---

## Conceptos de POO

### 1. Encapsulamiento (Encapsulation)
> [!summary] Ocultar el estado interno y requerir que todas las interacciones se realicen a través de una interfaz.

```csharp
public class CuentaBancaria {
    private decimal saldo; // Privado

    public void Depositar(decimal monto) { // Público
        if (monto > 0) saldo += monto;
    }
}
```

### 2. Herencia (Inheritance)
> [!summary] Una clase (hija) puede heredar atributos y métodos de otra (padre).

```csharp
public class Animal {
    public void Comer() { Console.WriteLine("Comiendo..."); }
}

public class Perro : Animal {
    public void Ladrar() { Console.WriteLine("Guau!"); }
}
```

### 3. Polimorfismo (Polymorphism)
> [!summary] Capacidad de tratar objetos de diferentes clases de manera uniforme.

```csharp
public virtual void HacerSonido() { ... }
public override void HacerSonido() { ... }
```

### 4. Abstracción (Abstraction)
> [!summary] Ocultar la complejidad y exponer solo lo esencial.

```csharp
public abstract class Forma {
    public abstract double CalcularArea();
}
```

---

## Sintaxis Básica

### Variables y Tipos
```csharp
int edad = 25;
string nombre = "Juan";
bool esEstudiante = true;
var fecha = DateTime.Now; // Inferencia de tipos
```

### Estructuras de Control
```csharp
// If-Else
if (edad >= 18) {
    Console.WriteLine("Mayor de edad");
}

// Bucles
for (int i = 0; i < 5; i++) {
    Console.WriteLine(i);
}

foreach (var item in lista) {
    Console.WriteLine(item);
}
```
