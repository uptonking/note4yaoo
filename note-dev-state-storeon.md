---
title: note-dev-state-storeon
tags: [dev, state]
created: '2020-11-01T18:29:13.989Z'
modified: '2020-11-01T18:30:30.758Z'
---

# note-dev-state-storeon

- event-based Redux-like state manager for React, Vue, Angular and Svelte.
  - The same Redux reducers.
  - 通过扩展可支持undo/redo
  - 不支持hot reload

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

## storeon-extension

- https://github.com/storeon/router
- https://github.com/storeon/undo
- https://github.com/octav47/storeonize
  - migrate from Redux to Storeon
- https://github.com/majo44/storeon-substore
  - Utility for creating feature sub store for Storeon
- https://github.com/mariosant/storeon-streams
  - Side effects management library for storeon
  - 依赖kefir

## storeon-repos

- https://github.com/andersonAncilon/storeon-to-do
- https://github.com/Youngestdev/storeon-app
  - [Event-driven state management in React using Storeon - note app_202006](https://blog.logrocket.com/event-driven-state-management-in-react-using-storeon/)
- https://github.com/takapro/react-counter
  - Example of counter with react, redux, reactn, storeon, and preact.
- https://github.com/ujinho/simple-exchanger
  - a yet another currency exchange app to perform conversion between USD, EUR
  - A storeon and react hooks playground.
- https://github.com/sovaai/chatKit-lib
  - react components that allows you to create dialog interface that interacts with a third-party service that provides the ability to interact with chat
  - Implemented with Storeon. You can see all content information in react dev tools.
- https://github.com/logux/state
  - Tiny state manager with CRDT, cross-tab, and Logux support
  - Logux is a new way to connect client and server. 
  - Instead of sending HTTP requests (e.g., AJAX and GraphQL) it synchronizes log of operations between client, server, and other clients.
- https://github.com/ilyalesik/weather-app
  - View layer: Preact
  - State management: Storeon
  - Bundler: Parcel
  - Styling: Reshadow + CSS Modules
- https://github.com/firstthumb/hsl-live-map
  - HSL Live Map that displays trams on map
  - 依赖react、styled-components、immutable4
- https://github.com/aki108/buff-up
  - 依赖react、styled-components、antd4
- https://github.com/rayriffy/nice-nut-november
  - 依赖react、next、tailwindcss、headless-ui
- https://github.com/sergiowalls/hackovid-web
  - 依赖react、blueprint
- https://github.com/Kuzmrom7/film-app
  - 依赖react，示例过于简单
- https://github.com/geralexgit/timerStack
  - Preact, Storeon, CSS Modules, PostCSS, Webpack 4
