---
title: note-react-preact-codebase
tags: [codebase, preact]
created: 2021-06-20T13:25:16.180Z
modified: 2021-06-20T13:25:39.488Z
---

# note-react-preact-codebase

# guide

- who is using #preact
  - tui.grid
  - algolia-autocomplete
  - blocky-editor
# examples
- https://github.com/zouhir/preact-phiber /MIT/201704/js
  - https://preact-phiber.netlify.com/
  - 3kb alternative to React Fiber with the same API
  - Preact Phiber allows you to render components in streamable chunks so that a component, its children, its aunts and uncles, its first, second cousins, and its maternal grandparents can load asynchronously.
- https://github.com/CodyJasonBennett/preact-reconciler /MIT/202307/ts
  - Custom renderers for Preact in <1KB.
  - This package implements react-reconciler which allows for custom renderers to be implemented and shared between Preact and React such as @react-three/fiber.
# codebase-blog

## 🆚️ [Differences to React – Preact Guide](https://preactjs.com/guide/v10/differences-to-react)

- Preact is not intended to be a reimplementation of React.
  - The reason Preact does not attempt to include every single feature of React is in order to remain small and focused 
  - `preact/compat` is a thin layer over Preact that attempts to achieve 100% compatibility with React.

- The main difference between Preact and React is that Preact does not implement a synthetic event system for size and performance reasons. 
  - Preact uses the browser's standard `addEventListener` to register event handlers
- Another notable difference is that Preact follows the DOM specification more closely. 
  - Custom elements are supported like any other element, and custom events are supported with case-sensitive names (as they are in the DOM).

- [async rendering · Pull Request · preactjs/preact](https://github.com/preactjs/preact/pull/3386)
  - async rendering is not a new concept. It's similar to React Fiber but the implementation is quite different
  - [Preact Async Rendering: Solution to Initial Render Blocking - DEV Community _202201](https://dev.to/cagdas_ucar/preact-async-rendering-51p2)

## [从Preact中了解React组件和hooks基本原理_荒山_201909](https://juejin.cn/post/6844903861434449933)

- 本文代码基于 Preact v10 版本
- 代码有所简化，忽略掉 svg、replaceNode、context 等特性

## [The Zen of Preact's source code_202105](https://puruvj.dev/blog/deep-dive-into-preact-source-code)

- Preact's source code is written in TypeScript, but the main files themselves aren't. 
  - The main files with the functionality are written in plain JavaScript, 
  - but they use JSDoc to pull in Types from TypeScript Definition files (.d.ts).
- There's a whole article about Using TypeScript without TypeScript, 
  - but the TLDR; here would be: Avoid development time tooling. 
  - If its just plain JS, you don't need to run a file watcher to transpile files as you change them. Just run what you got.
  - This is a very interesting approach and I see more and more libraries take it up, especially non-UI libraries
  - For UI libraries, you already got a web server running, so adding in TypeScript in the tooling won't change much, go ahead and add TypeScript

- Preact's source code is very very well written and commented, as you'd expect from such a paramount(最重要的；最重大的) framework.
  - One of the reasons Preact is so small is that it reuses it's own exported function in its other exported functions.
- Preact is quite a big library to cover in a blog post, so I'll just cover the interesting parts.

- Notable points: `h`, which is Preact's JSX factory, is actually named `createElement`. Just like `React.createElement`. 
  - But is exported as `h` because it allows you to write raw Preact(Without JSX), also because it was initially inspired from HyperScript 
- `ref`s in P/React are basically used to encapsulate values that shouldn't trigger re-renders and are not re-created on every re-render.
  - A `ref` is just an object with `current` property set to `null`.
- Consumer expects its children to be a function, and it's simply calling it with the context data. 
  - As for Provider, what it's doing mostly is modifying its parent component's lifecycle hooks to watch for context state changes.

- Hooks are located in a separate directory. 
  - Unlike React, everything is opt-in in Preact
- `useState` is basically calling `useReducer`.
  - `const useState = (initialState) => useReducer(invokeOrReturn, initialState); `.
- `useCallback` is just useMemo under the hood
  - `const useCallback = (callback, args) => useMemo(() => callback, args); `.
