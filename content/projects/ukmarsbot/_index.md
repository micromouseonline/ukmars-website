---
title: UKMARSBOT
date: '2020-07-17T08:16:32Z'
lastmod: '2026-09-04T20:39:35Z'
weight: 1
wp_id: 705
---

**A simple beginner’s multi purpose robot platform** **with 2 variants**

{{< figure src="/ukmars/wp-content/uploads/2024/04/image-5-640x517.png" alt="" caption="Standard UKMARSBOT with wall sensor board" >}}

Using inexpensive, readily available materials, components and techniques, UKMARS has created 2 basic robot designs that can be used in a variety of common contests such as line following, wall following, maze solving and drag race. The first (the Standard model) is designed to use the Arduino Nano whilst the second (the Gemini model) uses the Raspberry Pi Pico

For the Standard model, processor power is normally provided by the Arduino Nano board because it is very cheap and widely available. There is a huge range of sample code available for almost any purpose and support is easily found online. The Arduino software can be installed on any computer and is free. However, for anyone who wants to code in Python, the Waveshare ESP32 S3 Nano board or the Cytron Maker Nano RP2040 board will fit in the same socket and needs only a minor change to the build to run it. Free software for MicroPython is available from thonny.org

The Gemini model uses the Raspberry Pi Pico processor, and has an extra layer of PCB which means that alternative processors could also be used with a minor design of the top layer board

### Coding {#Coding}

For starting coding with the Arduino Nano, most people use is to create a program using the Arduino Integrated Development Environment (IDE). Arduino programs comprise functions written with C/C++ statements and the Arduino IDE takes care of turning them into a complete program and uploading it to the Arduino board. It can run on any of the major platforms: Windows, Mac and Linux enabling Arduino code to be readily developed on any PC. The Arduino project has lots of examples and help available for creating code, as well as libraries of functions to carry out specific tasks.

The Arduino IDE requires software to be downloaded and installed on the development PC as well as drivers to enable the developed code to be downloaded using the USB cable onto the Arduino board. All of this software and drivers are free and easy to install as long as you have software install permissions on the PC.  
There is also a recently introduced web based development environment, but as yet this does not support all Arduino models and platforms. and still requires various plug ins to be installed on the development PC to use it.

For the great majority of users, writing code using the Arduino IDE is the best choice. Alternative software environments are available and are identified at the end of this document.

For coding on the Gemini model the preferred language is Micro Python which can be used in the free Thonny development environment. The Pico will support other languages if required.

### Hardware {#Hardware}

The robot hardware is constrained by the various contest events to be within certain dimensional limits. That means that the basic chassis will be smaller than 100mm x 100mm although add-on sensors for individual events will increase the size. The robot is designed to be multipurpose so there is a core hardware setup that provides for a basic wheelchair drive of two motors, encoder feedback for individual motor speed and a minimal interface for user interaction. Components are modular so that substitutions are easy and to provide the greatest flexibility. Two plug in sensor boards are available, one for wall following and maze solving, and one for half-size line following. Note that the sensor boards are different for the Standard Arduino version and the the Gemini Pico version. Builders are free to make whatever modifications suit their purpose or add different sensor boards. For example, larger or smaller motors may be used or tracked drive may be substituted for wheeled drive.

### Power Supply {#Power_Supply}

For most purposes, the power supply for the robot will need to be compact, readily available and easy to recharge. Non rechargeable batteries are not economically viable for robot experiment and are, in any case, less environmentally friendly. Safety is a concern and so Lithium Polymer cells are only recommended when part of a regulated and protected pack. Perhaps the most common small battery is the rechargeable PP3 sized pack running at 8.4 Volts or 9 Volts. Rechargeable cells and their chargers can be purchased at supermarkets and online suppliers. More confident, or adventurous builders may install whatever power supply suits them.

### Motors {#Motors}

While there is endless variety in small DC electric motors, the N20-based gearmotors are excellent value for money and can be purchased in a huge range of performance characteristics. An example can be found here: [Pimoroni 20:1 gearmotor](https://shop.pimoroni.com/products/micro-metal-gearmotor-extended-back-shaft?variant=32587847050). The common dimensions make it easy to swap motors without changing the mechanical design of the robot. Versions are available with built-in encoders allowing for more accurate control of speed and greater precision in movement of the robot. Normally these would be used in any robot. The drivers for these motors are available on small circuit board modules that can easily be connected with the Arduino Nano.

### Materials {#Materials}

It will be possible to build the robot using parts that are commercially readily available and specialist materials will not be required, access to basic hand tools and soldering equipment will be necessary.

It is likely that some builders will have some access to a 3D printer or a laser cutter or both and the open design of the robot with upgrade paths will allow advanced builders to utilize these tools to create higher performing robots.

### Software {#Software}

Pre-written software examples for the Arduino IDE will be available together with any special libraries that might be necessary. The intention is to provide all the basic building blocks that will allow someone to construct a working robot that can be modified to run in a particular contest. There may be complete, working contest code examples but they will be intended to illustrate how things work and are very unlikely to be a direct short-cut to making a contest-winning robot. Instead, they will be designed as a starting point for higher performance entries.

If the Arduino IDE is not for you, then there are other programming choices to suit you. (Note that not all of these have been tried by UKMARS)

  - MicroPython -Thonny is an easy to use Micro-Python implementation for Windows, Mac and Linux available to download at https://thonny.org/ It will run on the Raspberry Pi Pico and Cytron Maker Nano RP2040 boards
  - FlashForth http://flashforth.com/ is a Forth stamp system implemented on the Microchip 8-bit PIC18F and 16-bit PIC24, 30, 33 and the Atmel Atmega microcontroller families. See also https://playground.arduino.cc/CommonTopics/ForthOnArduino/ for other options relating to Forth.
  - For Basic users there appear to be fewer options. One of these is Great Cow basic http://gcbasic.sourceforge.net/Typesetter/index.php/Home. *“The Great Cow BASIC suite is robust and fully functional compiler and assembler. Using Great Cow BASIC is the fastest method to program a Microchip PIC or Atmel AVR 8-bit microcontroller for those just starting and the professional user.”* The host software is cross platform and there is a graphical editor as well as a more traditional IDE.
  - Some users may prefer a visual programming environment similar to Scratch. Several of these are available and more information may be found here [Sparkfun Alternative Arduino Interfaces](https://learn.sparkfun.com/tutorials/alternative-arduino-interfaces/all).
