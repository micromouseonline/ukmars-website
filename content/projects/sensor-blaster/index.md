---
title: Sensor Blaster
date: '2020-07-17T12:06:37Z'
lastmod: '2025-11-17T19:45:42Z'
weight: 5
wp_id: 818
---

Building a reliable sensor to detect when a robot passes through a start or finish gate can be harder than you might imagine. The sensor must:

  - reliably detect the passage of a robot every single time
  - not be affected by the orientation of the robot
  - not be affected by the reflectivity of the robot
  - not be adversely affected by ambient light
  - not be falsely triggered by the robots own sensors

The Sensor Blaster is mostly meant to test the last point. It has one job and it does it well.

{{< figure src="/ukmars/wp-content/uploads/2020/07/sensor-blaster-top.png" alt="" caption="Sensor Blaster" >}}

Many small robot sensors emit short pulses of light at regular intervals. The pulses are often very bright and are likely be either of Infra Red (IR) or red light. The frequency of the pulses will probably be dependent on the processing loop in the robot. A common frequency is 1kHz but, because robot builders are simple souls at heart, the frequency may be some multiple of 100Hz. Each pulse is likely to be short – a few tens of microsecond.

This device is designed to behave like the mother of all robot sensor emitters. It emits very bright pulses of light using red, blue and IR emitters simultaneously. The pulses are sent at 1kHz and each is 100us long.

#### Eye Safety

The IR emitter is very powerful and may cause eye damage if you look into the beam. Always take care with this kind of emitter.

The circuit is constructed on a small piece or perfboard just the right size to attach to a battery holder taken from an old set of Christmas lights. The holder has a built in switch and takes two AA cells. No voltage regulation is needed and a pair of fresh AA cells will probably run it for 40-50 hours. This might be a good use for those not-quite-dead cells left over from Christmas or whenever you last used a set of lights.

{{< figure src="/ukmars/wp-content/uploads/2020/07/sensor-blaster-bottom.png" alt="" caption="Battery Holder for Sensor Blaster" >}}

To use the Sensor Blaster, simply turn it on and place it on the ground where it will interfere suitably with timing sensors. Clearly, it should not obscure the detector itself. The light emitted from the device is a reasonable facsimile of what a contest micromouse might emit so orient the device so that it emulates the output from a real robot.
