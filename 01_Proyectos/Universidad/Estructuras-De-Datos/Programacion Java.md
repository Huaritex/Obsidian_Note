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

