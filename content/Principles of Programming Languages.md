---
title: Principles of Programming Languages
draft: false
tags:
---
# Questions
- What is the real purpose of Integer, etc. classes in java?
	- Supposedly, they allow 'better' type inference because of wrapping in a class.
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
---
- Separation ≠ independence. 
	- Example: being in college, we are separated from our parents but dependent on them.
	- How analogy translates into the technical world is unclear.
	- Hinted at class module v/s user module example, but still doesn't make any sense. The two modules are supposedly separated but DEPENDENT. Separation is obvious, but dependence is not at all so.
- Specialisation in OOP: we can create subclasses to add additional functionality to the class, which only some objects will be able to access.
- (aside) we are currently studying procedural OO; functional OO might be better (rant article).
---
### Execution v/s Simulation
- This is a discussion on *how* computation is modelled - either as truly executing the computation to be performed, or modelling some real world process as a simulation.
- In imperative / procedural programming, there is true execution. Every 'how' instruction is detailed.
- In pure OO, there is simulation. Computations are modelled as changes of state of objects.
---
### Pass by Reference v/s Pass by Address
- Passing by address is not the same as passing by reference, because the object is not really being 'referenced' in any manner. It's members are being directly accessed through its address. The user would be able to freely access all members of the object.
- Passing by reference would be through an objects ID. The user would only be able to access what the API exposes.
---
- If an object is passed by value, there needs to exist a copy constructor to copy the contents of the object at the time of the function call. After the function call, there needs to exist a destructor to free the memory used for the copy.
- TODO: what is 'static' in C v/s C++ v/s Java v/s Python.
	- See which symbolic names continue to exist (e.g. types, formal parameters, local variables) (NOT static function names, etc.).
- Distinction between procedure activation time and call time: true 'calling' occurs in the body of the called function (this is pretty shaky; need to read up). The manner in which the passed parameters are passed depends on the body of the callee.
- Order of operations:
	- compile time
	- procedure activation time
	- linking time
	- loading time
	- runtime