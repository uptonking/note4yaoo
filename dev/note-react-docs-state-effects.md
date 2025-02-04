---
title: note-react-docs-state-effects
tags: [docs, react]
created: 2023-05-03T15:19:53.693Z
modified: 2023-05-03T15:20:18.719Z
---

# note-react-docs-state-effects

# guide

# docs

## [You Might Not Need an Effect – React](https://react.dev/learn/you-might-not-need-an-effect)

- In the above example,  `setSelection` is called directly during a render. 
  - React will re-render the List immediately after it exits with a `return` statement. 
  - React has not rendered the List children or updated the DOM yet, so this lets the List children skip rendering the stale selection value.
  - 💡 When you update a component during rendering, React throws away the returned JSX and immediately retries rendering. 
  - To avoid very slow cascading retries, React only lets you update the same component’s state during a render. 
  - Although this pattern is more efficient than an Effect, most components shouldn’t need it either. 
  - Always check whether you can reset all state with a key or calculate everything during rendering instead. 
