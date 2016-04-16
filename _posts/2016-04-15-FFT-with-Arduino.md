---
layout: post
title: Real-time Signal Processing with Arduino
excerpt: "How to use Arduino for real-time audio signal processing."
categories: Arduino
comments: true
---

The objective of this exercise is to reproduce "Sitting Wave" using an Arduino. The audio signal from a microphone connected to the Arduino is modulated with a signal with a known frequency to bring the audio signal to base band. A low pass filter is applied to the result. Then the audio signal is output to SWIM stick to illustrate the phenomenon of the Sitting Wave with the use of a long exposure photograph.

### Background Knowledge
Nyquist Theorem:

    We can only accurately measure frequencies equal or less than half of the sampling rate.




<!-- Code example goes here -->


<!-- Questions
1. Inside the same app, could multiple instance of tasks exist?
-->

[You can find the awesome Adafruit tutorial here.]( https://learn.adafruit.com/fft-fun-with-fourier-transforms?view=all)
[Documentation on Wave Shield from Adafruit.](https://learn.adafruit.com/adafruit-wave-shield-audio-shield-for-arduino?view=all)
