# Unidad 1

## 🔎 Fase: Set + Seek

## Set: ¿Qué aprenderás en esta unidad? 💡
Aprenderás acerca de las posibilidades que ofrecen los sistemas físicos interactivos. Te mostraré ejemplos aplicados al arte y al diseño generativos. Además, reflexionarás sobre cómo estas prácticas pueden relacionarse con tu perfil profesional.

## Actividad 01
### ¿Qué es un sistema físico interactivo?
* **¿Qué es un sistema físico interactivo?**  
  Un sistema físico interactivo es, por decir así, una cadena de input-procesamiento-output. Se toma una entrada por cualquier método que definamos, se procesa con el código que escribimos dentro de un computador, y luego se envía una salida con cierta información según lo que hayamos programado.
* **¿Cómo podrías aplicar lo que has visto en tu perfil profesional?**  
  Principalmente veo que los sistemas físicos interactivos me permitirían implementar nuevos métodos de comunicación con programas/aplicaciones que utilice. Me interesa mucho la idea de tener control completo sobre la "información" que recibo por parte de un periférico como un control de consola, pero especialmente pensando en periféricos más "extraños" como, por ejemplo, un *Kinect* o un control con sensores de movimiento (de *Wii* o de *Switch*, por ejemplo).

## Actividad 02
### ¿Qué es el diseño y el arte generativos?
* **¿Qué es el diseño/arte generativo?**  
  El diseño/arte generativo es el proceso de crear arte a través de un programa que toma "influencias" (inputs) y, siguiendo ciertas reglas establecidas por el programador (código), crea las distintas representaciones gráficas. La "gracia" del diseño generativo es pensar qué mensaje se pretende dar con la obra resultante para así planear las influencias que se utilizarán en el proceso de creación.
* **¿Cómo podrías aplicar lo que has visto en tu perfil profesional?**  
  Pensando en un caso muy específico, siento que el diseño generativo suele verse dentro de producciones mayores (como un juego completo/AAA) en forma de "extras" o mini-juegos que sirven para darle al usuario nuevas maneras de interactuar con mecánicas ya existentes dentro del juego.  
Un ejemplo que se me viene a la mente sería el juego ***Undertale***: en una zona del *Underground* el jugador puede interactuar con unas flores para emitir pequeños sonidos y, con suficiente esfuerzo, podría hacer una melodía. Quizá no sea un emplo 1-1 con el concepto, pero siento que esa sería la aplicación más directa del diseño generativo en mi posible perfil profesional.

## Seek: Investigación 🔎
Ahora que ya tienes una idea general de las posibilidades de los sistemas físicos interactivos y una aplicación al arte y al diseño generativos, es momento de profundizar en el tema, deconstruir algunos ejemplos y reflexionar sobre su relevancia en el contexto del entretenimiento digital.

## Actividad 03
### Herramientas y tecnologías
Con este código en *micro:bit*:
```python
from microbit import *

uart.init(baudrate=115200)
display.show(Image.BUTTERFLY)

while True:
    if button_a.is_pressed():
        uart.write('A')
        sleep(500)
    if button_b.is_pressed():
        uart.write('B')
        sleep(500)
    if accelerometer.was_gesture('shake'):
        uart.write('C')
        sleep(500)
    if uart.any():
        data = uart.read(1)
        if data:
            if data[0] == ord('h'):
                display.show(Image.HEART)
                sleep(500)
                display.show(Image.HAPPY)
```

Y este código en *p5.js*:
```javascript
let port;
let connectBtn;

function setup() {
    createCanvas(400, 400);
    background(220);
    port = createSerial();
    connectBtn = createButton('Connect to micro:bit');
    connectBtn.position(80, 300);
    connectBtn.mousePressed(connectBtnClick);
    let sendBtn = createButton('Send Love');
    sendBtn.position(220, 300);
    sendBtn.mousePressed(sendBtnClick);
    fill('white');
    ellipse(width / 2, height / 2, 100, 100);
}

function draw() {

    if(port.availableBytes() > 0){
        let dataRx = port.read(1);
        if(dataRx == 'A'){
            fill('red');
        }
        else if(dataRx == 'B'){
            fill('yellow');
        }
        else{
            fill('green');
        }
        background(220);
        ellipse(width / 2, height / 2, 100, 100);
        fill('black');
        text(dataRx, width / 2, height / 2);
    }


    if (!port.opened()) {
        connectBtn.html('Connect to micro:bit');
    }
    else {
        connectBtn.html('Disconnect');
    }
}

function connectBtnClick() {
    if (!port.opened()) {
        port.open('MicroPython', 115200);
    } else {
        port.close();
    }
}

function sendBtnClick() {
    port.write('h');
}
```
Se crea un sistema físico interactivo que tiene los siguientes inputs, outputs, y proceso(s)

#### Inputs
* *Desde p5.js:*
  * Botón "Connect to micro:bit"
  * Botón "Disconnect"
  * Botón "Send Love"
* *Desde el micro:bit:*
  * Botón A
  * Botón B
  * Acción de "Shake"
#### Outputs
* *Visibles en el micro:bit:*
  * Carita feliz (por defecto)
  * Corazón (al presionar "Send Love")
* *Visibles en p5.js:*
  * Círculo Blanco (por defecto)
  * Círculo Rojo (al presionar "A")
  * Círculo Amarillo (al presionar "B")
  * Círculo Verde (al hacer "Shake")
#### Proceso(s)
Esta parte no estoy seguro de si se puede categorizar igual en "lo que pasa en *micro:bit*" y "lo que pasa en *p5.js*", porque creo que ambos están constantemente trabajando en conjunto. El *micro:bit* está "atento" al input de "Send Love", pero también está preparado para enviarle a *p5.js* sus inputs de A, B y Shake. Por el otro lado, *p5.js* está "atento" a esos inputs del *micro:bit*, pero también está a cargo de enviar el input de "Send Love".  
Algo que sí creo que se puede mencionar es el "subproceso" (no creo que sea válido llamarlo así pero equis) antes de que se conecte el *micro:bit* al PC. Este es un momento a parte que solo importa a *p5.js*, donde solicita al usuario realizar la conexión con el *micro:bit* y, una vez realizada, abre el puerto serial y lo configura para poder comunicarse adecuadamente.

## Actividad 04
### Generando patrones visuales

