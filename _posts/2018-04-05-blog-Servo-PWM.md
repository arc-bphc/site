---
title: Servo Motors PWM
tags: [arduino,Servo,PWM]
layout: article
mode: normal
type: article
sharing: true
author: Yug Ajmera
show_author_profile: true
show_title: true
full_width: false
header: true
cover: /assets/images/blog/thumbnails/servo_pwm.jpg
---
## Aim
Explore the working of the servo library.
<!--more-->
## Story
While playing with servo motors, I came across an interesting concept of pulse width modulation connected to the servo motors which I will be discussing here.
Servo library has to be called and an object has to be made in the Arduino IDE for controlling the servo motor. Once we do that we use object_name.write() and specify the angle which the servo should be turned to. Servo control is actually achieved by sending a PWM signal to the servo motor. But since there are only 6 PWM pins on the Arduino Uno does that mean we can connect only 6 servos to it ?

For comparison I used the same servo on both PWM as well as non-PWM pins on the Arduino and there was no visible performance difference ! If PWM is used by servos, there has to be a difference ! So whats the hack then ?

The key to this is the fact that the Servo library does not use PWM !! The servo pulses are 1ms long. Therefore they must be driven by the frequencies around 1 kHz which is very easy to generate by the software. When we call the write() function, it computes a pulse width in micro seconds and stores it in a global array. Then there is a single timer that regularly triggers an interrupt which changes the output signals according to each channel's desired pulse width. Hence, the Servo library uses standard means to change the state of the pins just as we do Bit-Banging !

The Servo library supports up to 12 servos on most of the Arduino boards using only one timer. It can actually run servos on all pins simultaneously !