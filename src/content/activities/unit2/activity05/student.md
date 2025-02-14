``` java
let v3; 
let t = 0;

function setup() {
    createCanvas(300, 300);
}

function draw() {
    background(200);

    let v0 = createVector(100, 100);
    let v1 = createVector(120, 0);
    let v2 = createVector(0, 120);
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


### 1. **`lerp()`**
   La función lerp() en p5.js toma tres parámetros:

   - **start**: el valor inicial
   - **end**: el valor final
   - **amount**: el valor de interpolación (un número entre 0 y 1)

   La función devuelve un valor que está en algún punto intermedio entre los valores start y end

### 2. **lerpColor()**
   la función lerpColor() también realiza una interpolación, pero con colores en lugar de valores numéricos o vectores. Funciona de la misma manera que lerp(), interpolando entre dos colores de acuerdo con un valor de interpolación


### 3. **Dibujo de una flecha con drawArrow()**
   La función drawArrow() se encarga de dibujar una flecha en el lienzo. La flecha se dibuja de acuerdo con un vector base y un vector que define la dirección y longitud de la flecha 

   La función realiza los siguientes pasos:
   1. **push()** y **pop()**: Estas funciones guardan y restauran el estado de la transformación (es decir, las modificaciones de la posición y rotación) para que no afecten a otras flechas
   2. **stroke(myColor)** y **fill(myColor)**: Establece el color del contorno y el relleno de la flecha
   3. **translate(base.x, base.y)**: Mueve el origen del lienzo al punto base de la flecha
   4. **line(0, 0, vec.x, vec.y)**: Dibuja la línea de la flecha desde el origen (0, 0) hacia el punto definido por el vector vec
   5. **rotate(vec.heading())**: Rota el lienzo para que la flecha apunte en la dirección correcta (calculada con vec.heading())
   6. **triangle(0, arrowSize / 2, 0, -arrowSize / 2, arrowSize, 0)**: Dibuja la punta de la flecha como un triángulo en la parte superior de la línea
