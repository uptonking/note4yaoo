---
title: lib-editor-atlaskit-codebase-not-yet
tags: [atlaskit-editor, codebase]
created: '2021-07-17T13:59:02.057Z'
modified: '2021-07-17T13:59:24.514Z'
---

# lib-editor-atlaskit-codebase-not-yet

# reading
- primary toolbar
- typeAhead
- codeblock
# codebase-limitations
- Warning: Cannot update a component (`WidthEmitter`) while rendering a different component (`Context. Consumer`).
  - 在consumer的function child中调用了setState，也就是render方法调用了setState，会导致无限循环
  - 改用useContext + useEffect

- webpack 5 处理导入json时，按默认导入import defaultJsonVal from './a.josn; `，而不是命名导入 named import
  - 所以对于依赖的第三方包都会出现编译错误
  - 变通方法是重写第三方依赖包
# issues-not-yet
- fix-chrome-88-selection

```JS
view.dom.style.display = 'inline-block';
// 两个赋值间为什么要查询一次dom
view.dom.offsetHeight;
view.dom.style.display = 'block';
```
