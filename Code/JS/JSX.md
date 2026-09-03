JSX es una extensión de sintaxis para JavaScript que permite escribir elementos de diferentes frameworks o librerías, esta sintaxis especial de los archivos JSX se parece mucho a la sintaxis de HTML, pues se puede insertar dentro del código, pero con toda la potencia y dinamismo de JavaScript esto hace estructuras muy simples y potentes.

```jsx
function Hola (){
	return <h1>Hola como estas?</h1>
}
```

Aunque parece HTML simple, en realidad es te código es transformado por Babel (Un compilador de JS) este compilador lo que hace seria traducir el código anterior por:
``` jsx
function Hola(){
	return React.createElement("h1", null, "Hola como estas?");
}
```
