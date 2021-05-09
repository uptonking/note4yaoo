---
title: lib-ui-spectrum-issues
tags: [adobe-spectrum, issues, ui]
created: '2021-04-12T16:28:40.402Z'
modified: '2021-04-12T18:07:46.180Z'
---

# lib-ui-spectrum-issues

# guide

# todo

- CollectionBuilder应该提供预先计算(空闲计算)的能力
  - 目前全是基于generator函数延迟计算的数据，一般要等到点击父节点后才开始计算该节点下子节点的数据，然后计算成VDOM再渲染

# issues-not-yet

- ## [How to set text's color?](https://github.com/adobe/react-spectrum/issues/864)
- We haven't finished implementing the typography components in React Spectrum just yet. 
  - The current text components are mainly used as part of another component that provides the styling for it, e.g. menu items, illustrated message, dialog, etc. 
  - We will eventually have various predefined typography styles. Should be coming relatively soon.
- For now, the best I can suggest is to use either one of the existing components that styles `<Text>` for you, or use an element like `<span>` with custom CSS.

# issues

- ## 
