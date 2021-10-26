---
title: lib-editor-blog
tags: [blog, editor]
created: '2021-05-13T04:44:23.155Z'
modified: '2021-05-13T04:44:39.320Z'
---

# lib-editor-blog

# guide
- tldr: Unless browsers will open for the Web multiple crucial features (such as IME, keyboard, selection, touch, on-screen keyboard, spellchecker, etc.) contentEditable is the only sane way to handle text editing.

- contenteditable gives you one very important feature that you can't fake yourself: access to the browser's spell check and corrections
- Yep, we do use contentEditable as an input source and also as the view to which we render (you wouldn't be able to reliably handle the keyboard otherwise).
# repeat

## [ContentEditable  —  The Good, the Bad and the Ugly_201508](https://ckeditor.com/blog/ContentEditable-The-Good-the-Bad-and-the-Ugly/)

- ### ContentEditable is evil and the Selection API is its evil twin. Avoid them as much as possible. 
- You need a custom selection system. 
  - It must be doable nowadays to get position (represented by a range, but we’ll simplify this in a moment) in the DOM on mousedown/mousemove. 
  - You’ll display your custom caret (whoa… you can control its style now) and text selection (it’s a simple ).
- You need to handle typing. 
  - Let’s listen to the keyboard events and insert given character into the editor.
- You need to handle navigation using the Arrow keys. 
  - Left and right seem easy, up and down a bit trickier but if you have point 1, you’ll do this too. 
  - Wait, there’s the Alt modifier which makes the Left and Right Arrow keys jump entire words. 
  - But of course you’ll look for spaces in the text and that’s it — told you, it’s trivial!
- Then you need to do something with pasting. 
  - You see that with the Clipboard API you can listen to the paste event on the document and retrieve the data from the data transfer. 
  - You can also use the old paste bin mechanism.

- ### ContentEditable — the Good Parts
- It’s amazing that adding one attribute to an HTML element enables typing, selection, keyboard navigation, spell checking, drag and drop, pasting, undo manager. 
  - That all of this is integrated with the OS, 
  - that such editor can be used with a screen reader or on a touchscreen device 
  - and that it’s well internationalised. 

- ### CKEditor
- Over the past years, while working on CKEditor I noticed that we were gradually replacing native features with our own implementations. 
- Since version 4.0, CKEditor has its custom “insert HTML into selection” mechanism and a feature allowing reaching non-editable places.
- CKEditor 4.1 introduced highly customisable content filtering (no more mess on paste). 
- CKEditor 4.3 brought support for non-editable islands with editable islands inside which required overriding many native systems (selection, keyboard, focus, clipboard).
- Finally, just a few weeks ago we made a final takeover of the clipboard, which means that in some browsers copy, cut and paste operations are fully handled by CKEditor.
- It means that today CKEditor does not let the browser do anything to the content except handling typing, some deleting and that’s basically it. 
  - At the same time, it still uses the native selection system, keyboard navigation and other APIs such as those related to clipboard or focus management.

- With CKEditor 5 we are planning to conclude this process by letting the browser insert text only, but with CKEditor’s control.
# blogging

## [Slate 介绍分析与实践](https://coldstone.fun/post/2020/12/13/slate-intro/)

- 特点
  - 插件作为一等公民，能够完全修改编辑器行为
  - 数据层和渲染层分离，更新数据触发渲染
  - 文档数据类似于 DOM 树，可嵌套
  - 具有原子化操作 API，理论上支持协同编辑
  - 使用 React 作为渲染层
  - 不可变数据结构 Immer

- 渲染原理
  - Slate的文档数据是一颗类似 DOM 的节点树，slate-react 通过递归这颗树生成 children 数组，这个数组有两种类型的组件 Element 和 Text， 最终 react 将 children 数组中的组件渲染到页面上
- 传递渲染函数 renderElement 和 renderLeaf 给 Editable 组件，对元素和叶子节点进行自定义渲染。

- 不足
  - 还没有发布正式版，处于 Beta 阶段，API 可能会有变化
  - 渲染层目前只有 React，要在其他框架中使用需要自行实现
  - 数据渲染分离，需要完全控制用户输入行为，否则可能导致数据和渲染不同步
  - 基于 contenteditable 无法突破浏览器的排版效果
  - 对中文输入支持不足，详见此 链接
  - 社区驱动开发，问题可能得不到及时修复
# [CKEditor 5: The Future of Rich Text Editing_201510](https://medium.com/content-uneditable/ckeditor-5-the-future-of-rich-text-editing-2b9300f9df2c)
- Why CKEditor 5?
  - (tl; dr) To keep leading on innovation everything is to be re-thought.
# more
- [Text Rendering Hates You](https://gankra.github.io/blah/text-hates-you/)
- [TEXT EDITING HATES YOU TOO](https://lord.io/text-editing-hates-you-too/)

- [为什么 ContentEditable 很恐怖](https://www.oschina.net/translate/why-contenteditable-is-terrible)

- [Slate.js - 革命性的富文本编辑框架](https://s1973.top/blog/0015499011852838c3eb8e0d6d14a3f97bee6e61fa1cd26000)
