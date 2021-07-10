---
title: Object Tracking Robot
tags: [object-tracking,l298n,HC-05,bluetooth,arduino]
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
The main aim of this project was to build an object tracker based on the concept of image processing for the competition of IIT-B tech fest, Polaroid.

<!--more-->

## Details
The robot was built as per the specification and problem statement of the event, Polaroid of IIT B tech fest. The basic function of the robot was to track and pick specific colored objects and deposit them in a particular location.

## Hardware involved
- 2 wheels
- chassis 
- 1 castor wheel( free moving front wheel)
- 2 DC motors
- L298 motor driver (to drive motors)
- 12 V 1.3 Ah Lead Acid rechargeable battery (to power motors)
- Arduino (As the microcontroller)
- HC-05 Bluetooth module (to receive commands from laptop over Bluetooth)
- 6 V AA battery pack to power Arduino
- 2 6V AA battery packs to power SERVO MOTORS for gripper to grab blocks.

## Software Involved
MATLAB Image Acquisition Toolbox to acquire images over laptop webcam of the gestures and Image Processing Toolbox to extract gestures and interpret their meaning. Arduino programming to receive message through HC-05 bluetooth module and accordingly command motors. A MATLAB library to control Arduino from MATLAB.

## Advice from the Maker(s)
MATLAB is slow and thus it was not wise to control Arduino through MATLAB. This mistake was realized later after the competition. It would also be preferable to use on board camera rather than overhead camera to detect and pick blocks. Also it would be better to build the robot on the lines of gesture controlled robot, wireless and controlled by Bluetooth rather than being wired. The gesture controlled robot was built after this robot and is of better design than this.


Multiple Authors: Suyash Yeotikar, Amit Sharma, Saksham Phul
{:.info}
