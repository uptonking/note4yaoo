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

- ## how do people handle functions that can throw in typescript? 
- https://twitter.com/tmcw/status/1423404151149580292
  - half-considering starting to use an Either type of returning result | Error, don’t want to rely on just remembering which functions are throwy
- In majority of the cases it should be fine, but in some weird cases you might encounter some of the system errors `RangeError` or `TypeError` to name a few. Which makes me think exhaustively typing all the possible errors  is impossible.
- I would even recommend creating a simple `Err` class for the error side of it's a logical error and not an actual unrecoverable error. Switching our parser to our own error type was a massive perf boost (somewhere around 100x for us)

- ## how do you type a memoize function that accepts an arbitrary length of arbitrarily-typed arguments?
- https://twitter.com/Rich_Harris/status/1423023727680315392
  - we have a winner! guardian alumni network to the rescue 
  - `type Fn<T extends any[]> = (...args: T) => any; `
