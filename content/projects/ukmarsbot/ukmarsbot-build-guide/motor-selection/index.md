---
title: Motor Selection
date: '2020-07-25T11:25:00Z'
lastmod: '2020-07-25T11:25:02Z'
weight: 5
wp_id: 1453
---

The robot is designed to use two N20 12mm micro gearmotors. These are widely available on Ebay and electronics and hobby robotics sites from £5 to £20 each.

These are the factors to consider when choosing which ones to buy:

1.  Do you want to fit encoders to the motors so that you can accurately measure speed and distance gone by the robot?  
    For basic line and wall following or the drag race this is not essential. However they will be needed if you want your robot to perform at the best level achievable and also if you aspire to doing maze solving.  
      
    To fit encoders directly to the motors you need to buy the ones which have an extended back shaft out of the opposite side of the motor to the gearbox. This will reduce your range of available ones but if you search on the internet for “micro metal gearmotor extended back shaft” you should find suitable ones either on EBay or from suppliers such as Pimoroni or Polulo.  
      
    ![](images/motorstandard.jpg)![](/ukmars/wp-content/uploads/2020/07/motorstandard.jpg)![](/ukmars/wp-content/uploads/2020/07/motorbackshaft.jpg)  
    ![](images/motorbackshaft.jpg)
2.  Choosing a suitable Gear Ratio.  
      
    These motors come in a very wide range of available gear ratios, from typically 5:1 to over 1000:1. A low gear ratio such as 10:1 will allow your robot to go faster, but it will be more difficult to control as you will have less torque available. The suggested gear ratio is 20:1 but anything between 10:1 and 60:1 is likely to be OK depending on the wheel size used. If you want to use encoders then Pimoroni have extended back shaft 6 volt ones at 11:1, 20:1 and 50:1 gear ratios, all of which would work well. Polulo have similar extended back shaft motors with gear ratios of 5:1, 10:1, 30:1 and 50:1.
3.  Motor Voltage  
      
    The robot is designed for use with motors rated at 6 volts. Using a battery that delivers between 7.5 and 9 volts means that there is plenty of voltage available for 6 volt motors, with a bit spare to allow for some occasional over voltage power being applied to the motors. Make sure that the motors you use are rated at 6 volts and not 12 volts as some will be.
4.  Motor Power rating  
      
    Gearmotors come in four power ratings, Low, Medium, High and High with carbon brushes. The power rating will affect the top speed of the motor (the speed of the robot) and the torque (how fast it can accelerate or control the speed). For comparison, for a 10:1 6 volt gearmotor from Polulo the top speed of the motor with no load on it and the torque available will be :  
      
    High Power——————— 3000 RPM 3.0 oz/in torque  
      
    High power (carbon brush) – 3000 RPM 2.4 oz/in torque  
      
    Medium Power —————– 2200 RPM 1.5 oz/in torque  
      
    Low Power ———————- 1300 RPM 1.4 oz/in torque  
      
    The High Power motor will require higher current and consume more battery power but is worth using if you want to get maximum performance.
