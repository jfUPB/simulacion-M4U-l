## enlace p5js

https://editor.p5js.org/M4U-l/sketches/ehtO0wyC9

## codigo

```js
let souls = [];
let crosses = [];
let mic;
let showCrosses = false;

function setup() {
  createCanvas(800, 600);
  mic = new p5.AudioIn();
  mic.start();
}

function draw() {
  background(10, 10, 30, 100); 
  let vol = mic.getLevel();


  if (frameCount % 5 === 0) {
    souls.push(new Soul(createVector(random(width), height + 10)));
  }

  for (let i = souls.length - 1; i >= 0; i--) {
    let s = souls[i];
    s.applyBehaviors(vol);
    s.update();
    s.display();

    if (s.isDead()) {
      souls.splice(i, 1);
    }
  }

  if (showCrosses) {
    for (let i = crosses.length - 1; i >= 0; i--) {
      let c = crosses[i];
      c.update();
      c.display();
      if (c.isDead()) {
        crosses.splice(i, 1);
      }
    }
  }
}

function keyPressed() {

  showCrosses = true;
  crosses = [];

  for (let s of souls) {
    crosses.push(new CrossParticle(s.pos.copy()));
  }
}

class Particle {
  constructor(pos) {
    this.pos = pos.copy();
    this.vel = createVector(0, 0);
    this.acc = createVector(0, 0);
    this.lifespan = 255;
  }

  applyForce(f) {
    this.acc.add(f);
  }

  update() {
    this.vel.add(this.acc);
    this.pos.add(this.vel);
    this.acc.mult(0);
    this.lifespan -= 1;
  }

  isDead() {
    return this.lifespan < 0;
  }

  display() {
    noStroke();
    fill(255, this.lifespan);
    ellipse(this.pos.x, this.pos.y, 10);
  }
}

class Soul extends Particle {
  constructor(pos) {
    super(pos);
    this.size = random(4, 8);
  }

  applyBehaviors(vol) {
    
    this.applyForce(createVector(0, -0.02));
    let n = noise(this.pos.x * 0.01, this.pos.y * 0.01);
    let angle = map(n, 0, 1, -PI / 4, PI / 4);
    let dir = p5.Vector.fromAngle(angle);
    dir.mult(0.05);
    this.applyForce(dir);
 
    if (vol > 0.1) {
      let center = createVector(width / 2, height / 2);
      let force = p5.Vector.sub(center, this.pos);
      force.setMag(0.1);
      this.applyForce(force);
    }
  }

  display() {
    noStroke();
    fill(200, 100, 255, this.lifespan);
    ellipse(this.pos.x, this.pos.y, this.size);
  }
}


class CrossParticle extends Particle {
  constructor(pos) {
    super(pos);
    this.lifespan = 100;
  }

  update() {
    super.update();
    this.pos.y -= 0.3; 
  }

  display() {
    stroke(255, 100, 100, this.lifespan);
    strokeWeight(2);
    // línea vertical
    line(this.pos.x, this.pos.y - 10, this.pos.x, this.pos.y + 10);
    // línea horizontal
    line(this.pos.x - 6, this.pos.y, this.pos.x + 6, this.pos.y);
  }
}

```

## conceptos

Unidad 1: Vectores y Movimiento

Uso de p5.Vector para definir posición, velocidad, aceleración de las almas flotantes movimiento fluido y natural simula almas en suspensión.

Unidad 2: Fuerzas

Al detectar un volumen alto del micrófono o una pulsación de tecla, las partículas reciben una fuerza hacia el centro, como si fuesen absorbidas por un campo global de conciencia.

Unidad 3: Sistemas de partículas
Se implementa una clase Soul (subclase de Particle) con propiedades visuales y de vida cada partícula se elimina de la memoria tras cierto tiempo (lifespan) un arreglo souls[] contiene y gestiona todas las instancias.

Herencia y Polimorfismo
Clase base Particle y subclases como Soul y CrossParticle display() y update() se comportan diferente en cada subclase para representar partículas y cruces de forma polimórfica.

![](https://github.com/jfUPB/simulacion-M4U-l/blob/main/src/assets/Uni5Act3.png)
