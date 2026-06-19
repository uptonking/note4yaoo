---
title: lib-edit-typst-dev
tags: [typesetting, typst]
created: 2025-12-25T19:53:19.651Z
modified: 2025-12-25T19:53:44.941Z
---

# lib-edit-typst-dev

# guide

- pros
  - ?

- cons
  - 对数学公式的支持度不如latex
  - 对animation动画的支持不好，因为不是主要设计目标

- features
  - ?

- pm-markdown-typst
# draft
- viewers
  - 尝试将markdown编辑器的双栏预览，替换为 富文本/pdf打印预览
  - 类似overleaf的 从text到pdf， 市场需求小， 而从 text 到 WYSIWYG 需求大一点, 或者从 WYSIWYG 到 pdf 的需求更大

- table
  - lowcode table builder + export to markdown/typst

- converters
- html > typst, 基于html的场景数据源非常多
  - 参考 html2markdown 来实现typst，还可以将文档内容还原为pdf/ppt

- diagramming
  - 参考cetz， 基于mermaid实现

- lsp
  - formatter
  - lint
  - codemirror syntax highlighting
# dev-xp

# latex

# more
- [Typst Bundle export ](https://typst.app/docs/reference/bundle/)
  - Bundle output is useful for creating multi-page websites with HTML export, but it is not limited to HTML export. 
  - You can create bundles containing any combination of HTML pages, PDFs, PNGs, SVGs, and arbitrary assets.
  - A bundle is a collection of files. Each of these bundle files falls into one of two categories: Document or asset. 
    - A document takes content that is exported with one of Typst’s other export formats. 
    - Meanwhile, an asset takes raw byte data of your choice that will be written to disk as-is. 
  - Typst’s built-in linking mechanism natively supports cross-document links and resolves the correct relative paths for you. 
  - Documents and assets are normal elements, so you can use them with Typst’s usual scripting, styling, and introspection mechanisms.
  - Introspections always observe the full bundle rather than individual documents. For instance, querying for headings will give you all headings in all documents rather than the ones in the current document.
