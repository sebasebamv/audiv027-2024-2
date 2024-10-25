### clase 11

- Veremos *OpenFrameworks*, software utilizado por 2 personas que veremos hoy.

- Roy es una de estas personas, mide como 2 metros y a pesar de su nombre y apariencia, es Chileno.

- Pulse Islam, es una obra que se realizó utilizando ampolletas que se iluminaban siguiendo las pulsaciones de una persona en una isla.

- Arturo Castro, mantenía OpenFrameworks el mismo y hace poco abandonó el software.

- Para que un cuadro esté en rojo se coloca: *(255, 0, 0)*
- siempre es:

``` javascript
let captura;

let opciones = {
  video: {
    facingMode: "environment",
  },
  audio: false,
};


function setup() {
  createCanvas(windowWidth / windowHeight);
  console.log(windowWidth);
  captura = createCapture(opciones);
  captura.hide();
  image(captura, 0, 0);
}

function draw() {
  background(255, 0, 0);
  // image(captura, mouseX, mouseY);
  image(captura, 0, 0, windowWidth, windowHeight);
}

function windowResized() {
  console.log("cambio la pantalla");
  resizeCanvas(windowWidth / windowHeight);
}

function fantasia() {
  console.log("fantasiaaa");
}
```
- Acabamos de aprender a hacer un elemento para catura de audio y video.



