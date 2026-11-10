---
title: Gemini Developer Notes
date: '2025-08-08T21:36:33Z'
lastmod: '2026-09-04T16:26:35Z'
weight: 3
wp_id: 3537
cascade:
  type: docs
---

There are a number of things that you need to know about to write software in Micro-Python for the Pico on the Gemini UKMARSBOT.

The first two are imports and pin allocations: Gemini has most of the Pico pins assigned to specific functions. Look at the Initial Set up and Tests page for how to define firstly the import statements that you will need, then include the pin assignments. Note that you will always need the first set relating to the Mezzanine board, but then you will need EITHER the pin assignments for the wall sensor board OR the pin assignments for the line sensor board. DO NOT include both sets, only the ones relating to the specific sensor board that you have attached to the mezzanine board. You can copy these pin allocations directly from the web page into the start of your code

To make your robot move you will need to send pulse width modulated (PWM) speed values to the left and the right motors. The motor driver board needs specific signal from the Pico to do this. For each motor you need to insert two commands in your program, one for the forward PWM value and one for the reverse PWM value. Motor PWM values can be any integer value between 0 and 65535. To go forward on the left motor at a quarter of the full speed, set the forward value to the maximum value of 65535 and the reverse value to the maximum value minus the speed that you want to go at. So to go forward at speed 16384 we would insert these two commands in our program: leftFwd.duty\_u16(65535) and leftRev.duty\_u16(49151) We would then put in two similar commands for the right motor: rightFwd.duty\_u16(65535) and rightRev.duty\_u16(49151) Note that these names should match up with the names given in the pin assignments section. This may look strange, but it will drive the motors most effectively when done like this. If you are using a speed value that has had calculations done on, convert it to an integer value first using the int function e.g. like this: int(speedvalue)
