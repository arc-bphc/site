---
title: Clap Responding Bot
tags: [arduino,lm358,analog sound,clap]
layout: article
mode: normal
type: article
sharing: true
author: Hitesh Bhagchandani
show_author_profile: true
show_title: true
full_width: false
header: true
cover: /assets/images/blog/thumbnails/Clap Responding Bot.png
---
## Aim
To make a robot that responds and moves in the direction of clap sounds.
<!--more-->

## Hardware used 
-   1-Arduino Uno.
-   3-Analog sound sensors.
-   2-60 rpm geared motors.
-   1-LM358 motor driver.
-   1 – External 9v power supply.

## Details
The bot works on the fact that when sound is in a certain direction, the sensor closer to it measures a higher change in value than the sensor away from it due to sound attenuation.This bot uses three Analog sound sensors in front,right and left of the bot to record the clap sounds. Turns 90 degrees in the direction of the clap and 45 degrees if the claps come from a direction in between the cardinal directions.

<div>{%- include extensions/youtube.html id='zXLneInnu6I' -%}</div>


