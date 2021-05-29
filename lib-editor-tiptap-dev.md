---
title: lib-editor-tiptap-dev
tags: [lib, prosemirror, text-editor, tiptap]
created: '2021-05-06T09:45:58.536Z'
modified: '2021-05-06T09:46:30.944Z'
---

# lib-editor-tiptap-dev

> A headless, framework-agnostic and extendable WYSIWYG rich text editor, based on ProseMirror.

# guide

# faq-not-yet

# docs

## output

- You can store your content as a JSON object or as a good old HTML string.
- **tiptap doesn’t support Markdown as an input or output format**. 
  - Both, HTML and JSON, can have deeply nested structures, Markdown is flat.
  - tiptap’s strength is customization, that doesn’t work very well with Markdown.
  - Markdown standards vary.
  - There are enough packages to convert HTML to Markdown and vice-versa.
# discuss-stars
- ## [Markdown input and output_201810](https://github.com/ueberdosis/tiptap/issues/66)
- [prosemirror official Friendly Markdown example](https://prosemirror.net/examples/markdown/)
  - 支持在markdown和wysiwyg间切换，无外部依赖
- At the moment it's not possible to add this functionality with extensions. That's something I have to add to the core.
- I don’t see us adding this to the core, it’s just too different. So I’m closing this here for now. Consider using CodeMirror, if you really want to work with Markdown.
# discuss
