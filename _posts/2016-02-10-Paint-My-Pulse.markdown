---
title:  "Paint My Pulse"
date:   2016-02-10 19:29:59
categories: Augmented Reality
---

# Project Summary
This post is about how to augment reality with your pulse readings in realtime.

# Supply List

## Light Painting Device

  * S.W.I.M. Stick
  * 7805

## Signal Processing Circuit
[comment]: <> (TODO: Details need to be added)
  + Caps
  + Resistors
  + LM324

## Pulse Sensor [details here](http://pulsesensor.com/pages/code-and-guide)

# Steps

1. Construct Signal Visualization Circuit with LEDs

    An array of LEDs is the great way to visualize signals when working as a voltmeter! When a signal comes in,
    you want to light up the corresponding LEDs in the array

    There are multiple ways to achieve this, you could use a micro-controller such as Arduino to light up correct
    LED depending input voltage.

2. Construct Signal Processing Circuit

    The signal from the pulse sensor is usually in mV, in order to see your pulse signal clearly on

3. Interface with Pulse Sensor

    Resources:

    + Pulse Sensor Sample Code on [git](https://github.com/WorldFamousElectronics/PulseSensor_Amped_Arduino)
