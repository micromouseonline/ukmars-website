---
title: Powering The Pi Zero on UKMARSBOT
date: '2021-06-02T21:56:51Z'
lastmod: '2021-06-02T22:02:14Z'
url: /2021/06/powering-the-pi-zero-on-ukmarsbot/
categories:
- Monthly Meeting
wp_id: 2044
---

In this month’s presentation, Ian Butterworth describes how he managed to fit a Raspberry Pi Zero to the UKMARSBOT while ensuring that there is enough power for everything.

UKMARSBOT was designed to have a replaceable processor. What we didn’t think of was adding a Raspberry Pi Zero as a supervisory computer on top of the robot. This presents a particular challenge in getting adequate power to the Pi.

Although the Pi has an idling current draw that is probably (just) within the abilities of the Arduino Nano on-board regulator, Ian found that the Pi has much greater needs at time. This is particularly true at start-up when the total current requirement is much more than the existing regulator can handle. Consequently, the voltage sags and the system restarts and the cycle begins again.

To get the whole thing working, Ian found that some minor modifications are needed on the UKMARSBOT board and a supplementary power supply has to be constructed using a common DC-DC converter module from Murata.

{{< youtube 4q9WIEYzxag >}}
