---
title: lib-editor-ckeditor5-docs
tags: [ckeditor, editor]
created: 2021-10-25T09:32:44.058Z
modified: 2021-10-25T09:33:13.353Z
---

# lib-editor-ckeditor5-docs

# guide

- ckeditor架构亮点
  - view层包括editing view和data view

- ckeditor架构不足
  - 使用多套vdom使得架构很复杂，model和view的vdom有相似有差异

- [classic editor vs classic build](https://ckeditor.com/docs/ckeditor5/latest/api/module_editor-classic_classiceditor-ClassicEditor.html)
  - 注意区分 @ckeditor/ckeditor5-editor-classic  @ckeditor/ckeditor5-build-classic
  - The classic editor can be used directly from source
  - Builds are ready-to-use editors with plugins bundled in. 
  - **When using the editor from source, you need to take care of loading all plugins by yourself** (through the `config.plugins` option). 
  - Using the editor from source gives much better flexibility and allows easier customization.
