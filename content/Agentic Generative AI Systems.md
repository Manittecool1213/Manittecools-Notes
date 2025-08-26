---
title: Agentic Generative AI Systems
draft: false
tags:
---
# Questions
- What is the mechanism for context storage in agents?
- How are the actions of an agent monitored and authority restricted?
- How really do agents 'adapt'? It's not as though they can structurally change. How do you prevent them from hallucinating and deviating from their assigned task? What can you safely do with an agentic system that you *couldn't* with deterministic code?
- What is the mechanism for the usage of LLMs in agents? Is it simply structured prompt passing?
- Is there a context sharing mechanism across different LLMs in an agentic system? My first query could involve node A, while a follow up could involve node B. How would node B get the context that node A has?
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
# Agents
- What are they? AI systems that an perceive, reason, act and adapt in a loop.
- No architectural changes at all - we're harnessing the power off LLMs to perform a certain task.
- Task modelled as a graph, with each node being an agent. Each of these agents communicate with each other.
	- Communication flow might be conditional. Some tool nodes / agents might only be invoked if a certain condition is met. For example, the SQL agent would only be invoked if the query required searching a database.
- (aside) context window problem - NP hard.
- Model context protocol - protocol to standardise communication and interaction between agents.
- Principle: Each node will perform a human *task*. The entire agentic system will perform a human *role*.
- Scalability in services:
	- Goal: to avoid global variables, i.e., make most containers stateless.
	- Why? If they're stateless, scaling horizontally is easy.
	- Some containers will still need to be stateful.