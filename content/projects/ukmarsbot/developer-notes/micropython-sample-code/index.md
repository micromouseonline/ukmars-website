---
title: MicroPython sample code
date: '2024-07-26T19:07:37Z'
lastmod: '2024-07-26T19:29:21Z'
weight: 3
wp_id: 3214
---

## Here is some simple micro python sample line follower code

\# We start with setting up the pin definitions

from machine import Pin, ADC, PWM  
import time

\# then we add some global variable definitions

global leftside, leftfront, rightfront, rightside,

\# pin definitions. Sets pins for digital outputs on Maker Pi RP2040

RMOTOR\_DIR = Pin(8, Pin.OUT) \# right mmotor direction  
LMOTOR\_DIR = Pin(7, Pin.OUT) \# left mmotor direction  
TRIGGER\_PIN = Pin(16, Pin.OUT) \# Trigger for LEDs on line follow sensor board

\# define PWM motor speed pins

LMOTOR\_PWM = machine.PWM(machine.Pin(9)) \# left motor PWM is on pin 9  
RMOTOR\_PWM = machine.PWM(machine.Pin(17)) \# right motor PWM is on pin 17  
LMOTOR\_PWM.freq(2000) \# set PWM frequency  
RMOTOR\_PWM.freq(2000) \# set PWM frequency

\# set both motors to stopped

LMOTOR\_PWM.duty\_u16(0) \# left motor speed – range is 0 to 65535  
RMOTOR\_PWM.duty\_u16(0) \# right motor speed – range is 0 to 65535

\# Define analogue inputs used on sensor board

Lsidesense = ADC(Pin(29)) \# A3  
Lfrontsense = ADC(Pin(28)) \# A2  
Rfrontsense = ADC(Pin(27)) \# A1  
Rsidesense = ADC(Pin(26)) \# A0

\# This is some code to read the 4 line sensors

def photoread():  
global leftside, leftfront, rightfront, rightside  
TRIGGER\_PIN.value (True) \# switch on LEDs on sensor board  
time.sleep(0.01)  
leftside = Lsidesense.read\_u16()  
leftfront = Lfrontsense.read\_u16()  
rightfront = Rfrontsense.read\_u16()  
rightside = Rsidesense.read\_u16()  
TRIGGER\_PIN.value (False)  
return

\# and here is a simple line following routine that uses the photoread() routine above

def simplelinefollow(): \# Basic proportional line follower  
global leftside, leftfront, rightfront, rightside  
basespeed = 15000  
prevdiff = 0  
while (True):  
photoread()  
diff = int(((leftfront – rightfront) / 2 )) \# divider or multiplier used to adjust correction  
dterm = int((diff – prevdiff) \* 2) \# dervative term and it’s multiplier  
leftspeed = basespeed + diff + dterm  
rightspeed = basespeed – diff – dterm  
\# check that speeds have not gone negative  
if(leftspeed \< 0):  
leftspeed = 0  
if(rightspeed \< 0):  
rightspeed = 0  
\# adjust motor speed  
LMOTOR\_PWM.duty\_u16(leftspeed) \# set L motor – range is 0 to 65535  
RMOTOR\_PWM.duty\_u16(rightspeed)  
prevdiff = diff \# save diff as previous for next time round the loop

Save the file as main.py on the Cytron Maker Nano RP2040 and then it should run as soon as the robot is switched on.

One of the advantages of using micro python is that the source code is saved on the processor board and can be retrieved by opening the file for further editing., whereas on the Arduino Nano only the compiled code is saved on the processor so the source has to be saved and maintained on the developer’s PC
