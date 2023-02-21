---
title: lib-editor-editablejs-codebase
tags: [codebase, editablejs, slate-editor]
created: 2023-02-21T20:16:34.756Z
modified: 2023-02-21T20:17:00.638Z
---

# lib-editor-editablejs-codebase

# guide

# codebase

## model

- 在slate model上扩展了Grid、List类型的element
  - Grid和List都只是一系列的工具方法

- selection使用的是slate的定义

## view

- 编辑器内容div
  - userSelect: 'none'

- 编辑器内容div的下个兄弟元素是shadow dom，作为编辑器常用辅助元素
  - CaretComponent
  - DragCaretComponent
  - SelectionComponent
  - InputComponent/textarea-container

- TouchPointComponent

- Slots
  - block左边拖动按钮

## input

- 实现思路是在pointer事件的位置通过绝对定位放置一个oapcity为0宽约为1px的textarea来接收输入

## command

- reexport slate Transforms对象，修改了insertText/Nodes等方法
# more
