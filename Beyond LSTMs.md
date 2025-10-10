---
title: LSTMs
draft: false
tags:
---
# Gated Recurrent Units
- Decision about whether or not previous hidden state is relevant made before output is calculated (rather *how relevant* is the old information).
- Exam perspective: clarify difference between element-wise product and dot product (read up on this as well).
- Difference between reset and update gates:
	- Reset gate: how much previous context is relevant.
	- Update gate: once you've made a new prediction, how much of it needs to be remembered in the future?
- Hidden state isn't really long term memory; it's just *memory*; it doesn't distinguish between old and new memory as such.
- GRUs end up performing the same function as LSTMs without as much compute required.
# Deep RNNs
- RNNs can be stacked depthwise too.
- Depth allows you to create a hierarchy of features. Localised context can be understood more systematically across layers.
- An RNN model which struggles temporally will seldom perform significantly better with depth, unlike CNNs.
- Deepest layer ultimately determines output.
- Example usecase: financial data, which has context on various scales (day, month, year, etc.).
# Bidirectional RNNs
- Humans mostly read language left to right, but there is no reason RNNs need to do the same. 
- BRNNs process language in both directions, and create an output based on both.
- These aren't stacked as much as they are parallel; you effectively have two separate RNNs getting input independently and both influencing output.
# CNN-LSTM Architecture
- Example usecase: video data (video classification).
- Need an encoder and CNN to process spacial context.
- Need LSTM to process temporal context.
- This still actually SPLITS information into space and time; this isn't truly spacio-temporal reasoning.
