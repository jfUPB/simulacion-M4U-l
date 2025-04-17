*enlace p5js:*

https://editor.p5js.org/M4U-l/sketches/QH6LgtTRu

*codigo*

```js
let xspacing = 16;
let w;
let theta = 0.0;
let amplitude = 75.0;
let period = 500.0;
let dx;
let yvalues;

function setup() {
  createCanvas(800, 400);
  w = width + 16;
  dx = (TWO_PI / period) * xspacing;
  yvalues = new Array(floor(w / xspacing));
  noStroke();
}

function draw() {
  // Fondo con cielo suave
  background(135, 206, 235); // sky blue

  calcWave();
  renderWave();

  fill(0);
  textSize(16);
  text("Ola animada con degradado 🌊", 10, height - 10);
}

function calcWave() {
  theta += 0.05;

  let x = theta;
  for (let i = 0; i < yvalues.length; i++) {
    // Suma un poco de ruido para hacerlo más orgánico
    let noiseOffset = map(noise(i * 0.1, frameCount * 0.01), 0, 1, -15, 15);
    yvalues[i] = sin(x) * amplitude + noiseOffset;
    x += dx;
  }
}

function renderWave() {
  for (let x = 0; x < yvalues.length; x++) {
    let xpos = x * xspacing;
    let ypos = height / 2 + yvalues[x];

    // Degradado de color: de blanco a azul
    let inter = map(x, 0, yvalues.length, 0, 1);
    let col = lerpColor(color(255), color(0, 150, 255), inter);
    fill(col);

    // Tamaño variable para profundidad
    let size = map(yvalues[x], -amplitude, amplitude, 8, 20);
    ellipse(xpos, ypos, size, size);
  }
}

```

![](https://github.com/jfUPB/simulacion-M4U-l/blob/main/src/assets/Uni4Act8.png)
