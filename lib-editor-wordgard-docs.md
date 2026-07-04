---
title: lib-editor-wordgard-docs
tags: [docs, wordgard]
created: 2026-07-03T19:57:27.190Z
modified: 2026-07-03T19:57:38.654Z
---

# lib-editor-wordgard-docs

# guide

# overview

# 🆚 wordgard vs prosemirror
- One of the biggest mistake blunders in ProseMirror is that the editor view does not get access to the transaction objects when updating, just the state. Wordgard does not repeat this mistake, and makes updates take transactions, not just a new state.
  - This means that things like the DOM update logic and UI plugins can precisely observe what happened, and handle changes in a efficient and more effective way. The weird unexpected DOM redraws that are still a thing in ProseMirror should not occur. Only the precise DOM structure affected by the new transactions will be updated.

- 
- 
- 
- 
- 
- 
- 
- 
- 

# docs

# more
