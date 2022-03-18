# Nordic-BLE-EKG
 
Este es el repositorio principal para el Modulo EKG BLE para nordic.

# Components:

Todos los componentes se pensaron para usarse con el ecosistema de Nordic y ser de bajo consumo energetico.

- [nPM1100 EK](https://www.nordicsemi.com/Products/Development-hardware/nPM1100-EK)
- [XIAO nRF52840](https://www.seeedstudio.com/Seeed-XIAO-BLE-nRF52840-p-5201.html)
- [ECG 3 click](https://www.mikroe.com/ecg-3-click)
- LiPo Battery 3.7v, 4.2v max, 1C

NOTE: debido a un defecto de facbricacion la polaridad de el puerto de la bateria esta invertido, entonces si deseas usar el mismo nPM1100 para este proyecto recuerda invertir la polaridad del conector como se muetsra el diagrama, de no hacerlo corres el riesgo de hacer un corto circuito.

<img src="./Images/invert.png">

# Design:

Este es el diagrama de conexiones de los componentes por separado del circuito si es que deseas hacerlo de forma modular con estas piezas, sin embargo proximamente se hara una PCB con todos los componentes sobre el.

- La comunicacion con el ECG se realiza mediante protocolo SPI, a diferencia de otros modulos mas econocmicos como el AD8232 que se manejan con lecturas analogas y ocupan un ADC.
- La energia que estamos suministrando con la nPM1100 EK es de 3v, que es el voltaje maximo que suministra el EK.

<img src="./Images/Design_bb.png">

La configuracion del EK es la siguiente.

<img src="./Images/EKconfig.png">

# Connection Diagram:

Para el uso del device se conecto un cable de ECG conectado en los brazos al modulo de ECG, el cual tiene una entrada Jack, posteriormente este mediante BLE le manda los datos a una frecuencia de 100Hz a la app para poder visualizar una grafica coherente.

<img src="./Images/diagram.png">

Due to the fact that this is a device that we are going to be using for long periods of time and it is also a device that must be used every day, we soon understood that the use of disposable electrodes is not feasible. So that's why we decided to make our own dry electrodes.

Materials:

- Copper Plate.
- Silver Conductive Ink.
- Electrode External Snap.

<img src="https://hackster.imgix.net/uploads/attachments/1253077/68747470733a2f2f692e6962622e636f2f684c5a384454422f32303231303133302d3230343031332e706e67.png?auto=compress%2Cformat&w=1280&h=960&fit=max">

# BLE Service:

Toda la informacion del ECG se manda a una frecuencia de 100Hz al device que se conecte a el.

<img src="./Images/ble.png">

- BLE Service:
  - Name: ECG
  - UUID: 0x2a37
  - BLE Characteristic:
    - UUID: 0x2a37
    - Properties:
      - Read
      - Notify
    - Value:
      - 8-bit unsigned int.

# Power consumption:

Dentro de la documentacion oficial indican como leer el consumo de corriente del nPM con la PPKII.

<img src="./Images/ppk-example.png">

[Nordic Official Documentation](https://infocenter.nordicsemi.com/index.jsp?topic=%2Fug_npm1100_ek%2FUG%2FnPM1100_EK%2Fppk2_current_measurement.html)

El consumo energetico de todo nuestro diseño es menor a 10mAh, como se puede ver en nuestras mediciones con el PPKII.

- Conexion del POC al PPKII en modo Ampere Meter.

<img src="./Images/ppk.jpg">

- Mediciones del device, tenemos picos de 20mA debido a la lectura de los datos del ECG cada 10ms.

<img src="./Images/ppk-20220315T223256.png">

- Aqui una prueba de consumo de 2 min.

<img src="./Images/2minTest.png">

# POC:

Finalmente ponemos todo en una bonita case.

<img src="./Images/20220316_235156.jpg">