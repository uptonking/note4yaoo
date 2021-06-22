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

- ## 

- ## 

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
