
# Evidencias de la unidad 5

## Actividad 1

### Describe cómo se están comunicando el micro:bit y el sketch de p5.js. ¿Qué datos envía el micro:bit?

El micro:bit y el sketch de p5.js se comunican a través del puerto serie (UART). El micro:bit toma la información de sus sensores (acelerómetro y botones) y la convierte en una cadena de texto en formato ASCII, separada por comas y terminada en un salto de línea \n.

El envío se hace con una línea de código como esta:

    data = "{},{},{},{}\n".format(xValue, yValue, aState,bState)

De esta manera, el micro:bit manda paquetes de datos con la estructura:

    xValue,yValue,aState,bState\n
    
De esta manera, el micro:bit manda paquetes de datos con la estructura de (-345,278,1,0) y en el sketch de p5.js en la linea 77 a 108 se revisa continuamente por si llega esa informacion del micro:bit la cual llega en paquetes de datos separos por Un salto de línea (\n) que marca el final del paquete el que es la usado para poder dibujar siendo (xValue y yValue) los valores X y Y del acelerómetro los cuales indican la inclinación del micro:bit y (aState y bState) son lo valores de boton A y B del micro:bit leyendolos como un 1 y 0 o como un true o false.

### ¿Cómo es la estructura del protocolo ASCII usado?

La estructura del protocolo ASCII usado es muy simple el cual esta hecho para que p5.js pueda leer y separar fácilmente los datos que envía el micro:bit los caules tienen Cada valor representado como texto (ASCII) a los valores están separados por comas y al final siempre hay un salto de línea (\n) que indica el final del paquete de datos:

        xValue,yValue,aState,bState\n
        
como ya mencione antes de los datos anteriores los valorees de xValue y yValue son los datos de X y Y del acelerómetro los cuales indican la inclinación del micro:bit y aState y bState son lo valores de boton A y B del micro:bit leyendolos como un 1 y 0 o como un true o false.

### Muestra y explica la parte del código de p5.js donde lee los datos del micro:bit y los transforma en coordenadas de la pantalla.

En el sketch de p5.js la lectura de datos del micro:bit se hace dentro de la función draw() en la linea 77 allí se usa port.readUntil("\n") para recibir cada paquete de datos el cual llega como una cadena de texto en formato ASCII terminada en un salto de línea y luego con data.split(",") se separa esa cadena en cuatro valores: xValue, yValue, aState y bState.

Los dos primeros valores (xValue y yValue) se convierten a números enteros y se transforman en coordenadas de pantalla sumándoles windowWidth/2 y windowHeight/2, de manera que el centro de la pantalla corresponda a la posición de referencia del micro:bit de esta forma la inclinación del micro:bit se refleja en la posición en la que se dibuja en el lienzo de p5.js, mientras que los otros dos valores (aState y bState) corresponden a los estados de los botones A y B que se interpretan como valores de (true o false).

### ¿Cómo se generan los eventos A pressed y B released que se generan en p5.js a partir de los datos que envía el micro:bit?

En el sketch de p5.js los eventos A pressed y B released se generan en la función updateButtonStates() donde se comparan los estados actuales de los botones que llegan desde el micro:bit con los estados anteriores guardados en las variables prevmicroBitAState y prevmicroBitBState.

Cuando el nuevo valor de aState pasa de false a true significa que el botón A fue presionado y en ese momento el código ejecuta las acciones correspondientes (cambiar tamaño de la línea, guardar la posición de clic y mostrar en consola “A pressed”) y cuando el nuevo valor de bState pasa de true a false significa que el botón B fue soltado y en ese momento se genera el evento B released que cambia el color de dibujo y muestra en consola “B released”.

Estos estados se actualizan en cada ciclo gracias a la línea:

    microBitAState = values[2].toLowerCase() === "true";
    microBitBState = values[3].toLowerCase() === "true";
    updateButtonStates(microBitAState, microBitBState);
donde los valores enviados por el micro:bit (true o false en formato de texto) se convierten en valores booleanos y luego se pasan a la función encargada de detectar los cambios de estado que producen los eventos.

### Capturas de pantalla de los algunos dibujos que hayas hecho con el sketch.

<img width="855" height="801" alt="image" src="https://github.com/user-attachments/assets/3390b684-877e-4b20-bd26-3a59b5525123" />


## Actividad 2

### Captura el resultado del experimento anterior. ¿Por qué se ve este resultado?

<img width="755" height="542" alt="image" src="https://github.com/user-attachments/assets/14740dd9-bd3b-4b1b-93db-72cc7170a1d2" />

En el experimento los datos ya no se envían en formato ASCII sino en formato binario mediante la instrucción:

    data = struct.pack('>2h2B', xValue, yValue, int(aState), int(bState))

Esto significa que cada paquete contiene 6 bytes: 2 bytes para xValue, 2 bytes para yValue y 1 byte para cada botón (aState y bState), todos enviados en big-endian.

Cuando en el SerialTerminal se selecciona la opción “Mostrar datos como: Texto”, la aplicación intenta interpretar esos bytes binarios como caracteres de texto ASCII o UTF-8. Como la mayoría de los valores binarios no corresponden a caracteres imprimibles, en pantalla aparecen símbolos extraños, cuadros negros o caracteres aleatorios que no tienen sentido legible.

Este resultado se ve así porque los datos son binarios y no están pensados para ser entendidos directamente como texto, sino para ser decodificados en el programa receptor (p5.js u otro).

### Captura el resultado del experimento anterior. Lo que ves ¿Cómo está relacionado con esta línea de código?

<img width="984" height="708" alt="image" src="https://github.com/user-attachments/assets/da594dee-a46e-406a-993c-14b8a050c949" />

En el experimento los datos ya no se muestran como texto ASCII sino en su representación hexadecimal o byte por byte gracias a la instrucción:

    data = struct.pack('>2h2B', xValue, yValue, int(aState), int(bState))

Esto significa que cada paquete contiene 6 bytes: 2 bytes para xValue, 2 bytes para yValue y 1 byte para cada botón (aState y bState) todos enviados en big-endian.

Cuando en el SerialTerminal se selecciona la opción “Mostrar datos como: Todo en HEX”, la aplicación ya no intenta interpretar los bytes como texto, sino que muestra directamente el valor numérico hexadecimal de cada byte transmitido.

Este resultado se ve así porque el formato hexadecimal refleja exactamente la estructura binaria definida por struct.pack, pero es más difícil de leer para una persona que el texto en ASCII ya que requiere decodificar los bytes para obtener nuevamente los valores originales de xValue, yValue, aState y bState.

### ¿Qué ventajas y desventajas ves en usar un formato binario en lugar de texto en ASCII?


