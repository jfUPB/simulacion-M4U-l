```java
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
    this.position = createVector(width / 2, height / 2);  
  }

  show() {
    stroke(0);
    point(this.position.x, this.position.y); 
  }

  step() {
    let step = floor(random(4));
    let direction = createVector(0, 0); 

    if (step === 0) {
      direction = createVector(1, 1);  
    } else if (step === 1) {
      direction = createVector(1, -1); 
    } else if (step === 2) {
      direction = createVector(-1, 1); 
    } else if (step === 3) {
      direction = createVector(-1, -1); 
    }

    this.position.add(direction);  
  }
}
```
