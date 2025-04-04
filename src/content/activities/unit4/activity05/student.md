Primera modificación:

En este caso, se usa p5.Vector.fromAngle(theta), que crea un vector unitario con un ángulo theta. Esto significa que el radio r no se está teniendo en cuenta, por lo que el punto se moverá siempre sobre un círculo de radio 1. Además, hay un error en el código porque la línea sigue usando las variables x e y, que no han sido definidas en esta versión.

Segunda modificación:

Ahora, la función p5.Vector.fromAngle(theta, r) está generando un vector con ángulo theta y magnitud r. Esto hace que el punto se desplace en una circunferencia de radio r, reproduciendo el mismo comportamiento que la primera versión del código, pero utilizando un vector en lugar de cálculos separados para x e y.

Este método es más conveniente cuando se trabaja con p5.js, ya que permite manejar direcciones y magnitudes de manera más intuitiva mediante vectores.
