---
title: Motion Detection Glove 
tags: [arduino,ultrasonic,servo]
layout: article
mode: normal
type: article
sharing: true
author: Yohan MR
show_author_profile: true
show_title: true
full_width: false
header: true
cover: /assets/images/blog/thumbnails/Motion Detection Glove.png
---

## Aim
To successfully identify the position of a glove from its mean position and detect a throwing action.
<!--more-->
## Hardware
- MPU6050.
- Arduino uno.
- breadboard.
- jumper cable wires.

## Details
The main aim of this project is to understand i2c communication and using the mpu6050 sensor.

## Working
From the sensor we get the Yaw, Pitch, Roll values which enables us to tell the orientation  of the sensor in space as well as the distance travelled with respect to its initial position.

Setting the base value of yaw pitch roll as the intial position we can compare it the current feed to see how its moved in the xy- plane.

Once we know how far its travelled from the origin the next part is to see if a throwing action is made in the direction of the target. For this like before we compare values In the xz plane and also the rate of change of these  values to see if the hand is moving fast enough.

This is the basic working of the project.
<div>{%- include extensions/youtube.html id='uYUHfccAfc4' -%}</div>
