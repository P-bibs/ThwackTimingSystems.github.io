---
title: Overview
category: Finish Line
order: 1
---


The finish line is the main brains of the timing gate. It **times racers** as they go down the course and holds the **database of results**. Users can connect to the **web server** the finish line hosts to retrieve these results.

The design of the finish lines is not complete yet. Specifically, we are still researching powerful infra-red LEDs to use for a finish line break-beam sensor. Below is a partial list of materials.
1. [Raspberry Pi Model 3 B+](https://www.raspberrypi.org/products/raspberry-pi-3-model-b-plus/)
1. [2.4 Ghz Xbee](https://www.mouser.com/ProductDetail/Digi-International/XB24CDMSIT-001/?qs=XmMZR4xR0DDHBWHJZQYv7A%3d%3d&utm_source=eciaauthorized&utm_medium=aggregator&utm_campaign=XB24CDMSIT-001&utm_term=XB24CDMSIT-001&utm_content=Digi-International) with compatible [RPSMA Antenna](https://www.sparkfun.com/products/558)
1. [1.2" 7 Segment Display](https://www.adafruit.com/product/1270)

> This Xbee works over 4000 feet with line of sight. If you need less distance, others can be substituted to save on cost. Just make sure you find a compatible antenna!

> **A Note Regarding Power Supplies:**
> We have refrained from listing a power supply in the bill of materials, as we have found different solutions work well for different scenarios. Beyond simply wiring up a 9 volt battery or multiple AA batteries in parallel, we have also had success using USB battery banks that are widely available for charging cell phones. You simple need to take a USB cable and cut it open to expose the positive and ground wires, then plug these into the power terminals of the Raspberry Pi.


![](//placehold.it/800x600)
