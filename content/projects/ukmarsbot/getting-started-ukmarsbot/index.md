---
title: Getting Started
date: '2020-07-25T11:57:44Z'
lastmod: '2026-09-04T20:37:39Z'
wp_id: 1485
---

Before you start building the UKMARSBOT you will need to get yourself organised\!

You have obviously found the UKMARSBOT build guide, so mark that page as a favourite in your browser as you will be referencing it quite a lot. Note that there are 2 build guides available from the menus at the side of the page. The first one is for the original and still current UKMARSBOT using either the Arduino Nano coded in C++ in the Arduino Sketch development environment, or a Waveshare ESP32 S3 Nano or the Cytron Maker Nano RP2040 boards, coded in micro-python in a Thonny development environment. The second, the GEMINI one is for the build based on the Raspberry Pi Pico and coded in Python.Below is a checklist of things to do:

1.  Spend some time looking at all the Building Guide Pages so you have a good idea of what will be involved, so that you can be confident that you will be able to do everything needed.
2.  Decide what language you want to code in: C++ or Python. If you want to use C++, build the original UKMARSBOT with an Arduino Nano board. If you want to code in Python you can either build the original UKMARSBOT with the Waveshare ESP32 S3 Nano or the Cytron Maker Nano board or else build the GEMINI with the Raspberry Pi Pico board. The GEMINI is a slightly bigger build as it has an extra PCB for mounting the processor board. For Python on the original UKMRSBOT the Waveshare ESP32 S3 Nano is the best match to the Arduino in form factor and pin usage but the Cytron Maker Nano RP2040 has a Pizzo sounder and two RGD lights which can be useful for debugging but less AtoD inputs for things like battery monitoring Details of the build for the ESP32 S3 Nano are now being added to this guide.
3.  Have a look at the Tools and Materials page and make a list of the tools and parts that you need to get.
4.  Where you have options, such as for motors, encoders and batteries, read the Choosing Motors, Choosing Batteries and Fitting Encoders pages to help you decide what specific items you want
5.  Identify suppliers and part numbers for the parts that you will order. Group them by supplier and get as many as you can from a few suppliers as this will reduce your postage costs. Don’t forget that you will only be able to get the main PCB and sensor PCBs from UKMARS unless you want to get these PCBs produced yourself. Remember that parts bought on EBay that are coming from abroad may take some weeks or longer to be delivered.
6.  You don’t have to get everything at once. It all depends where you want to start. With just an Arduino Nano and mini USB cable you can download the free Arduino IDE and start learning to program in Sketch. When you are ready to start to write your programs, read all of the Developer Notes pages to help you, especially the Arduino and Pin Assignments pages.
7.  If you want to code in Python instead of C using Sketch you can use the Waveshare ESP32 S3 Nano board or the Cytron Maker Nano RP2040 board instead of the Arduino Nano and download free development tools from thonny.org, or you can build the GEMINI version of the UKMARSBOT which uses the Raspberry Pi Pico processor. Note that a different set of PCBs is required for a GEMINI build to that for a standard UKMARSBOT and there are a separate set of build instructions available from the link in the menus on the right side of the pages.
8.  When you are ready, assemble the main board, or 2 boards if building the GEMINI version, then fit the motors and the battery as per the build instruction pages. You will now have a robot that you can program and make move.
9.  Once you can control your robot, build one or more of the sensor boards and fit them. Again please note that the GEMINI version uses different line and wall sensor boards to the standard version
10. Make a small test line following or wall following board to test your robot on and get it working
11. Work out how to control your robot better and improve your programs until you are happy with them.
