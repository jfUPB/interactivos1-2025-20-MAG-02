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

### Actividad 03
#### Controlando la pantalla con una máquina de estados y concurrencia
```python
# Imports go at the top
from microbit import *
import utime

STATE_INIT = 0
STATE_HAPPY = 1
STATE_SMILE = 2
STATE_SAD = 3

currentState = STATE_INIT
startTime = 0
intervalHappy = 1500
intervalSmile = 1000
intervalSad   = 2000

def tarea1():
    global currentState
    global startTime
    
    if currentState == STATE_INIT:
        display.show(Image.HAPPY)
        startTime = utime.ticks_ms()
        currentState = STATE_HAPPY
        
    elif currentState == STATE_HAPPY:
        if button_a.was_pressed():
            display.show(Image.SAD)
            startTime = utime.ticks_ms()
            currentState = STATE_SAD
            
        elif utime.ticks_diff(utime.ticks_ms(), startTime) > intervalHappy:
            display.show(Image.SMILE)
            startTime = utime.ticks_ms()
            currentState = STATE_SMILE
        
    elif currentState == STATE_SMILE:
        if utime.ticks_diff(utime.ticks_ms(), startTime) > intervalSmile:
            display.show(Image.SAD)
            startTime = utime.ticks_ms()
            currentState = STATE_SAD

        elif button_a.was_pressed():
            display.show(Image.HAPPY)
            startTime = utime.ticks_ms()
            currentState = STATE_HAPPY
        
    elif currentState == STATE_SAD:
        if button_a.was_pressed():
            display.show(Image.SMILE)
            startTime = utime.ticks_ms()
            currentState = STATE_SMILE
            
        elif utime.ticks_diff(utime.ticks_ms(), startTime) > intervalSad:
            display.show(Image.HAPPY)
            startTime = utime.ticks_ms()
            currentState = STATE_HAPPY
        
    else:
        display.show(Image.SKULL)
        #currentState = STATE_INIT

# Code in a 'while True:' loop repeats forever
while True:
    tarea1()
```
- **Explica por qué decimos que este programa permite realizar de manera concurrente varias tareas.**  
  Debido a que nunca utiliza métodos como `sleep()`, que no permitirían que nada más suceda por un lapso de tiempo. Cada frame el programa intenta ejecutar sus distintos objetivos sin interponerse sobre otros o interrumpirlos.
- **Identifica los estados, eventos y acciones en el programa.**
  - **Estados:** Init (es un pseudo-estado), Happy, Smile, y Sad.
  - **Eventos:** Todos los eventos son el paso de lapsos de tiempo específicos para cada estado.
  - **Acciones:** El Display de la imagen específica, iniciar el respectivo contador.
- **Describe y aplica al menos 3 vectores de prueba para el programa. Para definir un vector de prueba debes llevar al sistema a un estado, generar los eventos y observar el estado siguiente y las acciones que ocurrirán. Por tanto, un vector de prueba tiene unas condiciones iniciales del sistema, unos resultados esperados y los resultados realmente obtenidos. Si el resultado obtenido es igual al esperado entonces el sistema pasó el vector de prueba, de lo contrario el sistema puede tener un error.**
  - **Vector 1:** Estado Init.  
    El programa empieza en el estado Init, y debe pasar correctamente al estado Happy. No hay condiciones iniciales específicas, pues es el momento inicial del programa.  
    El resultado esperado es que el programa pase al estado Happy y aparezca en el *micro:bit* una carita feliz :>  
    Este vector de prueba fue verificado en clase.



