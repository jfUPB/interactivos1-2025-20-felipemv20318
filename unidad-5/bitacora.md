
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

Sí, porque el formato hexadecimal muestra cada byte como un número en base 16, lo cual refleja con precisión la información transmitida, pero no es intuitivo para las personas. En ASCII, los datos se ven como palabras o símbolos reconocibles, mientras que en HEX sólo aparecen secuencias de números que necesitan ser interpretadas y decodificadas para entender su significado.

En otras palabras, el texto en ASCII resulta más fácil de leer para un humano porque se asocia con caracteres visibles, mientras que el formato hexadecimal es útil para el computador o para depuración técnica, pero no está pensado para ser interpretado directamente como mensaje legible.

### ¿Cuántos bytes se están enviando por mensaje? ¿Cómo se relaciona esto con el formato '>2h2B'? ¿Qué significa cada uno de los bytes que se envían?

En el experimento se envían 6 bytes por mensaje. Esto ocurre porque la instrucción

    data = struct.pack('>2h2B', xValue, yValue, int(aState), int(bState))

indica que cada paquete debe contener:

2 bytes para xValue (primer entero corto con signo).

2 bytes para yValue (segundo entero corto con signo).

1 byte para aState (estado del botón A).

1 byte para bState (estado del botón B).

El prefijo > significa que se envían en big-endian, es decir, primero el byte más significativo y luego el menos significativo.

Así, los primeros 4 bytes corresponden al valor del acelerómetro en x y y, y los últimos 2 bytes corresponden al estado de los botones.

### ¿Cómo se verían los números positivos y negativos en el formato '>2h2B'?

Los valores de xValue y yValue se representan como enteros de 16 bits con signo (tipo h).

Si el número es positivo, se guarda de forma directa en hexadecimal.
Ejemplo: 200 → 00 C8.

Si el número es negativo, se guarda usando complemento a dos en 16 bits.
Ejemplo: -200 → FF 38.

De esta manera, en el mensaje binario podemos ver valores positivos con bytes que comienzan en 00, mientras que los negativos suelen comenzar en FF u otro valor alto dependiendo de la magnitud.

### ¿Qué diferencias ves entre los datos en ASCII y en binario? ¿Qué ventajas y desventajas ves en usar un formato binario en lugar de texto en ASCII? ¿Qué ventajas y desventajas ves en usar un formato ASCII en lugar de binario?

En el experimento los datos enviados en ASCII aparecen como texto legible (por ejemplo: 123,-45,1,0), lo que permite que una persona los entienda fácilmente.
En cambio, en binario aparecen como bytes en hexadecimal (por ejemplo: 00 7B FF D3 01 00), que son más compactos pero difíciles de leer sin decodificación.

Binario:

Ventajas: ocupa menos espacio, la transmisión es más rápida y no necesita conversión adicional.
Desventajas: ilegible para una persona, depende de conocer el formato exacto para interpretarse.

ASCII:

Ventajas: legible y fácil de depurar, se pueden interpretar los valores sin herramientas extra.
Desventajas: ocupa más bytes, la transmisión es más lenta y necesita conversión de texto a número en el programa receptor.


## Actividad 3

### Explica por qué en la unidad anterior teníamos que enviar la información delimitada y además marcada con un salto de línea y ahora no es necesario.

En la unidad anterior los paquetes eran de longitud variable porque se enviaban como texto (ASCII) —por ejemplo "123,-45,1,0\n"— así que hacía falta un delimitador (el \n) para que el receptor supiera dónde termina cada paquete; sin ese delimitador el receptor no puede distinguir límites entre mensajes. En el formato binario que usamos después los paquetes tienen longitud fija (6 bytes para >2h2B), por eso el receptor puede leer siempre exactamente 6 bytes por paquete sin necesitar un carácter final que marque el cierre.

### Compara el código de la unidad anterior relacionado con la recepción de los datos seriales que ves ahora. ¿Qué cambios observas?

Antes se usaba readUntil("\n") y split(",") para procesar líneas de texto; ahora se usa readBytes() y DataView para leer bytes binarios, además se introdujo un serialBuffer para acumular bytes, se implementa búsqueda de header (0xAA) y comprobación de checksum, se reemplazó la conversión por int(values[0])/toLowerCase() por view.getInt16()/getUint8(), y se añadió port.clear() al conectar para evitar datos residuales.

### ¿Qué ves en la consola? ¿Por qué crees que se produce este error?

En la consola se ven lecturas correctas intercaladas con líneas con valores extraños (por ejemplo microBitY: 513 o microBitX: 3073) y números sueltos —esto ocurre porque el receptor a veces lee 6 bytes que no corresponden al mismo paquete (se desincroniza), ya sea porque la transmisión se fragmentó, porque había bytes residuales en el buffer o porque la lectura empezó a mitad de paquete; sin framing el receptor puede tomar bytes de dos paquetes distintos y entonces los getInt16/getUint8 devuelven valores incoherentes.

### ¿Por qué necesitamos framing?

Necesitamos framing (header + checksum) para sincronizar al receptor con el inicio del paquete y para verificar la integridad del paquete; el header permite descartar bytes hasta encontrar el comienzo real y el checksum detecta paquetes corruptos; juntos evitan desalineamientos y lecturas erráticas cuando la comunicación se fragmenta o hay ruido, haciendo la comunicación mucho más robusta.

### Analiza el código, observa los cambios. Ejecuta y luego observa la consola. ¿Qué ves?

Con framing implementado y el readSerialData() funcionando la consola muestra lecturas estables (microBitX: 500 microBitY: 524 microBitAState: true microBitBState: false), mensajes de estado (Connected to serial port, Microbit ready to draw, A pressed) y ocasionalmente Checksum error in packet si llega un paquete corrupto; ya no ves valores aleatorios como antes porque el receptor descarta bytes hasta encontrar 0xAA y sólo acepta paquetes cuyo checksum coincide.

