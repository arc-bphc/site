---
title: Gesture Controlled Bot
tags: [Gesture,l298n,HC-05,bluetooth,arduino,MATLAB,Image Processing]
layout: article
mode: normal
type: article
sharing: true
author: Suraj Partani
show_author_profile: true
show_title: true
full_width: false
header: true
cover: /assets/images/blog/Room-Automation/thumb.png
---


## Aim
To control the lights and fan of the room through an Android app over Bluetooth.
<!--more-->
## Hardware involved
- 4* 5 Volts Relay Board
- Arduino Board
- HC-05 Bluetooth Module
- Jumpers
- The  app which used is [Ardudroid](https://play.google.com/store/apps/details?id=com.techbitar.android.Andruino&hl=en)

Though Ardudroid has many Bugs but it works good.

<img src="{{site.baseurl}}/assets/images/blog/Room-Automation/1.png" alt="Resistor" width=auto height=auto>

## Technical details
Upload the code to Arduino (found at the bottom) and

### Connect the schematics as shown in the diagram:-
<img src="{{site.baseurl}}/assets/images/blog/Room-Automation/2.png" alt="Resistor" width=auto height=auto>

### How to connect your setup to the switch board:-

1. Go and find the MCB of your room. You will find a MCB Board in your corridor.
2. Turn the MCB off for your room only.
3. Open your Switch Board.
4. Look for a wire which is common to all the switches. The above found wire is LIVE  wire {Be cautious of it , Never touch it directly)
5. Extend this wire and feed it to all COMs of your Relay Board.
6. You will find the wire for tubelight connected to the other side of switch. Connect this wire to NO pin of any of the relays.
7. Connect other wires(From Fan/Lamp/Tubelight) to different Relays .
8. Pack your Switch Board.

## Precautions
- Don’t mess with the AC current.
- Use High quality wires for AC current.

<div>{%- include extensions/youtube.html id='YmVJkK9b70s' -%}</div>


Code files can be found [here](https://technopediabphc.files.wordpress.com/2015/10/bluetooth-code.docx)
