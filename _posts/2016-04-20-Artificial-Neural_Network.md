---
layout: post
title: Neural Network with Arduino 101
excerpt: "How to do some basic machine learning with Arduino"
categories: Arduino Machine Learning
comments: true
---

### Neurons Are Like Switches That Are Connected Together
When stimulated, a neuron could be thought as switched on, and it would activate other neutrons in the network. However, unlike switches, the amount of stimulus is related how strong each connections is. The output would be based on the stimulus passing through all these varying strength connections.

### How Software Models Neural Network
It uses Math of course! The software would receive a pattern an input, and it would adds up the input's stimulus effect on each neutron and calculate the output, in a cascaded style.

The software also has to have weights to define the strength of each neuron connection. For backpropagation algorithm specifically, the network is first initialized with random weights. Then the system would start receiving training sets (patterns that we know what they mean) and compare the computed outputs with the known outputs. If any error is found, the error is then fed back through the system to adjust the weights. After thousands or more training sets, all the weights inside the system would be adjusted to an optimal value to produce the correct output. Therefore, the system learned how to properly respond to (interprete) any input patterns.

Example of a 3 layer feed forward network: [Input -> Hidden -> output].
This layout can solve any truth table!!!

<!-- Code example goes here -->


<!-- Questions
1. Inside the same app, could multiple instance of tasks exist?
-->

[For more detailed information, see this tutorial.](http://robotics.hobbizine.com/arduinoann.html)
