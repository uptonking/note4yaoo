---
title: lib-editor-typewriter-codebase
tags: [codebase, typewriter]
created: 2023-02-09T12:26:00.002Z
modified: 2023-02-09T12:26:14.281Z
---

# lib-editor-typewriter-codebase

# guide

# not-yet
- lines是块级元素？
# codebase
- typewriter的delta结构就是一系列op集合和操作，非常类似经典OT算法

- 总共100行，每行`\n+字母`的场景
  - doc的length为293

- editor model数据变化后，会在update中自动触发视图更新
  - prosemirror的数据变化后，可以手动在dispatchTransaction中view.updateState(newState)

- Editor自身是一个eventemitter，在view模块初始化时，会注册view的onChange方法到editor
  - editor数据更新时，会触发执行view模块注册过的方法

- 触发rerender/update的场景
  - scroll
  - resize

## virtual-render

- virtualized-render示例要点
  - 仍将所有内容字符串放在内存
  - 但只显示指定区域大小的view元素
  - 需要计算每行元素的高度放在内存，这样在滚动被隐藏的区域只需要显示一个空div，高度为隐藏所有行的元素高度和

- dom元素结构，注意滚动位置不同时可视区域上下虚拟区域高度会变化
- div.editor contenteditable
  - div.spacer style="height: 4319px; "
  - p
  - p
  - div.spacer style="height: 319px; "
  - p end, 最后一个dom元素一直存在

- 滚动条的长度如何实现
  - 在内容上方显示一个height为 总元素*lineHeight 的空白div

- editor会监听第一个可滚动父元素的scroll事件
