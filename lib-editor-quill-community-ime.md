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
# discuss-not-yet
- ## 

- ## 

- ## [IME / Composing breaks when receiving ops _202008](https://github.com/quilljs/quill/issues/3143)
- When using an IME, like Chinese input — or even these days, an English swiping keyboard on mobile — Quill enters "batch" mode to avoid committing the change until `compositionend` . However, if we call `updateContents` before the end of composition, then `Editor.applyDelta` prematurely calls `batchEnd` , which flushes the intermediary IME input, which is undesirable.

- How did you solve it?
  - We no-op the Composition module with a no-op module to disable the upstream behavior
  - We then have do super heavy overriding in the Selection module, which we can only do because we moved it to a module in our fork
# discuss
- ## 

- ## 

- ## 

- ## [IME/Composing breaks when receiving ops](https://github.com/quilljs/quill/issues/3143)
- When using an IME, like Chinese input — or even these days, an English swiping keyboard on mobile — Quill enters "batch" mode to avoid committing the change until compositionend. However, if we call updateContents before the end of composition, then Editor.applyDelta prematurely calls batchEnd, which flushes the intermediary IME input, which is undesirable.
