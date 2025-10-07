# Evidencias de la unidad 7

## Actividad 01
#### ¿Qué URL de Dev Tunnels obtuviste? ¿Por qué crees que necesitamos usar esta URL en lugar de http://localhost:3000 o la IP local de tu computador para que el celular se conecte?
Mi URL de *Dev Tunnels* fue `https://p38zf773-3000.use2.devtunnels.ms/`. Usar una URL específica es necesario para distinguir a cada usuario dentro de los servidores en la nube de Microsoft, y no usamos el `http://localhost:3000` ni una IP local porque el dispositivo externo (en este caso, celular) no podría acceder/enviar información al computador porque este estaría protegido.
#### Describe brevemente qué hace npm install y npm start.
#### ¿Qué mensajes observaste en la terminal del servidor al conectar el cliente de escritorio y el cliente móvil? ¿Eran diferentes los mensajes o identificadores?
Primero conecté mi celular, y me salió `New client connected`. Después conecté el PC, y también me salió `New client connected`, y me preocupé porque no vi ningún identificador, pero resulta que simplemente no estamos creando/usando identificadores. Eso permite que cualquier persona y cualquier cantidad de clientes se pueden conectar e interactuar con el servidor a través de los *Dev Tunnels*.  
#### Describe el comportamiento observado: ¿Funcionó la interacción? ¿Hubo algún retraso (latencia)?
El comportamiento fue simple: Al tocar la pantalla del celular (cliente `/mobile`), se movía un círculo rojo en el computador (cliente `/desktop`). La interacción funcionó sin problema, y la única "latencia" que sentí resultó ser intencional, pues el código intenta no enviar un mensaje si la distancia movida es muy pequeña, es decir, se demora en enviar un mensaje el tiempo que uno se demore en mover el dedo una distancia especificada.

## Actividad 02
> Leer info preia en la actividad
#### Explica con tus propias palabras: ¿Por qué es necesario Dev Tunnels en este escenario y cómo funciona conceptualmente?
#### Describe la función de touchMoved() y por qué se usa la variable threshold en el cliente móvil.
#### Compara brevemente Dev Tunnels con simplemente usar la IP local. ¿Cuáles son las ventajas y desventajas de cada uno?
#### Coloca en tu bitácora capturas de pantalla del sistema completo funcionando. Esto lo puedes hacer abriendo tanto el mobile como el desktop en tu computador y tomando una captura de pantalla de todos los involucrados (celular, computador y terminal).
