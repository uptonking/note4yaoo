---
title: thread-lang-js-ts-stars
tags: [js, lang, thread, typescript]
created: '2021-06-22T11:54:15.957Z'
modified: '2021-06-22T11:54:44.506Z'
---

# thread-lang-js-ts-stars

# pieces

- ## 

- ## 

- ## 

- ## don't let friends write JS functions with multiple optional parameters, each of which can have multiple overloaded values and behaviors
- https://twitter.com/acemarke/status/1409971795894181904
  - this tweet brought to you by me looking at the `connect` implementation for the first time in a while and my mind boggling at how the `mapState/mapDispatch` overload detection behavior is implemented
- All JavaScript functions should only be allowed to take one argument
  - you already do this in @Reactjs as "props" 
- When I got started with JS, I treated jquery's design as the ideal and made functions with lots of different overloads and argument shortcuts.
  - First awkwardness was when I had to make some wrapper functions around these and it was pain making the wrappers support parsing the args the same way. 
  - It's a solvable problem, but it was effort for a design that had other downsides too. Sometimes you have to judge whether it's worth it to solve a problem versus just removing the problem.
- I’m increasingly close to adding a lint rule that forces all function definitions to have 0 or 1 param. Object definitions are cheap enough that I don’t see much a reason to have multiple function params
  - 0 or 1 required, 1 optional (often boolean), is my empirical limit

- ## What's the best way to dynamically import an npm package on the client-side? Like in documentation code playgrounds.
- https://twitter.com/diegohaz/status/1409278109573160960
- By appending a script at runtime. Use something like react helmet
- Perhaps dynamically replace the imports with links to a CDN like https://skypack.dev ?

- ## named exports exports a dynamic reference to the variable being exported, 
- https://twitter.com/yagopereiraaz/status/1406974989203611654
  - default exports only export the current value of the variable at the time of import.
- This is intentional in the spec.
  - `export default <expr>` snapshots the value of `<expr>` as if it were a new constant binding
  - `let x = 1;  export { x as default }` results in x becoming a live binding for the default export
- I very rarely use default exports as they don't play so well with refactoring tooling. This feels like another reason to double down on that choice!
  - I wrote a short (internal) article to prefer named exports. 
  - In particular, as an alternative to the common pattern of having a default exported object that contains all the functions you want to expose.
  - So far it seems uncontroversial.
- Please tell me you titled it "default exports considered harmful"
  - Unfortunately it's just a preference so doesn't deserve such a famous label.
- is this why you can't default export a declaration? example: export default const hello = 'world'; 
- Default exports de-sugar roughly to the below, which is why incrementing num has no effect. It's assignment by value, not reference.(Invalid syntax since you can't name an export "default", but you get the point).
  - `export const default = num'` 类似
- Same if you actually define a function at the module to update the variable thats being exported. Defaults exports are immutable, it seems
