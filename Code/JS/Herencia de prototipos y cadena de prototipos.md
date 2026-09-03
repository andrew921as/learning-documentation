NO HAY FORMA DE ESCAPAR DE LOS PROTOTIPOS EN JS
Un prototipo es un delegado, es un algo al que le delejamos algo.
En JS no hay herencia, hay delegacion de objetos, es decir que a medida que un objeto necesita algo va a ir pidiendolo a sus prototipos si no lo encuentra.

## Prototype chain
We always use prototypes in js, and the search of those prototypes, the prototype chain appears

Object.prototype es el padre de todos los objetos y prototipos, en ultimas en JS siempre se va a llegar a ese prototipo


### Ways to use prototypes:

Objetos literales
Object.create(proto)
Funciones constructoras y clases
Object.setPrototypeOf(obj1,obj2)
