---
title: Automated Flute Project
date: 2021-05-04 16:17:25 +/-0530
categories: [Tutorials, ROSCheatSheet]
tags: ros     # TAG names should always be lowercase
layout: article
sharing: true
# article_header:
#   type: cover
#   image:
#     src: /screenshot.jpg
cover: assets/images/resources/247-2474702_flute-clip-art.png
---
Automating the Flute playing process
<!--more-->
* * *

# Automated Flute Project

## Introduction

The Automated Flute Project was taken up by the 2019 Batch new inductees of the Automation & Robotics Club in January 2020. With only a few flute players on campus and it being one of the difficult instruments to master, It brought us the vision to come up with something that automates the flute playing process.

## Parts list

1.  1x Wooden flute:
2.  1x Air Pump: to blow air into the flute
3.  1x SMPS
4.  12x Servo motors
5.  3m Nylon thread
6.  6x Rubber bands
7.  1x Arduino Mega
8.  1x Air pump

## The Approach

### Getting the Notes

The first thing to grab ones attention on seeing a good flute player play are the holes he closes and the fashion in which the player attains the sounds that are rather pleasant to our ears.
We used a similar line of thought to decide that the first thing we will be needing are the notes that our flute would play.
We achieved the same using a Python script that took a waveform and generated a MIDI (Musical Instrument Digital Interface) file for the instrumental part of the song. We then converted the MIDI file to a numpy array that could be used later to play specific notes using Pyfirmata, which controlled the Arduino Mega.

### The Design

The most crucial part of the project was coming up with the correct closing mechanism for the flute holes, i.e., complete and partial closing for some specific notes. We primarily tried two designs, first with flaps and the second using rings for our closing mechanism. The former being more efficient in its functioning led us to design a flute holder with embedded flaps to act like the player's fingers which was later 3D printed. We also created a prop to channel air from the air pump into the flute. Nylon threads were used to move the flaps by tying them to the actuator -Servo motor in this case. We used rubber bands linked to the flute holder to hold the flaps in place and prevent air leakages.

<img src="{{site.baseurl}}/assets/images/resources/WhatsApp Image 2021-07-15 at 10.16.47 AM.jpeg">

### Not a bad player afterall

We then mapped the notes to a specific sequence of servos that were supposed to open the right flaps using the Numpy array to produce the "pleasant" sounds. Having everything in place, we used Pyfarmata to control the Arduino mega, which in turn controlled the 12 servos.

<img src="{{site.baseurl}}/assets/images/resources/WhatsApp Image 2021-07-15 at 10.16.47 AM (1).jpeg">