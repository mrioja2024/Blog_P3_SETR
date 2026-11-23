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
<img width="1726" height="1244" alt="fritzing(1)" src="https://github.com/user-attachments/assets/bda450bd-6f91-4ac8-b04c-5f9ff78dfa26" />

### 3. Organización del software
La solución se bas aen una máquina de estados principal con tres modos de funcionamiento:
