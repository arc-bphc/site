---
title: Arduino based Seismograph
tags: [op-amp,arduino,magnets]
layout: article
mode: normal
type: article
sharing: true
author: Shivam Bhagat
show_author_profile: true
show_title: true
full_width: false
header: true
cover: /assets/images/blog/thumbnails/Arduino based Seismograph.png
---

## Aim 
To make a seismograph that detects vibrations of ground and plots a graph accordingly.
<!--more-->

## Hardware used
- Arduino Uno
- Operational Amplifier
- Magnet wire(copper)
- Neodymium magnets
- Springs and metal rods

## Details
The project is based upon a fundamental principle of physics: Faradays’s law of electromagnetic induction. The design consists of two metal bars with magnets attached at their ends and held stationary using springs. The bars are positioned such that the magnet hangs close to the coil. The mechanical design is such that when ground shakes, magnet moves with respect to coils, thereby inducing an alternating EMF. This EMF is then recorded and a time graph is plotted accordingly.

<div class="swiper swiper-demo">
  <div class="swiper__wrapper">
    <div class="swiper__slide"><img class="image image" src="{{site.baseurl}}/assets/images/blog/thumbnails/Arduino based Seismograph.png"/></div>
    <div class="swiper__slide"><img class="image image" src="{{site.baseurl}}/assets/images/blog/Seismograph/1.png"/></div>
    <div class="swiper__slide"><img class="image image" src="{{site.baseurl}}/assets/images/blog/Seismograph/2.png"/></div>
    <div class="swiper__slide"><img class="image image" src="{{site.baseurl}}/assets/images/blog/Seismograph/2.png"/></div>
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


<div>{%- include extensions/youtube.html id='aRBLiYrYQns' -%}</div>


Multiple Authors: Shivam Bhagat (2015 Batch) & Murtaza Bohra (2015 Batch)
{:.info}