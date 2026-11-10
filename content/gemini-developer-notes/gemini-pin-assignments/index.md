---
title: Python code snippets
date: '2025-08-08T21:38:05Z'
lastmod: '2025-11-06T22:01:44Z'
wp_id: 3541
---

This page has sections of code for doing things you might want in your programs. You may want to use them as procedures in your program. Make sure that they are put before any code that calls them.

## **Read the wall sensor values**  {#Read_the_wall_sensor_values}

This section of code will read the sensors on the wall sensor board. The global statements are defined so that you can access and display the lit and unlit values plus the resulting leftSensorValue, rightSensorValue, and frontSensorValue fields outside of the procedure. for use in your program or for diagnostic purposes

```
def readSensors(): # read wall sensors
    #Values are derived by subtracting the lit value of a sensor 
    # from the unlit value 
    global leftSensorValue, rightSensorValue, frontSensorValue
    global leftSensorLit, rightSensorLit, frontSensorLit
    global leftSensorUnlit, rightSensorUnlit, frontSensorUnlit
    global leftval, rightval, frontval

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

## **Read the line sensor values**  {#Read_the_line_sensor_values}

This section of code will read the sensors on the line follower board

```
def readSensors(): # Read line and side marker sensors
    global leftSensorValue, rightSensorValue
    global radiusSensorValue, startSensorValue
    global leftSensorUnlit, rightSensorUnlit 
    global radiusSensorUnlit, startSensorUnlit

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

## **Flash the LEDs**.  {#Flash_the_LEDs}

This section of code will repeatedly flash the LEDs on the mezzanine board and the three indicator LEDs on either sensor board. For the line sensor board it will also briefly flash the line and marker illumination LEDs

```
def flashLEDs():
    i = 0
    while True:
        print ("flash LEDs", i)
        i = i + 1
        leftMezzLED.value(1) # left Mezzanine LED
        rightMezzLED.value(1)
        onBoardLED.value(1) # mini LED on Pico processor board
        time.sleep(1)
        leftMezzLED.value(0)
        rightMezzLED.value(0) # right Mezzanine LED
        onBoardLED.value(0)
        time.sleep(1)
        leftSensorLED.value(1) # Left LED on either sensor board
        time.sleep(0.5)
        centreSensorLED.value(1) # Centre LED on either sensor board
        time.sleep(0.5)
        rightSensorLED.value(1) # Right LED on either sensor board
        time.sleep(1)
        leftSensorLED.value(0)
        centreSensorLED.value(0)
        rightSensorLED.value(0)
        emitter.value(1)      # Line sensor line illumination LEDs
        time.sleep(0.1)
        emitter.value(0)
        radiusEmitter.value(1) # Line sensor marker illumination LED
        time.sleep(0.1)
        radiusEmitter.value(0)    
```

## Run the motors {#Run_the_motors}

The Initial Set up and Tests page has a section called Testing the mezzanine board which has a good example of code for running the motors forwards and backwards. Note that to go forward you should set the forward PWM value to the maximum value and the reverse PWM value to the maximum value minus your desired speed, The maximum value for the PWM setting is 65535 and the minimum is zero. You should not put a negative value in the PWM value setting or include any formulae in the PWM value parameter.

## **Write to a file**.  {#Write_to_a_file}

One of the great things about the raspberry Pi Pico is that it has a file system that can be written to and read from within Python and also from the Thonny development environment.

This procedure writes 3 numeric global data values to a file called saveddata.tx They are converted to string values before being written out. You could use code like this to write out diagnostic or calibration data collected by the program. After the program run has finished you can connect the USB cable to your computer and then Open and view the file from Thonny.

```
def savetofile(): # saves 3 data fields to a file called saveddata.tx
    global saved1, saved2, saved3
    # write data fields out to file
    print (saved1, saved2, saved3)
    filedata = "saveddata.txt"
    fdata = open(filedata, "w") # open file
    number = str(saved1)
    fdata.write(number + ", ")
    number = str(saved2)
    fdata.write(number + ", ")
    number = str(saved3)
    fdata.write(number + ", ")
    fdata.close()
    return 
```

## Maze solving using the Flood Algorithm {#Maze_solving_using_the_Flood_Algorithm}

You can find some sample code for a flood algorithm at this page: [maze-solving-in-micro-python/](/gemini-developer-notes/maze-solving-in-micro-python/)
