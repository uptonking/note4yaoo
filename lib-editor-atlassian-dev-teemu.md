---
title: lib-editor-atlassian-dev-teemu
tags: [atlaskit-editor, community, editor]
created: '2021-07-01T10:26:24.665Z'
modified: '2021-07-01T10:27:24.764Z'
---

# lib-editor-atlassian-dev-teemu

# guide
- 编辑器的交互与更新
  - 用户在普通pm-view编辑输入时，会自动触发 dispatchTransaction
  - 用户在react-NodeView编辑输入时，可手动触发dispatch()

- pm-state变化后，如何通知ReactNodeView
  - 可以在NodeView.update()中直接读取PMNode.attrs的值，但一般使用contentDOM，然后将新值作为新props传入react组件

- > ReactNodeView-state变化后，如何通知 prosemirror
  - Toolbar.tsx中使用了 viewProvider.execCommand()，一般command都会触发dispatch，对于简单样式操作星而非文档修改型的command，可以触发空dispatch
  - 手动创建newState，然后手动dispatch()
  - 一般流程：注册/hook up到 Plugin.view.update(){}或dispatchTransaction(){}
  - BlockQuote.tsx组件自身并不直接持有eidtorView，但props传入了能稍后执行的方法

- > 一个ReactNodeView-state变化后，如何通知另一个 ReactNodeView
  - 依赖context或发布订阅的事件
  - EditorViewProvider.replaceState()

```JS
// Fire an empty transaction to trigger PortalProvider to flush the created nodeViews
const tr = this.editorView.state.tr;
this.editorView.dispatch(tr);
```

- prosemirror-view更新的方法
  - dispatchTransaction()
  - dispatch()

- ReactNodeView更新的方法
  - react组件的useListenProps可以传入一个方法，会在 dispatchTransaction 生成newState和updateState后，随着`portalProvider.flush()`被调用而执行
  - 注意执行完后不会自动删除，若要取消事件需要手动unsubscribe

- 对于使用react组件作为NodeView的情况，`this.contentDOM`是`ReactNodeView`的child，`nodeViewReactElement`是`this.dom`的child

- 实现原地实时编辑katex的方法/inline-renderer
  - prosemirror-view to math-NodeView
  - math-NodeView to prosemirror-view: editorView.focus() 
  - 还要区分从左边进入还是右边进入
  - [Replicating Typora’s Inline/Display Math Editing](https://discuss.prosemirror.net/t/replicating-typoras-inline-display-math-editing/2906)

- 实现原地实时编辑code block的方法/block-render

- tips
  - implementing of the event-flow from the actions/key-press plugins to the plugin state, which would then notify the React components through an event-dispatcher
# todo-xp
- useSsrLayoutEffect 替换为 useEffect
- 将ReactNodeView作为Editor组件的children，这种api不合适，因为顺序有要求
# codebase-full-v2
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
- 核心Editor组件
  - 在componentDidMount()中创建edittorState和editorView
  - shouldComponentUpdate()始终return false
- plugins
  - baseKeymap + undo/redo + blockquote
- 定义了两种blockquote PMNode的schema，parseDOM都会解析为`tag: blockquote` PMNode
  - pmBlockquote节点有attrs属性，且toDOM会渲染处attrs中的数据
  - blockquote节点无attrs
- 提供了blockquote的ReactNodeView
  - 通过 ReactDOM.render 渲染react元素到this.dom
  - 在ReactNodeView中，this.contentDOM会作为child添加到BlockQuoteReact组件的ref.current.append
# discuss
- ## useSsrLayoutEffect vs useLayout
- https://github.com/styled-components/styled-components/issues/3369
- `useLayoutEffect` does nothing on the server, because its effect cannot be encoded into the server renderer's output format. 
  - This will lead to a mismatch between the initial, non-hydrated UI and the intended UI. 
  - To avoid this, useLayoutEffect should only be used in components that render exclusively on the client.
