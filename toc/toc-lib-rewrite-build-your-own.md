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

- https://github.com/JokerLHF/tiny-library
  - 各种库的模拟实现, express, koa
# data-structure

- https://github.com/childrentime/mini-immer
  - create a minimal version of the immer library that illustrates the core principles of immer.

- [Mutable immutability: creating immutable objects with Immer clone | CKEditor](https://ckeditor.com/blog/immutability-with-immer-clone/)
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
  - 每个VNode的属性
    - selector: tag#id.className
    - data: any
    - children: VNode[]
    - text: string
    - elm: 每个VNode对应的真实dom节点
  - who is using #snabbdom
    - vue, owl1
  - Snabbdom consists of an extremely simple, performant and extensible core that is only ≈ 200 SLOC. 
  - It offers a modular architecture with rich functionality for extensions through custom modules. 
  - To keep the core simple, all non-essential functionality is delegated to modules.
  - 未使用event-delegation或synthetic
    - `elm.addEventListener(name, listener, false)` 直接操作dom
    - Snabbdom allows swapping event handlers between renders. This happens without actually touching the event handlers attached to the DOM
  - [Support custom elements 已支持](https://github.com/snabbdom/snabbdom/issues/141)
  - https://github.com/ged-odoo/blockdom
    - Owl framework 1.x is based on a fork of snabbdom
    - version 2 is not ready yet, but will be based on blockdom.
    - It features blocks, supports fragments, manage synthetic event handlers and more.
  - [Isomorphic snabbdom](https://github.com/snabbdom/snabbdom/issues/86)
    - I have put together a little starter kit that does SSR with snabbdom-to-html

- https://github.com/AFASSoftware/maquette /ts
  - simple virtual DOM library

- https://github.com/google/incremental-dom /ts
  - Incremental DOM is a library for building up DOM trees and updating them in-place when data changes. 
  - 👉🏻 It differs from the established virtual DOM approach in that no intermediate tree is created (the existing tree is mutated in-place). 
  - This approach significantly reduces memory allocation and GC thrashing
  - Incremental DOM is primarily intended as a compilation target for templating languages. 
  - Think of it as ASM.dom

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

- https://github.com/leaon4/mini-vue
  - 大概是最全的一个基于vue3的 mini-vue 实现了
  - 项目结构尽量还原 vue3 源码，只做主线任务
  - [从零开始写个mini-vue_bilibili](https://www.bilibili.com/video/BV1564y1s7s5/)

- https://github.com/JokerLHF/mini-vue3
  - 模拟vue3，实现了模板编译、创建组件实例、运行渲染函数、挂载虚拟 dom、接合响应式系统、patch 更新渲染、scheduler 任务调度， 基本上完成主线任务。
# more
- https://github.com/aosabook/500lines
  - https://aosabook.org/en/
  - This is the source for the book 500 Lines or Less, the fourth in the Architecture of Open Source Applications series.
  - 示例包括 spreadsheet、template-engine、crawler、server
