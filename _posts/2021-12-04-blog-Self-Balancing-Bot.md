---
title: Self Balancing Bot
tags: [arduino, PID, MPU6050]
layout: article
mode: normal
type: article
sharing: true
author: Automation and Robotics Club
show_author_profile: true
show_title: true
full_width: false
header: true
cover: /assets/images/blog/thumbnails/Self Balancing Bot.png
---

## Aim
Making a robot that balances itself using accelerometer and PID
<!--more-->
## Story

The project aims to make a self balacing robot using Arduino and MPU-6050 IMU. 

## Build:
1. Chassis
The chassis is a standard steel chassis readily available in the market.
2. Motors:
We have used NEMA-17 stepper motors. These motors allow us to have precise control over the angle of rotaton. The motors are driven with a pair of A4988 stepper drivers.
3. Control system:
The controller is an Arduino UNO board which based arounf the ATmega 328 chip. It runs a PID loop which controls the motors. The Arduino board takes in input from the MPU-6050 via I2C communication
4. Power 
The robot is directly powered by a 12V power supply using an AC~DC power supply. The power supply is capable of supplying upto 5A of current which is greater than the total current draw of the motors. 

PID is a form of closed loop control system. A closed loop control system is a system in which we have some form of feedback which allows us to control the plant optimally

The notes are prepared considering the example problem of having to navigate a particle to a specific position.

Functions of PID:
<b>1.  Proportional:</b>
	&emsp;- P is the proportional part. 
	&emsp;- It is used to monitor the actual error. 
	&emsp;- It is also called the instantaneous error. 
<b>2. Integral:</b>
	&emsp;- I is for the total error changed.
	&emsp;- The total error changed should be equal to the initial error.
	&emsp;-  Also called the cummulitive error.
 <b>3. Deriavtive:</b>
	&emsp;-  D is for the rate of change of error.
	&emsp;-  It is used to predict the future error.
	
## PID	
We are using MPU-6050 to get the feedback. The raw data is converted into angular rate. The angular rate is integrated to get the proportional error. It is further integrated to give Integral error.

The setpoint is 0°. Hence as soon as the robot starts tiliting, the error term starts growing. To counter this, the stepper motors are switched on. 

The code for the PID loop id as follows:

//--------PID--------//  
  
  //Proportional
  error = requiredAngle - currentAngle;

  //Integral
  totalError = totalError + error*dt;

  //Derivative
  errorRate = (error - prevError)/dt;
  
  PIDout = kP*error + kI*totalError + kD*errorRate;
  prevError = error;
  prevTime = currentTime;


The PID constants, kP, kD, and kI are tuned manually. The PIDout term gives the output in terms of required angle. This is converted into 
The final output is written to the stepper motors in terms of number of steps.


## MPU-6050
The MPU 6050 is a 6-axis inertial measurement unit, and is capable of giving acceleration and rotational velocities about the x, y, and z directions, using an MEM accelerometer and a gyroscope. In this project, the use of such a sensor is to observe the orientation of the robot w.r.t the x, y and z axes (as marked on the sensor). 

If the robot tilts beyond the required angular position, the MPU will monitor its angular position and feed it to the arduino. For obtaining values from the sensor, we used the Wire library as it enabled us to perform I2C communication between the arduino UNO (Master) and the MPU 6050 (Slave).

The I2C communication works by interconnecting the master and slave devices through two wires that convey two signals i.e the serial data (SDA) and the serial clock (SCL), all slave devices have a pre-determined address that is used by the master device as an ID and enables it to choose the correct slave device to communicate with. The data is transfered using 8 bit sequences. As shown in the image attached below, the start condition for the communication occurs when the SDA line transitions from high to low while the SCL line is high, next a 7-bit address of the slave is sent which the device would acknowledge by pulling the SDA line low. After this, another address of the internal register of the device where the required data might be stored is sent to the device. For e.g in our case first we would send the address of the sensor using `Wire.write
(0x68)`, then we will send the address of the internal register where the required data is stored, which is 0x43 for obtaining values from the gyro, by using `Wire.write(0x43)
` . Next the required data is transmitted from the MPU which would be the values given by the gyroscope. The stop condition will now occur when the SDA line transitions from low to high while the clock signal remains low.

![](../_resources/4ecdddf59beb4ac496e83562cf4a133e.png)

Data is read using `Wire.read()`, but this is just raw data and has to be filtered properly to get accurate values. Since the angular position can be measured on two ways:
1) By using accelerometer values and using trigonometry to get angular position
2) By using the rotational velocity, initial angular position and the time difference.

The accelerometer values are change a lot with vibrations and  sudden movements leading to inaccurate results of the angular position determined by the first method. The gyroscope values are relatively stable but they tend to drift after longer periods of time due to internal noise and imperfections in the sesor. Hence a combination of both the values could be used to determine accurate angular position that is stable over time and doesn't change too much with sudden movements or vibrations. Such a combination is also referred to as a complimentary filter:
`currentAngle = a*gyroAngle + (1-a)accAngle;`

References: 
[1] https://www.arduino.cc/en/reference/wire
[2]https://www.youtube.com/watch?v=2AO_Gmh5K3Q&list=PLGs0VKk2DiYwEo-k0mjIkWXlkrJWAU4L9
[3]https://www.youtube.com/watch?v=6IAkYpmA1DQ