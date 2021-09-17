---
title: lib-editor-prosemirror-dx
tags: [dx, issues, prosemirror]
created: '2021-09-17T19:14:10.041Z'
modified: '2021-09-17T19:29:55.813Z'
---

# lib-editor-prosemirror-dx

# upgrading

# issues-not-yet
- ## [prosemirror-dev-tools: Add methods to properly unmount the component](https://github.com/d4rkr00t/prosemirror-dev-tools/pull/107)
  - Warning: render(...): It looks like the React-rendered content of this container was removed without using React. This is not supported and will cause errors. Instead, call ReactDOM.unmountComponentAtNode to empty a container.
  - 需要增加卸载vdom的逻辑，修改源码
