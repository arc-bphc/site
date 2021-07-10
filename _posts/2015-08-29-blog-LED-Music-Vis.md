---
title: LED Music Visualizer 
tags: [lm324,74hc595,arduino,music]
layout: article
mode: normal
type: article
sharing: true
author: Rohan Dvivedi
show_author_profile: true
show_title: true
full_width: false
header: true
cover: /assets/images/blog/LED-Music-Vis/led.png
---

## Aim
To make a LED Music Visualizer for Demonstration in ATMOS’14 Techtainment Event.
<!--more-->
## Hardware involved
1. LM324 – Op-Amp.
2. 74HC595 – 8 bit shift register (74HC164 a cheaper can also be used) X 8.
3. An Arduino.
4. And a couple of Capacitors and Resistors.

## Technical details
<img src="{{site.baseurl}}/assets/images/blog/LED-Music-Vis/led.png" alt="Resistor" width=auto height=auto>

The 8*8 led matrix reacts by reading the 8 bit analog value from ADC pin of a clone Arduino and the 2-D LED matrix can be made to dance on the beats. There is no frequency distinguishing done on the incoming signal.
An array of 8- 8 bit shift registers were made to make a 64 bit 2-D LED display(8*8). Serial in-parellel out shift registers were used all provided with 500 Hz clock from an Arduino pin through code and serially pushing the data in.
All the registers were provided same data and clock pins and 8 different latch pins.(only one latch pin can be used to control all of the LEDs, but to shift for fast movement of pattern they shifted to 8 different latch pin design.

<img src="{{site.baseurl}}/assets/images/blog/LED-Music-Vis/circuit.png" alt="Resistor" width=auto height=auto>


<div>{%- include extensions/youtube.html id='f7IMDipX1JE' -%}</div>


## Disadvantage or Drawback
Each design had to be encoded to show as a pattern on the Matrix, hence to change the pattern the code had to be changed a lot.


Multiple Authors: Rohan Dvivedi(2014 Batch), Anurag Anand(2014 Batch), Parthiv Kativarpu(2014 Batch), TDSK Sarath and Tejeshwar Reddy.
{:.info}