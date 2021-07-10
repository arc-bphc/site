---
title: Ball Picker Robot 
tags: [arduino,hc05,bluetooth,servo,l298n,mechanix]
layout: article
mode: normal
type: article
sharing: true
author: Murtaza Bohra
show_author_profile: true
show_title: true
full_width: false
header: true
cover: /assets/images/blog/thumbnails/Ball Picker Robot.png
---
## Aim
To build a manually controlled Robot which can pick and drop (at desired location) Table Tennis balls.
<!--more-->

## Hardware Used
- Arduino Nano.
- breadboard.
- 12V battery supply.
- 4-wheel chassis.
- Buck Convertor
- 100 rpm motors and wheels.
- castor wheel
- HC-05 bluetooth module.
- Micro servo
- MG995(Metal gear servo)
- L298 Motor Driver IC
- Mechanix Kit.

## Software used
Arduino IDE (you have to install CH-340 driver for  arduino nano) & control Joy stick app (available on play store) for Bluetooth Module.

## Working 
The working of the bot is simple it picks up the ball and place/drop the ball at desired location. Full mechanical design of the Bot is made using Mechanix Spares.

To lift the arm Four-Bar mechanism is used and bot is controlled via bluetooth.
<div class="swiper swiper-demo">
  <div class="swiper__wrapper">
    <div class="swiper__slide"><img class="image image" src="{{site.baseurl}}/assets/images/blog/Ball-Picker-Robot/1.png"/></div>
    <div class="swiper__slide"><img class="image image" src="{{site.baseurl}}/assets/images/blog/Ball-Picker-Robot/2.png"/></div>
    <div class="swiper__slide"><img class="image image" src="{{site.baseurl}}/assets/images/blog/thumbnails/Ball Picker Robot.png"/></div>
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


Multiple Authors: Murtaza Bohra(2015 batch), Prerit Agarwal(2015 batch) & Ebin Philip(2014 batch)
{:.info}


