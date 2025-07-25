# Unidad 1

## 🛠 Fase: Apply

### Actividad 05

#### ¿Cómo funciona el sistema físico interactivo que acabamos de crear?
Este Sistema Físico Interactivo logra cambiar el color de un cuadrado dibujado en p5 cuando un botón es presionado en el micro:bit.  
Para ello, primero *[PENDING]*

Describir como un sistema de 2 computadores - (cada uno con input y output) y procesamiento, cada input se debe procesar, como? eso se explica
 
### Actividad 06

#### Control de movimiento con micro:bit
Crea un programa en p5.js que muestre un círculo en la pantalla. Utiliza los botones A y B del micro:bit para controlar la posición en x del círculo en el canvas de p5.js.

- [**Programa de p5**](https://editor.p5js.org/MAG-02/sketches/QpZAfGesH)
- **Código del programa:**
```javascript
let port;
let connectBtn;
let connectionInitialized = false;
let x = 200;

function setup() {
  createCanvas(400, 400);
  background(220);
  port = createSerial();
  connectBtn = createButton("Connect to micro:bit");
  connectBtn.position(80, 300);
  connectBtn.mousePressed(connectBtnClick);
}

function draw() {
  background(220);

  if (port.opened() && !connectionInitialized) {
    port.clear();
    connectionInitialized = true;
  }

  if (port.availableBytes() > 0) {
    let dataRx = port.read(1);
    if (dataRx == "A") {
      fill("green");
      x -= 10;
    } else if (dataRx == "B") {
      fill("green");
      x += 10;
    } else {
      fill("red")
    }
  }

  ellipseMode(CENTER);
  ellipse(x, height / 2, 50)
  
  if (!port.opened()) {
    connectBtn.html("Connect to micro:bit");
  } else {
    connectBtn.html("Disconnect");
  }
}

function connectBtnClick() {
  if (!port.opened()) {
    port.open("MicroPython", 115200);
    connectionInitialized = false;
  } else {
    port.close();
  }
}
```
- **Código del micro:bit:**
```python
# Imports go at the top
from microbit import *

uart.init(baudrate=115200)
display.show(Image.PACMAN)

# Code in a 'while True:' loop repeats forever
while True:

    if button_a.is_pressed():
        uart.write('A')
    elif button_b.is_pressed():
        uart.write('B')
    else:
        uart.write('N')

    sleep(100)
```
