---
title: lib-editor-rich-markdown-docs
tags: [docs, rich-markdown-editor]
created: 2021-06-02T10:34:01.602Z
modified: 2021-06-02T10:34:16.329Z
---

# lib-editor-rich-markdown-docs

# docs

## overview

- rich-markdown-editor /2.7kStar/BSD/202112/ts/archived
  - https://github.com/outline/rich-markdown-editor
  - https://www.getoutline.com/
  - 依赖react、styled-components、prosemirror-markdown、markdown-it、prism-refractor、fuzzy-search、react-medium-image-zoom
  - v11.0.0_202009: styled-components is now a peer dependency
  - [v10.0.0_202005: a complete rewrite of the editor from slate to prosemirror](https://github.com/outline/rich-markdown-editor/releases/tag/v10.0.0)
  - A React and Prosemirror based editor that powers Outline
  - The editor is WYSIWYG and includes formatting tools whilst retaining the ability to write markdown shortcuts inline and output plain Markdown.
  - > This project is not attempting to be an all-purpose Markdown editor but for Outline's needs
# api

```JS
import Editor from "rich-markdown-editor";

<Editor
  defaultValue="Hello world!"
/>
```

## props

- `defaultValue`
  - A markdown string that represents the initial value of the editor. 
  - Use this to prop to restore previously saved content for the user to continue editing.
- `value`
  - A markdown string that represents the value of the editor. 
  - Use this prop to change the value of the editor once mounted, this will **re-render the entire editor** and as such is only suitable when also in `readOnly` mode. 
  - Do not pipe the value of `onChange` back into `value`, the editor keeps it's own internal state and this will result in unexpected side effects.
- `extensions`
  - Allows additional Prosemirror plugins to be passed to the underlying Prosemirror instance.

## callbacks

- `onChange(() => value): void`
  - This callback is triggered when the contents of the editor changes, usually due to user input such as a keystroke or using formatting options. 
  - You may use this to locally persist the editors state.
  - It **returns a function** which when called returns the current text value of the document. 
  - This optimization is made to avoid serializing the state of the document to text on every change event, allowing the host app to choose when it needs the serialized value.
