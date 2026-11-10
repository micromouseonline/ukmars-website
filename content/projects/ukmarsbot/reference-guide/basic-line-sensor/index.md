---
title: Line Sensor Basic
date: '2020-07-17T12:00:08Z'
lastmod: '2020-07-25T11:54:23Z'
weight: 2
wp_id: 801
---

The basic line sensor circuit board for the robot implements a series of circuits that connect the various electronic parts together. These circuits and their functions are described below:

1.  This circuit uses the D12 trigger signal from the Nano to switch on a transistor. This then supplies current through the limiting resistors to the LEDs that illuminate the line that is being followed and the markers at each side of the line.  
    ![](/ukmars/wp-content/uploads/2020/07/line-emitters.jpg)  
    ![](images/line-emitters.jpg)
2.  This circuit shows the four phototransistors that are used to measure the light returning from the illuminated board that the robot is looking down at. Series resistors are used to limit the current flowing through the phototransistors which also affects the sensitivity of the detectors. Additional resistors can be placed in the circuit by using the Line Sensor Sensitivity Adjustment Connector. Analogue values from the detectors are fed back to analogue inputs A0,A1,A2 and A3 on the Arduino Nano.  
    ![](/ukmars/wp-content/uploads/2020/07/line-detectors.jpg)  
    ![](images/line-detectors.jpg)
3.  This circuit takes Nano digital outputs D6 and D11 and feeds them to 2 LEDs used as indicators. These could be used for instance to indicate whether particular detectors are seeing a line or not.  
    ![](/ukmars/wp-content/uploads/2020/07/line-indicators.jpg)  
    ![](images/line-indicators.jpg)
4.  This part of the circuit shows the connector that is used to pass the signals to and from the main board. It is designed so that it will line up with the connector on the main board.  
    ![](/ukmars/wp-content/uploads/2020/07/line-connector.jpg)  
    ![](images/line-connector.jpg)
