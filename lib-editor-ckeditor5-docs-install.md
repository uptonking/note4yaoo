---
title: lib-editor-ckeditor5-docs-install
tags: [ckeditor, docs]
created: '2021-10-29T16:07:47.299Z'
modified: '2021-10-29T16:09:06.481Z'
---

# lib-editor-ckeditor5-docs-install

# guide

- 查看所有plugins
  - ClassicEditor.builtinPlugins

# predefined builds overview
- Predefined CKEditor 5 builds are a set of ready-to-use rich text editors.
  - **Every “build” provides a single type of editor with a set of features and a default configuration**. 
  - They provide convenient solutions that can be installed with no effort and that satisfy the most common editing use cases.

- Available builds
  - Classic editor
  - Inline editor
  - Balloon editor
  - Balloon block editor
  - Document editor

- In CKEditor 5 the concept of the “boxed” editor was reinvented:
  - The toolbar is now always visible when the user scrolls the page down.
  - By default the editor now grows automatically with the content.

- [DecoupledEditor](https://ckeditor.com/docs/ckeditor5/latest/api/module_editor-decoupled_decouplededitor-DecoupledEditor.html)
- **给出的示例程序是 Document editor**
- The decoupled editor provides an inline editable and a toolbar. 
  - However, unlike other editors, it does not render these components anywhere in the DOM unless configured.
  - This type of an editor is dedicated to integrations which require a customized UI with an open structure, allowing developers to specify the exact location of the interface.

- Inline editor comes with a floating toolbar that becomes visible when the editor is focused (e.g. by clicking it). 
  - Unlike classic editor, inline editor does not render instead of the given element, it simply makes it editable. 

- Balloon editor is very similar to inline editor. 
  - The difference between them is that the toolbar appears in a balloon next to the selection (when the selection is not empty)

- Balloon block editor is essentially the balloon editor with an extra block toolbar which can be accessed using the button attached to the editable content area and following the selection in the document. 
  - The toolbar gives an access to additional, block–level editing features.

- Document editor is focused on rich text editing experience similar to the native word processors. 
  - It works best for creating documents which are usually later printed or exported to PDF files.

- why build customization
  - override the default configuration of features
  - change the default toolbar configuration
  - remove features (plugins)

- CKEditor 5 Framework should be used, instead of builds, in the following cases:
  - When you want to create your own text editor and have full control over its every aspect, from UI to features.
  - When the solution proposed by the builds does not fit your specific use case.
