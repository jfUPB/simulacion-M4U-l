``` java
let v3; 
let t = 0; 

function setup() {
    createCanvas(300, 300);
    v3 = createVector(120, 0); 
}

function draw() {
    background(200);

    let v0 = createVector(100, 100);
    let v1 = createVector(120, 0);
    let v2 = createVector(0, 120);
    let v4 = createVector(120, 120);

    v3 = p5.Vector.lerp(v1, v2, t); 

    t += 0.01;
    if (t > 1) t = 0; 

    drawArrow(v0, v1, 'red');
    drawArrow(v0, v2, 'blue');
    drawArrow(v0, v3, 'purple'); 
    drawArrow(v0, v4, 'green'); 

    stroke(0);
    line(v1.x, v1.y, v3.x, v3.y); 
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
