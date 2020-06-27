---
tags: [browser, web]
title: note-web-browser-engine
created: '2020-06-27T08:19:22.900Z'
modified: '2020-06-27T08:43:00.851Z'
---

# note-web-browser-engine

## pieces
- 苹果曾经使用Gecko，嫌弃Gecko曾经有段时间太臃肿，就把KDE的HTML引擎KHTML、JavaScript引擎KJS加工过来，发布了WebCore+JavaScriptCore的Webkit并开源。
- 后来Google加入使用WebCore引擎，再后来Chromium又分支出去Blink引擎，JavaScript引擎是Google开源的V8。

## summary
- 浏览器的基本组成是GUI和html解析引擎，后来js引擎也被独立出来。
- chrome的html解析引擎是webkit fork出来的blink，js引擎是v8。而GUI框架它是在哪个操作系统上就用那个操作系统的主流框架，比如在mac上就是Cocoa，在linux上就是gtk，windows它基于win32 API开发了一个自己的框架
- 目前的edge，这三样大概就是edgeHTML, chakra，和win32 API包括mfc wpf这一套东西
- Firefox的html引擎是gecko，js是spidermonkey，GUI是XUL,XUL是一个基于各平台得底层api开发的一个高层的跨平台的图形界面框架，所以还有好些软件是用XUL来做自己的界面。而且XUL和gecko spidermonkey耦合的挺深，要用基本上就都要用。


## Chrome

## Firefox
- HTML引擎：Mariner -> Raptor -> NGLayout -> Gecko
- JavaScript引擎：Mocha -> SpiderMonkey
- JIT即时编译器: TraceMonkey -> JaegerMonkey -> IonMonkey+OdinMonkey

