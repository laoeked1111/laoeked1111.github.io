---
layout: project
title: Interactive Box Display
tags: [Hardware, Embedded]
date: 2026-05-12
img: box-display.jpg
project-date: May 2026
description: Interactive box-shaped display built off a Cypress PSoC 5.
---

***

For my 6.206 [6.115] Microcomputer Project Laboratory [final project](https://github.com/laoeked1111/boxy), 
I made an interactive box display that responds to accelerometer data. 
The display offers 3 display modes: milk in a glass, snowglobe, and 
Minecraft lantern which switch with the press of a button.

## Hardware

The hardware components included a PSoC 5 development board, 4 328x480
SPI-based colored LCD modules, and a MP6050 IMU. The screens and IMU 
were integrated together in a 3D printed housing. Using the PSoC CPU to 
write to the screens one by one via SPI would be too slow, so I used
the PSoC configurable hardware to create 4 DMAs that continuously pump 
data to the LCD screens while the CPU does computation. The result
was reasonably fast screen refreshing on all four LCDs.

## Milk Glass

In this display mode, the screens represent the four sides of a glass
half-full with milk. The accelerometer records tilting information of
the glass and adjusts the shapes on the screens to reflect the tilting
of milk in the glass.

<div class="video-container">
    <iframe src="https://www.youtube.com/embed/iEaTlnpD3cA?si=hmBm7AS0WQkniou3" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
</div>

## Snowglobe

In this display mode, the screens show small white particles (snow)
which fall in the direction determined to be pointing down by the
accelerometer. Additionally, the accelerometer detects disturbances
which causes the snowflakes to jitter.

<div class="video-container">
    <iframe src="https://www.youtube.com/embed/OS154H7HaEk?si=1k78JmZ5QiAyKAKw" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
</div>

## Lantern

In the final display mode, the screens show identical still images
inspired by Minecraft lanterns. They blink in brightness according to
a sine wave stored as a fixed-point wave table, and a button press allows 
switching between the orange and blue varieties. The video doesn't show 
the effect that well due to exposure adjustment, unfortunately.

<div class="video-container">
    <iframe src="https://www.youtube.com/embed/WuRyzk-yPVE?si=pa0quAgCg0eGxx3d" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
</div>