---
title: toc-lib-editor-text
tags: [lib, text-editor, toc]
created: 2021-07-27T15:11:58.769Z
modified: 2021-07-27T15:12:39.959Z
---

# toc-lib-editor-text

# known-text-editor

- prosemirror /6kStar/MIT/202208/ts
  - https://github.com/ProseMirror/prosemirror
  - http://prosemirror.net/
  - rich semantic content editor based on contentEditable, with support for collaborative editing and custom document schemas.
  - ProseMirror library consists of a number of separate modules.

- slate /18.6kStar/MIT/202009/ts
  - https://github.com/ianstormtaylor/slate
  - https://docs.slatejs.org/general/changelog
  - a completely customizable framework for building rich text editors.
  - since v0.50.0(201911), slate codebase has had a complete overhaul(彻底检修)
    - The data model is now comprised of simple JSON objects.(old: Immutable.js data structures)
    - Plugins are now plain functions that augment the Editor object they receive and return it again.
    - The codebase now uses TypeScript.

- textbus /648Star/GPL.v3/202208/ts
  - https://github.com/tbhuabi/textbus
  - https://textbus.io/collab
  - 依赖prismjs、~~rxjs~~、reflect-metadata、@tanbo/di、@tanbo/stream、@tanbo/color、katex
  - 依赖自研 @tanbo/stream，最基础的数据流类，每一次订阅产生一个新的数据流。
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
  - Textbus 2.0 已经到来
    - 重新设计了数据模型，可根据用户的操作生成特定的底层原子命令，这让细粒度的历史记录和文档协同成为可能
    - 重写了渲染层，现在 Textbus 2.0 大多数情况下更新视图仅需要 0.2ms 时间，比 1.0 性能更好
    - 核心架构脱离了具体平台，让 Textbus 的能力不仅限于在 PC 端，通过编写特定的中间层，可以方便的在移动端，甚至小程序上实现丰富的富文本能力
    - 重新设计了组件系统，去掉了大家难以理解的装饰器，改为用类似 vue 的 setup 形式开发组件

- editablejs-editable /17Star/MIT/202208/ts/只依赖slate不依赖slate-react/自绘光标
  - https://github.com/editablejs/editable
  - https://editor.aomao.com/
  - 一个实验性的富文本编辑器框架，希望通过自绘光标来替代原生 contenteditable 属性，提供更丰富、稳定的编辑能力。
  - 使用slatejs数据模型，借助 react 使用自绘光标的模式渲染，不再依赖 contenteditable 属性
  - 主要对一些 unicode 字符进行索引的计算。因为有些字符占位所占的字节数不确定，造成某些字符拆分后的索引不准确，所以需要这个工具包来解决这个问题。
- am-editor /541Star/MIT/202209/ts/maintenance
  - https://github.com/red-axe/am-editor
  - https://editor.aomao.com/zh-CN
  - 富文本实时协同编辑器框架，可以使用React和Vue自定义插件。
  - 协同编辑基于ShareDB实现。
  - 过去两年中，am-editor 编辑器基于 contenteditable 属性上做了很多功能和扩展，也遇到了很多问题。
    - 所以，现在大胆一些，尝试抛弃contenteditable属性，使用自绘光标的模式开发的下一个版本的富文本编辑器。

- taleweaver(织书) /71Star/MIT/202007/ts
  - https://github.com/yuzhenmi/taleweaver
  - https://yuzhenmi.github.io/taleweaver/
  - Web word processor for 2Tale Writer's Portal.
  - feature
    - 基于dom实现，且支持显示分页
  - core无依赖，react封装很少(只有2个文件)，不依赖prosemirror
  - 大量使用es6 class
  - 自己实现了依赖注入，设计了model/service/component
# collaborative-editor
- https://github.com/yjs/yjs
  - https://docs.yjs.dev/
  - Yjs is a CRDT implementation that exposes its internal data structure as shared types. 
  - Shared types are common data types like Map or Array with superpowers: changes are automatically distributed to other peers and merged without merge conflicts.

- https://github.com/josephg/reference-crdts
  - This repository contains simple proof-of-concept reference implementations of yjs, automerge and sync9's list types - all implemented in the same codebase. 

- https://github.com/YousefED/reactive-crdt
  - It's built on top of Yjs, a proven, high performance CRDT implementation.

- https://github.com/yjs/y-codemirror.next
  - https://demos.yjs.dev/codemirror/codemirror.html
  - Collaborative extensions for CodeMirror6
# open-editors
- wiz-editor /237Star/MIT/202207/ts/为知笔记
  - https://github.com/WizTeam/wiz-editor
  - 支持多人实时协同编辑的网页富文本编辑
# more-editor
- https://github.com/liferay/alloy-editor /ckeditor.v4
  - http://alloyeditor.com/
  - WYSIWYG editor based on CKEditor with completely rewritten UI
  - [Switch to CKEditor5 因为许可协议问题已放弃升级](https://github.com/liferay/alloy-editor/issues/618)

- https://github.com/jaredreich/pell
  - https://jaredreich.com/pell/
  - smallest WYSIWYG text editor with no dependencies
