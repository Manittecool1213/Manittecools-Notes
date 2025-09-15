---
title: Transfer Learning
draft: false
tags:
---
# Data Augmentation
- The manner in which augmentation is performed matters. 
	- e.g.: for a face recognition system, a vertical flip (lips above nose) might be *harmful* for the model, because the typical ordering of eyes-above-nose-above-lips is now reversed.
- Geometric transformations - rotating, scaling, cropping, etc.
- Photometric transformations - changing pixel and image parameters such as contrast, sharpness, blurring, etc.
- (aside) What is fundamentally different between generative and discriminative models?
	- Generative models have an ORGANISED latent / embedding space.
- Audio augmentation:
	- Noise injection
	- Shifting: shift left or right with a random number of seconds.
	- Changing speed of a stretch
	- Changing pitch
- Text data augmentation:
	- Word or sentence shuffling
	- Word replacement
	- Random word insertion
	- Random word deletion
---
# Transfer Learning
- What we're doing: copying weights of a pre-trained model, but training some layers (say output layer) from scratch on new dataset (with some initialisation, say random).
- Problem: the new feature representation might not be descriptive enough.
- Unfreezing more layers - obviously better.
- In case there's a large domain shift, say from images of dogs and cats to medical images, it is probably a good idea to train the model from scratch instead of using transfer learning. 
	- However, it has empirically been shown that starting from pre-trained weights yields better results than using some other initialisation strategy (ImageNet v/s Xavier example).
- Transfer learning - typically done with low learning rates.
- Availability of data also informs the decision of which transfer learning / fine tuning methodology is best.
### Domains of Datasets (need to read up more, pretty novel and pretty important)
- Domain is comprised of two elements:
	- Feature space
	- Marginal distribution, i.e., distribution of feature space elements in dataset.
- The 'task' can be modelled using a label space.
- Two datasets might differ in all of these - feature space itself might be different, feature space might be similar but marginal distribution might be different, label spaces might be different, etc.
- There exist different strategies for dealing with these mismatches:
	- When changing final few layers of convolution layer - we're assuming P(X_s) ≠ P(X_t).
	- We changing the MLP, we're assuming P(Y_s | X_s) ≠ P(Y_t | X_t) (very common).
- (aside) transfer learning is possible under a variety of scenarios - even when target labels are NOT available (need to read more on this).
- Should use this knowledge to decide which TL approach is best, instead of accuracy retrospectively justifying all choices. This is the difference between engineering a solution and understanding the approach used.