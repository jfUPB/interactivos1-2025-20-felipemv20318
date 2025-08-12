# Unidad 2


## 🤔 Fase: Reflect

### Actividad 06

En tu bitácora, sin consultar tu código, diagramas o notas, responde a las siguientes preguntas con tus propias palabras. Concéntrate en el esfuerzo de recordar, no en la perfección de la respuesta.

Parte 1: recuperación de conocimiento (Retrieval Practice)

Describe con tus palabras qué es una máquina de estados. ¿Cuáles son sus cuatro componentes fundamentales que has utilizado en esta unidad?

una maquina de estados es un programa que funciona estando en diferentes estados los cuales pueden seguir una o varias rutas para llegar a varios caminos o uno establecido si es lo rrequerido y sus cuatro componentes fundamentales que he utilizado son los estados, eventos, transiciones y acciones

Explica por qué la técnica de C es tan útil para gestionar la “concurrencia” (atender un temporizador y botones “al mismo tiempo”) en un dispositivo con un solo hilo de ejecución como el micro:bit. ¿Qué problema soluciona en comparación con usar funciones como sleep()?

que en una maquina de estados puede haver un evento como dejar pasar el tiempo e interrumpirlo si se cumple otro evento primero como presionar el boton A

Imagina que tienes que añadir una nueva funcionalidad a la bomba temporizada: si se agita (shake) el micro:bit mientras la cuenta regresiva está activa, el tiempo se reduce a la mitad. ¿Cómo modificarías tu diagrama de máquina de estados para incluir este nuevo evento y acción?

en el estado de Armada yo haria un evento de shake que haria una transicion al mismo estado de armado con la acion de dividir el tiempo actual del conteo por 2.

Explica qué es un “vector de prueba” y por qué es una herramienta crucial para verificar que una máquina de estados funciona como se espera.

un vector de prueba es una forma de revisar si una maquina de estado funciona ya que esta consta de vraias rutas de estados con diferentes eventos desencadenantes, la prueba de estado pone en teoria lo que deberia pasar si se hace una combinacion exacta de aciones y comprueba de que pase lo esperado o que pase algo que no deberia para saber si esta bien el programa o requiere arreglo como por ejemplo boton A 2 veces y luego esperary comprobar si salio lo que debia al final.

Parte 2: reflexión sobre tu proceso (Metacognición)

¿Qué parte del diseño de la bomba temporizada te resultó más desafiante: crear el diagrama de estados (Actividad 04) o traducir ese diagrama a código MicroPython (Actividad 05)? ¿Por qué?

batalle mucho con la teoria para hacer el diagrama ya que me cuesta tener que dejar k¿las cosas tan especificas y calras como se debe en esos diagramas pero despues de concejos de profe y mucho prueba y eroor me quedo muy claro y me quedo bien y por otro lado traducir ese diagrama a código MicroPython fue mas dificil por lo de siempre que aun estoy recordando como programar otravez pero con las ayudad del propio MicroPython como con el altavoz estubo bien y tambien al usar programas antiguos mios de base aunque eso me llevo a replicar un error de ese programa anterior en la bomba que no evito que funcionara pero lo debo mejorar en conclusion estuvo mas difil programar por mi lento reaprendizaje y mi incapacidad de usar material de apoyo aunque tenga errores.

Describe un error o “bug” que encontraste al implementar tu programa. ¿Cómo te ayudó pensar en términos de estados, eventos y transiciones a identificar y solucionar el problema?

como lo hice muy en base a ejercicios pasados con las guias MicroPython y con mi diagrama no encontre un bug y  pensar en términos de estados, eventos y transiciones me ayudo a hacerlo paso a paso lento para evitar errores exepto los que no vi como errores en ese moneto y no arregle como evitar que mis numeros se muestren en cada momento.

El problema de la bomba era complejo. ¿Qué estrategia usaste para abordarlo? ¿Comenzaste con una versión simple y añadiste funcionalidades poco a poco?

si era complejo pero nada que se aleje mucho de lo visto y explicado en clase y la estrategia use para abordarlo fue tener material de apoyo para luego comenzar hacer la version final desde el inicio gracias al diagrama que ya me decia que tenia que tener.

Ahora que entiendes el patrón de máquina de estados, ¿En qué otro tipo de proyecto o sistema de entretenimiento digital crees que podrías aplicarlo?

se me ocurre en muchos tipos de proyectos pero principalmente en juegos o interfaces que interactuen y se guien con diferentes eventos invluido el tiempo para ser mas proacctiva y para realizar experiencias interacitivoas como la boba del scaperoom 

### Actividad 07

Encuentra a un compañero de trabajo.
Intercambien las URLs de sus bitácoras de aprendizaje.
Revisa con atención las entradas de tu compañero para las Actividades 04 (diagrama de la bomba) y 05 (código y pruebas).
Analiza de manera crítica el diseño y la implementación de tu compañero y deja un comentario de retroalimentación específico y constructivo.
Conversa con tu compañero sobre su diseño y código, y discutan sus comentarios.

(No encontre compañero)

### Actividad 08

Continuar: ¿Qué actividad, explicación o ejemplo de esta unidad te ayudó más a entender el poder de las máquinas de estados? ¿Qué elemento consideras que es indispensable y debería mantener?

fue el diseño del diagrama como actividad y explicacion por aparte cada una ya que al verlo teni cosas en mente pero al intentar sin ayudo aplicarlas me hizo usar esas ideas profundizarlas y buscar mas para hacerlo bien y es el que veo mas indispensble porque para lo complejo que puede ser programar al hacerlo mas simple y en papel te deja mas claro su uso y diferencia on otras formas e programar.

Dejar de hacer: ¿Hubo algún paso o actividad que te pareció confuso, innecesariamente complicado o que aportó poco a tu aprendizaje? ¿Qué cambiarías o eliminarías?

Nada en particular

Empezar a hacer: ¿Qué te habría ayudado a entender mejor?

no se me ocurre nada

Ritmo y dificultad: En una escala del 1 (muy fácil) al 5 (muy difícil), ¿Cómo calificarías la dificultad de pasar del análisis de un programa (Actividad 03) al diseño desde cero de uno complejo (Actividad 04 y 05)? ¿Por qué?
Comentario adicional: ¿Hay algo más que te gustaría compartir sobre tu proceso de aprendizaje en esta unidad? ¿Algún momento de frustración o de “¡Aha!” que quieras destacar?

el ritmo y dificultad lo pondria en un 3 (normal) porque era desafiente ya que pasar de ver a hacer es mucho pero no fue imposible y lo considero adecuado y me gustaria aclarar que me parecio mejor al tener menos actividades que en el modulo anterior ya que asi me podia concentrar mas en los otros aumentando mi comprencion en ellos.
