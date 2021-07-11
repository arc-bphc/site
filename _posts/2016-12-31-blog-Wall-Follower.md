---
title: Wall Follower 
tags: [arduino,hcsr04,l298n]
layout: article
mode: normal
type: article
sharing: true
author: C.Vineel
show_author_profile: true
show_title: true
full_width: false
header: true
cover: /assets/images/blog/thumbnails/Wall Follower.png
---
## Aim
To follow a wall (The wall refers to a boundary line of any shape) .The robot has to simply follow the wall wherever the wall leads to, the robot must go there.
<!--more-->


## Hardware Used

1. Arduino Uno.

2. Breadboard.

3. Ultrasound Sensors(X3).

4. 12 Volt Battery.

5. L293d Motor Driver Chip With Breakout Board.

6. 150 RPM Motors.

7. Chassis (2 Wheel).

8. Regular Size Castor Wheel.


<img src="{{site.baseurl}}/assets/images/blog/thumbnails/Wall Follower.png" alt="Resistor" width=auto height=auto>

## WORKING
This Robot Uses 3 Ultrasound Sensors(Left(l),Right(r),Center(c)).The Robot first moves forward.If the distance measured between any of the sensors and a wall is less than 12 cm then it means that a wall is found(sensor is active) and this has to followed. The robot responds in the way that is given in the table below.

SENSOR ACTIVE |                RESPONSE|
--------------|------------------------
c only     |              Turn right or left
r only     |              Move Forward
l only    |                Move forward
l and r     |             Move forward
l and c    |          Turn Right
r and c        |         Turn Left
all sensors   |      Turn 180 degree and Reverse.
No Sensor   |        Move forward

(before a wall is found)

9.No Sensor           STOP ,Turn Right Search for a wall,if not found come back to initial position,Then Turn Left And Search for a wall and start following it as soon as it is found.

(After A wall is found)

It is also made sure that the wall follower lies at a distance range of 3-10 cms from the wall According to the following table.

SENSOR ACTIVE |     DISTANCE FROM WALL |     RESPONSE
--------------|------------------------|--------------
Left           |                less than 3          |                      Turn Right
Left           |               greater than 10         |               Turn Left
Right          |              less than 3              |                  Turn Left
Right          |              greater than 10            |           Turn Right

This will be helpful in case of walls which are not straight,round walls.It can even avoid obstacles of any shape.

The Robot Cannot Turn 90degree Perfectly near turnings  so there is a high chance it may  either collide with the wall or deviate slant wards.The above arrangement removes these difficulties.

<div>{%- include extensions/youtube.html id='D0oTSD_81vU' -%}</div>


Multiple Authors: Satcheel Reddy Chamakoora and C.Vineel
{:.info}