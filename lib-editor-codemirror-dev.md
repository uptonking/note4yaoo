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
  - 可扩展性很强, ext支持设置优先级
  - collab有官方支持, 基于ot算法变体
  - 支持selective undo
  - 🌰 diff-view的示例有官方开发，其他编辑器很少提供
  - ✨ v6实现了 virtualized-render, 可结合visible ranges进一步提高性能
  - ❓ incremental syntax highlighting, 可结合visible ranges
  - 支持mobile
  - accessible
  - 基于contenteditable(而不是textarea)实现，具备✨富文本的能力
  - 支持nested-editor，可在同一页面渲染多个编辑器，参考split-view示例、公式
  - 内置支持folded-code
  - 支持multi-cursor, 此时键盘输入字符会在多个光标后同时显示
  - ~~simpler than prosemirror~~

- cons
  - 非开箱即用，需要组装模块
  - collab基于ot变体，非标准ot
  - ssr默认不支持, 但有方案支持
  - 顶层容器不支持CSS transform 3d，但支持transform2d(用于画板缩放的场景, 但ace/monaco支持3d，有改进)

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
  - replit, codesandbox-sandpack, codepen, glitch(v5), phoenix-brackets(v5)
  - jupyter-notebook, observablehq-notebook, val-town, livebook(Elixir)
  - obsidian, zettlr, joplin-markdown-editor, supernotes
  - chrome-devtools(开源代码中使用v6)
  - known: mdn-bob, sourcegraph, odoo, ChatGPT-canvas
  - libfwk: svelte-playground, gitbutler
  - sql: duckdb, HuggingFace-sql-console, tisqleditor
  - more: tagspaces, hedgedoc
  - apps: desmos-classroom
  - ?: replay.io
  - 参考这些公司在开源项目中的用法

- who is using #highlightjs
  - stackoverflow
  - discord
- who is using #prismjs
  - mozilla
  - stripe, drupal

- who is using #xtermjs
  - duckdb-shell

- cloud-ide-pros
  - easy to start and leave
  - better collaborative editing
  - consistent env
- cloud-ide-solutions
  - monaco: Codespaces(GitHub绑定), Gitpod(yml), Coder(no-cloud/k8s), theia, OpenSumi, StackBlitz, codesandbox
  - Eclipse Che: OpenShift CDE
  - DevPod: devcontainer-spec + local-and-cloud
  - ace: miro
  - more: AWS Cloud9
- cloud-ide-cons
  - 计算资源受业务平台限制和云厂商限制
  - vps的性能不如本地计算机，vps很贵

- ide类产品 vs 文档类产品 🆚
  - ide一般支持远程连接代码仓库，本地仓库和远程仓库的文件通过git同步
  - ide的数据源多是远程git仓库，其他系统S可能会支持git命令绕过S直接修改远程仓库
    - 而文档类产品的数据源一般是数据库，只能通过系统S的ui修改

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
  - autocomplete
  - indentation
  - 行号、折叠
  - symbol跳转定义与查找引用
  - 代码编辑器通常commit会包含多个文件，而文本编辑器一般单文件操作

- 区分codemirror是v5和v6的方法 🆚
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
# not-yet
- 连续dispatch的实现方式，如何选择
  - viewPlugin.update
  - EditorView.updateListener
  - EditorState.transactionExtender.of
  - transactionFilter
  - stateField.update, 可以不使用值，只使用update逻辑

- cm-undo的粒度是什么，如何触发一次undo来撤销指定几个transaction

- cmdk-undo
  - 正向触发流程: originalDoc > newDoc > showDiff > hideDiff
  - undo更好的实现方式是手动控制tr的合并，更简单的这种方式是手动触发undo的逻辑

- 基于transactionExtender的ext，
  - 🤔 后注册的会先执行
  - ~~只能返回单个effect，不能返回数组~~, 看清楚.of的返回值类型时StateEffect或Anno，而不是Transaction
  - 处理changes推荐用transactionFilter

- codemirror似乎未使用rope数据结构

- 📝 实现notion-like的编辑器
  - 拖拽部分的处理可参考craftjs
  - 多维表格的实现需要考虑偏前端还是后端，可参考web-db的实现
  - 表格的公式编辑器可采用nested-codemirror
# draft
- nostable-editor
  - virtualized
  - draggable block-style
  - table/database: multi views, user-defined
  - markdown sync scroll
  - 尝试集成redux-devtools
  - vscode with codemirror

- not-yet
  - codemirror devtools
  - autocomplete
  - 迁移v5的示例到v6
  - migrate monaco-playground to codemirror
  - lezer-highlight vs highlightjs
  - EditorView.requestMeasure

- port to server side lang like prosemirror
  - hocuspocus for codemirror
  - codemirror-rust 🦀

- experimental
  - lazy
  - conflict
  - ~~stateField invertedEffects~~
  - ~~Cascading dispatch triggers another dispatch~~
  - ~~undo/addToHistory~~
  - ~~load new document~~

- extensions-to
  - katex

- lang
  - replace lezer with Tree-sitter

- integrations
  - strapi-codemirror
- web
  - quill/slate-codemirror
  - 尝试将prosemirror的使用场景替换为codemirror
- electron
  - obsidian-plugin

- later
  - 简化ast的设计和实现

- 难点
  - 渲染wysiwyg时采用 virtual render
  - 支持可缩放的编辑器，用于将编辑器嵌入画板/设计工具的场景

- ❓🆚 transaction vs changeSet
# dev-xp
- 在editor中插入内容要考虑
  - 选区， del键/快捷键操作影响， 复制粘贴
  - undo/redo

- beforeChange/beforeSelectionChange 可使用filter
  - afterChange 可使用 updateListener/viewPlugin.update

- 在github页面，每行代码的行号是确定的，不会显示软换行
  - 方便实现高亮搜索结果、查找引用

- 代码的ast和block编辑器的ast处理方式类似，代码的symbol跳转和双链类似

- 💄 自定义元素widget
  - codemirror会在widget最外层渲染一个contenteditable为false的元素
  - 💡 block widget前面默认没行号，inline widget会使用原行的行号，无论有没有使用Decoration.replace渲染
  - 可参考replit官方开源示例实现widget
  - blazor编辑器的image/mermaid都会在文本上渲染一个contenteditable为false的元素
  - overleaf-visual编辑器的image/table会渲染一个contenteditable为false的元素
  - ink-mde的image会渲染一个contenteditable为false的元素

- dispatch
  - 作者推荐将async逻辑放在编辑器之外，等到await asyncLogic完了，再执行dispatch

- 多标签页的实现思路和单标签差别不大，视觉上只有1个visible的editor，上方是tab

- baseTheme的specificity比theme低，且能使用&dark

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
  - ~~减少doc体积，~~方便支持自定义评论的形状颜色
  - 方便实现非行内的跨block的评论，行内评论和块级评论
  - 复制文本时不需要带上评论数据, 处理复制粘贴更简单

- To completely reset a state—for example to load a new document—it is recommended to create a new state instead of a transaction. 
  - That will make sure no unwanted state (such as undo history events) sticks around.

- Querying coordinates for positions outside of the current viewport will not work (since they are not rendered, and thus have no layout).

## collab-cm

- codemirror协作官方示例使用ot变体，社区有使用crdt如yjs

## dev-ai-coding/diff

- diff视图的结果是红色删除行在上、绿色增加行在下

- diff-to
  - cursor的代码修改使用了aider的codeblock diff格式
  - diff with magic-code-animation

- diff-view上下布局
  - 使用打字机动画修改unchanged的行时，先修改再交换行，避免视图跳跃
  - 高亮变更内容的粒度是整行，太粗了，但适合代码编辑场景
  - 已经实现了字符级的添加和删除，能高亮新插入的字符，但修改单个字符有时会高亮整个单词(符合左右布局)
  - ~~不支持 collapseUnchanged~~
  - 未实现行内渲染change和操作
  - 在红色部分前面的行末尾回车，有时新行会跑到红色之下，其实也符合预期
  - 插入换行符时会高亮整行作为新增，不符合预期，但这个是通过api修改的方式，通过ui修改是符合预期的

- 隐藏diff-view绿色行的实现方案
  - 思路0: 通过line-decoration给绿色行按条件添加隐藏、动画样式类
  - ~~思路0: 通过widget-decoration直接替换元素，但需要手动实现atomicRanges~~
  - 思路1: 自定义 cold-folding 组件的显示元素，使得fold后显示空
  - 思路2: 通过replace-decoration隐藏元素
  - 其他
    - mark-decoration的粒度过细，计算繁琐
    - 通过cold-fold实现隐藏元素的思路是否正确
  - 实现细节
    - 每个变更块的红色部分(可能包含多行)都是一个 `<div class="cm-deletedChunk" contenteditable="false">`, 多行红色会直接在TextNode里面换行文本，没有额外的html标签元素, deletedChunk.textContent会返回类似`four cups\nhello`

- diff-view-undo
  - 思路1: invertedEffects在修改stateField sf1时，将还原的effect保存到history
  - 思路2: 使用transactionFilter, 将undo的tr替换为撤销逻辑
- 如何在undo时恢复编辑器内容之外的数据，如cmdk的输入框的内容，思路是将自定义stateField的数据也加入history

- codemirror和cursor的undo实现
  - 默认只undo内容更改并移动光标到更改位置，不会触发undo仅仅移动光标而不修改内容
- dispatchTr是同步操作，tr都是基于当前state，若doc有变化，则合并tr的思路不可取
  - 是否采用合并transaction的思路要多考虑，When creating a transaction, you are basing it on the current editor state. It would often not make any sense anymore when applied from a different state. Also dispatching transactions is synchronous, so a queue seems needless complexity.

### cursor交互细节

- 修改单行代码
  - ai即将修改第10行
  - 旧代码被挤到第11行，ai在第10行写入新代码
  - 新代码写完后，立即交换新旧代码行，使得最终符合diff视图习惯，但存在视图跳动，体验不好

- 修改多行代码
  - 类似修改单行代码，ai先写新代码
  - 新代码写完后，将下面的旧代码换上去，体验差
  - 修改多行代码的提示词示例: 先选中递归版本的quickSort方法，然后cmd+k输入 change quickSort to not using recursive function

## dev-cde

- 基于文件系统实现的cde不适合实时协作
  - 协作难点：git，ssh
  - 集成和限制第三方服务: github，ai-token
  - playground容器在(无心跳3min)失活后，ssh无法打开, 所以要保持浏览器的cde页面打开

- 通过本地vscode打开ssh-url的方式打开cde文件后，在cde修改文件会同步到vscode，但在vscode修改文件不会立即在cde更新，cde需要手动刷新文件内容
  - 需要针对ssh协议更新协同编辑的逻辑

- 通过在命令行执行git pull的方式更新cde的文件，cde需要手动刷新文件内容
  - 需要针对git pull/rebase更新协同编辑的逻辑

- 在cde的xterm terminal执行命令，docker的cpu是正常的
  - 在vscode ssh的terminal执行命令，docker的cpu一般在100%之上
# styling

```CSS
/* 选区在页面失焦后显示灰色 */
.cm-selectionBackground {
  background: #d9d9d9;
}
```

# more

# devlog

- "codemirror" Field is not present in this state
  - 可能是代码import了不同版本的codemirror导致的，也可能是本地fork了代码但用的还是npm包
