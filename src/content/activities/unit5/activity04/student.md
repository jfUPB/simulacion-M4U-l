### 1. ¿Cómo se gestiona la creación y la desaparición de las partículas y cómo se gestiona la memoria?

Las partículas se crean constantemente dentro del draw() con un control usando frameCount % 5 === 0 para que no se generen todas al mismo tiempo. 

Para la desaparición, cada partícula tiene una variable lifespan que va disminuyendo en cada frame. Cuando este valor llega a cero, se considera que la partícula está “muerta” y la elimino del array con splice(). 

### 2. ¿Cómo se aplica el marco de movimiento motion 101 en los sistemas de partículas que analizaste en la actividad anterior?

Usé el enfoque de Motion 101 aplicando vectores para manejar el movimiento de las partículas. Cada partícula tiene su posición, velocidad y aceleración (pos, vel, acc) y en el update() se aplican las operaciones 

### 3. ¿Cómo se aplican fuerzas externas a los sistemas de partículas que trabajaste en la unidad? ¿Qué fuerzas se aplicaron y cómo están modeladas?

Apliqué varias fuerzas externas las más importantes fueron:

Una especie de gravedad invertida para que las partículas suban (createVector(0, -0.02))

Fuerzas basadas en ruido Perlin para que se muevan de manera orgánica, como si flotaran

Una fuerza de atracción hacia el centro de la pantalla cuando el volumen del micrófono pasa cierto umbral. Esto fue una forma de simbolizar la "unidad" de las almas, y le da un comportamiento interesante en tiempo real según el sonido ambiente.

Todas estas fuerzas las sumo a la aceleración con el método applyForce(), lo que me permite modular el movimiento de cada partícula según lo que está pasando en el entorno


### 4. ¿Cómo se aplicaste los conceptos de herencia y polimorfismo en los sistemas de partículas que trabajaste en la unidad?

Usé herencia creando una clase general Particle, que tiene lo esencial que comparten todas las partículas: posición, velocidad, aceleración, actualización, visualización y verificación de vida útil.

A partir de esa clase, hice dos subclases:

Soul, que representa las almas flotantes, y tiene un estilo más suave y translúcido.

CrossParticle, que representa las cruces rojas al estilo Evangelion. Se comporta de manera distinta y sube lentamente con un diseño en forma de cruz.

Esto es polimorfismo porque ambas clases usan métodos como update() y display(), pero cada una lo hace a su manera. Puedo usarlas de forma intercambiable dentro de arrays sin tener que preocuparme por cuál es cuál, porque cada una sabe cómo comportarse.



