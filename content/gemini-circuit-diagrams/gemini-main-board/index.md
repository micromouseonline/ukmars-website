---
title: Main Chassis & Mezzanine
date: '2025-08-08T21:31:52Z'
lastmod: '2025-08-19T20:04:09Z'
wp_id: 3524
---

Below are the circuits relating to the main chassis PCB. These are followed by those for the Mezzanine board which holds the processor and connected to the sensor boards

## Main Chassis PCB {#Main_Chassis_PCB}

Firstly the battery and main power circuit that powers the motors. Note the protection diode to prevent the battery being connected the wrong way round

![](/ukmars/wp-content/uploads/2025/08/image-68-640x332.png)

This provides the 5 volt supply for the processor and motor driver

![](/ukmars/wp-content/uploads/2025/08/image-69-640x349.png)

This is the motor controller circuit

![](/ukmars/wp-content/uploads/2025/08/image-70-640x299.png)

These are the left and right motor connections

![](/ukmars/wp-content/uploads/2025/08/image-71-640x210.png)

These are the connections to the mezzanine board through the two 6 pin connectors

![](/ukmars/wp-content/uploads/2025/08/image-72-640x174.png)

Finally the power smoothing circuits

![](/ukmars/wp-content/uploads/2025/08/image-73-640x291.png)

## Mezzanine PCB {#Mezzanine_PCB}

Below are the circuits for the mezzanine board

This connects the mezzanine board to the main chassis via two 6 pin connectors

![](/ukmars/wp-content/uploads/2025/08/image-80-640x231.png)

These are the processor Raspberry Pi Pico connections. They are the same for whichever version of the Pico you are using

![](/ukmars/wp-content/uploads/2025/08/image-81-640x499.png)

This is the 16 pin sensor connector J1

![](/ukmars/wp-content/uploads/2025/08/image-82.png)

There are 2 breakout connectors J2 and J5 that can be used in several different ways as described

![](/ukmars/wp-content/uploads/2025/08/image-83-640x278.png)

These 2 LED indicators can be used as you wish, such as for showing which program has been selected on the tactile switches. Also 2 of the 3 tactile switches SW1 and SW2 can be read by the Pico. The 3rd one SW3 is a reset button for the processor.

![](/ukmars/wp-content/uploads/2025/08/image-85-640x248.png)
