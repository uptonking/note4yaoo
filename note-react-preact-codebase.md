---
title: note-react-preact-codebase
tags: [codebase, preact]
created: 2021-06-20T13:25:16.180Z
modified: 2021-06-20T13:25:39.488Z
---

# note-react-preact-codebase

# guide

# codebase-blog

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

- Preact's source code is very very well written and commented, as you'd expect from such a paramount framework.
  - One of the reasons Preact is so small is that it reuses it's own exported function in its other exported functions. A LOT
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
