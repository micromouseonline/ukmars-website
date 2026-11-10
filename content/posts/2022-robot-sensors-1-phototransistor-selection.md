---
title: 'Robot Sensors: 1 Phototransistor Selection'
date: '2022-07-15T16:00:41Z'
lastmod: '2022-07-15T16:00:43Z'
url: /2022/07/robot-sensors-1-phototransistor-selection/
categories:
- Technotes
- UKMARSBOT
wp_id: 2526
---

If you are new to the robot game (and even if you are not) it can be a challenge to select suitable sensors for your creation. This series will look at some possile devices. It is not necessarily a recommendation because I have not tried them all in all circumstances. Instead, it is a list of items to consider.

The first part looks at some phototransistors from a parametric search on Farnell for leaded devices of 3 or 5mm. I only chose Farnell because they have good parametric search facilities. Many, or most, of these parts should be available from other suppliers, possibly at a better price. Similarly, other suppliers may have devices that are just as good or better but which are not shown below. I am only interested in phototransistors here. Later parts will look at emitters and photodiodes and then I will finish up with a note about usage and placement.

There are al ot of possible devices so I arbitrarily slimmed down the list to devices are UK sourced by Farnell and suitable for new designs. that is, not discontinued. The devices must be available in available in small quantities. The parametric search gave me 42 devices. Some have been eliminated for a variety of reasons:

  - anything that is only available on back order
  - anything from Kingbright because their datasheets are useless
  - devices with poor on-axis response
  - slow, photo-darlingtons
  - side-lookers
  - anything with key information missing from datasheet e.g. response vs wavelength

That got me down to about 20 parts listed approximately in order of increasing price.

  - [1540032NA3090](https://uk.farnell.com/wurth-elektronik/1540032na3090/phototransistor-850nm-t-1/dp/3408623?st=phototransistor). 3mm, 37p
      - [datasheet](https://www.farnell.com/datasheets/3115728.pdf)
      - Wurth, 3mm clear package
      - 37p ea
      - 15mA/mW/cm²
      - wide spectrum. peak at 850nm, 60% at 650nm
      - risetime not given
      - ±15° moderately peaky polar pattern
      - The peaky pattern might make alignment more tricky

<!-- end list -->

  - [1540052NA3090](https://uk.farnell.com/wurth-elektronik/1540052na3090/phototransistor-850nm-t-1-3-4/dp/3408624?st=phototransistor) 5mm otherwise same as above.
      - [datasheet](https://www.farnell.com/datasheets/3115729.pdf)
      - Wurth, 5mm clear package
      - 39p ea
      - 15mA/mW/cm²
      - wide spectrum. peak at 850nm, 60% at 650nm
      - risetime not given
      - ±15° moderately peaky polar pattern
      - A 5mm version of 1540032NA3090. The peaky pattern might make alignment more tricky

<!-- end list -->

  - [1540031NC6090](https://uk.farnell.com/wurth-elektronik/1540031nc6090/phototransistor-940nm-t-1/dp/3408625)
      - [datasheet](https://www.farnell.com/cad/3115730.pdf)
      - Wurth, 3mm package black
      - 40p ea
      - 7mA/mW/cm²
      - IR only Peak at 940nm, no response at 650nm
      - risetime not given
      - ±30° quite wide acceptance but still a bit peaky
      - might make a good line follower sensor, maze-based not so much

<!-- end list -->

  - [1540051NC2590](https://uk.farnell.com/wurth-elektronik/1540051nc2590/phototransistor-940nm-t-1-3-4/dp/3408626)
      - [datasheet](https://www.farnell.com/cad/3115731.pdf)
      - Wurth, 5mm package black
      - 40p ea
      - 10mA/mW/cm²
      - IR only peak at 940nm. no response at 650nm
      - risetime not given
      - ±12.5° pretty pointy response
      - note the peaky polar pattern and no given speed.

<!-- end list -->

  - [SFH 309](https://uk.farnell.com/osram-opto-semiconductors/sfh-309/photo-trans-npn-860nm-radial-leaded/dp/2981729)
      - [datasheet](https://www.farnell.com/datasheets/2711611.pdf)
      - Osram. 3mm clear package
      - 47p ea
      - 1-10mA/mW/cm² Look for single bin parts SFH309-5 for 3-6mA/mW/cm²
      - wide spectrum peak at 880nm, 60% at 650nm
      - 7µs into 1000 Ohm
      - ±12° quite narrow so alignment more fussy
      - Take care over possible wide sensitivity range if bin number not given

<!-- end list -->

  - [SFH 309FA](https://uk.farnell.com/osram-opto-semiconductors/sfh-309-fa/photo-trans-npn-900nm-radial-leaded/dp/2981730)
      - [datasheet](https://www.farnell.com/datasheets/2869823.pdf)
      - Osram, 3mm black package
      - 57p ea
      - 1-10mA/mW/cm² Look for single bin parts SFH309-5 for 3-6mA/mW/cm²
      - heavily filtered IR only. No response at 650nm
      - 7µs into 1000 Ohm
      - ±12° quite narrow so alignment more fussy
      - Filtered version of SFH309

<!-- end list -->

  - [SFH 310](https://uk.farnell.com/osram-opto-semiconductors/sfh-310/photo-trans-npn-880nm-radial-leaded/dp/2981731)
      - [datasheet](https://www.farnell.com/datasheets/2711613.pdf)
      - Osram, 3mm package clear
      - 48p ea
      - 1-4mA/mW/cm²
      - broad spectrum. peak at 880nm, 60% at 650nm
      - 8µs into 1000 ohm
      - ±25° good polar pattern with flattened peak
      - Useful all-rounder but 2:1 variability in sensitivity for one bin

<!-- end list -->

  - [SFH 310 FA](https://uk.farnell.com/osram-opto-semiconductors/sfh-310-fa/photo-trans-npn-890nm-radial-leaded/dp/2981732)
      - [datasheet](https://www.farnell.com/datasheets/2711614.pdf)
      - Osram, 3mm package black
      - 48p ea
      - 1-4mA/mW/cm²
      - Heavily filtered to exclude visible light. No response at 650nm.
      - 8µs into 1000 ohm
      - ±25° good polar pattern with flattened peak
      - filtered version of SFH300

<!-- end list -->

  - [SFH 300](https://uk.farnell.com/osram-opto-semiconductors/sfh-300/photo-trans-npn-880nm-radial-leaded/dp/2981724)
      - [datasheet](https://www.farnell.com/datasheets/2711608.pdf)
      - Osram, 5mm package clear
      - 74p ea
      - 2-6mA/mW/cm²
      - broad spectrum. peak at 880nm, 60% at 650nm
      - 10µs into 1000 ohm
      - ±25° good polar pattern with flattened peak
      - Useful all-rounder but 2:1 variability in sensitivity for one bin

<!-- end list -->

  - [SFH 300 FA](https://uk.farnell.com/osram-opto-semiconductors/sfh-310-fa/photo-trans-npn-890nm-radial-leaded/dp/2981732)
      - [datasheet](https://www.farnell.com/datasheets/2711609.pdf)
      - Osram, 5mm package black
      - 57p ea
      - 2-6mA/mW/cm²
      - heavily filtered to exclude visible light. no response at 650nm
      - 10µs into 1000 ohm
      - ±25° good polar pattern with flattened peak
      - A visible-light filtered version of SFH300

<!-- end list -->

  - [SFH 314 FA](https://uk.farnell.com/osram-opto-semiconductors/sfh-314-fa/photo-trans-npn-870nm-radial-leaded/dp/2981735)
      - [datasheet](https://www.farnell.com/datasheets/2711616.pdf)
      - OSRAM, 5mm package
      - 50p ea
      - 2-10mA/mW/cm². Parts from one bit have 2:1 variation
      - Filtered. IR only 850-950nm. No response to red light
      - 11us into 1000 Ohm
      - ±40° broad, slightly cardiod pattern
      - might be good for line follower but IR only

<!-- end list -->

  - [OP599A](https://uk.farnell.com/tt-electronics-optek-technology/op599a/phototransistor-t-1-3-4/dp/1497889)
      - [datasheet](https://www.farnell.com/datasheets/2331915.pdf)
      - Optek, 5mm, Dark blue package
      - 63p ea
      - approx 12mA/mW/cm^2
      - IR only – no response at 650nm
      - no risetime in datasheet
      - no polar pattern in datasheet
      - not recommended due to poor datasheet

<!-- end list -->

  - [BPW85](https://uk.farnell.com/vishay/bpw85/phototransistor-t1/dp/1045380)
      - [datasheet](https://www.farnell.com/datasheets/2046147.pdf)
      - Vishay, 3mm package
      - 67p ea.
      - 1-8mA/mW/cm² (BPW85C best at 3-8mA/mW/cm²)
      - wide response. peak 850nm, 60% at 650nm
      - 2µs into 100Ohm
      - ±25° peaky polar pattern
      - Common device with response similar to many others. Be sure to get parts all from same sensitivity bin – e.g. BPW85C. Parts without a bin suffix could have very large range of sensitivity.

<!-- end list -->

  - [TEFT4300](https://uk.farnell.com/vishay/teft4300/phototransistor-t1/dp/1045526)
      - [datasheet](https://www.farnell.com/datasheets/2049892.pdf)
      - Vishay, 3mm package
      - 83p ea
      - 3.2mA/mW/cm²
      - **Heavily filtered IR only. No response at \<= 850nm**
      - 2µs into 100Ohm
      - ±30° very nice polar pattern
      - This will only work with emitters running at about 940nm\!

<!-- end list -->

  - [TEPT5600](https://uk.farnell.com/vishay/tept5600/phototransistor-npn-570nm-5mm/dp/1497673)
      - [datasheet](https://www.farnell.com/datasheets/2050709.pdf)
      - Vishay, 5mm package
      - 89p ea
      - 3.5mA/1000lux
      - eye response so good for red light, no response at IR
      - no response time shown
      - ±20° response
      - effectively a narrow-angle TEPT5700

<!-- end list -->

  - [TEPT5700](https://uk.farnell.com/vishay/tept5700/photo-transistor-npn-570nm-5mm/dp/1497676)
      - [datasheet](https://www.farnell.com/datasheets/2050726.pdf)
      - Vishay, 5mm truncated package
      - 98p ea
      - 0.75mA/1000lux
      - eye response so good for red light, no response at IR
      - no response time shown
      - ±50° response but with poor on-axis figure 10% down
      - effectively a wide-angle TEPT5600

<!-- end list -->

  - [BPW16N](https://uk.farnell.com/vishay/bpw16n/phototransistor-npn-t-3-4/dp/1612656)
      - [datasheet](https://www.farnell.com/datasheets/2238195.pdf)
      - Vishay, 1.8mm top-hat package
      - 94p ea
      - 0.14mA/mW/cm²
      - wide reponse. peak 850nm, 60% at 650nm
      - 5µs into 100Ohm
      - ±40° – nice polar pattern
      - essentially the same as BPW17N but with wider acceptance

<!-- end list -->

  - [BPW17N](https://uk.farnell.com/vishay/bpw17n/phototransistor-t3-4/dp/1045523)
      - [datasheet](https://4donline.ihs.com/images/VipMasterIC/IC/VISH/VISH-S-A0001142650/VISH-S-A0001142650-1.pdf?hkey=6D3A4C79FDBF58556ACFDE234799DDF0)
      - Vishay, 1.8mm top-hat package
      - 105p ea
      - 1mA/mW/cm²
      - wide response. peak 850nM, 60% at 650nm
      - 5µs into 100Ohm
      - ±12°
      - narrow acceptance, fiddly package but fits inside 2.54mm grid, same silicon as BPW96?

<!-- end list -->

  - [BPW96B](https://uk.farnell.com/vishay/bpw96b/phototransistor-npn-optical-sensor/dp/1470163)
      - [datasheet](https://www.farnell.com/datasheets/2047104.pdf)
      - Vishay, 5mm package
      - 117p ea
      - 3-7mA/mW/cm²
      - wide response curve. peak at 850nm, 60% at 650nm
      - 2µs into 100Ohm
      - ±20° angle
      - nice polar pattern

<!-- end list -->

  - [SFH 3310](https://uk.farnell.com/osram-opto-semiconductors/sfh-3310/photo-trans-npn-570nm-radial-leaded/dp/2981743)
      - [datasheet](https://www.farnell.com/datasheets/2711863.pdf)
      - Osram 3mm package
      - 125p ea
      - human eye response, 0.5mA/mW/cm^2 (maybe), ambigiuous response chart
      - very wide angle ±75°
      - no risetime given

If you got this far and did not see your favourite part, let me know and I can add it to the list.
