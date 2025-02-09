---
title: lib-ide-vscode-blog-internals
tags: [blog, internals, vscode]
created: 2024-08-24T16:57:07.196Z
modified: 2024-08-24T16:57:22.198Z
---

# lib-ide-vscode-blog-internals

# guide

# architecture
- [从 VSCode 看大型 IDE 技术架构 (云凤蝶版) - 知乎 _201912](https://zhuanlan.zhihu.com/p/96041706)
  - 为什么要去看 VSCode？ 因为我们团队在做的中后台快速研发平台云凤蝶也是一款类似 Web IDE 形态的产品
  - 谈起 Web IDE，没人能绕开 VSCode，它非常流行，同时又完全开源，总共 350000 行 TypeScript 代码的巨大工程，使用了 142 个开源库。
  - 市面上选择基于 VSCode 去修改定制的 IDE 比比皆是：Weex Studio、白鹭Egret Wing、快应用IDE
# extensions/插件系统
- [vscode插件原理浅析与实战 - 掘金](https://juejin.cn/post/7099838116789387295)
# 👷🏻 [vscode源码解析-wzhu](https://wzhu.dev/posts)
- [hullis 博客系列](https://github.com/wzhudev/blog/issues?q=is%3Aissue)

- [vscode 源码解析 - 插件系统](https://github.com/hullis/blog/issues/37)
- [vscode 源码解析 - 进程间调用 · hullis/blog](https://github.com/hullis/blog/issues/41)
- [vscode 源码解析 - 事件模块 · hullis/blog](https://github.com/hullis/blog/issues/40)
- [vscode 源码解析 - vscode loader · hullis/blog](https://github.com/hullis/blog/issues/43)
- [vscode 源码解析 - 依赖注入 · hullis/blog](https://github.com/hullis/blog/issues/25)
# 👷🏻 微软VSCode IDE源码分析 v1.37.1版本 (作者工作于腾讯云)
- https://github.com/fzxa/VSCode-sourcecode-analysis
  - 微软VSCode IDE源码分析 v1.37.1版本
  - 依赖版本 Nodejs x64 version >= 10.16.0, < 11.0.0, python 2.7(3.0不能正常执行)

- [微软 VSCode IDE 源码分析揭秘 - 知乎](https://zhuanlan.zhihu.com/p/99587182)

- 
- 
- 
- 
- 

# 系列博客

-[vscode 定制开发 —— 基础准备 | 匠心博客](https://zhaomenghuan.js.org/blog/vscode-custom-development-basic-preparation.html)

- [vscode源码分析【一】从源码运行vscode - liulun - 博客园 _201906](https://www.cnblogs.com/liulun/p/11037537.html)
  - 作者专注于electron开发

- [vscode 源码学习 2- 目录结构 _202011](https://juejin.cn/post/6898907525547524110)

- [VS Code源码简析 | 黯羽轻扬 _201802](https://www.ayqy.net/blog/vs-code%E6%BA%90%E7%A0%81%E7%AE%80%E6%9E%90/)
# more-blogs-internals
- [图解 VSCode 源码架构前言 _202401](https://juejin.cn/post/7329573754987528229)
  - https://github.com/lzy19926/lzy-VSCode-Editor /202310/ts/inactive
    - 模仿VSCode原理与架构实现的简易版桌面端代码编辑器
  - Electron的渲染进程和主进程之间有进程隔离, 那么必然就有对应的通信机制, VSCode内部提供了以下三种通信机制
  - IPC进程通信模块: 在Electron的IPC模块基础上进一步封装, 每个打开的窗口既是Server也是Client
  - `:VS`内部通信协议: vscode-webview/vscode-file, 更安全高效，支持更多功能
  - Shared Process共享进程通信
  - 为了统一渲染进程与主进程代码的构建方案, VSCode中提供了自己的内部构建工具, 可以理解为内部自行实现了仅支持AMD的简易webpack
  - CodeMain: VSCode在Electron主进程中运行的服务, 同时也是VSCode的入口全局单例
  - VSCode中运行的每个插件, 都会单独启动一个node子进程(child_process), 主进程会暴露大量API供插件进程调用, 插件进程间由共享进程进行插件通信, 如果我们做VSCode插件开发, 其实也就是通过组合调用各种VSCode主进程提供的API实现对应的功能

- [VSCode技术解析与实践 (偏向卖课)](https://codeteenager.github.io/vscode-analysis/guide/introduction.html)
