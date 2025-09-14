---
title: Lab Notes
draft: false
tags:
---
 
The rest of your content lives here. You can use **Markdown** here :)
# Questions
- Why bother with validation at all? Why not use testing data for it, considering training is not performed on validation data?
- What are optimisers? What do they do?
---
# Lab 1: Syntax, Classification and Regression, Softmax
- Validation - used while training itself. Dataset needs to be split into training, testing AND validation sets.
	- Validation might be an indicator of overfitting. If training loss continues to decrease, while validation loss doesn't, the model is overfitting instead of learning.
- While performing training, loss is the most important metric, not accuracy.
- What differentiates classification from regression? Softmax. Softmax performs the requisite thresholding for confidence score computation.