
# Evidencias de la unidad 6

## Actividad 01
### Preparación del entorno y primer contacto

#### ¿Qué ocurrió en la terminal cuando ejecutaste npm install? ¿Cuál crees que es su propósito?
Bueno, vamos a instalar wooo! Apenas ejecuté el comando me salió este mensaje:
```
added 120 packages, and audited 121 packages in 3s

17 packages are looking for funding
  run `npm fund` for details

found 0 vulnerabilities
npm notice
npm notice New major version of npm available! 10.2.0 -> 11.6.0
npm notice Changelog: <https://github.com/npm/cli/releases/tag/v11.6.0>
npm notice Run `npm install -g npm@11.6.0` to update!
npm notice
```
Y haciendo el mismo proceso en el PC de mi casa me salió el siguiente mensaje:
```
added 120 packages, and audited 121 packages in 22s

17 packages are looking for funding
  run `npm fund` for details

found 0 vulnerabilities
npm notice
npm notice New major version of npm available! 10.9.3 -> 11.6.1
npm notice Changelog: https://github.com/npm/cli/releases/tag/v11.6.1
npm notice To update run: npm install -g npm@11.6.1
npm notice
```
Un poco diferente pero no cambia nada importante, la verdad. Solo sé que mi PC parece ser más lento :c

Luego de que causalmente no le funcionara a mi compañero David, descubrimos que `npm install` es un comando relacionado en alguna manera a *Node.js*. Probablemente se encargue de instalar las "herramientas" necesarias para correr el caso de estudio.

#### ¿Qué mensaje específico apareció en la terminal después de ejecutar npm start? ¿Qué indica este mensaje?
Salió el siguiente mensaje:
```
> nodejs-test-1@1.0.0 start
> node server.js

Server is listening on http://localhost:3000
```
El mensaje seguramente crea un servidor y me avisa/informa que lo creó y que está "escuchando" o pendiente de recibir información.

#### Describe lo que ves inicialmente en page1 y page2 en tu navegador.
Veo 2 círculos grises con relleno rojo, unidos por una línea también gris. Eso es cuando tengo una de las pestañas en pantalla completa; cuando están minimizadas, cada pestaña muestra un círculo específico, y ambos círculos se mantienen unidos por la línea gris sin importar la posición de las pestañas.

#### ¿Qué mensajes aparecieron en la terminal del servidor cuando abriste page1 y page2?
Me tocó volver a abrir la pestaña, pero me salió esto al conectar una pestaña en `http://localhost:3000/page1`:
```
A user connected - ID: ThU3Ba6u_LejkM0oAAAF
Received win1update from ID: ThU3Ba6u_LejkM0oAAAF Data: { x: 1054, y: 147, width: 500, height: 386 }
Debug - Connected clients: 1, Page1: 1, Page2: 0, Synced: 0
Sync status: pages=false, synced=false, clients=1
Debug - Connected clients: 1, Page1: 1, Page2: 0, Synced: 1
Sync status: pages=false, synced=true, clients=1
```
Y esto al abrir otra en `http://localhost:3000/page2`:
```
A user connected - ID: cPG3cuK8nPFnN8GNAAAH
Received win2update from ID: cPG3cuK8nPFnN8GNAAAH Data: { x: 1185, y: 360, width: 500, height: 386 }
Debug - Connected clients: 2, Page1: 1, Page2: 1, Synced: 1
Sync status: pages=true, synced=false, clients=2
Debug - Connected clients: 2, Page1: 1, Page2: 1, Synced: 1
Sync status: pages=true, synced=false, clients=2
Debug - Connected clients: 2, Page1: 1, Page2: 1, Synced: 2
All clients are fully synced
```

#### Describe qué sucede en ambas páginas del navegador cuando mueves una de las ventanas. ¿Cambia algo visualmente? ¿Qué mensajes aparecen (si los hay) en la consola del navegador (usualmente accesible con F12 -> Pestaña Consola) y en la terminal del servidor?
Sí pasa algo! En mi caso, la línea va cambiando su dirección para seguir uniendo ambos círculos. En mi terminal de git bash sale esta tanda de mensajes al mover una ventana (específicamente, la 2):
```
Received win2update from ID: cPG3cuK8nPFnN8GNAAAH Data: { x: 1175, y: 271, width: 500, height: 386 }
Debug - Connected clients: 2, Page1: 1, Page2: 1, Synced: 2
All clients are fully synced
Debug - Connected clients: 2, Page1: 1, Page2: 1, Synced: 2
All clients are fully synced
```
Lo de `All clients are fully synced` seguramente sale 2 veces porque el programa chequea cada cierto tiempo.  
En la consola del navegador, sale esto:
```
Received valid remote data: {x: 225, y: 157, width: 500, height: 386}
Sync status: SYNCED
```
Y si muevo específicamente la pestaña en la que abrí la consola, solo se repite y se repite `Sync status: SYNCED`.

## Actividad 02
### Viaje Conceptual
#### Piensa en cómo te conectas a Internet en casa o en la Universidad. ¿Usas Wi-Fi? ¿Un cable de red? Eso es simplemente tu “rampa de acceso” a la gran red de carreteras. ¿Qué pasaría si esa rampa se corta? Anota tus ideas.
#### ¿Puedes identificar otros ejemplos de relaciones `Cliente-Servidor` en tu vida diaria (no necesariamente digitales)? Por ejemplo, al pedir comida en un restaurante. ¿Quién es el cliente y quién el servidor? ¿Qué se pide y qué se entrega?
#### Toma la URL de tu sitio web favorito. Intenta identificar el protocolo, el nombre de dominio y la ruta (si la hay). ¿Qué crees que pasa si solo escribes el nombre de dominio (ej. `www.google.com`) sin una ruta específica? ¿Qué “página por defecto” crees que te envía el servidor?

Compara HTTP con los protocolos seriales que usaste.
#### ¿Qué similitudes encuentras?
#### ¿Qué diferencias clave ves?
#### ¿Por qué crees que HTTP necesita ser más complejo que un simple envío de bytes como hacías con el micro:bit?

Piensa en una página web simple, como un formulario de login.
#### ¿Qué parte crees que es `HTML` (ej. los campos de texto, el botón)?
#### ¿Qué parte es `CSS` (ej. el color del botón, el tipo de letra)?
#### ¿Qué parte es `JavaScript` (ej. la comprobación de si escribiste algo antes de enviar, el mensaje de “contraseña incorrecta” que aparece sin recargar la página)?

Compara el bucle `draw()` de p5.js con este modelo de “esperar a que algo pase y reaccionar”.
#### ¿Qué ventajas crees que tiene el modelo basado en eventos para una interfaz de usuario web?
#### ¿Sería eficiente tener un bucle `draw()` redibujando toda la página 60 veces por segundo si nada ha cambiado?

#### ¿Por qué crees que podría ser útil usar JavaScript tanto en el cliente (navegador) como en el servidor? ¿Se te ocurre alguna ventaja para los desarrolladores?

#### Resume con tus propias palabras la diferencia fundamental entre una comunicación `HTTP` tradicional y una comunicación usando `WebSockets`/`Socket.IO`. ¿En qué tipo de aplicaciones has visto o podrías imaginar que se usa esta comunicación en tiempo real?
