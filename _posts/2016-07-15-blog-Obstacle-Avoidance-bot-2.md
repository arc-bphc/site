---
title: Obstacle Avoidance Vehicle 2
tags: [arduino,ultrasonic,l298n]
layout: article
mode: normal
type: article
sharing: true
author: Somjit Banerjee
show_author_profile: true
show_title: true
full_width: false
header: true
cover: /assets/images/blog/thumbnails/Obstacle Avoidance Vehicle 2.png
---

## Aim
The aim of this robot is to avoid all the obstacles in its path and to move on the path that is less crowded.
<!--more-->

## Hardware Used
- 1 – Arduino Uno.
- 1 – breadboard.
- 1-9V battery supply for Arduino.
- 1 – 12V supply for motors.
- 1 – chasis.
- 2 – 100 rpm motors.
- 1 – regular sized castor wheel.
- 1 – ulrasound sensor.
- 1 – servo motor.
<img src="{{site.baseurl}}/assets/images/blog/thumbnails/Obstacle Avoidance Vehicle 2.png" alt="Resistor" width=auto height=auto>

## Working
This uses the ultrasound sensor to calculate the distance of the object in front of it and it is programmed in such a way that if the object distance is less than 30 cm the bot stops moving forward. The servo motor then makes the ultrasound sensor turn 90 degrees right and records the distance and then 90 degrees left and records the object distance.Depending on which of the object distances (left or right) is less it takes a turn towards that direction and continues to move forward until the initial condition is met.


<div>{%- include extensions/youtube.html id='nEKwp_5kVLY' -%}</div>

