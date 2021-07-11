---
title: Robotic Drawing Arm
tags: [drawing,arm,servo]
layout: article
mode: normal
type: article
sharing: true
author: Rohan Dvivedi
show_author_profile: true
show_title: true
full_width: false
header: true
cover: /assets/images/blog/thumbnails/Robotic Drawing Arm.png
---
## Aim
To make a Robotic Drawing Arm that mimics the motion of a finger on touchpad or a mouse.
<!--more-->

## Hardware used
- 2 – 5 kg-cm torque servos
- 1 – Micro Servo
- 1 – 31 cm * 3 cm corrugated plastic sheet
- 1 – 31 cm * 8 cm corrugated plastic sheet
- 2 – Regular sized castor wheel for support
- 1 – Arduino board
- 1 – External 5v power supply

## Details
The Structure of this Draw-arm is similar to the arm of a person posed for drawing/writing things up. A laptop was used for most of the processing and the Arduino was only used to control the servo motors. A Cpp code took the mouse co-ordinates as input and scaled them to the 31cm * 40cm drawing board. The scaled input was then used to change the angles of the servo motors to reach the particular point in the drawing board. This information of the angle of the servo motor was relayed to the Arduino using serial communication over USB.

<div class="swiper swiper-demo">
  <div class="swiper__wrapper">
    <div class="swiper__slide"><img class="image image" src="{{site.baseurl}}/assets/images/blog/Robotic-Drawing-Arm/1.png"/></div>
    <div class="swiper__slide"><img class="image image" src="{{site.baseurl}}/assets/images/blog/Robotic-Drawing-Arm/2.png"/></div>
    <div class="swiper__slide"><img class="image image" src="{{site.baseurl}}/assets/images/blog/Robotic-Drawing-Arm/3.png"/></div>
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

<div>{%- include extensions/youtube.html id='HpxBxgD3gcE' -%}</div>



Multiple Authors: Rohan Dvivedi(2014 Batch) and Kativarpu Parthiv(2014 Batch)
{:.info}