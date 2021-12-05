---
title: RC Bot
tags: [arduino,NRF, MPU6050, joystick]
layout: article
mode: normal
type: article
sharing: true
author: Automation and Robotics Club
show_author_profile: true
show_title: true
full_width: false
header: true
cover: /assets/images/blog/thumbnails/RC Bot.png
---

## Aim
NRF controlled RC Car
<!--more-->
## Story
# RC BOT
## Overview
<img src="{{site.baseurl}}/assets/images/blog/RC-Bot/1.png" alt="1" width=auto height=auto>

<div>{%- include extensions/youtube.html id='GEZFZWXSNjg' -%}</div>

The components used for the RC bot are-
* Arduino Pro Mini
* NRF24L01 2.4GHz
* Joysticks
* MPU 6050
* DC Motor
* Chasis from Remote Control Car
* Toggle switch
* OLED Display

The car is fitted with a pro mini and an NRFacting as a receiver. The remote consists of a pro mini, an NRF acting as a transmitter and an MPU 6050. The remote consists of a switch which enables the user to toggle between joystick mode and motion control mode. The NRF transmitter sends the joystick/ MPU reading to the receiving NRF which sends the appropriate signal to the pro mini on the bot and finally to the actuators
***
## MPU 6050
<img src="{{site.baseurl}}/assets/images/blog/RC-Bot/2.png" alt="2" width=auto height=auto>
The MPU-6050 is the world’s first and only 6-axis motion tracking devices designed for the low power, low cost, and high performance requirements of smartphones, tablets and wearable sensors.
MPU6050 is a Micro Electro-mechanical system (MEMS), it consists of three-axis accelerometer and three-axis gyroscope. It helps us to measure velocity, orientation, acceleration, displacement and other motion like features.
This module uses the I2C module for interfacing with Arduino.
Following is the code to interface it with Arduino
```
#include "MPU6050_6Axis_MotionApps20.h"
//#include "MPU6050.h" // not necessary if using MotionApps include file

// Arduino Wire library is required if I2Cdev I2CDEV_ARDUINO_WIRE implementation
// is used in I2Cdev.h
#if I2CDEV_IMPLEMENTATION == I2CDEV_ARDUINO_WIRE
    #include "Wire.h"
#endif

// class default I2C address is 0x68
// specific I2C addresses may be passed as a parameter here
// AD0 low = 0x68 (default for SparkFun breakout and InvenSense evaluation board)
// AD0 high = 0x69
MPU6050 mpu;
//MPU6050 mpu(0x69); // <-- use for AD0 high

/* =========================================================================
   NOTE: In addition to connection 3.3v, GND, SDA, and SCL, this sketch
   depends on the MPU-6050's INT pin being connected to the Arduino's
   external interrupt #0 pin. On the Arduino Uno and Mega 2560, this is
   digital I/O pin 2.
 * ========================================================================= */

/* =========================================================================
   NOTE: Arduino v1.0.1 with the Leonardo board generates a compile error
   when using Serial.write(buf, len). The Teapot output uses this method.
   The solution requires a modification to the Arduino USBAPI.h file, which
   is fortunately simple, but annoying. This will be fixed in the next IDE
   release. For more info, see these links:

   http://arduino.cc/forum/index.php/topic,109987.0.html
   http://code.google.com/p/arduino/issues/detail?id=958
 * ========================================================================= */



// uncomment "OUTPUT_READABLE_QUATERNION" if you want to see the actual
// quaternion components in a [w, x, y, z] format (not best for parsing
// on a remote host such as Processing or something though)
//#define OUTPUT_READABLE_QUATERNION

// uncomment "OUTPUT_READABLE_EULER" if you want to see Euler angles
// (in degrees) calculated from the quaternions coming from the FIFO.
// Note that Euler angles suffer from gimbal lock (for more info, see
// http://en.wikipedia.org/wiki/Gimbal_lock)
//#define OUTPUT_READABLE_EULER

// uncomment "OUTPUT_READABLE_YAWPITCHROLL" if you want to see the yaw/
// pitch/roll angles (in degrees) calculated from the quaternions coming
// from the FIFO. Note this also requires gravity vector calculations.
// Also note that yaw/pitch/roll angles suffer from gimbal lock (for
// more info, see: http://en.wikipedia.org/wiki/Gimbal_lock)
#define OUTPUT_READABLE_YAWPITCHROLL

// uncomment "OUTPUT_READABLE_REALACCEL" if you want to see acceleration
// components with gravity removed. This acceleration reference frame is
// not compensated for orientation, so +X is always +X according to the
// sensor, just without the effects of gravity. If you want acceleration
// compensated for orientation, us OUTPUT_READABLE_WORLDACCEL instead.
//#define OUTPUT_READABLE_REALACCEL

// uncomment "OUTPUT_READABLE_WORLDACCEL" if you want to see acceleration
// components with gravity removed and adjusted for the world frame of
// reference (yaw is relative to initial orientation, since no magnetometer
// is present in this case). Could be quite handy in some cases.
//#define OUTPUT_READABLE_WORLDACCEL

// uncomment "OUTPUT_TEAPOT" if you want output that matches the
// format used for the InvenSense teapot demo
//#define OUTPUT_TEAPOT



#define INTERRUPT_PIN 2  // use pin 2 on Arduino Uno & most boards
#define LED_PIN 13 // (Arduino is 13, Teensy is 11, Teensy++ is 6)
bool blinkState = false;

// MPU control/status vars
bool dmpReady = false;  // set true if DMP init was successful
uint8_t mpuIntStatus;   // holds actual interrupt status byte from MPU
uint8_t devStatus;      // return status after each device operation (0 = success, !0 = error)
uint16_t packetSize;    // expected DMP packet size (default is 42 bytes)
uint16_t fifoCount;     // count of all bytes currently in FIFO
uint8_t fifoBuffer[64]; // FIFO storage buffer

// orientation/motion vars
Quaternion q;           // [w, x, y, z]         quaternion container
VectorInt16 aa;         // [x, y, z]            accel sensor measurements
VectorInt16 aaReal;     // [x, y, z]            gravity-free accel sensor measurements
VectorInt16 aaWorld;    // [x, y, z]            world-frame accel sensor measurements
VectorFloat gravity;    // [x, y, z]            gravity vector
float euler[3];         // [psi, theta, phi]    Euler angle container
float ypr[3];           // [yaw, pitch, roll]   yaw/pitch/roll container and gravity vector

// packet structure for InvenSense teapot demo
uint8_t teapotPacket[14] = { '$', 0x02, 0,0, 0,0, 0,0, 0,0, 0x00, 0x00, '\r', '\n' };



// ================================================================
// ===               INTERRUPT DETECTION ROUTINE                ===
// ================================================================

volatile bool mpuInterrupt = false;     // indicates whether MPU interrupt pin has gone high
void dmpDataReady() {
    mpuInterrupt = true;
}



// ================================================================
// ===                      INITIAL SETUP                       ===
// ================================================================

void setup() {
    // join I2C bus (I2Cdev library doesn't do this automatically)
    #if I2CDEV_IMPLEMENTATION == I2CDEV_ARDUINO_WIRE
        Wire.begin();
        Wire.setClock(400000); // 400kHz I2C clock. Comment this line if having compilation difficulties
    #elif I2CDEV_IMPLEMENTATION == I2CDEV_BUILTIN_FASTWIRE
        Fastwire::setup(400, true);
    #endif

    // initialize serial communication
    // (115200 chosen because it is required for Teapot Demo output, but it's
    // really up to you depending on your project)
    Serial.begin(115200);
    while (!Serial); // wait for Leonardo enumeration, others continue immediately

    // NOTE: 8MHz or slower host processors, like the Teensy @ 3.3V or Arduino
    // Pro Mini running at 3.3V, cannot handle this baud rate reliably due to
    // the baud timing being too misaligned with processor ticks. You must use
    // 38400 or slower in these cases, or use some kind of external separate
    // crystal solution for the UART timer.

    // initialize device
    Serial.println(F("Initializing I2C devices..."));
    mpu.initialize();
    pinMode(INTERRUPT_PIN, INPUT);

    // verify connection
    Serial.println(F("Testing device connections..."));
    Serial.println(mpu.testConnection() ? F("MPU6050 connection successful") : F("MPU6050 connection failed"));

    // wait for ready
    Serial.println(F("\nSend any character to begin DMP programming and demo: "));
    while (Serial.available() && Serial.read()); // empty buffer
    while (!Serial.available());                 // wait for data
    while (Serial.available() && Serial.read()); // empty buffer again

    // load and configure the DMP
    Serial.println(F("Initializing DMP..."));
    devStatus = mpu.dmpInitialize();

    // supply your own gyro offsets here, scaled for min sensitivity
    mpu.setXGyroOffset(220);
    mpu.setYGyroOffset(76);
    mpu.setZGyroOffset(-85);
    mpu.setZAccelOffset(1788); // 1688 factory default for my test chip

    // make sure it worked (returns 0 if so)
    if (devStatus == 0) {
        // Calibration Time: generate offsets and calibrate our MPU6050
        mpu.CalibrateAccel(6);
        mpu.CalibrateGyro(6);
        mpu.PrintActiveOffsets();
        // turn on the DMP, now that it's ready
        Serial.println(F("Enabling DMP..."));
        mpu.setDMPEnabled(true);

        // enable Arduino interrupt detection
        Serial.print(F("Enabling interrupt detection (Arduino external interrupt "));
        Serial.print(digitalPinToInterrupt(INTERRUPT_PIN));
        Serial.println(F(")..."));
        attachInterrupt(digitalPinToInterrupt(INTERRUPT_PIN), dmpDataReady, RISING);
        mpuIntStatus = mpu.getIntStatus();

        // set our DMP Ready flag so the main loop() function knows it's okay to use it
        Serial.println(F("DMP ready! Waiting for first interrupt..."));
        dmpReady = true;

        // get expected DMP packet size for later comparison
        packetSize = mpu.dmpGetFIFOPacketSize();
    } else {
        // ERROR!
        // 1 = initial memory load failed
        // 2 = DMP configuration updates failed
        // (if it's going to break, usually the code will be 1)
        Serial.print(F("DMP Initialization failed (code "));
        Serial.print(devStatus);
        Serial.println(F(")"));
    }

    // configure LED for output
    pinMode(LED_PIN, OUTPUT);
}



// ================================================================
// ===                    MAIN PROGRAM LOOP                     ===
// ================================================================

void loop() {
    // if programming failed, don't try to do anything
    if (!dmpReady) return;

    // wait for MPU interrupt or extra packet(s) available
    while (!mpuInterrupt && fifoCount < packetSize) {
        if (mpuInterrupt && fifoCount < packetSize) {
          // try to get out of the infinite loop 
          fifoCount = mpu.getFIFOCount();
        }  
        // other program behavior stuff here
        // .
        // .
        // .
        // if you are really paranoid you can frequently test in between other
        // stuff to see if mpuInterrupt is true, and if so, "break;" from the
        // while() loop to immediately process the MPU data
        // .
        // .
        // .
    }

    // reset interrupt flag and get INT_STATUS byte
    mpuInterrupt = false;
    mpuIntStatus = mpu.getIntStatus();

    // get current FIFO count
    fifoCount = mpu.getFIFOCount();
	if(fifoCount < packetSize){
	        //Lets go back and wait for another interrupt. We shouldn't be here, we got an interrupt from another event
			// This is blocking so don't do it   while (fifoCount < packetSize) fifoCount = mpu.getFIFOCount();
	}
    // check for overflow (this should never happen unless our code is too inefficient)
    else if ((mpuIntStatus & _BV(MPU6050_INTERRUPT_FIFO_OFLOW_BIT)) || fifoCount >= 1024) {
        // reset so we can continue cleanly
        mpu.resetFIFO();
      //  fifoCount = mpu.getFIFOCount();  // will be zero after reset no need to ask
        Serial.println(F("FIFO overflow!"));

    // otherwise, check for DMP data ready interrupt (this should happen frequently)
    } else if (mpuIntStatus & _BV(MPU6050_INTERRUPT_DMP_INT_BIT)) {

        // read a packet from FIFO
	while(fifoCount >= packetSize){ // Lets catch up to NOW, someone is using the dreaded delay()!
		mpu.getFIFOBytes(fifoBuffer, packetSize);
		// track FIFO count here in case there is > 1 packet available
		// (this lets us immediately read more without waiting for an interrupt)
		fifoCount -= packetSize;
	}
        #ifdef OUTPUT_READABLE_QUATERNION
            // display quaternion values in easy matrix form: w x y z
            mpu.dmpGetQuaternion(&q, fifoBuffer);
            Serial.print("quat\t");
            Serial.print(q.w);
            Serial.print("\t");
            Serial.print(q.x);
            Serial.print("\t");
            Serial.print(q.y);
            Serial.print("\t");
            Serial.println(q.z);
        #endif

        #ifdef OUTPUT_READABLE_EULER
            // display Euler angles in degrees
            mpu.dmpGetQuaternion(&q, fifoBuffer);
            mpu.dmpGetEuler(euler, &q);
            Serial.print("euler\t");
            Serial.print(euler[0] * 180/M_PI);
            Serial.print("\t");
            Serial.print(euler[1] * 180/M_PI);
            Serial.print("\t");
            Serial.println(euler[2] * 180/M_PI);
        #endif

        #ifdef OUTPUT_READABLE_YAWPITCHROLL
            // display Euler angles in degrees
            mpu.dmpGetQuaternion(&q, fifoBuffer);
            mpu.dmpGetGravity(&gravity, &q);
            mpu.dmpGetYawPitchRoll(ypr, &q, &gravity);
            Serial.print("ypr\t");
            Serial.print(ypr[0] * 180/M_PI);
            Serial.print("\t");
            Serial.print(ypr[1] * 180/M_PI);
            Serial.print("\t");
            Serial.println(ypr[2] * 180/M_PI);
        #endif

        #ifdef OUTPUT_READABLE_REALACCEL
            // display real acceleration, adjusted to remove gravity
            mpu.dmpGetQuaternion(&q, fifoBuffer);
            mpu.dmpGetAccel(&aa, fifoBuffer);
            mpu.dmpGetGravity(&gravity, &q);
            mpu.dmpGetLinearAccel(&aaReal, &aa, &gravity);
            Serial.print("areal\t");
            Serial.print(aaReal.x);
            Serial.print("\t");
            Serial.print(aaReal.y);
            Serial.print("\t");
            Serial.println(aaReal.z);
        #endif

        #ifdef OUTPUT_READABLE_WORLDACCEL
            // display initial world-frame acceleration, adjusted to remove gravity
            // and rotated based on known orientation from quaternion
            mpu.dmpGetQuaternion(&q, fifoBuffer);
            mpu.dmpGetAccel(&aa, fifoBuffer);
            mpu.dmpGetGravity(&gravity, &q);
            mpu.dmpGetLinearAccel(&aaReal, &aa, &gravity);
            mpu.dmpGetLinearAccelInWorld(&aaWorld, &aaReal, &q);
            Serial.print("aworld\t");
            Serial.print(aaWorld.x);
            Serial.print("\t");
            Serial.print(aaWorld.y);
            Serial.print("\t");
            Serial.println(aaWorld.z);
        #endif
    
        #ifdef OUTPUT_TEAPOT
            // display quaternion values in InvenSense Teapot demo format:
            teapotPacket[2] = fifoBuffer[0];
            teapotPacket[3] = fifoBuffer[1];
            teapotPacket[4] = fifoBuffer[4];
            teapotPacket[5] = fifoBuffer[5];
            teapotPacket[6] = fifoBuffer[8];
            teapotPacket[7] = fifoBuffer[9];
            teapotPacket[8] = fifoBuffer[12];
            teapotPacket[9] = fifoBuffer[13];
            Serial.write(teapotPacket, 14);
            teapotPacket[11]++; // packetCount, loops at 0xFF on purpose
        #endif

        // blink LED to indicate activity
        blinkState = !blinkState;
        digitalWrite(LED_PIN, blinkState);
    }
}
```
***
## NRF 24
<img src="{{site.baseurl}}/assets/images/blog/RC-Bot/3.png" alt="3" width=auto height=auto>
The nRF24L01+ transceiver module is designed to operate in 2.4 GHz worldwide ISM frequency band and uses GFSK modulation for data transmission. The data transfer rate can be one of 250kbps, 1Mbps and 2Mbps. The nRF24L01+ transceiver module communicates over a 4-pin Serial Peripheral Interface (SPI) with a maximum data rate of 10Mbps. All the parameters such as frequency channel (125 selectable channels), output power (0 dBm, -6 dBm, -12 dBm or -18 dBm), and data rate (250kbps, 1Mbps, or 2Mbps) can be configured through SPI interface. The SPI bus uses a concept of a Master and Slave, in most common applications our Arduino is the Master and the nRF24L01+ transceiver module is the Slave.
Following is a link for a more practical understanding
https://electronoobs.com/eng_arduino_tut95.php
***




## Transmitter Code
```
#include <SPI.h>
#include <nRF24L01.h>
#include <RF24.h>
#include <Wire.h>
#include <Adafruit_MPU6050.h>
#include <Adafruit_Sensor.h>
#include <Adafruit_GFX.h>
#include <Adafruit_SSD1306.h>
#define SCREEN_WIDTH 128 // OLED display width, in pixels
#define SCREEN_HEIGHT 64 // OLED display height, in pixels

Adafruit_SSD1306 display(SCREEN_WIDTH, SCREEN_HEIGHT, &Wire, -1);
Adafruit_MPU6050 mpu;

// Define the digital inputs
/*#define jB1 1  // Joystick button 1
#define jB2 0  // Joystick button 2
#define t1 7   // Toggle switch 1
#define t2 4   // Toggle switch 1
#define b1 8   // Button 1
#define b2 9   // Button 2
#define b3 2   // Button 3
#define b4 3   // Button 4*/
#define forwardLed 7
#define sidewardLed 2
#define modeSwitchPin 3
//const int MPU = 0x68; // MPU6050 I2C address
float AccX, AccY, AccZ;
float GyroX, GyroY, GyroZ;
float accAngleX, accAngleY, gyroAngleX, gyroAngleY;
float angleX, angleY;
float AccErrorX, AccErrorY, GyroErrorX, GyroErrorY;
float elapsedTime, currentTime, previousTime;
int c = 0;

RF24 radio(5, 6);   // nRF24L01 (CE, CSN)
const byte address[6] = "00001"; // Address
// Max size of this struct is 32 bytes - NRF24L01 buffer limit
struct Data_Package {
  byte j1PotY;
  byte j2PotX;
  byte IMUfwdrev;
  byte IMUlr;
  byte ModeSwitch;
};

Data_Package data; //Create a variable with the above structure
void setup() {
  
  Serial.begin(115200);
  while (!Serial)
    delay(10); // will pause Zero, Leonardo, etc until serial console opens

  Serial.println("Adafruit MPU6050 test!");

  // Try to initialize!
  if (!mpu.begin()) {
    Serial.println("Failed to find MPU6050 chip");
    while (1) {
      delay(10);
    }
  }
  Serial.println("MPU6050 Found!");
  pinMode(forwardLed, OUTPUT);
  pinMode(sidewardLed, OUTPUT);

  if(!display.begin(SSD1306_SWITCHCAPVCC, 0x3C)) 
  { 
  Serial.println("SSD1306 allocation failed");
 
  //for(;;); // Don't proceed, loop forever
  }

//  display.clearDisplay();
//
//  display.setTextSize(2);
//  display.setTextColor(WHITE);
//  display.setCursor(0, 10);
//  // Display static text
//  display.println("The display is working");
//  display.display();
//  
  // Initialize interface to the MPU6050
  //initialize_MPU6050();
  // Call this function if you need to get the IMU error values for your module
  //calculate_IMU_error();
  
  // Define the radio communication
  radio.begin();
  radio.openWritingPipe(address);
  //radio.setAutoAck(false);
  //radio.setDataRate(RF24_250KBPS);
  radio.stopListening();
  //radio.setPALevel(RF24_PA_LOW);
  /*
  // Activate the Arduino internal pull-up resistors
  pinMode(jB1, INPUT_PULLUP);
  pinMode(jB2, INPUT_PULLUP);
  pinMode(t1, INPUT_PULLUP);
  pinMode(t2, INPUT_PULLUP);
  pinMode(b1, INPUT_PULLUP);
  pinMode(b2, INPUT_PULLUP);
  pinMode(b3, INPUT_PULLUP);
  pinMode(b4, INPUT_PULLUP);*/
  
  // Set initial default values
  //data.j1PotX = 127; // Values from 0 to 255. When Joystick is in resting position, the value is in the middle, or 127. We actually map the pot value from 0 to 1023 to 0 to 255 because that's one BYTE value
  data.j1PotY = 127;
  data.j2PotX = 127;
  /*data.j2PotY = 127;
  data.j1Button = 1;
  data.j2Button = 1;
  data.pot1 = 1;
  data.pot2 = 1;
  data.tSwitch1 = 1;
  data.tSwitch2 = 1;
  data.button1 = 1;
  data.button2 = 1;
  data.button3 = 1;
  data.button4 = 1;*/

   mpu.setAccelerometerRange(MPU6050_RANGE_8_G);
  Serial.print("Accelerometer range set to: ");
  switch (mpu.getAccelerometerRange()) {
  case MPU6050_RANGE_2_G:
    Serial.println("+-2G");
    break;
  case MPU6050_RANGE_4_G:
    Serial.println("+-4G");
    break;
  case MPU6050_RANGE_8_G:
    Serial.println("+-8G");
    break;
  case MPU6050_RANGE_16_G:
    Serial.println("+-16G");
    break;
  }
  mpu.setGyroRange(MPU6050_RANGE_500_DEG);
  Serial.print("Gyro range set to: ");
  switch (mpu.getGyroRange()) {
  case MPU6050_RANGE_250_DEG:
    Serial.println("+- 250 deg/s");
    break;
  case MPU6050_RANGE_500_DEG:
    Serial.println("+- 500 deg/s");
    break;
  case MPU6050_RANGE_1000_DEG:
    Serial.println("+- 1000 deg/s");
    break;
  case MPU6050_RANGE_2000_DEG:
    Serial.println("+- 2000 deg/s");
    break;
  }

  mpu.setFilterBandwidth(MPU6050_BAND_21_HZ);
  Serial.print("Filter bandwidth set to: ");
  switch (mpu.getFilterBandwidth()) {
  case MPU6050_BAND_260_HZ:
    Serial.println("260 Hz");
    break;
  case MPU6050_BAND_184_HZ:
    Serial.println("184 Hz");
    break;
  case MPU6050_BAND_94_HZ:
    Serial.println("94 Hz");
    break;
  case MPU6050_BAND_44_HZ:
    Serial.println("44 Hz");
    break;
  case MPU6050_BAND_21_HZ:
    Serial.println("21 Hz");
    break;
  case MPU6050_BAND_10_HZ:
    Serial.println("10 Hz");
    break;
  case MPU6050_BAND_5_HZ:
    Serial.println("5 Hz");
    break;
  }

  Serial.println("");
}
void loop() {
  // Read all analog inputs and map them to one Byte value
 // data.j1PotX = map(analogRead(A1), 0, 1023, 0, 255); // Convert the analog read value from 0 to 1023 into a BYTE value from 0 to 255
 data.ModeSwitch = digitalRead(modeSwitchPin);
 Serial.println(data.ModeSwitch);
  data.j1PotY = map(analogRead(A6), 0, 1023, 0, 255);
  data.j2PotX = map(analogRead(A1), 0, 1023, 0, 255);
  //Serial.println("for front-back joystick");
  Serial.println(data.j1PotY);
  if(data.j1PotY >= 140 || data.j1PotY <= 120)
    digitalWrite(forwardLed, HIGH);
  else
    digitalWrite(forwardLed, LOW);
 // Serial.println("for sideward joystick");
   // Serial.println(data.j2PotX);
  if(data.j2PotX <= 120 || data.j2PotX >= 140 )
    {
      
      digitalWrite(sidewardLed, HIGH);
    }
  else 
    digitalWrite(sidewardLed, LOW); 

//     
sensors_event_t a, g, temp;
  mpu.getEvent(&a, &g, &temp);

//  /* Print out the values */
//  Serial.print("Acceleration X: ");
//  Serial.print(a.acceleration.x);
//  Serial.print(", Y: ");
//  Serial.print(a.acceleration.y);
//  Serial.print(", Z: ");
//  Serial.print(a.acceleration.z);
//  Serial.println(" m/s^2");
//
//  Serial.print("Rotation X: ");
//  Serial.print(g.gyro.x);
//  Serial.print(", Y: ");
//  Serial.print(g.gyro.y);
//  Serial.print(", Z: ");
//  Serial.print(g.gyro.z);
//  Serial.println(" rad/s");

//  Serial.print("Temperature: ");
//  Serial.print(temp.temperature);
//  Serial.println(" degC");

  Serial.println("");


  AccX = a.acceleration.x;
  AccY = a.acceleration.y;
  AccZ = a.acceleration.z;
  GyroX = g.gyro.x;
  GyroY = g.gyro.y;
  GyroZ = g.gyro.z;
  
//    while (c < 20) {
//    AccErrorX = AccErrorX + ((atan((AccY) / sqrt(pow((AccX), 2) + pow((AccZ), 2))) * 180 / PI));
//    AccErrorY = AccErrorY + ((atan(-1 * (AccX) / sqrt(pow((AccY), 2) + pow((AccZ), 2))) * 180 / PI));
//    GyroErrorX = GyroErrorX + (GyroX / 32.8);
//    GyroErrorY = GyroErrorY + (GyroY / 32.8);
//    c++;
//  }
  read_IMU();

//  Serial.print("Angle X (used for direction change): ");
//  Serial.println(accAngleX);
//  Serial.print("Angle Y (used for fwd and rev): ");
//  Serial.println(accAngleY);

  Serial.println("Values sent to the car:  ");
  Serial.print("IMUfwdrev : ");
  Serial.println(data.IMUfwdrev);
  Serial.print("IMUlr : ");
  Serial.println(data.IMUlr);
  
  
    // Send the whole data from the structure to the receiver
  radio.write(&data, sizeof(Data_Package));
  

}

void read_IMU() {
 
  accAngleX = (atan(AccY / sqrt(pow(AccX, 2) + pow(AccZ, 2))) * 180 / PI) + 1.15; // AccErrorX ~(-1.15) See the calculate_IMU_error()custom function for more details
  accAngleY = (atan(-1 * AccX / sqrt(pow(AccY, 2) + pow(AccZ, 2))) * 180 / PI) - 0.52; // AccErrorX ~(0.5)
  // === Read gyro data === //
//  previousTime = currentTime;        // Previous time is stored before the actual time read
//  currentTime = millis();            // Current time actual time read
//  elapsedTime = (currentTime - previousTime) / 1000;   // Divide by 1000 to get seconds
//  GyroX = GyroX + 1.85; //// GyroErrorX ~(-1.85)
//  GyroY = GyroY - 0.15; // GyroErrorY ~(0.15)
//  // Currently the raw values are in degrees per seconds, deg/s, so we need to multiply by sendonds (s) to get the angle in degrees
//  gyroAngleX = GyroX * elapsedTime;
//  gyroAngleY = GyroY * elapsedTime;
//  // Complementary filter - combine acceleromter and gyro angle values
//  angleX = 0.98 * (angleX + gyroAngleX) + 0.02 * accAngleX;
//  angleY = 0.98 * (angleY + gyroAngleY) + 0.02 * accAngleY;
  // Map the angle values from -90deg to +90 deg into values from 0 to 255, like the values we are getting from the Joystick
  data.IMUfwdrev = map(accAngleY, -90, +40, 0, 255);
  data.IMUlr = map(accAngleX, -80, +80, 255, 0);  

}
```
***
## Receiver Code
```

#include <nRF24L01.h>
#include <RF24.h>
#include <Wire.h>
#include <SPI.h>

//RF24 radio(7, 8);   // nRF24L01 (CE, CSN) for NANO
//RF24 radio(9, 10);   // nRF24L01 (CE, CSN) for UNO
RF24 radio(5, 6);   // nRF24L01 (CE, CSN) for PRO MINI
const byte address[6] = "00001"; // Address
   //Max size of this struct is 32 bytes - NRF24L01 buffer limit

#define ForwardReverse 9 // pwm pin to the hbridge to vary motor speed
#define Sideward 10   // pwm pin to the hbridge to vary motor speed

#define ForwardReverse 9
#define Sideward 10
#define forward 7
#define reverse 8
#define right 3
#define left 4

int ModeSwitch;
struct Data_Package {
  byte j1PotY;
  byte j2PotX;
  byte IMUfwdrev;
  byte IMUlr;
  byte ModeSwitch;
};

Data_Package data;

  
void setup() {
  Serial.begin(9600);
  pinMode(right, OUTPUT);
  pinMode(left, OUTPUT);
  pinMode(2, OUTPUT);  // led for debugging and showing comms working
  pinMode(forward, OUTPUT);
  pinMode(ForwardReverse, OUTPUT);
  pinMode(Sideward, OUTPUT);
  pinMode(reverse, OUTPUT);
  digitalWrite(2, HIGH);
  delay(1000);
  digitalWrite(2, LOW);
  
  
  //pinMode(LED_BUILTIN, OUTPUT);
  radio.begin();
  radio.openReadingPipe(0, address);
  //radio.setPALevel(RF24_PA_MIN); 
  radio.startListening();
  
    //data.j1PotX = 127; // Values from 0 to 255. When Joystick is in resting position, the value is in the middle, or 127. We actually map the pot value from 0 to 1023 to 0 to 255 because that's one BYTE value
  data.j1PotY = 127;
  data.j2PotX = 127;
  /*data.j2PotY = 127;
  data.j1Button = 1;
  data.j2Button = 1;
  data.pot1 = 1;
  data.pot2 = 1;
  data.tSwitch1 = 1;
  data.tSwitch2 = 1;
  data.button1 = 1;
  data.button2 = 1;
  data.button3 = 1;
  data.button4 = 1;*/

}

void loop() {
 Serial.println("This is Receiver");
 if (radio.available())
 {
   Serial.println("All Good");
   digitalWrite(2, !digitalRead(2));
   radio.read(&data, sizeof(Data_Package));
   ModeSwitch = data.ModeSwitch;
   //Serial.println(data.j1PotY);
   //Serial.println(data.j2PotX);
   /*digitalWrite(2, HIGH);
   delay(500);
   digitalWrite(2, LOW);
   delay(500);*/
 }
 else 
 {
   digitalWrite(2, HIGH);
   //Stop();
  digitalWrite(forward, LOW);      // vehicle stops
  digitalWrite(reverse, LOW);
  analogWrite(ForwardReverse,0);
  digitalWrite(right, LOW);
  digitalWrite(left, LOW); 
 }

 if(ModeSwitch){                     // This is the mode in which the bot will work in joystick mode

 if(data.j1PotY >= 130)
 {
   onward();
   if(data.j2PotX >= 130)
   {
    turnRight();
   }
   
   else if(data.j2PotX <= 120)
   {
    turnLeft();
   }
 }

 else if(data.j1PotY <= 120)
 {
   Reverse();
   if(data.j2PotX >= 130)
   {
    turnRight();
   }
   
   else if(data.j2PotX <= 120)
   {
    turnLeft();
   }
 }

 else if(data.j1PotY <= 130 && data.j1PotY >=120)
 {
  Stop();
  if(data.j2PotX >= 130)
   {
    turnRight();
   }
   
   else if(data.j2PotX <= 120)
   {
    turnLeft();
   }
 }
 }

 

else if(!ModeSwitch){                     // this is the   mode n which the bot will work in motion control/ gesture control mode

  if(data.IMUfwdrev >= 140)
 {
   onwardMS();
   if(data.IMUlr >= 145)
   {
    turnRightMS();
   }
   
   else if(data.IMUlr <= 110)
   {
    turnLeftMS();
   }
 }

 else if(data.IMUfwdrev <= 100)
 {
   ReverseMS();
   if(data.IMUlr >= 145)
   {
    turnRightMS();
   }
   
   else if(data.IMUlr <= 110)
   {
    turnLeftMS();
   }
 }

 else if(data.IMUfwdrev < 140 && data.IMUfwdrev > 100)
 {
  Stop();
  if(data.IMUlr >= 145)
   {
    turnRightMS();
   }
   
   else if(data.IMUlr <= 110)
   {
    turnLeftMS();
   }
 }
  
}

 
}




int onward()
{
  digitalWrite(forward, HIGH);      // vehicle moves forward
  digitalWrite(reverse, LOW);
  analogWrite(ForwardReverse, (data.j1PotY-128)*2);
}

int Reverse()
{
  digitalWrite(forward, LOW);      // vehicle reverses
  digitalWrite(reverse, HIGH);
  analogWrite(ForwardReverse,(127-data.j1PotY)*2);
}
int turnRight()
{
  digitalWrite(left, LOW);      // steering turns right
  digitalWrite(right, HIGH);
  analogWrite(Sideward,(data.j2PotX-128)*2);
}

int turnLeft()
{
  digitalWrite(right, LOW);      // steering turns left
  digitalWrite(left, HIGH);
  analogWrite(Sideward,(127-data.j2PotX)*2);
}



int onwardMS()
{
  digitalWrite(forward, HIGH);      // vehicle moves forward
  digitalWrite(reverse, LOW);
  analogWrite(ForwardReverse, (data.IMUfwdrev-128)*2);
}

int ReverseMS()
{
  digitalWrite(forward, LOW);      // vehicle reverses
  digitalWrite(reverse, HIGH);
  analogWrite(ForwardReverse,(127-data.IMUfwdrev)*2);
}
int turnRightMS()
{
  digitalWrite(left, LOW);      // steering turns right
  digitalWrite(right, HIGH);
  analogWrite(Sideward,(data.IMUlr-128)*2);
}

int turnLeftMS()
{
  digitalWrite(right, LOW);      // steering turns left
  digitalWrite(left, HIGH);
  analogWrite(Sideward,(127-data.IMUlr)*2);
}

int Stop()
{
  digitalWrite(forward, LOW);      // vehicle stops
  digitalWrite(reverse, LOW);
  analogWrite(ForwardReverse,0);
  digitalWrite(right, LOW);
  digitalWrite(left, LOW); 
}
```




