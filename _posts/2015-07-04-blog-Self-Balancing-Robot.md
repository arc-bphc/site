---
title: Self-Balancing-Segway Robot
tags: [l298n,IMU]
layout: article
mode: normal
type: article
sharing: true
author: Suyash Yeotikar
show_author_profile: true
show_title: true
full_width: false
header: true
cover: /assets/images/blog/thumbnails/Self-Balancing-Segway Robot.png
---

## Aim
The main idea of the project was to build a wireless Dicycle robot that could balance itself on two wheels using its orientation (angle) with the vertical as a feedback.

<!--more-->


## Details
The project was inspired by segways, and to build an autonomous segway. The concept of segway is based on the inverted pendulum problem. The advantage of such a segway would be that it would consume lesser power (only two motors) and would still be able to move around and complete the tasks of a 3 wheeled or 4 wheeled robot.  The robot built was rudimentary and only capable of balancing itself. The further idea was to incorporate this with the gesture controlled robot , to control the robot using gestures. However the robot was not improved upon, and left at the rudimentary stage.

## Hardware involved
- 2 wheels
- mechanics kit to build structure
- 2 DC motors
- L298 motor driver (to drive motors)
- 6 V AA battery pack to power motors
- Arduino (As the microcontroller)
- MPU 6050 with accelerometer and gyroscope to measure angle of robot
- 6 V AA battery pack to power arduino.

## Software involved
Arduino programming to gather data from sensors apply filter on them and command the motors using a PI controller.

## Advice from the Maker(s)
The robot can improved upon by incorporating the readings of gyroscope too (it’s readings were faulty in my case). The filter that was used was a mean value filter on the readings of only the accelerometer. However in improvement, complementary filter or kalman filter will have to be used to combine the readings of gyroscope and accelerometer. The combined readings would make the robot more controlled and will reduce the oscillations.

<div>{%- include extensions/youtube.html id='XvHmo1aPvVg' -%}</div>


