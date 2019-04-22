---
title: Overview
category: Start Line
order: 1
---

The start line is rather simple: its only job is to allow racers to **input their ID number** and **send the start signal** to the finish line when the start wand is tripped

This is accomplished with a minimal bill of materials. Besides general electrical prototyping resources and 3d printed parts (which can be found in the next section), here is what you will need:
1. [Arduino Uno](https://store.arduino.cc/usa/arduino-uno-rev3)
    1. [Xbee Arduino Shield](https://www.robotshop.com/en/xbee-shield-arduino.html?gclid=Cj0KCQiAnuDTBRDUARIsAL41eDpHZFOGaLQYXSEpOHFxAVxpOQJQqTM2JMBtAN9JQMKceqJMhFQ_KqoaAlMgEALw_wcB)
1. [2.4 Ghz Xbee](https://www.mouser.com/ProductDetail/Digi-International/XB24CDMSIT-001/?qs=XmMZR4xR0DDHBWHJZQYv7A%3d%3d&utm_source=eciaauthorized&utm_medium=aggregator&utm_campaign=XB24CDMSIT-001&utm_term=XB24CDMSIT-001&utm_content=Digi-International) with compatible [RPSMA Antenna](https://www.sparkfun.com/products/558)
1. [9 Button Keypad](https://www.amazon.com/Adafruit-Membrane-Matrix-Keypad-Extras/dp/B00NAY2XUS/ref=pd_lpo_vtph_60_lp_tr_t_2?_encoding=UTF8&psc=1&refRID=GX9J0P5HFSPRCMQ4GF38)
1. Micro Switch (triggerable with 0.005N-m of torque)
1. Extensible Spring (Approximately 1/4" x 7/8")

> This Xbee works over 4000 feet with line of sight. If you need less distance, others can be substituted to save on cost. Just make sure you find a compatible antenna!

> **A Note Regarding Power Supplies:**
> We have refrained from listing a power supply in the bill of materials, as we have found different solutions work well for different scenarios. Beyond simply wiring up a 9 volt battery or multiple AA batteries in parallel, we have also had success using USB battery banks that are widely available for charging cell phones. You simple need to take a USB cable and cut it open to expose the positive and ground wires, then plug these into the power terminals of the Arduino.

