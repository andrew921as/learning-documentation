La coerción de tipos se refiere a la conversión implícita de tipos que realiza el moto de JavaScript para poder concretar una operación.

Esto quiere decir, que al hacer operaciones entre tipos de datos distintos, el resultado dependera de como se transformen los tipos de datos para poder dar un resultado.

``` JavaScript
console.log(2+3);
//5
console.log("Ho"+"la")
// "Hola"
console.log("4"+"5")
//"45"
console.log(2-3);
//-1
console.log("Ho"-"la")
//NaN
console.log("4"-"5")
//-1
console.log(4-"5")
//-1
console.log(5*5);
//25
console.log(5*"5");
//25
```

Esto toca tomarlo en cuenta a la hora de trabajar con datos en JS, pudiendo traer errores y comportamientos extraños dentro del programa