# Evidencias de la unidad 8

## Actividad 01
### 1. Documenta los referentes visuales que te inspiren.
Para la creación de visuales de música siempre he tenido en mente los visualizadores de barras, específicamente los "tradicionales" como [este](https://www.youtube.com/watch?v=-Yk7JLzsaqw), que parecen pequeños ladrillitos o barras más pequeñas y que van cambiando de color al subir.
<img width="1919" height="1079" alt="image" src="https://github.com/user-attachments/assets/331ae7b5-31bc-4c55-8179-a56c8db915d4" />
También como referencia tengo en mente estos gráficos de barras que forman un círculo. No sé explicarlo más a detalle, así que mejor mostrar un [ejemplo](https://www.youtube.com/watch?v=avXQPMNIj-k).
<img width="1919" height="1079" alt="image" src="https://github.com/user-attachments/assets/0a7c6b1d-0f48-4931-a5ca-e0de1824a2f8" />

Además de eso, también pienso en juegos de música como [este](https://www.youtube.com/watch?v=5mDjFdetU28), llamado *Super Hexagon*...
<img width="1919" height="1079" alt="image" src="https://github.com/user-attachments/assets/2a17434a-1058-4065-9c34-b3fe95b04a6f" />
...o [este](https://www.youtube.com/watch?v=yznyQwCLnaM), llamado *Geometry Dash*.
<img width="1919" height="1079" alt="image" src="https://github.com/user-attachments/assets/cc1967f9-4ebf-4561-8fd4-96ae178a0799" />

Ambos juegos presentan gráficos frenéticos y muy coloridos, que reaccionan a los altos y bajos de la música e incluso, en cierta forma, a la interacción del jugador. Entiendo que ambos conceptos son bastante complejos de emular, pero definitivamente diría que esos son mis referentes e inspiraciones.

### 2. Define el concepto de las visuales que quieres crear.
Me interesaría mucho crear algo similar a un diagrama de barras pero en una forma hexagonal, pero realmente no tengo la menor idea de cómo hacerlo :\  
Creo que, por cuestiones de tiempo y pensando en mi habilidad, me limitaré a hacer una gráfica de barras, de pronto que sea también circular, pero que sea simple. La interacción que deseo permitiría rotar el diagrama desde el dispositivo móvil, y pausar/empezar la canción y menejar el volumen (y, por ende, el gráfico) desde el *micro:bit*.

### 3. Explica cómo el móvil y el micro:bit controlarán las visuales.
Desde el **móvil**:
* Tocar la pantalla (`touchStarted()`) "soltará" el gráfico para permitirle rotar. Es decir, si no se está tocando la pantalla, el gráfico va a desacelerar lentamente o frenar por completo (no he decidido, dependerá de qué logro crear).
* Por ende, dejar de tocar la pantalla (`touchEnded()`) aplicará esa desaceleración progresiva que mencioné. Si el usuario está tocando la pantalla, la desaceleración no entrará en efecto.
* Y, por último, mover el dedo sobre la pantalla (`touchMoved()`) añadirá una velocidad especificada en la dirección específica hacia donde mueva el dedo el usuario. Pienso que acá debo tener un threshold de la distancia mínima para contar el movimiento.

Desde el ***micro:bit***:
* Realizar un `shake` va a empezar o pausar la canción, lo que es una funcionalidad realmente fácil de implementar.
* Presionar el botón `A` disminuirá el volumen, y el botón `B` lo aumentará. Es una funcionalidad simple pero que presentará cambios inmediatos en el diagrama final.

### 4. Haz un boceto de todas las interfaces del sistema.
Bocetos hechos en Paint:
<img width="1205" height="591" alt="image" src="https://github.com/user-attachments/assets/47ddc178-0ee7-46b6-8f84-113d662ce815" />

### 5. Haz un diagrama que explique cómo se comunicarán los diferentes componentes del sistema.
![Diagrama de Flujo](FlujoDelSistema.png)

