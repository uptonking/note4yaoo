---
title: lib-editor-slate-blog
tags: [blog, slate]
created: '2022-05-15T21:14:02.900Z'
modified: '2022-05-15T21:14:14.339Z'
---

# lib-editor-slate-blog

# guide

# slate-blogs

## [Slate 介绍分析与实践](https://coldstone.fun/post/2020/12/13/slate-intro/)

- 特点
  - 插件作为一等公民，能够完全修改编辑器行为
  - 数据层和渲染层分离，更新数据触发渲染
  - 文档数据类似于 DOM 树，可嵌套
  - 具有原子化操作 API，理论上支持协同编辑
  - 使用 React 作为渲染层
  - 不可变数据结构 Immer

- 渲染原理
  - Slate的文档数据是一颗类似DOM的节点树，slate-react 通过递归这颗树生成 children 数组，这个数组有两种类型的组件 Element 和 Text， 最终 react 将 children 数组中的组件渲染到页面上
- 传递渲染函数 renderElement 和 renderLeaf 给 Editable 组件，对元素和叶子节点进行自定义渲染。

- 不足
  - 还没有发布正式版，处于 Beta 阶段，API 可能会有变化
  - 渲染层目前只有 React，要在其他框架中使用需要自行实现
  - 数据渲染分离，需要完全控制用户输入行为，否则可能导致数据和渲染不同步
  - 基于 contenteditable 无法突破浏览器的排版效果
  - 对中文输入支持不足，详见此 链接
  - 社区驱动开发，问题可能得不到及时修复

## [富文本编辑器 wangEditor v5 渲染逻辑 - Model ，DOM，HTML 三者的关系](https://juejin.cn/post/7055206586175717390)

> 暂不支持移动端。

- wangEditor v5 是基于 slate.js 为内核进行开发的，slate.js 输入输出的数据一直是 JSON 格式，没有 HTML 格式。所以，我也就基于这一点，一直坚持用 JSON 格式数据。
- slate.js 能基于 JSON 格式，本质原因是它完全依赖于 React 框架，使用 React 来渲染页面。而 React 本身就是一个“数据驱动视图”的框架，所以 slate.js 提供 JSON 作为数据，交给 React 来渲染视图，这很合理。
- 而 wangEditor 虽然基于 slate.js 为内核，但它没有基于 Vue React 等任何框架。既然没有框架要求，那就需要自己去考虑渲染逻辑，那也就需要 HTML 。
- 很不幸，HTML 格式就是“乱来”的代名词。
- 但是呢，对 HTML 的支持又是势在必行的，所以这个问题我想了好久，最终得出一个虽不完美但可行的方案：HTML 仅支持 wangEditor 输出的格式（包括 V4 和 V5），其他的格式就保证了。

- JSON 数据就是编辑器的 Model 。可以把编辑器认为是一个黑盒，输入输出的可以是 HTML ，但其内部数据是规定格式的 JSON 数据。
  - 现代富文本编辑器的 Model 都是基于一种 DSL 的，不会直接基于 HTML 。因为 HTML 格式过于灵活，不好控制，而自己的 DSL 是完全可控的。
- Model（即 JSON 数据）需要实时的渲染到编辑器视图中，即把 Model 渲染为 View 。而且不同的组件要渲染为不同的 DOM 类型
- 数据驱动视图，这一点和 Vue React 一样，所以我们也做了类似的设计：第一，把 Model 转换为 vdom ；第二，把 vdom patch 到真实 DOM 中（使用 snabbdom.js）
- 但是还要考虑各个组件渲染为不同的 DOM 类型，所以需要让各个模块注册自己的 Render 函数，再统一渲染。
# more-slate
- [slate-angular 正式开源 202106](https://zhuanlan.zhihu.com/p/382685492)
