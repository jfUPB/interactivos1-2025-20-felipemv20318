# Unidad 1

## 🔎 Fase: Set + Seek

### Actividad 01

¿Qué es un sistema físico interactivo?  
un sistema fisico interactivo es la interaccion de dispositivos como computadora, consola o celular con con suceso del habiente ya sea que el dispositivo reciba algo que se manifiste en ambiente o se reciba algo del ambiente y se manifieste en el dispositivo

¿Cómo podrías aplicar lo que has visto en tu perfil profesional?  
se podria aplicar en la creacion de diversos metodos de interacion y personalizacion ya se en experiencias, juegos o diseños como interacciones en juegos con tus latidos  o que funcionen con tu vos o cosas parecidas.

### Actividad 02

¿Qué es el diseño/arte generativo?
el arte/diseño generativo es una forma de crear o diseñar con el uso de sistemas autonmos como programas, maquinas o hasta oersonas en base a unas reglas dadas por el autor las cuales pese a ser la misma se caracterriza dar un rsultado de menor a mayor medida un grado de aletoriedad para generar resultados diferentes.

¿Cómo podrías aplicar lo que has visto en tu perfil profesional?
podria aplicarlo en sistema de personalizacion interactiva poniedo reglas generales que permitan que las variaciones agragar o altera los diseños de coasa en mi juego para darle un toque unico y experiencia personal para cada usuario.

### Actividad 03

En este sistemas físico interactivo identifica los inputs, outputs y el proceso.
en este sistema el micro:bit es tanto el input como el output al igual que el computador ya que con ellos puede interactuar y recibir el resultado de la interacion del otro lado como la figuras de los leds o el cambio de letra y color del circulo.

### Actividad 04

Crea tu propio programa en p5.js. En ti bitácora:

Escribe el enlace a tu programa en el editor de p5.js.
https://editor.p5js.org/felipemv20318/sketches/324PswCKd

Copia el código de tu programa en la bitácora (recuerda insertarlo usando markdown y el lenguaje javascript).
function setup() {
  createCanvas(600, 600);
  noLoop(); 
  background(10);
  drawPattern();
}

function drawPattern() {
  translate(width / 2, height / 2);
  let shapes = int(random(5, 20)); 
  let radius = random(100, 250); 
  
  for (let i = 0; i < shapes; i++) {
    let angle = TWO_PI / shapes * i;
    let x = cos(angle) * radius + random(-20, 20);
    let y = sin(angle) * radius + random(-20, 20);
    
    let size = random(10, 50);
    let r = random(100, 255);
    let g = random(100, 255);
    let b = random(100, 255);
    
    fill(r, g, b, 150);
    noStroke();
    
    push();
    translate(x, y);
    rotate(angle + random(-0.5, 0.5));
    ellipse(0, 0, size, size * sin(frameCount * 0.01 + i)); // Uso de sin()
    pop();
  }
}

function mousePressed() {
  background(10);
  drawPattern(); 
}

Muestra una captura de pantalla del resultado de tu programa.
<img width="595" height="597" alt="image" src="https://github.com/user-attachments/assets/14581b17-a64f-4446-a303-e3e2c97d4db8" />

