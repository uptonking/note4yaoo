---
title: lib-notb-observablehq-codebase
tags: [codebase, notebook, observablehq]
created: 2021-05-22T14:52:00.120Z
modified: 2024-06-30T03:21:16.943Z
---

# lib-notb-observablehq-codebase

# guide

# view-dom

- notebook主要内容区的div内，从上到下依次是

- 以iframe为容器的视图渲染区
  - 每个cell对应的样式类是 `.observablehq`，每个cell的ui为4个部分： `单元格间空白 + 单元格内容区 + 代码编辑区对应的空白区 + 单元格间空白`，注意相邻单元格间空白是同一个
  - 单元格具体内容前面都有 `::before` 伪元素，默认作为在最左侧的空白间隔，也可以用来展示刷新状态和频率
  - sandbox属性很复杂
  - src的值为https://uptonking.static.observableusercontent.com/worker/worker.cedfe7aa6ceba7790b312f0c8c7a9e84130753477202bdac35d927c4aacfa21d.html
  - iframe内的`<html>`，script的src为 https://static.observableusercontent.com/worker/worker.5fed33b28855690e1a17ff1a81d26c36c454faff125a1e23653add34544962f6.js

- 左侧指示区
  - 一个简单的div，`position: absolute; `，height是100%
  - 只作为占位符，指示区的交互菜单ui不在这里，在下面dib内

- 与内容对应的代码编辑区，容器样式类是dib
  - 每个cell的样式通过style属性行内样式的方式设置，每个cell的ui为4个部分： `单元格间空白 + 单元格内容区 + 代码编辑区对应的空白区 + 单元格间空白`，注意相邻单元格间空白是同一个
  - 每个cell内从上到下包括4个部分
    - `<div class="bg-light-blue drag-marker-before"></div>`与上个单元格间空白区中间的蓝线，默认隐藏
    - `<div class="bg-light-blue drag-marker-after"></div>`与下个单元格间空白区中间的蓝线，默认隐藏
    - 单元格主要编辑区的容器，样式类为 .pea
    - 单元格的左边的菜单指示区，样式类为 .pea.pointer
  - 每个cell代码编辑区的容器样式类为`. CodeMirror.cm-s-observable. CodeMirror-wrap`，height为auto
    - textarea
    - .CodeMirror-vscrollbar
    - .CodeMirror-hscrollbar
    - .CodeMirror-scrollbar-filler
    - .CodeMirror-gutter-filler
    - .CodeMirror-scroll
      - .CodeMirror-sizer
        - .CodeMirror-lines
          - .CodeMirror-measure
          - .CodeMirror-cursors
          - .CodeMirror-code 显示的源代码在这里!!!
      - div
      - .CodeMirror-gutters
