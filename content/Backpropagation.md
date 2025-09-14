---
title: Backpropagation
draft: false
tags:
---
# Questions
- When using the ReLU function, the derivative would become zero in case of a negative pre-activation. Why should the dE/dW now become zero because of this?
---
- Goal: to associate 'blame' to each weight, and appropriately change it to reduce loss.
- How does backpropagation differ from the perception converge algorithm? We now have an activation function component in the derivative.
- Backpropagation allows parallelisation; every weight can be updated independently of every other.
- Because backpropagation expresses changes to weights in terms of inputs and outputs only, all weight change computations become independent of each other.