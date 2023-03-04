---
title: lib-editor-slate-features-table
tags: [features, slate-editor, table]
created: 2023-02-27T19:06:17.436Z
modified: 2023-02-27T19:07:31.111Z
---

# lib-editor-slate-features-table

# guide

# dev-to
- 如何去掉event-emitter
  - 难点在需要在最外层容器触发内层的 keydown/mousedown

- 将选区变化的逻辑移出react
  - 选区逻辑本身就在slate，只是视图层需要显示单元格选区，似乎无法将单元格选区加入editor.selection
# slate-table
- basics
  - [x] 方向键能准确移动光标
  - [x] 方向下键，光标退出表格
    - [ ] 合并单元格后不work

- copy-paste
  - 单元格内容

- undo/redo

- 按键、光标、选区
  - tab/shift+tab键移动选区到下/上一个单元格
  - 选择单元格内容
  - to-discuss
    - enter键在单元格内换行(~~还是新建一行~~)

- header
  - 切换表头深色
  - header-menu
    - readonly
  - caption

- row
  - 拖拽调整行高度
  - [x] 在当前行上方/下方插入新行
  - [x] 删除行

- col
  - 拖拽调整列宽度
  - [x] 在当前列左边或右边插入新列
  - [x] 删除列

- cell
  - 单元格可选支持nested content，表中表
  - [x] 合并、拆分单元格

- later
  - table themes
  - api & docs
  - 复制粘贴优化
  - 统一selection和table-selected-cells

- maybe
  - 完全自绘表格选区
  - 整个编辑器支持先渲染文本，此时表格渲染loading占位符，然后才渲染表格ui

## slate-table-impl

- style-header-背景色
  - 设置在cell: prezly
  - 设置在tr/thead: gitbook

- model-header-options
  - 设置在table上，容易实现单行表头
  - 设置在tr上，容易实现多行表头
  - 设置在单元格上，容易实现表头行、表头列

## faq

- 光标如何退出表格
  - 方向下键
  - 如果上下2个相邻表格，就直接进下个表格

- 如何在上下2个表格中间添加新元素
  - 利用表格左上角的块级菜单
# editor-table-solutions
- [Tables - CKEditor 5 Documentation](https://ckeditor.com/docs/ckeditor5/latest/features/table.html)
# more
