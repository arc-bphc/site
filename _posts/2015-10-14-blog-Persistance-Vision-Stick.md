---
title: Persistence of Vision Stick
tags: [POV,led,SIPO registers,]
layout: article
mode: normal
type: article
sharing: true
author: Rohan Dvivedi
show_author_profile: true
show_title: true
full_width: false
header: true
cover: /assets/images/blog/thumbnails/Persistence of Vision Stick.png
---

## Aim
To make a POV Display.
<!--more-->
## Hardware Used
- 8 – Green Colored LEDs.
- 1 – Serial in- Parallel out shift register.
- 1 – Digital InfraRed Sensor.
- 1 – Motor (rpm = 1000).
- 1 – On-board 5v power supply.
- 1 – Arduino

## Working
The LED to be glown in a frame was sent as data using SPI comm protocol
using slave select pin as the latch, and utilizing only MOSI.
IR sensor was used to detect the position of completion of one revolution.
By changing the delay ‘d’ in given code the width of characters can be changed.
Current Status:- Completed.

<div class="swiper swiper-demo">
  <div class="swiper__wrapper">
    <div class="swiper__slide"><img class="image image" src="{{site.baseurl}}/assets/images/blog/Persistence-Vision-Stick/1.png"/></div>
    <div class="swiper__slide"><img class="image image" src="{{site.baseurl}}/assets/images/blog/Persistence-Vision-Stick/2.png"/></div>
    <div class="swiper__slide"><img class="image image" src="{{site.baseurl}}/assets/images/blog/Persistence-Vision-Stick/3.png"/></div>
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

<div>{%- include extensions/youtube.html id='thcln1SD9bk' -%}</div>


Multiple Authors: Rohan V Dvivedi, Kativarpu Parthiv, Sri Harsha Grandhi, Anurag Anand, Kativarpu Parthiv, Anurag Anand and Parakh M Gupta.
{:.info}