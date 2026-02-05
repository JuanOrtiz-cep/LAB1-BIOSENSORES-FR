# LAB1-BIOSENSORES-FR

Se realizó una revisión literaria sobre el proceso respiratorio, enfocado en el conocimiento de las variables físicas. 
La respiración es el proceso fisiológico mediante el cual los organismos intercambian gases con el ambiente. En los humanos, está compuesta por dos grandes procesos: la ventilación pulmonar que es el movimiento de aire hacia adentro y afuera de los pulmones y el intercambio gaseoso que es la difusión de oxígeno hacia la sangre y dióxido de carbono hacia el exterior. Este proceso depende de la distensibilidad del sistema respiratorio y la resistencia de las vías aéreas. 
A su vez hay diferentes variables físicas medibles como el volumen pulmonar, flujo de aire, presión y concentración de gases que permiten hacer análiss sobre la salud de una persona. 
Para captar la señal respiratoria, la cual es una señal física, se puede utilizar un sensor respiratorio como será el caso, puede ser de flujo, presión o CO₂. Utilizando la magnitud física asociada, se requiere un transductor que convierta la magnitud en señal eléctrica y por medio de un sistema de adquisición se digitalizará la señal para poder ser visualizada y poder tomar la frecuencia respiratoria.
La frecuencia respiratoria (FR) es el número de ciclos respiratorios completos por minuto y está podrá ser calculada según los picos de la señal respiratoria.

Se desarrollo un sistema capaz de adquirir la señal respiratoria para calcular la frecuencia respiratoria de un sujeto sano.

#  Monitoreo de la Frecuencia Respiratoria y Análisis del Habla

##  Descripción del proyecto
Este repositorio contiene el desarrollo de una práctica de laboratorio enfocada en el monitoreo del proceso respiratorio mediante la adquisición y el análisis de una señal biológica. El objetivo principal es evaluar cómo la verbalización modifica el patrón y la frecuencia respiratoria en comparación con un estado de reposo.

La practica integra hardware de adquisición, sensores fisiológicos y herramientas de procesamiento digital de señales en MATLAB.

##  Objetivos

### Objetivo general
Evaluar  el patrón respiratorio.

### Objetivos específicos
- Identificar las principales variables físicas involucradas en el proceso respiratorio.
- Diseñar un sistema capaz de adquirir la señal respiratoria y calcular la frecuencia respiratoria.
- Analizar cambios en el patrón respiratorio asociados a tareas de verbalización.





PARTE A.
1. Llevar a cabo una revisión de la literatura sobre el proceso respiratorio, con
énfasis en el reconocimiento de las variables físicas principalmente
involucradas. En caso de utilizar modelos de IA generativa (e.g., ChatGPT)
debe verificar la información contra una fuente confiable (e.g., libros, manuales,
informes técnicos).
2. Seleccionar el sensor que considere más adecuado para medir la variable de
interés y, de esa forma, capturar las variaciones producidas por el proceso
respiratorio. Considere un voltaje de alimentación de +3.3 a +5 VDC, en el
caso de tratarse de un sensor pasivo. Medite sobre cómo adaptar el sensor al

UNIVERSIDAD MILITAR NUEVA GRANADA

El uso no autorizado de su contenido así como reproducción total o parcial por cualquier persona o entidad, estará en
contra de los derechos de autor Pagina 8 de 11
cuerpo del sujeto de prueba para capturar la señal con un mínimo de
interferencia.
3. Diseñe y elabore un sistema que acondicione y digitalice la señal respiratoria
utilizando para ello el sensor previamente elegido. Puede utilizar el conversor
análogo-digital integrado en la placa Arduino.
4. Coloque el sensor sobre alguno de los miembros del equipo para verificar la
operatividad del sistema.
5. Empleando la función “Serial Plotter” del menú “Herramientas” del entorno de
programación, tome capturas de pantalla que muestren la señal:
a. En reposo (cuente manualmente el número de veces que el sujeto inhala o
exhala).
b. Mientras el sujeto de prueba habla o lee.
PARTE B
1. Diseñe y elabore un breve código en MATLAB que permita la captura
temporizada de la señal respiratoria adquirida por el sistema que Ud. ha
construido y probado.
2. Capturar 30 segundos de señal respiratoria bajo las condiciones establecidas
en el paso 5 de la parte A (incisos “a” y “b”). Recuerde guardar en cada caso el
correspondiente archivo .MAT.
3. De ser necesario, aplique los filtros correspondientes para mejorar la calidad
de ambas señales. Especifique el tipo de filtro (pasa-bajas, pasa banda) y la(s)
frecuencia(s) de corte.
4. Obtenga la representación en frecuencia de ambas señales e identifique la
frecuencia dominante en cada caso.
PARTE C
Documente la práctica explicando paso a paso cuál fue el procedimiento que se
siguió y dando respuesta a las preguntas que se formulan en la guía (ver Parte
15). Suministre una breve conclusión y elabore un repositorio en la plataforma
GitHub que contenga toda la información recopilada en las partes A y B.
Asegúrese de incluir gráficas con buena resolución. Cada estudiante debe
tener su propia cuenta y deben aparecer como colaboradores en el repositorio.
En caso contrario, solo se calificará al estudiante que aparece como editor.

12.RESULTADOS DE LA PRÁCTICA:
Al finalizar esta práctica, el estudiante será capaz de:
1. Identificar las variables físicas más involucradas en el proceso respiratorio.

UNIVERSIDAD MILITAR NUEVA GRANADA

El uso no autorizado de su contenido así como reproducción total o parcial por cualquier persona o entidad, estará en
contra de los derechos de autor Pagina 9 de 11
2. Desarrollar un sistema capaz de monitorear el proceso respiratorio y obtener la
frecuencia respiratoria de un individuo sano.
3. Capturar, graficar y manipular vectores en MATLAB.
4. Evaluar la influencia del habla en el patrón respiratorio y en la frecuencia
respiratoria de un individuo sano.
5. Comparar la eficacia de distintos métodos matemáticos para representar una
serie temporal en el dominio de la frecuencia.
6. Plantear hipótesis o explicaciones posibles de los resultados obtenidos desde
la fisiología.
7. Utilizar GitHub como herramienta de documentación y colaboración,
asegurando la visibilidad del trabajo individual y en grupo.
