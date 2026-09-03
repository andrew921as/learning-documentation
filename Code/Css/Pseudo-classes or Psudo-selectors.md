son keywors añadidas a un selector que permiten añadir un estilo al componente dependiendo del estado del elemento (o elementos) seleccionado. 
```css
button:hover{
	color:blue;
}
```
Las pseudo-clases no solo permiten aplicar estilos dependiendo del contenido de los elemntos en el arbol del documento, tambien puede tener encuenta factores externos como el historial del navegador (`:visited`) o el estado de su contenido (`:checked` para algunos elementos de un formularo) o la posicion del mouse (`:hover`)

## Elemental pseudo-classes
Estas se basan en la identidad principal de los elementos
`:defined` Este selecciona cualqiuer elemento que este definido