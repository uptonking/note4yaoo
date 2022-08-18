---
title: lib-editor-guardian-dev
tags: [editor, guardian-editor, lib, prosemirror]
created: 2021-07-08T17:19:20.729Z
modified: 2021-07-08T17:19:56.328Z
---

# lib-editor-guardian-dev

# guide

- not-yet
  - ReactNodeView exec commands

- 给出的例子是向编辑器中插入复杂的表单，**使用了多个嵌套的编辑器**，每个块级节点可上下移动
  - 特别适合实现复杂的编辑器，比如支持多人协作填写的表单，但对于简单组件要慎用，因为wrapper封装太多了
  - [ProseMirror Elements Model ADR(Alternative dispute resolution替代性争议解决机制)](https://github.com/guardian/prosemirror-elements/blob/main/docs/decision-records/000-element-fields-model.md) 给出了4种数据建模方案
# codebase
- NodeView
  - 一个复杂Nodeview如imageElement只是一个PMNode，然后表单中的各项都作为子节点存在
  - 在`NodeView.update()`方法中触发执行注册过的`setState()`方法，从而更新react组件
    - 理论上在`plugin.view().update()`方法中触发执行setState也能更新
  - nodeViews的定义，使用的是方法，没有使用class
  - NodeView都没有使用contentDOM，ignoreMutation始终为true
  - 每个ReactNodeView组件都被ElementProvider包裹了一层，很冗余，包裹的目的就是注册setState到事件监听器
    - 每个组件都内置自己的事件管理器createUpdator，？？？很冗余
  - ReactNodeView的渲染使用的是ReactDOM.render

- FieldView
  - Represents a guardian-prosemirror-element view of a Prosemirror Node.
- CustomFieldView
  - a node that contains arbitrary fields that are updated atomically.
- ReactFieldView
  - 通过ref.current.appendChild将组件元素渲染到dom

- 代码架构
  - 几乎都基于函数实现，很少用class
# overview
- prosemirror-elements /21Star/MIT/202208/ts
  - https://github.com/guardian/prosemirror-elements
  - This Prosemirror plugin adds the ability to add custom 'elements' to a document.
    - Modelling non-text content in Prosemirror can be tricky. 
    - it provides an abstraction that makes it easy to write custom elements
  - A ProseMirror plugin for adding user-defined 'elements' containing arbitrary fields to a document.
  - renderer-agnostic (we use React as a default)
