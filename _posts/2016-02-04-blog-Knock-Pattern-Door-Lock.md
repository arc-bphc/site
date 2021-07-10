---
title: Knock Pattern Door Lock
tags: [LCD,arduino,servo,automation,Piezosensor]
layout: article
mode: normal
type: article
sharing: true
author: Ebin Phillip
show_author_profile: true
show_title: true
full_width: false
header: true
cover: /assets/images/blog/thumbnails/knock-door-lock.png
---

## Aim
To create a door lock which is based on Knock Pattern.
<!--more-->
## Hardware
- Arduino
- Piezosensor
- Servo
- LCD screen
- Plastic case
- Push button Switch
- Wires and resistances
- Batteries (9 V)

## Details
A piezosensor is mounted on the door. This senses the knocks and using this information, the Arduino records the intervals between the knocks and stores a knock pattern password.
The Arduino, servo (attached with the latch), LCD screen and circuit are enclosed in the plastic case.
The LCD screen displays appropriate messages to enable interaction with the user.
When a person knocks on the door, his/her knock pattern is compared with the preset knock password using Arduino.
If the person’s knock password matches the preset, the servo rotates and the latch opens.
<img src="{{site.baseurl}}/assets/images/blog/thumbnails/knock-door-lock.png" alt="Resistor" width=auto height=auto>

## Special features
1. The Arduino is programmed such that the tempo of the knocks can be varied.
2. The password can be reset and another knock pattern can be recorded as the preset.
3. In case required, a push switch is present which can reset the system and the original set knock password is considered as the preset.


<div>{%- include extensions/youtube.html id='gDD_UTZ6C_8' -%}</div>


Multiple Authors: Ebin Phillip(2014 Batch), Swarali Patil(2015 Batch), Tejeshwar Reddy (2014 Batch),Abhilash Chivukula (2015 Batch), Abhijit Bajaj (2015 Batch) and Shivang Dixit (2015 Batch).
{:.info}