**1)**   El código simula puntos de colores usando valores aleatorios con una distribución normal. con unos sliders se puede ajustar la dispersión, el tamaño, el color y la transparencia de las salpicaduras. Cada vez que se ejecuta, se genera un nuevo circulo en una posición aleatoria, con un tamaño y color aleatorio dentro de los rangos definidos

**2)** El ruido Perlin se genera mediante la función noise(), que toma un valor como entrada (en este caso this.tx y this.ty) y devuelve un valor entre 0 y 1. el ruido Perlin genera valores que están correlacionados y no tienen saltos bruscos. Esto hace que los movimientos de la lina sean más suaves y naturales.
this.tx y this.ty son variables que sirven como coordenadas para generar el ruido. Estas se incrementan en cada paso (this.tx += 0.01 y this.ty += 0.01), lo que provoca que el ruido cambie suavemente a medida que la linea se mueve.

```javascript
let walker;

function setup() {
  createCanvas(640, 240); 
  walker = new Walker(); 
  background(255);
  setTimeout(() => {
    saveCanvas('pantallazo', 'png');
  }, 5000); 
}

function draw() {
  walker.step();
  walker.show();
}

class Walker {
  constructor() {
    this.x = width / 2;
    this.y = height / 2;
    this.oldx = this.x;
    this.oldy = this.y;
    this.tx = 0;
    this.ty = 10000;
  }

  step() {
    this.x += map(noise(this.tx), 0, 1, -1, 1);
    this.y += map(noise(this.ty), 0, 1, -1, 1);

    this.tx += 0.01;
    this.ty += 0.01;
  }

  show() {
    stroke(0);
    line(this.oldx, this.oldy, this.x, this.y);
    this.oldx = this.x;
    this.oldy = this.y;
  }
}
```



![](https://github.com/jfUPB/simulacion-M4U-l/blob/main/src/assets/Uni1Act7.png)
