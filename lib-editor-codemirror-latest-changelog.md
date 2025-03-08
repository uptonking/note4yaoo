---
title: lib-editor-codemirror-latest-changelog
tags: [changelog, codemirror]
created: 2024-05-02T06:51:22.445Z
modified: 2024-05-02T06:51:34.217Z
---

# lib-editor-codemirror-latest-changelog

# guide

# roadmap

# changelog

- 2024-06-10 🐛
  - @codemirror/view@6.28.0
    - The editor will now, when available (which is only on Chrome for the foreseeable future) use the `EditContext` API to capture text input.
    - 此版本存在编辑器会意外捕获用户输入的问题，实测用户在编辑器外的input输入字符时，输入的字符会意外进入编辑器
    - 6.28.1关闭了此特性
    - 6.28.2又开启了此特性

- 202305
  - merge: [Add support for unified diff interface](https://github.com/codemirror/merge/commit/5916d24de61511fe687d485e45706e897967cf78)
  - The new `unifiedMergeView` extension can be used to display a diff inside a single editor, by **inserting deleted content as widgets** in the document.
# discuss-changes
- ## [CodeMirror 6 Status Update _201908](https://marijnhaverbeke.nl/blog/codemirror-6-progress.html)
- It has been almost a year since we officially announced the CodeMirror 6 project, which aims to rewrite CodeMirror (a code editor for in the browser) to align its design with the technological realities and fashions of the late 2010s.
- we integrate a new approach to code parsing.
- we finished a doc comment extractor for TypeScript
- I'm definitely suffering from second system syndrome, where after eight years with the old system, I am acutely aware of its limitations and want to fix them all this time around. 
  - That sometimes leads me into overly-ambitious design rabbit holes, and then it takes me a week or two to dig myself out again.
- Composition Support
  - Handling composition/IME (input method editor) in the browser is its own special kind of hell.
- Behaviors as Extension Primitive
  - A design where a generic core provides a platform for all kinds of features to be implemented in plugins has to, in a way, provide an extendable extension mechanism
  - I think we landed on a nice architecture. 
- CSS Modules
  - Since the browser platform's CSS support is still more or less completely unhelpful when it comes to modularized system, we've decided to use a CSS-in-JS approach where extensions can define their own styles from within JavaScript code and make sure they are included in the document or shadow DOM where the editor is placed.
- View Fields and Updates
  - I've added a new abstraction, view fields, for pieces of state that live in the view and affect things like decorations (styling and widgets in the content) and the attributes of the editor's wrapper DOM nodes.
- Block Widgets
  - Block widgets are a way to insert a block element into the document, either on a line boundary, in the middle of a line, or covering some content.
- Generic Gutters
- Doc Generation
- Lezer
  - tree-sitter, which is a practical implementation of an incremental LR parser, giving you a real syntax tree for your code and updating it cheaply when you make changes. It is used in the Atom editor.
  - I set out to clone tree-sitter in JavaScript. I didn't exactly clone it, but rather built a different system inspired by it. 
  - That system is Lezer, an incremental parser generator and runtime system for JavaScript.
