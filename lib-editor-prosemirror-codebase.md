---
title: lib-editor-prosemirror-codebase
tags: [codebase, editor, prosemirror]
created: '2021-06-02T17:13:01.416Z'
modified: '2021-06-02T17:13:37.692Z'
---

# lib-editor-prosemirror-codebase

# guide

- 要关注的重点
  - 编辑器state数据结构是如何设计的
  - 输入时如何更新dom元素
  - plugin如何更新state

- minimal example渲染出来的编辑器，默认内容为 `<p><br></p>`，`transaction.before.content.size`默认大小为2
# prosemirror-react-dev

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
# state

# view

# plugin

# model

# transform
