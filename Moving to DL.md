---
title: Moving to DL
draft: false
tags:
---
# Questions
- How did GoogleNet manage to match dimensions when using kernels of different sizes.
- Qualitatively, why does performance plateau and then degrade upon additional of too much depth.
---
# AlexNet
- Before AlexNet, features were modelled manually.
- Some design decisions surrounding architecture - empirical - likely no qualitative explanation (no explanation communicated in paper).
- Shift from average pooling to max pooling.
- Shift from sigmoid to ReLU activation.
- (aside) popular figure demonstrating AlexNet architecture has two 'branches' representing separation of computation on different GPUs.
- Large chunk of computation - comes from fully connected layers - because each parameter needs gradients from every one in the next layer during backprop.
---
# VGG 
- The 3x3 convolution kernel was popularised by VGG.
- The argument was: the area captured by a 5x5 kernel can be as well if not better captured by two consecutive 3x3 kernels.
- VGG also popularised: using convolution blocks, after which maxpooling was applied to reduce the size of the image.
- First paper to emphasise depth.
- Performance DEGRADED upon addition of too much depth.
---
# NIN
- Why use a 1x1 convolution?
	- Using an MLP on an image would need the image to be converted into a 1 dimensional vector.
	- This loss of dimensionality results in a loss of positional information which cannot be recovered when the processed output vector is converted back into an image.
	- The 1x1 convolution allowed the preservation of this positional information.
- Optimised for computational cost instead of quality.
--- 
# GoogleNet
- Made the decision to use multiple kernel sizes instead of choosing between them.
---
# ResNet
- Attempted to solve the degradation problem of convolution.
- Did this by adding skip connections, which would qualitatively 'allow simpler features to propagate to the later layers'.
---
# Batch Normalisation
- The output of a layer can differ significantly from its inputs if say a simple sum were performed. This would cause a lot of variation between output layers at different layers of the network. 
- To mitigate this, batch normalisation is used.
- The inputs to a neuron are normalised using an expression.
- The expression contains two learnable parameters to make the normalisation consistent with the entire dataset, considering that mean and variance computations are performed based on mini-batches instead.
---
# DenseNet
- Allowed skips across multiple blocks instead of just single blocks.
- Concatenated information instead of adding it.

