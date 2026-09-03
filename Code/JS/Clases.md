Las clases son moldes para crear objetos y una instancia es un objeto creado a partir de una clase

En JS no existen como tal las clases como Java o en C# en este caso JS es un lenguaje de delegacion de objetos.

En JS una **Clase** y un **Constructor** es lo mismo (Una funcion)

## Función Constructora
Las funciones constructoras son funciones comunes y correintes que se utilizan para crear instancias de una clase. Estas tienen que ser llamadas con new antes de su utilización.

```JavaScript
function Person(name){

}
const andrew = new Person("Andrew");
```

Es importante notar que no es posible utilizar arrow functions para hacer funciones constructoras

### New
El operador new lo que hace es retornar el this de la funcion constructora


Existe el operador instanceOf

```JavaScript
function Person(name){

}
const andrew = new Person("Andrew");

console.log(andrew instanceOf Person); //true
```

Ahora se agregaron tambien clases al lenguaje con azucar sintactica:
```JavaScript
class MyClass{
	constructor(name){
	this.name = name;
	}
	greetings(){
		console.log("Hello my name is "+this.name);
	}
}
 
```