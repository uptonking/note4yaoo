---
title: toc-office-markdown
tags: [doc, markdown, toc]
created: '2020-10-05T09:49:50.474Z'
modified: '2021-01-04T17:26:25.032Z'
---

# toc-office-markdown

# markdown-parser-generator

- https://github.com/markdown-it/markdown-it
  - https://markdown-it.github.io/
  - /10.4kStar/MIT/202009
  - Markdown parser. 
  - 100% CommonMark support, extensions, syntax plugins & high speed
- https://github.com/remarkjs/remark/tree/main/packages/remark-parse
  - Parses Markdown to mdast syntax trees. 
  - Built on micromark and mdast-util-from-markdown
- https://github.com/eczn/down-parse
  - /ts/2019
  - markdown parser with a wonderful plugin system
- https://github.com/markedjs/marked
  - /24kStar/MIT/202012/js
  - A markdown parser and compiler. Built for speed.
  - light-weight while implementing all markdown features from the supported flavors & specification
# markdown-editor
- https://github.com/iddan/react-universal-markdown
  - Markdown component for Web and Native powered by CommonMark

- react-markdown-editor-lite /446Star/MIT/202008
  - https://github.com/HarryChen0506/react-markdown-editor-lite
  - 基于textarea和React的markdown编辑器，实现简单且清晰
- rich-markdown-editor /2kStar/BSD/202105/ts
  - https://github.com/outline/rich-markdown-editor
  - 依赖prosemirror-markdown
  - React and Prosemirror based markdown editor that powers Outline.
  - The editor is WYSIWYG and includes formatting tools whilst retaining the ability to write markdown shortcuts inline and output plain Markdown.
- milkdown /454Star/MIT/202106/ts
  - https://github.com/Saul-Mirone/milkdown
  - https://saul-mirone.github.io/milkdown/
  - 依赖prosemirror、remark、prism、katex，但不依赖prosemirror-markdown、react
  - A plugin-driven WYSIWYG markdown Editor, inspired by Typora, built on top of prosemirror and remark.
  - ⚠️️breaking: @milkdown/core@4.4.0(202107) migrate from markdown-it to remark
- https://atlaskit.atlassian.com/packages/editor/editor-markdown-transformer
  - A Markdown to ProseMirror Node parser.

- https://github.com/remarkjs/react-markdown
  - https://remarkjs.github.io/react-markdown/
  - /7.1kStar/MIT/202105/js
  - 依赖remark-parse、remark-rehype、unified, vfile
  - Markdown component for React using remark.
  - why this one?
    - The two main reasons are that they often rely on `dangerouslySetInnerHTML` or have bugs with how they handle markdown. 
    - react-markdown uses a syntax tree to build the virtual dom which allows for updating only the changing DOM instead of completely overwriting.
- https://github.com/StackExchange/Stacks-Editor
  - Stack Overflow's Combination Rich Text/Markdown Editor
  - 依赖prosemirror, hightlight.js，不依赖react
- https://github.com/uiwjs/react-markdown-editor
  - A markdown editor with preview, implemented with React.js and TypeScript.
  - 依赖react-markdown、codemirror、highlight.js
- https://github.com/uiwjs/react-md-editor
  - A simple markdown editor with preview, implemented with React.js and TypeScript.
  - This is based on textarea encapsulation, so it does not depend on any modern code editors such as Acs, CodeMirror, Monaco etc.

- https://github.com/benweet/stackedit
  - In-browser Markdown editor
- https://github.com/pandao/editor.md
  - The open source embeddable online markdown editor (component).
- https://github.com/Vanessa219/vditor
  - /1.3kStar/MIT/202009
  - In-browser Markdown editor, support WYSIWYG (Rich Text), Instant Rendering (Typora-like) and Split View modes.
  - 依赖lute(go语言实现md解析)、hightlight、echarts、katex、mermaid、mathjax，注意依赖文件直接在源码的js/文件夹，不在package.json
- more-markdown-editor
  - vscode-monaco-editor
# markdown-viewer
- https://github.com/shd101wyy/markdown-preview-enhanced
  - One of the 'BEST' markdown preview extensions for Atom editor
# markdown-examples
- https://github.com/foambubble/foam
  - /7.3kStar/MIT/202010/ts
  - Foam is a personal knowledge management and sharing system built on VSCode and GitHub.
- https://github.com/atom-community/markdown-preview-plus
  - a fork of Markdown Preview that provides a real-time preview of markdown documents.
# more-repos
- https://github.com/rstudio/rmarkdown
  - rmarkdown package helps you create dynamic analysis documents
