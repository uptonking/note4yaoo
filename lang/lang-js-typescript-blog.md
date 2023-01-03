---
title: lang-js-typescript-blog
tags: [blog, lang, typescript]
created: 2021-03-22T14:43:18.681Z
modified: 2021-03-22T14:43:44.781Z
---

# lang-js-typescript-blog

# guide

# blogs

## [11 Tips That Make You a Better Typescript Programmer_202212](https://dev.to/zenstack/11-tips-that-help-you-become-a-better-typescript-programmer-4ca1)

#1 Think in {Set}
#2 Understand declared type and narrowed type
#3 Use discriminated union instead of optional fields
#4 Use type predicate to avoid type assertion
#5 Control how union types are distributed
#6 Use exhaustive checking to catch unhandled cases at compile time
#7 Prefer type over interface
#8 Prefer tuple over array whenever appropriate
#9 Control how general or specific the inferred types are
#10 Use infer to create extra generic type parameters
#11 Stay DRY by being creative with type manipulation

## [JS classes are not “just syntactic sugar”](https://webreflection.medium.com/js-classes-are-not-just-syntactic-sugar-28690fedf078)

- es6 class features
  - Strictly guarded by default
  - Builtin Extends
  - Species
  - The super
  - Methods
  - Enumerability
  - Arrows
  - Privates

- Summary
  - there are many things that could be simulated via ES5 and old prototypal inheritance, but none of these come out of the box, are as fast, or as safe, as using appropriate syntax for classes and, 
  - on top of that, there are things that are just not possible with prototypal inheritance.

- Do you have resources explaining how JS classes are not syntactic sugar?
  - The spec has some differences:
  1. A class constructor can't be called without new.
  2. Class methods are have their enumerable flag set to false.
  3. The internal flag [[FunctionKind]] has the value "classConstructor".
  4. "use strict" by default.
