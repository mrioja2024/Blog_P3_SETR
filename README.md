

**Video:** https://github.com/user-attachments/assets/77678807-80b9-480b-ba7b-b14a922051b7




# Blog_P3_SETR
## Practica 3: Controlador de Máquina Expendedora
### 1. Introducción
El objetivo de esta practica es desarrollar el controlador de una maquina expendedora mediante Arduino, integrando sensores y actuadores.

Para ello se ha utilizado una placa Arduino MEga 2560, una pantalla LCD 1602, un joystick analógico, un sensor DHT11, un sensor ultrasonidos HC-SR04, un pulsador externo y dos LEDs.

EL programa está organizado mediante máquinas de estado para gestionar el funcionamiento de la máquina sin depender de esperas largas mediante delay().

### 2. Montaje del circuito
El circuito se ha montado sobre una protoboard conectando distintos componentes al Arduino Mega 2560, como hemos comentado antes.

La pantalla LCD se comunica en modo paralelo de 4 bits. El joystick permite navegar por los menús y seleccionar opciones, mientras que el pulsador externo controla la cancelación y el acceso al modo administrador.

**Fotos y video del montaje y funcionamiento:**


<img width="4284" height="5712" alt="IMG_4895" src="https://github.com/user-attachments/assets/1cf7e2c8-eb59-4abe-b008-45fe7363fe4b" />
<img width="4284" height="5712" alt="IMG_4893" src="https://github.com/user-attachments/assets/151c8a58-bc7c-4674-a25b-296ca53b4cd9" />




**Esquemático:**
<img width="1726" height="1244" alt="fritzing" src="https://github.com/user-attachments/assets/fd685d61-9a2d-4d0c-be87-65a6e25d7cd8" />

### 3. Organización del software
La solución se basa en una máquina de estados principal con tres modos de funcionamiento:

#### ARRANQUE
Al inciar el Arduino, la pantala muetsra CARGANDO... mientars el LED1 parpadea tres veces. Después el programa pasa automáticamente al modo Servicio.

#### SERVICIO
Inicialmente, el sistema permanece esperando a que el sensor de ultrasonidos detecte un cliente a menos de 100cm.

Cuando sae detecta un cliente, se muestra la temperatura y la humedad durante cinco segundos. Después se permite seleccionar una de las cinco bebidas utilizanod eljoystick.

Tras confirmar la selección, se simula la preparación de loa bebida durante un tiempo pseudoaleatorio de entre cuatro y ocho segundos.

Durante la preparación se utiliza PWM para aumentar progresivamente el brillo de LED2.

Finalmente, la pantalla muestra REITRE BEBIDA durante tres segundos y el sistema regresa al estado de espera.

#### ADMIN
Se accede al modo administrador manteniendo pulsado el botón externo durante 5 segundos.

El menú permite consultar la temperatura y humedad, visualizar la distancia medida por el sensro ultrasónico, consultar el tiempo trasncurrido desde el encendido y modificar los precios de las bebidas.

Los precios se modifican en pasos de 0,05, y para ello se utiliza una variable temporal expresada en céntimos, evitando modificar el precio original hasta que se confirma el cambio con el joystick.

También es posible cancelar la modificación y conservar el precio anterior.

### 4.Recursos de programación utilizados
#### Máquinas de estados
Se han utilizado estrcuturas enum y switch para organizar el programa en estados y subestados.
Esta organización permite controlar qué operaciones deben ejecutarse en cada momento y facilita las transiciones entre los modos de Arrnaque, Servicio y Administrador.

#### Temporización con millis()
Se utiliza millisÇ() para controlar los tiempos de arranque, visualización, preparación y entrega sin recurrir a esperas largas con delay().

Esto permite que el programa principal continúe ejecutándose y atendiendo otras acciones.

#### Interrupciones hardware

El pulsador externo está conectado al pin D2 y utiliza attachInterrupt() con el modo CHANGE.

La interrupción registra los cambios del pulsador y permite distinguir entre una pulsación de 2 a 3 segundos, destinada a cancelar una operación y una pulsación de al menos 5 segundos, utilizada para entrat o salir de ADMIN.

Para compartir información entre la interrupción y el programa principal se emplean variables volatile. También se aplica un filtrado temporal básico para reducir los rebotes del pulsador.

#### Watchdog
Se ha configurado el Watchdog hardware mediante la biblioteca avr/wdt.h, con un tiempo límite de ods segundos.
El programa refresca su contador al finalizar cada iteración de loop(). Si el software se bloquea y no lo refresca a tiempo, el Watchdog puede provocar un reinicio del microcontrolador.

#### Control PWM
Durante la preparación de una bebida se utiliza analogWrite() para controlar el brillo del LED". La función map() transforma proporcionalmente el tiempo de preparación trasncurrido en un valor entre 0 y 255

#### Sensor ultrasónico
El HC-SR04 utiliza un pulso de disparo en TRIG y un pulso de respuesta en ECHO. La duración de este último permite calcular la distancia.

Se utiliza pulseIn() con un tiempo de espera limitado a 8000 microsegundos. Esta operación sigue siendo bloqueante, aunque con un timepo máximo acotado.

### 5.Conclusiones
Esta práctica ha permitido integrar sensores y actuadores en unúnico sistema empotrado, organizando el comportamiento mediante máquinas de estados.

Se han aplicado conceptos como interrupciones, temporización, PWM y Watchdog, además de gestionar la interacción con el usuario mediante una pantalla LCD y un joystick.
