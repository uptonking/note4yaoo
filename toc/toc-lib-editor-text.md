---
title: toc-lib-editor-text
tags: [lib, text-editor, toc]
created: '2021-05-14T10:28:05.856Z'
modified: '2021-05-14T10:28:38.524Z'
---

# toc-lib-editor-text

# guide

- monaco-editor-pros
  - 来自vscode，代码编辑功能强大，有大公司支持
  - 支持 language server protocol

- monaco-editor-cons
  - 设计目标是ide，而不是纯粹的代码编辑器
  - 不支持mobile
  - 引入项目比较麻烦，不能直接简单的import，webpack要使用专门的plugin，如cra无法直接使用

- ref
  - [codemirror6 vs prosemirror vs editorjs](https://www.npmtrends.com/@editorjs/editorjs-vs-@codemirror/state-vs-prosemirror-state-vs-monaco-editor-vs-codemirror)

# text-editor

- https://github.com/ProseMirror/prosemirror
  - http://prosemirror.net/
  - /5.1kStar/MIT/202002/js
  - rich semantic content editor based on contentEditable, with support for collaborative editing and custom document schemas.
  - ProseMirror library consists of a number of separate modules.

- https://github.com/tbhuabi/textbus
  - /150Star/GPL/202011/ts
  - 依赖prismjs、rxjs、reflect-metadata、@tanbo/di, @tanbo/css-themes, @tanbo/color
  - 基于数据驱动的富文本编辑器
  - 为什么我还要另起炉灶呢？
    - 目前大多数富文本内容都太脏了，比如，加粗一段文字，可能是一个 strong 标签，也有可能是多个，如果这段文字同时还有其它格式，那么就更热闹了
    - 较新的编辑器，基本都有自己的一套抽象数据结构来描述富文本，这同时又引起了另一个问题，即这一数据结构对有的富文本内容描述不了，导致要扩展特定的格式不能实现。
    - 部分富文本编辑器依赖特定的框架或库，造成使用上的限制
    - 实时的代码高亮，这个对程序员写文档来说，比较重要
    - 对于粘贴进来的内容，要么粗爆的只是提取文本内容，导致格式丢失。要么就直接扔进页面，产生非常多的脏数据（如粘贴 word 的内容）
  - TextBus 解决如下
    - 输出非常干净，没有冗余的标签及样式。
    - 没有定义一个标准的数据结构，只抽象出了 Formatter（格式） 和 Component（组件）两个维度的数据来格式化富文本的 Content（内容）
    - 不依赖特定的库
    - 实时代码高亮
    - 由于TextBus的架构设计天然的支持过滤脏内容，所以，当粘贴进 TextBus 不认识的数据时，会自动忽略掉
    - 粘贴进来的资源上传，目前正在开发中

# code-editor

- https://github.com/codemirror/CodeMirror
  - /21.3kStar/MIT/202010/js
  - In-browser code editor
  - CodeMirror 6 is a rewrite of the CodeMirror code editor. 
  - The new system provides solid accessibility, touchscreen support, better content analysis
  - It is not API-compatible with the old code.

- vscode-monaco-editor

# collaborative

- https://github.com/yjs/yjs
  - https://docs.yjs.dev/
  - Yjs is a CRDT implementation that exposes its internal data structure as shared types. 
  - Shared types are common data types like Map or Array with superpowers: changes are automatically distributed to other peers and merged without merge conflicts.

# more-editor

- https://github.com/liferay/alloy-editor
  - http://alloyeditor.com/
  - WYSIWYG editor based on CKEditor with completely rewritten UI
