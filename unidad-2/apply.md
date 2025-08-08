# Unidad 2


## 🛠 Fase: Apply

### Actividad 04

Construye un diagrama detallado de la máquina de estados, incluyendo estados, eventos, transiciones y acciones.

<img width="659" height="765" alt="image" src="https://github.com/user-attachments/assets/0291dacb-bc54-411a-afcf-b482a49e7820" />


### Actividad 05

Reporta en un tu bitácora lo siguiente:

``` js
from microbit import *
import utime
import music

STATE_CONFIG = 0
STATE_COUNTDOWN = 1
STATE_EXPLODED = 2

state = STATE_CONFIG
time_left = 20
start_time = utime.ticks_ms()

MIN_TIME = 10
MAX_TIME = 60

def show_number(n):
    if n < 10:
        display.show(str(n))
    else:
        display.show(str(n // 10))
        utime.sleep_ms(300)
        display.show(str(n % 10))
        utime.sleep_ms(300)

while True:
    if state == STATE_CONFIG:
        show_number(time_left)

        if button_a.was_pressed() and time_left < MAX_TIME:
            time_left += 1

        if button_b.was_pressed() and time_left > MIN_TIME:
            time_left -= 1

        if accelerometer.was_gesture("shake"):
            state = STATE_COUNTDOWN
            start_time = utime.ticks_ms()

    elif state == STATE_COUNTDOWN:
        show_number(time_left)

        if utime.ticks_diff(utime.ticks_ms(), start_time) >= 1000:
            time_left -= 1
            start_time = utime.ticks_ms()

        if time_left <= 0:
            state = STATE_EXPLODED

    elif state == STATE_EXPLODED:
        display.show(Image.SKULL)
        music.play(["C4:4", "E4:4", "G4:4", "C5:2"])

        if button_a.was_pressed():
            time_left = 20
            state = STATE_CONFIG

```
La definición de los vectores de prueba básicos que permiten verificar el correcto funcionamiento del programa.

1) El sistema inicia en estado de configuración mostrando el valor inicial de 20 segundos en el display. No se presiona ningún botón y no se realiza el gesto de shake. El sistema permanece en estado de configuración sin cambios.
Paso lo esperado, por lo tanto el sistema pasó esta prueba.

2) El sistema inicia en estado de configuración con un valor de 20 segundos. Se presiona el botón A tres veces de forma consecutiva, aumentando el tiempo a 23 segundos y manteniendo el valor mostrado en pantalla.
Paso lo esperado, por lo tanto el sistema pasó esta prueba.

3) El sistema inicia en estado de configuración con un valor de 20 segundos. Se presiona el botón B cinco veces de forma consecutiva, disminuyendo el tiempo a 15 segundos y manteniendo el valor mostrado en pantalla.
Paso lo esperado, por lo tanto el sistema pasó esta prueba.

4) El sistema inicia en estado de configuración con un valor de 60 segundos. Se presiona el botón A, pero el valor no aumenta y se mantiene en 60 segundos en pantalla.
Paso lo esperado, por lo tanto el sistema pasó esta prueba.

5) El sistema inicia en estado de configuración con un valor de 10 segundos. Se presiona el botón B, pero el valor no disminuye y se mantiene en 10 segundos en pantalla.
Paso lo esperado, por lo tanto el sistema pasó esta prueba.

6) El sistema inicia en estado de configuración con un valor de 20 segundos. Se realiza el gesto de shake y el sistema pasa al estado de cuenta regresiva, iniciando el conteo de 20 hacia 0 segundos.
Paso lo esperado, por lo tanto el sistema pasó esta prueba.

7) El sistema se encuentra en estado de cuenta regresiva y el valor mostrado es 1 segundo. Pasa un segundo adicional y el sistema llega a 0 segundos, cambiando automáticamente al estado de explosión, mostrando una calavera y reproduciendo un sonido.
Paso lo esperado, por lo tanto el sistema pasó esta prueba.

8) El sistema se encuentra en estado de explosión mostrando la calavera. Se presiona el botón A, lo que provoca que el sistema regrese al estado de configuración con un valor de 20 segundos en pantalla.
Paso lo esperado, por lo tanto el sistema pasó esta prueba.

