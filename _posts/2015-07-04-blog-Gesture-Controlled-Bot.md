---
title: Gesture Controlled Bot
tags: [Gesture,l298n,HC-05,bluetooth,arduino,MATLAB,Image Processing]
layout: article
mode: normal
type: article
sharing: true
author: Suyash Yeotikar
show_author_profile: true
show_title: true
full_width: false
header: true
cover: /assets/images/LogoWhite.png
---

## Aim
To build a wireless differential drive robot (3-wheeled robot) , that can controlled by using gestures which are recognised by using image processing.
<!--more-->

## Details
The project began as an extension of the virtual mouse, as per which the mouse of any computer can be controlled by using gestures which are identified by image processing. A finger was covered with colored paper to make it distinguishable from the environment for the algorithm. The direction as well as the speed of robot can be controlled. Direction is decided by the relative position of the finger with respect to centre and the speed is decided by the distance of the finger from the camera. The interpretation of gestures was then sent to the robot by using Bluetooth from laptop.


## Hardware involved
- 2 wheels
- chassis
- 1 castor wheel( free moving front wheel)
- 2 DC motors
- L298 motor driver (to drive motors)
- 12 V 1.3 Ah Lead Acid rechargeable battery (to power motors)
- Arduino (As the microcontroller)
- HC-05 Bluetooth module (to receive commands from laptop over Bluetooth)
- 6 V AA battery pack to power arduino.

## Software Involved
MATLAB Image Acquisition Toolbox to acquire images over laptop webcam of the gestures and Image Processing Toolbox to extract gestures and interpret their meaning. Arduino programming to receive message through HC-05 bluetooth module and accordingly command motors

<div>{%- include extensions/youtube.html id='cEbqooYJVtI' -%}</div>
