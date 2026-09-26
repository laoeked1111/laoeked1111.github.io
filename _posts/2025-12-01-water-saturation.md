---
layout: project
title: Analog Water Saturation Sensor
tags: [Hardware, PCB, Circuits, Analog]
date: 2025-12-01
img: water-saturation.jpg
project-date: December 2025
description: Battery-powered analog water saturation sensor.
---

***

This project was a battery-powered analog water saturation sensor based off of ultrasound attenuation through cloth. The final PCB files can be found in [this repo](https://github.com/laoeked1111/water-saturation).

The system runs on a 3.3V coin cell battery, which is boosted to 5V to power the ICs.
A 555 timer drives the ultrasound transducer, and a microphone captures the ultrasound signal.
The collected signal is amplified and filtered, then passed through a comparator to produce a PWM waveform that drives a LED.
The LED lights up when the signal is low, signallying high attenuation due to water saturation, and is dim/off when the signal is high.

![schematic](/img/portfolio/water-saturation/schematic.png)

The small PCB shown above was version 3 of the project, following a breadboard prototype and two previous PCBs.
During the breadboarding phase, I initially tried to use transistors as a switching network to drive the ultrasound transducer before
discovering that a 555 timer worked even better. 
I also played around with different values for gain of the microphone during this phase.

![breadboard](/img/portfolio/water-saturation/breadboard.jpg)

In v1 of the PCB, I created a relatively large single-sided PCB with through-hole components. 
This version worked reasonably well but required some component value adjustments.

![v1](/img/portfolio/water-saturation/v1.gif)

In v2 of the PCB, I attempted to reduce the board dimensions by using SMD components. 
Unfortunately, I routed a component incorrectly and had to solder a "botch" resistor to make the board work.
However, this board was working much better than the previous one after adjusting component values.

![v2](/img/portfolio/water-saturation/v2.gif)

Finally, in v3, I changed the layout to use both sides of the board and fixed all the routing issues.
The final board size measures at 25 mm by 52 mm.

![v3](/img/portfolio/water-saturation/v3.jpg)
