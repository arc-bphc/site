---
title: Room Cleaning Bot
tags: [arduino,ultrasonic,servo]
layout: article
mode: normal
type: article
sharing: true
author: Automation and Robotics Club
show_author_profile: true
show_title: true
full_width: false
header: true
cover: /assets/images/blog/thumbnails/Room Cleaning Bot.png
---

## Aim
Clean room using a robot.
<!--more-->
## Story
# Room Cleaning Bot
We designed a room-cleaning robot that performs the same function as other store-bought ones, despite being relatively cheaper. It consists of the following core components:

* 1 Arduino UNO,
* 3 HCSR04 ultrasonic sensors,
* 1 L298N motor driver,
* 2 DC motors,
* 1 12V DC fan,
* 1 Li-Po battery.

The bot acts as a collision avoidance robot for the most part, with the three ultrasonic sensors deciding the direction in which it should move.
The fan attached to the bottom of the chassis sucks dust and other forms of dirt into a dust collection pouch located behind.
Both the motors and the fan are operated by the Li-Po battery located on the chassis.

## The Code used in the Bot:

```c++
int trigPinF = 3;      // Trig Pin Of HC-SR04
int echoPinF = 2;// Echo Pin Of HC-SR04
int trigPinR = 7;
int echoPinR = 6;
int trigPinL = 4;
int echoPinL = 5;
int check_right();
int check_left();
int l1 = 10; // Motor Pins
int l2 = 11;
int r1 = 12;
int r2 = 13;
int fr = 0;
int fl = 0;
long durationF, durationR, durationL, distanceF, distanceR, distanceL;

void setup() {
  Serial.begin(9600);
  pinMode(l1, OUTPUT); // Set Motor Pins As O/P
  pinMode(l2, OUTPUT);
  pinMode(r1, OUTPUT);
  pinMode(r2, OUTPUT);
  pinMode(trigPinF, OUTPUT); // Set Trig Pin As O/P To Transmit Waves
  pinMode(echoPinF, INPUT); //Set Echo Pin As I/P To Recieve Reflected Waves
  pinMode(trigPinR, OUTPUT);
  pinMode(echoPinR, INPUT);
  pinMode(trigPinL, OUTPUT);
  pinMode(echoPinL, INPUT);
}

void loop() {

  digitalWrite(trigPinF, LOW);
  delayMicroseconds(2);
  digitalWrite(trigPinF, HIGH); // Transmit Waves For 10us
  delayMicroseconds(10);
  durationF = pulseIn(echoPinF, HIGH); // Recieve Reflected Waves
  distanceF = durationF / 58.2; // Get Distance

  if (distanceF > 20) // Condition For Absence Of Obstacle
  {
    digitalWrite(r2, HIGH); // Move Forward
    digitalWrite(r1, LOW);
    digitalWrite(l2, HIGH);
    digitalWrite(l1, LOW);
    if ((check_right() == 1 && check_left() == 1) || ((check_right() == 0 && check_left() == 0)))
    {
      //Move Forward
    }
    else if (check_right() == 1 && check_left() == 0)
    {
      //Move Left
    }
    else
    {
      //Move Right
    }
  }

  if (distanceF < 20) // Condition For Presence Of Obstacle
  {
    digitalWrite(r2, LOW); //Stop
    digitalWrite(r1, LOW);
    digitalWrite(l2, LOW);
    digitalWrite(l1, LOW);
    if ((check_right() == 1 && check_left() == 1) || ((check_right() == 0 && check_left() == 0)))
    {
      //Move Backward
    }
    else if (check_right() == 1 && check_left() == 0)
    {
      //Move Left
    }
    else
    {
      //Move Right
    }
  }
}

int check_right() {
  digitalWrite(trigPinR, LOW);
  delayMicroseconds(2);
  digitalWrite(trigPinR, HIGH); // Transmit Waves For 10us
  delayMicroseconds(10);
  durationR = pulseIn(echoPinR, HIGH); // Recieve Reflected Waves
  distanceR = durationR / 58.2; // Get Distance
  if (distanceR < 20)
  {
    fr = 1;
  }
  else
    fr = 0;
  return fr;
}

int check_left()
{
  digitalWrite(trigPinL, LOW);
  delayMicroseconds(2);
  digitalWrite(trigPinL, HIGH); // Transmit Waves For 10us
  delayMicroseconds(10);
  durationL = pulseIn(echoPinL, HIGH); // Recieve Reflected Waves
  distanceL = durationL / 58.2; // Get Distancel̥
  if (distanceL < 20)
  {
    fl = 1;
  }
  else
    fl = 0;
  return fl;
}
```

We shall now explain what the various functions in the code do and some essential snippets.

### int check_left() 
This function uses the ultrasonic sensor located on the left side of the bot and calculates the distance from an obstacle on the left. It returns a flag variable based on the distance. If the distance is less than the threshold, it returns 1, otherwise 0.
### int check_right()

This function uses the ultrasonic sensor located on the right side of the bot and calculates the distance from an obstacle on the right. It returns a flag variable based on the distance. If the distance is less than the threshold, it returns 1, otherwise 0.

### void loop()
This is the central part of the code. Here, we'll explain the various snippets and what they do.

```c++
   if (distanceF > 20) // Condition For Absence Of Obstacle
  {
    if ((check_right() == 1 && check_left() == 1) || ((check_right() == 0 && check_left() == 0)))
    {
	 digitalWrite(r2, HIGH); // Move Forward
     digitalWrite(r1, LOW);
     digitalWrite(l2, HIGH);
     digitalWrite(l1, LOW);
    }
    else if (check_right() == 1 && check_left() == 0)
    {
      //Move Left
    }
    else
    {
      //Move Right
    }
   }
if (distanceF < 20) // Condition For Presence Of Obstacle
  {
    digitalWrite(r2, LOW); //Stop
    digitalWrite(r1, LOW);
    digitalWrite(l2, LOW);
    digitalWrite(l1, LOW);
    if ((check_right() == 1 && check_left() == 1) || ((check_right() == 0 && check_left() == 0)))
    {
      //Move Backward
    }
    else if (check_right() == 1 && check_left() == 0)
    {
      //Move Left
    }
    else
    {
      //Move Right
    }
  }
```
This part calculates the distance of an obstacle in the front using the ultrasonic sensor. If the distance is less than a particular threshold, it stops; otherwise, it keeps moving according to the following logic:

1. If **check_right()** and **check_left()** both return **1** or **0** together, i.e., there are obstacles on both the left and right of the bot or neither, it moves **forward**.
2.  If only **check_right()** returns **1**, it means there is an obstacle only on the right side of the bot, and hence it moves to the **left and forward**.
3.   If only **check_left()** returns **1**, it means there is an obstacle only on the left side of the bot, and hence it moves to the **right and forward**.

When it stops, then depending on the flags returned by **check_right()** and **check_left()**, it decides on a course of action as given below.

1. If **check_right()** and **check_left()** both return **1** or **0** together, i.e., there are obstacles on both the left and right of the bot or neither, it moves **backwards**.
2.  If only **check_right()** returns **1**, it means there is an obstacle only on the right side of the bot, and hence it moves to the **left and backwards**.
3.   If only **check_left()** returns **1**, it means there is an obstacle only on the left side of the bot, and hence it moves to the **right and backwards**.

Hence, eventually the bot traverses the entirety of the room and cleans it.

