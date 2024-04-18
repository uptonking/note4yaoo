---
title: lib-editor-typewriter-dev
tags: [text-editor, typewriter]
created: 2023-02-09T12:24:05.159Z
modified: 2023-02-09T12:24:23.549Z
---

# lib-editor-typewriter-dev

# guide

- features
  - virtual render
  - collab

- 技术要点
  - 模型层TextDocument将Delta中的op数组按换行符拆分为blocks/lines数组
  - virtual-render只渲染指定区域内的元素
  - 默认render使用的是virtual dom
  - 选区同步基于浏览器的事件
  - 协作基于 json-patch + 简化版ot

- 渲染长文档的思路
  - virtualized render
    - 参考 ajaxorg/ace、codemirror、typewriter
    - 虚拟渲染能提高安全性?
  - defer render, 懒加载，viewport内才加载，按需请求再加载
    - 持久化分页后的数据，便可以按固定高度实现virtual render

- virtualized render cons
  - 影响浏览器自带的功能，如页面内查找
  - 锚点自动滚动，如生成标题目录toc，评论

- typewriter的delta结构就是一系列op集合和操作，非常类似经典OT算法
# dev
- typewriter /308Star/MIT/202301/ts
  - https://github.com/typewriter-editor/typewriter
  - A rich text editor based off of Quill.js and Ultradom, and using Svelte for UI.
  - 依赖 svelte、popperjs2、typewriter/delta
  - Built on the same data model as Quill.js, the Delta format, and using a tiny virtual DOM, Superfine, Typewriter aims to make custom rich text editors faster, easier, and more powerful
# changelog

## [prepare for 1.0 release _20210120](https://github.com/typewriter-editor/typewriter/pull/56)

- It's time to get Typewriter ready for a 1.0 release after a few years of indecisiveness on direction. This represents a major overhaul of the library after much learning.

- We are pivoting away from a monorepo with multiple packages back to a single package. 
  - This simplifies usage, the codebase, and deployment. 
  - We will have one npm package as before at `typewriter-editor` and `@typewriter/*` will be deprecated.
- As part of simplifying into 1 package, we've replaced `Paper` with the new `Typeset` interface which is similar and better named for what it represents. It combines the type definitions with their rendering and display information to simplify creation of new types for users.

- Instead of moving to a new Delta format or changing how newlines work in the existing Delta format, we are adding a new data format that builds on top of Delta and can be converted to and from Delta `TextDocument`. 
  - It just breaks Delta into lines and adds the selection information to the document. 
  - Deltas are still used in changes and for collaborative editing.

- To support atomic changes, we've added a `TextChange` class to encapsulate a single atomic change which could be a single character typed (along with the new selection) or a Replace-All operation on the document. This simplifies the events and history module.

- Since changes include selection info, we've simplified the events to a `changing` event (before a change is made and which can be canceled with `event.preventDefault()`) and a `change` event which is dispatched after the change is made. 
  - There is also a `changed` event which is dispatched after change to allow some things to respond after everything else has, though I don't anticipate this is needed by most.

- 👉🏻 We have moved user input, copy, paste, selection, rendering, and decorations, all into modules. `View` is no more. 
  - It turns out, very little is needed in the core editor and doing this allows these pieces to be replaced with custom implementations, such as replacing rendering with virtual rendering.

- A new keyboard module resolves Keyboard module? by both adding shortcut strings to the keydown event and handling basic editor input such as Enter & Delete.

- 👉🏻 We've moved back to using the browser `MutationObserver` for handling user input with a fallback to the `input` event for Firefox. 
  - This gives us the best support for text composition and the buggy Android GBoard keyboard which is default on most Android devices. 
  - But this is all handled in the input module which can be replaced as needed.

- 👉🏻 We've given up the dream of using Svelte to render the contents of the text editor, sticking with a small virtual DOM. 
  - This is part of the editor's core feature since Typesets include a function for rendering to the vDOM. 
  - The rendering module can be replaced, but it is assumed that all rendering will be done with the vDOM provided.

- And finally, we've embraced Svelte as the supported way to create UI for the editor and provided several renderless components which make it dead simple to add toolbars, hover menus, and inline menus. Recreating the Medium editor (which seems to be the thing to do) with the provided tools is very simple.
