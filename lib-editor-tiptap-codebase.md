---
title: lib-editor-tiptap-codebase
tags: [codebase, editor, headless, tiptap]
created: '2021-06-02T17:10:08.793Z'
modified: '2021-06-02T17:10:50.151Z'
---

# lib-editor-tiptap-codebase

# guide

# modules
- class `Editor` extends EventEmitter
  - constructor()
    - 创建基本commandManager/extensionManager
    - 构造函数中注册了各种事件处理函数 onCreate/onUpdate/onSelectionUpdate/onTransaction/onFocus，监听器只在构造函数这里添加
  - editorView.dispatchTransaction()中会执行很多事件处理函数
  - 暴露了很多api方法
  - new EditorView()创建时只传入了state.doc，然后plugins通过state.reconfigure({plugins})传入，再通过editorView.setProps设置nodeViews
  - store the editorView instance in the DOM element. So we’ll have access to it for tests.

- 常用类型定义
  - export type AnyExtension = Extension | Node | Mark
  - export type Extensions = AnyExtension[]

- ExtensionManager
  - 会先对所有extensions进行排序
  - 遍历各个extension，注册各种事件处理函数
  - getNodeViews()

- Extension class
  - 属性：name, parent, child, options
  - extend()内部创建了一个新的extension对象作为child属性值
  - configure()会调用extend()返回一个新的extension对象
- Node class
  - Node的属性与Extension大体相同，用来创建extension对象
- core-extensions
  - Blockquote, CodeBlock, Heading, ListItem...
  - 都是通过Node.create(extOptions)创建
  - 传入的参数包含schema定义数据
  - schema.toDOM()会使用传入的renderHTML()方法定义

- NodeView class
  - 支持拖拽
- ReactNodeView class
  - 每个ReactNodeView组件都会被 ReactNodeViewContext. Provider 包裹
  - todo 很冗余
- ReactNodeViewRenderer function
  - 是一个高阶组件，返回一个函数作为React组件
  - 最终会返回return new ReactNodeView(component, props, options)

- react相关实现显得比较杂乱
  - 因为很多组件既提供了灵活性高的hooks，又提供了灵活性低但开箱即用的react组件
