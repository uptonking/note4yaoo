---
title: lib-editor-blog-stars
tags: [blog, editor, text-editor]
created: 2020-12-24T18:17:55.072Z
modified: 2021-06-02T17:19:46.638Z
---

# lib-editor-blog-stars

# guide

- [基于 Google Doc 思想的L2编辑器演示项目](https://zhuanlan.zhihu.com/p/392055486)
  - https://github.com/cg0101/docs
  - https://cg0101.github.io/docs/

- [现代编辑器技术原理](https://www.wenxi.tech/principles-of-modern-editor-technology)
- [现代编辑器技术原理](https://www.wenxi.tech/principles-of-modern-editor-technology)
# [Are CRDTs suitable for shared editing?__202008](https://blog.kevinjahns.de/are-crdts-suitable-for-shared-editing/)
- CRDT don't require a central authority to resolve sync conflicts
  - They open up new possibilities to scale the backend infrastructure and are also well-suited as a data-model for distributed apps that don't require a server at all.
- However, several text editor developers report not to use them because they impose a too significant overhead.
- Marijn Haverbeke wrote about his considerations against using CRDTs as a data model for CodeMirror 6
  - the cost of such a representation is significant, and in the end, I judged the requirement for converging positions to be too obscure to justify that level of extra complexity and memory use
- The Xi Editor used a CRDT as its data model to allow different processes (syntax highlighter, type checker, ..) to concurrently access the editor state without blocking the process. They reverted to a synchronous model because
- [CRDT is not pulling its (considerable) weight.__201905](https://github.com/xi-editor/xi-editor/issues/1187#issuecomment-491473599)
  - By now we have lots of examples where trying to design features around the structure imposed by CRDT turned out to be a lot more complicated than it would be in a more synchronous world - we saw the auto-indent stuff above, difficulty getting the selection right in transpose
  - CRDT is a tradeoff
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
- [张驰技术博客](https://juejin.cn/user/3456520286121437/posts)

- [wangEditor - 开发web富文本编辑器的坑有哪些](https://juejin.cn/post/6951364054224994312)

- [自研一个word应用，需要哪些基本功能](https://juejin.cn/post/6922682336412696584)

- [基于Clipboard的复制粘贴实现](https://juejin.cn/post/7118899649687060487)
