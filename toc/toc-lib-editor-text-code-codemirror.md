---
title: toc-lib-editor-text-code-codemirror
tags: [code-editor, codemirror, text-editor, toc]
created: 2021-05-14T10:28:05.856Z
modified: 2022-08-18T11:29:26.644Z
---

# toc-lib-editor-text-code-codemirror

# guide

- monaco-editor-pros
  - 来自vscode，代码编辑功能强大，有大公司支持
  - 支持 language server protocol

- monaco-editor-cons
  - 体积大、复杂度高
  - 不支持mobile
  - 设计目标是ide，而不是纯粹的代码编辑器
  - 引入项目比较麻烦，不能直接简单的import，webpack要使用专门的plugin，如cra无法直接使用

- top-dependents-of-codemirror.v6
  - @codemirror/collab
  - @eldonlabs/autocomplete: 也是官方扩展
  - @codesandbox/sandpack-react: 依赖的sandpack-client(不依赖codemirror)
  - react-tools-codemirror: codemirror6的react组件封装
  - @writewithocto/ink: 原地预览样式的编辑器
  - markword: A WYSIWYG markdown syntax set for Codemirror 6

- top-dependents-of-codemirror.v5
  - react-codemirror
  - @toast-ui/editor
  - tui-editor
  - admin-lte
  - @jupyterlab/codemirror
  - grapesjs
  - @uiw/react-codemirror
  - playroom

- top-dependents-of-prosemirror
  - prosemirror-collab
  - @tiptap/core v2
  - @atlaskit/editor-core
  - rich-markdown-editor
  - @remirror/core

- ref
  - [html editors](https://gist.github.com/manigandham/65543a0bc2bf7006a487)
  - [codemirror6 vs prosemirror vs editorjs](https://www.npmtrends.com/@editorjs/editorjs-vs-@codemirror/state-vs-prosemirror-state-vs-monaco-editor-vs-codemirror)
  - https://bangle.io/ 编辑器的折叠体验很好，链接编辑也好
  - Abstracted Editors
    - These use separate document structures instead of HTML, 
    - some are more modular libraries than full editors
  - Dom-Based Editors
    - eg, tinymce,medium-editor,froala
# codemirror
- https://github.com/codemirror/CodeMirror
  - /21.3kStar/MIT/202010/js
  - In-browser code editor
  - CodeMirror 6 is a rewrite of the CodeMirror code editor. 
  - The new system provides solid accessibility, touchscreen support, better content analysis
  - It is not API-compatible with the old code.

- https://github.com/writewithocto/ink
  - https://octo.app/tags/examples
  - A plain-text javascript markdown editor library that renders formatting live and in-place without the need for a preview pane. 
  - Built on CodeMirror 6. Powers https://octo.app/

## code-editor

- https://github.com/acode/copenhagen /202110/js/inactive
  - https://copenhagen.autocode.com/
  - lightweight and hackable open source code editor for the web
  - powering the code-editing experience on Autocode, and it's written entirely in vanilla JavaScript with only `highlight.js` and feather icons bundled as dependencies.

- https://github.com/ghost23/east
  - Playing around with the idea of an AST-based code editor for JavaScript.

- https://github.com/maxmcd/plum
  - A mobile AST-based editor for Javascript

## apps

- https://github.com/vizhub-core/vizhub
  - https://vizhub.community/
  - Self Hosted CMS for Web-based Dataviz
  - VizHub 2 has been used in Data Visualization Course 2018, Datavis 2020
    - iFrame-based code execution environment.
  - VizHub 3
    - possible to self-host your own instance
    - possible to extend the core with plugins
  - https://github.com/vizhub-core/vzcode
# collab
- https://github.com/tanwarAalok/Code-Sync
  - A Realtime collaboration Code editor using codemirror5
# more-code-editor
