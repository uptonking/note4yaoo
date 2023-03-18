---
title: lib-editor-slate-features-dev
tags: [dev-log, features, slate-editor]
created: 2023-03-16T16:29:36.262Z
modified: 2023-03-16T16:29:47.610Z
---

# lib-editor-slate-features-dev

# guide

# noseditor

## dev-to

- 子级列表的拖拽按钮仅靠列表项开始的黑点

- 第一个一级标题通常字体会更大，一般不需要在标题折叠整篇文章

### drag

- 多级列表下的第一个p元素，无法拖拽到这个位置

- 拖拽时原布局不变，只显示预期位置的指示线
  - notion、飞书

## later

### 块级菜单

### 分栏布局

- 创建分栏
  - 手动添加具体数量分栏
  - 拖拽自动创建分栏

- 删除分栏
  - 拖拽改变位置后，变为整行块，还是维持分栏？
    - notion维持分栏； 原分栏位置变为空白分栏
    - 飞书变为整行块； 原分栏位置变为空白分栏

- 分栏后选区
  - 先向下，再向右

## maybe

# 顶部工具条 toolbar
- 工具条比编辑器宽，编辑器左边会有空白
  - lexical，左右28，上8

- 工具条与编辑器同宽
  - tinymce，左右16
# 悬浮工具条 toolbar

# general-elements

## list

- 若当前列表项为空，按回车应该转换为普通p标签

- 多级列表的缩进宽度
  - notion 24
  - 飞书 24
# more
