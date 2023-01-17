---
title: lang-js-typescript-blog
tags: [blog, lang, typescript]
created: 2021-03-22T14:43:18.681Z
modified: 2021-03-22T14:43:44.781Z
---

# lang-js-typescript-blog

# guide

# blogs

## [tRPC: TypeScript performance lessons while refactoring for v10_202301](https://trpc.io/blog/typescript-performance-lessons)

- Automating library performance
  - it's important to keep an eye on performance as your library grows and changes. 
  - Automated testing can remove an immense burden from your library authoring (and application building!) by programatically testing your library code on each commit.
  - For tRPC, we do our best to ensure this by generating and testing a router with 3, 500 procedures and 1, 000 routers. 
- tRPC is not a runtime-heavy library so our performance metrics are centered around type-checking. 
- Therefore, we stay mindful of:
  - Being slow to type-check using tsc
  - Having a large initial load time
  - If the TypeScript language server takes a long time to respond to changes
- How I found performance opportunities in tRPC
  - There is always a tradeoff between TypeScript accuracy and compiler performance. 
  - TypeScript has a built-in tracing tool that can help you find the bottleneck in your types. It's not perfect, but it's the best tool available.
  - tsc --generateTrace ./trace --incremental false
  - You'll be given a `trace/trace.json` file on your machine. You can open that file in a trace analysis app (I use Perfetto) or `chrome://tracing`.
- Lazy evaluation
  - The problem here is that TypeScript is evaluating all of this code in the type system, even though it's not used immediately. 
  - TypeScript defers type evaluation of properties on objects until they are directly used, so theoretically our type above should get lazy evaluation...right?
  - Well, it's not exactly an object. There's actually a type wrapping the entire thing: OmitNeverKeys.
  - We need to find a way for the v10 API to adapt to the legacy v9 routers more gracefully. 

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
