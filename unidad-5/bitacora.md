
# Evidencias de la unidad 5

## Actividad 01
### Repasa el caso de estudio
En esta actividad vas a poner a funcionar el caso de estudio de la unidad anterior y lo vas a repasar de nuevo. Mira, es muy importante que le dedique un tiempo generoso a revisar de nuevo el caso de estudio, ya que es un ejemplo muy completo y te va a ayudar a entender mejor el resto de la unidad.

De una, empecemos entonces 🫡

#### Describe cómo se están comunicando el micro:bit y el sketch de p5.js. ¿Qué datos envía el micro:bit?
La comunicación del *micro:bit* y el sketch de *p5.js* se da a través del puerto serial. El *micro:bit* envía 4 valores (`xValue`, `yValue`, `aState`, `bState`), que son las coordenadas en X y Y según su acelerómetro en forma de `floats`, y el estado de los 2 botones `A` y `B` en booleanos. Además, envía un caracter `\n`, para disiinguir entre cada "tanda" de valores.  
#### ¿Cómo es la estructura del protocolo ASCII usado?
El mensaje tiene los 4 valores en este orden: `xValue`, `yValue`, `aState`, `bState`. Estos están separados por comas `,` y sin espacios. Además, al final de cada "tanda", se envía un `\n`, referencia que usa *p5.js* para terminar de leer un "bloque" específico de datos. 
#### Muestra y explica la parte del código de p5.js donde lee los datos del micro:bit y los transforma en coordenadas de la pantalla.
La parte específica encargada de leer los datos se encuentra dentro de la función `draw()`:
```js
if (port.availableBytes() > 0) {
  let data = port.readUntil("\n"); // (1)
  if (data) {
    data = data.trim();            // (2)
    let values = data.split(",");
    if (values.length == 4) {
      microBitX = int(values[0]) + windowWidth / 2;
      microBitY = int(values[1]) + windowHeight / 2;
      microBitAState = values[2].toLowerCase() === "true";
      microBitBState = values[3].toLowerCase() === "true";
      updateButtonStates(microBitAState, microBitBState);
    } else {
      print("No se están recibiendo 4 datos del micro:bit");
    }
  }
}
```
#### ¿Cómo se generan los eventos A pressed y B released que se generan en p5.js a partir de los datos que envía el micro:bit?
#### Capturas de pantalla de los algunos dibujos que hayas hecho con el sketch.

## Timeline de proceso de investigación (Actividad 01)
### Como no sé organizar nada, simplemente voy a ir poniendo acá entradas de las cositas que van pasando.
Bueno, so, lo primero fue buscar el caso de estudio pasado para poder usarlo (el link que el profe nos proporcionó simplemente lleva a *p5.js*). Habiendo encontrado el código y habiéndolo probado directamente en el [p5 del profe](https://editor.p5js.org/juanferfranco/sketches/6ovAtsZ10), tomé nota de cómo funciona con el *micro:bit*, y creé un [duplicado del proyecto](https://editor.p5js.org/MAG-02/sketches/Z7NIsRbFm) en caso de necesitar editarlo.

También aprendí 2 maneras diferentes de adjuntar archivos en GitHub desde navegador LOL

*Método al tomar una captura:*
<img width="400" height="427" alt="image" src="https://github.com/user-attachments/assets/1534a126-ef06-48d9-a53c-df1f5311eb67" />

*Método con subida de archivo:*
![Obra de Arte hecha con *micro:bit*](./dibujo.png)

Explicando el funcionamiento del código, específicamente la lectura de datos por parte de *p5.js*, me di cuenta que había una (técnicamente 2) línea(s) específica(s) que no entendía:
```js
if (data) {
  data = data.trim();
}
```
Asumo que el `if (data)` simplemente verifica que sí se esté recibiendo algo. Creo que es una redundancia en nuestro caso porque sé que el código que tenemos funciona y los datos están siendo enviados correctamente. Aún así, intentaré ejecutar el código sin este `if` inicial para ver qué sucede.  
**Resultado:**  
<img width="1919" height="957" alt="image" src="https://github.com/user-attachments/assets/8c57e260-97d1-4a40-8232-95b996879b9e" />
El es similar a lo que esperaba: El código se ejecuta correctamente, y la funcionalidad no se ve afectada. Lo único es que, aparentemente, *p5.js* está un poco confundido y "deja perder" algunos datos, o quizá agrupa datos que no deberían ir juntos, por lo que muestra constantemente el error `No se están recibiendo 4 datos del micro:bit`





