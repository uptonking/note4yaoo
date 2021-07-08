---
title: lib-editor-atlassian-dev-teemu-codebase
tags: [atlaskit-editor, codebase, editor, prosemirror]
created: '2021-07-05T18:12:03.081Z'
modified: '2021-07-05T18:12:24.491Z'
---

# lib-editor-atlassian-dev-teemu-codebase

# guide
- EditorPlugin使用的是纯函数，而full-v2中Extension使用的是class
# codebase-atlassian

## not-yet

- 在full-v2示例中，ReactNodeView的BlockQuote.tsx组件会执行 `useListenProps(handleUpdate)`，实际是在向portalProvider注册事件函数，handleUpdate中可以包含setState吗

- plugin state变化时，为什么能触发WithPluginState处的react组件更新
  - plugin.view定义了update()方法，但使用的都是editorView.dispatch
  - plugin.state.apply使用类似redux的switch-case更新方式，每次dispatch都会执行所有注册的cb函数；其中WithPluginState的setState方法也注册到了里面

- 在callbackRef函数中调用forceUpdate()方法，各生命周期的执行顺序如何
  - Calling `forceUpdate()` will cause `render()` to be called on the component, skipping `shouldComponentUpdate()`.
  - [React lifecycle methods diagram](https://projects.wojtekmaj.pl/react-lifecycle-methods-diagram/)

- 为什么ReactEditorView用了2个事件管理器，providerFactory、eventDispatcher
  - providerFactory通过props传递过来，管理全局providers
  - eventDispatcher直接传递给pm-plugins

- 如何在typeAheadPlugin中修改ReactNodeView
  - 根本没有使用NodeView，不存在这个问题
  - 因为Plugin.view()和NodeView都可以定义update()方法
  - pm执行dispatchTransaction时, ~~可手动修改globalContextVal的二级属性值，然后forceUpdate~~
  - 常用方法是在globalContextVal的二级属性存放一个事件管理器，然后将顶层react组件的setState方法注册到事件管理器，在dispatchTransaction时执行此方法会forceUpdate所有子组件，react组件的props中可以向事件管理器注册处理函数，用来计算新的vdom，然后在diff+patch后更新dom
  - 其实没有直接通过函数调用进行更新，而是通过事件管理器的映射表流程，可以在不同时刻注册各种事件处理器，然后触发时按一定顺序执行，最后两者都更新了

- 多个复杂插件的执行顺序和最佳实践

- watching
  - eventDispatcher中事件函数的注册与执行时机
  - slash commands主要实现在typeAheadPlugin
  - how CodeBlock works

## pieces

- EditorPlugin的配置项非常多
  - 常见：nodes、plugins
  - toolbar
  - floatingToolbar
  - quickInsert

- prosemirror plugin view
  - TypeAhead组件的渲染和更新由typeAheadPlugin控制，而不是自定义NodeView，但更新方法是通用的，都基于pubsub
  - 注意TypeAhead组件渲染的位置提前指定好了

- ReactNodeView
  - 渲染react组件NoeView到portal使用的是ReactDOM.unstable_renderSubtreeIntoContainer()
  - 更新每个ReactNodeView组件时，有判断一次hasReactContext，若没有使用，则停止更新
  - ??? React组件没有state，只用props，因为NodeView的update方法每次都会传入新的props，这样设计正确吗

- ReactEditorView
  - 在constructor()中创建pm-EditorState，这里就综合计算出了所有prosemirror需要的schema、plugins、doc等
  - 在callbackRef中创建pm-EditorView，还会触发onCreated钩子函数
- FullPage
  - 提供了定位布局配置
  - 放置了popup、toolbar
  - ContentArea中平级放置 PluginSlot、PMEditor

- quickInsertPlugin
  - 提供了slash菜单项的初始化方法

- typeAheadPlugin
  - 提供了contentComponent返回的组件来渲染输入斜杠文字后弹出菜单会出现的条目

- WithPluginState
  - subscribe观察插件状态变化有2种方式，根据PluginState中是否含有subscribe属性
    - pluginState.subscribe(handler);
    - eventDispatcher.on(pluginKey.key, handler);

- PortalProvider/PortalProviderAPI
  - PortalProvider基于PortalProviderAPI实现
  - PortalProviderAPI实现了EventDispatcher接口，用来更新所有ReactNodeView
  - plugin.view处指定的contentComponent组件的更新由一路传下来的ReactEditorView.dispatch触发，因为里面会执行包含setState()方法的逻辑，
    - 而且这些组件的父元素与ReactEditorView平级，plugin.view处react组件的渲染不会触发ReactNodeView的渲染，因为不是一颗子树

- EditorActions
  - eventDispatcher：？？？作用是什么，全部被作为参数传递了，本Editor class内并未直接使用
# codebase-full
- editorPlugin和pmPlugin名称上很容易混淆，不如tiptap设计的extension，它们功能上都是封装某种组件紧密相关的操作

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
