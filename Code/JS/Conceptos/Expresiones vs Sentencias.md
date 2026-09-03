# Expresión
Unidad de código que **produce un valor**. Además, algunas expresiones pueden tener efectos seccundarios.
```JavaScript
10+10
20
```
### Expresión Primaria
Cualquier palabra pequeña que produsca un valor:

- Un valor primitivo
- La palabra reservada this
- Asignar una variable a otra variable
### Expresión de Función
En JS podemos definir un valor como una función. Cuando se escribe una función en un lugar del código donde se espera un valor.
```JavaScript
numeros 0 [1,4,5,6,2,6,7]
numeros.filter(fucntion filtrar(numero){
return numero%2 === 0
});
//No es necesario darle nombre a la funcion cuando es pasada como valor
numeros.filter(numero => numero%2=== 0);
```

### Invocación de una función
Las invocaciones de una funcion tambien son tomadas como Expresiones, dado que estas suelen devolver un valor

### Expresión de los operadores
Como en el primer ejemplo, los operadores son una forma muy comun de generar expresiónes inclusive el operador de asignacion
# Sentencia
Es una **acción** que JavaScript ejecuta para que ocurra algo, para que avance la lógica del programa, no necesariamente para que retorne el valor

### Sentencia de expresion
Sirve para evaluar una expresion, esto busca que se produsca el efecto secundario que tiene
```JavaScript
let counter = 1;
counter++
//El aumentar en 1 el contador es una sentencia de expresion, que busca aumentar el valor de counter, en este caso esta no retorna ningun valor, y lo unico que busca es cambiar el valor de la variable
```

### Sentencia vacia
Existe una sentencia vacia ; esta sentencia no suele ser comun pero se puede utilizar.

### Sentencia de bloque
Las sentencias de bloque, esta se utiliza para poder decir que bloque de codigo pertenece a que sentencia, {}.

### Sentencia de declaración
Se pueden crear varias variables en una sola linea o en varias lineas.
``` JavaScript
let una, variable, otra, declarada;
```
### Sentencia de Funcion
Sirve para **crear una funión** con el nombre y los parametros indicadoes, Dentros del scope donde se encuentra esa sentencia

### Sentencias de control
Podemos **alterar el flujo nomal de ejecución**. Podemos decidir que flujo va a seguir la ejecución de nuestro programa.

- El If
- El Switch
- Los diferentes For
- El While
- El Do While
- El break con un ciclo
- El continue con un ciclo
- El return
- El throw
- El try/catch/finally
### Sentencias miselaneas
Estas no tienen otra categoria, son sentencias sueltas que tienen funcionalidades por si mismas, pero no son suficientes como para tener su propia sección.
- **Debugger** El programa al pasar por esta sentencia se detendra y mostrara diferente información del programa
- '**use strict**' Esta sentencia permite ejecutar codigo con el modo estricto, sirve para ver mas errores por la consola y se pueden arreglar de forma prematura.