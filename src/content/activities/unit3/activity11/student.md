```js
let cuerpos = [];
let G = 0.1;  

function setup() {
  createCanvas(300, 300);

  for (let i = 0; i < 3; i++) {
    let x = random(width);
    let y = random(height);
    let masa = random(10, 30);
    let velocidadX = random(-1, 1);
    let velocidadY = random(-1, 1);
    cuerpos.push(new Cuerpo(x, y, masa, velocidadX, velocidadY));
  }
}

function draw() {
  background(0);
  for (let i = 0; i < cuerpos.length; i++) {
    let cuerpo = cuerpos[i];
    cuerpo.applyGravitationalForces(cuerpos);
    cuerpo.update();
    cuerpo.display();
  }
}

// Función que se activa cuando se hace clic en el lienzo
function mousePressed() {
  // Guardar el canvas como imagen
  saveCanvas('pantallazo', 'png');
}

class Cuerpo {
  constructor(x, y, masa, velX, velY) {
    this.x = x;
    this.y = y;
    this.masa = masa;
    this.velX = velX;
    this.velY = velY;
    this.trayectoria = [];  
  }
  
  applyGravitationalForces(cuerpos) {
    for (let i = 0; i < cuerpos.length; i++) {
      if (cuerpos[i] != this) {
        let dx = cuerpos[i].x - this.x;
        let dy = cuerpos[i].y - this.y;
        let distancia = sqrt(dx * dx + dy * dy);
        let fuerzaGrav = (G * this.masa * cuerpos[i].masa) / (distancia * distancia);
        let angle = atan2(dy, dx);
        let fx = cos(angle) * fuerzaGrav;
        let fy = sin(angle) * fuerzaGrav;
        this.velX += fx / this.masa;
        this.velY += fy / this.masa;
      }
    }
  }
  
  update() {
    this.x += this.velX;
    this.y += this.velY;
    
    if (this.x > width) this.x = 0;
    if (this.x < 0) this.x = width;
    if (this.y > height) this.y = 0;
    if (this.y < 0) this.y = height;
  }

  display() {
    fill(255);
    noStroke();
    ellipse(this.x, this.y, this.masa, this.masa); 
    this.trayectoria.push(createVector(this.x, this.y));
    if (this.trayectoria.length > 50) {
      this.trayectoria.shift();
    }
    stroke(255, 100);
    noFill();
    beginShape();
    for (let i = 0; i < this.trayectoria.length; i++) {
      vertex(this.trayectoria[i].x, this.trayectoria[i].y);
    }
    endShape();
  }
}

```

***Explicación:***
Para esta simulación, me inspiré en las esculturas cinéticas de Alexander Calder, que son conocidas por sus movimientos suaves y fluidos. En lugar de un sistema planetario estático, creé un sistema de cuerpos que interactúan entre sí y que se mueven libremente en un espacio 2D. Cada cuerpo tiene una masa y una velocidad inicial aleatoria, lo que hace que las interacciones entre los cuerpos sean impredecibles y visualmente interesantes.

Las trayectorias de los cuerpos se muestran como líneas, lo que permite observar cómo sus movimientos se desarrollan con el tiempo.


### link de la simulacion

https://editor.p5js.org/M4U-l/sketches/oXluaROH9



![](https://github.com/jfUPB/simulacion-M4U-l/blob/main/src/assets/Uni3Act11.png)
