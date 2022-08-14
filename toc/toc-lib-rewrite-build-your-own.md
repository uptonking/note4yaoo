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

- https://github.com/livoras/simple-virtual-dom
  - Simple virtual-dom algorithm. It has only ~500 lines of code
  - [深度剖析：如何实现一个 Virtual DOM 算法](https://github.com/livoras/blog/issues/13)
- https://github.com/Matt-Esch/virtual-dom
  - /10.8kStar/MIT/201604
  - A JavaScript DOM model supporting element creation, diff computation and patch operations for efficient re-rendering
- https://github.com/fantasticit/vdom
  - A simple basic implement of virtual-dom algorithm
  - [vdom 原理解析与简单实现](https://github.com/fantasticit/coding/issues/23)
  - 实际应用：https://github.com/spritejs/q-charts
- https://github.com/snabbdom/snabbdom
  - A virtual DOM library with focus on simplicity, modularity, powerful features and performance.
  - Snabbdom consists of an extremely simple, performant and extensible core that is only ≈ 200 SLOC. 
  - It offers a modular architecture with rich functionality for extensions through custom modules. 
  - To keep the core simple, all non-essential functionality is delegated to modules.
- more-vdom
# 3d-threejs
- Build your own react-three-fiber
  - https://codesandbox.io/s/build-your-own-react-three-fiber-zlq3c
  - The only issue is that events are blocking the render loop, but I'm not sure what's causing this.
