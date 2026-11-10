---
title: I2C Sensor Controller (ISC) for UKMARSBOT
date: '2021-04-05T15:54:49Z'
lastmod: '2024-01-22T23:04:01Z'
url: /2021/04/i2c-sensor-controller-isc-for-ukmarsbot/
categories:
- Member's Robots
- Technotes
tags:
- Arduino Library
- I2c
- I2C Sensors
- ISC
- Sensor Board
- UKMARSBOT
wp_id: 1925
---

The purpose of the ISC project is to offload sensor control to an embedded controller which communicates over an I2C interface to the UKMARSBOT MCU.

The ISC comprises a programmed ATtiny814 acting as an I2C Slave on a PCB which plugs in between the UKMARSBOT sensor board connection and cable to the sensor board itself.

![](/ukmars/wp-content/uploads/2021/02/IMG_8074-640x480.jpg)

Possible benefits include, but are not limited to:

  - Simplifies Arduino Sensor Code
      - Start/Stop marker detection by using configurable interrupts and internal hysteresis to prevent nuisance trips
  - Simplifies Arduino LED Indicator Code
  - Frees up Analog Inputs for other tasks
  - Facilitates the use of the I2C bus on the MARSBOT
      - Allowing Accelerometer / displays to be fitted
  - Faster Sample time (to be quantified)
  - I2C interface makes sensor boards compatible with MCUs with no Analog Inputs.

The project comprises of; ISC Arduino Library, supporting documentation and ISC PCB. All of which may be downloaded from: <https://github.com/slinkyfish/ISC-Project>

## ISC Arduino Library {#ISC_Arduino_Library}

The Arduino Library includes example sketches:

  - Example 0 Blink
  - Example 1 Left LED control
  - Example 2 Read Sensor
  - Example 3 Scan Time
  - Example 4 Interrupts

The below code \[Example 0\] is all that is required to start the Sensor board lights flashing.

![](/ukmars/wp-content/uploads/2021/04/Example0-640x171.png)

The below code \[Example 2\] configures SENSOR1 to use transmitter to reduce the affect of ambient light, then prints the sensor value to the screen every 100ms.

![](/ukmars/wp-content/uploads/2021/04/Example2-640x232.png)

## ISC board / firmware {#ISC_board_firmware}

I have 10 ISC boards with firmware installed. I am not sure how best to distribute these should anyone be interested in obtaining one. I can make design files and source code available, but a UPDI programmer is required to flash the ATtiny814 on the ISC itself.

![](/ukmars/wp-content/uploads/2021/04/diagram-640x299.png)
