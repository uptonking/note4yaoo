---
title: lib-editor-slate-features-table
tags: [features, slate-editor, table]
created: 2023-02-27T19:06:17.436Z
modified: 2023-02-27T19:07:31.111Z
---

# lib-editor-slate-features-table

# guide

# slate-table
- basics
  - 方向键能准确移动光标
  - 方向下键，光标退出表格
  - 复制粘贴单元格内容
  - undo/redo

- 按键、光标、选区
  - tab/shift+tab键移动选区到下/上一个单元格
  - ？ enter键在单元格内换行(~~还是新建一行~~)

- header-menu
  - readonly

- header
  - 可选表头
  - caption

- row
  - 在当前行上方/下方插入新行
  - 删除行
  - 拖拽调整行高度

- col
  - 在当前列左边或右边插入新列
  - 删除列
  - 拖拽调整列宽度

- cell
  - 单元格可选支持nested content，表中表
  - 合并、拆分单元格

- later
  - table themes
  - api & docs
  - 复制粘贴优化

- maybe
  - 完全自绘表格选区
  - 整个编辑器支持先渲染文本，此时表格渲染loading占位符，然后才渲染表格ui

## faq

- 光标如何退出表格
  - 方向下键

- 如何在上下2个表格中间添加新元素
  - 利用表格左上角的块级菜单
# editor-table-solutions
- [Tables - CKEditor 5 Documentation](https://ckeditor.com/docs/ckeditor5/latest/features/table.html)
# more
