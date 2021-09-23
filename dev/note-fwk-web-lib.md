---
title: note-fwk-web-lib
tags: [framework, web]
created: '2021-01-13T07:57:30.313Z'
modified: '2021-01-13T07:57:54.308Z'
---

# note-fwk-web-lib

# guide

# stimulus

- stimulus /10kStar/MIT/202101/ts
  - https://github.com/hotwired/stimulus
  - https://stimulus.hotwire.dev/
  - A modest JavaScript framework for the HTML you already have
  - it's designed to augment your HTML with just enough behavior to make it shine.

- ## [前端框架Stimulus的使用体验如何？](https://www.zhihu.com/question/266673543/answers/updated)
- 它是为了配合HTML页面，为传统（大量HTML，SEO，重写代价极大）项目提供动态交互支持。
- Stimulus是完全依靠HTML5的MutationObserver和实体DOM，而非Vue/React经过编译的DOM。
  - 同时Stimulus中并不存在vdom，并不会进行UI渲染。
- 这是Ruby社区给多页面应用设计的框架。
  - 别再拿单页面框架跟 Stimulus 做对比了，适用的场景是不同滴。
