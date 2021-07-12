---
title: Badminton Playing Bot - ROBOCON 2015
tags: [badminton,pneumatics,mecanum,robocon]
layout: article
#mode: normal
#type: article
sharing: true
author: Jayanth Kanikpati
show_author_profile: true
show_title: true
#full_width: false
header: true
#cover: /assets/images/blog/thumbnails/Badminton Playing Bot - ROBOCON 2015.png
---
## Aim
The bot was made to play Badminton in the ROBOCON 2015 as part of the theme, declared by Televisi Republik Indonesia (TVRI) as, “Robominton: Badminton Robo-Game”.
<!--more-->

## Team
1. Jayanth Kanikpati(Team Lead)
2. Mayank Shekhar
3. Moloy Das
4. Parth Gupta
5. Rishabh Gupta
6. Sanket Rout
7. Gundu Durgarao
8. Sonitabh Yadav
9. Viraj Panwar
10. Anirudh Shankar
11. Chandan Bothra
12. Deepak Upadhyay
13. Dikshant Patel
14. Goutham Varanasi
15. Vikas AG
16. Sidharth Sai
17. Sujeath Pareddy
18. Aayush Khandelwal
19. Akshaya Agarwal
20. Aman Nidhi
21. Animesh Agarwal
22. Suraj Partani


## Details
There were two Bots actually and were meant to play badminton’s doubles game. The highlight of this game were how the two robots hit and hit back shuttle by collaborating each other.The National ABU Robocon 2015 took place in the Badminton Hall of the Shree Shiv Chhatrapati Sports Complex, Balewadi, Pune on 7 March 2015.

BITS Pilani, Hyderabad campus participated first time in the competition with team leader Jayanth Kankipati and the faculty advisor YVD Rao sir. The team was sponsored by India Bank.Overall it was a good and a new experience. Both of our bots were working good, but we couldn’t win it.

## Technical details
The bot used 85 watt motors with Mecanum wheels powered by Motors and 2 lead acid batteries. The motors were operated at 24 volt. Several Servo Motors were used for the arm Mechanism and for hitting Pneumatics were used at 6 bar pressure.The gas was packed in PET containers. The bot was controlled by dummy arm Mechanism.
The other bot had everything same except the wheels it used Omni wheels.



<!-- <div class="w3-content w3-display-container">
  <img class="mySlides1" src="/site/assets/images/blog/thumbnails/Badminton Playing Bot - ROBOCON 2015.png" style="width:100%">
  <img class="mySlides1" src="/site/assets/images/blog/Badminton-Playing-Bot/field.png" style="width:100%">
  <img class="mySlides1" src="/site/assets/images/blog/Badminton-Playing-Bot/room.png" style="width:100%">
  <img class="mySlides1" src="/site/assets/images/blog/Badminton-Playing-Bot/workshop1.png" style="width:100%">
  <img class="mySlides1" src="/site/assets/images/blog/Badminton-Playing-Bot/workshop2.png" style="width:100%">
  <button class="w3-button w3-black w3-display-left" onclick="plusDivs(-1, 0)">&#10094;</button>
  <button class="w3-button w3-black w3-display-right" onclick="plusDivs(1, 0)">&#10095;</button>
</div>

<script>
var slideIndex = [1,1];
var slideId = ["mySlides1"]
showDivs(1, 0);
showDivs(1, 1);

function plusDivs(n, no) {
  showDivs(slideIndex[no] += n, no);
}

function showDivs(n, no) {
  var i;
  var x = document.getElementsByClassName(slideId[no]);
  if (n > x.length) {slideIndex[no] = 1}
  if (n < 1) {slideIndex[no] = x.length}
  for (i = 0; i < x.length; i++) {
    x[i].style.display = "none";  
  }
  x[slideIndex[no]-1].style.display = "block";  
}
</script>  -->

<div class="swiper swiper-demo">
  <div class="swiper__wrapper">
    <div class="swiper__slide">
    <img  src="/site/assets/images/blog/thumbnails/Badminton Playing Bot - ROBOCON 2015.png">
    </div>
    <div class="swiper__slide">
    <img  src="/site/assets/images/blog/Badminton-Playing-Bot/field.png">
    </div>
    <div class="swiper__slide">
    <img  src="/site/assets/images/blog/Badminton-Playing-Bot/workshop2.png">
    </div>
    <div class="swiper__slide">
    <img  src="/site/assets/images/blog/Badminton-Playing-Bot/room.png">
    </div>
    <div class="swiper__slide">
      <img  src="/site/assets/images/blog/Badminton-Playing-Bot/workshop1.png">
    </div>
  </div>
  <div class="swiper__button swiper__button--prev fas fa-chevron-left"></div>
  <div class="swiper__button swiper__button--next fas fa-chevron-right"></div>
</div>

<style>
  img {
  width: 400px;
  height: 600px;
  object-fit: contain;
}
</style>
 
<script>
{%- include scripts/lib/swiper.js -%}
var SOURCES = window.TEXT_VARIABLES.sources;
window.Lazyload.js(SOURCES.jquery, function() {
  $('.swiper-demo').swiper();
});
</script>