---
tags:
  - Code
  - JS
aliases:
  - Js-concepts
---

JavaScript es uno de los lenguajes más usados en el mundo del desarrollo web, este tiene bastante sintaxis y shortcuts para desarrollar, así como bastante teoría detrás de el.

JavaScript es un lenguaje de programación orientado a la web, originalmente fue pensado de forma dinámica, pues el manejar todos los datos que se pueden pasar en una web de forma tipada era una tarea muy tediosa. Después de su alta demanda y gran aceptación entre los desarrolladores este fue movido a un entorno de desarrollo donde no solo corre en los navegadores, sino que también corre en el lado del servidor, actualmente los **entornos de ejecución** mas famosos de JS son:

- NodeJS
- Deino
- Bun
*Siendo NodeJS el mas famoso*

Este lenguaje de programación no utiliza "*semicolons*" técnicamente, dado que el compilador interno se encarga de colocarlas de forma automática, utilizando los saltos de linea como una semicolon implícita, o el cierre de funciones, sin embargo hay ocasiones donde el compilador falla y da errores que son muy difíciles de detectar:
```JavaScript
alert("Hello")
[1,2].forEach(alert)
```

# Tipos de datos

>Para conocer el tipo de dato de una variable podemos utilizar la función **typeof**. 
> 
>	console.log(typeof var);

En JS existen diferentes tipos de datos, pero estos se pueden agrupar en 2 grandes grupos:
### Basicos o Primitivos \ Basic or Primitive 
En JS, un valor primitivo es aquel que no es un objeto y no tiene métodos.
Todos los primitivos son Inmutables.
Ejemplos de datos primitivos son:
- Integer
- String
- Boolean
[[Basic - Primitive data type]]


### Definidos por el usuario \ User Defined
Los tipos de datos no primitivos incluyen:
- Objetos
- Arrays 
- Funciones (Que son derivaciones de objetos en JS)
Todos los tipos de datos no primitivos son mutables, es decir pueden ser alterados.

# Funciones:

