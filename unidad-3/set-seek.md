# Unidad 3

## 🔎 Fase: Set + Seek

## Actividad 01
### Volvamos a la actividad del semáforo
Verersión propia del semáforo anterior:
```python
from microbit import *
import utime

class Pixel:
    def __init__(self, next, pixelX,pixelY,initState,interval):
        self.state = "Espera"
        self.nextColor = next
        self.startTime = 0
        self.interval = interval
        self.pixelX = pixelX
        self.pixelY = pixelY
        self.pixelState = initState

    def update(self):
        global current #Literalmente SOLO TUVE QUE AGREGAR ESTO
        
        if self.state == "Espera":
            self.pixelState = 9
            self.startTime = utime.ticks_ms()
            self.state = "Activo"
            display.set_pixel(self.pixelX,self.pixelY,self.pixelState)
            
            #display.set_pixel(0, 0, 9)

        elif self.state == "Activo":
            if utime.ticks_diff(utime.ticks_ms(),self.startTime) > self.interval:
                self.state = "Espera"
                current = self.nextColor
                

                self.pixelState = 0
                display.set_pixel(self.pixelX,self.pixelY,self.pixelState)

                #display.set_pixel(0, 0, 0)

pixel1 = Pixel("Yellow", 2,0,0,5000)
pixel2 = Pixel("Red", 2,1,0,2500)
pixel3 = Pixel("Green", 2,2,0,10000)

current = "Green"

while True:
    if current == "Green":
        pixel1.update()
    elif current == "Yellow":
        pixel2.update()
    elif current == "Red":
        pixel3.update()
```
Ejercicio de Semáforos Concurrentes terminado:
```python
from microbit import *
import utime

class Semaforo:
    def __init__(self, tr, ta, tv, col):
        self.tr = tr
        self.ta = ta
        self.tv = tv
        self.col = col
        display.set_pixel(self.col, 0, 9)
        self.startTime = utime.ticks_ms()
        self.state = "WaitInRed"
        
    def update(self):
        if self.state == "WaitInRed":
            if utime.ticks_diff(utime.ticks_ms(), self.startTime) >= self.tr:
                display.set_pixel(self.col, 0, 0)
                display.set_pixel(self.col, 1, 9)
                
                self.startTime = utime.ticks_ms()
                self.state = "WaitInYellow"

        if self.state == "WaitInYellow":
            if utime.ticks_diff(utime.ticks_ms(), self.startTime) >= self.ta:
                display.set_pixel(self.col, 1, 0)
                display.set_pixel(self.col, 2, 9)
                
                self.startTime = utime.ticks_ms()
                self.state = "WaitInGreen"

        if self.state == "WaitInGreen":
            if utime.ticks_diff(utime.ticks_ms(), self.startTime) >= self.tv:
                display.set_pixel(self.col, 2, 0)
                display.set_pixel(self.col, 0, 9)
                
                self.startTime = utime.ticks_ms()
                self.state = "WaitInRed"

class SemaforoM:
    def __init__(self, tr, ta, tv, col):
        self.tr = tr
        self.ta = ta
        self.tv = tv
        self.col = col
        display.set_pixel(self.col, 0, 9)
        self.startTime = utime.ticks_ms()
        self.state = "WaitInRed"
        
    def update(self):
        if self.state == "WaitInRed":
            if utime.ticks_diff(utime.ticks_ms(), self.startTime) >= self.tr:
                display.set_pixel(self.col, 0, 0)
                display.set_pixel(self.col, 2, 9)
                
                self.startTime = utime.ticks_ms()
                self.state = "WaitInGreen"

        if self.state == "WaitInGreen":
            if utime.ticks_diff(utime.ticks_ms(), self.startTime) >= self.tv:
                display.set_pixel(self.col, 2, 0)
                display.set_pixel(self.col, 1, 9)
                
                self.startTime = utime.ticks_ms()
                self.state = "WaitInYellow"

        if self.state == "WaitInYellow":
            if utime.ticks_diff(utime.ticks_ms(), self.startTime) >= self.ta:
                display.set_pixel(self.col, 1, 0)
                display.set_pixel(self.col, 0, 9)
                
                self.startTime = utime.ticks_ms()
                self.state = "WaitInRed"

semaforo1 = Semaforo(5000, 2000, 3000, 0)
semaforo2 = Semaforo(3000, 1000, 2000, 1)
semaforo3 = Semaforo(4000, 3000, 2000, 2)

semaforo4 = SemaforoM(3000, 1500, 3000, 4)

while True:
    semaforo1.update()
    semaforo2.update()
    semaforo3.update()
    semaforo4.update()
```

### Estructura general de tabla
|       | Hola! | Adiós!|
-----|
|Español| Hola! | Adiós!|
|---|
|Inglés | Hello!|Goodbye|
