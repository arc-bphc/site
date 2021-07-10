---
title: Interfacing 62256 SRAM using ATmega32A
tags: [62256 SRM,ATmega32A,AVR]
layout: article
mode: normal
type: article
sharing: true
author: Rohan Dvivedi
show_author_profile: true
show_title: true
full_width: false
header: true
cover: /assets/images/blog/thumbnails/Interfacing 62256 SRAM using ATmega32A.png
---
## Aim
Interfacing of a 32k x 8 bit SRAM chip 62256 with ATmega32A microcontroller.
<!--more-->

## Project Description
A learning oriented project done to just ensure the correctness of the 62256 32k x 8 SRAM chips. It uses ATmega32A microcontroller burned with the “uC-SRAM-interfacing.cpp” using your AVR programmer, after compiling from avr8 gcc compiler.
<img src="{{site.baseurl}}/assets/images/blog/thumbnails/Interfacing 62256 SRAM using ATmega32A.png" alt="Resistor" width=auto height=auto>

Connect the pins of SRAM and uC as shown. Connect your uC to PC by UART-USB communication, he has used PL2303HXA for USB to UART Compile and run the “console-control-for-RAM.cpp” on your desktop/laptop computer. In the Console : “Admin :” is where you type the input command. and “Microcontroller :” is where the uC responds.
<img src="{{site.baseurl}}/assets/images/blog/Interfacing-SRAM/1.png" alt="Resistor" width=auto height=auto>

here on both the sides ‘;’ is the string termination character.

to read the command is: “R-{address in RAM in decimal number};” (without quotes)

to write the command is: “W-{data to be written}-{address where you want to write data};” (without quotes)

Example : to read from address 11322; R-11322;

to write 112 to address 12136; W-112-12136;

Checkout whole code used in this tutorial at his GitHub repository [here](https://github.com/RohanVDvivedi/Interfacing-62256-32Kx8bit-SRAM-using-ATmega32A)


<div>{%- include extensions/youtube.html id='psKOW52DNus' -%}</div>


