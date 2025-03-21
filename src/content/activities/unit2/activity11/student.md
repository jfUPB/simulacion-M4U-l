``` java
let noiseX = 0;
let noiseY = 10000;
let shapes = [];
let maxShapes = 100;

let sizeFactor = 1.0;
let moveSpeed = 1; 
let shapeType = 0;

function setup() {
  createCanvas(640, 480);
  colorMode(HSB, 360, 100, 100, 1); 
  for (let i = 0; i < maxShapes; i++) {
    shapes.push(new Shape(random(width), random(height)));
  }

  setTimeout(() => {
    saveCanvas('pantallazo', 'png');  
  }, 5000); 
}

function draw() {
  background(255);
  for (let shape of shapes) {
    shape.update(moveSpeed); 
    shape.show(); 
  }
}

class Shape {
  constructor(x, y) {
    this.x = x;
    this.y = y;
    this.size = random(30, 80) * sizeFactor;
    this.angle = random(TWO_PI);
    this.baseHue = random(360); 
  }

  update(speed) {

    let dx = mouseX - this.x;
    let dy = mouseY - this.y;
    let dist = sqrt(dx * dx + dy * dy);

    if (dist < this.size / 2) {
      this.x = random(width);
      this.y = random(height);
    } else {
      this.x += (dx / dist) * speed;
      this.y += (dy / dist) * speed;
    }
  }

  show() {
    let c = color((this.baseHue + map(mouseY, 0, height, -50, 50)) % 360, 80, 80);
    fill(c);
    noStroke();
    
    push();
    translate(this.x, this.y);
    rotate(this.angle);
    if (shapeType === 0) {
      this.drawFractal(0, 0, this.size);
    } else if (shapeType === 1) {
      this.drawCircleFractal(0, 0, this.size);
    }
    pop();
  }

  drawFractal(x, y, s) {
    if (s < 5) return;
    triangle(x, y, x + s, y, x + s / 2, y - s);
    this.drawFractal(x, y, s / 2);
    this.drawFractal(x + s / 2, y, s / 2);
    this.drawFractal(x + s / 4, y - s / 2, s / 2);
  }
  
  drawCircleFractal(x, y, s) {
    if (s < 5) return;
    ellipse(x, y, s, s);
    this.drawCircleFractal(x - s / 2, y, s / 2);
    this.drawCircleFractal(x + s / 2, y, s / 2);
    this.drawCircleFractal(x, y - s / 2, s / 2);
    this.drawCircleFractal(x, y + s / 2, s / 2);
  }
}

function keyPressed() {
  if (key === 'W' || key === 'w') {
    sizeFactor += 0.1; 
  } else if (key === 'S' || key === 's') {
    sizeFactor = max(0.1, sizeFactor - 0.1);  
  }
  if (key === 'A' || key === 'a') {
    moveSpeed += 0.1; 
  } else if (key === 'D' || key === 'd') {
    moveSpeed = max(0.1, moveSpeed - 0.1);  
  }
  if (key === 'T' || key === 't') {
    shapeType = 0;  
  } else if (key === 'C' || key === 'c') {
    shapeType = 1;  
  }
}

```
![](https://github.com/jfUPB/simulacion-M4U-l/blob/main/src/assets/Uni2Act11.png)
