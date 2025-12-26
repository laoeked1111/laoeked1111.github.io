---
layout: default
modal-id: 1
title: Stepper Motor Driver
date: 2025-12-10
img: stepper-motor-driver.png
alt: image-alt
project-date: December 2025
description: For my final project in my power electronics class, I designed and built a stepper motor driver from scratch and a feed-forward boost converter to power a stepper motor from battery-level voltage. Later, I designed a PCB for the motor driver.
---

***

## Project Details

### Links

I made this [Github repository](https://github.com/laoeked1111/stepper-motor-driver) to store the files for this project. A full explanation of my power electronics is provided in [this document](https://github.com/laoeked1111/stepper-motor-driver/blob/main/power-electronics-final-project/Power_Electronics_Final_Project_Report.pdf), but a summary will be provided here.

### Context

A quick search on YouTube for "stepper motor music" will give many [results](https://www.youtube.com/results?search_query=stepper+motor+music) showcasing the creative use of stepper motors to play musical notes and recreate songs purely out of what would otherwise be undesirable mechanical noise. I wanted to try playing music like this, and while I had some stepper motors that I had obtained for cheap, I did not have any motor drivers. I decided that for my power electronics final project, I would make a driver, and the final demo for the project would be to play a song on a motor.

### Full-Step Driver

I decided to operate the stepper motor using full-step driving, where both coils in a bipolar stepper motor are energized at once but with different patterns to keep the motor spinning in one direction. Each individual coil can be energized by sending current in one direction for half a cycle, then flipping the polarity and sending current the other way for the other half-cycle. Both coils use this control pattern, but with a 90 degree phase offset. The driving can be accomplished using a H-bridge on each coil, such as the one depicted in this [article](https://forum.digikey.com/t/how-to-drive-a-stepper-motor/13412). To produce the control signals needed to operate the H-bridges, I used a four-state finite state machine and some digital logic to create the following waveforms:

![control signals](img/portfolio/stepper-motor-driver/four_control_signals.png)

These waveforms are used as the control signals to MOSFET gate drivers to control the H-bridges and drive the motor. With VDD at 12 volts, the voltage across one H-bridge with the motor connected swings between 12V and -12V, with some distortion due to motor back EMF.

![h bridge output](img/portfolio/stepper-motor-driver/h-bridge-output-with-motor.png)

### Feed-forward Boost Converter

As an additional challenge, I sought to be able to power the entire system with a battery-level voltage (6V). To reach the voltage required for the motor and the MOSFET drivers in H-bridges, I designed a boost converter to take any input voltage less than 15 volts and bring it up to 15V. Initially, I had wanted to implement current-mode control; however, it quickly became apparent that such a feedback system was too difficult to implement in the time allotted for the project. So instead, I used a feed-forward system that computes the duty cycle needed for the boost converter to produce 15V at the output, and that controls the switch in the boost converter. 
<br>
<br>
Additionally, since there is a MOSFET driver in this circuit that requires VCC of at least 12V to operate correctly, I also created a self-start circuit that would bring the boost converter output voltage up to 15V before shutting off and allowing the MOSFET driver to take over and run off the boosted output voltage. An example of the boost converter output voltage across a 100 ohm power resistor with 6V input is shown below. More details are availble in my [project report](https://github.com/laoeked1111/stepper-motor-driver/blob/main/power-electronics-final-project/Power_Electronics_Final_Project_Report.pdf).

![boost output](img/portfolio/stepper-motor-driver/boost-6V-input.png)

### Power Electronics Project Conclusion

By the end of the project, my circuitry spanned my whole desk space across 5 boards. But I was able to play music! I used the oscillator controlling the motor driver to play specific frequencies that would let me play "Mary Had a Little Lamb" on the motor.

![hardware](img/portfolio/stepper-motor-driver/hardware.jpg)

<div class="video-container">
    <iframe src="https://www.youtube.com/embed/u_e1eiWVLy0" title="Stepper Motor Music" frameborder="0" allow="accelerometer" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
</div>

I did a rough estimate and calculated that the overall efficiency of the system was around 50%, which is not great. I suspected that when the motor was running, the boost converter output voltage was sagging enough for the self-start circuit to turn on again, which was pulling more current and wasting more power.

### Current and Future Work

Currently, I am working on a PCB for the motor driver without the boost converter, which is also the thumbnail for this project post. I will add more details on that here later. Additionally, some things I would like to add in the future are direction control, current limiting with a chopper, and other driving patterns like half-step, wave drive, and microstepping.
