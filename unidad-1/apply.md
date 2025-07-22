# Unidad 1

## 🛠 Fase: Apply

### Actividad 05

En tu bitácora: explica cómo funciona el sistema físico interactivo que acabamos de crear.  
(d)

### Actividad 06

En tu bitácora:

Escribe el enlace a tu programa en el editor de p5.js.
https://editor.p5js.org/felipemv20318/sketches/V0uAnF84h

Copia el código de tu programa en la bitácora (recuerda insertarlo usando markdown y el lenguaje javascript).

let port;
let connectBtn;
let connectionInitialized = false;
let circleX = 200;
let circleSpeed = 5;

function setup() {
  createCanvas(400, 400);
  background(220);

  port = createSerial();
  connectBtn = createButton("Connect to micro:bit");
  connectBtn.position(80, 300);
  connectBtn.mousePressed(connectBtnClick);
}

function draw() {
  background(220);

  if (port.opened() && !connectionInitialized) {
    port.clear();
    connectionInitialized = true;
  }

  if (port.availableBytes() > 0) {
    let dataRx = port.read(1);
    if (dataRx === "A") {
      circleX -= circleSpeed;
    } else if (dataRx === "B") {
      circleX += circleSpeed;
    }
  }

  circleX = constrain(circleX, 0, width);

  fill("blue");
  noStroke();
  ellipse(circleX, height / 2, 50, 50);

  if (!port.opened()) {
    connectBtn.html("Connect to micro:bit");
  } else {
    connectBtn.html("Disconnect");
  }
}

function connectBtnClick() {
  if (!port.opened()) {
    port.open("MicroPython", 115200);
    connectionInitialized = false;
  } else {
    port.close();
  }
}


Copia el código del micro:bit en la bitácora (recuerda insertarlo usando markdown y el lenguaje python).

from microbit import *

uart.init(baudrate=115200)

while True:
    if button_a.is_pressed():
        uart.write('A')
    elif button_b.is_pressed():
        uart.write('B')
    else:
        uart.write('N')

    sleep(100)


