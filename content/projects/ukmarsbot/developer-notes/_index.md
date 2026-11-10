---
title: Developer Notes
date: '2020-07-25T10:37:26Z'
lastmod: '2024-07-26T16:51:00Z'
weight: 4
wp_id: 1409
---

UKMARSBOT Development software

You can choose to develop using the Arduino Sketch environment, or use micro-python with the Thonny environment

## Arduino Nano development environment setup {#Arduino_Nano_development_environment_setup}

If you don’t have the Arduino IDE installed, go to https://www.arduino.cc/en/software and download the latest version for your PC type. Versions are available for the Windows, Linux and Mac OS.

Look in the Pin Assignments page for the code that you will need to set up the inputs and outputs from the processor board.

## Cytron Maker Nano RP2040 development environment setup {#Cytron_Maker_Nano_RP2040_development_environment_setup}

If you don’t have the Arduino IDE installed, go to https://thonny.org/ and download the latest version for your PC type. Versions are available for the Windows, Linux and Mac OS.

The RP2040 comes  with CircuitPython installed on it. However, CircuitPython has non standard input and output commands and does not support interrupts, so it is a good move to reload the board with standard MicroPython.

To do this, go to:

[https://micropython.org/download/rp2-pico](https://micropython.org/download/RPI_PICO/)

Download the latest version  – probably v1.23.0 (2024-06-02).uf2 or later

Hold down the BOOT button on the Cytron Maker Nano RP2040 board while plugging the board into USB port on you PC. Copy the downloaded uf2 file to the USB mass storage device that appears. Once programming of the new firmware is complete the device will automatically reset and be ready for use. You now have MicroPython installed. In Thonny click on Run / Select interpreter/ MicroPython (Raspberry Pi Pico)

You are now ready to start programming in python. Look in the Pin Assignments page for the code that you will need to set up the inputs and outputs from the processor board.
