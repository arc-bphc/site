---
title: Thread Counting Using Image Processing
tags: [raspberry pi,Image Processing,webcam,OpenCV]
layout: article
mode: normal
type: article
sharing: true
author: Eda John
show_author_profile: true
show_title: true
full_width: false
header: true
cover: /assets/images/blog/thumbnails/Thread Counting Using Image Processing.png
---

## Aim
The main aim is to count the number of threads using image processing as the camera keeps moving. It is to be noted that the processing of image is done till approximately half of the image actual width since the camera is moving, the number of thread count keeps getting updated.
<!--more-->
## Details
The project was taken as an initiative for milling factory to detect wherever thread is cut loose due to high string tension.

## Hardware
- Raspberry pi
- Webcam
- 4 lasers (low intensity) for pinpointing from where to where the image is to be processed  mobile power bank with 1.5 A steady output
- 8GB SD card for storage memory.

## Software
The software involved was OpenCV 2.4.11, visual studio (for simulation on computer) and Raspberry pi GUC viewer.

## Advice from Makers
OpenCV is much better than almost all other visual processing softwares as it is not only available for simulation on computers but also for Android phones in the form of OpenCV SDK. The only problem we could probably face is the failure of initiation of functions as mentioned in OpenCV 2.4.11 documentation for which other source like stack overflow come into play. Having a microprocessor such as raspberry pi as an interface between software and hardware is really advised.

<div class="swiper swiper-demo">
  <div class="swiper__wrapper">
    <div class="swiper__slide"><img class="image image" src="{{site.baseurl}}/assets/images/blog/Thread-Counting/1.png"/></div>
    <div class="swiper__slide"><img class="image image" src="{{site.baseurl}}/assets/images/blog/Thread-Counting/2.png"/></div>
    <div class="swiper__slide"><img class="image image" src="{{site.baseurl}}/assets/images/blog/Thread-Counting/3.png"/></div>
    <div class="swiper__slide"><img class="image image" src="{{site.baseurl}}/assets/images/blog/Thread-Counting/4.png"/></div>
    <div class="swiper__slide"><img class="image image" src="{{site.baseurl}}/assets/images/blog/Thread-Counting/5.png"/></div>
    <div class="swiper__slide"><img class="image image" src="{{site.baseurl}}/assets/images/blog/Thread-Counting/6.png"/></div>
    <div class="swiper__slide"><img class="image image" src="{{site.baseurl}}/assets/images/blog/Thread-Counting/8.png"/></div>
    <div class="swiper__slide"><img class="image image" src="{{site.baseurl}}/assets/images/blog/Thread-Counting/9.png"/></div>
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

Multiple Authors: Eda John and Eda Amos William(2014 Batch).
{:.info}