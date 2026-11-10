---
title: Initial Set Up and Tests
date: '2020-07-25T10:35:45Z'
lastmod: '2025-08-20T16:21:55Z'
wp_id: 1407
---

Building a complex electronic project rarely goes smoothly, so here are a few initial test to do to check that various parts of the robot are working as they should be. The best way to check for any problems is to check each item or group of items work as you add them to the board. If you are building the robot in the sequence that is suggested in the Building Guides these tests should help you.

1.  Poor solder joints – After soldering in any component or connector look at the joint carefully with a jewellers loupe or any decent magnifying glass to see if the solder has flowed fully onto the component lead and the PCB pad. If it has not, reheat that joint and feed a bit more solder into it.
2.  Solder bridges – It is very easy to get a bridge between two adjacent pins, so check each joint to make sure that has not happened. If it has, remove the solder with either some solder wick or a solder sucker. Do not put any power onto the board or connect the USB cable if there are any solder bridged pins.
3.  Check that you can communicate with your Arduino Nano before you put it on the main board. Having downloaded the Arduino IDE and installed it and any drivers you need, connect your Nano to a USB port on your PC with the USB cable and see if you can download and run the blink example program. Sort this out before trying to do the same test with the Arduino Nano installed on the board. Then run the blink program using power from the battery with the USB cable disconnected to check that the battery connections, on/off switch and protection diode are all working correctly.
4.  Run a test program on the function switch to check that you can read and display the different vales obtained for each switch setting
5.  Run a simple motor test program to check that the motor driver board and motor connections are OK. This should move both motors forwards and backwards.
6.  If you get through to here You are looking good and can start doing some more serious programming, but if you get any problems with the above items have a look at the main troubleshooting page to help identify and fix the issues.
