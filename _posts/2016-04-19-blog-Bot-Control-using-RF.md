---
title: Bot Control using RF
tags: [RF,l298n,arduino]
layout: article
mode: normal
type: article
sharing: true
author: Rajat Bansal
show_author_profile: true
show_title: true
full_width: false
header: true
cover: /assets/images/blog/thumbnails/Bot Control using RF.png
---

## Aim
This is a basic project to control a bot or any other appliance wirelessly using RF Module. It provides 4 output channels which can be increased or decreased by minor changes in the code.

<!--more-->
## Hardware Used
- Arduino Mega
- Arduino Uno R3
- RF transmitter & Receiver module 433MHz
- Breadboard
- DC motors
- Some jumper wires
- 12V adapter

 
## Description
The transmitter was connected with the Arduino Uno and some push buttons to take inputs as a remote control.

The receiver was connected to mega and output pins were further extended to a relay board, which in this case was used as Dual H-Bridge to control motors. This relay board can be replaced with a common relay board to control electrical appliances for home automation using the same code. The relay board was powered with a 12V adapter.
<img src="{{site.baseurl}}/assets/images/blog/thumbnails/Bot Control using RF.png" alt="Resistor" width=auto height=auto>

## Code
Whenever a push button is pressed the corresponding pin changes it states either HIGH or LOW.

### Transmitter code
Virtual Wire lib was used to use RF.

Pin no 12 was used as data pin for Tx .Pin no 7,6,5,4 were used as input pins for remote.

Code can be found [here](https://github.com/rajatbansal427/RF-bot-controll-Room-automation/blob/master/transmitter_ro_aut.ino) 

### Receiver code
The Rx receives an string of characters in a message which is stored as buf[] and buflen is the max no of characters in the string.

The Boolean data type is used to toggle state.

code can be found [here](https://github.com/rajatbansal427/RF-bot-controll-Room-automation/blob/master/Receiver_ro_au.ino)
 
<div>{%- include extensions/youtube.html id='P7Eq_2rZxt0' -%}</div>


