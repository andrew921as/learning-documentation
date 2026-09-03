El scope son los entornos y le dan significado a las variables y depende desde donde y como se crean las variables. **Es el contexto actual de ejecucion** (Entorno de ejecución) [[Contexto y Contexto de ejecución]]. Es el contexto en que los valores y las expresiones son "Visibles", o pueden ser referenciados

### Scope de Función
Estas son las variables que son creadas desde una funcion y solo pueden ser accedidas desde esa funcion y no se pueden utilizar desde afuera (Incluyendo los parametros)

**VAR** Las variables definidas con *var* siempre van a tener un scope de funcion
### Scope de Bloque
En JS todo **Bloque** es aquel parte de codigo que esta encerrada entre llaves ({}) 
EJ:
- if(){}
- for(){}
- while(){}
Las variables declaradas con *let* y *const* tienen scope de bloque

Si modifico el valor de una variable que no existe, JS la va a crear en el contexto global
