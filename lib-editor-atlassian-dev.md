---
title: lib-editor-atlassian-dev
tags: [atlaskit-editor, editor]
created: '2021-06-30T19:29:35.962Z'
modified: '2021-06-30T19:30:57.926Z'
---

# lib-editor-atlassian-dev

# guide

- watching
  - nodeViews: code-block, width, card, emoji, hyperlink, placeholder-text, text-color
    - 所有组件的实现都很复杂！！！
    - 大量依赖atlassian design system中的react组件
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

## [Atlassian Document Format(ADF)](https://developer.atlassian.com/cloud/jira/platform/apis/document/structure/)

- Atlassian Document Format (ADF) represents rich text stored in Atlassian products. 
  - For example, in Jira Cloud platform, the text in issue comments and in `textarea` custom fields is stored as ADF.
- An Atlassian Document Format document is a JSON object. A JSON schema is available to validate documents.
- An ADF document is composed of a hierarchy of nodes. 
- There are two categories of nodes: block and inline. 
- Block nodes define the structural elements of the document such as headings, paragraphs, lists, and alike. 
- Inline nodes contain the document content such as text and images. 
- Some of these nodes can take marks that define text formatting or embellishment such as centered, bold, italics, and alike.
- A document is ordered, that is, there's a single sequential path through it: traversing a document in sequence and concatenating the nodes yields content in the correct order.

## [confluence macros](https://confluence.atlassian.com/doc/macros-139387.html)

- You can use macros to:
  - change the format and layout of your page
  - display media like video, audio, and social media content
  - collate and organise Confluence pages, blogs, and files
  - perform actions from a page, such as creating a page from a template. 
# pieces

# examples

- https://github.com/b-yond-infinite-network/md-to-adf
  - Markdown to Atlassian Document Format translation/traduction
