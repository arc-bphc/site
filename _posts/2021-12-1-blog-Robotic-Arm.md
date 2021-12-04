---
title: Robotic Arm
tags: [arduino,Servo,PWM]
layout: article
mode: normal
type: article
sharing: true
author: Shashank Raghav, Pavan Kalyan, Swetha Krishna, Vibhum Raj
show_author_profile: false
show_title: true
full_width: false
header: true
cover: /assets/images/blog/thumbnails/Servo Motors PWM.png
---

# Robotic Arm
## A Brief Overview.
We worked on building a **Mechanical Manipulator[M.M.]**, i.e. a Robotic Arm, with 3 Degrees of Freedom. We tried to control the arm with a Bluetooth module. To achieve our goal we used 3 servos.
***
### Degrees of Freedom.
In **Mechanical Manipulators[M.M.]**, **Degrees of Freedom** typically refers to the joints in the arm. They represent the axes of rotation in the arm. These **joints** allow us to control the arm. These joints usually have some kind of **actuators** which enable the  **M.M.** to move. We used **servos** to achieve this task.

***
### MG995s
**MG995s** is the servo model which we have utilized. 
Its specifications are as follows :
• Weight: 55 g
• Dimension: 40.7 x 19.7 x 42.9 mm approx.
• Stall torque: 8.5 kgf·cm (4.8 V ), 10 kgf·cm (6 V)
• Operating speed: 0.2 s/60º (4.8 V), 0.16 s/60º (6 V)
• Operating voltage: 4.8 V a 7.2 V
• Dead band width: 5 µs
• Stable and shock proof double ball bearing design
• Temperature range: 0 ºC – 55 ºC


<img src="{{site.baseurl}}/assets/images/blog/Robotic-Arm/1.png" alt="Resistor" width=auto height=auto>

<img src="{{site.baseurl}}/assets/images/blog/Robotic-Arm/2.png" alt="Resistor" width=auto height=auto>

***
### Connecting Linkers
**Linkers** are the connecting rods - which are typically rectangular - that are placed between two joints. These linkers constitute a major part of the **" M.M."**. We 3D printed the linkers and we connected them together at the joints in the following way:

<img src="{{site.baseurl}}/assets/images/blog/Robotic-Arm/3.png" alt="Resistor" width=auto height=auto>


***

### Power Supply and the Final Circuit
The 3 servos were powered using a SMPS. A Switch Mode Power Supply (SMPS) is a power supply which can provide a fixed voltage and current upto a maximum value pertaining to that voltage.
We used the 5V mode of the SMPS.
The positive of the SMPS was connected to the 3 servos via a common positive, same with the negative terminal. The input pin of motor was connected to PWM pins. 
The arduino board was also powered from the same positive. 




### HC05 Bluetooth Module

HC-05 is a Bluetooth device used for wireless communication with Bluetooth enabled devices, like smartphones. It communicates with microcontrollers using serial communication (USART).

This module enables communication between the arduino uno and the custom-built android app. Information from the app is transmitted to the uno and thus to the arm's servos. It uses the 2.45GHz frequency band. The transfer rate of the data can vary up to 1Mbps and is in range of 10 meters. It operates within the 4-6V power supply range.

Here, the app gives a number between 0 and 180 to be sent to a given servo (number is based on the position of the slider). This is then transmitted to the module as serial data and thus to the uno. This information is used to operate the servo accordingly using servo.write().


<img src="{{site.baseurl}}/assets/images/blog/Robotic-Arm/4.png" alt="Resistor" width=auto height=auto>

<img src="{{site.baseurl}}/assets/images/blog/Robotic-Arm/5.png" alt="Resistor" width=auto height=auto>


Pin Description:

- Enable - This pin is used to set the mode: Data Mode or AT command mode (set high).
- VCC - This is connected to the +5V power supply.
- Ground - Connected to ground of powering system.
- Tx (Transmitter) - This pin transmits the received data Serially.
- Rx (Receiver) - Used for broadcasting data serially over bluetooth.
- State -Used to check if the bluetooth is working properly.

### Code

```c++

#include<Servo.h>
#include<SoftwareSerial.h>
Servo servo1;
Servo servo2;
Servo servo3;

int servo1_angle;
int servo2_angle;
int servo3_angle;
int x=2;
int y=120;
int z=2;

void setup() {
  // put your setup code here, to run once:
  Serial.begin(9600);
  servo1.attach(9);
  servo2.attach(10);
  servo3.attach(11);
  pinMode(13,OUTPUT);
  servo1.write(x);
  servo3.write(y);
  servo2.write(z);
}


void loop() {
  while(Serial.available()>0){
    char input = Serial.read();
    
    if(input=='F'){
      if (x >= 2 && x < 178)
      {
        x=x+1;
        servo1.write(x);
      }
    }
    if(input=='B'){
      if (x >= 2 && x < 178)
      {
        x=x-1;
        servo1.write(x);
      }
    }

    if(input=='L'){
      if (y >= 2 && y < 178)
      {
        y=y+1;
        servo2.write(y);
      }
    }
    if(input=='R'){
      if (y >= 2 && y < 178)
      {
        y=y-1;
        servo2.write(y);
      }
    }

    if(input=='G'){
      if (z >= 2 && z < 178)
      {
        z=z+1;
        servo3.write(z);
      }
    }
    if(input=='I'){
      if (z >= 2 && z < 178)
      {
        z=z-1;
        servo3.write(z);
      }
    }
  }
}
```

Given above is the code used for the project. As we can see the 3 degrees of freedom of the arm are controlled using 3 independent servos. Information is received via the Bluetooth Module - a number that indicates the degree of rotation or movement required (on a scale of 2 to 178-based on the slider in the app) is received and the required servo is activated accordingly using servo.write(). The two directional movements possible for each servo is coded (2 functions for each servo). Each slider in the app is meant for a particular servo's movement.

### Demonstration
This is a demonstration of the working of the arm, done at the expo.

