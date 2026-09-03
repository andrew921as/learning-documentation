Event driver architecture: 
Es lo que le permite a Nodejs realizar operacioens de E/S no bloqueantes. El kernel es el que se encarga de notificar a NodeJs las operaciones requeridas.

## No es:
El EventLoop esta dentro de NodeJs. pero en realidad forma parte de la libreria loopui

Node.js no es el mismo que el Browser (Node no maneja webapi)

No es un vigilante que mira las tareas y las ejecuta

## Si es
El va ejecutando fases en orden y cada fase tiene una logica para ejecutar los callbacks. El ejecuta los callbacks de esa cola, pero estos tienen un limite.

Las micro tasks se ejecutan cuando de complete la operacion actual

Hace uso del Call Stack para ver las tareas e irlas sacando