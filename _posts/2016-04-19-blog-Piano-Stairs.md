---
title: Piano Stairs
tags: [ldr,speaker,arduino,LED]
layout: article
mode: normal
type: article
sharing: true
author: Rajat Bansal
show_author_profile: true
show_title: true
full_width: false
header: true
cover: /assets/images/blog/thumbnails/Piano Stairs.png
---
## Aim/Details
Converting normal stairs into the keys of piano so that when someone steps on the stairs and one particular key of piano plays.
<!--more-->
The light sources should be on one side of the stair, the photo-resistors on the other. In this setup, the Arduino reads from the sensors  and plays a tone using PWM format by sending the signal wave  to the speaker.


## Hardware used
- Arduino mega 2560
- 1 Watt Led
- Photo resistors
- Resistors of values-4.7K ,10Ω
- Cardboard
- Speaker
- 5mm Audio socket
- 5mm audio jack
- Single Strand wire
- 5 V power supply
 

## Principle
A photo-resistor’s resistance value changes with respect to the intensity of light falling on it.
 <img src="{{site.baseurl}}/assets/images/blog/Piano-Stairs/circuit.png" alt="Resistor" width=auto height=auto>



## Basic circuit
Repeat this circuit 10 times to make an array.

Also, make a array of 1 watt led to illuminate the LDR

 <img src="{{site.baseurl}}/assets/images/blog/thumbnails/Piano Stairs.png" alt="Resistor" width=auto height=auto>


Code:- [Pitches](https://technopediabphc.files.wordpress.com/2016/04/pitches.docx)

[ToneMelodyino](https://technopediabphc.files.wordpress.com/2016/04/tonemelodyino.docx)
