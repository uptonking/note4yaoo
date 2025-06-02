---
title: lib-editor-codemirror-codebase
tags: [code-editor, codebase, codemirror]
created: 2024-05-02T06:41:04.049Z
modified: 2024-05-02T06:41:19.983Z
---

# lib-editor-codemirror-codebase

# guide
- codemirror的架构主要分3方面: model/state, view, extension
  - extension的扩展方式也是这3方面，state-field, deco, view-dom/event

- editor业务的数据更新
  - 修改编辑器内容
  - 修改其他状态
# dev-debug
- 编辑器最外层contenteditable的dom在调试时可以store as global variable，在属性上可拿到 cmView, 可以进一步拿到 cmView.view/ cmView.view.state
# not-yet
- document是否总以换行符结尾
# overview

# architecture

- codemirror的整体架构和extension的架构都是从model/view/update三方面考虑的
  - 在mvu架构的基础上通过provide暴露api
# extensions/plugins

# state

# view

## widget

- 通过eq和updateDOM多层拦截判断来减少重绘
- `toDOM`
  - 具体实现可以调用this.updateDOM()，也可以不调用
- `updateDOM`
  - if return true, the original dom is kept and updated
  - if return false, the original dom is destroyed and recreated
- `eq` is used in merge widgets/decorations
# styling
- 编辑器获取到焦点时 .cm-editor 的dom元素会增加样式类 .cm-focused
# more
