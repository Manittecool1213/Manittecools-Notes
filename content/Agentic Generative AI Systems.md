---
title: Agentic Generative AI Systems
draft: false
tags:
---
# Introduction
--- 
### General / Econ Material
- Properties of the market landscape:
	- Large number of customers.
	- Large variation of usage between significant events.
	- Large variation in price points.
- CUDA made GPUs general purpose.
- Paradigms of intelligence:
	- Modelling the mind: logic, reasoning, etc - deterministic systems which don't learn.
	- Modelling the brain: neural networks which can learn.
- Search about: Geoffrey Hinton - 'godfather of AI'.
- LangChain - framework for writing generative applications.
	- Also look into LangGraph
---
### Technical Material
- Possible research direction: effective modelling of Indian languages (tokenisation, storage, etc.).
- Foundational Models solved learning problem:
	- A human being can learn to recognise birds with very few images. A model would need thousands.
	- If a _new_ animal was encountered, a human being would be able to learn this new information very quickly. A model would once again need thousands more.
	- But this problem doesn't exist to the same degree with foundational models. They are able to learn with far smaller magnitudes of data.
- Read up on: training LLMs in non-english languages. Were foundational models trained on english only? Can they perform translation? Does language even matter if at the end of the day a model is performing and embedding into a vector space?
- GPU Slicing:
	- GPU almost always sliced, and different slices used for different applications / processes.
	- It is the equivalent of virtualisation for GPUs; they're divided into smaller, isolable units.
	- If the required task would utilise the entire GPU, slicing would NOT be performed.
- Context windows:
	- In a chat with an LLM, you keep reprompting the LLM with the entire chat history. 
	- After the chat history reaches a certain length, it needs to be truncated. What remains is your context window.
---
