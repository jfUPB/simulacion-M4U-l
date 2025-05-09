*Link p5js*

https://editor.p5js.org/M4U-l/sketches/jZsO8ZlT6

*codigo*

```js
let oscillators = [];

function setup() {
  createCanvas(800, 400);
  for (let i = 0; i < 10; i++) {
    oscillators.push(new Oscillator());
  }
}

function draw() {
  background(255);
  for (let osc of oscillators) {
    osc.applyGravity();  // Unidad 3: fuerza
    osc.update();
    osc.display();
  }

  // Título
  noStroke();
  fill(0);
  textSize(16);
  text("Osciladores con aleatoriedad (U1) y gravedad (U3)", 10, height - 10);
}

class Oscillator {
  constructor() {
    this.angle = createVector(0, 0);
    this.velocity = createVector(random(0.01, 0.05), random(0.01, 0.05)); // Unidad 1: aleatoriedad
    this.acceleration = createVector(0, 0);
    this.amplitude = createVector(random(20, 100), random(20, 100)); // Unidad 1: aleatoriedad
    this.gravity = createVector(0, 0.0005); // Unidad 3: fuerza
    this.size = random(10, 20); // Aleatoriedad visual también
  }

  applyGravity() {
    this.acceleration.add(this.gravity);
  }

  update() {
    this.velocity.add(this.acceleration);
    this.angle.add(this.velocity);
    this.acceleration.mult(0);
  }

  display() {
    let x = this.amplitude.x * sin(this.angle.x);
    let y = this.amplitude.y * sin(this.angle.y);

    push();
    translate(width / 2, height / 2);
    stroke(0);
    fill(100, 150, 255, 150);
    ellipse(x, y, this.size, this.size);
    pop();
  }
}

```

![](https://github.com/jfUPB/simulacion-M4U-l/blob/main/src/assets/Uni4Act7.png)
