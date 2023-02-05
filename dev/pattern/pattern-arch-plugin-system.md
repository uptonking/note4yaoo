---
title: pattern-arch-plugin-system
tags: [architecture, pattern, plugin-system]
created: 2020-10-17T13:55:35.958Z
modified: 2020-12-20T15:46:29.566Z
---

# pattern-arch-plugin-system

# guide

- 很多成熟优秀的系统都是插件式架构
  - react hooks
# plugin-system-repos
- https://github.com/moonrailgun/mini-star
  - [介绍 | MiniStar](https://ministar.moonrailgun.com/zh-Hans/docs/tutorial/intro)
  - A micro-kernel framework which can pluginize your project. Progressive Migration!
  - mini-star 是一个为实现项目微内核(插件化)前端库，旨在帮助大家能更简单、无痛的构建(或改造成)一个生产可用微内核(插件化)架构系统。
  - [MiniStar 一个用于实现微内核(插件化)架构的前端框架 - V2EX](https://www.v2ex.com/t/781263)

- https://github.com/Webpack/tapable /js/202012
  - The tapable package expose many Hook classes, which can be used to create hooks for plugins.
  - Hook types: basic, waterfall, bail, loop, sync, async
  - interception, context, hookMap, multiHook
- https://github.com/gr2m/javascript-plugin-architecture-with-typescript-definitions /js/201910
  - The goal of this repository is to provide a template of a simple plugin Architecture 
    - which allows plugins to created and authored as separate npm modules and shared as official or 3rd party plugins.
  - This plugin architecture was extracted from @octokit/core
- https://github.com/c9/architect /js/2012
  - A simple yet powerful plugin system for large-scale node applications
  - Each plugin registers itself with Architect, so other plugins can use its functions. 
  - Plugins can be maintained as NPM packages so they can be dropped in to other Architect apps.
- https://github.com/brianreavis/microplugin.js /2013
  - Plugins can declare dependencies to other plugins and can be initialized with options (in a variety of formats). 
  - It's AMD-compatible and it works identically in Node.js and in a browser.

- https://github.com/jalaali/moment-jalaali
  - A Jalaali (Jalali, Persian, Khorshidi, Shamsi) calendar system plugin for moment.js.
- https://github.com/GeekyAnts/react-pluggable
  - https://react-pluggable.github.io/
  - 插件基于IPlugin接口，给出的例子基于class实现
  - With React Pluggable, we can think of our app as a set of features instead of a set of components
  - A plugin can be added or removed by a single line (which is perfect for A/B testing)
# discuss
- ## 

- ## [前端开发，如何优雅的实现这样一个插件机制？](https://www.zhihu.com/question/294560351)

# ref
- [The Architecture of Open Source Applications](http://aosabook.org/en/index.html)
  - 500 Lines or Less

- [如何设计一个JavaScript插件系统，编程思维比死磕API更重要](https://zhuanlan.zhihu.com/p/211072788)
