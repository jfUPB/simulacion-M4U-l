El concepto de Lévy flight se refiere a un tipo de movimiento aleatorio que se caracteriza por pasos de longitud variable, donde la longitud de cada paso sigue una distribución de probabilidad de tipo **Lévy** o Lévy flight, se puede interpretar como quela mayoría de los pasos son cortos, pero ocasionalmente pueden producirse saltos muy largos. Este comportamiento es una mezcla entre un movimiento aleatorio estándar y movimientos más dispersos.



## Aplicaciones en programación

**Optimización y algoritmos evolutivos**: En problemas complejos de optimización, los movimientos tipo Lévy pueden ser útiles para evitar quedar atrapados en óptimos locales. Los saltos largos aleatorios permiten una mejor exploración del espacio de soluciones, favoreciendo la búsqueda global

**Generación de rutas aleatorias**: Si estás trabajando en la creación de rutas o trayectorias aleatorias para algo como videojuegos o sistemas autónomos (drones, robots, etc.), un comportamiento tipo Lévy podría ayudar a generar rutas más naturales o realistas, en comparación con patrones de movimiento más predecibles como el random walk tradicional

```javascript
let x, y; 
let path = []; 
function setup() {
  createCanvas(640, 240);
  x = width / 2;
  y = height / 2;
  background(255);
  setTimeout(captureScreen, 5000);
}

function draw() {
  let stepSize = levyStep();
  
  let angle = random(TWO_PI);
  let dx = cos(angle) * stepSize;
  let dy = sin(angle) * stepSize;

  x += dx;
  y += dy;

  x = constrain(x, 0, width);
  y = constrain(y, 0, height);

  path.push(createVector(x, y));

  noFill();
  stroke(0, 50);
  beginShape();
 
  endShape();

  fill(0);
  noStroke();
  ellipse(x, y, 5, 5);
}

function levyStep() {
  let exponent = 1.2;
  let stepSize = pow(random(), -1 / exponent);
  return stepSize * 10;
}

function captureScreen() {
  saveCanvas('walker_screenshot', 'png'); // Guarda la pantalla como una imagen PNG
}
```

![](https://github.com/jfUPB/simulacion-M4U-l/blob/main/src/assets/Uni1Act6.png)

