---
title: Initial Set up and Tests
date: '2025-08-08T21:34:57Z'
lastmod: '2025-09-05T10:43:39Z'
wp_id: 3533
---

This page contains information and code for the initial software setup of the UKMARS Gemini robot. You can copy these pieces of code directly into your development environment such as the Thonny code editor.

**Import statements** :

At the start of your program put in the following 3 import statements which will give you access to various functions that you will need. UART is only needed if you are planning to use a Bluetooth communications module:

```
from machine import Pin, ADC, PWM, UART
import time
import os
```

**Pin assignments**

Next you should put in lines that define the uses of each of the pins on the Pico  
This set define the uses of the pins relating to the **Mezzanine board.** They set up the motor control through the PWM and direction settings, the 2 indicator LEDs, and the tactile button switches:

```
leftMezzLED = Pin(12,Pin.OUT) # The LED marked D1 on the left side of the board
rightMezzLED = Pin(13,Pin.OUT) # The LED marked D2 on the right side of the board
leftFwd = PWM(Pin(2))
leftFwd.freq(2000)
leftRev = PWM(Pin(3))
leftRev.freq(2000)
rightFwd = PWM(Pin(4))
rightFwd.freq(2000)
rightRev = PWM(Pin(5))
rightRev.freq(2000)
leftButton = Pin(15, Pin.IN, Pin.PULL_UP) # The tactile button switch marked SW1
rightButton = Pin(14, Pin.IN, Pin.PULL_UP) # The tactile button switch marked SW2
```

This set define the uses of the pins relating to the **wall sensor board**. Only put these in if you are connecting the wall sensor board to the front of the robot:

```

# These are the pin connection settings for use with the wall sensor board
# phototransistor sensor pins
leftSensor = ADC(28) # input from the left wall sensor
rightSensor = ADC(26) # input from the right wall sensor
frontSensor = ADC(27) # input from the front wall sensor
#Triggers for LEDs
sidesEmitter = Pin(22,Pin.OUT) # switches on the 2 side facing wall illumination LEDs
frontEmitter = Pin(21,Pin.OUT) # switches on the forward facing wall illumination LEDs
# These are the indicator LEDs on the wall sensor board
leftSensorLED = Pin(20,Pin.OUT) # indicator LED for when left wall seen
centreSensorLED = Pin(19,Pin.OUT) # indicator LED for when front wall seen
rightSensorLED = Pin(18,Pin.OUT) # indicator LED for when right wall seen
```

This set define the uses of the pins relating to the **line sensor board**. Only put these in if you are connecting the line sensor board to the front of the robot. Note that the two side sensor share the same ADC input pin. You can tell which is responding to a marker by switching on the appropriate LED before it is read.

```
# These are the pin connection settings for use with the line sensor board
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
```

You can now define any variables or global variables that you need for passing data around, then put in functions that you need to use to select which code to run, read the sensors, control the motors, or anything else that you need.

Follow this by the code which will be executed when your program runs. Save it all as main.py on the Pico and it will automatically run when you switch it on.

## **Testing the mezzanine board** {#Testing_the_mezzanine_board}

To check that the mezzanine board is working with the main chassis and motors, add this set of code to your import and mezzanine pin assignments statements shown above. When you run it the left LED should light and both motors run forward for 5 seconds. Then the other mezzanine LED will light up and the motors reverse for 5 second before they stop and the LEDs go out. If your motors do not go in the correct directions, swap round the 2 motor connections on J1 if the left motor is going the wrong way, or on J2 if the right motor is going the wrong way.

```
# Run motors forward and backwards and light the LEDs then stop motors
maxspeed = 65535 
botspeed = maxspeed - 15000 # desired speed of 15000
leftMezzLED.on() # Switch on the left mezzanine LED
leftFwd.duty_u16(maxspeed) # Set left forward speed to maxspeed
leftRev.duty_u16(botspeed) # and reverse speed to maxspeed - desired speed of 15000
rightFwd.duty_u16(maxspeed) # Set right forward speed to maxspeed
rightRev.duty_u16(botspeed) # and reverse speed to maxspeed - desired speed of 15000
time.sleep(5) # Wait for 5 seconds
leftMezzLED.off() # Switch off the left mezzanine LED
rightMezzLED.on() # Switch on the right mezzanine LED
leftRev.duty_u16(maxspeed) # Set left reverse speed to maxspeed
leftFwd.duty_u16(botspeed) # and forward speed to desired reverse speed of 15000
rightRev.duty_u16(maxspeed) # Set left reverse speed to maxspeed
rightFwd.duty_u16(botspeed) # and forward speed to desired reverse speed of 15000
time.sleep(5) # Wait for 5 seconds
leftMezzLED.off() # Switch off the left mezzanine LED
rightMezzLED.off() # Switch off the right mezzanine LED
leftFwd.duty_u16(maxspeed) # Set left forward speed to zero
leftRev.duty_u16(maxspeed) # and reverse speed to zero
rightFwd.duty_u16(maxspeed) # Set right forward speed to zero
rightRev.duty_u16(maxspeed) # and reverse speed to zero
```

If the motors are turning as expected and the mezzanine LEDs come on then the mezzanine and main chassis are working. You can now add either the line or wall sensor boards and after adding the appropriate set of pin settings from above you can test these. See the Python code snippets menu item for some sample code that you can use to test these.

## **Set up and testing the line sensor board** {#Set_up_and_testing_the_line_sensor_board}

To check that the line sensor board is working run this piece of code which will read the sensors and display the results on the connected computer. Start your program with the import statements, mezzanine pin assignments and the line sensor pin assignments as detailed in the sections above. Then follow it with this code which is a routine that will read all of the four line and marker sensors

```
def readSensors():
    #Values are derived by subtracting the lit value of a sensor from the unlit value 
    #Unlit raw readings close to 65000 indicate good separation from ambient light
    #The radius and start/finish sensors are multiplexed onto the same ADC channel using separate emitters
    #The UKMARS line follower sensor board gives high value readings for low incident light and low value readings for high incident light
    
    global leftSensorValue, rightSensorValue, radiusSensorValue, startSensorValue
    global leftSensorUnlit, rightSensorUnlit, radiusSensorUnlit, startSensorUnlit

    emitter.value(0)
    radiusEmitter.value(0)
    leftSensorUnlit = leftSensor.read_u16()
    rightSensorUnlit = rightSensor.read_u16()
    startSensorUnlit = startSensor.read_u16()
    radiusSensorUnlit = radiusSensor.read_u16()
    
    emitter.value(1)
    time.sleep_us(15)
    leftSensorLit = leftSensor.read_u16()
    rightSensorLit = rightSensor.read_u16()
    startSensorLit = startSensor.read_u16()
    emitter.value(0)
    
    radiusEmitter.value(1)
    time.sleep_us(15)
    radiusSensorLit = radiusSensor.read_u16()
    radiusEmitter.value(0)

    leftSensorValue = (leftSensorUnlit - leftSensorLit)
    rightSensorValue = (rightSensorUnlit - rightSensorLit)
    startSensorValue = (startSensorUnlit - startSensorLit)
    radiusSensorValue = (radiusSensorUnlit - radiusSensorLit)
```

Then follow it with this code that will repeatedly call the read routine and display the values of the 4 sensors

```
def printSensors():
    global leftSensorValue, rightSensorValue, radiusSensorValue, startSensorValue
    global leftSensorUnlit, rightSensorUnlit, radiusSensorUnlit, startSensorUnlit
    while True:
        readSensors()
        print("left L-line R-line right")
        print(radiusSensorValue,leftSensorValue,rightSensorValue,startSensorValue)
        time.sleep(0.5)
# run the program
printSensors() # call the print Sensors program
```

Run this program from Thonny with the USB cable connected to the robot to display the 4 sensor readings every half a second.

You should get one set of four values when on white paper which are significantly higher from those that you get when place on black paper. If this is happening for all sensors then your line sensor board is working correctly

We now need to align the central LED and sensors. Place the robot on a white piece of paper and run the printSensor program again with the USB cable connected. we need the two central line sensor readings to be within 10 percent of each other. Check that the LED id central and the 2 line sensor phototransistors are vertical. Using a small screwdriver move the central LED slightly sideways and see if this gets the 2 central readings closer to each other. If it has made it worse move the LED the other way. When you have similar readings on both central sensors the board is well aligned and ready to use.

You can use these highest and lowest readings on each sensor to detect whether you are seeing the line or the markers. In the sample line follower code page you can see the highlow() routine that captures these values after reading the sensors, and subsequent code that calculates trigger values for seeing if we are still on the line.

## **Set up and testing the wall sensor board** {#Set_up_and_testing_the_wall_sensor_board}

Reading the wall sensors is simpler as there are only 3 sensors, so there is no need to multiplex the sensor outputs. The sensors are read in the unlit and the lit mode and one value subtracted from the other. The two side LEDs are lit by one emitter signal and then read. Then the front LED is separately lit by the other emitter signal and the front sensor read. This procedure will read the values of the wall sensor:

```
def readSensors():
    #Values are derived by subtracting the unlit value of a sensor from the lit value  
    global leftSensorValue, rightSensorValue, frontSensorValue
    global leftSensorLit, rightSensorLit, frontSensorLit
    global leftSensorUnlit, rightSensorUnlit, frontSensorUnlit

    leftSensorUnlit = leftSensor.read_u16()
    rightSensorUnlit = rightSensor.read_u16()
    sidesEmitter.value(1)
    time.sleep_us(75)
    leftSensorLit = leftSensor.read_u16()
    rightSensorLit = rightSensor.read_u16()
    sidesEmitter.value(0)
    
    frontSensorUnlit = frontSensor.read_u16()    
    frontEmitter.value(1)
    time.sleep_us(75)
    frontSensorLit = frontSensor.read_u16()
    frontEmitter.value(0)
    time.sleep_us(75)

    leftSensorValue = (leftSensorLit - leftSensorUnlit) # 
    rightSensorValue = (rightSensorLit- rightSensorUnlit) # 
    frontSensorValue = (frontSensorLit- frontSensorUnlit)
```

Then follow it with this code that will repeatedly call the read routine and display the values of the 3 sensors

```
def printSensors():
    global leftSensorValue, rightSensorValue, frontSensorValue
    global leftSensorLit, rightSensorLit, frontSensorLit
    global leftSensorUnlit, rightSensorUnlit, frontSensorUnlit
    while True:
        readSensors()
        print("left front right")
        print(leftSensorValue,frontSensorValue, rightSensorValue)
        time.sleep(0.5)
# run the program
printSensors() # call the printSensors programe
```

With the USB cable connected to the computer run the program and see the values being displayed. As you move a test wall towards or away from each wall sensor you should see the values increase and decrease. If this is happening the wall sensor board is working correctly. You can use the initial values of the 2 side sensors when you put the robot in a maze cell to determine whether either side wall is present and to control the distance being kept away from it.
