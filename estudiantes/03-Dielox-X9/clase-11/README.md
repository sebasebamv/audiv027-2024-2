# clase 11: RESUMEN

## Primera Parte: 

### Recapitulatorio de lo que pasó en las últimas semanas:
- Comenzamos hablando sobre las clases en Temuco que realizó el profesor Aaron y sobre las observaciones que dejamos en el clase 9.

- Como la clase 10 fue el 18OCT la clase se suspendió, pero se nos dejó una tarea investigativa opcional.

- Comentamos sobre **"OpenFramework"** escrito en **"C++"** y de algunos de sus creadores. Arturo Castro Formaba parte del software, pero abandonó el proyecto.  
---
### Utilizar WebCam del celular usando P5
- Mandar link de p5 a Ucursos para tenerlo a mano cuando lo vayamos a utilizar.

- Estamos viendo como personalizar el video en el lienzo, como ocultarlo, modificar tamaños, etc.
``` javascript
let captura;
let opciones = {
  video: {
    mandatory:{
      minWidth: 1280,
      minHeight: 720
    },
  },
  audio: false,
};

function setup() {
  // windowsWidth adapta el tamaño de la pantalla 
  createCanvas(windowWidth/2, 400);
  console.log(windowWidth)

  captura = createCapture(VIDEO);
}

function draw() {
  background(255, 0, 0);
}

function windowResized(){
  console.log("Me MaReOoOoOoOoOo Deja de moverme!!!!")
  resizeCanvas(windowWidth/2, 400);
}

function fantasia(){
  console.log("fantasiaaa")
}
```
Investigué bien el como invertir la cámara y esto es lo averiguado:

---
# *BREAK*

## Segunda Parte:

- LOREM IPSUM

# CIERRE DE CLASE
