---
title: EasyMouse
tags: [arduino,ADXL345,IMU,mpu6050,nrfl2401]
layout: article
mode: normal
type: article
sharing: true
author: Akhil Raj Baranwal
show_author_profile: true
show_title: true
full_width: false
header: true
cover: /assets/images/blog/thumbnails/EasyMouse.png
---

## AIM
Carpal Tunnel syndrome is a common problem with people who are involved in desk-work, working with a traditionally designed mouse, or a pointing device to be more specific. EasyMouse aims to make a pointing device optimised for gaming, based solely on gestures. As a result, Carpal Tunnel Syndrome is avoided in the long run.
<!--more-->
<img src="{{site.baseurl}}/assets/images/blog/thumbnails/EasyMouse.png" alt="Resistor" width=auto height=auto>

## Hardware 
- ARDUINO NANO
- ADXL345
- MPU-6050
- nRF24L01(for the wireless communication)

### ADXL345
ADXL345  is a small, thin, ultralow power, 3-axis accelerometer with high resolution (13-bit) measurement at up to ±16 g.  The ADXL345 is well suited for mobile device applications. It measures the static acceleration of gravity in tilt-sensing applications, as well as dynamic acceleration resulting from motion or shock. Its high resolution  (3.9mg/LSB) enables measurement of inclination changes less than 1.0°.

### nRF24L01
nRF24L01 is a single chip radio transceiver for the world wide 2.4 – 2.5 GHz ISM
band. The transceiver consists of a fully integrated frequency synthesizer, a power
amplifier, a crystal oscillator, a demodulator, modulator and Enhanced ShockBurst™
protocol engine. Output power, frequency channels, and protocol setup are easily
programmable through a SPI interface. Current consumption is very low.

## Working
The ‘driver’  which is written in Python, receives instruction packets from the Arduino and uses pyautogui to perform GUI operations. Since this is a custom mouse, a gesture can be programmed to trigger, for example, 5 mouse-clicks in 250 milliseconds.
Similarly, another gesture can be programmed to trigger a series of perfectly timed combination of keystrokes and mouse-clicks, which are useful in hitting combos in games like Mortal Kombat.General pointing and cursor movement will also have greater precision and sensitivity, all of which can be customised according to personal preference.

All files related to this project are [here](https://github.com/akhilrb/easymouse).

