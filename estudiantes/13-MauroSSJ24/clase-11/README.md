# clase

Ver la tarea opcional de lo enviada (ayer): Tarea Infinita.

Dorothy Santos:
https://dorothysantos.com/work/speaking-engagements/
https://dorothysantos.com/


Rafael Lozano-Hemmer:
https://www.lozano-hemmer.com/publications.php?order=Author_(A_to_Z)
https://www.lozano-hemmer.com/projects.php
*Hace mucho arte, junto a otras 30 personas.
*Estudio arte
Ejmplo:
https://www.lozano-hemmer.com/pulse_island.php


https://openframeworks.cc/
(Arturo Castro)_Era el programador mas importante de openframeworks, hasta que renuncio.
*No porque una herramienta deje de usarse, no funciona.


Vamos a aprender y repasar lo de jvascript, para verse en el celular, para llegar ver lo que vemos en el computador en el celular. (Que es lo que es la camara o webcam para el computador)
*Ingresar a p5js (con github)
*crtl + s (hacerlo un tik, osea un movimiento automatico nuestro)
*Si dice fuction+"un nombre" significa que eso existe.


*Actividad de ejemplos*
// Tamaño de la ventana de la muestra
function setup() {
  createCanvas(windowWidth / 2, 400);
  console.log(windowWidth);
}
// color del dibujo
function draw() {
  background(255, 0, 0);
}
//Todo lo de aqui va a ocurrir cuando se mueva la ventana es determinado por estas funciones
function windowResized() {
  console.log("cambio la pantalla!!");
  resizeCanvas(windowWidth / 2, 400);
 }

function fantasia() {
  console.log("fantasiaaaaa");
  }
// pruebas 1 para verlo en el celular tambien



*Actividad de ejemplos 2*
let captura;

// Tamaño de la ventana de la muestra
function setup() {
  createCanvas(windowWidth / 2, 400);
  console.log(windowWidth);
  
  captura = createCapture(VIDEO)
}
// color del dibujo
function draw() {
  background(255, 0, 0);
}
//Todo lo de aqui va a ocurrir cuando se mueva la ventana es determinado por estas funciones
function windowResized() {
  console.log("cambio la pantalla!!");
  resizeCanvas(windowWidth / 2, 400);
 }

function fantasia() {
  console.log("fantasiaaaaa");
  }
// pruebas 2 para verlo en el celular tambien con camara y video


*Actividad de ejemplos 3*
// nos permite hacer streaming de audio y video.
let captura;

let opciones = {
  video:{
    mandatory: {
      minWidth:1280,
      minHeight: 720
    },
  },
  audio: false, // or True
};


// Tamaño de la ventana de la muestra
function setup() {
  createCanvas(windowWidth / 2, 400);
  console.log(windowWidth);
  
  captura = createCapture(VIDEO)
}
// color del dibujo
function draw() {
  background(255, 0, 0);
}
//Todo lo de aqui va a ocurrir cuando se mueva la ventana es determinado por estas funciones
function windowResized() {
  console.log("cambio la pantalla!!");
  resizeCanvas(windowWidth / 2, 400);
 }

function fantasia() {
  console.log("fantasiaaaaa");
  }



  



  
