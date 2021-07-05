---
title: lib-editor-atlassian-dev-teemu-codebase
tags: [atlaskit-editor, codebase, editor, prosemirror]
created: '2021-07-05T18:12:03.081Z'
modified: '2021-07-05T18:12:24.491Z'
---

# lib-editor-atlassian-dev-teemu-codebase

# codebase-atlassian
- not-yet
  - 在callbackRef函数中调用forceUpdate()方法，各生命周期的执行顺序如何

- watching
  - eventDispatcher如何传播事件
  - slash commands
  - CodeBlock works
# codebase-full
- editorPlugin和pmPlugin名称上很容易混淆，不如tiptap主导的extension，它们功能上都是封装某种组件紧密相关的操作

- EditorPlugin的设计将创建pm-Plugin对象的过程又封装了一层，层次有点深
  - 但schema、keymap等都在不同文件夹，灵活性很高
- EditorPlugin使用的是纯函数，而full-v2中Extension使用的是class
# codebase-full-v2
- Editor的api使用的是composition的模式
  - 优点是灵活性高
  - 缺点是隐式顺序规定

```JS
<div>
  <Editor>
    <Base />
    <BlockQuote />
  </Editor>
  <PortalRenderer />
</div>
```

- 每次执行dispatchTransaction()，都会rerender `PortalRenderer`组件中所有的ReactNodeViews，性能消耗大吗
  - 可以类比react，每次都会recreate触发setState的组件及其子树构成的vdom，所以最好在每个组件都实现shouldComponentUpdate

> todo 如何优化

- 对于这里的应用场景，`PortalRenderer`的children是一个扁平的数组，数组每项都是一个ReactNodeView，所以每次rerender都会创建所有ReactNodeViews
- 可以尝试类似react-virtualized的滑动窗口，只渲染可见部分，因为屏幕大小有限，就算每次重新渲染，实际执行的render()和渲染出的dom节点都不会太多；
  - 但整个文档的结构不是每项都相似的list结构，如何拆分文档难度较大

- createDefaultProviders()会创建并返回默认的全局provider对象
  - AnalyticsProvider，普通类，用于日志打印监测
  - APIProvider，普通类，实现socket相关功能
  - ExtensionProvider，普通类，基于Set
  - PluginsProvider，普通类，基于 EventDispatcher
  - CollabProvider
  - PortalProvider，普通类，
  - EditorViewProvider，普通类，提供操作文档的方法，replaceDocument、replaceState

- ReactEditorContext默认使用createDefaultProviders的返回值作为全局传递的value
# codebase-minimal
- 核心的Editor组件
  - 在`componentDidMount()`中创建edittorState和editorView
    - 为什么createEditorView()后要执行`this.forceUpdate();`，因为Editor组件没有传入props，没有children，也没有state，所以正常情况下不会rerender，pm编辑器自己管理pm-state，然后通过`editorRef`挂载到最外层div上
    - 这里执行forceUpdate()是在生命周期constructor -> render -> didMount中触发，这里才第一次真正将编辑器渲染到dom，且只执行一次除非remount，callbackRef一般只在mount和unmount时触发
  - shouldComponentUpdate()始终return false

- plugins
  - baseKeymap + undo/redo + blockquote-keymaps

- 定义了两种blockquote PMNode的schema，parseDOM都会解析为`tag: blockquote` PMNode
  - pmBlockquote类型节点有attrs属性，且toDOM会渲染处attrs中的数据
  - blockquote类型节点无attrs
- 提供了blockquote类型对应的的ReactNodeView
  - 通过 `ReactDOM.render` 渲染react元素到this.dom
  - 在NodeView class的constructor(){}中，`this.contentDOM`会作为child，通过操作react组件的ref`ref.current.customAppend`添加到该react组件所在的dom

```JS
ReactDOM.render(
  <BlockQuote ref={this.ref} />,
  this.dom,
  this.putContentDomInRef
)

putContentDomInRef = () => {
  this.ref.current.customAppend(this.contentDOM)
}
```
