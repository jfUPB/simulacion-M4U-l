### 1. ejemplo 4.2: an Array of Particles.

## codigo

```js
let particles = [];
let noiseScale = 0.01;
let mode = 0; // Cambiará con las teclas

function setup() {
  createCanvas(800, 600);
  background(0);
}

function draw() {
  // Fondo con transparencia para dejar trazas (efecto fractal)
  fill(0, 20);
  rect(0, 0, width, height);

  // Agregamos partículas constantemente desde el centro
  particles.push(new FractalParticle(width / 2, height / 2));

  for (let i = particles.length - 1; i >= 0; i--) {
    let p = particles[i];
    p.update();
    p.display();
    if (p.isDead()) {
      particles.splice(i, 1);
    }
  }
}

function keyPressed() {
  if (key === '1') mode = 0;
  if (key === '2') mode = 1;
  if (key === '3') mode = 2;
}

// Fractal-like particle using Perlin noise
class FractalParticle {
  constructor(x, y) {
    this.pos = createVector(x, y);
    this.vel = createVector(0, 0);
    this.acc = createVector(0, 0);
    this.lifespan = 255;
    this.noiseOffset = random(1000);
  }

  update() {
    // Movimiento guiado por Perlin noise
    let angle;
    let n;

    switch (mode) {
      case 0:
        n = noise(this.pos.x * noiseScale, this.pos.y * noiseScale);
        angle = n * TWO_PI * 2;
        break;
      case 1:
        n = noise(this.noiseOffset, frameCount * 0.01);
        angle = n * TWO_PI * 4;
        break;
      case 2:
        n = noise(this.pos.x * noiseScale, this.pos.y * noiseScale, frameCount * 0.01);
        angle = n * TWO_PI * 6;
        break;
    }

    let dir = p5.Vector.fromAngle(angle);
    this.acc = dir.mult(0.3);
    this.vel.add(this.acc);
    this.vel.limit(2);
    this.pos.add(this.vel);

    this.lifespan -= 2;
    this.noiseOffset += 0.01;
  }

  display() {
    stroke(255, this.lifespan);
    strokeWeight(1.5);
    point(this.pos.x, this.pos.y);
  }

  isDead() {
    return this.lifespan < 0;
  }
}
```

## Concepto

A cada partícula se le da un ciclo de vida: nace, se mueve, envejece y desaparece, se aplica el principio de programación orientada a objetos: cada partícula es una instancia independiente con sus propios datos y métodos, al eliminar partículas muertas del array, se evita que la memoria siga ocupada por objetos que ya no se usan.

## Gestion de particulas y memoria

La memoria se gestiona eliminando manualmente las partículas que ya no se usan (splice()), de esta forma evitamos que el array particles[] crezca infinitamente, lo cual previene fugas de memoria y mantiene el programa optimizado.
