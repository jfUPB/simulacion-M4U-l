En el código propuesto, el método **applyForce** está reemplazando la aceleración con la nueva fuerza aplicada, pero esto tiene un problema, la aceleración no se debe reemplazar, sino acumularse.


**solucion:** debemos acumular las fuerzas aplicadas sobre el objeto en cada frame, de manera que cada fuerza agregue su contribución a la aceleración en vez de reemplazarla. la ecuación correcta para calcular la aceleración:

\[
\vec{a} = \frac{\sum \vec{F}}{m}
\]

Donde la suma de todas las fuerzas aplicadas sobre el objeto se divide por la masa. 

\[
\vec{a} = \sum \vec{F}
\]

### Implementación en p5.js:

```javascript
let mover;
let wind;
let gravity;

function setup() {
  createCanvas(640, 240);
  mover = new Mover();  
  wind = createVector(0.1, 0);  
  gravity = createVector(0, 0.2);  
}

function draw() {
  background(255);
  mover.applyForce(wind);
  mover.applyForce(gravity);
  mover.update();
  mover.show();
  mover.checkEdges();
}

class Mover {
  constructor() {
    this.position = createVector(width / 2, height / 2);  
    this.velocity = createVector(0, 0);  
    this.acceleration = createVector(0, 0); 
  }

  applyForce(force) {
    this.acceleration.add(force);  
  }

  update() {
    this.velocity.add(this.acceleration);
    this.velocity.limit(5);
    this.position.add(this.velocity);
    this.acceleration.mult(0);
  }

  show() {
    fill(127);
    noStroke();
    ellipse(this.position.x, this.position.y, 48, 48);
  }

  checkEdges() {
    if (this.position.x > width) this.position.x = 0;
    if (this.position.x < 0) this.position.x = width;
    if (this.position.y > height) this.position.y = 0;
    if (this.position.y < 0) this.position.y = height;
  }
}
```
