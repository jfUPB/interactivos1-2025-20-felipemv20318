
# Evidencias de la unidad 8

## Actividad 01

### 1) Documenta los referentes visuales que te inspiren.

Los referentes que inspiraron el proyecto son:
Juego “Light Show” de Friv
👉 https://www.friv.com/z/games/lightshow/game.html
Me gustó porque combina líneas de colores cambiando constantemente que responden al movimiento del usuario.

Ejemplo de “Generative Design” – Líneas interactivas
👉 https://editor.p5js.org/generative-design/sketches/P_2_2_6_03
me gusto porque me sive de base a mi idea de las linas ya hecho en p5js.

Estos referentes me ayudaron a definir una idea que combina lo visual con la interacción en tiempo real desde el celular y el micro:bit.

### 2) Define el concepto de las visuales que quieres crear.

La idea es crear una aplicación web interactiva donde el usuario pueda dibujar en un canvas del computador usando el celular como control remoto, y usar el micro:bit para cambiar el color o el tipo de trazo:
  
  -En la pantalla del computador aparece un canvas (hecho con p5.js) donde se van dibujando líneas o figuras.
 
  -El usuario controla el dibujo desde su celular, moviendo el dedo sobre la pantalla.

  -El micro:bit permite cambiar el color de las líneas con un botón (por ejemplo el botón A) y cambiar la forma (líneas → círculos) con el otro botón (B).

### 3) Explica cómo el móvil y el micro:bit controlarán las visuales.

Móvil:
Se conecta al servidor (por medio de Socket.IO) y envía la posición del toque del usuario (x, y) al computador. Cada movimiento del dedo genera una línea o figura en el canvas.

Micro bit:
Conecta al mismo servidor por puerto serial o Bluetooth.

  -Botón A: cambia el color del trazo (por ejemplo entre rojo, azul, verde, amarillo).

  -Botón B: cambia el modo de dibujo (líneas o círculos).

### 4) Haz un bocetos de todas las interfaces del sistema.

<img width="1105" height="628" alt="image" src="https://github.com/user-attachments/assets/717250c5-1f34-47b0-94a7-521682451658" />

### 5) Haz un diagrama que explique cómo se comunicarán los diferentes componentes del sistema.


