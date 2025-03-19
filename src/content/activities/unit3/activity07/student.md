
### El Problema:

El problema principal es que, cuando modificamos force dentro de applyForce, este cambio se refleja fuera de la función, ya que el objeto force fue pasado por referencia. Así que la próxima vez que pases el mismo objeto force a applyForce, ya no tendrá el valor que esperamos. 

```javascript
applyForce(force) {
    let f = force.copy();   // Hacemos una copia del vector de fuerza
    f.div(10);               // Dividimos la copia entre la masa (10)
    this.acceleration.add(f); // Sumamos la copia a la aceleración
}
```

En JavaScript, los tipos primitivos como number, boolean, etc. se pasan por valor, lo que significa que cualquier cambio en el parámetro dentro de la función no afecta a la variable original. Sin embargo, los objetos y arrays se pasan por referencia, lo que implica que si modificamos un objeto dentro de una función, también modificamos el objeto original fuera de la función.
