---
layout: default
modal-id: 5
date: 2023-10-01
img: watermelon-ripeness.jpg
alt: image-alt
project-date: October 2023
description: In high school, I built a photoacoustic probe in order to test the ripeness of watermelons. This was a multi-year project that culminated in the publication of a manuscript in IEEE Sensors.
---

***

## Project Details

### Links

All the technical details can be found in this [manuscript](https://ieeexplore.ieee.org/document/10255625), but a fairly detailed summary of the project is given here.

### Context

The quality and taste of a watermelon depend mostly on its degree of ripeness. 
Many different properties of the watermelon change during ripening, but two important ones are the redness of the flesh and the thickness of the rind. 
In particular, as the watermelon ripens, the flesh becomes more red due to lycopene buildup while the rind thickness.

Cutting open the watermelon is a very easy way to determine its ripeness, but we would obviously prefer a nondestructive method for ripeness detection. Some of the methods used include acoustic methods like knocking on the watermelon and NIR spectroscopy, but these have faced various limitations.
I wanted to use a photoacoustic method to determine watermelon ripeness.

### Rationale

By shining a pulsed laser onto a watermelon, some of the light will be absorbed on the outside skin, and some will transmit through the skin and be absorbed at the inner flesh. These two areas of absorption will rise in temperature and expand, each producing a photoacoustic wave which can be detected. The time delay between the two waves, multiplied by the speed of sound through the watermelon, should equal the thickness of the rind. Meanwhile, the strength of the wave from the inner flesh should correlate with flesh redness.

![rationale](img/portfolio/watermelon-ripeness/rationale.png)

### Feasibility

In order to determine the feasibility of using photoacoustics for detecting watermelon ripeness, I performed some characterization experiments on the watermelon rind and then performed a feasibility experiment using what I learned.
A summary of my findings is given below.

![feasibility experiments](img/portfolio/watermelon-ripeness/feasibility-experiments.png)

I used a spectrometer to determine the transmission spectrum of watermelon rind in order to determine what laser color would be best for reaching the inner flesh. I found that green or blue light had the greatest transmission, so I settled on a laser wavelength of 532 nm. 

Then, using a 532 nm laser, I observed the transmission when varying the excitation spot and the rind thickness. As expected, thicker rinds had lower transmission due to scattering inside the rind, while darker spots on the surface resulted in greater absorption at the surface, reducing the overall transmission.

Using a pulser-receiver and two ultrasound transducers, I also determined that lower frequencies transmit through the rind better than higher frequencies and that the speed of sound through the watermelon rind is approximately 400 m/s.

With this knowledge, I set up a feasibility experiment, where a 532 nm pulsed laser shined onto a watermelon half and an ultrasound transducer received the photoacoustic signals. 
The watermelon and transducer were submerged in water for better acoustic coupling.
The waveforms that I collected were good quality, and I was able to visually identify the beginnings of the waves coming from the skin and flesh respectively.
When I took the time difference and multiplied by the speed of sound, I got results that were close to the actual rind thickness, so I concluded that this method was feasible. 
An example of a PA signal is shown below.

![pa signal](img/portfolio/watermelon-ripeness/pa-signal.png)

I presented this work at Regeneron ISEF and received 3rd place in Embedded Systems.

### Handheld Probe

After determining that the idea was feasible, I set out to create a more compact and practical design for the ripeness detector. An image is shown below.

![probe](img/portfolio/watermelon-ripeness/probe.png)

The 3D printed cuboidal structure can be screwed directly onto the laser head, and the ultrasound transducer can be screwed onto the side via a 3D printed piece. 
The opposite side has a photodiode that is used as a trigger signal for synchronization during data collection.
Inside the cube, there is a glass pane which is transparent to the laser beam but reflective to ultrasound, so the laser light can shine straight onto the watermelon while the photoacoustic waves will be reflfected toward the ultrasound transducer.
Additionally, water inside the cube serves for acoustic coupling.
The sides are made out of clear acrylic to avoid absorbing any extra light and interfering with measurement of the signal of interest.
The bottom is made of food-wrap to provide a surface that will conform to the watermelon.

Some new additions were also made to the design of the photoacoustic probe that were not present in the feasibility study. 
An optical filter was added in front of the laser beam to only allow 532 nm laser light through and block other extraneous wavelengths produced by the laser.
Additionally, an acoustic lens was made for the ultrasound transducer out of PDMS for better signal pickup.

### Testing the Probe

I first tested the probe's ability to determine rind thickness and then tested the ability to determine flesh redness.

To test rind thickness detection, I took a watermelon and removed layers of rind to simulate different rind thicknesses.
I used a cross-correlation algorithm to compare each signal to one in which I had manually determined the two PA waves, and using the calculated time delay, I calculated the rind thickness. 
I found fairly accurate estimates of the rind thickness this way.

For flesh redness testing, I simulated different redness levels by making different solutions of red ink and placing them in plastic bags under the same depth of rind.
From each signal, I subtracted a "background" signal where there was no ink bag and normalized the difference. 
After using cross-correlation to determine the location of the inner flesh PA wave, I am able to compare the relative signal strength of the different concentrations of ink.
Again, I found promising results, with the signal strength improving with concentration.

For fun, I also fed everything into a bag of SFA symbols (BOSS) classifier and found that the classifier was able to achieve high accuracy when classifying both rind thickness and flesh redness.

### Later Steps

I made some modifications to the design of the probe later and did more testing. More details are available in the [manuscript](https://ieeexplore.ieee.org/document/10255625).
