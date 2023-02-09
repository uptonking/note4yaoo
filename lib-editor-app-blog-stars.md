---
title: lib-editor-app-blog-stars
tags: [blog, editor, text-editor]
created: 2020-12-24T18:17:55.072Z
modified: 2022-08-21T10:11:43.095Z
---

# lib-editor-app-blog-stars

# guide

- 渲染长文档的思路
  - virtualized render
    - 参考 ajaxorg/ace、codemirror、typewriter
  - defer render

- 编辑器入门经典示例
  - slate
    - minimal-render > event-keydown > custom-element > custom-format > commands > save-to-local > api/transform
    - rich-text-editor, mention, search-highlight
  - ckeditor5
    - timestamp-plugin > abbreviation-plugin > box/card-widget > inline-word-widget > react-add-product
    - demos for every feature
  - prosemirror
    - example-setup > custom-node > toolbar-menu > tooltip > custom-schema > > img-upload > markdown
    - footnotes: inline node
    - linter
    - track-change
    - collab
# blogs

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

## [A Brief Glance at How Various Text Editors Manage Their Textual Data_201505](https://ecc-comp.blogspot.com/2015/05/a-brief-glance-at-how-5-text-editors.html)

- A review of how GNU Moe, Plan 9 Sam, Bill Joy's Ex/Vi, GNOME GtkTextView/GtkTextBuffer, GNU Emacs, and due to popular demand, Scintilla, manage their textual data. This article is subject to updates.

### [A Brief Glance at How Various Text Editors Manage Their Textual Data (2015) | Hacker News](https://news.ycombinator.com/item?id=11244103)

- If you are interested in this, [Data Structures for Text Sequences](https://www.cs.unm.edu/~crowley/papers/sds.pdf) by Charles Crowley is an excellent paper to study.

- The article is missing one of the important but commonly overlooked structures: a "piece chain" (aka "piece table"). 
  - Not easy to find editors using it, especially among the popular ones, but:
  - from what I've read somewhere, MS Word was/is (?) using it internally
  - AbiWord the text editor of the Oberon OS used it 

- I'd like to see someone write on how web based rich text editing tools store their textual data.
  - quill/draftjs/prosemirror/trix 
  - Each of them might be relying on some form of Tree to store the content which actuates the views to react. I'm only guessing. A deeper, closer look might be interesting and useful.



- 
- 
- 
# blogs-dev
- [编辑器背后的数据结构](https://dontpanic.blog/data-structures-under-editors/)
  - 部分Emacs使用了Gap Buffer，包括古老的 Emacs on TECO、现代的GNU/Emacs及其前辈Gosling Emacs。
  - Scintilla (即包括Code:: Blocks在内的很多IDE/编辑器使用的代码编辑控件) 也使用了Gap Buffer
  - Emacs进入由Lisp实现的时代后，一些Emacs版本使用了LinkedLine。
  - Vim使用的是一种基于行的数据结构，但行与行之间不是简单地使用链表连接，而是用一种树结构进行管理。
  - KDE的Okteta 16进制编辑器使用了Piece Table Buffer

- [《从零开始, 开发一个 Web Office 套件》系列博客目录_赵康_202202](https://www.cnblogs.com/forzhaokang/p/15907371.html)
  - https://github.com/zhaokang555/canvas-text-editor
  - https://zhaokang555.github.io/canvas-text-editor/
  - 基于 HTML Canvas 的富文本编辑器

- [基于 Google Doc 思想的L2编辑器演示项目](https://zhuanlan.zhihu.com/p/392055486)
  - https://github.com/cg0101/docs
  - https://cg0101.github.io/docs/

- [现代编辑器技术原理](https://www.wenxi.tech/principles-of-modern-editor-technology)
# ref
- [前端——富文本编辑器专栏](https://www.yuque.com/xiaoxiaojianbojun/wt03g5)

- [张驰技术博客](https://juejin.cn/user/3456520286121437/posts)

- [wangEditor - 开发web富文本编辑器的坑有哪些](https://juejin.cn/post/6951364054224994312)

- [自研一个word应用，需要哪些基本功能](https://juejin.cn/post/6922682336412696584)

- [基于Clipboard的复制粘贴实现](https://juejin.cn/post/7118899649687060487)
