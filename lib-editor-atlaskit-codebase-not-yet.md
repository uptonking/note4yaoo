---
title: lib-editor-atlaskit-codebase-not-yet
tags: [atlaskit-editor, codebase]
created: '2021-07-17T13:59:02.057Z'
modified: '2021-07-17T13:59:24.514Z'
---

# lib-editor-atlaskit-codebase-not-yet

# issues-not-yet

- fix-chrome-88-selection

```JS
view.dom.style.display = 'inline-block';
// 两个赋值间为什么要查询一次dom
view.dom.offsetHeight;
view.dom.style.display = 'block';
```
