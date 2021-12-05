---
title: POV Wand
tags: [arduino, POV, LED]
layout: article
mode: normal
type: article
sharing: true
author: Bhavya Jain
show_author_profile: true
show_title: true
full_width: false
header: true
cover: /assets/images/blog/thumbnails/POV Wand.png
---

## Aim
Making a Presistence of Vision Wand
<!--more-->
## Story
# POV Wand

## About this project

POV (Persistence of Vision) is a kind of optical illusion in which a visual image seems to persist even when the light from it ceases to enter our eyes. This can be used to make POV displays where we can display text, images, gifs, etc.

<div class="swiper swiper-demo">
  <div class="swiper__wrapper">
    <div class="swiper__slide"><img class="image image" src="{{site.baseurl}}/assets/images/blog/POV-Wand/o1.png"/></div>
    <div class="swiper__slide"><img class="image image" src="{{site.baseurl}}/assets/images/blog/POV-Wand/o2.png"/></div>
    <div class="swiper__slide"><img class="image image" src="{{site.baseurl}}/assets/images/blog/POV-Wand/o3.png"/></div>
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


## Components and tools

1.  (1x) Arduino Uno
2.  (20x) Red LEDs
3.  (20x) 220 $\Omega$ Resistors
4.  (1x) Perf Board
5.  (1x) Toggle Switch
6.  M-M and M-F jumper wires

### Tools

1.  Soldering iron

## Construction

1.  Take a perf board and cut it to the required size for 20 LEDs.
    
2.  Solder the LEDs in a single line with all Anode on the same side.
    
3.  Attach 220 $\Omega$ resistors beside each LED and solder them.
    
4.  Add toggle switch to turn on the display whenever the the switch is turned on.
    
5.  Solder wires to anode of each LED and common Gnd.
    
   <img src="{{site.baseurl}}/assets/images/blog/POV-Wand/1.png" alt="1" width=auto height=auto>
6.  Make the connections, connect wires to Arduino in the following manner.
    Pin connections:
    Top of wand
    1 -----> Digital Pin 13
    
    2 -----> Digital Pin 12
    
    3 -----> Digital Pin 11
    
    4 -----> Digital Pin 10
    
    5 -----> Digital Pin 9
    
    6 -----> Digital Pin 8
    
    7 -----> Digital Pin 7
    
    8 -----> Digital Pin 6
    
    9 -----> Digital Pin 5
    
    10 -----> Digital Pin 4
    
    11 -----> Digital Pin 3
    
    12 -----> Digital Pin 2
    
    13 -----> Digital Pin 1
    
    14 -----> Digital Pin 0
    
    15 -----> Analog Pin A5
    
    16 -----> Analog Pin A4
    
    17 -----> Analog Pin A3
    
    18 -----> Analog Pin A2
    
    19 -----> Analog Pin A1
    
    20 -----> Analog Pin 0
    
    Bottom of wand
    
7.  Upload the code and you are good to go.
    

<img src="{{site.baseurl}}/assets/images/blog/POV-Wand/2.png" alt="2" width=auto height=auto>

<img src="{{site.baseurl}}/assets/images/blog/POV-Wand/3.png" alt="3" width=auto height=auto>

## Code

The complete code can be found on [github]( https://github.com/jainbhavya832/POV_Wand)

<div>{%- include extensions/youtube.html id='aroFEp9cHeM' -%}</div>
