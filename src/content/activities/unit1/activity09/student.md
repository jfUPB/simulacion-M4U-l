```javascript
let noiseX = 0;
let noiseY = 10000;
let shapes = [];
let maxShapes = 100; 

let sizeFactor = 1.0; 
let moveSpeed = 0.01; 
let shapeType = 0; 

function setup() {
  createCanvas(640, 480);
  colorMode(HSB, 360, 100, 100, 1); 
  for (let i = 0; i < maxShapes; i++) {
    shapes.push(new Shape(random(width), random(height)));
  }

  // Captura la pantalla después de 5 segundos
  setTimeout(() => {
    saveCanvas('pantallazo', 'png');  // Guarda la imagen como PNG
  }, 5000); // 5000 milisegundos = 5 segundos
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
    this.baseHue = random(360); // Color base
  }

  update(speed) {
    this.x += map(noise(noiseX), 0, 1, -speed, speed);
    this.y += map(noise(noiseY), 0, 1, -speed, speed);
    noiseX += 0.01;
    noiseY += 0.01;
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
    sizeFactor += 0.1;  // Aumenta el tamaño de las formas
  } else if (key === 'S' || key === 's') {
    sizeFactor = max(0.1, sizeFactor - 0.1);  // Disminuye el tamaño de las formas
  }

  if (key === 'A' || key === 'a') {
    moveSpeed += 0.001;  // Aumenta la velocidad de movimiento
  } else if (key === 'D' || key === 'd') {
    moveSpeed = max(0.001, moveSpeed - 0.001);  // Disminuye la velocidad de movimiento
  }

  if (key === 'T' || key === 't') {
    shapeType = 0;  // Cambia al tipo de forma: Triángulo
  } else if (key === 'C' || key === 'c') {
    shapeType = 1;  // Cambia al tipo de forma: Círculo
  }
}
```

![](https://github.com/jfUPB/simulacion-M4U-l/blob/main/src/assets/Uni1Act9.png)
