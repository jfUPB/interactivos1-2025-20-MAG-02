# Unidad 3


## 🛠 Fase: Apply

### Actividad 06
#### Crear la bomba en p5.js
**En esta actividad vas a transferir la técnica de programación con máquinas de estado a p5.js.**  

```javascript
//INIT ------------------------------
// -- Variables --
//p5
let validChars = "ABST";

//Bomba
let count = 20;
let password = ["A", "B", "A"];
let llave = [" ", " ", " "];
let index = 0;
let state = "CONFIG";
let startTime;

// -- Funciones --
function setup() {
  createCanvas(400, 400);
  background(220);
  textAlign(CENTER);
}

function draw() {
  //Setup general
  background(220);
  textSize(12);
  text("Press A,B,S,T to simulate micro:bit keys", width/2, height - height/3);
  
  //Texto por Estados
  if (state == "CONFIG") {
    textSize(40);
    text(count, width/2, height/2);
    textSize(10)
    text("CONFIG", 20, height-2)
  }
  
  else if (state == "ARMED") {
    textSize(70);
    text(count, width/2, height/2);
    textSize(10)
    text("ARMED", 19, height-2)
    
    let now = millis();
    if (now - startTime >= 1000) {
      startTime = now;
      count -= 1;
      
      if (count <= 0) {
        state = "EXPLODED"
      }
    }
    
    if (index == password.length) {
      let passIsOK = true;
      for (i = 0; i < password.length; i += 1) {
        if(llave[i] != password[i]) {
          passIsOK = false;
          index = 0;
          break;
        }
      }
      if (passIsOK == true) {
        index = 0;
        count = 20;

        state = "CONFIG";
      }
    }
  }
  
  else if (state == "EXPLODED") {
    textSize(30);
    text("Nah bro, mala tuya :c", width/2, height/2);
    textSize(10)
    text("EXPLODED", 27, height-2)
  }
}

function keyPressed() {
  keyValue = key.toUpperCase();
  if(validChars.includes(keyValue)){
    bombTask(keyValue);
  }
}

//BOMBA ------------------------------
function bombTask(keyValue) {
  if (state == "CONFIG"){
    if (keyValue == "A" && count < 60) {
      count += 1;
    }
    else if (keyValue == "B" && count > 10) {
      count -= 1;
    }
    else if (keyValue == "S") {
      state = "ARMED"
      startTime = millis();
    }
  }
  
  else if (state == "ARMED"){
    if (keyValue == "A" || keyValue == "B") {
      llave[index] = keyValue;
      index += 1;
    }
  }
  
  else if (state == "EXPLODED"){
    if (keyValue == "T") {
      index = 0;
      count = 20;

      state = "CONFIG";
    }
  }
}
```


