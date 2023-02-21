---
title: lib-editor-typewriter-codebase
tags: [codebase, typewriter]
created: 2023-02-09T12:26:00.002Z
modified: 2023-02-09T12:26:14.281Z
---

# lib-editor-typewriter-codebase

# guide

- dev-to
  - 支持表格
# not-yet
- 示例文档有100行，每行`\n+字母`的场景
  - doc的length为293？
# codebase
- lines是块级元素
  - 类似quill中的blocks, formats, embeds

- editor model数据变化后，会在update中自动触发视图更新
  - prosemirror的数据变化后，可以手动在dispatchTransaction中view.updateState(newState)

- Editor自身是一个eventemitter，在view模块初始化时，会注册view的onChange方法到editor
  - editor数据更新时，会触发执行view模块注册过的方法

- 触发rerender/update的场景
  - scroll
  - resize

## model/TextDocument/Delta

- typewriter的delta结构就是一系列op集合和操作，非常类似经典OT算法

- 模型中的数据editor.doc并不会包含所有op记录，只包含insert，不包含delete/retain
  - 和quill的parchment结构非常类似，都只包含insert
  - 带格式的富文本会

## view/render

### virtual-render

- virtualized-render示例要点
  - 仍将所有内容字符串放在内存
  - 但只显示指定区域高度大小的view元素
  - 需要计算每行元素的高度放在内存，这样在滚动被隐藏的区域只需要显示一个空div，高度为隐藏所有行的元素高度和

- dom元素结构，注意滚动位置不同时可视区域上下虚拟区域高度会变化
- div.editor contenteditable
  - div.spacer style="height: 4319px; "
  - p
  - p
  - div.spacer style="height: 319px; "
  - p end, 最后一个dom元素一直存在

- 🤔 虚拟渲染时每行高度如何计算
  - p标签的mt和mb为16px=1rem，但单行高度与语言相关，英文一行height为18px，中文一行height为24px
  - https://codepen.io/uptonking/pen/QWVwNRr
  - 👉🏻 每行的高度依赖滚动时去计算，开始必须是从上向下的滚动，所以会动态渲染并计算每行高度，然后缓存已滚动行的高度
  - 后面未滚动行的行高会使用averageHeight，取的是已滚动行高度的平均值

- 滚动条的长度如何实现
  - 在可见区域上方和下方显示一个height为 已滚动元素和未滚动元素个数*averageHeight 的空白div

- editor会监听第一个可滚动父元素的scroll事件，然后计算当前需要渲染的元素范围

## commands/op/editor-change

- 主要基于 MutationObserver 获取用户输入来更新editor.doc模型
  - 在beforeinput中处理了Gboard输入bugs、historyUndo

## collab
