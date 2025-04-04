Simulación 1

1. en la simulación, los elementos gráficos giran en torno a un punto central. La interacción ocurre a través de la rotación de estos elementos alrededor del centro de la pantalla

2. se hace para facilitar las transformaciones, como la rotación. Al mover el origen al centro, las rotaciones se realizan de manera intuitiva alrededor del centro de la pantalla en lugar de alrededor del origen predeterminado 

3. la función rotate() rota el sistema de coordenadas en lugar de los elementos en sí. Cuando se aplica rotate(), todos los objetos dibujados después de la transformación son afectados por esta rotación

4. los elementos se dibujan en (0,0) en el sistema de coordenadas local, pero como el origen ha sido trasladado al centro de la pantalla y el sistema de coordenadas ha sido rotado, los objetos giran alrededor de ese nuevo origen

Simulación 2

1. se está aplicando un modelo básico de movimiento en el que un objeto se mueve en la dirección de un vector de velocidad. Se usa este marco para hacer que los objetos apunten en la dirección del movimiento

2. heading() devuelve el ángulo de dirección de un vector en radianes. En este caso, se usa para obtener la orientación del vector de velocidad y rotar el objeto en esa dirección

3. push() guarda el estado actual del sistema de coordenadas pop() restaura el estado previamente guardado esto permite aplicar transformaciones sin afectar otros elementos en el mismo lienzo.

4. establece el modo de dibujo de rectángulos de manera que su punto de referencia sea su centro, en lugar de la esquina superior izquierda

5. el ángulo de rotación es directamente proporcional a la dirección del vector de velocidad. Al rotar el objeto por el ángulo obtenido de velocity.heading(), se garantiza que el objeto apunte en la dirección en la que se está moviendo
