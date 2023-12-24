---
title: lib-editor-app-community-selection-cursor
tags: [community, cursor, editor, selection]
created: 2023-11-21T04:36:45.818Z
modified: 2023-11-21T04:37:09.686Z
---

# lib-editor-app-community-selection-cursor

# guide

# discuss-stars
- ## 

- ## 

- ## 
# discuss
- ## 

- ## 悬浮工具条挤在一起好烦人，关键是每个都有用还不能关掉，我觉得操作系统应该出一个专门的 API 让程序往统一的悬浮窗里加东西，而不是各做各的 ...
- https://twitter.com/kk_shinkai/status/1738781514064708070
- iOS就是统一的
  - 然而 SwiftUI 到现在还没有办法添加 EditMenu Action Button
- 还有一个选择就是有个 all in one 的 app，大家给它开发插件就可以了，有点像 popclip 那样，但也觉得差点意思。 网页里面最好还是 browser 给个 api 咯，像 chrome extension 那样
- 我感觉那个输入法条条可以关掉

- ## The current cursor position of a `<textarea>` is so slow to update on mobile devices (mobile iOS specifically), but work. 
- https://twitter.com/RogersKonnor/status/1726723216432042145
  - Anyone else encountered this? Thinking I'm gonna have to bite the bullet and manually set selection based on `touchstart` event
