---
title: lib-editor-rich-markdown-codebase
tags: [codebase, rich-markdown-editor]
created: '2021-06-02T17:07:07.909Z'
modified: '2021-06-02T17:07:33.920Z'
---

# lib-editor-rich-markdown-codebase

# guide

- 分析一个产品的实现
  - 使用的ui框架
  - 状态管理
  - css 样式和主题

- 细节亮点
  - 悬浮工具条支持给文本添加高亮背景色
  - 右对齐的图片不会占据整行空间，左侧部分仍然可以书写文字，甚至文字会自动换行不会被图片挡住
# faq
- 如何自定义组件样式，最好能直接使用现有react组件
  - 大部分组件是vanillajs，少部分使用基于react组件的NodeView

- 编辑器state数据结构是如何设计的
- 输入时如何更新dom元素
- plugins如何更新state
- extension vs plugin
- slash commands如何实现，如何添加新命令菜单

- 如何自定义toDOM, parseDOM(toJSON/nodeFromJSON类似)
- 上传图片、文件等资源的处理方法
- markdown 导入、导出

- 修改defaultValue后，不会rerender
  - 符合设计目标，要修改值需要使用value属性
# rich-markdown-editor.v11.11.1_202106_BSD
- RichMarkdownEditor组件的逻辑
  - 设置defaultProps、initialState
  - 依次初始化 
    - extensions、nodes、marks、schema、plugins、keymaps、serializer、parser、inputRules、nodeViews、view、commands
    - 后面的成员变量都是从extensions中直接计算出来的
  - react声明周期函数处理更新
  - 定义输入和其他事件的处理函数，大多数的逻辑都是调用setState
  - render()创建编辑器vdom的结构

## dom-elements

- 编辑器ui结构层次
- 顶层RichMarkdownEditor组件，都是自闭合的组件，没有children
  - StyledEditor: 包含编辑器的div
  - SelectionToolbar
  - LinkToolbar
  - BlockMenu

## render/view

- 基于react组件的NodeView
  - Embed
    - 使用react组件作为NodeView，toDOM使用了iframe
  - Image
    - 使用react组件作为NodeView，基于react-medium-image-zoom
  - Notice
    - 没有提供react组件作为NodeView
    - schema.toDOM()方法中直接执行ReactDOM.render()
  - 在min-app示例中，默认加载的nodeViews只有embed、image

## state

- 通过extension组织一个组件相关的各种数据
