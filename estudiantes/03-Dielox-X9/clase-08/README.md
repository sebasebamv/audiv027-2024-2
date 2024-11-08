# clase
## PROCESO DE TRABAJO
* * *
## Introducción
### 1. Intento de integrar FaceMesh con modelos .obj
Como primer enfoque para el desarrollo del proyecto, intentamos vincular la tecnología de FaceMesh de ML5 con modelos 3D en formato .obj, buscando una solución que permitiera superponer esa estructura tridimensional sobre los rostros detectados. Significó una serie de dificultades debido a que los archivos .obj/.stl que probamos eran demasiado pesados, lo que impactaba negativamente en el rendimiento, y en muchos casos el sistema no era capaz de reconocerlos correctamente como rostros.


![pruebas_caras01@2x-100](https://github.com/user-attachments/assets/2a96196c-9e05-494a-80d6-af1862d70665)

### 2. Reconocimiento facial y seguimiento de coordenadas
Se implementó una funcionalidad que permitió hacer un seguimiento de las coordenadas de la nariz y los ojos en tiempo real, usando el reconocimiento facial. Este seguimiento permitió que una imagen siga dichos puntos clave, aunque el rendimiento no fue del todo preciso y aún necesita ajustes. En este enfoque, sigue la fase de desarrollo y prueba.

* https://editor.p5js.org/cottito/sketches/rOvRVM_xn

![000](https://github.com/user-attachments/assets/857d1aed-b957-4a43-a3bc-e7b2b671ea33)

![deteccion_rostro](https://github.com/user-attachments/assets/57f10138-1cf2-40c0-9c57-31cdc6700474)


### 3. Búsqueda de alternativas: modelo Sticker (Let Emoji)
Al no obtener los resultados deseados con faceMesh, exploramos otras ideas, encontrando el modelo de "sticker" (Daniel Shiffman). Esta alternativa permitió la implementación de un objeto gráfico (sticker) sobre el rostro, logrando cierta interacción con las poses faciales. Aparte del primer acercamiento a los comandos LET EMOJI y POSENET.

![sticker_truco](https://github.com/user-attachments/assets/697beea0-67de-4ded-b7bc-7d7c89e5bfcb)

* https://editor.p5js.org/cottito/sketches/F9u6YjDgK

### 4. Problemas con la estabilidad de imagen sobre el rostro
En la fase de prueba, la imagen superpuesta sobre el rostro seguía las coordenadas de los puntos faciales, pero no de manera completamente estable. En ciertos momentos, la imagen se movía excesivamente o incluso desaparecía cuando el reconocimiento de los puntos esenciales del rostro fallaba.


https://github.com/user-attachments/assets/7a3a4ba6-8155-4c69-b124-cc9c22427367


### 5. Implementación de CANVASTEXT para indicaciones
Se añadió la funcionalidad CANVASTEXT para proporcionar al usuario instrucciones claras durante la experiencia. Estas incluían mensajes como “Colocar una imagen o URL” para guiar en la interacción con la aplicación.

![url texto](https://github.com/user-attachments/assets/0425bd99-33f9-469f-9d68-1fd05290b24a)

### 6. Cambio a BodyPose de ML5: Mejora en resultados
Debido a los problemas de estabilidad con PoseNet, optamos por cambiar a BodyPose de ML5, lo que permitió obtener mejores resultados en el reconocimiento facial y una mayor estabilidad en la superposición de imágenes. 
* El sistema fue capaz de reconocer zonas esenciales del rostro con mayor precisión, incluso en casos donde no estaban presentes todos los puntos faciales.

https://github.com/user-attachments/assets/82e7cc87-72d7-479a-8cf9-25e28ae94150


### 7. Correcciones y depuración de código
Durante el proceso de desarrollo, realizamos varias modificaciones y ajustes manuales en el código para optimizar el rendimiento general del sistema. Entre estas modificaciones, se incluyó la eliminación de funciones que no cumplían un rol importante o que afectaban negativamente el rendimiento del programa. También se corrigieron detalles menores, como redundancias en el código, lo que nos permitió depurar y simplificar el flujo de trabajo, mejorando tanto la velocidad de procesamiento como la estabilidad del programa en su conjunto.

![diferencia 01](https://github.com/user-attachments/assets/8f6b50b1-951f-44a5-819d-4cfa6311f0aa)

### 8. Optimización del código: Doble personaje
Como parte de la optimización del código establecido, se añadió una nueva funcionalidad que permite proyectar dos imágenes de manera simultánea en el canvas. Para lograr esto, se implementó una división visual en la mitad de la pantalla, dividiendo el área de trabajo en dos secciones claramente diferenciadas. Esta hendidura actúa como una línea divisoria que facilita la proyección de una imagen en cada lado del lienzo, manteniendo un balance visual y estructural dentro de la experiencia. Esta división ayuda a experimentar con comparaciones en tiempo real, lo que resulta útil para probar diferentes parámetros de reconocimiento facial y ajustes gráficos sin la necesidad de recargar el entorno.

### 9. Uso del comando tint para ajustar la transparencia en la división de pantalla
Para mejorar la visualización de las dos imágenes proyectadas en la pantalla dividida, se implementó el uso del comando tint, que permite ajustar la transparencia de las imágenes de manera dinámica. Este ajuste de opacidad resulta esencial para ofrecer una experiencia visual más clara y evitar que las imágenes superpuestas se confundan o se mezclen en exceso. Al reducir la opacidad de una o ambas imágenes mediante el uso de tint, logramos una distinción más nítida entre las dos secciones del lienzo, lo que refuerza la función de la hendidura visual central y mejora la percepción de cada imagen de manera individual.


* * *
#  Desarrollo de código
### 1. Copiamos el código base BodyPoses de ML5 punto por punto

* https://docs.ml5js.org/#/reference/bodypose

### 2. Modificación de valores originales para lograr superponer imagenes utilizando las coordenadas de los ojos y nariz de BodyPoses.
   
```
function drawImage(img, imgSize, imgX, imgY) {
  for (let i = 0; i < poses.length; i++) {
    let pose = poses[i];
    let nosePoint = pose.keypoints[0];
    let leftEyePoint = pose.keypoints[1];
    let rightEyePoint = pose.keypoints[2];
    let noseX, noseY, leftX, leftY, rightX, rightY;

    if (nosePoint.confidence > 0.2) {
      noseX = width - nosePoint.x;
      noseY = nosePoint.y;
    }

    if (leftEyePoint.confidence > 0.2) {
      leftX = width - leftEyePoint.x;
      leftY = leftEyePoint.y;
    }

    if (rightEyePoint.confidence > 0.2) {
      rightX = width - rightEyePoint.x;
      rightY = rightEyePoint.y;
    }

    if (rightX && rightY && leftX && leftY && noseX && noseY) {
      dis = dist(rightX, rightY, leftX, leftY);
      //Reescalado de imagen
      let calculatedSize = imgSize1;

      image(img1, noseX - imgSize1  / 2 + imgX1, noseY - imgSize1  / 2 - imgY1, imgSize1, imgSize1);
    }
  }
}
```
![dos_imgs@2x-100](https://github.com/user-attachments/assets/6f935238-bc04-49ca-870a-44f8d87f6029)

### 2.1. Eliminación de la función 'Connection'
La función Connection fue descartada al no ser necesaria para el funcionamiento del sistema.

### 3. Implementación de Drop de imágenes
Para hacer mas comoda la experiencia se optó por utilizar el código de Dropeo de imagenes, las cuales se actualizan automaticamente al momento de Arrastrar y dejar una nueva imagen.

```let canvasText = 'ARRASTRA TU IMAGEN\n(PNG)\nO PEGA UNA URL\n(JPG)';```
```
// Permitir el "drop" de imagen en el canvas
  let dropArea = select('canvas');
  dropArea.drop(gotFile);
```
```
function gotFile(file) {
  if (file.type === 'image') {
    img1 = createImg(file.data, '').hide();
    canvasText = ''; 
  } else {
    canvasText = 'ERROR:\nARCHIVO NO VÁLIDO\nVUELVA A INTENTAR';
  }
}
```
![Captura de pantalla 2024-10-04 132127](https://github.com/user-attachments/assets/5304ed28-fd94-4887-88f1-740f52e89136)

### 4. Opción de añadir imagen por URL + Botón de carga + Reseteo de la barra
Además del Drop de imágenes de decidió añadir una barra en el que se puedan escribir enlaces URL de iamgenes en caso de querer utilizar el código en un dispositivo movil, ofreciendo más flexibilidad. El usuario puede pegar la dirección de una imagen y cargarla directamente en el lienzo. Además, se implementó un botón de carga y una barra de progreso que se resetea automáticamente tras su carga.
```
// Crear cuadro de texto para URL
  let urlInput1  = createInput();
  urlInput1.position(10, height + 10);
  urlInput1.size(150);
  urlInput1.attribute('placeholder', 'Ingresar URL');
  //Crea botón de carga
  let button1 = createButton('CARGAR');
  button1.position(urlInput1.x + urlInput1.width + 10, urlInput1.y);
  button1.mousePressed(() => {
    let url1 = urlInput1.value();
    loadImage(url1, (loadedImage) => {
      img1 = loadedImage;
      //Limpia el texto del canvas
      canvasText = '';
      //Vacía la barra de URL
      urlInput1.value('');
    }, (error) => {
      urlInput1.value('');
    });
  });
```
![Captura de pantalla 2024-10-04 131913](https://github.com/user-attachments/assets/eac3dea0-53ff-4379-801a-8443cb658feb)

### 5. Control del tamaño de la imagen con slider
Al ver el resultado se optó por añadir Sliders para personalizar las medidas de tamaño y posicionamiento de la imagen en el rostro, con sus respectivas etiquetas de identificación:
```
// Crear sliders para drop 1
  sizeSlider1  = createSlider(50, 350, imgSize1);
  sizeSlider1.position(25, height + 50);
  xSlider1  = createSlider(-100, 100, imgX1);
  xSlider1.position(25, height + 90);
  ySlider1  = createSlider(-100, 100, imgY1);
  ySlider1.position(25, height + 140);
  
  // Crear etiquetas para los sliders
  createP('Tamaño Imagen').position(sizeSlider1.x + 15, sizeSlider1.y - 30);
  createP('Mover Eje X').position(xSlider1.x + 25, xSlider1.y - 30);
  createP('Mover Eje Y').position(ySlider1.x + 25, ySlider1.y - 30);
  createP('+').position(sizeSlider1.x + sizeSlider1.width + 10, sizeSlider1.y - 15);
  createP('+').position(xSlider1.x + xSlider1.width + 10, xSlider1.y - 15);
  createP('+').position(ySlider1.x + ySlider1.width + 10, ySlider1.y - 15);
  createP('-').position(sizeSlider1.x - 10, sizeSlider1.y - 15);
  createP('-').position(xSlider1.x - 10, xSlider1.y - 15);
  createP('-').position(ySlider1.x - 10, ySlider1.y - 15);
}

```
![SLIDER](https://github.com/user-attachments/assets/3cc19c59-295f-48ff-8034-f99102e4d61e)

### 6. Notas finales:
El código reconoce el rostro de más de una persona capaz de asisgnarle la misma imagen.
![Captura de pantalla 2024-10-04 134817](https://github.com/user-attachments/assets/b64f75ec-8e26-4b85-86d6-b5a35d9d785a)
![Captura de pantalla 2024-10-04 134901](https://github.com/user-attachments/assets/9ac25115-3c64-4ebd-a7ea-22b2bf481440)

### BONUS

Se intentó crear un código que permitiera la superposición de dos imagenes, asignando una "imagen A" en el lado izquierdo de la pantalla y otra "imagen B" en el lado derecho, finalmente esto no fue posible
![Captura de pantalla 2024-10-04 065702](https://github.com/user-attachments/assets/3896ad19-15bb-4675-ab7a-7c1960160fb5)
![Captura de pantalla 2024-10-04 060209](https://github.com/user-attachments/assets/13ef9249-76dd-44a1-9b5a-dbca70ff5dad)

### Adjunto código

https://editor.p5js.org/Dielox-X9/sketches/7ePb1opfI

### Repertorio de imágenes PNG para probar el código:
Se añadió un conjunto de imágenes PNG que se pueden usar para probar el funcionamiento del código

https://github.com/Dielox-X9/Pruebas

![Recurso 10](https://github.com/user-attachments/assets/d048197e-cd6b-4d38-8e3d-719741b15520)

Links imagen con URL:
https://eltallerdehector.com/wp-content/uploads/2022/10/spiderman-png-free.png


# Referencias
## Documentación a utilizar:
* https://docs.ml5js.org/#/reference/facemesh
* https://www.youtube.com/watch?v=ZXK8eFi0yK
* https://github.com/Dielox-X9/Pruebas/blob/main/Walter-White.p
* PosesNET original https://editor.p5js.org/codingtrain/sketches/ULA97pJXR
* PosesNET EMOJI https://editor.p5js.org/cottito/sketches/F9u6YjDgK
* BodyPoses Original ML5 https://editor.p5js.org/ml5/sketches/hMN9GdrO3

## Códigos investigados:
* https://docs.ml5js.org/#/reference/bodypose
* https://p5js.org/reference/
* https://p5js.org/examples/imported-media-image-transparency/

## Links varios no usados:
* https://docs.ml5js.org/#/reference/facemesh
* https://github.com/tensorflow/tfjs-models/tree/master/face-landmarks-detection
* https://github.com/tensorflow/tfjs-models/tree/master/face- landmarks-detection/demos
* https://teachablemachine.withgoogle.com/train
* https://mit-cml.github.io/yrtoolkit/yr/tutorials/facemesh.html
* https://ai.google.dev/edge/mediapipe/solutions/vision/face_landmarker?hl=es-419
* https://mediapipe-studio.webapps.google.com/demo/face_landmarker?hl=es-419
* https://www.youtube.com/watch?v=ZXK8eFi0yKs
* https://editor.p5js.org/p5/sketches
* https://p5js.org/reference/p5/createModel/

 
 ## Fallos
 ![Recurso 12](https://github.com/user-attachments/assets/3a6492dd-24a8-424c-bd4f-f84d24c141b6)


## Edición final
* https://editor.p5js.org/cottito/sketches/wx6DdNEEf
* https://editor.p5js.org/Dielox-X9/sketches/7ePb1opfI



```md
mi equipo de trabajo es <https://github.com/cottito> y <<https://github.com/Dielox-X9>>, entregamos en el repositorio en este enlace <https://github.com/disenoUChile/audiv027-2024-1/estudiantes/NOMBRE/clase-06>.
```
