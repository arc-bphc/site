---
title: Indoor Radar Using Ultrasound 
tags: [hcsr04]
layout: article
mode: normal
type: article
sharing: true
author: Rohan Dvivedi
show_author_profile: true
show_title: true
full_width: false
header: true
cover: /assets/images/blog/thumbnails/Indoor Radar Using Ultrasound.png
---


## Aim
To build a indoor map of a room/chamber(rough map) by mapping the relative distance of objects on a map.

<!--more-->

## Hardware Used
- 1 – Micro servo.
- 1 – Ultrasonic sound sensor.
- 1 – Arduino.
- 1 – An image of radar.
<img src="{{site.baseurl}}/assets/images/blog/Indoor-Radar/const.png" alt="Resistor" width=auto height=auto>

## Details
A Ultrasonic distance sensor is mounted over a servo, that keeps rotating. The distances in different directions are recorded and the value of angle and distance is sent to the computer.
<img src="{{site.baseurl}}/assets/images/blog/thumbnails/Indoor Radar Using Ultrasound.png" alt="Resistor" width=auto height=auto>
In the computer a cpp code shows a image that is manipulated according to the data recieved from the controller. Black dots will be put up for the objects traced as close as 50 cm or less.

<div>{%- include extensions/youtube.html id='YPpjadmx1t0' -%}</div>
