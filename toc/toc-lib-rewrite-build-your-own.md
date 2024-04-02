---
title: toc-lib-rewrite-build-your-own
tags: [repeat, rewrite, toc]
created: 2020-10-11T09:40:20.215Z
modified: 2021-09-29T13:23:09.969Z
---

# toc-lib-rewrite-build-your-own

# guide

- search: rewrite, alternative, clone
# catalog
- https://github.com/aosabook/500lines
  - https://aosabook.org/en/
  - This is the source for the book 500 Lines or Less, the fourth in the Architecture of Open Source Applications series.
  - 示例包括 spreadsheet、template-engine、crawler、server

- https://github.com/gouflv/build-my-own-x
  - 再次发明轮子, 重写常用api和工具库

- https://github.com/JinJieTan/Peter-
  - Peter的手写源码集合

- https://github.com/danistefanovic/build-your-own-x
  - https://github.com/codecrafters-io/build-your-own-x
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

# 3d-threejs
- Build your own react-three-fiber
  - https://codesandbox.io/s/build-your-own-react-three-fiber-zlq3c
  - The only issue is that events are blocking the render loop, but I'm not sure what's causing this.
# vue
- https://github.com/HiWayne/Self-Vue
  - 自己实现的vue监听数据变化和双向绑定源码，单文件

- https://github.com/themarcba/vue-reactivity /js
  - basic implementation of the Vue 3 reactivity engine - from scratch
  - 提供了分步实现思路

- https://github.com/bplok20010/vue-toy /ts
  - [vue-toy: 200行代码模拟Vue实现](https://my.oschina.net/nobo/blog/4310649)
  - 观察对象主要使用的是Object.defineProperty或Proxy来实现

- https://github.com/leaon4/mini-vue
  - 大概是最全的一个基于vue3的 mini-vue 实现了
  - 项目结构尽量还原 vue3 源码，只做主线任务
  - [从零开始写个mini-vue_bilibili](https://www.bilibili.com/video/BV1564y1s7s5/)

- https://github.com/JokerLHF/mini-vue3 /202204/ts
  - 模拟vue3，实现了模板编译、创建组件实例、运行渲染函数、挂载虚拟 dom、接合响应式系统、patch 更新渲染、scheduler 任务调度， 基本上完成主线任务。
  - 其中 compiler 并没有完成 vue3 的一系列优化

- https://github.com/Ubugeeei/chibivue /ts/代码多
  - https://ubugeeei.github.io/chibivue/en/
  - minimal Vue.js v3 core implementations (reactivity, virtual DOM, component, compiler (template, SFC))
  - This project began in February 2023 with the goal of simplifying the understanding of Vue's core implementation.
# react-ecosystem
- https://github.com/atlassubbed/atlas-relax /201904/js
  - Minimal, powerful declarative VDOM and reactive programming library.
  - This tiny 2.5KB (.min.gz) engine lets you define data-driven apps using declarative components. Relax combines ideas from Meteor, Mithril and Preact into one simple library.
  - https://github.com/atlassubbed/atlas-munchlax
    - Mobx clone
  - https://github.com/atlassubbed/atlas-mini-dom
    - React clone
# compiler
- https://github.com/jamiebuilds/the-super-tiny-compiler /202001/js/inactive
  - This is an ultra-simplified example of all the major pieces of a modern compiler written in easy to read JavaScript.
# more
- https://github.com/bradtraversy/vanillawebprojects /202311/js
  - https://vanillawebprojects.com/
  - Mini projects built with HTML5, CSS & JavaScript. No frameworks or libraries
  - This is the main repository for all of the projects in the course.

- https://github.com/pierregoudjo/build-your-own-excel /202308/ts/redux
  - A Javascript version of a talk showing how to build a simle version of Excel based on functional principles.
  - This javascript version use Preact and Redux with Typescript instead of Elmish and Fable with F#.
