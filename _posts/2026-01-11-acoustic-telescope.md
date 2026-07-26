---
layout: project
title: Please Listen Carefully
tags: [Hardware, Software, Circuits, Mechanical]
date: 2026-01-11
img: please-listen-carefully.jpg
project-date: January 2026
description: Metamaterials approach to varifocal acoustic lensing.
---

***

This project was a collaborative effort between Jieruei Chang, Caroline Jiang, Bernard Jin, Liong Ma, Nevin Thinagar, and me as part of Formlabs' hardware hackathon during IAP 2026. Inspired by a paper we read, we sought to create a varifocal acoustic focusing system that automatically focuses sound at a target.

The lenses were designed using k-wave simulation and SLA printed at Formlabs. The front lens can move relative to the back lens because of a linear rail controlled by a stepper motor. A Teensy is connected to the stepper motor as well as an ultrasonic distance sensor to identify the distance from the target. 

Power is supplied via a 6S LiPo battery which is bucked down to 3.3V. A fire alarm is used as a switch to connect power to the device, and a keyboard switch is used as the trigger to play 1kHz noise out of a speaker directed at the lenses.
