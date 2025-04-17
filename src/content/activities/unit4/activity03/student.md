```js
let vehicle;

function setup() {
  createCanvas(600, 400);
  vehicle = new Vehicle(width / 2, height / 2);
}

function draw() {
  background(220);
  vehicle.update();
  vehicle.display();
}

function keyPressed() {
  if (keyCode === LEFT_ARROW) {
    vehicle.applyForce(createVector(-0.1, 0));
  } else if (keyCode === RIGHT_ARROW) {
    vehicle.applyForce(createVector(0.1, 0));
  } else if (keyCode === UP_ARROW) {
    vehicle.applyForce(createVector(0, -0.1));
  } else if (keyCode === DOWN_ARROW) {
    vehicle.applyForce(createVector(0, 0.1));
  }
}

class Vehicle {
  constructor(x, y) {
    this.position = createVector(x, y);
    this.velocity = createVector(0, 0);
    this.acceleration = createVector(0, 0);
    this.angle = 0;
  }

  applyForce(force) {
    this.acceleration.add(force);
  }

  update() {
    this.velocity.add(this.acceleration);
    this.position.add(this.velocity);
    this.acceleration.mult(0);
    
    if (this.velocity.mag() > 0.1) {
      this.angle = this.velocity.heading();
    }
  }

  display() {
    push();
    translate(this.position.x, this.position.y);
    rotate(this.angle);
    fill(127);
    stroke(0);
    triangle(-10, 10, 10, 10, 0, -15);
    pop();
  }
}

```
link de la simulacion:

https://editor.p5js.org/M4U-l/sketches/Ecu8-O-n1

![](https://github.com/jfUPB/simulacion-M4U-l/blob/main/src/assets/Uni4Act2.png)
