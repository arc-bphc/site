---
title: Mecanum Wheeled Rover
tags: [arduino,Servo,PWM]
layout: article
mode: normal
type: article
sharing: true
author: Anish Agarwal, Saksham Yadav
show_author_profile: false
show_title: true
full_width: false
header: true
cover: /assets/images/blog/thumbnails/Servo Motors PWM.png
---

# Mecanum Wheeled Rover 

The Mecanum wheel is based on a tireless wheel, with a series of rubberized external rollers obliquely attached to the whole circumference of its rim. These rollers typically each have an axis of rotation at 45° to the wheel plane and at 45° to the axle line.Each Mecanum wheel is an independent non-steering drive wheel with its own powertrain, and when spinning generates a propelling force perpendicular to the roller axle, which can be vectored into a longitudinal and a transverse component in relation to the vehicle.


<img src="{{site.baseurl}}/assets/images/blog/Mecanum-wheeled-bot/1.png" alt="Resistor" width=auto height=auto>



Movements to any directions:
blue: wheel drive direction; red: vehicle moving direction
a) Moving straight ahead, b) Moving sideways, c) Moving diagonally, d) Moving around a bend, e) Rotation, f) Rotation around the central point of one axle
The typical Mecanum design is the four-wheel configuration as demonstrated by one of the URANUS omni-directional mobile robot  or a wheelchair with Mecanum wheels, with an alternating with left- and right-handed rollers whose axles at the top of the wheel are parallel to the diagonal of the vehicle frame (and hence perpendicular to the diagonal when at where the bottom of the wheel contacts the ground). In such a way, each wheel will generate a thrust roughly parallel to the corresponding frame diagonal. By varying the rotational speed and direction of each wheel, the summation of the force vectors from each of the wheels will create both linear motions and/or rotations of the vehicle, allowing it to maneuver around with minimal need for space. 

For example:
Running all four wheels in the same direction at the same speed will result in a forward/backward movement, as the longitudinal force vectors add up but the transverse vectors cancel each other out;
Running (all at the same speed) both wheels on one side in one direction while the other side in the opposite direction, will result in a stationary rotation of the vehicle, as the transverse vectors cancel out but the longitudinal vectors couple to generate a torque around the central vertical axis of the vehicle;
Running (all at the same speed) the diagonal wheels in one direction while the other diagonal in the opposite direction will result in a sideways movement, as the transverse vectors add up but the longitudinal vectors cancel out.
A mix of differential wheel motions will allow for vehicle motion in almost any direction with any rotation.

# Assembling the chassis

## Components

The following is a list of all things necessary to build the chassis for the line follower robot. All the below listed items are included in the kit.

| Sl No. | Name | Quantity |
| --- | --- | --- |
| 1   | Chassis Base | 2 |
| 2   | Mechanum Wheels | 4  |
| 3   | BO Motors | 4   |
| 4   | Arduino UNO | 1   |
| 5   | HC05 Bluetooth Module | 1 |
| 6  | L293D Motor Driver Shield | 1 |
