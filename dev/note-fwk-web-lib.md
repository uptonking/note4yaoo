---
title: note-fwk-web-lib
tags: [framework, web]
created: 2021-01-13T07:57:30.313Z
modified: 2021-01-13T07:57:54.308Z
---

# note-fwk-web-lib

# guide

# react系

## [如何看待由react router原班人马打造并获得三百万美元融资的ts全栈开发框架remix框架?](https://www.zhihu.com/question/502743886)

- 如果remix框架仅仅是解决了语言的问题是远远不够的，它需要提供类似springcloud的完整解决方案，否则很可能类似现在的BFF模式，不是很有价值。
  - 未来当然是好的，但是我们也应该看到，后端的技术栈并不仅仅是语言，它包含了许多的知识体系，比如SQL优化、微服务架构、RPC、限流、熔断降级、负载、读写分离、高并发等等。

- 看过router源码的都知道其实现没什么难度。。。用的还是react提供的api.
  - 这就像写了一个github很多人用的组件，比如通用switch按钮，tab之类的，说拿到融资然后要实现一个js框架。。。。你只会觉得unbelievable，至于期待什么的，我倒是挺好奇他们的技术水平能实现到什么程度
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
