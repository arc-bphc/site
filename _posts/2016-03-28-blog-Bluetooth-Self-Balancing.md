---
title: Bluetooth controlled Self-Balancing Segway Robot
tags: [self-balancing,l298n,IMU,mpu6050,arduino,hc05,bluetooth]
layout: article
mode: normal
type: article
sharing: true
author: Parakh M. Gupta
show_author_profile: true
show_title: true
full_width: false
header: true
cover: /assets/images/blog/thumbnails/Bluetooth controlled Self-Balancing Segway Robot.png
---

## Aim
To make a self-balanced robot which can be controlled through Bluetooth.
<!--more-->
## Hardware used
- 1 – Arduino Uno
- 2 – Bluetooth Module HC-05.
- 2 – 500 RPM Geared motor.
- 1 – L298 H-bridge motor driver.
- 1 – MPU-6050 Accelerometer+Gyroscope.
- 1- 7.4V LiPo Battery.
<img src="{{site.baseurl}}/assets/images/blog/bluetooth-self-balancing/2.png" alt="Resistor" width=auto height=auto>

## Details
The project was inspired by Segways, and to control it using Bluetooth. The battery being used is 7.4V LiPo but the motors need 11.1V in order to perform at the maximum capacity. The values of the constants for PID algorithm make it stable by calculating and adjusting the input 30 times a second.
<img src="{{site.baseurl}}/assets/images/blog/bluetooth-self-balancing/1.png" alt="Resistor" width=auto height=auto>

<div>{%- include extensions/youtube.html id='_0YfaQifOyI' -%}</div>
