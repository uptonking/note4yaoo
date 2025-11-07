---
title: lib-editor-prosemirror-dev
tags: [lib, prosemirror, text-editor]
created: 2021-05-06T09:39:21.604Z
modified: 2021-05-06T09:39:53.522Z
---

# lib-editor-prosemirror-dev

# guide
- pros
  - powerful features and stable
  - 🔌 modular, extensible
  - 🔀 collaborative plugin is optional
  - selective undo/redo
  - 🔡 codemirror采用相似的架构
  - support branch
  - 支持rebase
  - 支持多实例，参考官方示例
    - 支持nested-editor，参考footnote示例
  - selection支持多个ranges
  - 存在python/go的port，方便在服务端操作编辑器内容

- cons
  - 实现逻辑(model/view)复杂度高、功能丰富
  - 数据结构层的设计不够通用, step/transform不是典型的ot operation
  - 数据层和示例没有优先使用json, 不如slate的数据层直观
  - 不支持动态改变schema
  - 编辑器的多个插件存在依赖关系时如何处理
  - 与其他框架的集成不是很完美，ReactNodeView用不用portal的最佳实践不明确

- features
  - Unopinionated
    - core is small and generic, allowing different types of editors
  - Customizable schemas
    - Document schemas allow editing documents with a custom structure
  - Modular
    - only load the code you need
  - Pluggable/Extensible
    - easily enable additional functionality
  - Collaborative editing
    - multiple people can work on the same document in real time
  - Functional
    - largely functional and immutable architecture to implement complex behavior

- who is using #prosemirror
  - atlassian, nytimes, guardian
  - linear
  - manuscripts
  - 美团学城
  - chatwoot
  - llm: open-webui

- roadmap-toys
  - prosemirror offline / local-first
  - prosemirror-codeblock
  - prosemirror-handsontable/data-grid
  - prosemirror-css/theming
  - vscode-prosemirror
  - page builder: WordPress-gutenberg, wix

- tips
  - 实现复杂组件可参考
    - 官方基于CodeMirror实现Embedded code editor的例子，使用NodeView，没用contentDOM
    - 官方Footnotes的例子，使用NodeView，没用contentDOM，但用了sub-editor，总共2个editor
  - 一个prosemirror document是一个无依赖的普通js object对象，所以实现第三方renderer也可行
  - 如果关注的重点是markdown和table，那就将更多的工作放在prosemirror层，增强通用性，将react wrapper层的工作尽量减少，方便迁移
  - 提供renderless/themeable不同封装层次/灵活性的组件
  - 类似footnotes使用多个pm-EditorView的例子

- 编辑器问题
  - 光标、选区、输入法、键盘事件
  - 首屏渲染完成后，用户输入文本时，是否还需要走一次完整的解析渲染流程
  - 分析一个产品或框架，需要考虑的方面：存储的数据结构、状态管理(更新转换)、视图渲染、样式主题

- prosemirror-renderer
  - `<canvas>`是标准的html元素，考虑实现nodeViews将特殊文本渲染到canvas，如表格、图表
  - tiptap的drawing示例，可以在空svg元素上画路径
  - atlaskit-editor开源了自定义renderer可以参考
  - atlaskit-editor实现了layout多列插件和图片排版插件
# draft
- roadmap
  - fwk agnostic noseditor: prosekit + atlaskit <> tiptap
    - rewrite tiptap/blocknote/atlaskit extension in prosemirror
  - lasuite/colanode + diff-view
  - codemirror-chat 移植到 prosemirror

- 🆚 diff-view
  - diff-match-patch + prosemirror-diff
  - prosemirror-diff + codemirror-diff + (ai-writing)
  - diff support codeblock/table, 📈 pivotable + diff
  - diff for tiptap extensions/schema(rewrite tiptap diff)
  - diff for version-history-timeline
  - streamable diff
  - ⚖️ diff for rich-text

- ✨ custom-elements
- code
  - code-diff
  - sandbox: sandpack
- table
  - group
  - views
  - 针对 vlm 优化的表格及编辑
- image
  - img-diff 使用slider对比交互
  - img-editor
  - img-gen

- 👾 ai
- stream-text/md
- partial-edit
- pdf-edit-with-vlm/ocr
  - pdf-image upscale
- graphics-by-text: mermaid-editor, drawio-xml
- markdown-partial
  - treesitter as markdown stream parser

- prosemirror-markdown
  - rewrite with remark
  - rewrite with codemirror/lezer
  - mdx

- collab
  - codemirror in prosemirror: all collaborative

- examples
  - 迁移docling在线识别文档的示例

- chart
  - markdown-chart + llm

- tiptap
  - ai-extension open version

- 兼容obsidian extension

- devtools
  - migrate prosemirror-dev-toolkit features to prosemirror-devtools
  - rewrite prosemirror-devtools in tanstack-devtools style
# dev-xp
- 🤔 deep-research 的产物形态是不是使用rich-text-editor更好，甚至产出ppt
  - gemini的deep-research支持直接导入google-docs显示为在线文档且可编辑
  - 可以突出重点文本
  - 可以加入脑图/大纲
  - 可以加入图片
# faq-not-yet
- 待确认
  - 嵌入画板的体验和性能，参考 tldraw/PPTist

> 参考 site:github.com/ottypes

## 是否支持 batch update

- 另一个方向是先compose operations，再update model, 再update view

- `transform.Step.merge` (merge/group)
  - Try to merge this step with another one, to be applied directly after it. Returns the merged step when possible, null if the steps can't be merged.

- you can add steps and other updates to transaction

- https://github.com/facebook/lexical
  - The most common way to update the editor is to use editor.update()
  - When starting a fresh update, the current editor state is cloned and used as the starting point.
  - Creating an update is typically an async process that allows Lexical to batch multiple updates together in a single update – improving performance. 

- react更新也用了transaction
  - ReactUpdatesFlushTransaction
- [React transaction完全解读](https://segmentfault.com/a/1190000021303172)
- [理解React如何实现批量状态更新](https://huangtengxiao.gitee.io/post/%E7%90%86%E8%A7%A3React%E5%A6%82%E4%BD%95%E5%AE%9E%E7%8E%B0%E6%89%B9%E9%87%8F%E7%8A%B6%E6%80%81%E6%9B%B4%E6%96%B0.html)
  - 所有的setState会将生成一个update对象，并加入到一个队列中。接着会调用下面的requestWork方法，进行更新的任务调度。
  - 而在其中，会判断isBatchingUpdates是否为true。如果是，则将任务放置在队列，等待UnbatchingUpdates时统一执行，否则，就会同步执行。
  - 如果你现在去拉react的最新代码，会发现里面已经找不到Transcation这个类了。不过你可以在ReactFiberWorkLoop文件中，找到batchedEventUpdates这个方法。里面的实现基本是和transcation一样的，只是bool值换成了枚举
  - 如果setState不在这个transcation过程中执行，那么就会导致同步更新。比如说通过setTimeout方法，异步设置state。
  - React的batchedUpdates方法，也是类似Transcation的方式，将执行包裹在一个BatchedContext的环境中。从而实现批量调用。

- yjs通过 observe和observeDeep 实现了协同数据的监听
  - 当协同数据更新时，会触发监听的回调函数，回调函数会通过更新事件`YEvent`传入当前的更新内容，从而执行相应的操作。
  - YEvent包含transaction对象
# faq

## prosemirror-transaction vs mxgraph-transaction

- 效果类似
  - 在transaction内所有operations结束后，才触发modelUpdate事件

- [prosemirror transaction](https://prosemirror.net/docs/guide/#state)
  - prosemirror的tr类似steps/operations/actions工厂，可以不更新state
  - 一般先更新state/model，再更新视图

```JS
let state = EditorState.create({ schema })
let view = new EditorView(document.body, {
  state,
  dispatchTransaction(transaction) {
    let newState = view.state.apply(transaction);
    view.updateState(newState);
  }
});

// easiest way to create a transaction is with the tr getter on an editor state
let tr = state.tr
tr.insertText("hello")
let newState = state.apply(tr)
tr.delete(6, 8);
tr.setSelection(TextSelection.create(tr.doc, 3));
```

- [mxgraph 系列【4】：事务管理](https://juejin.cn/post/6844904193094860808)
  - mxGraph 的事务功能与此类似，当我们需要一次执行多个图形更新操作时，可将代码放入一个事务上下文中执行
  - 默认情况下在 try-catch 中出现异常中断时，异常语句之前的更新代码会被正常执行，而之后的代码则没有应用到图形上。此时，视场景需求可选择使用 mxGraphModel.prototype.currentEdit.undo 接口回滚所有操作
  - 事务接口支持嵌套调用

- [mxgraph](https://jgraph.github.io/mxgraph/docs/manual.html#3.1.2)
- there is a counter in the model that increments for every beginUpdate call and decrements for every endUpdate call. 
  - After increasing to at least 1, when this count reaches 0 again, the model transaction is considered complete and the event notifications of the model change are fired.
- This provide the ability in mxGraph to create separate transactions that be used as “library transactions”, the ability to create compound changes and for one set of events to be fired for all the changes and only one undo created. 
  - Automatic layouting is a good example of where the functionality is required.
# 🎞️ [cs-repeat: Marijn Haverbeke: Salvaging contentEditable: Building a Robust WYSIWYG Editor | JSConf EU__201510](https://www.youtube.com/watch?v=EEF2DlOUkag)
- some new editors like google docs drop contenteditable and create their own selection and caret
  - good xp
- problems: 
  - 1. mobile touch interfaces, native selection is subtle
  - 2. if u maintain your own selection and caret entirely, you get all the complexity of bi-directional text on your plate. you have to implement what the cursor is supposed to be doing if it moves left-to-right/r-to-l.
  - 3. if you are mixing Arabic or Hebrew, you get islands inside of your paragraphs that are running in different directions.
  - 4. for context menu like cut/paste, you have to decide the position/range.
# more
