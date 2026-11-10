---
title: Arduino Nano Performance
date: '2020-08-20T12:19:32Z'
lastmod: '2020-08-20T12:20:20Z'
url: /2020/08/arduino-nano-performance-table/
categories:
- Arduino
wp_id: 1680
---

The basic Arduino Nano board has been around for a while now. Based on the same ATMega328P processor as several other mainstream Arduino boards, it has more than adequate performance for many tasks. Have a look at what else the range has to offer.

<!--more-->

## New Nano Alternatives {#New_Nano_Alternatives}

If your project has greater needs than can be met by the humble Nano, there are now alternatives in the same form factor. The Arduino Nano Every boasts a processor with more memory while the new Nano33 series add wireless communications. Wireless connectivity (BT, BLE and WiFi) demand faster processors with more memory. At the top of the range, the Nano33 BLE and Nano33 BLE Sense use a very capable nrf52840 processor that includes hardware arithmetic options.

Be aware that the Nano33 boards are not 5 Volt compatible and may require a change to existing circuits before they can be used as a replacement for the Nano and Nano Every.

Looking on the Arduino store seems to indicate that the ordinary Nano is being phased out although the clone manufacturers are likely to continue to make them for some time to come.

## Arduino Nano Performance Table {#Arduino_Nano_Performance_Table}

The following table shows the main differences between the boards in terms of resources and performance. You can clearly see that the nrf52840 gives a very significant boost to the available processing power for all operations but particularly where its hardware floating point unit is used. If Arduino Nano performance is important to you, then this table may help you decide.

|                 | nano 328p  | nano every | nano33 iot | nano33 ble |      |
| --------------- | ---------- | ---------- | ---------- | ---------- | ---- |
| Processor       | ATMega328P | ATMega4809 | ATSAMD21   | NRF52840   |      |
| Flash           | 32K        | 48K        | 256K       | 1024K      |      |
| RAM             | 2K         | 6K         | 32k        | 256K       |      |
| EEPROM          | 1024       | 256        | none       | none       |      |
| Voltage         | 5V         | 5V         | 3.3V       | 3.3V       |      |
| Clock           | 16MHz      | 16MHz      | 48MHz      | 64MHz      |      |
|                 |            |            |            |            |      |
| nop             | 0.09       | 0.08       | 0.03       | 0.02       | usec |
| micros()        | 3.22       | 6.68       | 1.67       | 7.72       | usec |
| millis()        | 1.31       | 1.50       | 0.22       | 9.92       | usec |
| fadd            | 9.25       | 9.70       | 2.65       | 0.11       | usec |
| fsub            | 8.62       | 9.08       | 2.92       | 0.12       | usec |
| fmul            | 8.30       | 8.25       | 3.05       | 0.12       | usec |
| fdiv /=         | 7.77       | 7.86       | 2.67       | 0.33       | usec |
| fdiv 2/x        | 31.16      | 30.98      | 10.19      | 0.31       | usec |
| dadd            | 9.18       | 9.50       | 4.09       | 1.56       | usec |
| dsub            | 8.56       | 8.87       | 4.64       | 1.59       | usec |
| dmul            | 6.08       | 6.28       | 4.32       | 0.83       | usec |
| ddiv            | 6.01       | 6.22       | 4.00       | 1.19       | usec |
| sin()           | 115.40     | 112.38     | 94.15      | 2.99       | usec |
| cos()           | 109.36     | 106.50     | 85.90      | 2.72       | usec |
| tan()           | 130.74     | 127.49     | 178.06     | 4.27       | usec |
| acos()          | 165.88     | 162.59     | 118.37     | 4.46       | usec |
| asin()          | 172.36     | 168.89     | 112.47     | 4.82       | usec |
| atan2()         | 191.40     | 187.60     | 158.92     | 7.57       | usec |
| sqrt()          | 31.90      | 31.55      | 10.48      | 1.01       | usec |
| iadd8           | 0.51       | 0.63       | 0.20       | 0.10       | usec |
| isub8           | 0.52       | 0.64       | 0.20       | 0.10       | usec |
| imul8           | 0.72       | 0.84       | 0.20       | 0.11       | usec |
| idiv8           | 5.93       | 5.66       | 0.60       | 0.11       | usec |
| iadd16          | 1.00       | 1.24       | 0.20       | 0.11       | usec |
| isub16          | 1.00       | 1.24       | 0.20       | 0.10       | usec |
| imul16          | 1.56       | 1.75       | 0.20       | 0.10       | usec |
| idiv16          | 13.64      | 13.46      | 1.09       | 0.11       | usec |
| iadd32          | 1.97       | 2.37       | 0.17       | 0.10       | usec |
| isub32          | 1.97       | 2.38       | 0.17       | 0.09       | usec |
| imul32          | 6.32       | 6.41       | 0.17       | 0.10       | usec |
| idiv32          | 37.77      | 38.16      | 0.52       | 0.10       | usec |
| iadd64          | 4.25       | 5.08       | 0.34       | 0.27       | usec |
| isub64          | 4.26       | 5.08       | 0.34       | 0.28       | usec |
| imul64          | 22.86      | 22.47      | 1.68       | 0.23       | usec |
| idiv64          | 33.74      | 34.25      | 6.36       | 1.76       | usec |
| memcpy128       | 57.66      | 49.11      | 27.35      | 12.94      | usec |
| memset128       | 5.50       | 2.29       | 0.44       | 0.46       | usec |
| delay\_ms(1)    | 1008.40    | 1010.92    | 1002.77    | 997.07     | usec |
| delay\_us(1000) | 1008.96    | 1008.76    | 1010.01    | 1007.57    | usec |

## References {#References}

  - [Arduino Nano Every](https://store.arduino.cc/arduino-nano-every)
  - [Arduino Nano 33 IOT](https://store.arduino.cc/arduino-nano-33-iot)
  - [Arduino Nano BLE](https://store.arduino.cc/arduino-nano-33-ble)
  - [Arduino Nano BLE Sense](https://store.arduino.cc/arduino-nano-33-ble-sense)
