---
title: lib-editor-quill-community-ime
tags: [community, ime, input-method, quill]
created: 2023-11-27T15:59:54.295Z
modified: 2023-11-27T16:00:15.296Z
---

# lib-editor-quill-community-ime

# guide

# discuss-stars
- ## 

- ## 

- ## 
# discuss
- ## 

- ## 

- ## 

- ## [IME/Composing breaks when receiving ops](https://github.com/quilljs/quill/issues/3143)
- When using an IME, like Chinese input — or even these days, an English swiping keyboard on mobile — Quill enters "batch" mode to avoid committing the change until compositionend. However, if we call updateContents before the end of composition, then Editor.applyDelta prematurely calls batchEnd, which flushes the intermediary IME input, which is undesirable.
