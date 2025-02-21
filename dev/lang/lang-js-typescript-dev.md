---
title: lang-js-typescript-dev
tags: [dev, lang, typescript]
created: 2021-03-22T14:45:04.462Z
modified: 2021-03-22T14:46:25.568Z
---

# lang-js-typescript-dev

# guide

# dev-xp
- enum vs union
  - enum即可作为类型，也可作值
  - enum比字符串方便统一修改和重构
# tutorials
- [Type-Challenges解析 | 汪图南](https://wangtunan.github.io/blog/typescript/challenge.html)

## [Beginner's TypeScript by Matt Pocock](https://www.totaltypescript.com/tutorials/beginners-typescript)

- [Total TypeScript Essentials | Total TypeScript](https://www.totaltypescript.com/books/total-typescript-essentials)
  - https://x.com/mattpocockuk/status/1831317324743287075
  - I wrote a book. It takes you from zero TS experience to wizard-level

- https://github.com/total-typescript/beginners-typescript-tutorial
  - Take the course on Total TypeScript

- https://github.com/total-typescript/typescript-generics-workshop
  - Interactive tutorial on using generics in TypeScript  
# ts-play
- [TS Playground - An online editor for exploring TypeScript and JavaScript](https://www.typescriptlang.org/play/)

- [ts-blank-space playground](https://bloomberg.github.io/ts-blank-space/play/)
  - https://github.com/bloomberg/ts-blank-space /apache2/202409/ts
  - https://bloomberg.github.io/ts-blank-space/
  - small, fast, pure JavaScript type-stripper that uses the official TypeScript parser
  - It supports a modern subset of TypeScript by erasing the types and replacing them with whitespace. 
  - It is not a type checker and does not perform any other code transformations.
  - The implementation is pure TypeScript. It is simple enough to read and understand in a few minutes because it is only 700 lines of code and reuses the original TypeScript parser.
  - https://github.com/branchseer/oxidase
    - ts-blank-space inspired TypeScript type stripping implemented on OXC - strip TS types at the speed of parsing, 4x faster than swc_fast_ts_strip which is used in Node.js

- [tsplay.dev](https://tsplay-dev.vercel.app/)
  - tsplay.dev links will always redirect to the TypeScript Playground
# utils
- https://github.com/beenotung/live-tsc
  - A lightweight esbuild-based implementation of tsc that trim off the types (without type checking)
