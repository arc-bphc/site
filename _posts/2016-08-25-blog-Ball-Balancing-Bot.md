---
title: Ball-balancing Bot 
tags: [arduino,hcsr04,servo]
layout: article
mode: normal
type: article
sharing: true
author: Abhinav Kumar
show_author_profile: true
show_title: true
full_width: false
header: true
cover: /assets/images/blog/thumbnails/Ball-balancing Bot.png
---

## Aim
To balance the ball automatically at the center of plate using PID controller and Machine Learning(supervised learning).
<!--more-->

## Hardware used
- Breadboards.
- Ultrasonic sensors HC SR04.
- 9v battery power supply.
- Jumper wires.
- 1-Servo motor.
- wood-to make the frame,platform and support.

## Details
The main aim of this project was to apply machine learning(Supervised Learning: Learning with the help of the given examples), to let the bot learn to balance the ball in one dimension(further it will be extended to 2 dimension).

First we measure the distance (position) of the ball using ultrasound sensor. We then calculate the deviation of the ball from its mean position (center). For training we use joystick to train the model how much it should move the servo (which is used to rotate the plate) which is proportional to angle of deviation from mean.

<img src="{{site.baseurl}}/assets/images/blog/thumbnails/Ball-balancing Bot.png" alt="Resistor" width=auto height=auto>


### Distance Measurement:
For measuring the distance  or position of the ball on the plate we have used Ultrasound Sensor to determine the deviation of ball from the mean position (center) of plate. We have used two ultrasound sensor (second one would have been redundant in ideal cases as length of plate is known),but due to noisy measurement we had use two.

### Joystick:
We have used joystick as an input to train the Machine learning model to predict the response. While training we displace the ball and give input to the computer as in the form rotating the joystick, which should be proportional to the displacement from deviation from the mean position. Its basically like playing ATARI games but in real. There our expert human response according to visual input is given to the computer and the target value for a particular deviation.

After training phase the “learned” model with its parameter was given to the Arduino which then ran and tried to balance the ball automatically. The Arduino measured the distance(position of the ball) the calculated how much it should jerk, using Servo in the right direction to bring the ball to its correct position using the model learned from us.


<div>{%- include extensions/youtube.html id='37u1pUv5rH4' -%}</div>
