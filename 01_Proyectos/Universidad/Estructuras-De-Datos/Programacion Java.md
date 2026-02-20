---
tags:
  - note
  - computer-science
  - algorithms
  - data-structures
fecha_creacion: 2026-02-14
relaciones: []
---
 [[programacion-estructurada]]
# Java

> [!summary] Que es Java?

> Java es un lenguaje `orientada a objetos` y `fuertemente tipado`
- `Orientado a Objetos:` Todo se construye como si fueran "piezas" o "maquetas". (Clases)
- `Fuertemente Tipado:` Si dices una variable es un numero entero , no puede meterle un texto despues. Esto evita errores en estructuras de datos complejas.

---

## Sintaxis Basica

> Java , no puedes lanzar código al aire. Todo debe vivir dentro de una **Clase**. Imagina que una clase es el plano arquitectónico de una casa.

```java
public class Estudiante {
    // 1. Atributos (Variables) -> Lo que el objeto "tiene"
    String nombre;
    int edad;

    // 2. Constructor -> Cómo se crea el objeto
    public Estudiante(String nombre, int edad) {
        this.nombre = nombre;
        this.edad = edad;
    }

    // 3. Métodos -> Lo que el objeto "hace"
    public void saludar() {
        System.out.println("Hola, soy " + nombre);
    }
}
```

### Conceptos Clave que confunden

- `public:` significa que cualquiera puede usarlo
- `static:` Significa que algo le pertenece a la clase en general, no a un objeto especifico
- `void:` Significa que el método hace algo pero no te devuelve ningún resultado (como una impresora que imprime pero no te entrega un papel de vuelta con datos).

---

## Estructuras de Datos y POO

> Aquí es donde Java brilla. Las estructuras de datos no son más que formas de organizar objetos en la memoria.

### A. El Nodo: La base de todo

> Para entender estructuras como Listas Enlazadas o Árboles, debes entender el concepto de **Nodo**. Un Nodo es un objeto que guarda un valor y "apunta" a otro objeto.

```java
public class Nodo {
    int valor;      // El dato que guardamos
    Nodo siguiente; // La referencia al siguiente "eslabón" de la cadena

    public Nodo(int valor) {
        this.valor = valor;
        this.siguiente = null; // Al principio no apunta a nadie
    }
}
```

### B. Listas Enlazadas (Sintaxis en Accion)

> Si quieres crear una lista, básicamente conectas objetos Nodo.

```java
public class ListaSimple {
    Nodo cabeza; // El primer elemento de la lista

    public void agregar(int valor) {
        Nodo nuevo = new Nodo(valor);
        if (cabeza == null) {
            cabeza = nuevo;
        } else {
            // Lógica para recorrer la lista y ponerlo al final
        }
    }
}
```

---

## Diferencias de Sintaxis Criticas

> Para manejar estructuras de datos, debes distinguir entre estos tipos de datos:

| **Tipo**                  | **Ejemplo**                   | **Memoria**                                     |
| ------------------------- | ----------------------------- | ----------------------------------------------- |
| **Primitivos**            | `int`, `double`, `boolean`    | Guardan el valor real.                          |
| **Objetos (Referencias)** | `String`, `Nodo`, `ArrayList` | Guardan la **dirección** de dónde está el dato. |

> [!inote] Nota Importante:  En estructuras de datos, casi siempre trabajarás con **Referencias**. Cuando dices `nodoA.siguiente = nodoB`, no estás copiando el objeto, estás creando un "puente" entre ellos.

---

## POO Dificultades

>[!info] Probablemente porque intentas ver el código de forma lineal (paso 1, paso 2...). En Java, debes pensar en **responsabilidades**:

- `La Clase Nodo:` Solo sabe guardar un dato y quien sigue.
- `La Clase Lista:` Sabe como agregar . borrar o buscar, pero no le importa que hay dentro del Dato.
- `La Clase Principal:` Es el director de orquesta que crea los objetos y les dice que hacer.

---





funciones -> Devuelve un valor
procedimiento -> No devuelve nada

ambas se les conoce como -> Metodo

hay dos tipos de variables primitivas
-> Primitiva: Int, char, etc
-> No Primitiva: String por ejemplo

Tanto funciones como Procedimientos tienen parametros
Estos Parametros pueden ser por Referencia o por Valor

Preguntas:
- Porque se le dice programacion estructurada?
- POO Estructurada?
- Que es Paradigma Estructurada?

Instalar .NET, C# -> NET  core


Relacionado: [[programacion-csharp]]



- Ejercicio de Convertir numero a Literal

```C++
#include <iostream>
using namespace std;

  

int main() {

const char* numeros[4][10] = {

{"", "uno", "dos", "tres", "cuatro", "cinco", "seis", "siete", "ocho", "nueve"},

{"", "diez", "veinte", "treinta", "cuarenta", "cincuenta", "sesenta", "setenta", "ochenta", "noventa"},

{"", "cien", "doscientos", "trescientos", "cuatrocientos", "quinientos", "seiscientos", "setecientos", "ochocientos", "novecientos"},

{"mil"}

};

  

int numero;

cout << "Ingrese un numero del 1 al 1000: ";

cin >> numero;

  

if (numero < 1 || numero > 1000) {

cout << "Numero fuera de rango." << endl;

return 1;

}

  

if (numero == 1000) {

cout << numeros[3][0] << endl;

return 0;

}

  

int centenas = numero / 100;

int decenas = (numero % 100) / 10;

int unidades = numero % 10;

  

if (centenas > 0) {

cout << numeros[2][centenas] << " ";

}

if (decenas > 0) {

cout << numeros[1][decenas] << " ";

}

if (unidades > 0) {

cout << numeros[0][unidades] << " ";

}

  

return 0;

}
```

- Hacer una funcion sin bucles,  para sacar cuantos numeros tiene un digito

```C++
#include <iostream>
using namespace std;

int num(int numero){

if(numero < 10){

return 1;

}

return 1 + num(numero/10);

}

  

int main() {

int numero;

cout << "Ingrese un numero: ";

cin >> numero;

cout << "El numero tiene " << num(numero) << " digitos." << endl;

return 0;
}

