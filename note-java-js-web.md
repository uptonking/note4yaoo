---
tags: [java, js, web, webview]
title: note-java-js-web
created: '2019-10-15T12:34:00.837Z'
modified: '2019-10-25T10:07:02.908Z'
---

# note-java-js-web

## js engine
- jdk里的js引擎  
    - JavaScriptCore：在JavaFX webview里的JavaScript解析引擎
        - 在JavaFX的Webview中支持触摸, 虚拟键盘等
    - Nashhorn：JDK 8里的JavaScript引擎, 就是JSR 223
    - Rhino：JDK 7里的JS引擎

## webkit
- v8是谷歌开源的一个基于C++语言开发的JavaScript引擎，可以实现ECMA-262中规定的ECMAScript，其被用于谷歌浏览器chrome、安卓浏览器、node.js等大型项目当中，V8引擎可以独立运行不依赖于其他环境，也可以嵌入任何的C++应用当中使用
- JavaScriptCore是WebKit中默认的JavaScript引擎，它是苹果开源的一个项目，是苹果Safari浏览器的JavaScript引擎，应用较为广泛
- JavaScriptCore的大致流程：JavaScript源代码 -> 抽象语法树（AST）-> 字节码-> 本地代码
- V8的大致流程：JavaScript源代码 -> 抽象语法树（AST）-> 本地代码 （2017年4月发布5.9版本后新增了Ignition字节码解释器，与JScore流程大致相同）
- 参考
    - https://zhuanlan.zhihu.com/p/27628685

### blink
- chromium早期的排版引擎是Webkit，后面慢慢的Webkit被google改成了blink，虽然名字改了但是目前很多框架和原理还是Webkit
- 随着浏览器内核的发展，blink和webkit越走越远，最近的一个大改动就是使用最新的NG排版引擎
- 早期Blink采用的是引用计数管理内存，引用计数有循环引用的风险，C++中可以通过Raw指针绕开引进计数的管理，存在风险
- Blink是实现了**Oilpan**垃圾自动回收机制

## react-native
- React Native对于你写的所有JS和JSX代码都会被JS Engine来执行。在iOS上，默认的就是JavaScriptCore， iOS 7之后的设备都支持，**iOS不允许用自己的**JS Engine
- JavaScriptCore来自于WebKit，安卓上默认也是用JavaScriptCore
- 有关原生功能调用的第三方库不够丰富，质量不高
- 也许可互操作，flutter可能会变成rn的一个实现，一个backend，一个基于skia的rn

