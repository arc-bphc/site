---
title: Secret Clap Door Lock
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
cover: /assets/images/blog/thumbnails/Secret Clap Door Lock.png
---
## Aim
To build a secret door lock that can be unlocked via clap.
<!--more-->

## Hardware Used 
- Arduino Uno
- Bread Board
- LED ( any color)
- Resistor ( 10K )
- Jumper wire (for conncetions )
- Sound sensor module 

### Sound sensor module :-
The sound sensor module provides an easy way to detect sound and is generally
used for detecting sound intensity. This module can be used for security, switch, and
monitoring applications. Its accuracy can be easily adjusted for the convenience of
usage.
It uses a microphone which supplies the input to an amplifier, peak detector and
buffer. When the sensor detects a sound, it processes an output signal voltage which is
sent to a microcontroller then performs necessary processing.
<img src="{{site.baseurl}}/assets/images/blog/Secret-Clap-door/1.png" alt="Resistor" width=auto height=auto>

## Software & Working
Here we are glowing an LED instead of opening a lock for simplicity. You can use a servo motor to open a lock. If a particular pattern of claps is detected , only then the lock will open . For this we are using a sound sensor module. In normal state , the sensor gives HIGH . As soon as a clap is detected , it gives LOW .

Access the code [here](http://yainnoware.blogspot.in/p/secret-clap-door-lock.html) 

<div>{%- include extensions/youtube.html id='toYhCtMNnYs' -%}</div>


