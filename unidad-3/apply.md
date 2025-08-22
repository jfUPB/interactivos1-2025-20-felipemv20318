# Unidad 3


## 🛠 Fase: Apply


### Actividad 06

El código fuente de la bomba en p5.js. No olvides el propósito de esta evaluación: utilizar la técnica de máquina de estados que estamos trabajando en el curso.

``` js
let estado = "CONFIGURACION";
let cuenta = 20;
let secuencia = [];
let intervalo;

function setup() {
  createCanvas(400, 200);
  textAlign(CENTER, CENTER);
  textSize(20);
}

function draw() {
  background(220);

  if (estado === "CONFIGURACION") {
    text("CONFIGURACION", width/2, 40);
    text("Tiempo: " + cuenta + " s", width/2, 100);
    text("Presiona ENTER para armar", width/2, 160);
  } 
  
  else if (estado === "ARMADO") {
    text("ARMADO", width/2, 40);
    text("Cuenta: " + cuenta + " s", width/2, 100);
    text("Ingresa A, B, A para desactivar", width/2, 160);
  } 
  
  else if (estado === "EXPLOCION") {
    text("EXPLOSION", width/2, height/2);
    text("Presiona ENTER para reiniciar", width/2, height - 40);
  }
}

function keyPressed() {
  if (estado === "CONFIGURACION") {
    if (key === "A" && cuenta < 60) {
      cuenta++;
    } 
    else if (key === "B" && cuenta > 10) {
      cuenta--;
    } 
    else if (keyCode === ENTER) {
      estado = "ARMADO";
      iniciarCuenta();
    }
  }
  
  else if (estado === "ARMADO") {
    if (key === "A" || key === "B") {
      secuencia.push(key);
      if (secuencia.length > 3) secuencia.shift();
      if (secuencia.join("") === "ABA") {
        estado = "CONFIGURACION";
        clearInterval(intervalo);
        secuencia = [];
        cuenta = 20; 
      }
    }
  }

  else if (estado === "EXPLOCION") {
    if (keyCode === ENTER) {
      estado = "CONFIGURACION";
      clearInterval(intervalo);
      cuenta = 20;
      secuencia = [];
    }
  }
}

function iniciarCuenta() {
  intervalo = setInterval(() => {
    if (estado === "ARMADO") {
      cuenta--;
      if (cuenta <= 0) {
        clearInterval(intervalo);
        estado = "EXPLOCION";
      }
    }
  }, 1000);
}

```


### Actividad 07

Código p5.js

``` js
let estado = "configuracion";
let cuenta = 20;
let secuencia = [];
let serial;
let botonA = false;
let botonB = false;

function setup() {
  createCanvas(400, 400);
  textAlign(CENTER, CENTER);
  textSize(32);

  // Inicializar puerto serial
  serial = new p5.WebSerial();
  serial.getPorts();
  serial.on("data", recibirSerial);
}

function draw() {
  background(0);

  if (estado === "configuracion") {
    fill(0, 255, 0);
    text("Config: " + cuenta, width / 2, height / 2);
  } else if (estado === "armada") {
    fill(255, 255, 0);
    text("Cuenta: " + cuenta, width / 2, height / 2);

    if (frameCount % 60 === 0 && cuenta > 0) {
      cuenta--;
    }
    if (cuenta <= 0) {
      estado = "explosion";
    }
  } else if (estado === "explosion") {
    fill(255, 0, 0);
    text(" EXPLOSION ", width / 2, height / 2);
  }
}

function keyPressed() {
  if (estado === "configuracion") {
    if (key === "a" || key === "A") {
      if (cuenta < 60) cuenta++;
    } else if (key === "b" || key === "B") {
      if (cuenta > 10) cuenta--;
    } else if (key === " ") {
      estado = "armada";
      secuencia = [];
    }
  } else if (estado === "armada") {
    if (key === "a" || key === "A") {
      secuencia.push("A");
    } else if (key === "b" || key === "B") {
      secuencia.push("B");
    }
    if (secuencia.length === 3) {
      if (secuencia[0] === "A" && secuencia[1] === "B" && secuencia[2] === "A") {
        estado = "configuracion";
        cuenta = 20;
      } else {
        secuencia = [];
      }
    }
  } else if (estado === "explosion") {
    if (key === "r" || key === "R") {
      estado = "configuracion";
      cuenta = 20;
    }
  }
}

function recibirSerial() {
  let data = serial.readLine().trim();
  if (data === "A") {
    if (estado === "configuracion" && cuenta < 60) cuenta++;
    else if (estado === "armada") secuencia.push("A");
  } else if (data === "B") {
    if (estado === "configuracion" && cuenta > 10) cuenta--;
    else if (estado === "armada") secuencia.push("B");
  } else if (data === "START") {
    if (estado === "configuracion") {
      estado = "armada";
      secuencia = [];
    }
  } else if (data === "RESET") {
    if (estado === "explosion") {
      estado = "configuracion";
      cuenta = 20;
    }
  }

  if (secuencia.length === 3) {
    if (secuencia[0] === "A" && secuencia[1] === "B" && secuencia[2] === "A") {
      estado = "configuracion";
      cuenta = 20;
    } else {
      secuencia = [];
    }
  }
}
```

Enlace al editor de p5.js con tu código.


Código del micro:bit.

``` js
from microbit import *

while True:
    if button_a.was_pressed():
        uart.write("A\n")
    if button_b.was_pressed():
        uart.write("B\n")
    if pin0.is_touched():  
        uart.write("START\n")
    if pin1.is_touched(): 
        uart.write("RESET\n")
```
