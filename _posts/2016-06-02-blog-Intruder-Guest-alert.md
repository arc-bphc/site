---
title: Intruder-Guest alert system
tags: [webcam,OpenCV,Image Processing]
layout: article
mode: normal
type: article
sharing: true
author: Surya Teja Chadella
show_author_profile: true
show_title: true
full_width: false
header: true
cover: /assets/images/blog/thumbnails/Intruder-Guest alert system.png
---

## Aim
To build your own “Intruder Alert System”  with following capabilities:
1. Recognising people who enter your room in a real-time video recording.
2. Notifies you and your friends/neighbours on social media if some one entered your room without your permission.
<!--more-->
<img src="{{site.baseurl}}/assets/images/blog/thumbnails/Intruder-Guest alert system.png" alt="Resistor" width=auto height=auto>


## Hardware used
1. A laptop/desktop with built-in camera or a USB-camera.
2. Your system running on Ubuntu is preferred. You can manage with windows but, installing all the programs required, on windows machine is a bit difficult.

## Software used
1. As we are coding in python, you need to install python on your machine.
2. You need to install OpenCV bindings for Python, so that we can tackle with computer vision stuff.
3. And lastly, some Python modules like ‘requests’, which we will be using to post a status update on social media to notify you and your friends.

## Technical details
For building this system I have used my Laptop running on Ubuntu OS. I used Sublime text 3 for writing the code. I build this system in Python language using OpenCV to tackle with Computer vision problem.

You can find the whole code used in this tutorial at my GitHub repository [here](https://github.com/SnShine/FaceRecognizer).
<img src="{{site.baseurl}}/assets/images/blog/Intruder-Guest-alert/1.png" alt="Resistor" width=auto height=auto>

## Setting up the system
1. Position your camera (USB/ built-in) pointing towards the main door and start the program. The program starts recording the video and analyses it to detect any humans in real-time.
2. When some one enters your room it detects that person and checks with our database to recognize him/her.
3. It notifies you/your friends by posting a status on social media.

<div>{%- include extensions/youtube.html id='1SnUQQRJDI8' -%}</div>
