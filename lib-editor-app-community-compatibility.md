---
title: lib-editor-app-community-compatibility
tags: [community, compatibility, editor]
created: 2023-02-12T15:19:35.641Z
modified: 2023-02-12T15:19:54.332Z
---

# lib-editor-app-community-compatibility

# guide

# discuss
- ## 

- ## 调研一下 iOS 的选区菜单能不能取消掉或者可定制
- https://twitter.com/_Xheldon/status/1412688317015990274
- [How to disable the mobile Safari selection menu? - discuss. ProseMirror](https://discuss.prosemirror.net/t/how-to-disable-the-mobile-safari-selection-menu/2581)
  - I did more research on this and it appears to be part of iOS itself, not Safari like I originally stated. The same menu appears when you select text in other applications.

- [Tooltip inline menu fights with iOS selection menu](https://github.com/ProseMirror/prosemirror/issues/7)
- Since control over the tooltip menu is impossible for web pages, the **recommendation** here is to either not use the tooltip menu on iOS, or set its `position` option to "below" to prevent the two tooltips from overlapping.
