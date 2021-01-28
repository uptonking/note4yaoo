---
title: thread-lang-js-ts
tags: [js, lang, typescript]
created: '2021-01-28T14:33:59.037Z'
modified: '2021-01-28T14:34:20.579Z'
---

# thread-lang-js-ts

# pieces

- ## 

- ## Using TypeScript without classes feels suboptimal, like I'm using it for something it wasn't designed for. TypeScript really shines with classes and static methods.
- https://twitter.com/BenLesh/status/1354541556234137600
- [To clarify: I'm not advocating programming with classes. ](https://twitter.com/mjackson/status/1354524449706414080)
  - I typically avoid them. There is 1 class in the codebase I'm currently working on, and it's a React class because there is no hook for React error boundaries 
  - I'm just saying, TypeScript seems designed for them.
- That's interesting.
  - I view TS as just a type system on top of JavaScript
  - Classes in TS are just interfaces.
  - TS is all just interfaces, types, and function signatures. 
  - In my head, the actual "class" is a runtime thing.
  - So functions and classes feel pretty much the same to me.
  - Totally agree with everything you said here. I think about it the same way.
  - But there are a few spots where I wish TS had better support for working with functions, like typing a whole module of functions, for example. I could easily do it w/ a class, but not w/ a module.
  - What is a "module of functions"?
  - Just talking about JavaScript modules. There is no way to type all the exports of a module in TypeScript.
  - namespaces are nice for that but unfortunately discouraged because of tree shaking issues (i think...)
  - referring to ECMAScript Modules.
  - Modules =/= Classes.  You can have a javascript file that exports only functions.
- I find it exactly the opposite. 
  - I use plain functions and values 90% of the time with TS and classes only when I really need to (mostly for perf). 
  - Generics are easier to manage with functions too.
  - I do the same thing. There are 0 classes in the codebase I'm currently working on, but sometimes it feels like things would be easier if there were. For example, typing a whole module would be easier using static methods on a class.
  - I don't see how this is different than just plain typed functions?
  - You can't get a type for the whole module, just each individual function.
  - 但是可以通过单独的文件专门导出一个文件中所有的export，虽然可行，但增加了文件数量
  - Clever, but there’s no way to open up a new module and say “this module is one of these” (ie implements an interface)
