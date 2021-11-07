---
title: lib-editor-ckeditor5-docs-faq
tags: [ckeditor, docs, faq]
created: '2021-10-29T16:09:39.273Z'
modified: '2021-10-29T16:09:54.083Z'
---

# lib-editor-ckeditor5-docs-faq

# faq-repeat

## data view vs editing view

- 都由model通过converter计算得到

- 使用场景不同
  - data侧重于粘贴、读写数据
  - editing侧重于编辑交互

- editor.data没有提供document属性，
  - editor.editing.view.document提供了虚拟dom的属性和操作方法

## [Update CkEditor config on the basis of React state](https://stackoverflow.com/questions/59907888)

- 如何动态修改配置的问题
  - 思路是将可配置的部分做成state，初始化时就设置state，之后更新state即可，
  - 可考虑添加新的配置项到配置对象，而不是重新创建配置或插件对象

- getEditorConfig which would give me the changed config 
- Next a helper function which creates a new editor instance and adds it to the DOM.
- In one of the issues, it is suggested to destroy the old editor and create a new one when you want to update the config.
- destroy old editor instance and use the addEditor function to create a new one. 
  - The getEditorConfig should give you the updated config you wish to apply for the new editor.

- [Changing configuration options of a CKEditor instance](https://stackoverflow.com/questions/7636277)
  - Usually the configuration options will work only upon creation. 
  - You might be able to perform some tricks and so get some of the options to work at a later time, but that's usually more difficult.

- How to change CKEditor 5 plugin configuration programmically
  - simply destroy existing editor instance and create new one with updated configuration
# faq

## [Why can I insert a custom element into ckeditor without modifying the schema](https://stackoverflow.com/questions/52156467)

- The reason for that is that it's a pretty low-level tool which implements ways to perform atomic operations on the model (OK, I'm lying here, because there's an even lower level underneath, represented by operations themselves, but that's a protected API). Anyway, the writer is pretty low-level.
  - when you implement a command or any other feature you may need to perform multiple operations to do all the necessary changes. The state in the meantime (between these atomic operations) may be incorrect. The writer must allow that.
  - we could solve by checking the schema at the end of a `change()` block 

## raw elements(能被选中) vs ui elements(不可选中)

- [raw elements](https://ckeditor.com/docs/ckeditor5/latest/api/module_engine_view_rawelement-RawElement.html)
  - Raw elements work as data containers but their children are not managed or even recognized by the editor.
  - 方便集成。Raw elements are a perfect tool for integration with external frameworks and data sources.
  - they are considered by the editor selection and they can work as widgets.
  - You should not use raw elements to render the UI in the editor content
  - 注意editingDowncast中，createRawElement('div', options)创建div作为react组件容器

- [ui elements](https://ckeditor.com/docs/ckeditor5/latest/api/module_engine_view_uielement-UIElement.html)
  - It should be used to represent editing UI which needs to be injected into the editing view
  - The editor will ignore your UI element
    - the selection cannot be placed in it, 
    - it is skipped (invisible) when the user modifies the selection by using arrow keys 
    - and the editor does not listen to any mutations which happen inside your UI elements.
  - The limitation is that you cannot convert a model element to a UI element. 
    - UI elements need to be created for markers or as additional elements inside normal container elements.
