---
layout: default
modal-id: 2
date: 2025-05-01
img: analog-neural-network.jpg
alt: image-alt
project-date: May 2025
description: For our final project in our analog electronics class, my teammates and I created a circuit that performs the computations necessary for the forward propagation stage of an analog neural network.
---

***

## Project Details

### Context

My project team in analog electronics had hearad about [FPAAs](https://en.wikipedia.org/wiki/Field-programmable_analog_array), the analog counterpart to FPGAs, and we thought it would be cool to make an analog neural network. Due to the time constraint of the final project, however, we were advised not to attempt the "learning" portion of the neural network and to simply focus on the forward propagation steps.

In a typical [neural network](https://en.wikipedia.org/wiki/Neural_network_(machine_learning)), there are many neurons which each perform forward propagation as the result of 3 operations: multiplication of inputs by weights, addition of a bias, and activation function. Our project implemented all three of these operations in conjunction.

### Summer

To add two voltages, we used a noninverting op amp summer, which averages the input voltages and then amplifies to scale the mean into the sum. The summer worked well for any voltage between the supplies of the op amp.

![summer](img/portfolio/analog-neural-network/summer.png)

### Multiplier

We tried to make several topologies for multiplying voltages, including the Gilbert cell, but were unsuccessful with getting them to work outside of simulation. After a significant amount of trial and error, we were successful at using a modified log-antilog multiplier to multiply two voltages. The circuit utilizes the fact that adding the logarithms of two numbers is equal to the logarithm of their product.
<br>
<br>
The logarithm circuit exploits the fact that the diode i-v curve is exponential. By using this property, an op amp circuit can be used to get an output voltage that is proportional to the natural logarithm of the input.

![log antilog](img/portfolio/analog-neural-network/log-antilog.png)

A big limitation with the log-antilog multiplier is that it can only perform single-quadrant multiplications; that is, the inputs must both be positive, since taking the logarithm of a nonpositive number is nonsense. To deal with this, I came up with a workaround: we could take the absolute value of the inputs and use those to find the absolute value of the product using the log-antilog multiplier. Then, we would choose to invert that answer depending on how many of the inputs were negative.
<br>
<br>
The absolute value circuit is shown below. It uses two op amps and two diodes to keep positive inputs and invert negative ones.

![absolute value](img/portfolio/analog-neural-network/abs-value.png)

If exactly one of the inputs is negative, then the product will be negative. Otherwise, it is positive. To determine whether the product is negative, we can use a XOR gate. The below shows a simplified interpretation; during the project we did not have access to an XOR gate and instead constructed our own out of logic MOSFETs.

![polarity](img/portfolio/analog-neural-network/polarity.png)

This signal is used as the control to select between two voltages using another MOSFET: one at twice the magnitude of the product of the inputs (produced using a noninverting amplifier) and ground. Then, the magnitude is subtracted from whatever is outputed by the multiplexer. This gives the correct answer regardless of whether the answer is positive or negative.

### Activation Function

Different neural networks may opt to use different nonlinear activation functions. The simplest one is ReLU, where positive inputs are kept the same and negative inputs are set to 0. This would simply be the behavior of an ideal diode. Since real diodes have a "turn on voltage" which would be lost if we simply fed the signal to the diode, we used precision rectifiers instead of real diodes to eliminate that error.

![relu](img/portfolio/analog-neural-network/relu.png)

### Project Conclusion

At the end, we fabricated some single-sided PCBs with all the circuits. When fully put together, the full neuron performed decently but had significant amounts of error in the calculations at times. The main takeaway is that while analog computations are definitely faster than clocked digital computation, accuracy is the tradeoff.

![full circuit](img/portfolio/analog-neural-network/full-circuit.png)
