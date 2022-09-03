---
title: lib-editor-prosemirror-dx-log
tags: [dx, issues, prosemirror]
created: 2021-09-17T19:14:10.041Z
modified: 2021-09-19T15:14:41.307Z
---

# lib-editor-prosemirror-dx-log

# guide

- faq
  - 编辑器多实例时，如何从插件中获取状态
    - 插件对象可以复用，但取插件对象的状态依赖唯一的editorState对象
# upgrading

# issues-not-yet
- ## [prosemirror-dev-tools: Add methods to properly unmount the component](https://github.com/d4rkr00t/prosemirror-dev-tools/pull/107)
  - Warning: render(...): It looks like the React-rendered content of this container was removed without using React. This is not supported and will cause errors. Instead, call ReactDOM.unmountComponentAtNode to empty a container.
  - 需要增加卸载vdom的逻辑，修改源码
