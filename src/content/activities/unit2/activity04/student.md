El método **mag()** se utiliza para calcular la longitud de un vector en el espacio 2D. se calcula utilizando el teorema de Pitágoras
Este valor representa la "distancia" desde el origen (0, 0) hasta el punto \((x, y)\)

Por otro lado, el método magSq() calcula la magnitud del vector al cuadrado

### Diferencia entre mag() y magSq():
- **mag()** devuelve la magnitud del vector (la longitud real)
- **magSq()** devuelve la magnitud al cuadrado, que es útil cuando solo te interesa comparar magnitudes o realizar operaciones que no requieren la raíz cuadrada

### ¿Cuál es más eficiente?
El método **magSq()** es más eficiente que mag() porque no necesita calcular la raíz cuadrada. Si solo necesitas comparar las magnitudes de diferentes vectores o hacer cálculos donde la raíz cuadrada no sea necesaria, es mejor usar magSq() porque evita un cálculo adicional 


### ¿Para qué sirve el método normalize()?
El método **normalize()** convierte un vector en un **vector unitario**, es decir, lo escala para que su magnitud sea 1, manteniendo su dirección. Esto es útil cuando solo se necesita la dirección de un vector sin preocuparse por su longitud

### ¿Qué le responderías al periodista sobre el método dot()?
Le diría: El método dot() calcula cuánto se alinean dos vectores, midiendo la "proyección" de uno sobre el otro. Si el valor es alto, los vectores están muy alineados; si es 0, son perpendiculares

### Diferencia entre la versión estática y la de instancia de dot():
- Versión de instancia (v1.dot(v2)): Se llama sobre un vector (v1) y toma como parámetro otro vector (v2), y calcula el producto punto entre ambos.
- Versión estática (p5.Vector.dot(v1, v2)): Se llama directamente a la clase p5.Vector y también toma dos vectores (v1, v2) como parámetros. Es equivalente a usar la versión de instancia

###¿Cuál es la interpretación geométrica del producto cruz de dos vectores?

el producto cruz mide la "cantidad" de diferencia entre los dos vectores a través de su magnitud, sino que también nos da un vector que pertenece a un plano perpendicular a los vectores originales


###¿Para que te puede servir el método dist()?

El método **dist()** se utiliza para calcular la distancia entre dos puntos en el espacio, que están representados por vectores


### ¿Para qué sirven el métodos  limit()?

- **limit()**: Este método limita la magnitud de un vector a un valor máximo especificado. Si la magnitud del vector es mayor que el límite, se escala para que su longitud sea igual al valor máximo. Si la magnitud ya está por debajo del límite, no cambia
