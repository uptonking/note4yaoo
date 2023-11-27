---
title: lib-editor-quill-codebase
tags: [codebase, quill]
created: 2023-02-09T18:24:22.295Z
modified: 2023-02-09T18:24:31.494Z
---

# lib-editor-quill-codebase

# guide

# codebase

# model-delta

# view

# update

- Quill 只用 mutation observer 监听文本改动。其他的 enter delete 等，都还是劫持 keydown，修改 model
