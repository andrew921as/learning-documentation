---
tags:
  - JS
  - Code
---
En JS el tipado de las variables es **Dinamico**, es decir **NO** tienen un tipo de dato en particular asociado, es decir se le puede asigar cualquier valor a cualquier variable.
Ademas de esto este tiene un **Tipado Debil**, esto indica que podemos realizar operaciones entre valores de distintos tipos, hacer estas conversiones se llama [[Coerción de tipos]].
En este caso, un valor primitivo es aquel que no es un objeto, no tiene métodos ni propiedades, todos los tipos de datos primitivos son **inmutables**. Existen 7 tipos de datos primitivos en JS
- String
- Number
- BigInt
- Boolean
- Null
- Undefined
- Symbol

# String:
Este es definido como una conexión de caracteres. Cada carácter tiene su propio index en el string. 
Como es un tipo de datos primitivo este dato en inmutable.
En JS el string se crea con las comillas o comillas simples " " o ' '.

```JavaScript
const str ='I am a string'
const str2 = "I am another string"

// Al ser un tipo de dato primitivo no es mutable
let strMut = "Hola"
strMut.[0]="P";
console.log(strMut)
// Hola y no Pola
```

Aunque el String es un tipo de dato primitivo y no tiene metodos, se puede acceder al largo del string con el metodo length, esto gracias al [[Object wrapper]].

```JavaScript
"Sacha".length
// 5
```

# Number
Este representa valores numéricos que van desde el valor entero  -(2^53-1) hasta un valor entero máximo de (2^53-1)
>Para chequear el valor máximo y mínimo podemos utilizar el método Number.MAX_VALUE o Number.MIN_VALUE

El tipo Number incluye lo que en otros lenguajes llamamos Integer y también incluye Doubles
En JS para crear un number solo es necesario poner un numero:
```JavaScript
const num = 3;
console.log(typeof num);
//Se espera: number
```

En los numeros para poder truncar una valor y evitar tener problemas de redondeo se puede utilizar el metodo *toFixed*, este es utilizado por el [[Object wrapper]]

```JavaScript
(0.1+0.2).toFixed(2)
//"0.30"
//Para poder convertirlo a num se utiliza un operador logico
+(0.1+0.2).toFixed(2)
//0.30
```

**NaN** Not a Number, a pesar de que sea contradictorio NaN es de tipo numerico y representa operaciones invalidas, es un valor especial que no es igual ni a el mismo, pero hay una funcion que permite ver si un valor es NaN esa es: *isNaN(NaN)*

# BigInt
BigInt  es un tipo de dato que permite manejar y crear grandes valores enteros, ya sean positivos o negativos que se salen de los parámetros de lo que mide un number. Estos no pueden ser operados con tipos de datos Number y para crearlos solo es necesario agregar una n al final.

```JavaScript
let bignum = 123535347069584739045n

```

# Boolean
Es un tipo de dato que tiene 2 valores True y False, este tiene su equivalente en Objeto y tambien puede utilizar el [[Object wrapper]]

# Null
Es el tipo de dato para representar la ausencia de valor. Es utilizado para decir que no se ha inicializado el valor de una variable. Este tipo de dato solo tiene un valor posible Null.

### Hay un Bug 🐞
Al hacer:

```JavaScript
typeof null;
//object
```

Pero si es un tipo de dato primitivo, sin embargo este bug no puede corregirse porque esto puede dañar muchas paginas
# Undefined
Significa que el tipo de dato es desconocido, mientras que Null se utiliza para decir que la variable aun no tiene valor. Undefined se utiliza para decir que no se conoce nisiquiera su tipo de dato. Este es el tipo de dato que se le asigna a las variables cuando de declaran y no se inicializan

# Symbol
Se utilizan para crear valores unicos, este no tiene una manera literal de crearlo, para crearlo toca hacer Symbol()

``` JavaScript
var Sym = Symbol();
```
Tambien se le pueden poner descripciones, pero estas solo sirven para poder entender el codigo, por mas que se creen 2 simbolos con la misma descripcion, estos seran diferentes

```JavaScript
var sym1= Symbol("des");
var sym2= Symbol("des");

sym1===sym2;
// false
```