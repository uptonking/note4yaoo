---
title: lib-editor-slate-codebase
tags: [codebase, slate-editor]
created: 2022-05-15T18:46:02.235Z
modified: 2023-02-05T19:03:12.722Z
---

# lib-editor-slate-codebase

# guide

# Editable
- 默认是div
- 解构props剩下的参数放在 attributes 中

- 接受的实参中包含事件处理器时，若事件处理器中`return true`，则不会执行slate内置逻辑
  - 受影响的内置事件包括
    - onBeforeInput
    - onBlur
    - onClick
    - onCompositionStart
    - onCompositionEnd
    - onCompositionUpdate
    - onCopy
    - onCut
    - onPaste
    - onDragOver
    - onDragStart
    - onDragEnd
    - onDrop
    - onFocus
    - onKeyDown
  - 始终会执行的内置事件包括
    - onInput

- 
- 
- 
- 
- 
- 
