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

- 要关注的重点
  - 编辑器state数据结构是如何设计的
  - 输入时如何更新dom元素
  - plugin如何更新state
  - extension vs plugin
  - slash commands如何实现
  - 如何自定义组件样式，最好能直接使用react组件的样式
    - 大部分组件是vanillajs，少部分使用基于react组件的NodeView
  - 如何自定义toDOM, parseDOM(toJSON/nodeFromJSON类似)
  - 上传图片、文件等资源的处理方法

- features-details
  - 悬浮工具条支持给文本添加高亮背景色
# todo
- stories
  - ~~long doc~~
  - 替换内置组件样式为成熟react组件库
  - 添加新组件，如Collapse、emoji、OJSCodeBlock、Katex、TabView, Slider, LocalForm(类似excel公式)、Accordion、References & Citations
    - 参考atlaskit、curvenote、bangle
    - 如何实现 Interactive Components/views/viewof
  - 优化复杂NodeView，比如table

- storybook
  - 没有对大多数组件创建story

- tests
  - 只有一个.test文件

- fix
  - 默认文本存在时，按回车新起一行，slash命令选择标题一，会将上一行修改为标题一，而不是当前行
  - 编辑器默认初始状态只有第一行且文本较短，此时通过选择文本使用悬浮工具条加粗后，悬浮工具条不会消失，工具条很大会挡住默认的短文本
    - 临时绕过：按回车，点击空行，悬浮条会自动消失
    - 方案1: 修改悬浮条的位置

- rewrite-markdown
  - parser
    - MarkdownSerializer/Parser to remark
  - serializer
  - 格式化配置
    - 列表、粗体、斜体等可预定义偏爱符号

- rewrite-more
  - class to hooks
  - nodeViews to ReactDOM.createPortal

- optimize
  - table
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
    - toDOM使用了iframe
  - Image
    - 使用了 react-medium-image-zoom
  - Notice
    - 在该组件的toDOM()方法中执行ReactDOM.render

- ？？？ min-app示例中，默认加载的nodeViews只有embed、image

## state

# keyboardnotes.v0.1.0_202101_NALic
- features
  - keyboard first
  - no vendor lock-in
    - all in markdown text format, with opt-in extended features
  - fast with modern web tech stacks
  - beautiful design
  - cloud sync, secure by auth0

- xp
  - 首页默认左右双栏布局(文档列表/预览)，通过jk按键可快速切换预览
  - 按enter可进入编辑模式，默认左中右3栏布局(文档列表/编辑/预览)

- todo
  - 标题输入后，不能按enter进入输入内容，必须手动将光标移到内容区
  - 文档列表支持多级文件夹
  - ~~编辑器支持配置指定的markdown特性~~，支持指定文本原样显示

- later
  - 官网demo按`c`键创建新笔记会有延迟，本地却没有延迟，可能是外网连接慢的问题

- xp-pros
  - reducer和action设计得非常好，可以直接从redux迁移到useReducer

- xp-cons
  - useReducer不支持thunk，所以dispatch异步action时要修改逻辑
