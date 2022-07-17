---
title: lib-editor-rich-markdown-codebase-extensions
tags: [codebase, extensions, rich-markdown-editor]
created: 2021-06-23T13:27:13.078Z
modified: 2021-06-23T13:27:56.975Z
---

# lib-editor-rich-markdown-codebase-extensions

# bugs

## bugs-highest

- 前面时slash/w时，按enter键无法换行
  - 在BlockMenuTrigger处优化

## bugs-low

- slash弹出菜单会被image挡住，甚至离得很远
  - 源码运行时偶尔会有此问题，特别是在屏幕宽度很窄时，或者上一行也是图片时当前行的弹出菜单位置就在很远的上面
  - 问题出现的时机，在图片caption描述紧邻的下一行，书写slash弹出菜单时，菜单会离得很远；若在caption的下两行，slash弹出菜单可以在当前位置挡住图片
  - 图片的文字描述使用的是contenteditable的p元素
# xp-todo
- roadmap
  - EditorView: provide nodeViews prop
    - createNodeViews支持react组件和普通prosemirror NodeView class

- 替换内置组件样式为成熟的react组件库
  - 模仿Image/Embed替换Notice、FencedCodeBlock/Table/Link, kbd
  - 替换Notice组件碰到问题
    - notice组件内容是文本，需要将PMDoc的内容添加进去，但Notice作为extension，component却不是标准的react组件，难以操作ref
  - 方案1: 重写react组件作为NodeView的部分
  - 方案2: 直接从PMNode中读取textnode的内容值
    - 方案2实现渲染后，若要实现编辑，要考虑悬浮工具条的位置
  - 使用react作为NodeView后，状态和dom就交给react管理，包括`contenteditable`编辑状态，react自身也会警告，特别是自身要处理退格键的状态
  - 可参考image如何实现添加图片caption描述及删除操作
  - ??? image编辑caption时没有触发pm和react的事件
  - 只有提供了uploadImage的回调函数，slash菜单中才会出现image选项

- 添加新组件到slash命令菜单，如Collapse、emoji、OJSCodeBlock、Katex、TabView, Slider, LocalForm(类似excel公式)、Accordion、References & Citations
  - 参考atlaskit、curvenote、bangle
  - 如何实现 Interactive Components/views/viewof
  - 参考word，ReviewComment
  - add: insert-image
  - refactor: search commands

- stories
  - ~~long doc~~
  - 优化复杂NodeView，比如table

- storybook
  - 没有对大多数组件创建story

- dependencies
  - update prosemirror-transform v1.2.5 to latest
  - update react-medium-image-zoom v3 to v4
  - update refractor v3 to v4

- tests
  - 只有一个.test文件

- rewrite-markdown
  - parser
    - MarkdownSerializer/Parser to remark
  - serializer
  - 格式化配置
    - 列表、粗体、斜体等可预定义偏爱符号
  - table

- rewrite-more
  - class to hooks
  - nodeViews to ReactDOM.createPortal
  - 传递给EditorView的nodeViews只支持react组件，不支持普通NodeView class

- keybinding
  - ctrl+enter: insert line below
  - ctrl+shift+enter: insert line above
  - shift+enter: run current cell (block)
- keybinding-cn-更好的支持
  - / 、
  - 1、

- 图片toolbar
  - 图片不支持缩放、拖拽缩放
# bugs-to-fix
- 编辑器默认初始状态只有第一行且文本较短，此时通过选择文本使用悬浮工具条加粗后，悬浮工具条不会消失，工具条很大会挡住默认的短文本
  - 临时绕过：按回车，点击空行，悬浮条会自动消失
  - 方案1: 修改悬浮条的位置

## nodes

- Headings只支持4级标题，应该扩展到支持6级标题

## marks

# nice-to-do
- 默认文本存在时，按回车新起一行，slash命令选择标题一，会将上一行修改为标题一，而不是当前行
  - 合并rtl的pr时，打乱了编辑器的状态处理逻辑，slash命令会作用在上一行
  - 原因其实是r-m-e不支持prosemirror-transform的最新版本
  - ref
    - [using the '/' to create a new row, the new row's pattern will override the row above the new one](https://github.com/outline/rich-markdown-editor/issues/427)
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
