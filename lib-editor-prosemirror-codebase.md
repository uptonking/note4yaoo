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

- parseDOM实现解析
- 编辑时要toDOM，特殊节点如footnote/编辑操作一般是通过insert菜单
# not-yet
- ？NodeView.update() 和plugin.view().update()的先后顺序
  - 简单测试结果
    - 先执行NodeView，再执行plugin.view的更新
  - 很多时候NodeView无需更新，就不会触发update
  - 要测试复杂的例子，观察声明顺序和触发顺序是否一致
# tutorials-examples
- 渲染出来的编辑器，默认内容为 `<p><br></p>`，`transaction.before.content.size`默认大小为2
- 编辑器默认支持按backspace退格键删除、del删除键
- 编辑器默认不支持enter换行
# state

# view

- 编辑输入时如何更新dom
  - 编辑器最外层样式类为`. ProseMirror`的div元素的`contenteditable`为true，所以编辑器内元素都可编辑
  - 但cursor光标由prosemirror自己实现
# plugin

# model

# transform

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
