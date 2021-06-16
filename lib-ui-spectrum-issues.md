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
- ## watching
- [Allow disabled menu items to be focused](https://github.com/adobe/react-spectrum/issues/1696)
- [why textfield onChange does not receive an event?](https://github.com/adobe/react-spectrum/discussions/1884)

- ## [Make onChange event handler accept standard event object as argument](https://github.com/adobe/react-spectrum/issues/1860)
- I think the problem is that there isn't always a DOM event for all change events. 
  - It might be true for input elements but for other components that's not the case. 
  - We'd rather be consistent and avoid leaking implementation details of our components if possible.
  - For example, a custom select dropdown isn't going to have native DOM change events available.

- ## [How to set text's color?](https://github.com/adobe/react-spectrum/issues/864)
- We haven't finished implementing the typography components in React Spectrum just yet. 
  - The current text components are mainly used as part of another component that provides the styling for it, e.g. menu items, illustrated message, dialog, etc. 
  - We will eventually have various predefined typography styles. Should be coming relatively soon.
- For now, the best I can suggest is to use either one of the existing components that styles `<Text>` for you, or use an element like `<span>` with custom CSS.
# issues
- ## ActionGroup now supports collapsing into a menu when space is limited. 
- https://twitter.com/devongovett/status/1404830456806141952
  - It can even automatically hide the button labels and display them in a tooltip. 
  - When selection is enabled, we hide all options at once, and display the selection when collapsed.
- Does the collapse behavior work ok with SSR?
  - It's done in a layout effect, which only runs client side. So it will render all items on the server, and then collapse on the client during hydration.
- From a11y perspective did you turn the last tab into a menu button?
  - Well, no tabs in this example. It’s a toolbar with a menu button. 
  - When selection is enabled it’s either a checkbox or radio group, and when collapsed only a menu button (we don’t mix them).
  - Our tabs also have a collapsing behavior, but it collapses them all at once and basically becomes a menu button. We don’t mix tabs and buttons together.
