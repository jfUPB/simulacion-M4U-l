**1. ¿Qué resultado esperas obtener?**

Cuando ejecutas el código, lo que espero es que el vector "posicion" sea modificado por la función "playingVector()". Esto debería cambiar los valores de "posicion" de (6, 9) a (20, 30). Posteriormente, se debería imprimir en la consola el mensaje "Only once" 


**2. ¿Qué resultado obtuviste?**

El código  "Only once" una sola vez en la consola. El vector "posicion" es modificado dentro de la función "playingVector()", pero no se muestra en la consola porque el código no contiene ningún "console.log()" para imprimir el valor de "posicion"


**3. Paso por valor y paso por referencia**

En JavaScript, existen dos formas principales de pasar datos a las funciones:

- **Paso por valor**: Si se pasa un valor primitivo (como un número, string, booleano), se pasa una copia del valor. Cambiar la copia no afecta al valor original


- **Paso por referencia**: Si se pasa un objeto o un array, se pasa una referencia al mismo objeto en memoria. Esto significa que si modificamos el objeto dentro de la función, el objeto original se ve afectado.


**4. ¿Qué tipo de paso se está realizando en el código?**

En el código, se está utilizando **paso por referencia**. Estás pasando un vector p5.Vector a la función "playingVector()", que es un objeto en memoria. Como los objetos se pasan por referencia en JavaScript, cualquier cambio que realices dentro de la función (en este caso, cambiar las coordenadas x y del vector) afectará directamente al objeto 

**5. ¿Qué aprendiste?**

Este código ilustra cómo funciona el paso por referencia en JavaScript cuando trabajamos con objetos. Lo que aprendo de este experimento es que al modificar el valor de un objeto dentro de una función, los cambios persisten fuera de la función, ya que estamos trabajando con la referencia al objeto original, no con una copia del mismo
