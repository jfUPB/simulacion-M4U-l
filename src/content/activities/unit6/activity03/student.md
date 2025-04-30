Reglas del comportamiento
El algoritmo de flocking simula el movimiento colectivo de agentes mediante tres reglas principales: separación, alineación y cohesión. Estas reglas se aplican en cada ciclo del programa para modificar la dirección y velocidad de cada agente con base en su entorno cercano.

Separación tiene como propósito evitar la superposición o hacinamiento. Cada agente calcula un vector de dirección opuesto a la posición de los agentes demasiado cercanos, generando una fuerza que lo aleja.

Alineación busca que el agente se dirija en la misma dirección promedio de sus vecinos. Para esto, se calcula la velocidad media de los agentes dentro del radio de percepción y se genera una fuerza que adapta la dirección del agente hacia esa media.

Cohesión tiene como objetivo mantener al agente dentro del grupo. Se calcula el punto medio entre los vecinos percibidos y se genera un vector de dirección desde la posición del agente hacia ese centro.

Parámetros clave
Los parámetros que controlan el comportamiento de los agentes son:

perceptionRadius: define el área en la que un agente puede detectar a otros como vecinos. Influye directamente en cuántos agentes afectan su comportamiento.

maxspeed: define la velocidad máxima que puede alcanzar un agente.

maxforce: determina la fuerza máxima con la que puede cambiar su dirección.

Pesos relativos de cada regla (por ejemplo, multiplicadores para cohesión, alineación y separación) que permiten ajustar la influencia de cada una en el comportamiento final.

Modificación del código
Se realizó una modificación reduciendo la cohesión a cero y aumentando la separación. Los multiplicadores quedaron definidos de la siguiente manera:

javascript
Copiar
Editar
separation.mult(2.5);
alignment.mult(1.0);
cohesion.mult(0.0);
El efecto de esta modificación fue una dispersión generalizada de los agentes. Como ya no existía atracción hacia el grupo, los agentes tendían a alejarse entre sí, sin formar estructuras compactas. La alineación mantenía cierto orden en la dirección del movimiento, pero el comportamiento colectivo se volvió menos estable. Esto generó un patrón de movimiento más errático y menos agrupado.

Conclusión
El ejercicio permitió observar cómo el comportamiento emergente cambia dependiendo de pequeños ajustes en los parámetros. Aunque mi enfoque profesional está más orientado a lo visual y al 3D, entender estas dinámicas desde la programación ofrece herramientas valiosas para la simulación de multitudes, animación procedural y control de movimiento en entornos interactivos o generativos.
