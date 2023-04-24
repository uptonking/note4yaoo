---
title: lib-editor-slate-features-dev
tags: [dev-log, features, slate-editor]
created: 2023-03-16T16:29:36.262Z
modified: 2023-03-16T16:29:47.610Z
---

# lib-editor-slate-features-dev

# guide
- 编辑器较通用的功能
  - editor-features-playground: migrate lexical for slate, with devtools
  - 复制、粘贴
  - 导入、导出
  - 兼容word、excel
  - 支持多实例

- 编辑器难点
  - 分页
  - 页眉、页脚
  - 虚拟渲染

- editor-ecosystem
  - data-grid
  - chart
  - calendar
  - image-editor

- products-inspration
  - [GitHub Blocks](https://blocks.githubnext.com/)
# noseditor

# to-refactor
- serialize/deserialize的定制逻辑暴露在各个plugin，而不是统一的useSerDes
# dev-to
- 整理每个plugin的export

- 子级列表的拖拽按钮仅靠列表项开始的黑点

- 第一个一级标题通常字体会更大，一般不需要在标题折叠整篇文章

- isCollapsibleElement逻辑优点混乱
  - 作为DraggableEditor的static方法
  - 在editor.isCollapsibleElement被增强

## drag

- 多级列表下的第一个p元素，无法拖拽到这个位置

- 拖拽时原布局不变，只显示预期位置的指示线
  - notion、飞书

### 拖拽指示线的实现思路

- notion和飞书都不能拖拽到页面标题之上
  - notion的拖拽指示线与block结构绑定，绝对定位渲染在鼠标最近block的下面或上面，默认是下面 bootom: -4px
    - antd-tree采用的也是这种思路
  - 飞书的拖拽指示线不与block结构绑定，全局绝对定位
# later
- emoji

- 中文优化

### 块级菜单

- 菜单position不要用fixed，因为要随文档滚动

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

### 多编辑器实例

- 每个editor带有自己的
  - 工具条、悬浮菜单
  - 右键菜单
# maybe
- devtools
  - 可参考 ckeditor、prosemirror、tanstack-query/table
# 顶部工具条 toolbar
- 工具条比编辑器宽，编辑器左边会有空白
  - lexical，左右28，上8

- 工具条与编辑器同宽
  - tinymce，左右16

- 工具条ui设计分组
  - undo/redo, paint-format
  - block-type
  - font-size, formats, font-color
  - lists, aligns
  - image, table, link, blockquote, code...
# 悬浮工具条 toolbar

# editor-elements

## formats

- 🖐🏻 (wont-fix) 选中文本添加格式如下划线后，接着按空格按字母也会出现下划线
  - 主流编辑器都存在这个问题，如notion、飞书、google-docs、ckeditor、tiptap
  - 解决方案是再次选中带格式的文本，然后取消格式

## list

- 🤔 重构
  - 不使用单一type加listType2种判断列表类型的方式，而用3个type值，能简化isActive的逻辑

- dev-to
  - 变可选, list操作要与所有子元素一起
  - 变可选，toggle标题/list
  - 父级checkbox支持显示部分选中的intermediate中间态
  - checkbox前的拖拽图标位置要往上一点

- 若当前列表项为空，按回车应该转换为普通p标签

- bullet list
  - 自定义符号为emoji

- number list
  - 支持小数，如2.1，2.2

- 多级列表的缩进宽度
  - notion 24
  - 飞书 24
# image

# mention

# variables
- refs
  - [TURO, a calculator notepad](https://www.turo.io/)
# more
- 搜索时能够搜索emoji
