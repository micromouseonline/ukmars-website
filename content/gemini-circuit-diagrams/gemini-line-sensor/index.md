---
title: Line Sensor PCB
date: '2025-08-08T21:32:32Z'
lastmod: '2025-08-19T17:56:28Z'
weight: 1
wp_id: 3527
---

These are the circuits on the line sensor PCB

This circuit drives 2 of the 3 LEDs, the one at the front over the middle of the line and also the one on the right side that lights the start and end markers on the right side of the line follower track

![](/ukmars/wp-content/uploads/2025/08/image-74-640x344.png)

This circuit drives the other LED which lights the change of radius markers on the left side of the line follower track

![](/ukmars/wp-content/uploads/2025/08/image-75-640x491.png)

These are the 4 phototransistor detectors that measure the light coming back from the illuminated line. Note that the signals from the Start/Finish detector and that from the Radius detector on the other side both go the same analogue input on the Pico. This is because the Pico only has 3 analogue to Digital inputs so we have to multiplex two of the inputs together. By deciding which of the LEDs to light at what time we can differentiate the detection of the Star/Finish marker from that of the Radius marker.

![](/ukmars/wp-content/uploads/2025/08/image-77-640x204.png)

This is the circuit for the 3 indicator LEDs that you can use as you wish, such as showing if a marker has been detected

![](/ukmars/wp-content/uploads/2025/08/image-78-640x310.png)

Finally, these are the connections from the mezzanine board to the line sensor board, and also the power decoupling and smoothing capacitors

![](/ukmars/wp-content/uploads/2025/08/image-79-640x298.png)
