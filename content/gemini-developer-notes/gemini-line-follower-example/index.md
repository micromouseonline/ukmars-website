---
title: Line Follower Example
date: '2025-08-08T21:37:30Z'
lastmod: '2025-09-01T18:48:53Z'
weight: 1
wp_id: 3539
---

This is a very simple line follower. It does not read or process the side markers or stop at the end but should get round a line follower track

```
# simple line follower for the Gemini version of UKMARSbot

from machine import Pin, ADC, PWM, UART
import time
import os
# These are the pin connection settings for the main board and mezzanine
leftMezzLED = Pin(12,Pin.OUT) # The LED marked D1 on the left side
rightMezzLED = Pin(13,Pin.OUT) # The LED marked D2 on the right side 
onBoardLED = Pin("LED", Pin.OUT) # The LED on the Pico processor board
leftFwd = PWM(Pin(2))
leftFwd.freq(2000)
leftRev = PWM(Pin(3))
leftRev.freq(2000)
rightFwd = PWM(Pin(4))
rightFwd.freq(2000)
rightRev = PWM(Pin(5))
rightRev.freq(2000)
leftButton = Pin(15, Pin.IN, Pin.PULL_UP) # The tactile switch SW1
rightButton = Pin(14, Pin.IN, Pin.PULL_UP) # The tactile switch SW2

# These are the pin connection settings for the line sensor board
# phototransistor sensor pins
leftSensor = ADC(28) # left front line sensor 
rightSensor = ADC(26) # right front line sensor
radiusSensor = ADC(27) # left side radius change marker sensor
startSensor = ADC(27) # right side start/stop marker sensor
#Triggers for LEDs
emitter = Pin(22,Pin.OUT) # trigger for front and right side start/stop LED
radiusEmitter = Pin(18,Pin.OUT) # trigger for left side radius change LED
# These are the indicator LEDs on the line sensor board
leftSensorLED = Pin(21,Pin.OUT) # left indicator LED
centreSensorLED = Pin(20,Pin.OUT) # centre indicator LED
rightSensorLED = Pin(19,Pin.OUT) # right indicator LED

# Variables
maxspeed = 65535

def readSensors():  # only reads line sensors. LEDs stay on
    global leftSensorValue, rightSensorValue
    emitter.value(1)
    leftSensorValue = leftSensor.read_u16()
    rightSensorValue = rightSensor.read_u16()

def linefollow():
    global leftSensorValue, rightSensorValue
    global leftFrontLow, leftFrontHigh,rightFrontLow, rightFrontHigh, maxspeed
    leftFrontLow = rightFrontLow = 35000
    leftFrontHigh = rightFrontHigh = 35000
    pfactor = 0.4
    dfactor = 20
    preverr = 0
    difference = 0
    basespeed = 11500 
    leftspeed = maxspeed - basespeed
    rightspeed = maxspeed - basespeed
    leftFwd.duty_u16(maxspeed)  # Set left forward speed to max
    leftRev.duty_u16(leftspeed)      # and reverse speed to max - desired speed
    rightFwd.duty_u16(maxspeed) # Set right forward speed to max
    rightRev.duty_u16(rightspeed)     # and reverse speed to max - desired speed
    while(True):
        readSensors() #read the sensors
        highlow() # capture lowest and highest sensor values
        side =  0
        leftSensorTrigger = leftFrontHigh - ((leftFrontLow + leftFrontHigh) / 4)
        if leftSensorValue > leftSensorTrigger : # going off the line to left
            side = 1
            leftspeed = int(basespeed * 1.2)
            rightspeed = int(basespeed / 2)
        rightSensorTrigger = rightFrontHigh - ((rightFrontLow + rightFrontHigh) / 4)
        if rightSensorValue > rightSensorTrigger : # going off the line to right
            side = 2
            leftspeed = int(basespeed /2)
            rightspeed = int(basespeed * 1.2)        
        if side == 0:    
            difference = leftSensorValue - rightSensorValue # get diff between sensors
            dterm = int((difference - preverr) * dfactor)
            error = int(difference * pfactor) # proportional factor
            leftspeed = basespeed + error + dterm
            rightspeed = basespeed - error - dterm
        # check that speed values have not gone out of range
        if (leftspeed > 65500):
            leftspeed = 65500
        if (leftspeed < 1000):
            leftspeed = 1000
        if (rightspeed > 65500):
            rightspeed = 65500
        if (rightspeed < 1000):
            rightspeed = 1000
        #print( leftSensorValue,  rightSensorValue, difference, leftspeed, rightspeed)
        #time.sleep(0.5)
        # light mezzanine LEDs to say which side of line we are on
        if (difference > 0):
            leftMezzLED.on()
            rightMezzLED.off()
        else:
            leftMezzLED.off()
            rightMezzLED.on()
        leftFwd.duty_u16(maxspeed)  # Set left forward speed to max
        leftspeed = maxspeed - leftspeed
        leftRev.duty_u16(leftspeed) # Set left forward speed to max - required speed
        rightFwd.duty_u16(maxspeed) # Set right forward speed to max
        rightspeed = maxspeed - rightspeed
        rightRev.duty_u16(rightspeed) # Set left forward speed to max - required speed
        preverr = difference

def highlow():
    global leftSensorValue, rightSensorValue, radiusSensorValue, startSensorValue
    global leftFrontLow, leftFrontHigh,rightFrontLow, rightFrontHigh
    if leftSensorValue > leftFrontHigh:
        leftFrontHigh = leftSensorValue
    if leftSensorValue < leftFrontLow:
        leftFrontLow = leftSensorValue
    if rightSensorValue > rightFrontHigh:
        rightFrontHigh = rightSensorValue
    if rightSensorValue < rightFrontLow:
        rightFrontLow = rightSensorValue

linefollow()
```

It will just read the line sensors on the line follower board and use the difference between their value to adjust the motor speeds. If it detects that tit is going off the line it slows one motor down to half speed. The LEDs are left on all the time instead of being pulsed.
