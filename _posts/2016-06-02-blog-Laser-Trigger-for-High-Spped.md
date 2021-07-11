---
title: Laser Trigger for High Speed Photography
tags: [arduino,laser,photography,ldr,camera,NPN]
layout: article
mode: normal
type: article
sharing: true
author: Ankur Maheshwari
show_author_profile: true
show_title: true
full_width: false
header: true
cover: /assets/images/blog/thumbnails/Laser Trigger for High Speed Photography.png
---

## Aim
Capturing moment that whiz past your naked eyes by setting a laser to trigger a camera via Arduino .
<!--more-->

## Hardware used
- Arduino 
- 3.3V LASER 
- Light Dependent Resistor 
- NPN Transistor 
- Camera/Flash

## Details
The camera was setup on BULB mode (the sensor would remain open till the shutter wasn’t pressed again) and all the lights of the room were switched off. Since it was a dark room only the light of the flash would be visible on the final image. Hence, the flashes (2) were fired by the laser trigger not the camera. Camera shutter was manually set.  A speaker was put between the laser and LDR. Black plastic was put over the speaker and little drops of paint were put using a syringe. The paint drops would fly once the music was turned on. The flying paint would obstruct the laser beam and flashes would be fired. Then the camera shutter was closed..

## Schematic
<img src="{{site.baseurl}}/assets/images/blog/Laser-trigger-high-speed-photo/schematic.png" alt="Resistor" width=auto height=auto>


<div class="swiper swiper-demo">
  <div class="swiper__wrapper">
    <div class="swiper__slide"><img class="image image" src="{{site.baseurl}}/assets/images/blog/Laser-trigger-high-speed-photo/1.png"/></div>
    <div class="swiper__slide"><img class="image image" src="{{site.baseurl}}/assets/images/blog/Laser-trigger-high-speed-photo/2.png"/></div>
    <div class="swiper__slide"><img class="image image" src="{{site.baseurl}}/assets/images/blog/Laser-trigger-high-speed-photo/3.png"/></div>
    <div class="swiper__slide"><img class="image image" src="{{site.baseurl}}/assets/images/blog/Laser-trigger-high-speed-photo/4.png"/></div>
    <div class="swiper__slide"><img class="image image" src="{{site.baseurl}}/assets/images/blog/Laser-trigger-high-speed-photo/5.png"/></div>
    <div class="swiper__slide"><img class="image image" src="{{site.baseurl}}/assets/images/blog/Laser-trigger-high-speed-photo/6.png"/></div>
    <div class="swiper__slide"><img class="image image" src="{{site.baseurl}}/assets/images/blog/thumbnails/Laser Trigger for High Speed Photography.png"/></div>
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
