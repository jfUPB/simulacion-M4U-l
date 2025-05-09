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

## link p5js

https://editor.p5js.org/M4U-l/sketches/T18hl1Pyl

## imagen

![](https://github.com/jfUPB/simulacion-M4U-l/blob/main/src/assets/Uni5Act2Img1.png)



### 2. ejemplo 4.4: a System of Systems.

## Codigo

```js
let systems = [];

function setup() {
  createCanvas(640, 240);
}

function draw() {
  background(255);

  // Ejecutar todos los sistemas de partículas
  for (let i = 0; i < systems.length; i++) {
    systems[i].addParticle();
    systems[i].run();
  }
}

// Crear un nuevo sistema en la posición del mouse
function mousePressed() {
  systems.push(new ParticleSystem(createVector(mouseX, mouseY)));
}

// Clase para manejar un sistema de partículas
class ParticleSystem {
  constructor(position) {
    this.origin = position.copy();
    this.particles = [];
  }

  addParticle() {
    this.particles.push(new Particle(this.origin.x, this.origin.y));
  }

  run() {
    for (let i = this.particles.length - 1; i >= 0; i--) {
      let p = this.particles[i];
      p.attractToMouse();
      p.run();
      if (p.isDead()) {
        this.particles.splice(i, 1);
      }
    }
  }
}

// Partícula individual con atracción al mouse
class Particle {
  constructor(x, y) {
    this.pos = createVector(x, y);
    this.vel = createVector(random(-1, 1), random(-1, 0));
    this.acc = createVector(0, 0);
    this.lifespan = 255;
  }

  applyForce(force) {
    this.acc.add(force);
  }

  attractToMouse() {
    let mouse = createVector(mouseX, mouseY);
    let dir = p5.Vector.sub(mouse, this.pos);
    dir.normalize();
    dir.mult(0.1); // Ajusta la fuerza de atracción
    this.applyForce(dir);
  }

  update() {
    this.vel.add(this.acc);
    this.pos.add(this.vel);
    this.acc.mult(0);
    this.lifespan -= 2;
  }

  display() {
    stroke(0, this.lifespan);
    fill(127, this.lifespan);
    ellipse(this.pos.x, this.pos.y, 8, 8);
  }

  run() {
    this.update();
    this.display();
  }

  isDead() {
    return this.lifespan < 0;
  }
}

```

## Concepto

OOP, ciclo de vida, limpieza de arrays

## Gestion de particulas y memoria

Arrays dinámicos + limpieza manual	Para mantener el rendimiento óptimo
splice() si lifespan < 0	Para evitar saturación de memoria

## link p5js

https://editor.p5js.org/M4U-l/sketches/JNWf_92W4

## imagen

![](https://github.com/jfUPB/simulacion-M4U-l/blob/main/src/assets/Uni5Act2Img2.png)


### 3. ejemplo 4.5: a Particle System with Inheritance and Polymorphism.

## Codigo

```js
let systems = [];

function setup() {
  createCanvas(640, 360);
  systems.push(new ParticleSystem(createVector(width / 2, 50)));
}

function draw() {
  background(255);

  for (let ps of systems) {
    ps.addParticle();
    ps.applyMutualAttraction();
    ps.run();
  }
}

// Agrega un nuevo sistema de partículas donde el usuario haga clic
function mousePressed() {
  systems.push(new ParticleSystem(createVector(mouseX, mouseY)));
}

// Sistema de partículas (emisor)
class ParticleSystem {
  constructor(position) {
    this.origin = position.copy();
    this.particles = [];
  }

  addParticle() {
    this.particles.push(new Particle(this.origin.x, this.origin.y));
  }

  applyMutualAttraction() {
    for (let i = 0; i < this.particles.length; i++) {
      for (let j = 0; j < this.particles.length; j++) {
        if (i !== j) {
          let force = this.particles[j].attract(this.particles[i]);
          this.particles[i].applyForce(force);
        }
      }
    }
  }

  run() {
    for (let i = this.particles.length - 1; i >= 0; i--) {
      let p = this.particles[i];
      p.update();
      p.display();
      if (p.isDead()) {
        this.particles.splice(i, 1);
      }
    }
  }
}

// Partícula individual
class Particle {
  constructor(x, y) {
    this.pos = createVector(x, y);
    this.vel = p5.Vector.random2D().mult(random(0.5, 2));
    this.acc = createVector(0, 0);
    this.mass = random(1, 3); // Masa aleatoria
    this.lifespan = 255;
  }

  applyForce(force) {
    let f = p5.Vector.div(force, this.mass);
    this.acc.add(f);
  }

  attract(other) {
    let G = 0.4;
    let force = p5.Vector.sub(this.pos, other.pos);
    let distance = constrain(force.mag(), 5, 25);
    force.normalize();
    let strength = (G * this.mass * other.mass) / (distance * distance);
    force.mult(strength);
    return force;
  }

  update() {
    this.vel.add(this.acc);
    this.pos.add(this.vel);
    this.acc.mult(0);
    this.lifespan -= 2;
  }

  display() {
    stroke(0, this.lifespan);
    fill(127, this.lifespan);
    ellipse(this.pos.x, this.pos.y, this.mass * 6, this.mass * 6);
  }

  isDead() {
    return this.lifespan < 0;
  }
}

```

## Concepto

Atracción gravitacional	attract() entre partículas con masas	Para hacer que las partículas interactúen de manera más orgánica.

## Gestion de particulas y memoria

No se usan estructuras globales innecesarias, cada ParticleSystem maneja su propio array de partículas (this.particles), las partículas muertas se eliminan con splice() para liberar memoria.

## link p5js

https://editor.p5js.org/M4U-l/sketches/BCwRkX7F0

## imagen

![](https://github.com/jfUPB/simulacion-M4U-l/blob/main/src/assets/Uni5Act2Img3.png)

### 4. ejemplo 4.6: a Particle System with Forces.

## Codigo

```js

![image](https://github.com/user-attachments/assets/7d7718a4-05b8-4fc3-9a0d-6ebb4bb52dbd)

```

## Concepto

Resorte: fuerza que intenta devolver la partícula a su punto de origen.

Velocidad angular: para que la cuerda tenga un movimiento oscilante natural.

Visualización de la cuerda: dibujar una línea desde la partícula hasta su posición inicial.

## Gestion de particulas y memoria

Creación de Partículas en el Emisor:

Se utiliza la clase Emitter, que actúa como emisor de partículas, ubicando las partículas en un punto de origen, que en este caso está en el centro del canvas.

Cada vez que se ejecuta el método addParticle(), se crea una nueva partícula y se agrega al array this.particles, Este paso garantiza que no se acumulen partículas que ya no existen visualmente o en términos de comportamiento, evitando sobrecargar la memoria.

## link p5js

https://editor.p5js.org/M4U-l/sketches/YgzwvAr8e

## imagen

![](https://github.com/jfUPB/simulacion-M4U-l/blob/main/src/assets/Uni5Act2Img4.png)


### 5. ejemplo 4.7: a Particle System with a Repeller.

## Codigo

```js
let emitter;
let repeller;

function setup() {
  createCanvas(640, 240);
  emitter = new Emitter(width / 2, 60);
  repeller = new Repeller(mouseX, mouseY); // Posición inicial
}

function draw() {
  background(255);
  emitter.addParticle();

  let gravity = createVector(0, 0.1);
  emitter.applyForce(gravity);

  // 🧲 Repeller sigue al mouse
  repeller.position.set(mouseX, mouseY);

  emitter.applyRepeller(repeller);
  emitter.run();

  repeller.show();
}

// ------------------ Emitter ------------------
class Emitter {
  constructor(x, y) {
    this.origin = createVector(x, y);
    this.particles = [];
  }

  addParticle() {
    this.particles.push(new Particle(this.origin.copy()));
  }

  applyForce(f) {
    for (let p of this.particles) {
      p.applyForce(f);
    }
  }

  applyRepeller(r) {
    for (let p of this.particles) {
      let force = r.repel(p);
      p.applyForce(force);
    }
  }

  run() {
    for (let i = this.particles.length - 1; i >= 0; i--) {
      let p = this.particles[i];
      p.update();
      p.display();
      if (p.isDead()) {
        this.particles.splice(i, 1);
      }
    }
  }
}

// ------------------ Particle ------------------
class Particle {
  constructor(pos) {
    this.pos = pos.copy();
    this.vel = createVector(random(-1, 1), random(-1, 0));
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
    this.lifespan -= 2;
  }

  display() {
    stroke(0, this.lifespan);
    fill(175, this.lifespan);
    ellipse(this.pos.x, this.pos.y, 8);
  }

  isDead() {
    return this.lifespan < 0;
  }
}

// ------------------ Repeller ------------------
class Repeller {
  constructor(x, y) {
    this.position = createVector(x, y);
    this.power = 100; // Fuerza de repulsión
  }

  repel(p) {
    let dir = p5.Vector.sub(this.position, p.pos);
    let d = dir.mag();
    d = constrain(d, 5, 100); // Evita divisiones por 0 y hace el efecto realista
    dir.normalize();

    let force = -1 * this.power / (d * d); // Ley del inverso del cuadrado
    dir.mult(force);
    return dir;
  }

  show() {
    noStroke();
    fill(255, 0, 0, 150);
    ellipse(this.position.x, this.position.y, 24, 24);
  }
}

```

## Concepto

fuerza angular

## Gestion de particulas y memoria

Cada vez que se llama a emitter.addParticle() en el draw(), se crea una nueva instancia de la clase Particle.

Esto se traduce en: Una partícula nueva por cada cuadro de animación se guarda en el arreglo particles dentro del Emitter esto es fundamental para que el sistema crezca dinámicamente y tenga vida continua, simulando la emisión constante de partículas desde un punto.

## link p5js

https://editor.p5js.org/M4U-l/sketches/-3jXB2Dtq

## imagen

![](https://github.com/jfUPB/simulacion-M4U-l/blob/main/src/assets/Uni5Act2Img5.png)
