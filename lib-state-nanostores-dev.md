---
title: lib-state-nanostores-dev
tags: [nanostores, state]
created: 2023-05-19T12:17:24.870Z
modified: 2023-05-19T12:17:49.983Z
---

# lib-state-nanostores-dev

# guide
- who is using #nanostores
  - webstudio
  - standardnotes/app
  - open-ui
  - kiwicom/orbit
  - react-flow-editor
# dev
- memoize

- [Nano Stores 0.9](https://github.com/nanostores/nanostores/issues/172)
# examples
- https://github.com/tiana-y/todos
  - Small project for training with React context and styled-components

- https://github.com/franjsb1903/weather-app
  - https://fran-saa-weather-app.vercel.app/
  - 简单天气

- https://github.com/FlaritV/nanostores-react-example
  - build custom simple router
  - 不依赖@nanostore/react

- https://github.com/v4irajvimu/nanostores-demo
  - counter，依赖多
# docs
- Action is a function which change the store.
  - This wrap allows DevTools to see the name of action, which changes the store.
# more

# discuss

- ## [How to work with nested objects?](https://github.com/orgs/nanostores/discussions/142)
  - `state.setKey(2, { ...state.get()[2], street: 'New' })`

- ## [Context](https://github.com/nanostores/nanostores/issues/171)
  - Problem 1: Cache API
  - Problem 2: SSR
    - In SSR, Node.js will render HTML for multiple users in the same time (in the same Node.js environment). If you just export store from a file, all users will share the same store. It could be a very dangerous.
    - the best solutions is to export store creators and not stores themselves. And then create a single instance in application root.
  - Problem 3: Mocks
  - Problem 4: DevTools
