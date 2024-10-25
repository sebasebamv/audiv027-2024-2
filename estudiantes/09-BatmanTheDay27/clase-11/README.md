### clase 11

- Veremos *OpenFrameworks*, software utilizado por 2 personas que veremos hoy.

- Roy es una de estas personas, mide como 2 metros y a pesar de su nombre y apariencia, es Chileno.

- Pulse Islam, es una obra que se realizó utilizando ampolletas que se iluminaban siguiendo las pulsaciones de una persona en una isla.

- Arturo Castro, mantenía OpenFrameworks el mismo y hace poco abandonó el software.

- para que un cuadro esté en rojo se coloca: *(255, 0, 0)*
- siempre es:

- function () {
-   console.log()
-   }

ejemplo: 

let captura;

function setup() {
  createCanvas(windowWidth / 2, 400);
  console.log(windowWidth);
  
  captura = createCapture(VIDEO);
}

function draw() {
  background(255, 0, 0);
}

function windowResized() {
  console.log("cambio la pantalla");
  resizeCanvas(windowWidth / 2, 400)
}

function fantasia() {
  console.log("fantasiaaa");
