
# Evidencias de la unidad 7

## Actividad 01

### ¿Qué URL de Dev Tunnels obtuviste? ¿Por qué crees que necesitamos usar esta URL en lugar de http://localhost:3000 o la IP local de tu computador para que el celular se conecte?

Obtuve una URL similar a: https://h7mprn73-3000.use2.devtunnels.ms/mobile/
Usamos esa dirección porque “localhost” solo funciona dentro del mismo computador, y el devtúnnels permite que otros dispositivos, como el celular, accedan al servidor desde Internet.

### Describe brevemente qué hace npm install y npm start.

npm install descarga e instala todas las dependencias necesarias del proyecto.
npm start ejecuta el servidor definido en el archivo principal (por ejemplo, server.js).

### ¿Qué mensajes observaste en la terminal del servidor al conectar el cliente de escritorio y el cliente móvil? ¿Eran diferentes los mensajes o identificadores?

Aparecieron mensajes como “New client connected”, “Received message => …” y “Client disconnected”.
Los dos clientes se conectaban con identificadores distintos, pero los mensajes eran parecidos.

### Describe el comportamiento observado: ¿Funcionó la interacción? ¿Hubo algún retraso (latencia)?

Sí, la interacción funcionó. Al mover el dedo en el celular, el círculo en el computador se movía.
Hubo muy poco o ningún retraso perceptible aunque como el profe explico en clase se debia hacer un minimo de movimiento para que el programa lo recibiera.

## Actividad 02

### Explica con tus propias palabras: ¿Por qué es necesario Dev Tunnels en este escenario y cómo funciona conceptualmente?

### Describe la función de touchMoved() y por qué se usa la variable threshold en el cliente móvil.

### Compara brevemente Dev Tunnels con simplemente usar la IP local. ¿Cuáles son las ventajas y desventajas de cada uno?

### Coloca en tu bitácora capturas de pantalla del sistema completo funcionando. Esto lo puedes hacer abriendo tanto el mobile como el desktop en tu computador y tomando una captura de pantalla de todos los involucrados (celular, computador y terminal).


## Actividad 03

### ¿Cuál es la función principal de express.static(‘public’) en este servidor? ¿Cómo se compara con el uso de app.get(‘/ruta’, …) del servidor de la Unidad 6?

### Explica detalladamente el flujo de un mensaje táctil: ¿Qué evento lo envía desde el móvil? ¿Qué evento lo recibe el servidor? ¿Qué hace el servidor con él? ¿Qué evento lo envía el servidor al escritorio? ¿Por qué se usa socket.broadcast.emit en lugar de io.emit o socket.emit en este caso?

### Si conectaras dos computadores de escritorio y un móvil a este servidor, y movieras el dedo en el móvil, ¿Quién recibiría el mensaje retransmitido por el servidor? ¿Por qué?

### ¿Qué información útil te proporcionan los mensajes console.log en el servidor durante la ejecución?

## Actividad 04

### Realiza un diagrama donde muestres el flujo completo de datos y eventos entre los tres componentes: móvil, servidor y escritorio. Puedes ilustrar con un ejemplo de coordenadas táctiles (x, y) y cómo viajan a través del sistema.

## Actividad 05

### Diseña una aplicación interactiva que use el touch del móvil para controlar una visuales de tema musical de tu elección. Las visuales correrán en una aplicación de escritorio (desktop). Recuerda que ambas aplicaciones las construirás usando p5.js y utilizando el servidor Node.js como puente.

### Implementa tu diseño. Puedes usar IA generativa para ayudarte a escribir el código, pero primero debes hacer el diseño de lo que quieres.

### Incluye todos los códigos (servidor y clientes) en tu bitácora.



