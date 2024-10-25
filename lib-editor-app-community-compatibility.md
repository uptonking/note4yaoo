---
title: lib-editor-app-community-compatibility
tags: [community, compatibility, editor]
created: 2023-02-12T15:19:35.641Z
modified: 2023-02-12T15:19:54.332Z
---

# lib-editor-app-community-compatibility

# guide

# discuss-events
- ## 

- ## 

- ## [In web browsers, what's the difference between onblur and onfocusout? - Stack Overflow](https://stackoverflow.com/questions/7755052/in-web-browsers-whats-the-difference-between-onblur-and-onfocusout)
- `onBlur` event fires for an element if that element had the focus, but loses it.
  - `onFocusOut` event fires in this case, but also triggers if any child element loses focus.

- Acccording to the spec for the `focusout` event type: This event type is similar to blur, but is dispatched before focus is shifted, and does bubble.
  - Whereas `blur` events do bubble, and are dispatched later.
# discuss
- ## 

- ## 

- ## 

- ## 

- ## 调研一下 iOS 的选区菜单能不能取消掉或者可定制
- https://twitter.com/_Xheldon/status/1412688317015990274
- [How to disable the mobile Safari selection menu? - discuss. ProseMirror](https://discuss.prosemirror.net/t/how-to-disable-the-mobile-safari-selection-menu/2581)
  - I did more research on this and it appears to be part of iOS itself, not Safari like I originally stated. The same menu appears when you select text in other applications.

- [Tooltip inline menu fights with iOS selection menu](https://github.com/ProseMirror/prosemirror/issues/7)
- Since control over the tooltip menu is impossible for web pages, the **recommendation** here is to either not use the tooltip menu on iOS, or set its `position` option to "below" to prevent the two tooltips from overlapping.
