https://editor.p5js.org/M4U-l/sketches/JEte_uRQT

```js
let pendulum1, pendulum2;

function setup() {
  createCanvas(600, 600);
  pendulum1 = new Pendulum(width / 2, 200, 125);
  pendulum2 = new Pendulum(0, 0, 125); 
}

function draw() {
  background(255);
  pendulum1.update();
  pendulum1.drag();
  pendulum1.show();
  pendulum2.pivot = pendulum1.bob.copy();
  pendulum2.update();
  pendulum2.drag();
  pendulum2.show();
}

function mousePressed() {
  pendulum1.clicked(mouseX, mouseY);
  pendulum2.clicked(mouseX, mouseY);
}

function mouseReleased() {
  pendulum1.stopDragging();
  pendulum2.stopDragging();
}


class Pendulum {
  constructor(x, y, r) {
    this.pivot = createVector(x, y);
    this.bob = createVector();
    this.r = r;
    this.angle = PI / 4;
    this.angleVelocity = 0.0;
    this.angleAcceleration = 0.0;
    this.damping = 0.995;
    this.ballr = 24.0;
    this.dragging = false;
  }

  update() {
    if (!this.dragging) {
      let gravity = 0.4;
      this.angleAcceleration = ((-1 * gravity) / this.r) * sin(this.angle);
      this.angleVelocity += this.angleAcceleration;
      this.angle += this.angleVelocity;
      this.angleVelocity *= this.damping;
    }
  }

  show() {
    this.bob.set(this.r * sin(this.angle), this.r * cos(this.angle));
    this.bob.add(this.pivot);

    stroke(0);
    strokeWeight(2);
    line(this.pivot.x, this.pivot.y, this.bob.x, this.bob.y);

    fill(127);
    if (this.dragging) fill(200);
    circle(this.bob.x, this.bob.y, this.ballr * 2);
  }

  clicked(mx, my) {
    let d = dist(mx, my, this.bob.x, this.bob.y);
    if (d < this.ballr) {
      this.dragging = true;
    }
  }

  stopDragging() {
    this.angleVelocity = 0;
    this.dragging = false;
  }

  drag() {
    if (this.dragging) {
      let diff = p5.Vector.sub(this.pivot, createVector(mouseX, mouseY));
      this.angle = atan2(-1 * diff.y, diff.x) - radians(90);
    }
  }
}

```

![](https://github.com/jfUPB/simulacion-M4U-l/blob/main/src/assets/Uni4Act10.png)
