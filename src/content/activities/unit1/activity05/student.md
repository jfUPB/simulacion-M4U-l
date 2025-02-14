```javascript
function setup() {
  createCanvas(500, 500);

  background(200);

}

function draw() {
  noStroke();
  fill(10, 100);

  let x = random(300);
  let y = 20;
  circle(x, y, 5);

 
  x = randomGaussian(100);
  y = 50;
  circle(x, y, 5);

  x = randomGaussian(100, 20);
  y = 75;
  circle(x, y, 5);
}
```
![](https://github.com/jfUPB/simulacion-M4U-l/blob/main/src/assets/Uni1Act5.png)

la distribucion gaussiana se refleja en la forma en la que se generan las lineas, dado que siempre se llena de circulos en el centro de forma mas rapida y mas lenta en lso extremos 
