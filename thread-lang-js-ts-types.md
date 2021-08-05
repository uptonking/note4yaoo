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

- ## 

- ## 

- ## how do you type a memoize function that accepts an arbitrary length of arbitrarily-typed arguments?
- https://twitter.com/Rich_Harris/status/1423023727680315392
  - we have a winner! guardian alumni network to the rescue 
  - `type Fn<T extends any[]> = (...args: T) => any; `
