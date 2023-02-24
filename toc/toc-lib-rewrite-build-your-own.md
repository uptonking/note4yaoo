---
title: toc-lib-rewrite-build-your-own
tags: [repeat, rewrite, toc]
created: 2020-10-11T09:40:20.215Z
modified: 2021-09-29T13:23:09.969Z
---

# toc-lib-rewrite-build-your-own

# guide

- https://github.com/gouflv/build-my-own-x
  - 再次发明轮子, 重写常用api和工具库

- https://github.com/JinJieTan/Peter-
  - Peter的手写源码集合

- https://github.com/danistefanovic/build-your-own-x
  - Build your own (insert technology here), listing examples
  - 3D Renderer, database, react, redux, git, Neural Network, Physics Engine, Regex Engine
  - Web Server, package manager
  - Programming Language, Operating System, Search Engine
  - Text Editor(c/cpp/python/ruby)

- https://github.com/iampava/steal-like-a-dev
  - Tutorial series focused on implementing from scratch popular packages/libraries.
  - create-react-app, react-router, react-redux, redux-thunk, styled-components
# web

## vdom

- [如何理解虚拟DOM](https://www.zhihu.com/question/29504639)

- https://github.com/livoras/simple-virtual-dom /js
  - Simple virtual-dom algorithm. It has only ~500 lines of code
  - [深度剖析：如何实现一个 Virtual DOM 算法](https://github.com/livoras/blog/issues/13)

- https://github.com/fantasticit/vdom /js
  - A simple basic implement of virtual-dom algorithm
  - [vdom 原理解析与简单实现](https://github.com/fantasticit/coding/issues/23)
  - 实际应用：https://github.com/spritejs/q-charts

- https://github.com/snabbdom/snabbdom /ts
  - A virtual DOM library with focus on simplicity, modularity, powerful features and performance.
  - Snabbdom consists of an extremely simple, performant and extensible core that is only ≈ 200 SLOC. 
  - It offers a modular architecture with rich functionality for extensions through custom modules. 
  - To keep the core simple, all non-essential functionality is delegated to modules.

- https://github.com/AFASSoftware/maquette /ts
  - simple virtual DOM library

- https://github.com/Matt-Esch/virtual-dom /10.8kStar/MIT/201604/js
  - A JavaScript DOM model supporting element creation, diff computation and patch operations for efficient re-rendering

- https://github.com/patrick-steele-idem/morphdom /js
  - Fast and lightweight DOM diffing/patching (no virtual DOM needed)
  - Instead of replacing the existing DOM tree with a new DOM tree, we want to transform the existing DOM tree to match the new DOM tree while minimizing the number of changes to the existing DOM tree. This is exactly what the morphdom module does! 
  - Because morphdom is using the real DOM, the DOM that the web browser is maintaining will always be the source of truth.

- https://github.com/trueadm/t7 /js
  - lightweight JavaScript template library that compiles ES2015 template strings into virtual DOM objects.
# 3d-threejs
- Build your own react-three-fiber
  - https://codesandbox.io/s/build-your-own-react-three-fiber-zlq3c
  - The only issue is that events are blocking the render loop, but I'm not sure what's causing this.
# vue
- https://github.com/HiWayne/Self-Vue
  - 自己实现的vue监听数据变化和双向绑定源码，单文件
