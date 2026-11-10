---
title: Raspberry Pi Controller for UKMARSBOT
date: '2021-01-07T00:00:43Z'
lastmod: '2021-01-07T00:00:45Z'
url: /2021/01/raspberry-pi-controller-for-ukmarsbot/
categories:
- Member's Robots
- UKMARSBOT
wp_id: 1876
---

The UKMARSBOT training robot, designed by members of UKMARS, was always intended to be flexible. It can be adapted to use a number of different processor modules in place of the standard Arduino Nano. one of the Society’s members, Rob Probin, has gone one stage further by adding a Raspberry Pi Zero **as well as** the standard controller.

The Pi Zero brings all the advantages of a high-level development interface with WiFi, processor power and high-level languages as well as the relatively huge amounts of storage compared to an Arduino Nano. The compact form factor of the Pi Zero makes it a relatively easy fit onto the robot with a simple adaptor mount. Communications are handled directly over the serial link to give the Pi Zero access to the sensors and motor of the base robot.

This approach will let users familiar with the Raspbery Pi environment expand their horizons into mobile robotics and hardware control. For users more familiar with the Arduino environment, the addition of a Pi Zero makes it realistic to experiment with artificial intelligence and even vision-based tasks with a Pi camera module.

At the January meeting of members, Rob described the project and its goals. There followed a good discussion around some of the practicalities of implementing this solution. Future posts on this site will examine some of the details in greater depth. Meanwhile, the project files are available on Github here: [Adding a Rapberry Pi Zero onto a UK Mars Bot (github.com)](https://github.com/robzed/pizero_for_ukmarsbot)

The meeting was recorded and is available on YouTube:

{{< youtube 3ZbhDZFe_Pg >}}
