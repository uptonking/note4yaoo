---
title: lib-xplat-electron-community
tags: [community, electron]
created: 2023-01-02T10:29:39.911Z
modified: 2023-01-02T10:30:19.459Z
---

# lib-xplat-electron-community

# guide

# discuss
- ## 

- ## 

- ## 

- ## [【CEP 扩展开发一】简介 - 知乎](https://zhuanlan.zhihu.com/p/506927682)
- Adobe 插件，大致可以分成以下几类：
  - ExtendScript 脚本
  - 面板插件：Flash 面板插件，CEP 面板插件，UXP 面板插件
  - 独立客户端
  - C++ 插件
- ExtendScript 是 ECMAScript3 的一种方言，和 JavaScript 基本上语法一样，不过集成了一些例如指令，模块化，反射系统，三引号字符串，操作符重载等语法特性。文件后缀名是 .jsx（不是 react 用的那个 JS 的 DSL），所以 ExtendScript 又被称为 jsx。由宿主（例如 PS, AE, PR 等设计软件自身都叫宿主）实现的 ExtendScript 引擎解释执行，不同宿主都能解释执行 jsx，但是底层实现以及注入的宿主特有的 API 不一样。
- ExtendScript 可以调用宿主的各种 API，例如在 AE 中可以访问图层信息，调用渲染队列输出媒体资源，也有原生能力例如读写文件，还可以使用内置的各种窗口和控件接口去创建图形界面。因此它完全可以作为一种插件形式去实现独立的功能。
- 其实 adobe 软件支持的脚本语言并不只有 ExtendScript，例如在 PS 其实是支持：Apple Script, VBScript 和 ExtendScript
- CEP(Common Extensibility Platform) 扩展的界面是使用 Chromium 渲染的，采用的是 CEF（Chromium Embedded Framework） 架构。
  - CEF 简单理解就是将浏览器嵌入到其它应用中让我们可以直接使用前端技术去开发界面，electron, nwjs，tauri 是 CEF 架构的代表框架了。
  - 这类框架除了是使用前端技术开发界面，runtime 往往都还搞成混合型的，例如开启了 node 集成的 electron 和 nwjs 的浏览器窗口的运行时都是 web runtime 和 nodejs runtime 的复合 runtime。
- 其实 CEP 的架构和从 HTML 页面启动的 nwjs 最像，每一个 CEP 扩展本质就是本地的一个文件夹，打开一个 CEP 扩展其实就是就是去渲染 manifest.xml 指定的一个 HTML 文件。

- ✨ UXP (Unified Extensibility Platform)是下一代的面板插件架构，未来 CEP 扩展的结局会和 Flash 插件一样被废弃，并被 UXP 架构取代。
- CEP 的劣势：
  - CEP 使用完整的 Chromium 渲染 web，非常的吃资源，开多个 CEP 插件的时候更甚
  - CEP 并不能直接访问宿主，需要写 jsx 代码访问宿主。实际开发时你要写两端代码，一份是 jsx，一份是浏览器环境代码，分别被两个不同的 js 引擎执行，互相调用很不方便
  - CEP 插件不能使用原生控件，你需要编写很多 CSS 样式才能与原生面板和对话框的样式风格匹配
  - jsx 的 ECMAScript 规范版本很低，你需要在浏览器的高版本 ECMAScript 和 jsx 的 ECMAScript3 来回切换
- UXP 的优势：
  - UXP 可以直接沟通宿主，不需要编写 jsx
  - UXP 官方有提供一个插件启动器和自定义的 Chrome Dev Tools 用于 debugger，比起 CEP 开发更简单
  - UXP 可以使用 Spectrum CSS 组件库来，这个组件库支持自动切换主题而且是跨平台的，能够让你开发的面板看起来和应用本身风格一致
- UXP 目前只支持 PS 平台，如果你是给 PS 以外的 adobe 软件开发面板插件，那你只能选 CEP，CEP 扩展支持的平台很多
