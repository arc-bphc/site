---
title: Automatically Opening Dustbin
tags: [hcsr04,arduino,servo,automation]
layout: article
mode: normal
type: article
sharing: true
author: Yashdeep Thorat
show_author_profile: true
show_title: true
full_width: false
header: true
cover: /assets/images/blog/thumbnails/automatic-dustbin.png
---
## Aim
To make a dustbin that will open when you hover your hand over it.
<!--more-->

## Requirements
- Arduino Uno
- HC-SR04 Ultrasound Sensor
- Servo motor (operating voltage: 6V DC , torque: 3.5 Kg.cm)
- Battery (12V 3AH)
- Jumper Cables
- A foot pedal Dustbin
- Breadboard
 

## Details
The ultrasound sensor is connected to the front of the dustbin and the servo is attached to a lever in the back which is a part of the foot pedal mechanism. A code is uploaded into the arduino which is used to accept inputs from the ultrasound sensor and direct the movements of the servo. The arduino is powered by the battery.
<div class="swiper swiper-demo">
  <div class="swiper__wrapper">
    <div class="swiper__slide"><img class="image image" src="{{site.baseurl}}/assets/images/blog/thumbnails/automatic-dustbin.png"/></div>
    <div class="swiper__slide"><img class="image image" src="{{site.baseurl}}/assets/images/blog/Automatic-Dustbin/1.png"/></div>
    <div class="swiper__slide"><img class="image image" src="{{site.baseurl}}/assets/images/blog/Automatic-Dustbin/2.png"/></div>
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

Hence the dustbin is opened using the servo when an object hovers over it and is similarly closed when the object is removed.

<div>{%- include extensions/youtube.html id='IHb7ubgyXPU' -%}</div>

