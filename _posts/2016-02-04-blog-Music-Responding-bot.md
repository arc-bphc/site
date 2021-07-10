---
title: Music Responding Bot
tags: [l293d,arduino,analog sound sensor,music]
layout: article
mode: normal
type: article
sharing: true
author: P.V.Nikhilanj
show_author_profile: true
show_title: true
full_width: false
header: true
cover: /assets/images/blog/thumbnails/Music Responding Bot.png
---

## Aim
To make an autonomous robot which can respond to sound/claps.
<!--more-->

## Hardware used
-   1 – Arduino Uno
-   2 – Analog sound sensors (one on each side of the bot).
-   2 – 100 rpm geared motors.
-   1 – L293D H-bridge motor driver.
-   1– Regular sized castor wheel for support.
-   1 – External 9v power supply for Arduino as well as motors.

## Details
The bot works on the fact that when sound is in a certain direction, the sensor closer to it measures a higher change in value (of amplitude/intensity) than the sensor away from it due to sound attenuation i.e. if the sound is to the right of the bot, the right sensor detects a higher change in sound intensity than the left sensor. Hence it moves to the right according to the code.


<div>{%- include extensions/youtube.html id='QmcCbVV7kX8' -%}</div>


