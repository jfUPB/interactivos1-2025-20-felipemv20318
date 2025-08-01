# Unidad 2

## 🔎 Fase: Set + Seek

### Actividad 01

Escribe en tu bitácora lo siguiente:

Describe detalladamente cómo funciona este ejemplo.

Este programa hace que dos puntos o píxeles de la pantalla del micro:bit se enciendan y apaguen cada cierto tiempo:

Uno cambia cada 1 segundo 1000 milisegundos.
El otro cambia cada medio segundo 500 milisegundos.

El programa usa una clase llamada Pixel que maneja el comportamiento de cada punto con unas máquina de estados que es como una forma organizada de hacer que las cosas cambien dependiendo de lo que pase.

¿Cuáles son los estados en el programa?

serian 2, cuando el pixel se prende por primera vez y cuando el segundo cuando cambia

¿Cuáles son los eventos/inputs en el programa?

el input seria cuando hacemos que el programa inicie y se enciende el primer pixel y el output seria el tiempo que hace que el pixel cambie su tiempo de brillo o que salga otro

¿Cuáles son las acciones en el programa?

las acciones serian cuando el programa inicia y los pixeles brillan y luego de pasar el tiempo establezido el pixel cambia de alguna manera.


### Actividad 02

Escribe el código que soluciona este problema en tu bitácora.

``` js

from microbit import *
import utime

class Semaforo:
    def __init__(self):
        self.state = "Rojo"
        self.startTime = utime.ticks_ms()

    def update(self):
        if self.state == "Rojo":
            display.clear()
            display.set_pixel(2, 0, 9)
            if utime.ticks_diff(utime.ticks_ms(), self.startTime) > 3000:
                self.state = "Amarillo"
                self.startTime = utime.ticks_ms()

        elif self.state == "Amarillo":
            display.clear()
            display.set_pixel(2, 1, 9)
            if utime.ticks_diff(utime.ticks_ms(), self.startTime) > 1000:
                self.state = "Verde"
                self.startTime = utime.ticks_ms()

        elif self.state == "Verde":
            display.clear()
            display.set_pixel(2, 2, 9)
            if utime.ticks_diff(utime.ticks_ms(), self.startTime) > 3000:
                self.state = "Rojo"
                self.startTime = utime.ticks_ms()

semaforo = Semaforo()

while True:
    semaforo.update()


```

Identifica los estados, eventos y acciones en tu código.

los estados serian 3 uno por cada luz primero el de arriba como rojo, luego el medio como amarillo y por ultimo el de abajo como verde  
los eventos o outputs sserian el tiempo y el resultado seria el cambio en la posicion del pixel que brilla  
las acciones serian cuando se prende un led y tras un tiempo se apaga y prende otro

