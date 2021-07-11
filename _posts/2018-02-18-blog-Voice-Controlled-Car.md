---
title: Voice Controlled Car
tags: [arduino,LM7805,l293d,hc05,bluetooth]
layout: article
mode: normal
type: article
sharing: true
author: Yug Ajmera
show_author_profile: true
show_title: true
full_width: false
header: true
cover: /assets/images/blog/thumbnails/Voice Controlled Car.png
---
## Aim
To build a bluetooth operated voice controlled car.

<!--more-->

## Hardware Used
- Arduino Uno
- Bread Board
- Motors x 2
- Wheels x 2
- Chassis ( of appropriate size )
- Voltage Regulator LM 7805
- Motor Driver L293D
- 12V Batter ( Power source)
- Jumper Wires
- Bluetooth Module HC-05

### About Bluetooth Module HC-05
In our world of embedded electronics hackery, Bluetooth serves as an excellent protocol for wirelessly transmitting relatively small amounts of data over a short range (<100m). It’s perfectly suited as a wireless replacement for serial communication interfaces.

HC‐05 module is an easy to use Bluetooth SPP (Serial Port Protocol) module, designed for transparent wireless serial connection setup. The module has two modes of operation, Command Mode where we can send AT commands to it and Data Mode where it transmits and receives data to another Bluetooth module.

<img src="{{site.baseurl}}/assets/images/blog/Voice-Controlled-Car/1.png" alt="Resistor" width=auto height=auto>

### About Voltage Regulator LM 7805
Voltage sources in a circuit may have fluctuations resulting in not providing fixed voltage outputs. A voltage regulator IC maintains the output voltage at a constant value. 7805 IC, a member of 78xx series of fixed linear voltage regulators used to maintain such fluctuations, is a popular voltage regulator integrated circuit (IC).

<img src="{{site.baseurl}}/assets/images/blog/Voice-Controlled-Car/2.png" alt="Resistor" width=auto height=auto>

### About Motor Driver L293D
L293D is a typical Motor driver or Motor Driver IC which allows DC motor to drive on either direction. L293D is a 16-pin IC which can control a set of two DC motors simultaneously in any direction. It works on the concept of H-bridge. H-bridge is a circuit which allows the voltage to be flown in either direction.

<img src="{{site.baseurl}}/assets/images/blog/Voice-Controlled-Car/3.png" alt="Resistor" width=auto height=auto>

## Software & Working 
We connect the Bluetooth module with the mobile app. Once done, the commands which we give through the mobile get sent to the Arduino via the module. We accept character by character from the serial buffer sent by the app and combine them to form a string.

We then compare it to the command. If it matches the command is carried out. For example, the string we receive is “right” ,the bot turns right.

The code for the same are available [here]( http://yainnoware.blogspot.in/p/voice-controlled-car.html)

<div>{%- include extensions/youtube.html id='q5I7UFtxVUY' -%}</div>
