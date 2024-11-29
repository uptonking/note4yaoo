---
title: lib-utils-shell-xtermjs
tags: [shell, terminal, utils, xtermjs]
created: 2024-11-29T06:37:16.572Z
modified: 2024-11-29T06:37:44.110Z
---

# lib-utils-shell-xtermjs

# guide

# not-yet

- 处于 `display: grid; place-content: center;` 包围的xterm容器的滚动条很难被鼠标点击选中，被其他元素遮挡了
  - 甚至鼠标hover在滚动条thumb上时滚动条会消失，而不是变粗且出现track
# dev-xp



- dom结构 🏠
- .xterm.terminal  相对定位，未设置宽高
  - .xterm-viewport 绝对定位，四方trbl为0px, overflow--scroll
    - .xterm-scroll-area 隐藏的空div，visibility--hidden
  - .xterm-screen 
    - textarea.xterm-helper-textarea 用于用户输入
    - canvas中渲染需要显示的内容
# dev-log
- [How to set background color on terminal · xtermjs/xterm.js](https://github.com/xtermjs/xterm.js/issues/1719)
  - term.setOption('theme', { background: '#fdf6e3' }); 
- [Release 5.0.0 · xtermjs/xterm.js](https://github.com/xtermjs/xterm.js/releases/tag/5.0.0)
  - The deprecated getOption and setOption APIs have been removed in favor of options assignment
  - term.options.scrollback = 1000; 
  - term.options.theme = { background: '#ccc' } 注意这里更新是replace而不是merge

- [Migrate to @xterm org on npm · xtermjs/xterm.js _](https://github.com/xtermjs/xterm.js/issues/4859)
  - Publish 5.4 to new scope
# docs

# more
