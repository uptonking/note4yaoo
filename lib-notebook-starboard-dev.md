---
title: lib-notebook-starboard-dev
tags: [notebook, starboard]
created: '2021-05-06T09:41:49.951Z'
modified: '2021-05-06T09:44:07.629Z'
---

# lib-notebook-starboard-dev

> Starboard is an in-browser literate notebook that is extendable, portable, sharable and hackable.

# guide

- starboard pros
  - 可导出文件本地编辑，但导出文本是自定义格式.sbnb
  - 基于cell/block的编辑模式，适合数据分析
  - 可查看每区块的源码，也可查看整篇文档的源码
  - 可以从上到下一个个单元格执行，也可以全部执行
  - 支持多种单元格类型，包括md、latex、html、css、js、py
  - 全部在浏览器中执行，不需要服务器，不需要构建打包

- starboard cons
  - 跨区块选择文字很难用
  - 自定义一种新的文档格式, [Starboard Notebook format](https://github.com/gzuidhof/starboard-notebook/blob/master/docs/format.md)

- features
  - Browser-native
  - Portable
  - Hackable
  - Works on mobile devices

# ideas

- 导出到本地的tradeoff
  - local file的上传与下载，只支持简单样式与标准交互功能模块
  - 若需要细粒度地定制样式布局，则需要切换到高级编辑器，且下载时只能下载图片
    - (~~会忽略样式、忽略布局，因为样式太多了比excel更复杂~~)
    - 需要确定困难样式的属性值有哪些
    - 自定义复杂ui组件的代码太多就偏离重心了，要以计算逻辑的代码为主

- block区块内容编辑应该提供3种模式
  - split：对于代码类型区块，上面是代码、下面是执行结果
  - inline：对于文档类型区块，WYSIWYG
  - in-place-toggle：对所有区块，按切换键显示代码，按esc显示预览

- 当代码过多时，效果比不上直接使用ide来开发计算
- tableau只能使用专用的软件编辑和查看，不能导出到本地

# pieces
