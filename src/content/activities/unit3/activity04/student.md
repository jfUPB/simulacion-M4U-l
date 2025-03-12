**1. ¿Dónde está el marco motion 101?**

el marco básico para simular movimiento está estructurado a través de la creación de múltiples formas que siguen al ratón. El principio de movimiento se basa en el cálculo de las distancias y las velocidades entre las formas y la posición del ratón, lo que las lleva a moverse hacia él.

Aunque este código no está directamente dentro del marco `motion 101`, sigue la estructura fundamental del mismo, con objetos que se mueven en el lienzo de acuerdo a ciertas reglas de movimiento.


En la unidad anterior, la aceleración generalmente se calculaba usando un vector que apuntaba hacia el ratón, lo que generaba un efecto de "atracción" o "fuerza" hacia el cursor. En este caso, se utilizaba la diferencia entre las coordenadas del ratón y las del objeto para determinar la aceleración. Aquí tienes un ejemplo de cómo se calculaba la aceleración en esa unidad:

```javascript
let dx = mouseX - this.x;
let dy = mouseY - this.y;
let dist = sqrt(dx * dx + dy * dy);

// Calculamos un factor de aceleración, por ejemplo inversamente proporcional a la distancia
let acceleration = dist * 0.01;

let angle = atan2(dy, dx);
this.velocity.x += cos(angle) * acceleration;
this.velocity.y += sin(angle) * acceleration;
```

En este fragmento, la aceleración se calcula en función de la distancia entre el objeto y el ratón, generando un movimiento de atracción hacia el ratón. La aceleración aquí es inversamente proporcional a la distancia


La aceleración calculada en esta unidad tiene todo que ver con las **leyes del movimiento de Newton**, específicamente la **segunda ley**. Según esta ley, la aceleración de un objeto es directamente proporcional a la fuerza neta que actúa sobre él e inversamente proporcional a su masa. Esto se expresa en la fórmula:

\[
F = ma
\]

Donde:
- \(F\) es la **fuerza** neta aplicada sobre el objeto.
- \(m\) es la **masa** del objeto.
- \(a\) es la **aceleración** resultante.


**Código de ejemplo relacionado con las leyes de movimiento de Newton:**


```javascript
update() {
    // Calculamos la aceleración en función de la dirección hacia el mouse
    let dx = mouseX - this.x;
    let dy = mouseY - this.y;
    let dist = sqrt(dx * dx + dy * dy);
    
    // Aquí estamos simulando una "fuerza" hacia el ratón
    let forceMagnitude = 1 / dist; // Cuanto más cerca, más fuerte la "fuerza"
    let ax = (dx / dist) * forceMagnitude; // Aceleración en X
    let ay = (dy / dist) * forceMagnitude; // Aceleración en Y

    this.acceleration.set(ax, ay); // Establecemos la aceleración

    // Ahora calculamos la velocidad sumando la aceleración
    this.velocity.add(this.acceleration);
    this.velocity.limit(this.topSpeed); // Limitar la velocidad máxima

    // Finalmente, actualizamos la posición
    this.position.add(this.velocity);
}
```

En este código, la aceleración se calcula de acuerdo con la distancia al ratón, generando una fuerza que afecta directamente la aceleración del objeto, y esta aceleración finalmente cambia la velocidad y la posición, siguiendo la lógica de las leyes de Newton.

**Conclusión:**
En resumen, esta unidad se basa en el cálculo de la aceleración a partir de la "fuerza" simulada por la atracción hacia el ratón. Aunque el código no hace uso explícito de masa, el concepto subyacente sigue las leyes de Newton, donde la fuerza produce una aceleración que cambia el movimiento del objeto en el lienzo.
