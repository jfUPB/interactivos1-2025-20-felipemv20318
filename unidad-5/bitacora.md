
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

### Capturas de pantalla de los algunos dibujos que hayas hecho con el sketch.

<img width="855" height="801" alt="image" src="https://github.com/user-attachments/assets/3390b684-877e-4b20-bd26-3a59b5525123" />


