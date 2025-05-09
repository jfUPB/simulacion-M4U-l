Algoritmo elegido: Flocking
Concepto de aplicación inesperada
En lugar de representar aves o peces, utilicé el algoritmo de flocking para simular el comportamiento de pensamientos dispersos en una mente distraída. Cada boid representa una idea o pensamiento que trata de alinearse, agruparse y separarse de otros en función de su “claridad”. A veces los pensamientos se concentran, pero otras veces se dispersan caóticamente, simulando momentos de concentración y distracción mental. El objetivo es representar visualmente cómo fluye el pensamiento humano en estados de enfoque o dispersión.
Adaptación de la lógica del algoritmo
Mantengo las tres reglas del algoritmo original (separación, alineación y cohesión), pero reinterpretadas conceptualmente. En este caso:

Separación representa el rechazo de pensamientos incompatibles o contradictorios.

Alineación representa la tendencia a seguir una línea de pensamiento o narrativa interna.

Cohesión simboliza la atracción hacia una idea central o dominante.

Los boids se visualizan como manchas suaves y translúcidas que cambian de color según su cercanía a otros pensamientos, lo cual refuerza la idea de una mente orgánica y en movimiento.

Interacción
El usuario puede influir en el grado de “claridad mental” con el mouse. Mientras más cerca del centro esté el cursor, más fuerte es la cohesión entre pensamientos. Cuando el mouse se aleja, los boids se dispersan, simbolizando distracción. También se puede presionar una tecla para alternar entre distintos "estados mentales", que modifican los pesos de cada regla.


```js
let boids = [];
let cohesionSlider, alignmentSlider, separationSlider;

function setup() {
  createCanvas(800, 600);
  for (let i = 0; i < 150; i++) {
    boids.push(new Boid());
  }
  cohesionSlider = createSlider(0, 5, 1, 0.1);
  alignmentSlider = createSlider(0, 5, 1, 0.1);
  separationSlider = createSlider(0, 5, 1.5, 0.1);
}

function draw() {
  background(15, 15, 30, 60);
  for (let boid of boids) {
    boid.edges();
    boid.flock(boids);
    boid.update();
    boid.show();
  }
}

class Boid {
  constructor() {
    this.position = createVector(random(width), random(height));
    this.velocity = p5.Vector.random2D();
    this.velocity.setMag(random(2, 4));
    this.acceleration = createVector();
    this.maxForce = 0.05;
    this.maxSpeed = 3;
  }

  edges() {
    if (this.position.x > width) this.position.x = 0;
    else if (this.position.x < 0) this.position.x = width;
    if (this.position.y > height) this.position.y = 0;
    else if (this.position.y < 0) this.position.y = height;
  }

  align(boids) {
    let perceptionRadius = 50;
    let steering = createVector();
    let total = 0;
    for (let other of boids) {
      let d = dist(this.position.x, this.position.y, other.position.x, other.position.y);
      if (other != this && d < perceptionRadius) {
        steering.add(other.velocity);
        total++;
      }
    }
    if (total > 0) {
      steering.div(total);
      steering.setMag(this.maxSpeed);
      steering.sub(this.velocity);
      steering.limit(this.maxForce);
    }
    return steering;
  }

  cohesion(boids) {
    let perceptionRadius = 50;
    let steering = createVector();
    let total = 0;
    for (let other of boids) {
      let d = dist(this.position.x, this.position.y, other.position.x, other.position.y);
      if (other != this && d < perceptionRadius) {
        steering.add(other.position);
        total++;
      }
    }
    if (total > 0) {
      steering.div(total);
      steering.sub(this.position);
      steering.setMag(this.maxSpeed);
      steering.sub(this.velocity);
      steering.limit(this.maxForce);
    }
    return steering;
  }

  separation(boids) {
    let perceptionRadius = 30;
    let steering = createVector();
    let total = 0;
    for (let other of boids) {
      let d = dist(this.position.x, this.position.y, other.position.x, other.position.y);
      if (other != this && d < perceptionRadius) {
        let diff = p5.Vector.sub(this.position, other.position);
        diff.div(d * d);
        steering.add(diff);
        total++;
      }
    }
    if (total > 0) {
      steering.div(total);
      steering.setMag(this.maxSpeed);
      steering.sub(this.velocity);
      steering.limit(this.maxForce);
    }
    return steering;
  }

  flock(boids) {
    let alignment = this.align(boids);
    let cohesion = this.cohesion(boids);
    let separation = this.separation(boids);

    alignment.mult(alignmentSlider.value());
    cohesion.mult(cohesionSlider.value());
    separation.mult(separationSlider.value());

    // Influencia del mouse sobre la cohesión
    let d = dist(mouseX, mouseY, width/2, height/2);
    let cohesionFactor = map(d, 0, width/2, 2, 0.2, true);
    cohesion.mult(cohesionFactor);

    this.acceleration.add(alignment);
    this.acceleration.add(cohesion);
    this.acceleration.add(separation);
  }

  update() {
    this.position.add(this.velocity);
    this.velocity.add(this.acceleration);
    this.velocity.limit(this.maxSpeed);
    this.acceleration.mult(0);
  }

  show() {
    noStroke();
    let c = color(map(this.velocity.mag(), 0, this.maxSpeed, 100, 255), 100, 255, 100);
    fill(c);
    ellipse(this.position.x, this.position.y, 8, 8);
  }
}

```

https://editor.p5js.org/M4U-l/sketches/QxSmlYtfi


![](https://github.com/jfUPB/simulacion-M4U-l/blob/main/src/assets/Uni6Act4.png)
