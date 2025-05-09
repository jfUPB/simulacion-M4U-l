https://editor.p5js.org/M4U-l/sketches/1MFJsAohA

```js
let particles = [];
let flowfield;
let cols, rows;
let inc = 0.1;
let scl = 20;
let zoff = 0;
let mic, vol;

function setup() {
  createCanvas(600, 600);
  colorMode(HSB, 360, 255, 255, 255);

  mic = new p5.AudioIn();
  mic.start();

  cols = floor(width / scl);
  rows = floor(height / scl);
  flowfield = new Array(cols * rows);

  for (let i = 0; i < 1000; i++) {
    particles[i] = new Particle();
  }

  background(0);
}

function draw() {
  background(0, 0.05); // un poquito de transparencia para trazo más suave

  vol = mic.getLevel(); // Obtener volumen actual del micro

  let yoff = 0;
  for (let y = 0; y < rows; y++) {
    let xoff = 0;
    for (let x = 0; x < cols; x++) {
      let index = x + y * cols;
      let angle = noise(xoff, yoff, zoff) * TWO_PI * 4;
      let v = p5.Vector.fromAngle(angle);
      v.setMag(1);
      flowfield[index] = v;
      xoff += inc;
    }
    yoff += inc;
  }
  zoff += 0.003;

  for (let i = 0; i < particles.length; i++) {
    particles[i].follow(flowfield, vol);
    particles[i].update(vol);
    particles[i].edges();
    particles[i].show(vol);
  }
}

class Particle {
  constructor() {
    this.pos = createVector(random(width), random(height));
    this.vel = createVector(0, 0);
    this.acc = createVector(0, 0);
    this.maxSpeed = 2;
    this.prevPos = this.pos.copy();
    this.hue = random(360);
  }

  applyForce(force) {
    this.acc.add(force);
  }

  follow(vectors, volume) {
    let x = floor(this.pos.x / scl);
    let y = floor(this.pos.y / scl);
    let index = x + y * cols;
    let force = vectors[index];
    this.applyForce(force);

    // Interacción con el mouse y sonido
    let mouse = createVector(mouseX, mouseY);
    let dir = p5.Vector.sub(mouse, this.pos);
    let d = dir.mag();
    if (d < 100) {
      dir.setMag(map(d, 0, 100, 0.5 + volume * 20, 0)); // Aumenta fuerza con sonido
      this.applyForce(dir);
    }
  }

  update(volume) {
    let speedBoost = map(volume, 0, 1, 1, 5); // velocidad según volumen
    this.vel.add(this.acc);
    this.vel.limit(this.maxSpeed * speedBoost);
    this.pos.add(this.vel);
    this.acc.mult(0);
  }

  show(volume) {
    stroke(this.hue, 255, 255, map(volume, 0, 1, 20, 255));
    strokeWeight(map(volume, 0, 1, 0.5, 2));
    line(this.pos.x, this.pos.y, this.prevPos.x, this.prevPos.y);
    this.updatePrev();
  }

  updatePrev() {
    this.prevPos.x = this.pos.x;
    this.prevPos.y = this.pos.y;
  }

  edges() {
    if (this.pos.x > width) {
      this.pos.x = 0;
      this.updatePrev();
    }
    if (this.pos.x < 0) {
      this.pos.x = width;
      this.updatePrev();
    }
    if (this.pos.y > height) {
      this.pos.y = 0;
      this.updatePrev();
    }
    if (this.pos.y < 0) {
      this.pos.y = height;
      this.updatePrev();
    }
  }
}

```


![](https://github.com/jfUPB/simulacion-M4U-l/blob/main/src/assets/Uni4Act11.png)
