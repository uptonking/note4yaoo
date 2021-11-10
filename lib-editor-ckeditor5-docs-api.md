---
title: lib-editor-ckeditor5-docs-api
tags: [api, ckeditor, docs]
created: '2021-10-29T16:17:17.807Z'
modified: '2021-10-29T16:17:32.723Z'
---

# lib-editor-ckeditor5-docs-api

# guide

- [x] 编辑器editor.getData()再editor.setData()时，mermaid的model会多出一个空的imageBlock的问题
  - 比较理想的方式，是getData时只输出mermaidCode，不输出image，但没有找到具体实现方法，因为dataDowncast无法完全控制getData的输出过程
  - 变通的方式，是getData时输出mermaid和imageBlock，setData时修改upcast过程，避免创建新的imageBlock

- 测试编辑器内容的保存
  - editor.setData(editor.getData())

- editor.getData()的实现原理
  - 会调用DataApiMixin.getData( options ) { return this.data.get( options ); }
  - core/editor中 this.data = new DataController( this.model, stylesProcessor ); 
  - DataController.constructor中，会创建 this.viewDocument

- mermaid dataDowncast的输出是正常的
  - mermaidView = writer.createContainerElement

- 检查editor.getData的过程和dataDowncast的关系
