---
title: WiFi Controlled Lock for Room
tags: [esp-8266,l298n,linear actuator,arduino]
layout: article
mode: normal
type: article
sharing: true
author: Parakh M. Gupta
show_author_profile: true
show_title: true
full_width: false
header: true
cover: /assets/images/blog/thumbnails/WiFi Controlled Lock for Room.png
---

## Aim
To make a lock for the room which can be controlled through a webpage on local network of the router.

<!--more-->
## Hardware Used 
- 1-Arduino
- 1-ESP-8266 WiFi Module
- 1-Battery
- 1-Linear Actuator
- 1-L298 Motor Driver
<img src="{{site.baseurl}}/assets/images/blog/thumbnails/WiFi Controlled Lock for Room.png" alt="Resistor" width=auto height=auto>

## Details
The lock consists of the above mentioned hardware. The ESP hosts a webpage on the local network hosted by router. The ESP can be programmed to connect to the router and then it gives an IP which when typed into the browser of any device on the same network, provides the graphical user interface for the control of the lock. The ESP triggers its pin and the Arduino controls the Linear Actuator accordingly.
<img src="{{site.baseurl}}/assets/images/blog/Wifi-controlled-lock/1.png" alt="Resistor" width=auto height=auto>

<div>{%- include extensions/youtube.html id='1R6iNJImTr0' -%}</div>
