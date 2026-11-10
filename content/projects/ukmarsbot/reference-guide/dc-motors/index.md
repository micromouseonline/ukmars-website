---
title: DC Motors
date: '2020-07-17T11:59:29Z'
lastmod: '2020-07-25T11:54:09Z'
weight: 1
wp_id: 799
---

DC motors like those used on the UKMARSBOT are very common and apparently simple to drive. Apply a voltage to the terminals and the motor spins. Reverse the connections and the motor spins the other way. Higher voltages make the motor spin faster. What could be easier? Well, it will help to understand a little more about the motors and the way that computers can generate drive signals.

## Using DC Motors {#Using_DC_Motors}

DC (Direct Current) motors a get their name from the fact that they are driven from a DC power supply like a battery. Motors used in small robots and toys operate from quite low voltages. Typically up to 12 Volts or maybe 24 Volts. The motors used in UKMARSBOT are rated for continuous voltages of 6 Volts. They can be driven from higher voltages for short periods of time but to do so for very long will, at best, shorten the life of the motors and may cause it to fail completely very quickly.

The first thing to note about DC motors is that the speed at which they turn is proportional to the voltage applied to the terminals. If there is no friction or other losses, the motor will turn twice as fast with 6 Volts applied as it would with only 3 Volts applied. Real motors and real systems have losses and so it may be that the actual relationship is less linear. Also, it may be that the motor will not even begin to turn until some minimum voltage is applied – possibly even as much as 0.5 Volts or more.

Another key feature is that the motor cannot respond instantaneously to changes in applied voltage. This is partly because of the nature of the electrical windings in the motor but mostly because of the inertia of the motor and whatever it is attached to. You probably know all about inertia. It is the reluctance of something to start moving or to change speed once it is moving. On a bicycle for example it takes a good push to get you moving but then only relatively little effort to keep you moving. On the flat anyway. For an electric motor attached to a robot, once the voltage is applied to the motor, it will take some time for it to get up to speed – to accelerate. A large robot and a small voltage will mean it takes a lot longer than with a small robot and a large voltage. For best acceleration and highest final speed, robots need to be a light as possible. Even a very light robot with a large motor and big battery may take quite some time to get up to its top speed – perhaps a second or so. Not long for you but ages for a computer.

## Pulse Width Modulation {#Pulse_Width_Modulation}

Digital computers like the Arduino do not have any way to simply generate a known voltage on one of their pins. The outputs are binary – they are either on or off. When a pin is on, there will be 5 Volts available from the pin, when it is off there will be 0 Volts available. A motor that can only be fully on or fully off would not be very useful in most circumstances. If the power were applied all in one go, the wheels might slip or it may take so much power that some component in the robot breaks.

Suppose, however, the pin were turned on and off very fast – hundreds or thousands of times per second. The motor and robot cannot possibly change speed that quickly so what happens? If the pin was high exactly half the time (50%) and low exactly half the time, then as far as the motor is concerned, that is equivalent to having a drive voltage that is half of 5 Volts. The motor cannot tell the difference between a 2.5 Volt battery and a 5 Volt battery that is turned on half the time and off half the time. This is only true if the rate at which the drive is switched is very high compared to the rate at which the motor can respond.

This effect is true when the proportion of time that the pin is high is varied. So, with a 5 Volt supply, if the pin is on for one tenth (10%) of the time, the motor behaves as if it has a supply of 10% of 5 Volts which is 0.5 Volts. In the same way, of the pin is on for 80% of the time, the motor behaves like it has 80% of 5 Volts which is 4 Volts.

This whole business of varying the proportion of time that a pin is held high is called **Pulse Width Modulation (PWM)**.

## Duty Cycle {#Duty_Cycle}

A special term is used to describe the proportion of time that the pin is ‘on’. This is the Duty Cycle. A duty cycle of 0% means the pin is always off, 33% means the pin is on approximately one third of the time and 100% means that the pin is on all the time.

Duty Cycle can be given in many ways. It is most meaningful when given as a percentage as above. On the Arduino, the duty cycle is a number between 0 and 255 where 0 is 0% and the pin is always off and 255 is 100% and the pin is always on. A duty cycle of 127 would be 50%.

## `analogWrite()` {#analogWrite}

On the arduino there is a special instruction that can make a digital pin generate PWM pulses and set the duty cycle a particular value. That is the built in function `analogWrite(pin,duty)`.

**pin** is one of 3,5,6,9,10 and 11 on the Arduino nano. No other pins will work.  
**duty** is a value in the range 0…255.

The PWM signal generated on the pin will have a frequency of 490Hz by default. This is probably not high enough for the best control of small motors but it is worth trying. It is possible to change the frequency of the PWM signal but that will mean writing some custom code to implement a special version of analogWrite().
