---
title: lib-editor-quill-dev
tags: [quill, text-editor]
created: 2023-02-09T18:17:22.759Z
modified: 2023-02-09T18:23:23.288Z
---

# lib-editor-quill-dev

# guide

- pros
  - 提出delta结构表示编辑器的内容和changes, popular delta format

- cons
  - 扁平的结构查询一个节点的子节点不太方便，但也可通过attributes自定义属性来实现
  - inactive maintainance
  - lack of classic examples and ecosystem: search搜索示例、word导入导出

- features
  - stable rich text editor

- who is using #quilljs
  - 石墨文档
  - slab, Reedsy
  - ERPNext
  - Grammarly Editor
  - [vaadin rich-text-editor is built with Quill](https://vaadin.com/docs/latest/components/rich-text-editor)

- tips
  - 视图层的实现可参考: wangEditor/typewriter/autocomplete, 库和应用层有不同
# not-yet
- y-quill中`quill.setContents(type.toDelta(), this);`第2个参数不能设为ts类型中的`silent`
# dev

# more
