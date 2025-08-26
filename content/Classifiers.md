---
title: Classifiers
draft: false
tags:
---
---
- (aside) Expect the following for exams:
	- Conditional probability.
	- Traces of gradient descent, logistic regression.
	- Because sigmoid is being used, answers will all be close to each other. Consequently, decimal place values are critical; your answer needs to be accurate.
---
# Questions
- Why do we get rid of the activation function in the output layer when using softmax?
---
# Naive Bayes Classifier
- Why called 'naive'? Makes naive assumption - all features in the dataset are conditionally independent from each other.
- What to use when this assumption fails? Markov Chains, RNNs.
- What is the Bayes classifier trying to estimate: Given certain features, what is the probability that the example belong to a particular class?
---
# Logistic Regression
- How to achieve classification through regression? Use thresholding. Example: everything above the best fit line is one class, everything below is another.
- Gradient descent won't work with threshold activation functions - they're non differentiable. This motivates the usage of logistic regression.
- The name is a misnomer; in ML, logistic regression is used for classification.
- Choice of activation function: depends on what its derivative looks like. 
	- Gradients are always expressed in terms of expected output, actual output, and input.
	- If the derivative of the activation function can be expressed using these, computation is easy.
- MSE equivalent can be used with sigmoid activation as well.
---
# Softmax
- When working with a single perceptron - the only kind of classification which you can perform is binary. 
- How to interpret scores?
	- Have a threshold. 
	- Any value above the threshold belongs to the class.
	- Any value below DOESN'T belong to the class (cat or not cat, NOT cat or dog).
- How to improve this classification, enabling cat / dog classification?
	- Use another perceptron in the same layer. 
	- Outputs now become: P(cat / not cat), P(dog / not dog).
	- These outputs would now need to be combined - which is what softmax does.
- Softmax values are calculated based on the predicted output, WITHOUT any activation function.
- We perform exponentiation in order to handle negative values, which are possible for the raw output value.
---
# Modelling Outputs and Probabilities
- Regression lends itself to MSE - because of the way the expression of negative log likelihood looks; it contains the MSE term.
- Similarly, classification lends itself to binary cross entropy.
- (aside) The cross entropy loss slide assumes single-dimensional output with a sigmoid activation function. It is only applicable for binary classification, not a situation where softmax is used and the output vector is multidimensional.
- There is no 'incorrect' loss. If you were to use MSE for classification, it is not as though you would get no solution (minima). You would just get a suboptimal minima.
- Loss functions are NOT hyperparameters. Each model has certain properties, which determine what the best loss function is.
- (aside) Read up on: contrastive losses.