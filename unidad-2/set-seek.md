# Unidad 2
## Introducción 📜
En esta unidad vamos a profundizar un poco más en la programación del computador embebido o micro:bit. Vamos a estudiar una técnicas de programación basada en máquinas de estados que nos permitirá crear programas más complejos y con mayor control sobre el flujo de ejecución. Esta técnica de programación no es exclusiva del micro:bit, sino que se utiliza en muchos otros lenguajes de programación y plataformas, por lo que es una habilidad valiosa para cualquier ingeniero en diseño de entretenimiento digital. En la próxima unidad verás cómo podrás transferir esta técnica a otros lenguajes de programación y plataforma.

## 🔎 Fase: Set + Seek

### Set: ¿Qué aprenderás en esta unidad? 💡
Vas a resolver problemas de programación en el micro:bit utilizando máquinas de estados.

### Actividad 01
1. **Describe detalladamente cómo funciona este ejemplo.**  
Este ejemplo crea 2 objetos `Pixel`, los inicializa con coordenadas e intervalos diferentes, y luego los actualiza constantemente por medio de un while. Algo notorio en el código es que no utiliza `sleep()`, sino intervalos de tiempo que no se interrumpen entre sí.
2. **¿Cuáles son los estados en el programa?**  
Está el estado `WaitTimeout` y el pseudo-estado `Init`.
3. **¿Cuáles son los eventos/inputs en el programa?**  
Sólo hay un evento, que es cuando pasa el tiempo especificado en el intervalo (`if utime.ticks_diff()`).
4. **¿Cuáles son las acciones en el programa?**  
El conteo del tiempo/"mirar la hora" (`self.startTime`), cambiar el estado de los Pixeles (`self.pixelState`), cambiar el estado del objeto (`self.state`)

### Actividad 02
**Implementando un semáforo con máquina de estados**  
Implementemos juntos un semáforo simple (rojo, amarillo, verde) utilizando una máquina de estados en Micropython. Representaremos cada color del semáforo con un LED del display del micro:bit.  

El primer intento de hacer el semáforo me quedó lleno de machetazos y cosas que *en teoría* deberían funcionar, pero que no funcionan :c  
Aquí está el código, se hizo lo que se pudo 🫡  
```c++
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
        if self.state == "Espera":
            self.pixelState = 9
            self.startTime = utime.ticks_ms()
            self.state = "Activo"
            display.set_pixel(self.pixelX,self.pixelY,self.pixelState)
            
            display.set_pixel(0, 0, 9)

        elif self.state == "Activo":
            if utime.ticks_diff(utime.ticks_ms(),self.startTime) > self.interval:
                self.state = "Espera"
                current = self.nextColor
                

                self.pixelState = 0
                display.set_pixel(self.pixelX,self.pixelY,self.pixelState)

                display.set_pixel(0, 0, 0)

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
