---
title: note-web-browser-engine
tags: [browser, web, webkit]
created: '2020-06-27T08:19:22.900Z'
modified: '2020-07-14T12:01:16.533Z'
---

# note-web-browser-engine

## pieces

- 苹果曾经使用Gecko，嫌弃Gecko曾经有段时间太臃肿，就把KDE的HTML引擎KHTML、JavaScript引擎KJS加工过来，发布了WebCore+JavaScriptCore的Webkit并开源。
- 后来Google加入使用WebCore引擎，再后来Chromium又分支出去Blink引擎，JavaScript引擎是Google开源的V8。

## summary

- 浏览器的主要结构
  - 用户界面 
    - 包括地址栏、前进/后退按钮、书签菜单等。
    - 除了浏览器主窗口显示的您请求的页面外，其他显示的各个部分都属于用户界面。
  - 浏览器引擎 
    - 在用户界面和呈现引擎之间传送指令。
  - 呈现引擎 
    - 负责显示请求的内容。
    - 如果请求的内容是HTML，它就负责解析HTML和CSS内容，并将解析后的内容显示在屏幕上。
    - 与其他浏览器不同的是：chrome浏览器中每个tab页对应一个呈现引擎实例，每个tab页都是一个单独的进程
  - 网络 
    - 用于网络调用，比如HTTP请求。其接口与平台无关，并为所有平台提供底层实现。
  - 用户界面后端 
    - 用于绘制基本的窗口小部件，比如组合框和窗口。
    - 其公开了与平台无关的通用接口，而在底层使用操作系统的用户界面方法。
  - JavaScript解释器
    - 用于解析和执行JavaScript代码。
  - 数据存储
    - 这是持久层。浏览器需要在硬盘上保存各种数据，例如Cookie。
    - HTML5定义了网络数据库，这是一个完整但轻便的浏览器内数据库
- 浏览器的基本组成是GUI和html解析引擎，后来js引擎也被独立出来。
- chrome的html解析引擎是webkit fork出来的blink，js引擎是v8。而GUI框架它是在哪个操作系统上就用那个操作系统的主流框架，比如在mac上就是Cocoa，在linux上就是gtk，windows它基于win32 API开发了一个自己的框架
- 目前的edge，这三样大概就是edgeHTML, chakra，和win32 API包括mfc wpf这一套东西
- Firefox的html引擎是gecko，js是spidermonkey，GUI是XUL, XUL是一个基于各平台得底层api开发的一个高层的跨平台的图形界面框架，所以还有好些软件是用XUL来做自己的界面。而且XUL和gecko spidermonkey耦合的挺深，要用基本上就都要用。


## Firefox

- HTML引擎：Mariner -> Raptor -> NGLayout -> Gecko
- JavaScript引擎：Mocha -> SpiderMonkey
- JIT即时编译器: TraceMonkey -> JaegerMonkey -> IonMonkey+OdinMonkey
