Estructura del campo de flujo
El campo de flujo está implementado como un arreglo unidimensional que simula una cuadrícula 2D de vectores. Cada celda de la cuadrícula almacena un p5.Vector que representa una dirección que los agentes seguirán. Estos vectores se generan usando Perlin noise, lo que permite crear una continuidad espacial en las direcciones. Aunque se ve como 2D, se accede al arreglo mediante la fórmula index = x + y * cols.

Comportamiento del agente
En la clase del agente (Vehicle), hay una función llamada follow() que le permite seguir el flujo. El agente toma su posición actual y la traduce a coordenadas de la cuadrícula dividiendo entre la resolución. Luego obtiene el vector del campo en esa celda y lo utiliza para calcular una fuerza deseada. Esta fuerza se compara con la velocidad actual del agente para generar una fuerza de dirección (steering). Finalmente, se limita esta fuerza para que no sea demasiado abrupta y se aplica como fuerza externa al movimiento del agente.

Parámetros clave
Los principales parámetros que controlan el comportamiento del sistema son:

resolution: define el tamaño de las celdas en la cuadrícula del campo.

maxspeed: velocidad máxima que puede alcanzar un agente.

maxforce: fuerza máxima que se puede aplicar a un agente para cambiar su dirección.

Modificación realizada
Reemplacé la fórmula basada en Perlin noise por una fórmula trigonométrica más estructurada:

javascript
Copiar
Editar
let angle = sin(xoff * 3) * cos(yoff * 3) * TWO_PI;
let v = p5.Vector.fromAngle(angle);
v.setMag(1);
field[index] = v;
Esto cambió por completo el comportamiento del sistema. En vez de tener un movimiento orgánico parecido al viento, los agentes seguían patrones repetitivos y más rígidos. El movimiento se volvió más geométrico, lo cual puede ser útil si se busca un efecto más visualmente controlado y menos aleatorio.

Conclusión
Aunque mi enfoque profesional es más hacia el arte 3D, este ejercicio me ayudó a entender cómo se puede usar un sistema basado en vectores para controlar movimiento de manera fluida. Veo un potencial claro para aplicarlo en animaciones, simulaciones o como base para efectos visuales en tiempo real. Además, me ayudó a entender mejor cómo modelar comportamientos emergentes a partir de reglas simples.
