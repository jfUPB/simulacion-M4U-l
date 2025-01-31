La diferencia entre una distribución uniforme y una distribución no uniforme de números aleatorios radica en cómo se distribuyen esos números dentro de un rango.

En una distribución uniforme, todos los números dentro de un rango tienen la misma probabilidad de ser elegidos mientras que en una distribución no uniforme, la probabilidad de que un número específico sea elegido no es igual para todos los números del rango. 


**codigo**

let walker;

function setup() {
  createCanvas(640, 240);
  walker = new Walker();
  background(255);
  
  setTimeout(captureScreen, 5000);
}

function draw() {
  walker.step();
  walker.show();
}

class Walker {
  constructor() {
    this.x = width / 2;
    this.y = height / 2;
  }

  show() {
    stroke(0);
    point(this.x, this.y);
  }

  step() {

    let xstep = random(-2, 2); 
    let ystep = random(0, 4);  
    if (ystep < 0) {
      ystep = 0;
    }
    this.x += xstep;
    this.y += ystep;
  }
}

function captureScreen() {
  saveCanvas('walker_screenshot', 'png'); // Guarda la pantalla como una imagen PNG
}

![]([https://github.com/jfUPB/simulacion-M4U-l/blob/main/src/assets/Uni1Act3.png](https://github.com/jfUPB/simulacion-M4U-l/blob/main/src/assets/Uni1Act4.png))
