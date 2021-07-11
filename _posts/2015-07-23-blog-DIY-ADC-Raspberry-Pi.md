---
title: DIY ADC for Raspberry Pi
tags: [adc,raspberry pi,cd4051,555 timer]
layout: article
mode: normal
type: article
sharing: true
author: Suyash Yeotikar
show_author_profile: true
show_title: true
full_width: false
header: true
cover: /assets/images/blog/thumbnails/DIY ADC for Raspberry Pi.png
---

## Aim
To Build a cheap ADC for Raspberry Pi.
<!--more-->

## Details
Raspberry Pi does not have an in-built ADC and but it needs one for sure. It is tough finding MCP3008 or ADS series ICs which are costlier and easier to use (they have an SPI or I2C integrated). This is how he found his new way to solve out the problem, which many of you may face while dealing with Raspberry Pi.

## Hardware Used 
ADC0808 or ADC0809 (8 bit analog to parallel digital converter )
CD4051 (3 to 8 multiplexer/demultiplexer)
555 timer ICs.
Resistor and Capacitors for clock.
Pull down resistors of higher value.

## Technical details
Here the ADC0809 IC is kept at a stable input of 0, 0, 0 to pins a, b, c to read ADC pin no 0 (it can be kept altering also and controlled by processor as per the need).The ADC needs a clock to read the Analog input pin and then store in a parallel out register. Here, in the project, a 1Khz clock from a 555 timer IC has been used.
NOTE : Clock frequency can not be increased over 6 MHz as this hampers the raspberry pi digital pins.

You can find out values of resistors and capacitors used for clock, from online 555 timer calculator, he used a tutorial for his [clock.](http://www.eng.buffalo.edu/shaw/student/m1_safety/01_home/ksb/ksb3/old_ksb3_timer.htm)

The parallel data out from ADC0809 is then read by the processor bit by bit starting from the LSB to MSB and a code verifies the value of Analog read and returns an integer between 0 to 255(we used an 8 bit ADC).
Essentially on purpose the code has been reduced to a library for C++ language.

### To make a library:

store the source file under `~/analogread/src/analogread.cpp`
store the header file under `~/analogread/inc/analogread.h`
also use
`mkdir ~/analogread/obj ~/analogread/lib`

then compile your obj code
`g++ ~/analogread/src/analogread.cpp -o ~/analogread/obj/analogread.o -lwiringPi`

then make a static lib as
`ar rcs ~/analogread/lib/analogread.a ~/analogread/obj/analogread.o`

now your lib is ready
it has 2 methods for the object type analogread.

- void setabcr(int a,int b,int c,int r)
as in picture shown a,b,c,r are the I/O pins that are connected.
- read(void)
returns an integer corresponding to the reading.

### Attachments

1 [Header](https://technopediabphc.files.wordpress.com/2015/07/header.docx)
2 [Source](https://technopediabphc.files.wordpress.com/2015/07/source.docx)


<div class="swiper swiper-demo">
  <div class="swiper__wrapper">
    <div class="swiper__slide"><img class="image image" src="{{site.baseurl}}/assets/images/blog/DIY-ADC-Raspi/pinout.png"/></div>
    <div class="swiper__slide"><img class="image image" src="{{site.baseurl}}/assets/images/blog/DIY-ADC-Raspi/PCB.png"/></div>
    <div class="swiper__slide"><img class="image image" src="{{site.baseurl}}/assets/images/blog/DIY-ADC-Raspi/exp.png"/></div>
    <div class="swiper__slide"><img class="image image" src="{{site.baseurl}}/assets/images/blog/DIY-ADC-Raspi/ADC.png"/></div>
  </div>
  <div class="swiper__button swiper__button--prev fas fa-chevron-left"></div>
  <div class="swiper__button swiper__button--next fas fa-chevron-right"></div>
</div>

<style>
.swiper-demo {
  height: auto;
}
</style>
<script>
{%- include scripts/lib/swiper.js -%}
var SOURCES = window.TEXT_VARIABLES.sources;
window.Lazyload.js(SOURCES.jquery, function() {
  $('.swiper-demo').swiper();
});
</script>