---
title: lib-editor-atlaskit-codebase
tags: [atlaskit-editor, codebase]
created: '2021-07-12T17:18:47.506Z'
modified: '2021-07-14T15:35:53.716Z'
---

# lib-editor-atlaskit-codebase

# guide

- 关注的重点
  - 编辑器插件的配置项过多时，如何处理更好

- src-branch-commit
  - [master-snapshot-v146.0.0](https://bitbucket.org/atlassian/atlassian-frontend-mirror/commits/92512bab8602ac0bc2bc8021a488c8fa81afe4dd)
# reading
- primary toolbar
- typeAhead
- codeblock

- comment/mobile variant
# issues-limitations
- 依赖redux的模块只有conversation

- 不支持动态改变编辑器底层prosemirror的schema
  - A significant issue is that we lose the ability to keep track of a user's history as the internal plugin state keeps a list of Steps to undo/redo (which are tied to the schema).
  - 尝试将部分plugin state同步到编辑器之外
# modules

## Atlaskit Editor/EditorProps

### common editor props

- appearance/ui
  - contentComponents
  - popupsMountPoint
  - popupsBoundariesElement

- toolbar
  - primaryToolbarComponents
  - secondaryToolbarComponents
  - useStickyToolbar

- quickInsert
  - insertMenuItems

- events/cb
  - saveOnEnter
  - onEditorReady
  - onChange
  - onSave
  - onCancel

### EditorPlugins

- extensionHandlers
- extensionProviders
- dangerouslyAppendPlugins

- contextPanel

- providers
  - emojiProvider
  - taskDecisionProvider
  - searchProvider
  - annotationProviders
  - collabEditProvider
  - presenceProvider
  - mentionProvider

- media
- elementBrowser
- codeblock
- UNSAFE_predictableLists
- mentionInsertDisplayName
- placeholder

- collabEdit

- features
  - featureFlags
  - disabled
  - allowBlockType, allowTasksAndDecisions, allowBreakout
  - allowTables
  - allowHelpDialog, allowJiraIssue
  - allowExtension
  - allowTemplatePlaceholders
  - allowDate, allowLayouts
  - allowTextAlignment, allowTextColor, allowDynamicTextSizing
  - allowIndentation
  - allowFindReplace
  - allowExpand

### more settings

- tracking and analytics
  - performanceTracking
  - trackValidTransactions
  - allowAnalyticsGASV3

- extensionProviders
  - new extension API. This eventually is going to replace `quickInsert.provider, extensionHandlers, macroProvider`.

## PortalProvider/PortalRenderer

### PortalProviderAPI

- 事件管理器的子类，非react组件，通过`ReactDOM.unstable_renderSubtreeIntoContainer`渲染react元素。
- 因为不是react组件，所有没有使用react context，不要被名称迷惑。
  - ??? render/forceUpdate方法执行渲染，但自身不是react组件，所以有没有挂载到react vdom tree上
- 实例变量portals映射表会保存所有dom对象及其对应的react元素

### PortalProvider

- 基于render props定义的普通react组件，this.portalProviderAPI作为数据，会传给render组件渲染。
- 主要逻辑都由PortalProviderAPI实现。
- constructor()中创建 PortalProviderAPI
- componentDidUpdate()中 `this.portalProviderAPI.forceUpdate();` 会更新portal中所有react元素

### PortalRenderer

- 本组件自身是一个普通react组件(注意createPortal返回值)，基于`ReactDOM.createPortal`渲染react元素。
  - 还将包含自身setState的更新方法注册到了portalProviderAPI，允许被更新。
  - PortalProvider是不使用react context而使用事件管理器传递数据典型案例。
 
- ??? 调用setState会触发本组件更新，但注册后从未被执行。PortalRenderer.state.portals始终为空。
  - 所以PortalRenderer组件起到的作用仅仅是挂载到vdom tree中占个位置

## codeblock

## EditorPlugins

### paste/clipboard

- clipboard实现比较简单

### base

- ? inlineCursorTargetPlugin
- ? betterTypeHistoryPlugin
