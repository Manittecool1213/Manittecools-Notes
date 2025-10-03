# Notes
- Need to go through MobileNet paper and understand its block diagram.
- Need to read up on:
	- Depthwise convolution
	- Pointwise convolution
	- Inverted bottleneck block
- Novelty of approach - parallel Mobile and Former instead of serially using mobile before or after former.
### Ria
- Add flagpost for inverted bottleneck while explaining MobileNet
- Add content on main contributions of MobileNet
- Add content on LIMITATIONS of MobileNet (setting up MobileFormer)
- Introduction:
	- The paper we've chosen for our presentation is titled MobileFormer: Bridging MobileNet and Transformer by Chen et. al..
	- It was accepted at the Computer Vision and Pattern Recognition Conference (CVPR) in 2022.
	- Per the title, the high level idea of the paper is to combine the existing performant MobileNet with Transformers to simultaneously achieve high accuracy and token efficiency. 
	- Before we move on to the core solution design, I'll be giving a quick overview of MobileNet.
### Ananya
- Explain metrics before starting
- For graph, explain what is 'good' for graph (top left => better perf.)
- Compare to best in class (MobileFormer better than best CNN) (for word efficiency)
- Add content on: the authors only draw comparisons to models in the same class, i.e., token efficient models
### Manit
- Inverted bottleneck block
- Be more specific about what each bridge is doing
	- Be more clear about the Q-K-V being absent on mobile side