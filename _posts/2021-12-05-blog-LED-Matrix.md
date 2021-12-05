---
title: LED Matrix
tags: [arduino, neopixel, audio]
layout: article
mode: normal
type: article
sharing: true
author: Automation and Robotics Club
show_author_profile: true
show_title: true
full_width: false
header: true
cover: /assets/images/blog/thumbnails/LED Matrix.png
---

## Aim
Making a robot that balances itself using accelerometer and PID
<!--more-->
## Story
# LED Matrix Spectrum Analyser
### By Sirish, Andrew, Shaurya
---

## Fast Fourier Transform(FFT)
 
FFT is based on the principle that any signal(periodic or not) can be reconstructed by adding sinusoidal waves of different frequencies and amplitudes. Now FFT does this in reverse, where it splits an already existing wave into sinusoidal signals i.e the frequencies the wave contains.






<img src="{{site.baseurl}}/assets/images/blog/LED-Matrix/1.png" alt="1" width=auto height=auto>



<img src="{{site.baseurl}}/assets/images/blog/LED-Matrix/2.png" alt="2" width=auto height=auto>






Thus, we make use of FFT to identify which frequencies are present in any analog signal and also see which of those frequencies are the most dominating.
Coming to applying FFT to our audio visualiser, when we feed in an audio signal into an FFT we can find out the relative strengths of the frequencies.

Now let’s take a look at how FFT is applied.

## Sampling Frequency and Nyquist Theorem
Sampling frequency is the number of times we sample the wave per second.

The Nyquist-Shannon Sampling Theorem tells us that to be able to sample a signal, the sampling frequency needs to be at least twice the frequency of the signal we’re trying to sample.
In other words, the FFT will only be able to detect frequencies up to half the sampling frequency.

To explain how this works let’s use an example:

Say we want to sample an audio signal 10,000 times per second, i.e. 
**Sampling frequency =10,000Hz.**
- Now we want to see how many samples we can record from a wave of a certain frequency.
If we take a 2kHz wave, the number of samples we get is 10,000/2000=5 samples per wave.
Thus for a wave of this frequency, 5 samples per wave is good enough to recreate the wave.
- Now if we consider a wave of frequency 5kHz, we see that we only get 2 samples per wave.
- Furthermore, if we take a wave of frequency 10kHz we see that we only get 1 sample per wave, and the signal can no longer be reconstructed as it results in a straight line.
- 
Thus this is where the Nyquist theorem comes in and says that the maximum frequency we are able to sample is half of the sampling frequency.

<img src="{{site.baseurl}}/assets/images/blog/LED-Matrix/3.png" alt="3" width=auto height=auto>



## Number of Samples
The FFT algorithm works with a finite number of samples. This number needs to be 2n where n is an integer (resulting in 32, 64, 128, etc). The larger this number is, the slower the algorithm will be. However, with many samples, you will get a larger resolution for the results.

<img src="{{site.baseurl}}/assets/images/blog/LED-Matrix/4.png" alt="4" width=auto height=auto>

## Implementation:
We can implement FFT into our projects conveniently using the arduinoFFT.h library, the documentation for which can be found online.
arduinoFFT - Arduino Reference

## Results of FFT:

After we have achieved the results of FFT, we now have to understand them.
Let’s say we used 16 samples and a sampling rate of 40kHz

Since we use 16 samples we get 16 bins.

The term bins is related to the result of the FFT, where every element in the result array is a bin. One can say this is the “resolution” of the FFT. Every bin represents a frequency interval, just like a histogram. The number of bins you get to use is half the amount of samples spanning the frequency range from zero to half the sampling rate as the other half of the values are negative and meaningless.

In practicality, we can’t use the first bin either as this is swapped by DC. SO we only get to use 7 bins in the end for this case.

We can now map the bins as we wish to the number of bands we require.
For an audio signal, all the interesting stuff is towards the low end.
To help us do the calculations in mapping the bins to the bands, we can make use of the following spreadsheet. ( Courtesy: Scott Marley)

https://github.com/s-marley/ESP32_FFT_VU/blob/master/FFT.xlsx


### Implementation:
We can implement FFT into our projects conveniently using the arduinoFFT.h library, the documentation for which can be found online.
arduinoFFT - Arduino Reference
Results of FFT:
After we have achieved the results of FFT, we now have to understand them.
Let’s say we used 16 samples and a sampling rate of 40kHz.
Since we use 16 samples we get 16 bins.
The term bins is related to the result of the FFT, where every element in the result array is a bin. One can say this is the “resolution” of the FFT. Every bin represents a frequency interval, just like a histogram. The number of bins you get to use is half the amount of samples spanning the frequency range from zero to half the sampling rate as the other half of the values are negative and meaningless.
In practicality, we can’t use the first bin either as this is swapped by DC. SO we only get to use 7 bins in the end for this case.
We can now map the bins as we wish to the number of bands we require.
For an audio signal, all the interesting stuff is towards the low end. To help us do the calculations in mapping the bins to the bands, we can make use of the following spreadsheet.

Now that we have understood the theory we can apply it to our code.

## FastLED in a nutshell

FastLED is a fast, efficient, easy-to-use Arduino library for programming addressable LED strips and pixels such as WS2810, WS2811,
LPD8806, Neopixel and more. In this project we have used WS2812B LED strip. The first step is to include the library and define constants. 
```
include <FastLED.h> 
define NUM_LEDS 64 // number of leds in the matrix 
define DATA_PIN 4 
 Next, we set up an array to store the LED data.

CRGB leds[NUM_LEDS]
```
Then, we setup the LEDs.
`void setup(){ FastLED.addLeds(WS2812B, DATA_PIN)(leds, NUM_LEDS); }` 

### Writing to an LED 
```
void loop(){
leds[0] = CRGB::Red;
FastLED.show();
delay(50);
}
```

This will set the first led to red. To make it blink, we can change the code to this
```
void loop(){ leds[0] = CRGB::Red; FastLED.show();
delay(500); 
leds[0] = CRGB::Black;
FastLED.show();
delay(500);
}
``` 
**For writing to multiple LEDS, we can use loops.**
void loop(){ for(int i=0; i<NUM_LEDS; i++){ leds[i] = CRGB::Red;
FastLED.show(); delay(50); } } 
You can also display various patterns using FastLED.
For more details, refer:

## Resources: 

Scott Marley's github is an amazing resource for all things FastLED: https://github.com/s-marley
He also has a youtube channel explaining his projects: https://www.youtube.com/c/ScottMarley/playlists

## Testing:

<div>{%- include extensions/youtube.html id='1JBfoynNbsk' -%}</div>

<div>{%- include extensions/youtube.html id='1-eKlAaiR5k' -%}</div>

