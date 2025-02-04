---
title: lib-collab-nanostores-dev
tags: [nanostores, state]
created: 2023-05-19T12:17:24.870Z
modified: 2023-06-02T23:14:54.641Z
---

# lib-collab-nanostores-dev

# guide
- who is using #nanostores
  - webstudio
  - standardnotes/app
  - open-ui
  - kiwicom/orbit
  - react-flow-editor
# dev
- memoize

- [done: Remove Proxy hack_202102](https://github.com/nanostores/nanostores/commit/c2a5e8042fe3487035727af175a87a84ebb27bf7)
# examples
- https://github.com/tiana-y/todos
  - Small project for training with React context and styled-components

- https://github.com/kseniaSs/react-flow-editor /ts
  - https://kseniass.github.io/react-flow-editor/
  - DnD multiple selected nodes with SHIFT
  - 依赖nanostores/react

- https://github.com/dkzlv/nanoform
  - form library for Nano Stores.
  - Only rerenders those fields that got updates.

- https://github.com/franjsb1903/weather-app
  - https://fran-saa-weather-app.vercel.app/
  - 简单天气

- https://github.com/FlaritV/nanostores-react-example
  - build custom simple router
  - 不依赖@nanostore/react

- https://github.com/v4irajvimu/nanostores-demo
  - counter，依赖多
# docs
- `atom` store can be used to store strings, numbers, arrays.
  - You can use it for objects too if you want to prohibit key changes and allow only replacing the whole object (like we do in nanostores/router).

- `map` store can be used to store objects with one level of depth and change keys in this object.

- `deepMap` work the same as map, but it supports arbitrary nesting of objects and arrays that preserve the fine-grained reactivity.

- A unique feature of Nano Stores is that every state has two modes:
  - Mount: when one or more listeners was mount to the store.
  - Disabled: when store has no listeners.
- Mount/disabled modes allow you to create lazy stores, which will use resources only if store is really used in the UI.
  - For performance reasons, store will move to disabled mode with 1 second delay after last listener unsubscribing.

- Action is a function which change the store.
  - It is a good place to move business logic like validation or network operations.
  - Wrapping functions with `action()` can track who changed the store in the logger.
  - This wrap allows DevTools to see the name of action, which changes the store.
# changelog

## [v0.9.0_20230525](https://twitter.com/sitnikcode/status/1661652304141983746)

- [Nano Stores 0.9](https://github.com/nanostores/nanostores/issues/172)

- New version will call subscribers only if store value was really changed (not on every `store.set()` call as it was before).
  - @IAmTrySound changed it to sync behavior across all frameworks (React’s useSyncExternalStore requires it) and improve performance
- In new versions we also introduced new code style with having `$` in store’s variables.
  - It will separate variable with store and with store’s value. But it is completely optional. For instance, this code style is not compatible with Svelte.

  ## [v0.8.0_202304](https://github.com/nanostores/nanostores/pull/161)
- Adding deepMap implementation
- TLDR: MapStore that's friendly to nested attributes and arrays.
- Main magic happens in our own naïve implementation of object-path getting/setting. 
  - It uses recursion to only change object reference (via structuredClone) for the object that has some changed keys. 
  - It only works with **plain objects and arrays**, not sets, maps, getters/setters and other stuff.

## [v0.5_202109](https://github.com/nanostores/nanostores/issues/57)

- Unclear terms: store to atom
- Fix Diamond problem
# more
