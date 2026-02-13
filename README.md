Juan Esteban Ortiz Cepeda            5600742     

Catalina Martínez Franco             5600832

Joseph Emmanuel Rodríguez Ramírez    5600835       


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
La presente práctica de laboratorio enfocada en el monitoreo del proceso respiratorio mediante la adquisición y el análisis de una señal biológica. El objetivo principal es evaluar cómo la verbalización modifica el patrón y la frecuencia respiratoria en comparación con un estado de reposo. La practica integra hardware de adquisición, sensores fisiológicos y herramientas de procesamiento digital de señales en MATLAB.

##  Objetivos

### Objetivo general
Evaluar  el patrón respiratorio.

### Objetivos específicos
- Identificar las principales variables físicas involucradas en el proceso respiratorio.
- Diseñar un sistema capaz de adquirir la señal respiratoria y calcular la frecuencia respiratoria.
- Analizar cambios en el patrón respiratorio asociados a tareas de verbalización.

## Sensor

Se usó el conversor análogo-digital integrado en la placa Arduino usando un Termistor NTC 10 K ohmnios, el cual es un senstor pasivo ya que requiere una fuente externa para su funcionamiento.

### PROCEDIMIENTO

Se escogió el sensor de temperatura Termistor NTC 10kohmnios que posteriormente se conectó con el micro controlador Arduino Nano, usando como entrada para el sensor el pin A0.

Primero se observó la señal usando el serial plotter en Arduino IDE, para obtener una mejor señal adaptamos y poder realizar una mejora externa se coloco el sensor en una en una masacara de oxígeno.

Finalmente en Matlab se programó un código con el procesamiento y filtrados de la señal, el cálculo de las frecuencias respiratorias y las frecuencias dominantes.

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

    Serial.println(voltage);
  }
}
```
IDE Arduino

<img width="1366" height="768" alt="image" src="https://github.com/user-attachments/assets/a48f516d-d53b-4653-a48f-e5f96ad069dd" />

Mientras que haciendo una prueba sencilla de conteo de inhalaciónes y exhalaciones de forma manual a uno de nuestros compañeros, también se observó en la sola IDE de Arduino los cambios de amplitud generados por el sensor.
Hay dos lineas, siendo la azul la recibida por el sensor con un pasabajos, y la roja siendo unos espacios que podrían llegar a considerar cuales son inhalaciones y cuales exhalaciones

<img width="1366" height="768" alt="image" src="https://github.com/user-attachments/assets/477e0f80-bfae-4be0-8f12-a906dce717ba" />

Sin embargo la diferencia no es clara a simple vista y por esto se hace la implementación a matlab para trabajar con más herramientas y filtros.

##  Código Matlab
## Código

```cpp
clear; clc; close all

s = serialport("COM3",115200);
configureTerminator(s,"LF");
flush(s);

answer = inputdlg("Tiempo de adquisición (s):","Configuración",[1 40],{"30"});
T = str2double(answer{1});
Fs = 50;                
N = Fs*T;

t = zeros(1,N);
x = zeros(1,N);
xf = zeros(1,N);

[b_hp,a_hp] = butter(2,0.05/(Fs/2),'high');    
[b_lp,a_lp] = butter(4,5/(Fs/2),'low');       

zi_hp = zeros(max(length(a_hp),length(b_hp))-1,1);
zi_lp = zeros(max(length(a_lp),length(b_lp))-1,1);

%% FIGURA TIEMPO
figure('Name','Monitor Respiratorio - ESP32');
subplot(2,1,1)
h1 = plot(0,0,'Color',[0.6 0.6 0.6]); hold on
h2 = plot(0,0,'b','LineWidth',2);
grid on
xlabel("Tiempo (s)")
ylabel("Voltaje")
legend("Cruda","Filtrada")
title("Señal respiratoria en tiempo real")
xlim([0 T])
ylim([-1 1])


k = 1;
disp("Midiendo...")

while k <= N
    if s.NumBytesAvailable > 0
        v = str2double(strtrim(readline(s)));

        if ~isnan(v)
            t(k) = (k-1)/Fs;
            x(k) = v;

            [yhp, zi_hp] = filter(b_hp,a_hp,v,zi_hp);
            [y, zi_lp] = filter(b_lp,a_lp,yhp,zi_lp);
            xf(k) = y;

            subplot(2,1,1)
            set(h1,'XData',t(1:k),'YData',x(1:k))
            set(h2,'XData',t(1:k),'YData',xf(1:k))
            drawnow limitrate

            k = k + 1;
        end
    end
end

disp("Adquisición finalizada")


Nfft = length(xf);
X = fft(xf);
f = (0:Nfft-1)*(Fs/Nfft);
mag = abs(X)/Nfft;

f = f(1:Nfft/2);
mag = mag(1:Nfft/2);

subplot(2,1,2)
plot(f,mag,'LineWidth',2)
grid on
xlabel("Frecuencia (Hz)")
ylabel("|X(f)|")
title("Espectro de frecuencia")
xlim([0 5])

idx_range = find(f >= 0.15 & f <= 0.7);

[~,idx2] = max(mag(idx_range));
f_resp = f(idx_range(idx2));

FR_fft = f_resp*60;

disp("Frecuencia respiratoria por FFT (rpm):")
disp(FR_fft)

datos.t = t;
datos.raw = x;
datos.filtrada = xf;
datos.FR_fft = FR_fft;
save("respiracion_termistor.mat","datos")

clear s
```
Matlab Code


## En reposo:
<img width="696" height="616" alt="image" src="https://github.com/user-attachments/assets/a4566371-d030-4aae-b46f-db96b5c87f55" />

Para el caso en reposo, se le solicita al paciente que respire de manera natural durante un tiempo determinado, en este caso es de 30 segundos. Ahora bien, en la gráfica observamos un patron de ondas lentas que aunque poseen ruido tienden a ser periódicas, gracias a la transformada de fourier observamos el espectro de frecuencia que nos ayuda a obtener las rpm, en este caso, con respiracion normal y moderada se obtuvieron 16 rpm. 


## Hablando:
<img width="691" height="614" alt="image" src="https://github.com/user-attachments/assets/324a9d64-bdc4-4b0d-b69a-75eda118fcb0" />

En la segunda parte de la medición, se le pide al paciente que realice el mismo ejercicio anterior con la misma duración pero hablando, ya que, ahora se espera que al hablar, se evidencie que la señal tiende a aser algo más ruidosa, irregular, llena de vibraciones rápidas. Es aquí en donde aparecen muchos picos ya que cuando hablamos el aire se usa para producir sonido, por lo cual la respiración se fragmenta. Con esto se mide que la frecuencia es mas baja con relación que el anterior ejercicio, pese a que estamos respirando más rápido. Aquí de igual manera gracias a la FFT pudimos obtener una medida de 12 rpm. 



## Discusión:

1: ¿Son los patrones respiratorios y frecuencias respiratorias iguales o diferentes en cada caso? ¿A qué se debe esto?

R/ Los patrones son similares, sin embargo, la frecuencia al hablar es menor debido  a que se toma aire y se "aguanta" la respiración al hablar, por ende habrá menos picos durante el tiempo tomado.

2: ¿Cuáles serían las ventajas y desventajas de emplear múltiples sensores para el monitoreo del proceso respiratorio? ¿Cuáles podrían ser
las razones?

R/ Las ventajas de usar múltiples sensores podría ser la posibilidad de comparar resultados para encontrar patologías o momentos en común para tener diferentes puntos de vista y diagnosticar con mayor facilidad, es decir, empleados correctamente se pueden complementar, como por ejemplo, para la polisomnografía se requiere aproximádamente 8 tipos de sensores diferentes para realizar el estudio completo.
Sin embargo por esto mismo no todos son igual de efectivos y hay que buscar la compatibilidad, el factor económico es influyente, por eso tiene mucha importancia el estudio de cada uno de estos y sus posibles adaptaciones para mejorar la captura. 

## Conclusión:

En esta práctica de laboratorio se pudo evidenciar la importancia de elegir un sensor acorde a los requerimientos y disponibilidades, haciendo una mejor revisión de la literatura, ya que, aunque a simple vista no se logre ver el cambio en la frecuencia cardiaca o en los picos, al momento de ejecutar el código este detecta por medio de los picos y las frecuencias dominantes que al hablar la frecuencia respiratoria es menor que en un estado de reposo, por lo cual se concluye que es posible realizar la práctica con mejores condiciones, así como es posible aprovechar tanto los filtros digitales como los análogos para lograr lo esperado, sumándole a esto la importancia de reconocer y entender las diferentes mediciones fisiológicas y como obtenerlas a través de los diferentes tipos de sensores.

## Referencias

https://medlineplus.gov/spanish/pruebas-de-laboratorio/pruebas-de-funcion-pulmonar/

https://www.ncbi.nlm.nih.gov/books/NBK607438/

https://www.sciencedirect.com/topics/medicine-and-dentistry/mechanics-of-breathing
