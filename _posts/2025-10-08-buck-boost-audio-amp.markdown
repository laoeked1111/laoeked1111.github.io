---
layout: default
modal-id: 3
date: 2025-10-08
img: buck-boost-audio-amp.jpg
alt: image-alt
project-date: October 2025
description: During my power electronics class, we were tasked with applying our class content to determine appropriate design parameters for an adjustable audio amplifier powered by cascaded buck and boost converters.
---

***

## Project Details

The entire audio amplifier was powered by a 6 volt power supply. A boost converter stepped this voltage up to 15 volts, and then a buck converter stepped 15 volts down to a variable output voltage which could be tuned by turning a potentiometer. This voltage is used as the high side power supply of a totem pole that drives a speaker. The control signal for the totem pole is produced with a comparator that has the audio signal as an input, which is how the audio is coupled into the system. During the lab, we were asked to calculate various component values that would produce desired switching frequencies, ensure that the inductors of both the boost and buck converters would remain in continuous conduction mode, and yield a particular output voltage with sufficiently small ripple.

![full](img/portfolio/buck-boost-audio-amp/full.jpg)

Below is a video clip of me adjusting the frequency of the input sound. The recording doesn't show it too well, but it was very loud!

<div class="video-container">
    <iframe width="815" height="458" src="https://www.youtube.com/embed/hijinGS11QM" title="Buck Boost Audio Amp" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
</div>
