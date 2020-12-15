---
title: toc-lib-editorjs
tags: [editor, editorjs, toc]
created: '2020-11-17T13:37:09.407Z'
modified: '2020-11-17T13:38:27.686Z'
---

# toc-lib-editorjs

## text-editor

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

## plugins-editorjs

- https://github.com/yijian166/all-in-one-editorjs

- https://github.com/affandes/katex-editorjs
- https://github.com/affandes/image-editorjs

- https://github.com/jakekara/editorjs-footnotes
- https://github.com/hata6502/editorjs-inline
- https://github.com/hata6502/editorjs-style
- https://github.com/chanhha91/editorjs-title

## repos-editorjs

- https://github.com/codex-team/codex.notes
  - /81Star/MIT/202009/js/inactive
  - 依赖旧版codex.editor, graphql-request, electron-pug, nedb, tapable, winston
  - 开发不活跃
  - Write notes in WYSIWYG editor
  - Organize notes by folders
  - It integrates Editor.js and supports cloud backups of your notes.

- https://github.com/Jungwoo-An/react-editor-js
- https://github.com/jessypouliot98/advanced-react-input

- https://github.com/pavittarx/editorjs-html
  - parse editorjs clean data to html. 
- https://github.com/hata6502/editorjs-element
  - DOM event, CSS Style, etc may conflict each other when multiple Editor.js instances are launched in same page. 
  - By launching Editor.js in iframe, these problems are resolved forcibly. 
  - This repository provides the template of Editor.js in iframe.

- https://github.com/vikingcms/viking
  - The main repository for Viking CMS. Currently in Development.
