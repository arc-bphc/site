---
title: Music Visualisation 
tags: [arduino,3528 LED,NPN,op-amp]
layout: article
mode: normal
type: article
sharing: true
author: Gaurab Dasgupta
show_author_profile: true
show_title: true
full_width: false
header: true
cover: /assets/images/blog/thumbnails/Music Visualisation.png
---
## AIM
To filter the incoming audio signal and see how each coloured LED of RGB 3528 SMD strip reacts to different frequencies of the signal.
<!--more-->

## HARDWARE NEEDED
- Arduino Uno(1)
- RGB 3528 LED Strip(1)
- TIP31C NPN transistor(3)
- Electret Microphone(1)
- 12V Battery(1)
- 470 Ω resistors(3)
- 10 µF capacitor(1)
- 100nF capacitor(1)
- LM3528 op-amp(1)
- 1KΩ resistor(2)
- 10KΩ resistor(2)
- 100KΩ resistor(1)

## THE WORKING 
The project basically consists of 3 stages:-

1. Constructing a pre-amplifier mic circuit

2. Taking the mic signals as the input in the Arduino and filtering it into three frequency ranges using the FIR filter implemented in the code itself.

3. Building the LED circuit and using the filtered outputs to control the brightness of the  LEDs.

### Building The Pre-Amp Mic Circuit
To amplify the voltage signals of the electret mic, op-amp(LM 358) was used. Op-amps were preferred over NPN transistors because of the high voltage gain of the op-amps. Fundamentally, an op-amp is an equivalent of many transistors and so, has a higher performance .

The inverting AC amplifier configuration was used which mean that there is inversion of the output signal with respect to the input as it is 180o out of phase. This is the circuit diagram for it :-
<img src="{{site.baseurl}}/assets/images/blog/Music-Visualisation/1.png" alt="Resistor" width=auto height=auto>


The V_OUT_UC goes into the Arduino. The V_OUT is for connecting earphones directly.

Voltage gain for an inverting amplifier is given by the inverting operational amplifier gain equation

Here, the voltage gain is given by -R5/R4. Using R5 as 100K and R4 as 1K, a voltage gain of 100x was achieved.

A graphical representation of the op-amp circuit is here
<img src="{{site.baseurl}}/assets/images/blog/Music-Visualisation/2.png" alt="Resistor" width=auto height=auto>


Here, an electrolytic Microphone Coupling Capacitor has been used. A coupling capacitor is generally used in audio circuits to keep the DC and AC signals apart. DC is used give power to the parts of the circuit while the incoming audio signal will be AC. Since a capacitor blocks low frequencies and allows high frequencies, it can be used to block the DC signals and allowing only AC signals to pass through, effectively decreasing the noise.                                                                                                                                                   The next interesting component is the ceramic Power Supply Decoupling Capacitor which protects the ICs by suppressing the high frequency signals in the power supply signals.                                                                                                                                         The power supply is taken from the 5V  of the Arduino.

The reading on the serial plotter look like this :-
<img src="{{site.baseurl}}/assets/images/blog/Music-Visualisation/3.png" alt="Resistor" width=auto height=auto>

<img src="{{site.baseurl}}/assets/images/blog/Music-Visualisation/4.png" alt="Resistor" width=auto height=auto>


### The RGB LED Strip Circuit
This strip works on 12V. Since the Arduino cannot provide 12V, NPN transistors (TIP31Cs) have been used.

The PWM voltage output pins of the Arduino, which control the brightness, are connected to the base, the LED strip to the collector and the emitter to the ground.

This is the graphical representation of the circuit:-
<img src="{{site.baseurl}}/assets/images/blog/Music-Visualisation/5.png" alt="Resistor" width=auto height=auto>


### The Code for Sampling and Filtering
The Arduino Uno clock is at 16MHz.
The ADC clock is at (16/prescaler) where the prescalar can be 16,32,64 or 128.
One ADC conversion takes 13 ADC clocks.
According to the Atmega328p datasheet, the recommended ADC clock should be between 50KHz and 200KHz. So, by default, the prescaler is set to 128, which, would in turn give us a sampling rate of approximately 9600 Hz. But to get 8KHz analyzable spectrum one needs to sample at 16KHz according to Nyquist theorem. So, in the code, the prescaler is set to 64 so that  a sampling rate of 17800 Hz(almost 16KHz) is got.

After sampling at 17800 Hz, filter the signal through digital [FIR filters](https://en.wikipedia.org/wiki/Finite_impulse_response).
[This MATLAB code](https://github.com/gaurabdg/FIR-Spectrum-Analyzer/blob/master/src/matlab/FIR_FilterDesign.m) was used to generate the FIR coefficients.

The cut-off frequencies for the filters were calculated by playing tracks and observing the most active frequency ranges on [trueRTA](https://trueaudio.com/rta_abt1.htm).

[This is the link to the Arduino Code.](https://github.com/gaurabdg/FIR-Spectrum-Analyzer/blob/master/src/arduino/BeatDet.ino)

Just a few snaps
<img src="{{site.baseurl}}/assets/images/blog/Music-Visualisation/6.png" alt="Resistor" width=auto height=auto>
<img src="{{site.baseurl}}/assets/images/blog/Music-Visualisation/7.png" alt="Resistor" width=auto height=auto>


<div>{%- include extensions/youtube.html id='zxZnOtWrG0c' -%}</div>
