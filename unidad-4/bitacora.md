# Evidencias de la unidad 4

## Código

[Enlace a la aplicación a modificar](https://editor.p5js.org/generative-design/sketches/P_2_0_02)

Código a modificar:

``` js
// P_2_0_02
//
// Generative Gestaltung – Creative Coding im Web
// ISBN: 978-3-87439-902-9, First Edition, Hermann Schmidt, Mainz, 2018
// Benedikt Groß, Hartmut Bohnacker, Julia Laub, Claudius Lazzeroni
// with contributions by Joey Lee and Niels Poldervaart
// Copyright 2018
//
// http://www.generative-gestaltung.de
//
// Licensed under the Apache License, Version 2.0 (the "License");
// you may not use this file except in compliance with the License.
// You may obtain a copy of the License at http://www.apache.org/licenses/LICENSE-2.0
// Unless required by applicable law or agreed to in writing, software
// distributed under the License is distributed on an "AS IS" BASIS,
// WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
// See the License for the specific language governing permissions and
// limitations under the License.

/**
 * drawing with a changing shape by draging the mouse.
 *
 * MOUSE
 * position x          : length
 * position y          : thickness and number of lines
 * drag                : draw
 *
 * KEYS
 * del, backspace      : erase
 * s                   : save png
 */
'use strict';

function setup() {
  createCanvas(720, 720);
  noFill();
  background(255);
  strokeWeight(2);
  stroke(0, 25);
}

function draw() {
  if (mouseIsPressed && mouseButton == LEFT) {
    push();
    translate(width / 2, height / 2);

    var circleResolution = int(map(mouseY + 100, 0, height, 2, 10));
    var radius = mouseX - width / 2;
    var angle = TAU / circleResolution;

    beginShape();
    for (var i = 0; i <= circleResolution; i++) {
      var x = cos(angle * i) * radius;
      var y = sin(angle * i) * radius;
      vertex(x, y);
    }
    endShape();

    pop();
  }
}

function keyReleased() {
  if (keyCode == DELETE || keyCode == BACKSPACE) background(255);
  if (key == 's' || key == 'S') saveCanvas(gd.timestamp(), 'png');
}

```

[Enlace a la aplicación modificada](https://editor.p5js.org/MAG-02/sketches/iNSjDyRH4)

Código modificado:

``` js
/**
 * drawing with a changing shape by draging the mouse.
 *
 * MOUSE
 * position x          : length
 * position y          : thickness and number of lines
 * drag                : draw
 *
 * KEYS
 * del, backspace      : erase
 * s                   : save png
 */
'use strict';

// Código para soportar el serial
let port;
let connectBtn;
let connectionInitialized = false;
let microBitConnected = false;

let debug = false;

let microBitX = 0;
let microBitY = 0;
let microBitAState = false;
let microBitBState = false;
let prevBState

const STATES = {
  WAIT_MICROBIT_CONNECTION: "WAITMICROBIT_CONNECTION",
  RUNNING: "RUNNING",
};

let appState = STATES.WAIT_MICROBIT_CONNECTION;

function setup() {
  createCanvas(720, 720);
  noFill();
  background(255);
  strokeWeight(2);
  stroke(0, 25);
  
  // Adición del serial
  port = createSerial();
  connectBtn = createButton("Connect to micro:bit");
  connectBtn.position(0, 0);
  connectBtn.mousePressed(connectBtnClick);
  
  //appState = STATES.RUNNING;
  debug = true;
}

function connectBtnClick() {
  if (!port.opened()) {
    port.open("MicroPython", 115200);
    connectionInitialized = false;
  } else {
    port.close();
  }
}

function updateBState(newBState) {
  // Generar eventos de key released
  if (newBState === false && prevBState === true) {
    background(255);
    print("B released");
  }
  
  prevBState = newBState;
}

function draw() {
  if (!port.opened()) {
    connectBtn.html("Connect to micro:bit");
    microBitConnected = false;
  } else {
    microBitConnected = true;
    connectBtn.html("Disconnect");
    
    if (port.opened() && !connectionInitialized) {
      port.clear();
      connectionInitialized = true;
      appState = STATES.RUNNING;
    }

    if (port.availableBytes() > 0) {
      let data = port.readUntil("\n");
      if (data) {
        data = data.trim();
        let values = data.split(",");
        if (values.length == 4) {
          microBitX = int(values[0]) + windowWidth / 2;
          microBitY = int(values[1]) + windowHeight / 2;
          microBitAState = values[2].toLowerCase() === "true";
          microBitBState = values[3].toLowerCase() === "true";
          updateBState(microBitBState);
          
          if (debug == true) {
            print("X = ", microBitX)
            print("Y = ", microBitY)
            print("A = ", microBitAState)
            print("B = ", microBitBState)
          }
          
        } else {
          print("No se están recibiendo 4 datos del micro:bit");
        }
      }
    }
  }
  
  switch (appState) {
    case STATES.WAIT_MICROBIT_CONNECTION:
      break;
    case STATES.RUNNING:
      if (microBitAState) {
        push();
        translate(width / 2, height / 2);

        /*
        var circleResolution = int(map(mouseY + 100, 0, height, 2, 10));
        var radius = mouseX - width / 2;
        var angle = TAU / circleResolution;
        */

        var circleResolution = int(map(microBitY + 100, 0, height, 2, 10));
        var radius = microBitX - width / 2;
        var angle = TAU / circleResolution;
        
        beginShape();
        for (var i = 0; i <= circleResolution; i++) {
          var x = cos(angle * i) * radius;
          var y = sin(angle * i) * radius;
          vertex(x, y);
        }
        endShape();

        pop();
      }
      break;
  }
}

function keyReleased() {
  if (key == 's' || key == 'S') saveCanvas(gd.timestamp(), 'png');
}
```

## Video

[Video demostratativo](https://youtu.be/uUkYU7kqrxk)




