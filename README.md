# Nordic-BLE-EKG
 
This is the main repository for the npm11

# Components:

All components are designed to be used with the Nordic ecosystem and to be energy efficient..

- [nPM1100 EK](https://www.nordicsemi.com/Products/Development-hardware/nPM1100-EK)
- [XIAO nRF52840](https://www.seeedstudio.com/Seeed-XIAO-BLE-nRF52840-p-5201.html)
- [ECG 3 click](https://www.mikroe.com/ecg-3-click)
- LiPo Battery 3.7v, 4.2v max, 1C

NOTE: due to a manufacturing defect the polarity of the battery port is reversed, so if you wish to use the same nPM1100 for this project remember to reverse the polarity of the connector as shown in the diagram, otherwise you run the risk of making a big mistake. Short circuits are not fun. This was just the case of MY OWN npm device, you have to check the polarity of your own if you wish to replicate this project.

<img src="./Images/invert.png">

# Introduction to this series


# A Little bit on the problem and why it is important to quantify health markers.




# Design:

This is the connection diagram of the components separately from the circuit if you want to do it in a modular way with these pieces, however, a PCB will be made soon with all the components on it.

- Communication with the ECG is done through the SPI protocol, unlike other more economical modules such as the AD8232 that are handled with analog readings and occupy an ADC.
- The power that we are supplying with the nPM1100 EK is 3v, which is the maximum voltage that the EK supplies.

<img src="./Images/Design_bb.png">

The EK configuration is as follows.

<img src="./Images/EKconfig.png">

# Connection Diagram:

To use the device, an ECG cable connected to the arms was connected to the ECG module, which has a Jack input, later this through BLE sends the data at a frequency of 100Hz to the app to be able to visualize a coherent graph.

<img src="./Images/diagram.png">

Due to the fact that this is a device that we are going to be using for long periods of time and it is also a device that must be used every day, we can understand that the use of disposable electrodes is not feasible. So that's why we decided to make our own dry electrodes.

Materials:

- Copper Plate.
- Silver Conductive Ink.
- Electrode External Snap.

<img src="https://hackster.imgix.net/uploads/attachments/1253077/68747470733a2f2f692e6962622e636f2f684c5a384454422f32303231303133302d3230343031332e706e67.png?auto=compress%2Cformat&w=1280&h=960&fit=max">

# BLE Service:

All ECG information is sent at a frequency of 100Hz to the device that is connected to it.

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

Within the official documentation they indicate how to read the current consumption of the nPM with the PPKII.

<img src="./Images/ppk-example.png">

[Nordic Official Documentation](https://infocenter.nordicsemi.com/index.jsp?topic=%2Fug_npm1100_ek%2FUG%2FnPM1100_EK%2Fppk2_current_measurement.html)

The power consumption of our entire design is less than 10mAh, as can be seen in our measurements with the PPKII.

- Connection of the POC to the PPKII in Ampere Meter mode.

<img src="./Images/ppk.jpg">

- Device measurements, we have peaks of 20mA due to the reading of the ECG data every 10ms.

<img src="./Images/ppk-20220315T223256.png">

- Here is a 2 min consumption test.
- 
<img src="./Images/2minTest.png">

# POC:

Finally we put everything in a 3D printed case for the moment.

<img src="./Images/20220316_235156.jpg">

# End of Part 1 and Next steps:

As a three part series this is just the initial design, component selection, showcase of the npm1100

