---
title: Arduino IDE with a Raspberry Pi Pico (or RP2040 based boards)
date: '2023-05-01T14:10:41Z'
lastmod: '2023-05-01T21:42:42Z'
url: /2023/05/arduino-ide-with-a-raspberry-pi-pico-or-rp2040-based-boards/
categories:
- Arduino
- How To
- UKMARSBOT
tags:
- Arduino
- Raspberry Pi Pico
- RP2040
wp_id: 2687
---

These are instructions for setting the Arduino IDE with a Pico / RP2040

*NOTE: I already had the support board installed before writing this post, so some of this might be missing some steps. If anyone spots a problem, then let please me know.*

We’d like people to be able use the C/C++ code from [ukmarsbot-mazerunner](https://github.com/ukmars/ukmarsbot-mazerunner) easily via the Arduino IDE if they are using something like the [Cytron Maker Nano RP2040](https://www.cytron.io/p-maker-nano-rp2040-simplifying-projects-with-raspberry-pi-rp2040) or the [Arduino Nano RP2040 Connect](https://docs.arduino.cc/hardware/nano-rp2040-connect). (IMPORTANT NOTE: Both require modifications before fitting on a standards [UKMARSBot](https://github.com/ukmars/ukmarsbot) – that’s covered elsewhere). It’s technical possible to use the standard Pico/RP2040 tools – but you require more changes. Hence this guide.

1.  Download Arduino IDE from <https://www.arduino.cc/en/software> (I have Arduino 2.1.0).
2.  Install the Raspberry Pi Pico Library under the Menu: Boards -\> **Board Manager** -\> Raspberry Pi RP2040 Boards(2.6.3). There is also a “Arduino Mbed OS RP2040” … that works as well, but doesn’t have the DEBUG option (see below).
3.  Connect you Pico, holding down **BOOTSEL** as you do so.
4.  Select **UF2 Board** under the Menu: Tools -\> Port
5.  Select the **Blink** example from the Menu: File -\> Examples -\> 01.Basics -\> Blink
6.  Click **Verify** on the sketch (the tick icon) – this is probably optionals, since I guess upload does a compile (‘verify’) first.
7.  Click **Upload** on the sketch (the right-arrow icon).

Your Pico on board LED will be flashing. VERY slowing. If you think it’s too slow, edit the code to say:

```cpp
void setup() {
  // initialize digital pin LED_BUILTIN as an output.
  pinMode(LED_BUILTIN, OUTPUT);
}

// the loop function runs over and over again forever
void loop() {
  digitalWrite(LED_BUILTIN, HIGH); // turn the LED on (HIGH is the voltage level)
  delay(300); // wait for a second
  digitalWrite(LED_BUILTIN, LOW); // turn the LED off by making the voltage LOW
  delay(300); // wait for a second
}
```

I’ve only altered the delay here.

If you wish to reprogram the board, you’ll need (a) re-power/reset the board with BOOTSEL held down, and (b) Select the UF2 Board again, (c) Select upload.

## DEBUGGING

There is a debug option on the Arduino IDE 2 – but I haven’t really played with this yet. I know using the standard Raspberry Pi C / C++ tools you can debug, but I haven’t checked if the Arduino IDE does this. I’ll create a follow up post with more details.
