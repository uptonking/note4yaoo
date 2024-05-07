---
title: lib-editor-codemirror-dev
tags: [codemirror, lib, text-editor]
created: 2021-05-06T09:37:37.030Z
modified: 2021-05-06T09:38:31.520Z
---

# lib-editor-codemirror-dev

# guide

- pros
  - MIT
  - 可扩展性强
  - 官方支持collab, 基于ot变体算法
  - v6实现了 virtualized-render
  - 支持mobile

- cons
  - 非开箱即用，需要组装模块

- features
  - Mobile Support: Use the platform's native selection and editing features on phones.
  - Accessibility: Works well with screen readers and keyboard-only users
  - Bidirectional Text: ltr, rtl
  - Syntax Highlighting
  - Line Numbers
  - Autocompletion
  - Code Folding
  - Search/Replace
  - Full Parsing
  - Extension Interface
  - Modularity
  - Speed: Remains responsive even on huge documents and long lines
  - Bracket Closing
  - Linting
  - Flexible Styling
  - Theming
  - Collaborative Editing
  - Undo History
  - Multiple Selections: Select and edit multiple ranges of the document at once
  - Internationalization

- who is using #codemirror 🌰
  - jupyter
  - observablehq-notebook, val-town
  - codesandbox, codepen, replit
  - overleaf
  - obsidian
  - sourcegraph
  - more: tagspaces

- 代码编辑器要点
  - incremental syntax highlighting
  - virtualized render

- dev-xp
  - 在github页面，每行代码的行号是确定的，不会显示软换行
    - 方便实现高亮搜索结果、查找引用
  - 协作示例官方使用ot，社区有使用crdt如yjs

- 区分codemirror是v5和v6的方法
  - 6️⃣ cm6的默认css，样式名小写
    - .cm-editor
    - .cm-gutters
    - .cm-content
      - .cm-line
      - .cm-activeLine
    - .cm-layer.cm-selectionLayer
  - 5️⃣ cm5的默认css
    - .CodeMirror-lines
    - .CodeMirror-cursors
    - .CodeMirror-code
      - .CodeMirror-gutter-wrapper
      - .CodeMirror-line 
    - .CodeMirror-gutters

- resources
  - [Ace, CodeMirror, and Monaco: A Comparison of the Code Editors You Use in the Browser _202112](https://blog.replit.com/code-editors)
# draft
- features
  - diff with magic-code-animation
  - highlight current selection
# dev

# more
