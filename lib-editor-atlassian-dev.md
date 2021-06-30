---
title: lib-editor-atlassian-dev
tags: [atlaskit-editor, editor]
created: '2021-06-30T19:29:35.962Z'
modified: '2021-06-30T19:30:57.926Z'
---

# lib-editor-atlassian-dev

# guide

# [docs](https://atlaskit.atlassian.com/packages/editor/editor-core)
- polyfills
  - promise
  - fetch
  - element.closest

- simplest editor starter

```JS
import { Editor } from '@atlaskit/editor-core';

<Editor appearance="comment" />;
```

- Editor with mentions
- Collapsed Editor

- `EditorContext` allows you, in conjunction with `WithEditorActions`, to manipulate the editor from anywhere inside the `EditorContext`. 

## props

- appearance
  - comment
    - you have a field input but require a toolbar & save/cancel buttons
  - full-page
  - chromeless
    - essentially the comment editor but without the editor chrome, like toolbar & save/cancel buttons
  - mobile
    - should be used for the mobile web view. 
    - It is a full page editor version for mobile.
# pieces

# discuss

- ## 
