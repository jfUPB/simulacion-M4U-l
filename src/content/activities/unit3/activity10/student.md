### Fricción

```js
let ball;
let friction = 0.1;

function setup() {
  createCanvas(600, 400);
  ball = new Ball(width / 2, height / 2);
}

function draw() {
  background(255);

  ball.applyFriction(friction);
  ball.update();
  ball.display();
}

class Ball {
  constructor(x, y) {
    this.position = createVector(x, y);
    this.velocity = createVector(3, 0);  // Velocidad inicial
    this.acceleration = createVector(0, 0);
    this.mass = 1;
  }

  applyFriction(mu) {
    let frictionForce = this.velocity.copy();
    frictionForce.normalize();
    frictionForce.mult(-1);
    frictionForce.mult(mu * this.mass);  // La fricción es proporcional a la masa
    this.acceleration.add(frictionForce);
  }

  update() {
    this.velocity.add(this.acceleration);
    this.position.add(this.velocity);
    this.acceleration.mult(0);  // Resetear la aceleración después de cada actualización
  }

  display() {
    fill(127);
    ellipse(this.position.x, this.position.y, 40, 40);
  }
}

```

Explicación: La fricción se modela reduciendo la velocidad del objeto en cada fotograma, aplicando un coeficiente de fricción.

***Link codigo ejemplo friccion:***

https://editor.p5js.org/M4U-l/sketches/Yj0-vbApP

### Resistencia al aire y fluidos

```js
let object;
let gravity = 0.2;
let airResistance = 0.02;  

function setup() {
  createCanvas(600, 400);
  object = new FallingObject(width / 2, 0);
}

function draw() {
  background(255);

  object.applyForce(createVector(0, gravity)); 
  object.applyAirResistance(airResistance);
  object.update();
  object.display();
}

class FallingObject {
  constructor(x, y) {
    this.position = createVector(x, y);
    this.velocity = createVector(0, 0);
    this.acceleration = createVector(0, 0);
    this.mass = 1;
  }

  applyForce(force) {
    let f = force.copy();
    f.div(this.mass);
    this.acceleration.add(f);
  }

  applyAirResistance(c_d) {
    let airResist = this.velocity.copy();
    airResist.normalize();
    airResist.mult(-c_d * this.velocity.magSq());
    this.acceleration.add(airResist);
  }

  update() {
    this.velocity.add(this.acceleration);
    this.position.add(this.velocity);
    this.acceleration.mult(0);  
  }

  display() {
    fill(127);
    ellipse(this.position.x, this.position.y, 40, 40);
  }
}

```

Explicación: La resistencia del aire se modela como una fuerza proporcional al cuadrado de la velocidad (velX * velX).
A medida que el objeto se mueve, esta resistencia reduce su velocidad hasta que el objeto se detiene.

***Link codigo ejemplo restencia al aire:***

https://editor.p5js.org/M4U-l/sketches/C9GtCdX1q

### Gravedad

```js
let objeto;
let planeta;
let G = 0.1;  
let masaObjeto = 5;
let masaPlaneta = 1000;

function setup() {
  createCanvas(600, 400);
  objeto = new Ball(300, 50, masaObjeto);
  planeta = new Planet(width / 2, height / 2, masaPlaneta);
}

function draw() {
  background(220);
  let gravedad = planeta.gravitationalForce(objeto); 
  objeto.applyForce(gravedad);
  objeto.move();
  objeto.display();

  planeta.display();
}

class Ball {
  constructor(x, y, masa) {
    this.x = x;
    this.y = y;
    this.velX = 0;
    this.velY = 0;
    this.masa = masa;
  }

  applyForce(fuerza) {
    let acelX = fuerza.x / this.masa;
    let acelY = fuerza.y / this.masa;
    
    this.velX += acelX;
    this.velY += acelY;
  }

  move() {
    this.x += this.velX;
    this.y += this.velY;
    
    if (this.y > height) {
      this.y = height;
      this.velY = 0;
    }
  }

  display() {
    fill(0, 255, 0);
    ellipse(this.x, this.y, 20, 20); 
  }
}

class Planet {
  constructor(x, y, masa) {
    this.x = x;
    this.y = y;
    this.masa = masa;
  }

  gravitationalForce(objeto) {
    let dx = this.x - objeto.x;  
    let dy = this.y - objeto.y;  
    let r = dist(this.x, this.y, objeto.x, objeto.y); 
    
    // Evitar división por cero
    if (r == 0) {
      return createVector(0, 0);
    }
    
    // Calcular la fuerza gravitacional
    let fuerzaGravedad = (G * this.masa * objeto.masa) / (r * r);
    let angle = atan2(dy, dx);  
    let fx = cos(angle) * fuerzaGravedad; 
    let fy = sin(angle) * fuerzaGravedad; 
    
    return createVector(fx, fy);
  }

  display() {
    fill(255, 0, 0);
    ellipse(this.x, this.y, 50, 50);
  }
}

```

Clase Ball (objeto):

El objeto (la bola) tiene una masa y se mueve de acuerdo a las fuerzas que le son aplicadas.

La función applyForce() recibe una fuerza y la aplica para modificar la velocidad del objeto, teniendo en cuenta su masa.

Movimiento de la bola:

En cada fotograma, la bola se mueve hacia el planeta debido a la fuerza gravitacional. Esta fuerza hace que su velocidad aumente, lo que genera una aceleración hacia el centro del planeta.


***Link codigo ejemplo atraccion gravitacionañ:***

https://editor.p5js.org/M4U-l/sketches/pSLC9g4v9
