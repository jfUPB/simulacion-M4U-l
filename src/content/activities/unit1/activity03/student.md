**Describe el experimento que vas a realizar**

El ejemplo dado por la pagina describe que el random walk puede moverse a 8 posiciones distintas, a demas de la posibilidad de quedarse en la misma casilla dando como resultado 9 posibles movimientos, lo que pienso cambiar es la posibilidad de que solo se mueva en las diagonales para dar un resultado de 4 posibles movimientos 

**¿Qué pregunta quieres responder con este experimento?**

como funciona el movimiento diagonal aleatorio 

**¿Qué resultados esperas obtener?**

una figura formada completamente por lineas diagonales

**¿Qué resultados obtuviste?**

el resultado esperado donde el walker solo podia moverse diagonalmente

**¿Qué aprendiste de este experimento?**

como usar numeros aleatorios para desplazar un objeto 

**codigo modificado**

let walker;

function setup() {
  createCanvas(640, 240);
  walker = new Walker();
  background(255);
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
    let step = floor(random(4)); // 0, 1, 2, 3
    if (step === 0) {
      this.x += 1;
      this.y += 1;
    } else if (step === 1) {
      this.x += 1;
      this.y -= 1;
    } else if (step === 2) {
      this.x -= 1;
      this.y += 1;
    } else if (step === 3) {
      this.x -= 1;
      this.y -= 1;
    }
  }
}


![](https://github.com/jfUPB/simulacion-M4U-l/blob/main/src/assets/Uni1Act3.png)
