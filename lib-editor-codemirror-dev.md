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
  - 可扩展性强, ext支持设置优先级
  - 官方支持collab, 基于ot算法变体
  - ✨ v6实现了 virtualized-render, 可结合visible ranges进一步提高性能
  - ❓ incremental syntax highlighting, 可结合visible ranges
  - 支持mobile
  - accessible
  - 基于contenteditable(而不是textarea)实现，具备✨富文本的能力
  - 支持split-view
  - 支持nested-editor，可在同一页面渲染多个编辑器
  - ~~simpler than prosemirror~~

- cons
  - 非开箱即用，需要组装模块
  - 协作基于ot变体，非标准ot
  - 默认不支持ssr, 但有方案支持
  - 顶层容器不支持CSS transform(用于画板缩放的场景, 但ace/monaco支持)

- features
  - dispatch高性能，只写不读
  - Mobile Support: Use the platform's native selection and editing features on phones
  - Accessibility: Works well with screen readers and keyboard-only users
  - Bidirectional Text: ltr, rtl
  - Syntax Highlighting
  - Line Numbers
  - position uses numeric index, index-by-lines
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
  - overleaf(latex-code+rich)
  - jupyter-notebook, observablehq-notebook, val-town
  - codesandbox-sandpack, codepen, replit, glitch(v5), phoenix-brackets(v5)
  - sourcegraph
  - obsidian, zettlr, joplin-markdown-editor, supernotes
  - chrome-devtools(开源代码中使用v6)
  - known: mdn-bob
  - more: tagspaces, hedgedoc
  - ?: replay.io
  - apps: desmos-classroom
  - 参考这些公司在开源项目中的用法

- who is using #highlightjs
  - stackoverflow
  - discord
- who is using #prismjs
  - mozilla
  - stripe, drupal

- why-cloud-ide
  - easy to start and leave
  - better collaborative editing
  - consistent env

- cloud-ide
  - monaco: Codespaces(GitHub绑定), Gitpod(yml), Coder(no-cloud/k8s), theia, OpenSumi, StackBlitz, codesandbox
  - Eclipse Che: OpenShift CDE
  - DevPod: devcontainer-spec + local-and-cloud
  - ace: miro
  - more: AWS Cloud9
  - 缺点
    - vps的性能不如本地计算机，vps很贵

- ide要点
  - 主要组件: editor, fileTree, workbench-layout, extension
  - 自动同步编辑器内容、代码仓库、配置

- 代码编辑器要点
  - tradoff: 侧重预览、协作，轻量编辑、调试
  - csb-cde: quick-restore-by-snapshot, quick-switch-br/repo, preview-br/pr, collab
  - features: 符号大纲
  - incremental syntax highlighting
  - virtualized render, 可提升highlighting的性能
  - LSP
  - DAP: debug

- code-editor vs text-editor
  - syntax-highlighting, 包括对新的自定义语言的支持
  - auto-closing brackets
  - indentation
  - 行号、折叠
  - symbol跳转定义与查找饮用
  - 代码编辑器通常commit会包含多个文件，而文本编辑器一般单文件操作

- dev-xp
  - 在github页面，每行代码的行号是确定的，不会显示软换行
    - 方便实现高亮搜索结果、查找引用
  - codemirror协作官方示例使用ot，社区有使用crdt如yjs
  - 代码的ast和block编辑器的ast处理方式类似，代码的symbol跳转和双链类似

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

- poi
  - ast

- resources
# draft
- features
  - diff with magic-code-animation
  - highlight current selection

- integrations
  - strapi-codemirror
- web
  - quill/slate-codemirror
  - 尝试将prosemirror的使用场景替换为codemirror
- electron
  - obsidian-plugin


- discuss
  - 简化ast的设计和实现

- 难点
  - 渲染wysiwyg时采用 virtual render
  - 支持可缩放的编辑器，用于将编辑器嵌入画板/设计工具的场景
# dev-xp
- 多标签页的实现思路和单标签差别不大，视觉上只有1个visible的editor，上方是tab

- 难以完全使用state对象控制的状态
  - screen-coordinates
  - scroll, focus
  - cursor
  - text-dir

- commands
  - hotkeys
  - menu-item
  - command-palette

- To completely reset a state—for example to load a new document—it is recommended to create a new state instead of a transaction. That will make sure no unwanted state (such as undo history events) sticks around.

- Querying coordinates for positions outside of the current viewport will not work (since they are not rendered, and thus have no layout).

- 
- 
- 
- 
- 
- 
- 

# more
