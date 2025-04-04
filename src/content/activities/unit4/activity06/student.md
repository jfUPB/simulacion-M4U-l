*Link p5js*

https://editor.p5js.org/M4U-l/sketches/XWEOApxhh


*codigo*

```js
let amplitudeSlider, frequencySlider, phaseSlider;
let t = 0;

function setup() {
  createCanvas(800, 400);

  createP("Amplitud");
  amplitudeSlider = createSlider(10, 200, 100);

  createP("Frecuencia (Hz)");
  frequencySlider = createSlider(0.1, 5, 1, 0.1);

  createP("Fase (radianes)");
  phaseSlider = createSlider(0, TWO_PI, 0, 0.01);
}

function draw() {
  background(255);
  stroke(0);
  noFill();
  
  let A = amplitudeSlider.value();            // Amplitud
  let f = frequencySlider.value();            // Frecuencia
  let φ = phaseSlider.value();                // Fase
  let T = 1 / f;                               // Periodo
  let ω = TWO_PI * f;                         // Velocidad angular

  // Ejes
  stroke(200);
  line(0, height/2, width, height/2);
  
  stroke(50);
  beginShape();
  for (let x = 0; x < width; x++) {
    let y = A * sin(ω * (x * 0.01) + φ);
    vertex(x, height / 2 - y);
  }
  endShape();

  // Mostrar valores
  fill(0);
  noStroke();
  textSize(14);
  text(`Amplitud (A): ${A}`, 20, 20);
  text(`Frecuencia (f): ${f.toFixed(2)} Hz`, 20, 40);
  text(`Periodo (T): ${T.toFixed(2)} s`, 20, 60);
  text(`Velocidad angular (ω): ${ω.toFixed(2)} rad/s`, 20, 80);
  text(`Fase (φ): ${φ.toFixed(2)} rad`, 20, 100);
}
```

![](https://github.com/jfUPB/simulacion-M4U-l/blob/main/src/assets/Uni4Act6.png)
