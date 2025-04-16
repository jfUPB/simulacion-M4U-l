### ¿Qué concepto de oscilación utilizaste como base para tu obra? Describe cómo lo implementaste.

Utilicé el concepto de oscilación armónica suave, modelado mediante el uso de ruido Perlin aplicado sobre un campo vectorial. Este ruido genera direcciones que cambian lentamente con el tiempo, simulando un movimiento ondulante, similar al de un fluido o viento suave.
En el código, la función noise(x, y, z) genera un ángulo que luego se convierte en un vector direccional, y las partículas lo siguen. La oscilación se ve reflejada en cómo estos vectores cambian constantemente de dirección de manera fluida y natural. Además, con cada frame el valor zoff se incrementa ligeramente, lo que permite que el campo evolucione en el tiempo

### ¿Cómo funciona la interacción en tu obra? Explica cómo el usuario puede modificar la obra en tiempo real.

Con el mouse:

Cuando el usuario mueve el mouse, este actúa como un centro de atracción para las partículas cercanas.

Las partículas que están dentro de un rango cercano al cursor son atraídas hacia él, alterando su trayectoria y generando remolinos de movimiento en tiempo real.

Con el micrófono (sonido del entorno o música):

El volumen detectado modifica dinámicamente la velocidad, color y grosor del trazo de las partículas.

Si hay música fuerte, las partículas se aceleran y los trazos se hacen más intensos.

El efecto es una visualización emocional del sonido, como si el jardín respondiera al ambiente.

### ¿Qué desafíos encontraste durante el proceso de creación? ¿Cómo los superaste?

Captura de audio en tiempo real:
Al principio fue complicado hacer que el micrófono funcionara correctamente en p5.js. Lo solucioné usando p5.AudioIn() y asegurándome de que el usuario dé permiso al navegador para usar el micrófono.

Mantener el movimiento suave:
Con muchos elementos en pantalla, las partículas podían sobrecargar el renderizado. Ajusté el número de partículas, su velocidad y utilicé un fondo transparente parcial (background(0, 0.05)) para evitar borrar constantemente la pantalla y mejorar el rendimiento visual.

Interacción sutil pero perceptible:
Quería que tanto el mouse como el sonido influyeran sin dominar la escena. Hice muchos ajustes de escala con map() y probé distintas intensidades para encontrar un equilibrio armónico.


### ¿Qué aprendiste sobre las oscilaciones y su aplicación en el arte generativo?


Aprendí que las oscilaciones no solo se aplican a objetos físicos como péndulos o resortes, sino que también pueden modelar movimientos orgánicos, fluidos y naturales en medios digitales. El uso de ruido Perlin como una forma de oscilación compleja permite generar sistemas visuales hermosos y suaves que imitan patrones de la naturaleza.
