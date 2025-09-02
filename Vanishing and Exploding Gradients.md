---
title: Vanishing and Exploding Gradients
draft: false
tags:
---
# Questions
- How do I exploit knowledge of precision and recall to train my model to optimise for either of them specifically? If I knew I wanted to classify disease samples, I already know that I care more about recall than precision. How do I make use of this knowledge to curate my dataset / change my training loop / loss function.
	- (partial answer) use the metric directly; pick models which give you higher values of either precision or recall, instead of using loss.
- Practically, performing modifications after one iteration of training has been completed is just impossible. Training ChatGPT *once over* takes months; can't expect to train it again with better hyperparameters. What do you do in that case?
- How do dropout and regularisation achieve the same results?
---
# Validating the Model
- Validation is a means to detect overfitting.
- When might overfitting happen? When the model begins to capture the noise present in the dataset alongside the signal.
- How to detect it? validation loss reaches a minima, and then starts *rising*. 
- A GAP between validation loss and training loss DOES NOT imply overfitting; it just implies that the validation data is more challenging to model than the training data.
--- 
# Confusion Matrix
- Accuracy doesn't convey everything about your model.
	- Consider a dataset with 90 cats and 10 dogs. This model classifies *everything* as cats.
	- This model would have an accuracy of 90%, but is obviously a very bad model.
- Precision and recall values are going to be calculated in a binary manner irrespective of how many classes are present in the dataset.
- You might want to optimise precision or recall depending on the situation.
	- (aside) these are only meaningful when accuracy ≠ 100%. If it IS 100%, both these values are just 1.
	- Examples: 
		- Precision more important for a face recognition model for your phone. You would rather have your phone misclassify you than unlock when someone else tried to use it.
		- Recall more important for a disease classification model; you would rather know that you have a disease when you don't have one that stay without knowledge and treatment.
- F1 score: combination (harmonic mean) of precision and recall; useful when you want to optimise in a 'mixed' manner.
	- Example: dog-cat classifier where you don't really care more about any one class.
- 
---
# Imbalanced Datasets
- If you can't justify having the imbalance, it is a very bad idea to have am imbalanced dataset.
- Your model will always be biased towards the class which has more samples. This won't mimic the distribution in the real world, and poorly impact performance.
---
# Regularisation
- What is regularisation? Adding a regularisation term to your loss function, with the aim to focus on the dataset signal while ignoring the noise.
- L2 regularisation - most common - encourages the weight values towards zero.
- L1 regularisation - harsher than L2.
- If you know your data has a lot of noise, prefer L1, else L2.
--- 
# Dropout
- During training, with some probability P a neuron gets turned off entirely, making the neural network simpler.
- This achieves the same end effect as regularisation.
---
# Momentum
- Idea: help push a model out of a local minimum by letting a previous weight update influence a later one.
- Adam optimiser - makes use of 'primary' and 'secondary' momentum. Consequently, it functions as an optimisation algorithm for gradient descent.
