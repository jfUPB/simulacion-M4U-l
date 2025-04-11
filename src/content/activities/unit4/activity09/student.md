https://editor.p5js.org/M4U-l/sketches/v-yCFHG7T

```js
let bobA, bobB;
let spring;
let dragging = false;

function setup() {
  createCanvas(400, 400);

  bobB = new FixedBob(width / 2, 50, 5);
  bobA = new Bob(width / 2, 150, 10);
  spring = new Spring(bobB, bobA, 100, 0.2);
}

function draw() {
  background(240);

  if (!dragging) {
    let gravity = createVector(0, 0.5);
    bobA.applyForce(p5.Vector.mult(gravity, bobA.mass));
  }

  spring.connect();
  bobA.update();

  spring.display();
  bobB.display();
  bobA.display();
}

function mousePressed() {
  let d = dist(mouseX, mouseY, bobA.position.x, bobA.position.y);
  if (d < bobA.radius) {
    dragging = true;
  }
}

function mouseDragged() {
  if (dragging) {
    bobA.position.set(mouseX, mouseY);
    bobA.velocity.set(0, 0); // Reset velocity to prevent snapping
  }
}

function mouseReleased() {
  dragging = false;
}

class Bob {
  constructor(x, y, m) {
    this.position = createVector(x, y);
    this.velocity = createVector(0, 0);
    this.acceleration = createVector(0, 0);
    this.mass = m;
    this.radius = this.mass * 8;
  }

  applyForce(force) {
    let f = p5.Vector.div(force, this.mass);
    this.acceleration.add(f);
  }

  update() {
    if (!dragging) {
      this.velocity.add(this.acceleration);
      this.position.add(this.velocity);
    }
    this.acceleration.mult(0);
  }

  display() {
    fill(175);
    stroke(0);
    strokeWeight(2);
    ellipse(this.position.x, this.position.y, this.radius * 2, this.radius * 2);
  }
}

class FixedBob {
  constructor(x, y, m) {
    this.position = createVector(x, y);
    this.mass = m;
    this.radius = this.mass * 8;
  }

  display() {
    fill(100, 200, 255);
    stroke(0);
    strokeWeight(2);
    ellipse(this.position.x, this.position.y, this.radius * 2, this.radius * 2);
  }
}


class Spring {
  constructor(a, b, len, k) {
    this.a = a;
    this.b = b;
    this.length = len;
    this.k = k;
  }

  connect() {
    let force = p5.Vector.sub(this.b.position, this.a.position);
    let d = force.mag();
    let stretch = d - this.length;

    force.normalize();
    force.mult(-1 * this.k * stretch);

    this.b.applyForce(force);
  }

  display() {
    stroke(0);
    strokeWeight(2);
    line(this.a.position.x, this.a.position.y, this.b.position.x, this.b.position.y);
  }
}

```
![](https://github.com/jfUPB/simulacion-M4U-l/blob/main/src/assets/Uni4Act9.png)
