---
title: dev-log-faq-web-mobile
tags: [faq, mobile, web]
created: 2021-08-25T12:30:18.405Z
modified: 2021-08-25T12:34:00.049Z
---

# dev-log-faq-web-mobile

# not-yet

# 移动端到底有没有contextmenu
- [HTMLElement.contextMenu](https://developer.mozilla.org/en-US/docs/Web/API/HTMLElement/contextMenu) property refers to the context menu assigned to an element using the contextmenu attribute. 
  - The menu itself is created using the `<menu>` element.
  - This feature is no longer recommended. 
  - 所有的浏览器都不支持了

- [oncontextmenu](https://developer.mozilla.org/en-US/docs/Web/API/Element/contextmenu_event) 事件中执行 `e.preventDefault()` 后，桌面版无法打开右键菜单，但移动端仍然可以显示copy工具条
  - contextmenu event事件所有浏览器都支持，除了safari ios

- [onContextMenu event does not get fired on iOS 13.1](https://github.com/facebook/react/issues/17596)
  - Seens to not be a bug, instead, iOS seems to not fire 'contextmenu' events. 
  - It fires 'touchstart', 'touchend', 'touchmove' events instead.
