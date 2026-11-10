---
title: Encoders on UKMARSBOT
date: '2020-07-25T10:43:25Z'
lastmod: '2020-07-25T10:43:27Z'
weight: 4
wp_id: 1418
---

## Interrupts {#Interrupts}

Among the many sources of interrupts on the ATMega328p, two are particularly interesting when you want to interface encoders. These are INT0 and INT1. Each has a dedicated pin on the processor and each has a separate interrupt service vector. This means that the interrupt service can respond quickly to the specific pin without having to waste time working out which pin caused the change.

Each of these pins can be programmed to generate an interrupt when there is a logical change on the pin. The encoders attached to the motors generate a series of pulses that change state 12 times for every rotation of the motor. By using the INT0 and INT1 interrupts, the processor can keep a count of those changes and so measure the speed of rotation and the distance travelled by the robot.

## Setting up the processor {#Setting_up_the_processor}

The ATMega328p used in the Arduino nano has INT0 and INT1 connected to two of the digital pins:

> PD2 for INT0 – Arduino Digital Pin 2  
>   
> PD3 for INT1 – Arduino Digital Pin 3

To tell the processor to generate interrupts when these pins change state, values must be written to particular bits in the External Interrupt Control Register A (`EICRA`) and the External Interrupt Mask egister (`EIMSK`).

### The EICRA {#The_EICRA}

For each of the pin change interrupts, the processor must be told what kind of change can generate an interrupt. The bits that control these settings are found in the External Interrupt Control Register A (`EICRA`).

The External Interrupt 0 is activated by the external pin INT0 if the corresponding interrupt mask is set and global interrupts are enabled. The level and edges on the external INT0 pin that activate the interrupt are defined as

| ISC01 | ISC00 | Description                                |
| ----- | ----- | ------------------------------------------ |
| 0     | 0     | Low Level of INT0 generates interrupt      |
| 0     | 1     | Logical change of INT0 generates interrupt |
| 1     | 0     | Falling Edge of INT0 generates interrupt   |
| 1     | 1     | Rising Edge of INT0 generates interrupt    |

The External Interrupt 1 is activated by the external pin INT1 if the corresponding interrupt mask is set and global interrupts are enabled. The level and edges on thexternal INT1 pin that activate the interrupt are defined as

| ISC11 | ISC10 | Description                                |
| ----- | ----- | ------------------------------------------ |
| 0     | 0     | Low Level of INT1 generates interrupt      |
| 0     | 1     | Logical change of INT1 generates interrupt |
| 1     | 0     | Falling Edge of INT1 generates interrupt   |
| 1     | 1     | Rising Edge of INT1 generates interrupt    |

To respond to changes from the motor encoders, the proper setting is for any logical change.

### The EIMSK {#The_EIMSK}

A single register in the processor holds bits that enable and disable the various sources of interrupts. To enable these pin change interrupts, two bits in this register must be set.

`EIMSK:INT0` (bit 0) enables the INT0 external interrupt  
`EIMSK:INT1` (bit 1) enables the INT1 external interrupt

## The configuration code {#The_configuration_code}

It may have seemed complicated to perform all this configuration but in reality it needs only a few of lines of code:

```
bitClear(EICRA, ISC01);                 // logical change on INT0
bitSet(EICRA, ISC00);
bitClear(EICRA, ISC10);                 // logical change on INT1
bitSet(EICRA, ISC11);
bitset(EIMSK,INT0);                     // enable INT0 interrupt
bitset(EIMSK,INT1);                     // enable INT1 interrupt
```

## Interrupt Service Routines {#Interrupt_Service_Routines}

Once the state of one of the pins changes, the processor will generate an interrupt and the flow of execution will jump to a predetermined location where it expects to find some code that can respond to the interrupt. This is written as a special type of function called an Interrupt Service Routine (ISR). Note that, if the ISR is not present, the processor behaviour is not defined and the program will fail.

To declare an ISR in the arduino environment, you need to use one of the predefined names. For the INT0 and INT1 interrupts, you will need these two ISRs:

```
ISR(INT0_vect) {
}

ISR(INT1_vect) {
}
```

If there is no code in the ISR, the processor will clear the interrupt state and immediately return to normal execution.

## Servicing the Encoders {#Servicing_the_Encoders}

Each of the robot’s encoders behaves the same way. Two pins are used on the processor. One has the combined pulse signal from the XOR gate and is connected to one of the interrupt pins, INT0 or INT1. The other signal is connected to another pin so that the ISR can examine it and work out whether the motor has turned and in what direction. Both ISRs have essentially the same code but operate on different pins. Here are the complete ISRs:

```
volatile int encoderLeftCount;
volatile int encoderRightCount;

ISR(INT0_vect) {
  static bool oldB = 0;;
  bool newB = bool(digitalReadFast(encoderLeftPinB));
  bool newA = bool(digitalReadFast(encoderLeftPinAxB)) ^ newB;
  if(newA == oldB){
    encoderLeftCount++;
  } else {
    encoderLeftCount--;
  }
  oldB = newB;
}

ISR(INT1_vect) {
  static bool oldB = 0;;
  bool newB = bool(digitalReadFast(encoderRightPinB));
  bool newA = bool(digitalReadFast(encoderRightPinAxB)) ^ newB;
  if(newA == oldB){
    encoderRightCount++;
  } else {
    encoderRightCount--;
  }
  oldB = newB;
}
```

The code may be a little hard to understand but it is written to execute as fast as possible. On a 16MHz Arduino, each function will takes about 2.3 microseconds to execute so it should be possible to respond to quite high pulse rates without getting the processor bogged down.

Note the use of `digitalReadFast()` to read the pin state. This is much quicker than the built-in digitalRead() function but the implementation is a bit broken and the result needs casting to a boolean. If the standard digitalRead() function is used instead, each interrupt will take 10us to execute. That is four times as long.
