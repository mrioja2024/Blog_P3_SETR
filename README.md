# Blog_P3_SETR
## Practica 3: Controlador de Máquina Expendedora
### 1. Introducción
El objetivo de esta practica es desarrollar el controlador de una maquina expendedora mediante Arduino, integrando sensores y actuadores.

Para ello se ha utilizado una placa Arduino MEga 2560, una pantalla LCD 1602, un joystick analógico, un sensor DHT11, un sensor ultrasonidos HC-SR04, un pulsador externo y dos LEDs.

EL programa está organizado mediante máquinas de estado para gestionar el funcionamiento de la máquina sin depender de esperas largas mediante delay().

### 2. Montaje del circuito
El circuito se ha montado sobre una protoboard conectando distintos componentes al Arduino Mega 2560, como hemos comentado antes.

La pantalla LCD se comunica en modo paralelo de 4 bits. El joystick permite navegar por los menús y seleccionar opciones, mientras que el pulsador externo controla la cancelación y el acceso al modo administrador.

** Fotos del montaje: **



** Esquemático: **
<img width="1726" height="1244" alt="fritzing" src="https://github.com/user-attachments/assets/fd685d61-9a2d-4d0c-be87-65a6e25d7cd8" />

### 3. Organización del software
La solución se bas aen una máquina de estados principal con tres modos de funcionamiento:
#### ARRANQUE
Al inciar el Arduino, la pantala muetsra CARGANDO... mientars el LED1 parpadea tres veces. Después el programa pasa automáticamente al modo Servicio.
### SERVICIO
Inicialmente, el sistema permanece esperando a que el sensor de ultrasonidos detecte un cliente a menos de 100cm.

Cuando sae detecta un cliente, se muestra la temperatura y la humedad durante cinco segundos. Después se permite seleccionar una de las cinco bebidas utilizanod eljoystick.

Tras confirmar la selección, se simula la preparación de loa bebida durante un tiempo pseudoaleatorio de entre cuatro y ocho segundos.

Durante la preparación se utiliza PWM para aumentar progresivamente el brillo de LED2.

Finalmente, la pantalla muestra REITRE BEBIDA durante tres segundos y el sistema regresa al estado de espera.
