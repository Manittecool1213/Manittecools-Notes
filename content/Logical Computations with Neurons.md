---
title: Logical Computations with Neurons
draft: false
tags: 
Date: Wednesday, 13th August 2025
---
# Questions
- In a hot-cold perceiver type network, isn't it a problem if the classification times are different for different inputs? If multiple classifications were being performed one after another, this time lag would cause a thresholding issue.
- Where does the time-step notion arise from? Why couldn't modelling be done using some sort of electrical network with instant propagation?
- Why can't learning take place with neurons? Why is the activation function or the bias term required?
	- The concept of 'learning' information / classifications simply wasn't discovered while neurons were relevant.
	- It was only with the introduction of the perceptron that the concept of 'learning' and the Hebbian learning strategy were introduced.
--- 
# McCulloch-Pitts Neuron
Can perform various operations such as logical and / logical or using weights and thresholds.
- What is noteworthy: there are (infinitely) many combinations of weights and thresholds possible for performing such a classification.
- Issue: not every logical gate can be modelled as a classification problem.
	- XOR cannot be modelled using a single neuron.
	- Resolving issue:
		- Using more layers and more neurons in each layer.
		- A XOR B can be expanded as (A and not B) or (not A and B).
		- Consequently, the total number of neurons required is 3, with the not gate being handled by negative weight values.
- Temporal dynamics:
	- The deeper the network, the more time units required for processing. 
	- Each layer is processed parallely, but successive layers require information from previous layers to function.
- When talking about 'layers' of a neural network, we typically omit the input and output layer; we focus only on layers with trainable parameters.
---
# Rosenblatt's Perceptron
- The perceptron is where 'learning' starts to happen, because of the introduction of three elements:
	- Bias term
	- Activation function
	- Hebbian Learning
- Why use biasses at all?
	- Without a bias term, every hyperplane would pass through the origin.
	- With a bias term, we are able to transpose the hyperplane to any position in the 2D-plane.
	- Bottom line: more flexibility and expressibility added.
- Expression: 
	- Full expression fn(W^T * X + b):
		- W: weight
		- X: input
		- b: bias
	- The bias term can be absorbed into the weight as W_0, with X_0 = 1, reducing the expression to fn(W^T * X).
- At this time, backpropagation didn't exist. Hebbian learning was used instead. This is also why thresholding functions were used instead of the constrained functions we now use with backpropagation.
- General idea of Hebbian learning:
	- Use the difference between the expected and given outputs.
	- The amount of change required depends on the input which caused the change.
- Hebbian learning is not obsolete; some models today still use Hebbian learning.
