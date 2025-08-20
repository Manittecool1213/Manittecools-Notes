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
- How is batched gradient descent representative of the error of the entire dataset? Why not just update weights after each mini batch?
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
- (aside) How to get a *single* neuron to perform non-linear classification? Replace X here with some non-linear f(X). Issue: doesn't backpropagate well.
### Hebbian Learning Algorithm
- At this time, backpropagation didn't exist. Hebbian learning was used instead. This is also why thresholding functions were used instead of the constrained (differentiability, etc.) functions we now use with backpropagation.
- General idea of Hebbian learning:
	- Use the difference between the expected and reported outputs.
	- The weight of a neuron which was contributed more to an incorrect output will be changed more.
- Hebbian learning is not obsolete; some models today still use Hebbian learning.
- Limitations: 
	- Training progresses one input after another. This means that by the end of the training cycle, the weights may have become 'stale' relative to the initial inputs.
	- Processing one input after another also means that all compute is sequential - there is no scope for parallelisation.
	- Only works for a single layer; no way to propagate error if multiple layers exist.
---
# Learning Rate
- Parameters v/s hyperparameters:
	- Parameters: learnt by model during learning process.
	- Hyperparameters: need to be set; design choices.
- While learning rate is, strictly speaking, a hyperparameter, because of extensive literature there are now commonly accepted defaults, e.g.:
	- Start of with 10^-3, reduce if needed.
	- If performing transfer learning, use 10^-6.
- Epoch: number of times the training algorithm iterates through the entire dataset.
- What happens if you don't set the learning rate right?
	- Too low: too many updates required to reach minima.
	- Too high: drastic updates which may lead to divergent behaviours (oscillations in loss plot, which will eventually dampen).
- Rule of thumb: start of with a low value and steadily increase.
### Loss Plots: Quick Convergence ≠ Well Trained Model
- A high learning rate may result in the model quickly arriving at a non-divergent solution.
- However, convergence alone is not a good indicator of performance; the final training error which the model converges to also matters. If the final error is high, quick convergence is meaningless.
- Varying learning rate is also not the only available option. Instead of reducing the learning rate to reduce error, one can also increase the number of epochs to allow the model to converge to a lower minima.
- The only way to diagnose whether your model is working well or not is the loss plot. Don't only focus on accuracy; look at the trends of change of loss through the plot.
### Lack of Convergence
- What if you never see any convergence?
	- Your model is not complex enough.
	- This is DIFFERENT from oscillations due to too high a learning rate. Those oscillations will likely dampen, but if the model is not enough, it will just never converge at all.
---
# Loss Function
- Why it's non-trivial: you need some method to *accumulate* error in a manner such that it errors don't cancel each other out but add up instead.
- A perceptron without the activation function would perform regression.
- Regression uses Mean Squared Error, which harshly penalises a value which is 'distant' from the expectation. This means that the penalty is non-uniform; there may arise scenarios where we want the penalisation to be uniform instead.
--- 
# Batching
- First approach: use Hebbian learning to update weights per training example. Issue: completely serial; can't parallelise.
- Second approach: use a learning method which uses all training examples to make each update. Issue: might have too *much* data, such that each update takes a very long time.
- Solution: use batches (subsets of the entire training set) to compute loss. 
- With batching, you loss plot might not be as smooth as compared to the plot without any batching; there might be sharp edges owing to the fact that batching is stochastic. Inspite of this 'jaggedy' progression, the model will still converge with batching.
- Analytic solution - only applicable for single perceptron - proof cannot be extended to MLPs.
- Computation of batches - uses different sampling strategies - depending on parameters.
### Batched Gradient Descent
- Loss computed for every single batch, but update only made for entire epoch.