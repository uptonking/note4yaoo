---
title: lib-editor-atlaskit-codebase-not-yet
tags: [atlaskit-editor, codebase]
created: '2021-07-17T13:59:02.057Z'
modified: '2021-07-17T13:59:24.514Z'
---

# lib-editor-atlaskit-codebase-not-yet


# codebase-refactor

## high

- 很多provider的value使用的是对象字面量
  - 如 ContextPanelWidthProvider

## medium

## low

- useEffect/useMemo这类hooks的deps

- 不同组件的props有很多重复但大多都是单独重新定义的，如Toolbar/ToolbarInner
  - 更好的方式是使用 Pick + Omit
# codebase-limitations
- Warning: Cannot update a component (`WidthEmitter`) while rendering a different component (`Context. Consumer`).
  - 在consumer的function child中调用了setState，也就是render方法调用了setState，会导致无限循环
  - 改用useContext + useEffect

- webpack 5处理导入json时，按默认导入`import defaultJsonVal from './a.json; `，而不是命名导入
  - 所以对于依赖的使用过命名导入的第三方包会出现编译错误
  - 变通方法是重写第三方依赖包
# issues-not-yet
- fix-chrome-88-selection

```JS
view.dom.style.display = 'inline-block';
// 两个赋值间为什么要查询一次dom
view.dom.offsetHeight;
view.dom.style.display = 'block';
```
