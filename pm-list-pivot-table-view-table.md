---
title: pm-list-pivot-table-view-table
tags: [pivot-table, pm, table]
created: 2022-12-16T01:52:01.861Z
modified: 2022-12-16T01:52:33.729Z
---

# pm-list-pivot-table-view-table

# guide

- 多维表格的使用场景
  - 充分考虑github实现的业务，如何将任务管理project、issues、discussions关联

- roadmap
  - in-memory > virtual-render > on-demand
# features
- facets/multi-tables

- table-in-table
  - [Bootstrap Table Examples - Sub Table](https://examples.bootstrap-table.com/#welcomes/sub-table.html)


# table-in-editor
- [CKEditor 5 table](https://ckeditor.com/docs/ckeditor5/latest/features/table.html)
  - 行列操作在悬浮工具条的二级菜单

- [Atlaskit editor with (huge) table](https://atlaskit.atlassian.com/examples/editor/editor-core/kitchen-sink)
  - 每个单元格右上角提供了行列操作菜单
  - 光标在表格内时会显示表格悬浮工具条

- [tiptap table](https://tiptap.dev/examples/tables)
  - 支持合并单元格
  - 支持拖拽修改列宽度
  - 提供了很多commands
  - 暂未提供悬浮工具条

- [plate table](https://plate.udecode.io/docs/plugins/table)
  - 光标在表格内时会显示表格悬浮工具条，如删除

- [lexical-editor](https://playground.lexical.dev/)
  - 光标在表格内时会显示表格悬浮工具条
  - 提供了2版table
  - 新版table
    - 默认支持sort, filter开发中
    - 点击单元格时默认是先选中单元格，而不是直接编辑单元格

- [tinymce table](https://www.tiny.cloud/docs/tinymce/6/full-featured-premium-demo/)
  - 光标在表格内时会显示表格悬浮工具条，如行列操作
  - 支持拖拽修改列宽度

## table-products

- 表格单元格的选区
  - 飞书通过浅蓝背景色
  - notion通过蓝色边框

- 行高可以通过列宽调整
  - 飞书编辑器表格
  - notion

- 单元格 悬浮工具条
  - 飞书将工具按钮显示在单元格左边那格
  - notion将工具按钮显示在行首和列首

- 单元格 合并拆分
  - 飞书支持合并cells，
    - 鼠标从左上到右下可触发选中合并后的单元格，然后可以在单元格悬浮工具条拆分单元格
    - 拆分后的单元格内容不能还原，内容都在第一个单元格
  - notion不支持合并单元格

- 单元格enter键
  - notion焦点移到下一行
  - 飞书、ckeditor、tiptap都是单元格内新加一行
# draft

# examples-

# maybe
- copy column data
# more
