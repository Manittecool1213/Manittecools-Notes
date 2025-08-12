---
title: Example Title
draft: false
tags: []
---
 
# Read up on
- SVMs
- Non-linearities
- Kernels and decision trees
# Questions
- Why is transfer learning impossible with ML?
# Notes
--- 
- All neurons are structurally the same - those that help you smell and those that control your hand.
- Each individual neuron doesn't do much. It's the connections which create something meaningful.
- Hyperparameters are empirical; there is no algorithmic way of determining the best configuration. Past experience is used to choose 'good' hyperparameters.
--- 
### Benefits of Neural Networks
- Nonlinearity:
	- What does it mean to make a model 'more complex'?
		- Introduce non-linearities which can model data better.
		- Neural networks allow the introduction of such non-linearities.
		- The neural network itself decides what the complexity of the hyperplane needs to be.
	 - How to introduce non-linearities using conventional ML:
		- Use a kernel to project linear data into a higher dimensional space.
		- Use a decision tree.
- Adaptivity (Transfer Learning)
	- ML v/s DL
		- If you had an SVM classifier which could classify between dogs and cats, this same classifier would not be able to be used to distinguish between cats, inspite of there being some common knowledge to be shared.
		- This same knowledge would need to be repurposed and reconceptualised. This cannot be achieved through ML, only DL.
- Evidence:
	- Neural networks AREN'T total black boxes; there does exist evidence for decisions.
- Parallel Computing
---
- DL is not perfect; several instances of it failing:
	- Jaywalking detection in China.
	- Football detection.
	- McDonald's drive-thru with IBM.
	- Air Canada's chatbot.
	- Microsoft's Tay AI.