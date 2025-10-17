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

## Actividad 03
#### ¿Cuál es la función principal de express.static(‘public’) en este servidor? ¿Cómo se compara con el uso de app.get(‘/ruta’, …) del servidor de la Unidad 6?
`express.static('public')` es la línea que establece que las solicitudes de los distintos clientes hechas al servidor serán "enrutadas" hacia la carpeta `public`, y dentro de esta podrán encontrar `desktop` o `mobile` según la ruta que establezca el usuario. Esto se puede hacer porque dentro de cada subcarpeta de `public` están los índices `index.html` que abrirá el navegador y sketch `sketch.js` que hace funcionar la página con el server.  
Respecto a usar `app.get('/ruta', ...)`, este método ahorra el tener una carpeta dedicada `views` y además tener que dedicar un pequeño pedazo de código para cada vista. En la unidad anterior cada página hacía la solicitud de las bibliotecas necesarias que estaban ubicadas en la carpeta `public`.
#### Explica detalladamente el flujo de un mensaje táctil: ¿Qué evento lo envía desde el móvil? ¿Qué evento lo recibe el servidor? ¿Qué hace el servidor con él? ¿Qué evento lo envía el servidor al escritorio? ¿Por qué se usa socket.broadcast.emit en lugar de io.emit o socket.emit en este caso?
La función encargada de enviar los mensajes desde el móvil es `touchMoved()`:
```js
function touchMoved() {
    if (socket && socket.connected) { 
        let dx = abs(mouseX - lastTouchX);
        let dy = abs(mouseY - lastTouchY);

        if (dx > threshold || dy > threshold || lastTouchX === null) {
            let touchData = {
                type: 'touch',
                x: mouseX,
                y: mouseY
            };
            socket.emit('message', touchData);

            lastTouchX = mouseX;
            lastTouchY = mouseY;
        }
    }
    return false;
}
```
Esta función específicamente *solo* envía información (`socket.emit('message', touchData)`) cuando el usuario está tocando la pantalla **y se mueve** más que un *threshold* especificado. También verifica que `socket && socket.connected` sean *True*.  
En el servidor, este pedacito de código es el que está atento a los mensajes:
```js
socket.on('message', (message) => {
        console.log('Received message =>', message);
        socket.broadcast.emit('message', message);
    });
```
Y lo que hace es imprimir el mensaje recibido en la consola y luego reenviarlo, o más bien, *broadcast*earlo. La razón de usar *broadcast* en vez de algún *emit* directo es para poder tener funcionalidad con varios dispositivos a la vez (estén en `/desktop` o `/mobile`).
#### Si conectaras dos computadores de escritorio y un móvil a este servidor, y movieras el dedo en el móvil, ¿Quién recibiría el mensaje retransmitido por el servidor? ¿Por qué?
De nuevo, debido al `socket.broadcast.emit(...)`, ambos computadores de escritorio recibirán el mensaje, y ambos se actualizarán acorde. De hecho, realicé el experimento con mi compañero Jhon en clase, y funcionó en ambos sentidos (2 clientes en `/desktop`, luego 2 clientes en `/mobile`).
#### ¿Qué información útil te proporcionan los mensajes console.log en el servidor durante la ejecución?
El servidor envía a la consola 4 mensajes distintos, siendo uno de ellos el puerto al que se conectó, y los otros 3 reacciones a los clientes. Envía un mensaje al conectarse y desconectarse un cliente, pero el mensaje más común es su "Received message =>". Los logs se ven así:
```bash
Server is listening on http://localhost:3000
New client connected
Received message => { type: 'touch', x: 129, y: 213 }
Client disconnected
```
El mensaje "Received message =>" trae las coordenadas del `touch` realizado por el usuario, que son necesarias para que el `/desktop` pueda recalcular la posición del círculo en pantalla.

## Actividad 04
#### Realiza un diagrama donde muestres el flujo completo de datos y eventos entre los tres componentes: móvil, servidor y escritorio. Puedes ilustrar con un ejemplo de coordenadas táctiles (x, y) y cómo viajan a través del sistema.
Primero que nada, desde el cliente `/mobile` se envía un mensaje con el tag `'message'`. Este mensaje carga 3 cosas: Un *type* (`'touch'`), y 2 coordenadas `x, y`.
```js
if (dx > threshold || dy > threshold || lastTouchX === null) {
    let touchData = {
        type: 'touch',
        x: mouseX,
        y: mouseY
    };
    socket.emit('message', touchData);

    lastTouchX = mouseX;
    lastTouchY = mouseY;
}
```
Este mensaje pasa primero por el `server.js`. Ahí, el servidor lo imprime en la consola y lo emite como un broadcast:
```js
socket.on('message', (message) => {
    console.log('Received message =>', message);
    socket.broadcast.emit('message', message);
});
```
Ahora, el mensaje llega al cliente `/desktop`, el cual lo recibe con este código:
```js
socket.on('message', (data) => {
    console.log(`Received message:`, data);
    if (data && data.type === 'touch') {
        circleX = data.x;
        circleY = data.y;
    }
});
```
Y toma directamente las coordenadas del toque del usuario en `/mobile` para asignárselas al círculo en pantalla. Así de simple es :p

## Actividad 05




