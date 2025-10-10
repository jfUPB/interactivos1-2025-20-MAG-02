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
#### Explica con tus propias palabras: ¿Por qué es necesario Dev Tunnels en este escenario y cómo funciona conceptualmente?
Dev Tunnels lo que hace es conectar 2 dispositivos de forma segura y externa a ambos y a la red en la que están conectados. La única otra manera de conectar 2 dispositivos así sería usando las *IP*s individuales (estando en la misma red) pero es posible que algún *firewall* detenga el proceso.  
Dev Tunnels funciona únicamente como un túnel de información, pasando la información que recibe de un dispositivo a otro, pero sin dar directamente la "información sensible" de ninguno de los dispositivos.
#### Describe la función de touchMoved() y por qué se usa la variable threshold en el cliente móvil.
La función `touchMoved()` se llama continuamente mientras el usuario esté tocando la pantalla y moviéndose, es decir, no funciona solo con tocar la pantalla, sino que espera específicamente que haya movimiento.  
El uso de `threshold` sí es limitado a dispositivos móviles porque un mouse será más estable que un toque a la pantalla con un dedo. Existe para evitar que la aplicación se esté actualizando constantemente por cambios mínimos en el contacto o la posición del dedo sobre la pantalla, que muchas veces no son ni  siquiera intencionales. 
#### Compara brevemente Dev Tunnels con simplemente usar la IP local. ¿Cuáles son las ventajas y desventajas de cada uno?
La primera y más clara sería poder conectar 2 dispositivos en cualquier lugar sin ninguna restricción de red o ubicación, que es básicamente la gracia de *Dev Tunnels*. La segunda, es la mayor seguridad respecto a la información "sensible" del dispositivo en el que está el servidor, ya que compartir la *IP* de este puede resultar en usos maliciosos o accesos no deseados (no sé si directamente al dispositivo, pero en general pasarían cosas malas :p)
#### Coloca en tu bitácora capturas de pantalla del sistema completo funcionando. Esto lo puedes hacer abriendo tanto el mobile como el desktop en tu computador y tomando una captura de pantalla de todos los involucrados (celular, computador y terminal).
Vista en `https://zvsmgggn-3000.use2.devtunnels.ms/destop`:  
<img width="446" height="475" alt="image" src="https://github.com/user-attachments/assets/02122284-458f-4cbb-9cad-d91a4f0abb8b" />

Vista en `https://zvsmgggn-3000.use2.devtunnels.ms/mobile`:  
<img width="720" height="834" alt="image" src="https://github.com/user-attachments/assets/1cd31868-cba5-4321-8d51-11704a618e27" />

*GitBash* y *Visual Studio Code*:
<img width="1276" height="729" alt="image" src="https://github.com/user-attachments/assets/40ef9482-6850-4cd3-9968-b7ace09b5734" />

Habiendo subido esta imagen, noté que no había puesto Público el puerto "Forwardeado", lo que explica por qué tuve que iniciar sesión en *GitHub* antes de conectarme al *DevTunnel*.



