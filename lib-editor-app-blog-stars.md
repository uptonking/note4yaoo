---
title: lib-editor-app-blog-stars
tags: [blog, editor, text-editor]
created: 2020-12-24T18:17:55.072Z
modified: 2022-08-21T10:11:43.095Z
---

# lib-editor-app-blog-stars

# guide

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

- [《从零开始, 开发一个 Web Office 套件》系列博客目录_赵康_202202](https://www.cnblogs.com/forzhaokang/p/15907371.html)
  - https://github.com/zhaokang555/canvas-text-editor
  - https://zhaokang555.github.io/canvas-text-editor/
  - 基于 HTML Canvas 的富文本编辑器.

- [基于 Google Doc 思想的L2编辑器演示项目](https://zhuanlan.zhihu.com/p/392055486)
  - https://github.com/cg0101/docs
  - https://cg0101.github.io/docs/

- [现代编辑器技术原理](https://www.wenxi.tech/principles-of-modern-editor-technology)
# [Concept of Block Style Editor](https://domino-editor.psyhyde.vercel.app/docs/)
- https://github.com/psyhyde/domino-editor
  - A Playbook for Block Style Editor (BSE): Text Styling, Block Components, Misc Functions & Theme Switcher

- Background of Block-Style Editor：
  - Markdown, for its high readability and simple syntax, has been adopted widely; 
    - Pure Markdown editing is WYSIWYM
  - Most Web-based RTF editors follow WYSIWYG interaction pattern
  - Block Style Editors provide a Markdown-like but WYSIWYG editing experience
  - On UX and interaction level, BSE provides a similar experience to Typora, MarkText, but with integrated Mini-App Blocks

- Features of Block-Style Editor：
  - Follow a structure of Markdown (Template) + CSS + Fonts
  - Inherent the text styling rules of Markdown, 
    - keep its simplicity and content-focusing approach; 
    - Remove features like: line spacing, font size, font color
  - Expand text editing into Text Editing & Styling and Mini-App Customization
  - Mini-App Blocks: table, image container, advanced code block, prefabricated UI view, embeds.
  - A web-based Content Editor that, take Interactive Document and Modular UI as guideline, 
    - use Block or Paragraph as content unit, 
    - use Markdown as its Template Structure.

- Block-Style Editor has its roots in CMS(content management system), SSG (static site generator), GitHub& Markdown, MDX, JSX, and Low-code Site Building.
- In a sense, a Block Style Editor is a Modular CMS for web document use case.
# ref
- [前端——富文本编辑器专栏](https://www.yuque.com/xiaoxiaojianbojun/wt03g5)

- [张驰技术博客](https://juejin.cn/user/3456520286121437/posts)

- [wangEditor - 开发web富文本编辑器的坑有哪些](https://juejin.cn/post/6951364054224994312)

- [自研一个word应用，需要哪些基本功能](https://juejin.cn/post/6922682336412696584)

- [基于Clipboard的复制粘贴实现](https://juejin.cn/post/7118899649687060487)
