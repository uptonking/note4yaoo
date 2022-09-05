---
title: lib-editor-prosemirror-dev-nodeview
tags: [editor, lib, prosemirror]
created: 2021-07-02T18:23:48.398Z
modified: 2021-07-02T18:24:12.955Z
---

# lib-editor-prosemirror-dev-nodeview

# guide

- 基于react组件实现NodeView要注意区分两处逻辑
  - 一般在NodeView class的constructor()方法中创建react VDOM
  - 然后在NodeView class的update()方法中更新vdom
  - 更新时常使用基于pubsub的发布订阅模式

- nodeViews作为一个props的定义
  - `image(node, view, getPos) { return new ImageView(node, view, getPos) }`本身是一个方法，只是返回值经常创建类的实例
  - NodeView本身是一个Interface而不是class，所以可以像guardian-pm-elements一样定义一个工厂方法，返回值就是实现了NodeView接口的对象
# problems-not-yet
- how to manage a list of NodeViews

- complicated/big nodeview
  - 可参考guardian-prosemirror-elements将编辑器作为NodeViews的例子

- nodeview partially editable like textarea

## NodeView vs decoration

- 渲染PMNode的控制权不同
  - NodeView可完全自己控制
    - By default, document nodes are rendered using the result of the `toDOM` method of their spec, and managed entirely by the editor.
    - If you provide a `contentDOM` property, the library will render the node's content into that, and handle content updates. 
    - If you don't, the content becomes a black box to the editor, and how you display it and let the user interact with it is entirely up to you.
  - Decorations make it possible to influence the way the document is drawn, without actually changing the document.
    - 在plugin的apply()方法中可以add/remove decorations
    - 一般用来装饰样式，而不是加减内容组件

- NodeView需要自己定制toDOM/parseDOM
  - decoration一般不修改doc

- 可以通过修改更新decoration来触发NodeView更新
