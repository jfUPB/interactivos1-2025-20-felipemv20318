# Evidencias de la unidad 4

## Código

[https://editor.p5js.org/generative-design/sketches/M_6_1_02](URL)

Código a modificar:

``` js
// M_6_1_02
// Spring.js
//
// Generative Gestaltung – Creative Coding im Web
// ISBN: 978-3-87439-902-9, First Edition, Hermann Schmidt, Mainz, 2018
// Benedikt Groß, Hartmut Bohnacker, Julia Laub, Claudius Lazzeroni
// with contributions by Joey Lee and Niels Poldervaart
// Copyright 2018
//
// http://www.generative-gestaltung.de
//
// Licensed under the Apache License, Version 2.0 (the "License");
// you may not use this file except in compliance with the License.
// You may obtain a copy of the License at http://www.apache.org/licenses/LICENSE-2.0
// Unless required by applicable law or agreed to in writing, software
// distributed under the License is distributed on an "AS IS" BASIS,
// WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
// See the License for the specific language governing permissions and
// limitations under the License.

/**
 * two nodes and a spring
 *
 * MOUSE
 * click, drag   : postion of one of the nodes
 *
 * KEYS
 * s             : save png
 */

'use strict';

var sketch = function(p) {

  var nodeA, nodeB;
  var spring;

  p.setup = function() {
    p.createCanvas(p.windowWidth, p.windowHeight);
    p.noStroke();
    p.fill(0);

    nodeA = new Node(p.width / 2 + p.random(-50, 50), p.height / 2 + p.random(-50, 50));
    nodeB = new Node(p.width / 2 + p.random(-50, 50), p.height / 2 + p.random(-50, 50));

    nodeA.damping = 0.1;
    nodeB.damping = 0.1;

    spring = new Spring(nodeA, nodeB);
    spring.length = 100;
    spring.stiffness = 0.6;
    spring.damping = 0.3;
  };

  p.draw = function() {
    p.background(255);

    if (p.mouseIsPressed == true) {
      nodeA.x = p.mouseX;
      nodeA.y = p.mouseY;
    }

    // update spring
    spring.update();

    // update node positions
    nodeA.update();
    nodeB.update();

    // draw spring
    p.stroke(0, 130, 164);
    p.strokeWeight(4);
    p.line(nodeA.x, nodeA.y, nodeB.x, nodeB.y);

    // draw nodes
    p.noStroke();
    p.fill(0);
    p.ellipse(nodeA.x, nodeA.y, 20, 20);
    p.ellipse(nodeB.x, nodeB.y, 20, 20);
  };

  p.keyPressed = function() {
    if (p.key == 's' || p.key == 'S') p.saveCanvas(gd.timestamp(), 'png');
  };

};

var myp5 = new p5(sketch);

```

[https://editor.p5js.org/felipemv20318/sketches/P_AnJ30EQ](URL)

Código modificado:

``` js
// sketch.js - M_6_1_02 adaptado para micro:bit usando navigator.serial
var sketch = function(p) {

  var nodeA, nodeB;
  var spring;

  // --- variables para serial (Web Serial API) ---
  let port = null;
  let reader = null;
  let keepReading = false;
  let buffer = "";
  let connectBtn;
  let microBitConnected = false;

  let microBitX = 0;
  let microBitY = 0;
  let microBitAState = false;
  let microBitBState = false;
  let prevmicroBitAState = false;
  let prevmicroBitBState = false;

  let springColor = [0, 130, 164];

  p.setup = function() {
    p.createCanvas(p.windowWidth, p.windowHeight);
    p.noStroke();
    p.fill(0);

    nodeA = new Node(p.width / 2 + p.random(-50, 50), p.height / 2 + p.random(-50, 50));
    nodeB = new Node(p.width / 2 + p.random(-50, 50), p.height / 2 + p.random(-50, 50));

    nodeA.damping = 0.1;
    nodeB.damping = 0.1;

    spring = new Spring(nodeA, nodeB);
    spring.length = 100;
    spring.stiffness = 0.6;
    spring.damping = 0.3;

    // botón para conectar/desconectar (debe ser acción de usuario)
    connectBtn = p.createButton("Connect to micro:bit");
    connectBtn.position(8, 8);
    connectBtn.mousePressed(connectBtnClick);

    console.log("Sketch listo. Presiona Connect para abrir puerto serial.");
  };

  // --- botón: abrir / cerrar puerto (async) ---
  async function connectBtnClick() {
    try {
      if (!port) {
        if (!("serial" in navigator)) {
          console.log("Web Serial API no está disponible en este navegador.");
          alert("Web Serial no disponible. Usa Chrome/Edge en localhost o HTTPS.");
          return;
        }
        // pedir puerto al usuario
        port = await navigator.serial.requestPort(); // muestra el diálogo del navegador
        await port.open({ baudRate: 115200 });
        microBitConnected = true;
        connectBtn.html("Disconnect");
        console.log("Puerto abierto. Iniciando lector...");
        // preparar lector de texto (TextDecoderStream)
        const decoder = new TextDecoderStream();
        port.readable.pipeTo(decoder.writable);
        reader = decoder.readable.getReader();
        keepReading = true;
        readLoop(); // iniciar loop de lectura (no await to keep UI responsive)
      } else {
        // desconectar
        keepReading = false;
        if (reader) {
          try { await reader.cancel(); } catch (e) {}
          try { reader.releaseLock(); } catch (e) {}
          reader = null;
        }
        try { await port.close(); } catch (e) {}
        port = null;
        microBitConnected = false;
        connectBtn.html("Connect to micro:bit");
        console.log("Puerto cerrado por el usuario.");
      }
    } catch (err) {
      console.log("Error connectBtnClick:", err);
      // limpiar estado en caso de error
      try { if (reader) { await reader.cancel(); reader = null; } } catch(e){}
      try { if (port) { await port.close(); port = null; } } catch(e){}
      microBitConnected = false;
      connectBtn.html("Connect to micro:bit");
    }
  }

  // --- loop de lectura asíncrono ---
  async function readLoop() {
    buffer = "";
    try {
      while (keepReading && reader) {
        const { value, done } = await reader.read();
        if (done) break;
        if (value) {
          buffer += value;
          let idx;
          while ((idx = buffer.indexOf("\n")) !== -1) {
            let line = buffer.slice(0, idx);
            buffer = buffer.slice(idx + 1);
            processLine(line);
          }
        }
      }
    } catch (err) {
      console.log("Read loop error:", err);
    } finally {
      // cleanup
      try { if (reader) { await reader.cancel(); reader = null; } } catch(e){}
      keepReading = false;
    }
  }

  // --- procesar línea completa recibida ---
  function processLine(line) {
    if (!line) return;
    line = line.trim();
    console.log("REC RAW:", line);
    const values = line.split(",");
    if (values.length === 4) {
      microBitX = parseInt(values[0]);
      microBitY = parseInt(values[1]);
      microBitAState = values[2].trim().toLowerCase() === "true";
      microBitBState = values[3].trim().toLowerCase() === "true";
      updateButtonStates(microBitAState, microBitBState);
      applyAccelerometerToNodes(microBitX, microBitY);
    } else {
      console.log("ERROR: no se recibieron 4 campos. Raw:", line);
    }
  }

  // --- actualizar estados de botones (edge detection) ---
  function updateButtonStates(newAState, newBState) {
    // A pressed edge (false -> true) : mover nodeA inmediatamente
    if (newAState === true && prevmicroBitAState === false) {
      nodeA.x = p.width/2 + p.map(p.constrain(microBitX, -1024, 1024), -1024, 1024, -200, 200);
      nodeA.y = p.height/2 + p.map(p.constrain(microBitY, -1024, 1024), -1024, 1024, -200, 200);
      console.log("A pressed -> mover nodeA (evento)");
    }
    // B released edge (true -> false) : cambiar color del spring
    if (newBState === false && prevmicroBitBState === true) {
      springColor = [p.random(0,255), p.random(0,255), p.random(0,255)];
      console.log("B released -> color cambiado");
    }
    prevmicroBitAState = newAState;
    prevmicroBitBState = newBState;
  }

  // --- mapear acelerómetro a nodos / parámetros ---
  function applyAccelerometerToNodes(ax, ay) {
    var mappedX = p.width/2 + p.map(p.constrain(ax, -1024, 1024), -1024, 1024, -p.width/2, p.width/2);
    var mappedY = p.height/2 + p.map(p.constrain(ay, -1024, 1024), -1024, 1024, -p.height/2, p.height/2);
    nodeB.x += (mappedX - nodeB.x) * 0.05;
    nodeB.y += (mappedY - nodeB.y) * 0.05;
    spring.stiffness = p.map(p.constrain(ax, -1024, 1024), -1024, 1024, 0.1, 1.2);
    spring.damping = p.map(p.constrain(ay, -1024, 1024), -1024, 1024, 0.0, 0.7);
  }

  p.draw = function() {
    p.background(255);

    // Si no conectado, mostrar mensaje
    if (!microBitConnected) {
      p.noStroke();
      p.fill(0);
      p.textSize(16);
      p.text("Conecta el micro:bit y presiona Connect", 20, 70);
    }

    // actualizar física y dibujar (igual que original)
    spring.update();
    nodeA.update();
    nodeB.update();

    p.stroke(springColor[0], springColor[1], springColor[2]);
    p.strokeWeight(4);
    p.line(nodeA.x, nodeA.y, nodeB.x, nodeB.y);

    p.noStroke();
    p.fill(0);
    p.ellipse(nodeA.x, nodeA.y, 20, 20);
    p.ellipse(nodeB.x, nodeB.y, 20, 20);

    // overlay de datos cuando B está presionado
    if (microBitBState === true) {
      p.push();
      p.noStroke();
      p.fill(0, 120);
      p.rect(10, p.height - 60, 380, 50);
      p.fill(255);
      p.textSize(14);
      p.text(`x:${microBitX} y:${microBitY} A:${microBitAState} B:${microBitBState}`, 20, p.height - 35);
      p.pop();
    }
  };

  p.keyPressed = function() {
    if (p.key == 's' || p.key == 'S') p.saveCanvas(gd.timestamp(), 'png');
  };

}; // end sketch

var myp5 = new p5(sketch);


```

## Video

[https://youtu.be/8Dc0Oi2JqHE?si=VkT1XU_Jr8bWOeij](URL)



