---
title: thread-lang-js-ts-types
tags: [lang, thread, typescript]
created: '2021-08-05T04:30:46.106Z'
modified: '2021-08-05T04:31:02.298Z'
---

# thread-lang-js-ts-types

# guide

- ## React TypeScript Cheatsheet
- https://github.com/typescript-cheatsheets/react
  - https://react-typescript-cheatsheet.netlify.app/docs/basic/setup

- more-cheatsheet
  - https://nerdcave.com/tailwind-cheat-sheet
# discuss
- ## 

- ## 

- ## Cross-fading any two DOM elements is impossible right now. Here's why
- https://twitter.com/jaffathecake/status/1462803936679763971
  - [Cross-fading any two DOM elements is currently impossible](https://jakearchibald.com/2021/dom-cross-fade/)
- The spec change has landed, and there's an implementation behind a flag in Chrome Canary!
- This is a good explanation of why there can be subtle opacity dips with Framer Motion's shared layout animations. We use opposing easing curves that keep the overall opacity as close to 1 as possible but something like this CSS rule would really help.

- ## Note to future self: this is the tsconfig you want for a library in a monorepo. Don't use `paths` to get types from other packages, use `references`!
- https://twitter.com/steveruizok/status/1464906551664250884
  - The reason for this is that you'll also want to run some code after build to replace the "~" paths with relative paths, but you don't want to replace imports from other packages in the repo (e.g. @monorepo/vec) with relative paths
- do you build with tsc or esbuild? I found that references only work with tsc and it's extremely slow
  - I do use esbuild! I only use tsc to generate type declarations.
- If the dep is meant to be published and depended upon - ye, it should still be defined as a dep in pkg.json

- ## Always publish `src` files, 
- https://twitter.com/__morse/status/1471169129478508551
  - if you use typescript you can also pass the `declarationMap` option to tsconfig to make cmd+click go to the original src file instead of the `.d.ts` file

- ## Using generics in @TypeScript beyond simple use cases becomes a massive deep dive into the variable/type dependency graph of any system it touches. 
- https://twitter.com/tannerlinsley/status/1476604095817404452
  - TLDR: If your types have circular dependencies, you will eventually have to short circuit your inference and pick a starting point.
- This is the primary reason why migrating JS libraries to TS is never a simple .js => .ts rename with added annotations. 
  - The Typescript compiler forces you to write code that can incrementally reason about the inferrable and knowable parts of the entire system
  - As you consume more generics, complexity grows linearly. If those generics begin to rely on each other or need to come in a specific order, the complexity skyrockets. And this is where the dependency graph of your vars/types comes in.
- In the case of #ReactTable, we need to know the shape of your row data, filterFns, sorters, aggregators, etc, before we can infer anything in your column definitions, which consume all of those types together. Columns also have value-based inference as well, 
  - So technically we need to know about your column accessor, too, before we let you configure anything else. 

- ## how to extract the generic type determined by a type guard function
- https://twitter.com/acemarke/status/1435731824303648771
  - type GuardedType<T> = T extends (x: any) => x is (infer T) ? T : never; 
- [Get the guarded type of a custom type guard](https://github.com/microsoft/TypeScript/issues/30542)

- ## TypeScript—I’ve switched:  From: `string[]` To: `Array<string>`

- https://twitter.com/rauschma/status/1431884615862603781
  – Better for complicated element types: Array<[string, number]>
  – Looks similar to other types.
  – Look similar to new `Array<string>()` which helps with type inference (default values, class field initializers).
- Definitely better readability. When you see `Array<number>` you read it from the start as "array of numbers".
- I used to prefer `Array<string>` for the same reasons but then switched to `string[]` because of readability in nested types. 
  - `Promise<Array<string>>`  vs `Promise<string[]>`
- After personally having strong opinions about code style in the past, I've learned that it's better to just align with common practices.
  - By applying common practices you will get a trained eye for it, which helps to read third-party code that most likely uses the same code style
  - Therefor I personally decided to just keep using `[]` for arrays.
  - Unless things really get error prone... like with tuple element type... in which case I will use `Array<..>` for an array.
- In the same way, prefer `Record<string, T>` over `{ [key: string]: T }` for key value objects with consistent key value types.
- Linters say to use [] though, so that's what I follow, simply so that the whole team can standardize on one model

- ## Specifying the type of this for functions
- https://stackoverflow.com/questions/44164032
- Following up on specifying the type of `this` in a class or an interface, functions and methods can now declare the type of `this` they expect.
  - By default the type of `this` inside a function is `any` . 
  - Starting with TypeScript 2.0, you can provide an explicit `this` parameter. 
  - `this` parameters are fake parameters that come first in the parameter list of a function
- Notice that `this` won't get translated into js, so it's not a real argument in the function.
- function f(this: void)  // make sure `this` is unusable in this standalone function

- ## how do people handle functions that can throw in typescript? 
- https://twitter.com/tmcw/status/1423404151149580292
  - half-considering starting to use an Either type of returning result | Error, don’t want to rely on just remembering which functions are throwy
- In majority of the cases it should be fine, but in some weird cases you might encounter some of the system errors `RangeError` or `TypeError` to name a few. Which makes me think exhaustively typing all the possible errors  is impossible.
- I would even recommend creating a simple `Err` class for the error side of it's a logical error and not an actual unrecoverable error. Switching our parser to our own error type was a massive perf boost (somewhere around 100x for us)

- ## how do you type a memoize function that accepts an arbitrary length of arbitrarily-typed arguments?
- https://twitter.com/Rich_Harris/status/1423023727680315392
  - we have a winner! guardian alumni network to the rescue 
  - `type Fn<T extends any[]> = (...args: T) => any; `
