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


### Actividad 03

Explica por qué decimos que este programa permite realizar de manera concurrente varias tareas.

este progrma permite realizar varias tareeas de manera concurrente ya que las tareas de este programa que son la muestra de imagenes de expresiones funcionan de manera constante y autonma con el tiempo y tambien funciona de inmediato a la pulsación del botón A, sin esperar a que el tiempo del estado actual termine.

Identifica los estados, eventos y acciones en el programa.

los estados son el estado de incio y las expresiones mientras que los eventos son el paso del tiempo o la pulsacion del boton A y la accion final es el cambio de la la expresion o del evento.

Describe y aplica al menos 3 vectores de prueba para el programa. Para definir un vector de prueba debes llevar al sistema a un estado, generar los eventos y observar el estado siguiente y las acciones que ocurrirán. Por tanto, un vector de prueba tiene unas condiciones iniciales del sistema, unos resultados esperados y los resultados realmente obtenidos. Si el resultado obtenido es igual al esperado entonces el sistema pasó el vector de prueba, de lo contrario el sistema puede tener un error.

1) El sistema inicia desde el estado inicial, donde inmediatamente se muestra la cara feliz durante un segundo y medio, no se presiona el botón A en ningun momento y al pasar ese tiempo el sistema cambia automáticamente al estado siguiente mostrando una cara sonriente durante un segundo.  
Paso lo esperado, por lo tanto el sistema pasó esta prueba.

2) El sistema se encuentra en el estado de cara feliz y antes de que se complete el tiempo asignado de un segundo y medio se presiona el botón A y como resultado el sistema interrumpe inmediatamente la secuencia normal y cambia al estado de cara triste, mostrando la imagen correspondiente y actualizando el temporizador para una duración de dos segundos.  
Paso lo esperado, por lo tanto el sistema pasó esta prueba.

3) El sistema se encuentra en el estado de cara triste y en ese momento se presiona el botón A y el sistema responde al instante dejando el estado actual y mostrando la cara sonriente y esta imagen permanece durante un segundo como está establecido y luego el sistema regresa al estado de cara triste reiniciando su ciclo.  
Paso lo esperado, por lo tanto el sistema pasó esta prueba.

