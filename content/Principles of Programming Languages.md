---
title: Principles of Programming Languages
draft: false
tags:
---
# OOP
- Objects should be entities with a generic name: this generic name should invoke the same understanding in all users' minds.
- The definitions of object and class are both bottom up and recursive. They refer to each other. Objects and classes are only meaningful when both are used together.
---
### Fundamental Properties of Objects
- Independence:
	- Intrinsic properties of an object that need clear expression without reference to some aggregate whole.
	- e.g.: position of a number in a sorted array is NOT an independent property; it is dependent on the other objects in the array.
- Uniqueness: some intrinsic properties of an object should distinguish it from others.
---
- In procedural programming, the core idea is that procedures will solve problems. In OOP, it is now the object which is responsible for solving problems.
- Classes can be thought of as storage structures to which methods have been bound. 
- In functional programming languages, these methods are not *stored* with the objects. The linking of method and data occurs at runtime (the compiler does not know whether a method is part of a class). This could potentially lead to the user incorrectly using the method, which is the problem we aim to solve with OOP.
---
### Designing by Modelling
- 'All models are false, some are useful'.
- It is impossible to model every aspect of anything we are planning to work with. We include some elements and create a model. 
- This implies that we have already created an abstraction (the model itself) before we design on top of it. This abstraction represents our understanding of what we're trying to build *before* we've even built it.
---
- Using the procedural paradigm is inevitable. Even with an OO language, the methods associated with objects MUST be modelled procedurally.
- In the procedural paradigm, methods were referenced by address. In OO, we want to reference methods by their names and properties to perform dynamic binding.
---
### Binding / Linking
- Four distinct elements:
	- Names: 
		- Primary components of the program / structural elements.
		- Their unique existence is retained and used for execution by the compiler, etc.
	- Declarations
	- Locations
	- Values