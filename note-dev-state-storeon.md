---
title: note-dev-state-storeon
tags: [dev, state]
created: '2020-11-01T18:29:13.989Z'
modified: '2020-11-01T18:30:30.758Z'
---

# note-dev-state-storeon

## guide

## docs

- ### [Storeon: “Redux” in 173 bytes](https://evilmartians.com/chronicles/storeon-redux-in-173-bytes)
- fully compatible with Redux DevTools.
- No one prevents you from placing your initial state, reducers, and business logic in a single module.
- Storeon checks which parts of the state were changed and re-renders only components subscribed to those changes.
- Trade-offs
  - Due to the way Storeon’s code is structured, it will be impossible to implement proper support for hot reloading, 
    - as Redux does by separating reloadable “pure” reducers and not-reloadable “impure” middleware. 
    - In Storeon, both reducers and middleware (or action creators) are implemented as event listeners in the same file.
  - state in Storeon must always be represented by a JavaScript object ({}) with no restrictions on data types for its keys. 
    - This assumption allows to track state changes directly and to avoid Redux-style selector functions altogether. 
    - In my experience, non-object state stores are rare anyway.
