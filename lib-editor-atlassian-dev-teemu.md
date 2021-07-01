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
  - 可以在NodeView中直接读取PMNode.attrs的值

- > ReactNodeView-state变化后，如何通知 prosemirror
  - 手动创建newState，然后手动dispatch()

- prosemirror-view更新的方法
  - dispatchTransaction()
  - dispatch()

- ReactNodeView更新的方法
  - react组件的useListenProps可以传入一个方法，会在 dispatchTransaction 生成newState和updateState后，随着`portalProvider.flush()`被调用而执行
  - 注意执行完后不会自动删除，要取消事件需要手动unsubscribe

- 对于使用react组件作为NodeView的情况，`this.contentDOM`是`ReactNodeView`的child，`nodeViewReactElement`是`this.dom`的children
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
# discuss
- ## useSsrLayoutEffect vs useLayout
- https://github.com/styled-components/styled-components/issues/3369
- `useLayoutEffect` does nothing on the server, because its effect cannot be encoded into the server renderer's output format. 
  - This will lead to a mismatch between the initial, non-hydrated UI and the intended UI. 
  - To avoid this, useLayoutEffect should only be used in components that render exclusively on the client.
