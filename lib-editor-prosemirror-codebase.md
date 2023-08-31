---
title: lib-editor-prosemirror-codebase
tags: [codebase, editor, prosemirror]
created: 2021-06-02T17:13:01.416Z
modified: 2021-06-02T17:13:37.692Z
---

# lib-editor-prosemirror-codebase

# guide

- 编辑器的设计与实现
  - 最核心的文档数据结构
  - 选区与slice
  - 节点类型与约束
  - 文档操作 operation与transform
  - editorState
  - editorView
  - 协作

- 要关注的重点
  - 编辑器state数据结构是如何设计的
  - plugin如何更新state

- 用户输入时如何更新editorState
  - 获取输入内容，beforeinput/keydown/MutationObserver
  - 寻找合适的插入位置
  - 替换节点
  - 返回新文档
  - 更新选取等其他状态

- editorState变化时如何更新dom元素
  - 更新viewDesc
  - node
  - mark
  - decoration
  - renderDescs 更新dom

- PMENode与DOM
  - parseDOM实现解析
  - 编辑时要toDOM，特殊节点如footnote/编辑操作一般是通过insert菜单
# roadmap
- plugin既可以包含state，也可以包含view，显得混乱

- 直接将plugin的状态挂在editorState对象上
  - @see EditorState.create
# not-yet
- branch的实现思路
  - 保存各branch的id-name/delta-changes/baseBranchId，然后根据以上数据获取分支对应的所有delta-changes，然后计算出文档对象数据
  - 分支相关数据:
    - change表: branch-id-name, author, timestamp(实现版本)
    - branch表: branch-id-name, base-branch-id, start-timestamp, latest-timestamp

- ## editor pluginState、pluginView的更新顺序
- ？NodeView.update() 和plugin.view().update()的先后顺序
- 简单测试结果
  - 先执行NodeView，再执行plugin.view的更新
- 很多时候NodeView无需更新，就不会触发update
- 要测试复杂的例子，观察声明顺序和触发顺序是否一致

- ## 支持动态改变schema的变通实现方式？

- ### schema中node约束的定义使用context-expression字符串，如何设计为更好的/类型友好的方式

- ## beforeinput的优点与使用

- ## setTimeout的回避方法
- 目前setTimeout的主要使用场景
  - android输入、ios
  - composition事件
  - 鼠标相关事件，如拖拽mightDrag
  - focus事件

- ## decoration与NodeView的理解
- 装饰集是作用于文档内容的，而不是作用于文档模型的。
- Decoration与编辑器模型/Node/Mark并无直接关系，可以用于高亮文档之类的目的

- NodeView是与schema中的node定义直接相关的

- ## prosemirror的step与ot的operation的关系

- ## readonly即editable为false时，编辑器不支持什么行为

- ## 如何实现virtualized虚拟化渲染
- 参考思路，先实现分页，再渲染前后2页
# architecture
- dataflow
  - 先更新state/model，再更新view

```JS
let state = EditorState.create({ schema })
let view = new EditorView(document.body, {
  state,
  dispatchTransaction(transaction) {
    let newState = view.state.apply(transaction);
    view.updateState(newState);
  }
})
```

- model-layer
  - Node树
  - model更新基于node.copy复用数据，❓只是局部更新，是immutable的吗

- view-layer
  - ViewSpec vdom
  - NodeView 与模型层数据紧密相关，仅在相关node数据变化时update
  - Decoration 与模型层数据相关，可与具体节点无关
  - plugin view 可控制EditorView的dom之外的元素渲染和交互
# state
- state内容
  - doc、selection、storedMarks、plugins-state
  - config、schema
  - tr创建新的transaction

- state是plugins的容器

- editorState的更新总是2步
  - const newState= new EditorState()
  - newState[pluginKey] = pluginNewState; 

- immutable state
  - 分析keypress插入文本
  - 会触发 view.dispatch(view.state.tr.insertText(text).scrollIntoView()); 
  - dispatch()会执行view.updateState(this.state.apply(tr)); 
  - 其中state.apply总是返回new EditorState()，数据对象引用变了，但变化的节点Node是通过copy()替换的，内容尽可能复用了

- [recommended way to communicate from a plugin to a NodeView](https://discuss.prosemirror.net/t/how-can-i-communicate-from-a-plugin-to-a-custom-nodeview/952)
  - it seems possible to decorate the NodeViews and then update the decorations when the external data changes

- EditorState和plugin.state的首次创建顺序
  - `EditorState.create()` > 所有plugin.state.init() > `new EditorView()` > **所有plugin.view()**  > 所有plugin.state.apply() > editorView.dispathTransaction(tr) > ~~部分~~插件plugin.view().update()
  - 注意：NodeView的init()在实际创建Node时才执行，编辑器中没有此类型的Node时不会创建和更新
  - 实例场景：在plugin.view()中也可以创建和更新dom，基于ReactDOM.render()，参考Aditor，功能上可以部分替代NodeView，但需要自己控制update的内容; 
  - plugin.view()方法自身只执行一次，但返回值中的view().update()后面编辑器更新时会多次执行

- 不涉及NodeView(如只按回车键)时，EditorState和plugin.state的更新顺序
  - 所有plugin.state.apply()依次执行 > editorView.dispathTransaction(tr) > plugin.view().update()

- 涉及NodeView时，EditorState和plugin.state的更新顺序
  - 所有plugin.state.apply()依次执行 > editorView.dispathTransaction(tr) > `NodeView.init()/update()` > plugin.view().update()
# view
- view模块
  - vdom定义、decoration、selection同步、domObserver状态同步、dom-coords、clipboard处理、浏览器兼容性处理

- decoration vs NodeView vs plugin.view()
  - decoration不影响prosemirror document
  - NodeView可以完全定制渲染逻辑和更新逻辑，只有在编辑器中存在该类型PMNode时，才会创建和更新
  - plugin.view()只要EditorView更新了，就会被调用，因此要注意控制更新逻辑提高性能

- editorView.props存放了editorState，获取时会同步获取最新的
  - this._props.state = this.state

- 编辑输入时如何更新dom
  - 编辑器最外层样式类为`. ProseMirror`的div元素的`contenteditable`为true，所以编辑器内元素都可编辑
  - 浏览器编辑发生后，通过domObserver将修改同步到editorState
# plugin
- plugin-dev
  - undo和collab都作为plugin实现
  - plugin.state的初始化时机在editorState之后
  - 可影响op的执行

- pluginProps和editorProps基本相同，方便理解和扩展编辑器的能力

- state允许plugin有自己的状态
  - init和apply分别提供初始值和更新逻辑

- view允许plugin影响ui
  - update + destroy

- filter/appendTransaction允许影响action/op
# model

# transform
- Transactions track changes to the document, but also other state changes, like selection updates and adjustments of the set of storedMarks
  - you can store metadata properties in a transaction
# tutorials-examples
- 渲染出来的编辑器，默认内容为 `<p><br></p>`，`transaction.before.content.size`默认大小为2
- 编辑器默认支持按backspace退格键删除、del删除键
- 编辑器默认不支持enter换行
# prosemirror-mdx-dev
- 一种实现思路是使用react组件作为NodeView，视图层用react封装prosemirror-view实现，一般基于portal渲染
  - pros：使用丰富的react组件和prosemirror插件
  - cons：很多地方需要修改，灵活性有一点点限制；封装较多，影响性能
  - ref
    - atlaskit-editor

- 一种实现思路是不使用prosemirror-view，完全基于react实现视图层，这样mdx节点生成的react组件可直接使用
  - pros：灵活性极高，react视图部分完全由开发者控制
  - cons：无法使用现有的依赖pm-EditorView的插件，需要自己实现同步selection等；工作量大；
  - ref
    - https://github.com/marionebl/prosemirror
    - https://www.npmjs.com/package/@marduke182/prosemirror-react-view

- 一种思路是自定义schema/toDOM，实现 mdx node > PMNode > dom，基于prosemirror-view来渲染，视图层不需要react
  - pros：不依赖react
  - cons：jsx到dom转换的自定义schema，仍然避免不了创建react tree到渲染的dom的过程，可以借助于类似svelte的jsx aot工具
  - ref
    - https://github.com/Novartis/mdx-utils
    - https://github.com/marceloadsj/babel-plugin-react-aot
# prosemirror-react-dev
- prosemirror-react-view
  - 基于react组件和类似redux的发布订阅模式，自己实现了prosemirror-view的视图层
  - 虽然很多逻辑错误，但测试可用了

## 使用react组件作为nodeViews的方法

- @atlaskit/editor(prosemirror-react-typescript-example)
- In case you want to use nodeViews as React components, they use `portalProvider` to render themselves as portals which are updated inside each `dispatchTransaction` call to flush the changes only once (instead of updating them in each update call in each `ReactNodeView` separately).
  - Syncing PM editor state to React components isn't always that easy and definitely there are still some enhancements that I should do.

- prosemirror-react-nodeviews/bangle.dev-editor/tiptap
- 原理是`ReactDOM.createPortal(<Component />, container, shortid.generate()); `，事件传播会根据组件在react tree中的位置，而不是根据在真实dom tree中的位置
  - 先手动创建div，然后通过ReactDOM.createPortal将react组件渲染到dom上
  - [Updated ProseMirror + React example with TypeScript and styled-components using NodeViews](https://gist.github.com/TeemuKoivisto/771e6522f092fa1f0ff9eab7545f8fad)
- cons
  - 每个react组件形式的NodeView实例对象，都会创建一个被Provider包裹的组件

- pubpub-editor
  - 原理是 ReactDOM.render，不推荐，因为每个NodeView的更新都会更新dom，应该尽量减少dom操作
  - `React.Component.render()` only creates the virtual DOM. It does not add it to the actual browser DOM.
  - `ReactDOM.render()` does both. It creates (or updates) the virtual DOM, and then additionally adds it to the actual browser DOM.
