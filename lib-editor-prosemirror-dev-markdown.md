---
title: lib-editor-prosemirror-dev-markdown
tags: [editor, markdown, prosemirror]
created: '2021-06-16T07:09:35.180Z'
modified: '2021-06-16T07:09:49.289Z'
---

# lib-editor-prosemirror-dev-markdown

# guide
- MarkdownParser
  - 基于markdown-it
  - uses markdown-it to tokenize a file, and then runs the custom rules it is given over the tokens to create a ProseMirror document tree.

- MarkdownSerializer
  - serializing a ProseMirror document as Markdown/CommonMark text.

- MarkdownSerializerState
  - This is an object used to track state and expose methods related to markdown serialization. 

- This module implements 
  - a ProseMirror schema that corresponds to the document schema used by CommonMark, 
  - and a parser and serializer to convert between ProseMirror documents in that schema and CommonMark/Markdown text.
# pieces
