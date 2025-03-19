## Paso por valor:

Cuando se pasa una copia de un valor a una variable, se está trabajando con una copia independiente del valor original. Es decir, si modificamos esa copia, el valor original no se ve afectado. 

### Paso por referencia:

En el caso de los objetos como arrays, funciones, etc., pasar por referencia significa que, en lugar de copiar el objeto, pasamos la dirección de memoria donde está almacenado el objeto. Esto quiere decir que si modificamos la variable que contiene la referencia, estamos modificando el objeto original, no una copia.

---

#### Diferencia en el código:

```js
let friction = this.velocity.copy();
let friction = this.velocity;
```

Primera línea: let friction = this.velocity.copy();

Aquí this.velocity.copy() crea una copia del objeto this.velocity. El método .copy() devuelve una nueva instancia de un vector con los mismos valores que this.velocity, pero es independiente de él.
   
Esto es paso por valor porque estamos trabajando con una copia del vector, no con el vector original.

Segunda línea: let friction = this.velocity;

En esta línea, simplemente estamos asignando this.velocity a friction. Esto no crea una copia del vector, más bien friction y this.velocity apuntan al mismo objeto en memoria.
   



### ¿Qué podría salir mal con let friction = this.velocity;?

El principal problema con esta asignación es que cualquier cambio que realicemos sobre friction afectará directamente a this.velocity. Esto puede ser un comportamiento no deseado si esperas que frictio` sea una copia independiente de this.velocity. 
