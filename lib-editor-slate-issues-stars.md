---
title: lib-editor-slate-issues-stars
tags: [issues, slate]
created: '2022-05-15T18:48:42.427Z'
modified: '2022-05-15T18:48:53.816Z'
---

# lib-editor-slate-issues-stars

# guide

# faq

## [Why is content pasted as plain text?](https://docs.slatejs.org/general/faq)

- One of Slate's core principles is that, unlike most other editors, it does not prescribe a specific "schema" to the content you are editing.
  - For the most part, this leads to increased flexibility without many downsides, but there are certain cases where you have to do a bit more work. Pasting is one of those cases.
  - Since Slate knows nothing about your domain, it can't know how to parse pasted HTML content (or other content). So, by default whenever a user pastes content into a Slate editor, it will parse it as plain text. 
  - If you want it to be smarter about pasted content, you need to override the insert_data command and deserialize the `DataTransfer` object's `text/html` data as you wish.
