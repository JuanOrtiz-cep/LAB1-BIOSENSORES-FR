# LAB1-BIOSENSORES-FR
Se desarrollo un sistema capaz de adquirir la señal respiratoria para calcular la frecuencia respiratoria de un sujeto sano.

# 🫁 Monitoreo de la Frecuencia Respiratoria y Análisis del Habla

##  Descripción del proyecto
Este repositorio contiene el desarrollo de una práctica de laboratorio enfocada en el **monitoreo del proceso respiratorio** mediante la adquisición y el análisis de una señal biológica. El objetivo principal es **evaluar cómo la verbalización (hablar o leer en voz alta) modifica el patrón y la frecuencia respiratoria** en comparación con un estado de reposo.

El proyecto integra hardware de adquisición (Arduino), sensores fisiológicos y herramientas de procesamiento digital de señales en MATLAB.

---

##  Marco teórico
La respiración es un proceso fisiológico esencial que permite el intercambio de gases entre el organismo y el ambiente. Durante la inhalación, el aire rico en oxígeno ingresa a los pulmones, donde el oxígeno atraviesa la membrana alveolocapilar hacia el torrente sanguíneo. De manera complementaria, el dióxido de carbono, producto del metabolismo celular, es eliminado durante la exhalación. Este conjunto de eventos conforma el ciclo respiratorio.

La **frecuencia respiratoria (RR)** es uno de los signos vitales más relevantes para la evaluación del estado clínico de una persona. Alteraciones en este parámetro suelen estar asociadas a patologías respiratorias, cardiovasculares o metabólicas. Estudios clínicos han demostrado que cambios anormales en la frecuencia respiratoria pueden anticipar eventos críticos como el ingreso a unidades de cuidados intensivos o el paro cardíaco, incluso con varias horas de anticipación.

A diferencia de otros signos vitales como la presión arterial o la frecuencia cardíaca, la frecuencia respiratoria presenta una alta sensibilidad para diferenciar pacientes estables de aquellos en riesgo. Por esta razón, su medición continua y análisis resultan de gran interés en aplicaciones biomédicas y de monitoreo clínico.

---

##  Objetivos

### Objetivo general
Evaluar la influencia del habla o verbalización sobre el patrón respiratorio.

### Objetivos específicos
- Identificar las principales variables físicas involucradas en el proceso respiratorio.
- Diseñar un sistema capaz de adquirir la señal respiratoria y calcular la frecuencia respiratoria.
- Analizar cambios en el patrón respiratorio asociados a tareas de verbalización.

---

##  Descripción de la práctica
En esta práctica se diseña y construye un sistema de monitoreo respiratorio que permite comparar la **frecuencia respiratoria** y el **comportamiento del ciclo respiratorio** bajo dos condiciones experimentales:
- Estado de reposo.
- Estado de verbalización (hablar o leer).

---

##  Materiales del laboratorio
- Generador de señales biológicas  
- Osciloscopio digital  
- Fuente de voltaje DC  
- Computador con acceso a Internet  
- MATLAB  
- Arduino UNO o Nano  
- Protoboard  
- Cables de conexión  

---

##  Seguridad en el laboratorio
- Verificar niveles de voltaje y corriente antes de energizar el sistema.
- Usar adecuadamente los elementos de protección personal.
- Cerrar sesiones y no dejar archivos guardados en equipos institucionales.

---

##  Metodología

###  Parte A: Adquisición de la señal respiratoria
1. Revisión bibliográfica del proceso respiratorio y sus variables físicas.
2. Selección de un sensor adecuado para capturar la señal respiratoria.
3. Diseño del sistema de acondicionamiento y digitalización usando Arduino.
4. Prueba del sistema en un sujeto sano.
5. Visualización de la señal mediante **Serial Plotter** en:
   - Reposo.
   - Verbalización.

---

###  Parte B: Procesamiento de la señal
1. Desarrollo de un script en MATLAB para la captura temporizada de la señal.
2. Registro de 30 segundos de señal en ambas condiciones.
3. Aplicación de filtros digitales para mejorar la calidad de la señal.
4. Análisis en el dominio de la frecuencia e identificación de la frecuencia dominante.

---

###  Parte C: Documentación
- Explicación detallada del procedimiento experimental.
- Análisis de resultados obtenidos.
- Elaboración de conclusiones.
- Organización de un repositorio en GitHub con todo el material generado.

---

##  Resultados esperados
- Diferencias observables en el patrón respiratorio entre reposo y verbalización.
- Cambios en la frecuencia respiratoria durante el habla.
- Identificación clara de la frecuencia respiratoria dominante en cada condición.

---

##  Estructura del repositorio
