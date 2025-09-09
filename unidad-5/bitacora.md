
# Evidencias de la unidad 5

## Actividad 1

### Describe cómo se están comunicando el micro:bit y el sketch de p5.js. ¿Qué datos envía el micro:bit?

el micro:bit y el sketch de p5.js se comunican gracias a las cadenas de texto enviadas por el puerto serie UART que se crean a travez del codigo guardado en el microbite ue convierte la informacion que da el micro:bit a un string de texto separado por comas.

    data = "{},{},{},{}\n".format(xValue, yValue, aState,bState)
    
esa parte del codigo la lee esta informacion (xValue, yValue, aState, bState) y la deja parecida a esto (-345,278,1,0) y en el sketch de p5.js en la linea 77 a 108 se revisa continuamente por si llega esa informacion del micro:bit que es la usada para poder dibujar siendo xValue y yValue los valores X e Y del acelerómetro los cuales indican la inclinación del micro:bit y aState y bState son lo valores de boton A y B del micro:bit leyendolos como un 1 y 0 o como un true o false.

### ¿Cómo es la estructura del protocolo ASCII usado?

### Muestra y explica la parte del código de p5.js donde lee los datos del micro:bit y los transforma en coordenadas de la pantalla.

### ¿Cómo se generan los eventos A pressed y B released que se generan en p5.js a partir de los datos que envía el micro:bit?

### Capturas de pantalla de los algunos dibujos que hayas hecho con el sketch.
