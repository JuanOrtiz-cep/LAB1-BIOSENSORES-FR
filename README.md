# LAB1-BIOSENSORES-FR

La respiración es el proceso fisiológico mediante el cual los organismos intercambian gases con el ambiente. En los humanos, está compuesta por dos grandes procesos: la ventilación pulmonar que es el movimiento de aire hacia adentro y afuera de los pulmones y el intercambio gaseoso que es la difusión de oxígeno hacia la sangre y dióxido de carbono hacia el exterior. Este proceso depende de la distensibilidad del sistema respiratorio y la resistencia de las vías aéreas. 

A su vez hay diferentes variables físicas medibles como el volumen pulmonar, flujo de aire, presión y concentración de gases que permiten hacer análiss sobre la salud de una persona. 

Variables Principales
Las tres variables físicas esenciales son la presión, el flujo y el volumen. La presión genera gradientes que mueven el aire hacia los alvéolos, el flujo mide la velocidad del movimiento aéreo (en L/min), y el volumen cuantifica la cantidad de aire desplazado. Estas se ven influenciadas por la elasticidad pulmonar y resistencias de las vías aéreas.

Mecánica Respiratoria
La inspiración ocurre por reducción de la presión intrapulmonar (ley de Boyle: presión inversa al volumen), gracias a la contracción del diafragma y músculos intercostales. En la espiración, la elasticidad torácica genera presión positiva para expulsar aire, limitada por el cierre de vías aéreas pequeñas. La viscosidad y tensión superficial (modulada por surfactante) afectan estas dinámicas, se requiere un transductor que convierta la magnitud en señal eléctrica y por medio de un sistema de adquisición se digitalizará la señal para poder ser visualizada y poder tomar la frecuencia respiratoria, siendo la frecuencia respiratoria el número de ciclos respiratorios completos por minuto y está podrá ser calculada según los picos de la señal respiratoria.
​

#  Monitoreo de la Frecuencia Respiratoria y Análisis del Habla

##  Descripción del proyecto
Práctica de laboratorio enfocada en el monitoreo del proceso respiratorio mediante la adquisición y el análisis de una señal biológica. El objetivo principal es evaluar cómo la verbalización modifica el patrón y la frecuencia respiratoria en comparación con un estado de reposo. La practica integra hardware de adquisición, sensores fisiológicos y herramientas de procesamiento digital de señales en MATLAB.

##  Objetivos

### Objetivo general
Evaluar  el patrón respiratorio.

### Objetivos específicos
- Identificar las principales variables físicas involucradas en el proceso respiratorio.
- Diseñar un sistema capaz de adquirir la señal respiratoria y calcular la frecuencia respiratoria.
- Analizar cambios en el patrón respiratorio asociados a tareas de verbalización.


PARTE A.
## Sensor
Seleccionar el sensor que considere más adecuado para medir la variable de
interés y, de esa forma, capturar las variaciones producidas por el proceso
respiratorio. Considere un voltaje de alimentación de +3.3 a +5 VDC, en el
caso de tratarse de un sensor pasivo. Medite sobre cómo adaptar el sensor al
cuerpo del sujeto de prueba para capturar la señal con un mínimo de
interferencia.
Se usó el conversor análogo-digital integrado en la placa Arduino.

## Resultados
“Serial Plotter” del menú “Herramientas” del entorno de
programación,
capturas de pantalla que muestren la señal:
a. En reposo (cuente manualmente el número de veces que el sujeto inhala o
exhala).
b. Mientras el sujeto de prueba habla o lee.

### Código Arduino:

```cpp
const int sensorPin = A0;
const unsigned long Ts = 20; // 20 ms -> 50 Hz
unsigned long t0 = 0;

void setup() {
  Serial.begin(115200);
}

void loop() {
  if (millis() - t0 >= Ts) {
    t0 = millis();

    int adcValue = analogRead(sensorPin);
    float voltage = adcValue * (5.0 / 1023.0);

    // Enviar SOLO el voltaje (ideal para Serial Plotter y MATLAB)
    Serial.println(voltage);
  }
}
```

PARTE B
## código en MATLAB que permita la captura

2. Capturar 30 segundos de señal respiratoria bajo las condiciones establecidas
en el paso 5 de la parte A (incisos “a” y “b”). Recuerde guardar en cada caso el
correspondiente archivo .MAT.
3. De ser necesario, aplique los filtros correspondientes para mejorar la calidad
de ambas señales. Especifique el tipo de filtro (pasa-bajas, pasa banda) y la(s)
frecuencia(s) de corte.
4. Obtenga la representación en frecuencia de ambas señales e identifique la
frecuencia dominante en cada caso.




## Conclusión: 

Pregunta 1: ¿Son los patrones respiratorios y frecuencias respiratorias
iguales o diferentes en cada caso? ¿A qué se debe esto?
Pregunta 2: ¿Cuáles serían las ventajas y desventajas de emplear múltiples
sensores para el monitoreo del proceso respiratorio? ¿Cuáles podrían ser
las razones?


