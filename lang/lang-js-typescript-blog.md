---
title: lang-js-typescript-blog
tags: [blog, lang, typescript]
created: 2021-03-22T14:43:18.681Z
modified: 2021-03-22T14:43:44.781Z
---

# lang-js-typescript-blog

# guide

# blogging

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
