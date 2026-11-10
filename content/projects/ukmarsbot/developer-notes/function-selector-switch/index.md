---
title: Function Selector Switch
date: '2020-07-25T10:49:41Z'
lastmod: '2020-07-25T10:49:43Z'
weight: 5
wp_id: 1420
---

- The robot has a four pole switch on it that can be used to select a program or function for the robot to perform. It also has a press button tactile switch that can be used in conjunction with the 4 pole switch as a user button.![](images/switchs2s4.jpg)

![](/ukmars/wp-content/uploads/2020/07/switchs2s4.jpg)

  - The 4 pole switch is connected to resistors R2 to R5 so that the 4 switches short out different resistors that are wired in a series. As each of the resistors that are shorted out have a different value, the effect is to make a different analogue voltage appear on the function select pin of the Nano for each different 4 switch combination.

![](/ukmars/wp-content/uploads/2020/07/circuit-function-selector-e1595026533513.jpg)

  - The user button is wired to connect the function select pin to 5 volts
  - By reading the function select pin as an analogue voltage we can distinguish 16 different analogue voltages for each combination of settings of the 4 pole switch, plus one extra value when the user button is pressed.
  - To write the program for this, you should make a test program to continuously read the analogue value of the function select pin and write it to the serial monitor. Then cycle the switches through each of the 16 combinations in sequence from 0000 to 1111, noting the value returned against each. Then write some code that tests for the mid-point values between the values noted earlier and returns a function value number in the corresponding range 0 to 15
  - If the value returned is close to the maximum value of 1023 then return a value showing that the user button has been pressed
