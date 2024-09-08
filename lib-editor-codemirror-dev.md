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
  - 支持强大的扩展, ext支持设置优先级
  - 官方支持collab, 基于ot算法变体
  - ✨ v6实现了 virtualized-render, 可结合visible ranges进一步提高性能
  - ❓ incremental syntax highlighting, 可结合visible ranges
  - 支持mobile
  - accessible
  - 基于contenteditable(而不是textarea)实现，具备✨富文本的能力
  - 支持split-view
  - 支持nested-editor，可在同一页面渲染多个编辑器
  - ~~simpler than prosemirror~~
  - 内置支持folded-code

- cons
  - 非开箱即用，需要组装模块
  - 协作基于ot变体，非标准ot
  - 默认不支持ssr, 但有方案支持
  - 顶层容器不支持CSS transform 3d，但支持transform2d(用于画板缩放的场景, 但ace/monaco支持，有改进)

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
  - obsidian, zettlr, joplin-markdown-editor, supernotes
  - chrome-devtools(开源代码中使用v6)
  - known: mdn-bob, sourcegraph
  - libfwk: svelte-playground, gitbutler
  - more: tagspaces, hedgedoc
  - ?: replay.io, duckdb
  - apps: desmos-classroom
  - 参考这些公司在开源项目中的用法

- who is using #highlightjs
  - stackoverflow
  - discord
- who is using #prismjs
  - mozilla
  - stripe, drupal

- who is using #xtermjs
  - duckdb-shell

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

- ide类产品 vs 文档类产品 🆚
  - ide一般支持远程连接代码仓库，本地仓库和远程仓库的文件通过git同步
  - ide的数据源多是远程git仓库，其他系统S可能会支持git命令绕过S直接修改远程仓库
    - 而文档类产品的数据源一般是数据库，只能通用系统S的ui修改

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

- code-editor vs text-editor 🆚
  - syntax-highlighting, 对新的自定义语言的支持
  - auto-closing brackets
  - indentation
  - 行号、折叠
  - symbol跳转定义与查找饮用
  - 代码编辑器通常commit会包含多个文件，而文本编辑器一般单文件操作

- dev-xp
  - 在github页面，每行代码的行号是确定的，不会显示软换行
    - 方便实现高亮搜索结果、查找引用
  - codemirror协作官方示例使用ot变体，社区有使用crdt如yjs
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
- nostable-editor
  - virtualized
  - draggable block-style
  - table/database: multi views, user-defined

- not-yet
  - codemirror devtools
  - autocomplete
  - 迁移v5的示例到v6
  - lezer-highlight vs highlightjs

- port to server side lang like prosemirror
  - hocuspocus for codemirror
  - codemirror-rust

- experimental
  - lazy
  - load new document
  - conflict

- extensions-to
  - katex

- integrations
  - strapi-codemirror
- web
  - quill/slate-codemirror
  - 尝试将prosemirror的使用场景替换为codemirror
- electron
  - obsidian-plugin

- diff-to
  - cursor的代码修改使用了aider的codeblock diff格式
  - diff with magic-code-animation

- diff-view左右布局
  - 默认示例是左边旧代码可编辑，右边新代码不可编辑，与vscode相反

- diff-view上下布局
  - 使用打字机动画修改unchanged的行时，先修改再交换行，避免视图跳跃
  - 高亮变更内容的粒度是整行，太粗了，但适合代码编辑场景
  - 已经实现了字符级的添加和删除，能高亮新插入的字符，但修改单个字符有时会高亮整个单词(符合左右布局)
  - ~~不支持 collapseUnchanged~~
  - 未实现行内渲染change和操作
  - 在红色部分前面的行末尾回车，有时新行会跑到红色之下，其实也符合预期
  - 插入换行符时会高亮整行作为新增，不符合预期，但这个是通过api修改的方式，通过ui修改是符合预期的

- discuss
  - 简化ast的设计和实现

- 难点
  - 渲染wysiwyg时采用 virtual render
  - 支持可缩放的编辑器，用于将编辑器嵌入画板/设计工具的场景
# dev-xp
- 自定义元素widget
  - 可参考replit

- 隐藏diff-view绿色行的实现方案
  - 思路0: 通过line-decoration给绿色行按条件添加隐藏、动画样式类
  - ~~思路0: 通过widget-decoration直接替换元素，但需要手动实现atomicRanges~~
  - 思路1: 自定义 cold-folding 组件的显示元素，使得fold后显示空
  - 思路2: 通过replace-decoration隐藏元素
  - 其他
    - mark-decoration的粒度过细，计算繁琐
    - 通过cold-fold实现隐藏元素的思路是否正确

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

- 💬 实现评论时考虑是否支持评论协作、undo/redo， 一般将评论数据内容放在编辑器内容doc之外
  - 减少doc体积，方便支持自定义评论的形状颜色
  - 方便实现非行内的跨block的评论，行内评论和块级评论
  - 复制文本时不需要带上评论数据, 处理复制粘贴更简单

- To completely reset a state—for example to load a new document—it is recommended to create a new state instead of a transaction. That will make sure no unwanted state (such as undo history events) sticks around.

- Querying coordinates for positions outside of the current viewport will not work (since they are not rendered, and thus have no layout).

- deco-mark
  - Syntax highlighting
  - add some attributes or wrapping DOM element 
- deco-widget
  - insert a DOM element in editor: inline elements or blocks
- deco-replacing 可以修改多行
  - code folding or replacing an element in the text with something else
  - possible to display a widget instead of the replaced text
- deco-line 修改一行
  - influence the attributes of the DOM element that wraps the line
- Decorations that significantly change the vertical layout of the editor, for example by replacing line breaks or inserting block widgets, must be provided directly, since indirect decorations are only retrieved after the viewport has been computed.
  - Indirect decorations are appropriate for things like syntax highlighting or search match highlighting, where you might want to just render the decorations inside the viewport or the current visible ranges

## dev-ai-coding

- diff视图的结果是红色删除行在上、绿色增加行在下

### cursor交互细节

- 修改单行代码
  - ai即将修改第10行
  - 旧代码被挤到第11行，ai在第10行写入新代码
  - 新代码写完后，立即交换新旧代码行，使得最终符合diff视图习惯，但存在视图跳动，体验不好

- 修改多行代码
  - 类似修改单行代码，ai先写新代码
  - 新代码写完后，将下面的旧代码换上去，体验差
  - 修改多行代码的提示词示例: 先选中递归版本的quickSort方法，然后cmd+k输入 change quickSort to not using recursive function

- 
- 
- 

# more
