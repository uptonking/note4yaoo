---
title: page-lang-js
tags: [js, lang]
created: '2020-08-28T07:27:16.385Z'
modified: '2020-08-28T07:27:31.736Z'
---

# page-lang-js

## Why I Don’t Use Classes

- [Why I Don’t Use Classes](https://spin.atomicobject.com/2020/03/12/why-i-dont-use-classes/)

- For context, my projects lately have been in full-stack Typescript, and what I value in writing software is highly influenced by the experiences in the Typescript ecosystem. 
- I also should note that I don’t actively avoid writing classes. 
- I just lean toward other solutions, typically functional solutions over object-orientated solutions

- I'm terrible at making good abstractions with classes. 
  - But typically, using inheritance and polymorphism to model a problem space evolves into a mess. 
  - First, classes end up having terrible method names if those methods are overriding base class methods. 
    - I’ve been fooled by too many method names that end up doing more than what they said they would.
    -  But I’ve found much more success creating groups of functions that don’t belong in a class. 
    -  And I can give them any name I want and split responsibilities into new functions as I please.
  - Secondly, I’ve noticed that classes have a tendency to grow large. 
    - They will collect pieces of functionality that need to live in the context of the class, usually to access the internal state of that class. 
    - This dependency on the internal state makes it difficult to break the methods up into logical chunks.
    - This usually isn’t a huge pain point, but teams I’ve been on have preferred using groups of functions in modules that have state passed to them. 
    - It tends to be easier to break large modules into smaller ones if needed.
- State contained and controlled by a class has been the cause of undesirably behaviors. 

- Alternatives to Classes
  - I like to use modules that expose groups of functions. 
  - These functions accept state and other dependencies. 
  - These modules tend to look like what my colleague Drew describes as the functional module pattern.
