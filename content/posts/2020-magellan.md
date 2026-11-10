---
title: Magellan
date: '2020-12-04T23:49:58Z'
lastmod: '2020-12-04T23:52:24Z'
url: /2020/12/magellan/
categories:
- Member's Robots
- Projects
wp_id: 1862
---

![](/ukmars/wp-content/uploads/2020/12/image-1.png)

Magellan, built by Ian Butterworth, is an example of UKMARSBOT a beginner’s robot with the standard basic line sensor board extended to improve reliability when detecting radius and start/finish markers. UKMARSBOT is covered in detail here  

[https://ukmars.org/projects/ukmarsbot/getting-started-ukmarsbot/](/projects/ukmarsbot/getting-started-ukmarsbot/)

and the modification of the sensors was discussed at Minos 2020, a recording of this presentation can be seen here 

{{< youtube mIUJ-PYy37A >}}

Motors are Pololu HP N20s with magnetic encoders and in line follower configuration a 10:1 gearbox. The maze variant uses 30:1 gearboxes.

Sensors are red visual light and power supplied by a USB rechargeable battery with a PP3 form factor. The build has been extended to include an HC05 Bluetooth module mounted vertically from the serial connections on the motherboard through a small horizontal prototype board that swaps the pins around and performs level shifting to 3.3V from the Arduino 5V transmit line. This connection is used to collect logging data and to allow the robot to be started remotely.

Future development will see Magellan able to compete in Wall-following, Drag Race, Time Trials and maze solving events.

Meanwhile, see Magellan complete the 2020 Virtual Line Follower course:

{{< youtube OYdQMNrzta4 >}}
