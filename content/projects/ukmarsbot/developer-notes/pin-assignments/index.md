---
title: Pin Assignments and program set up
date: '2020-07-25T10:42:05Z'
lastmod: '2026-09-04T20:33:41Z'
wp_id: 1416
---

Below are the pin assignments for use in Arduino sketch followed by those for Micro-python

## Arduino Nano pin assignments for programming with Arduino Sketch {#Arduino_Nano_pin_assignments_for_programming_with_Arduino_Sketch}

The UKMARSBOT robot PCB assigns specific roles to most of the input and output pins. As these are fixed, it is important to use the correct pins for the assigned functions. To help in programming, these pins have been allocated meaningful names as shown below.  
Include this section of Sketch code below at the start of your program to make these standard names available for use in your program

```
// Input pins:
int lside         = A0; // left side sensor input
int rfront        = A1; //front left line sensor input
int lfront        = A2; //front right left sensor input
int rside         = A3; // right side sensor input
int sens1         = A4; // unassigned sensor input 1
int sens2         = A5; // unassigned sensor input 2
int fourwayswitch = A6; // input from function switch
int battery       = A7; // input for battery measurement
int Receive      = 0;  // Receive pin
int Transmit      = 1:  // Transmit pin
int m1encoder1    = 2;  // motor 1 encoder 1 input interrupt pin
int m1encoder2    = 4;  // motor 1 encoder 2 input
int m2encoder1    = 3;  // motor 2 encoder 1 input interrupt pin
int m2encoder2    = 5;  // motor 2 encoder 2 input
// Output pins:
int sensorLED1    = 6;  // 1st diagnostic LED on sensor board
int lmotorDIR     = 7;  // Left motor dirn input 1
int rmotorDIR     = 8;  // Right motor dirn input 3
int lmotorPWM     = 9;  // Left motor PWN pin<br />
int rmotorPWM     = 10; // Right motor PWN pin<br />
int sensorLED2    = 11; // 2nd diagnostic LED on sensor board<br />
int trigger       = 12; // trigger for sensor LEDs<br />
int LED13         = 13; // ext LED Red<br />
```

In the void setup () section of your program also include the following section of Sketch code:

```
  pinMode(sensorLED1, OUTPUT);
  pinMode(lmotorDIR, OUTPUT);
  pinMode(rmotorDIR, OUTPUT);
  pinMode(lmotorPWM, OUTPUT);
  pinMode(rmotorPWM, OUTPUT);
  pinMode(sensorLED2, OUTPUT);
  pinMode(trigger, OUTPUT);
  pinMode(LED13, OUTPUT);
  pinMode(m1encoder1, INPUT);
  pinMode(m1encoder2, INPUT);
  pinMode(m2encoder1, INPUT);
  pinMode(m2encoder2, INPUT);
```

Also include this next line in the `void setup()` section to allow the serial monitor to work

```
  Serial.begin(9600);          // set up serial monitor comms on USB
```

## Installing Micro python on the Cytron Maker Nano RP2040 {#Installing_Micro_python_on_the_Cytron_Maker_Nano_RP2040}

When you purchase a Cytron Maker Nano RP2040 board it comes with Circuit-Python installed on it. It is best to replace this with Micro-Python which has better functionality. To do this: Go to this web page https://micropython.org/download/RPI\_PICO/ and download the latest .uf2 file. Then with the white button labelled BOOT held down, plug in the USB connection on the CPU board to your computer. A file explorer window should open called RPI-RP2 showing a couple of files. Now copy the downloaded .uf2 file to this folder, and then disconnect the board from your computer. You should now have Micro-Python on the CPU board.

## Installing Micro python on the Waveshare ESP32 S3 Nano {#Installing_Micro_python_on_the_Waveshare_ESP32_S3_Nano}

Instructions for loading Micro-python on the Waveshare ESP32 S3 Nano are given at :

<https://www.davidhannaford.com/esp32/ESP32S3Nano.pdf>

## Micro python pin assignments for programming with Thonny on Cytron Maker Nano Rp2040 {#Micro_python_pin_assignments_for_programming_with_Thonny_on_Cytron_Maker_Nano_Rp2040}

Place these import statements at the beginning of your code:

from machine import Pin, ADC, PWM  
import neopixel  
import time

\# Set pins for digital outputs on Cytron Maker Nano RP2040

LED\_PIN = Pin(18, Pin.OUT) \# ext LED on GP18  
RMOTOR\_DIR = Pin(8, Pin.OUT)  
LMOTOR\_DIR = Pin(7, Pin.OUT)  
PIEZO\_PIN = Pin(22, Pin.OUT) \# Pin connected to piezo buzzer  
SENSOR1\_PIN = Pin(19, Pin.OUT) \# 1st Sensor LED on line follow sensor board  
SENSOR2\_PIN = Pin(6, Pin.OUT) \# 2nd Sensor LED on line follow sensor board  
TRIGGER\_PIN = Pin(16, Pin.OUT) \# Trigger for LEDs on line follow sensor board

\# Define PWM motor speed pins

LMOTOR = machine.Pin(9) \# left motor is pin 9  
MOTOR = machine.Pin(17) \# right motor is pin 17  
LMOTOR\_PWM = machine.PWM(machine.Pin(9))  
RMOTOR\_PWM = machine.PWM(machine.Pin(17))  
LMOTOR\_PWM.freq(2000)  
RMOTOR\_PWM.freq(2000)  
LMOTOR\_PWM.duty\_u16(0) \# left motor speed – range is 0 to 65535  
RMOTOR\_PWM.duty\_u16(0) \# right motor speed – range is 0 to 65535

\# Define analogue inputs used on sensor board

Lsidesense = ADC(Pin(29)) \# A3  
Lfrontsense = ADC(Pin(28)) \# A2  
Rfrontsense = ADC(Pin(27)) \# A1  
Rsidesense = ADC(Pin(26)) \# A0

\# Define RP2040 on-board button with pull up so it goes false when pressed

btn1 = machine.Pin(20, Pin.IN, Pin.PULL\_UP)

\# Define press button switch on UKMARS board

Switch = Pin(14, Pin.IN) \# button / switch pin

Follow this with your procedure definition and then the code that you want to run when the program starts

## **Micro python pin assignments for programming with Thonny on the Waveshare ESP32 S3 Nano** {#Micro_python_pin_assignments_for_programming_with_Thonny_on_the_Waveshare_ESP32_S3_Nano}

The ESP32 uses GPIO numbers as pin numbers in Micro-Python so use these pin definitions:

RMOTOR\_DIR = Pin(17, Pin.OUT) \#  right motor direction

LMOTOR\_DIR = Pin(10, Pin.OUT) \#  left motor direction

LED\_PIN = Pin(48, Pin.OUT)   \# ext red LED on PCB if present

SENSOR1\_PIN = Pin(12, Pin.OUT) \# 1st indicator LED on sensor board

SENSOR2\_PIN = Pin(11, Pin.OUT)  \# 2nd indicator LED on sensor board

TRIGGER\_PIN1 = Pin(47, Pin.OUT) \# Trigger for LEDs on sensor board

TRIGGER\_PIN2 = Pin(38, Pin.OUT) \# Trigger for LEDs on sensor board

\#define PWM motor speed pins

LMOTOR\_PWM = PWM(Pin(18))  \# left motor PWM

RMOTOR\_PWM = PWM(Pin(21)) \# right motor PWM

LMOTOR\_PWM.freq(2000) \# set PWM frequency

RMOTOR\_PWM.freq(2000) \# set PWM frequency

\# Define analogue inputs used on line sensors

Lfrontsense = ADC(Pin(3))  \# 

Rfrontsense = ADC(Pin(2))  \# 

Lsidesense = ADC(Pin(4))   \#  Sees change of radius markers

Rsidesense = ADC(Pin(1))   \#  Sees start and end markers

Rwidesense = ADC(Pin(11)) \# A4 new right side wide sensor

Lwidesense = ADC(Pin(12)) \# A5 new left side wide sensor

funcswitch = ADC(Pin(13)) \# A6 4 way function switch

battery = ADC(Pin(14)) \# A7 battery volts

\# encoder pins

Leftenc1 = Pin(5, Pin.IN) \#

Rightenc1 = Pin(6, Pin.IN) \#

Leftenc2 = Pin(7, Pin.IN) \#

Rightenc2 = Pin(8, Pin.IN) \#
