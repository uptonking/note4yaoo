---
title: lib-editor-ckeditor5-docs-api
tags: [api, ckeditor, docs]
created: '2021-10-29T16:17:17.807Z'
modified: '2021-10-29T16:17:32.723Z'
---

# lib-editor-ckeditor5-docs-api

# guide

# editor

# widget

## WidgetResize

- Use the `attachTo` method to create a resizer for the specified widget.

- editor
  - The editor instance.
  - Note that most editors implement the `EditorWithUI` interface in addition to the base `Editor` interface. 
  - However, editors with an external UI (i.e. Bootstrap-based) or a headless editor may not implement the `EditorWithUI` interface.
  - Because of above, to make plugins more universal, it is recommended to split features into:
    - The "editing" part that only uses the `Editor` interface.
    - The "UI" part that uses both the `Editor` interface and the `EditorWithUI` interface.
