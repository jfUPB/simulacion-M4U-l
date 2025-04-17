``` java
let v3; 
let t = 0;

function setup() {
    createCanvas(300, 300);
}

function draw() {
    background(200);

    let v0 = createVector(mouseX, mouseY);
    let scaleFactor = dist(mouseX, mouseY, width / 2, height / 2) / 100;

    let v1 = createVector(120 * scaleFactor, 0);  
    let v2 = createVector(0, 120 * scaleFactor);  

    let v1_end = createVector(v0.x + v1.x, v0.y + v1.y);
    let v2_end = createVector(v0.x + v2.x, v0.y + v2.y);
    let v4 = createVector(v2_end.x - v1_end.x, v2_end.y - v1_end.y);

    v3 = p5.Vector.lerp(v1, v2, t); 

    t += 0.01;
    if (t > 1) t = 0; 

    drawArrow(v0, v1, 'red');
    drawArrow(v0, v2, 'blue');
    drawArrow(v0, v3, 'purple'); 
    drawArrow(v1_end, v4, 'green');  
}

function drawArrow(base, vec, myColor) {
    push();
    stroke(myColor);
    strokeWeight(3);
    fill(myColor);
    translate(base.x, base.y);
    line(0, 0, vec.x, vec.y);
    rotate(vec.heading());
    let arrowSize = 7;
    translate(vec.mag() - arrowSize, 0);
    triangle(0, arrowSize / 2, 0, -arrowSize / 2, arrowSize, 0);
    pop();
}
```


En lugar de usar un valor fijo para v0, lo cambie a let v0 = createVector(mouseX, mouseY);, lo que hace que el origen de las flechas siga el cursor del mouse
Escalado de los vectores:

Para escalar los vectores, calculamos un scaleFactor que depende de la distancia entre el mouse y el centro de la pantalla (dist(mouseX, mouseY, width / 2, height / 2)). Esto hace que los vectores crezcan o se reduzcan según qué tan cerca o lejos esté el mouse del centro de la ventana
