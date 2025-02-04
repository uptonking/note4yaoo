---
title: lib-editor-textbus-codebase
tags: [codebase, textbus]
created: 2023-02-20T22:11:09.750Z
modified: 2023-02-20T22:11:32.184Z
---

# lib-editor-textbus-codebase

# guide

# overview
- tips
  - 源码采用经典的oop风格，继承的层数很深，抽象复杂
  - 对编辑器底层框架抽象和业务开发抽象和主流编辑器产品有所不同，setup/hooks/slots
  - 获取Selection/Command要用依赖注入的方式 
    - const selection = editor.get(Selection)
    - const commander = editor.get(Commander)

- model层数据被封装为slot/component
  - 获取内容数据不直观
  - slots保存内容的数据结构类似quill的delta
  - 可通过editor.getHTML()分析model层数据

- view
  - 使用vdom的高性能渲染，基于细粒度缓存

- input
  - 不依赖contenteditable，自绘光标

- Commander
  - 通过自定义Event对象，然后触发全局eventCacheMap中注册过的事件
