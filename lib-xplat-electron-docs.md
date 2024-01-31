---
title: lib-xplat-electron-docs
tags: [docs, electron]
created: 2024-01-31T19:33:53.245Z
modified: 2024-01-31T19:34:04.442Z
---

# lib-xplat-electron-docs

# guide

# faq

## 🆚️ electron vs cef

- The CEF is a project that turns Chromium into a library, and provides stable APIs based on Chromium's codebase. 
  - Very early versions of Atom editor and NW.js used CEF.
- To maintain a stable API, **CEF hides all the details of Chromium and wraps Chromium's APIs with its own interface**. 
- So when we needed to access underlying Chromium APIs, like integrating Node.js into web pages, the advantages of CEF became blockers.
- So in the end **both Electron and NW.js switched to using Chromium's APIs directly**.
- ref
  - https://www.electronjs.org/blog/electron-internals-building-chromium-as-a-library

### [CEF和Electron的区别是什么？ - 知乎](https://www.zhihu.com/question/510368054)

- Electron面向的开发者是纯前端开发者，会用JavaScript，HTML，CSS，但不会用C++。
- CEF面向的开发者是会用C++也会用JavaScript，HTML，CSS的开发者。

- V8只负责解析并执行JavaScript，它是没有访问操作系统的能力的，比如读写文件，访问网络（这里主要指通过Socket访问网络），访问进程信息等，这些能力V8没有，集成了Node.js后，开发者就拥有这些能力了，
  - 但光集成Node.js还不够，Electron自己还封装了一些操作系统的能力供JavaScript调用，比如访问剪切板，发送系统通知，访问托盘图标等，
  - 这些能力是V8和Node.js都没有的，但却是开发一个桌面应用所必备的。

- CEF则比较单纯，只对Chromium做了精简和封装，允许开发者通过C++代码控制Chromium核心，允许JavaScript和C++互操作，允许开发者在Chromium的多个进程间通信，
  - 像访问托盘图标、访问剪切板、Socket通信、读写文件这类事情，它都没做，要完成这些工作，开发者得自己写代码。
  - 这也无可厚非，因为C++开发者可以很容易的完成这些任务。
  - 但JavaScript开发者就很难完成这些任务，所以Electron为他们做了这些事情，而且做的很好。

## 🆚️ electron vs nw.js

- [Technical Differences Between Electron and NW.js | Electron](https://www.electronjs.org/docs/latest/development/electron-vs-nwjs)
  - Electron works more like the Node.js runtime
  - In NW.js, the Node integration in web pages requires patching Chromium to work, while in Electron we chose a different way to integrate the libuv loop with each platform's message loop to avoid hacking Chromium. 
  - By using the multi-context feature of Node, Electron doesn't introduce a new JavaScript context in web pages. NW.js has optionally supported multi-context since 0.13.
  - Electron has a bigger community, more production apps 

- 两个原理应该不一样，electron应一个窗口会对应一个渲染进程，而nw.js本身是可选一个窗口一个渲染进程，且默认应该不是，你可以比较下当nw.js开启一个窗口一个渲染进程后两者的速度。

### [NW.js 和 Electron 各有什么优缺点 - 知乎](https://www.zhihu.com/question/38854224)

- 比较NW.js和Electron之前，先要明白虽然是用javascript+html写的app，但是都会跑两部分的js runtime，分别是node-runtime和chromium-runtime

- 功能上看，2者差不多，主要的区别是入口方式。
- Electron是基于node的，入口是类似node module的index.js，这是因为Electron是基于node的event-loop将chromium的功能和event全部整合app，Electron的开发跟其他的node应用没区别。
- NW.js像一个跑在node-platform上的浏览器，所以他的入口是index.html，NW.js将自己的功能都整合进了chromium-runtime，因此更接近一个前端的应用开发方式。NW.js也可以用到node的api，这是通过binding到chromium-runtime来调用的。
- 👉🏻 NW把2套js-runtime环境整合到了一起，Electron则是保持2套js-runtime彼此独立。
  - NW的app中的js代码可以使用所有的API（这不见得是好事）。electron的app中的js是可以分前后端的。

- NW提供了二进制JS加密方案，electron没有并且以后也不打算搞
  - 常规画界面那种低价值代码，minified就差不多够用了。核心代码（如果有）可以转webassembly，既解决代码保密问题又解决性能问题

- nw和electron 出自同一个人之手，而且他也玩知乎。 electron 比 nw 后出世，你说该用哪个？

### [Electron 和 NW.js 在技术上的差异 - 知乎](https://zhuanlan.zhihu.com/p/34250289)

- 程序入口。
  - 在NW.js中，应用的主入口是网页或者js脚本；
  - 在Electron中，入口是一个js脚本
- 构建系统。
  - Electron通过libchromiumcontent来访问Chromium的Content API，避免了构建整个Chromium带来的复杂度
- 与Node集成。
  - 在NW.js，网页中的Node集成需要通过给Chromium打补丁来实现，Electron通过各个平台的消息循环与libuv的循环集成，避免了直接在Chromium上做改动
- 多上下文语境。
  - NW.js包括Node上下文和web上下文，自从0.13以来NW.js选择性支持多上下文。通过使用Node的multi-context特性，Electron不需要在网页中引入新的js上下文

### [为什么用 electron 开发的桌面应用那么多？ - 知乎](https://www.zhihu.com/question/509656170/answers/updated)

- 飞书和钉钉肯定不是，他俩用的CEF。
  - Electron和CEF底下其实都是chromium内核。

- 因为软件开发太卷了，及其追求速度，所以怎么快怎么来呗，至于性能啥的，后面再说，又不是不能用

## electron中可以使用web worker吗？

- 可以用，但不推荐
- It is possible to use Node.js features in Electron's Web Workers, to do so the nodeIntegrationInWorker option should be set to true in webPreferences
- All built-in modules of Node.js are supported in Web Workers
- However none of Electron's built-in modules can be used in a multi-threaded environment.
- Any native Node.js module can be loaded directly in Web Workers, but it is strongly recommended not to do so. 
  - **Most existing native modules have been written assuming single-threaded environment, using them in Web Workers will lead to crashes and memory corruptions**.
  - Note that even if a native Node.js module is thread-safe it's still not safe to load it in a Web Worker because the `process.dlopen` function is not thread safe.
  - The only way to load a native module safely for now, is to make sure the app loads no native modules after the Web Workers get started.

- ref
  - https://www.electronjs.org/docs/tutorial/multithreading
# docs

# more
