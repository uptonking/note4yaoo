---
title: note-dev-state-storeon
tags: [dev, state]
created: '2020-11-01T18:29:13.989Z'
modified: '2020-11-01T18:30:30.758Z'
---

# note-dev-state-storeon

- event-based Redux-like state manager for React, Vue, Angular and Svelte.
  - The same Redux reducers.

## guide

## docs

- ### [storeon-counter-app-demo](https://github.com/storeon/storeon)

``` JS
import { createStoreon } from 'storeon';

// Initial state, reducers and business logic are packed in independent modules
let count = store => {
  // Initial state
  store.on('@init', () => ({ count: 0 }));
  // Reducers returns only changed part of the state
  store.on('inc', ({ count }) => ({ count: count + 1 }));
}

export const store = createStoreon([count]);

import { useStoreon } from 'storeon/react';

export const Counter = () => {
  // Counter will be re-render only on `state.count` changes
  const { dispatch, count } = useStoreon('count')
  return <button onClick={() => dispatch('inc')}>{count}</button>
}

import { StoreContext } from 'storeon/react';

render(
  <StoreContext.Provider value={store}>
    <Counter />
  </StoreContext.Provider>,
  document.body
)
```

- ### api
- `export const store = createStoreon([projects, users])`
  - store.get() 
    - will return current state. The state is always an object.
  - store.on(event, callback) 
    - will add an event listener.
  - store.dispatch(event, data) 
    - will emit an event with optional data.

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

## storeon-repos

- https://github.com/sovaai/chatKit-lib
  - react components that allows you to create dialog interface that interacts with a third-party service that provides the ability to interact with chat
  - Implemented with Storeon. You can see all content information in react dev tools.
- https://github.com/mariosant/storeon-streams
  - Side effects management library for storeon
  - 依赖kefir
- https://github.com/logux/state
  - Tiny state manager with CRDT, cross-tab, and Logux support
  - Logux is a new way to connect client and server. 
  - Instead of sending HTTP requests (e.g., AJAX and GraphQL) it synchronizes log of operations between client, server, and other clients.
- https://github.com/octav47/storeonize
  - migrate from Redux to Storeon

## ref
- [Event-driven state management in React using Storeon - note app_202006](https://blog.logrocket.com/event-driven-state-management-in-react-using-storeon/)
  - https://github.com/Youngestdev/storeon-app
