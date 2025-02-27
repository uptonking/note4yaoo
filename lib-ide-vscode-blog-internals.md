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

# vscode原理

## 

## 

## 

## 

## [VSCode Architecture Analysis - Electron Project Cross-Platform Best Practices - DEV Community _202310](https://dev.to/ninglo/vscode-architecture-analysis-electron-project-cross-platform-best-practices-g2j)

## [Migrating VS Code to Process Sandboxing _202211](https://code.visualstudio.com/blogs/2022/11/28/vscode-sandbox)

- Enabling the sandbox in Electron renderer processes is a critical requirement for secure and reliable Electron applications such as Visual Studio Code. 
  - The sandbox reduces the harm that malicious code can cause by limiting access to most system resources.
- This was a team effort as fundamental architectural changes as well as code modifications were required in almost all VS Code components.
  -  The VS Code process architecture was overhauled and in the process significantly strengthened. 

- For a long time, Electron has allowed direct use of Node.js APIs in HTML and JavaScript. 
  - Components in the renderer process that require access to system resources will have to delegate to another process that is not sandboxed.
  - Blocking Node.js from renderer processes is an encouraged Electron security recommendation. 

- While creating a web version of VS Code, we had learned how to remove Node.js dependencies from the workbench – the main VS Code user interface window.
  - Removing dependencies to Node.js meant finding alternatives. For example, our dependency on the Node.js Buffer type was replaced with a VSBuffer equivalent that would fall back to Uint8Array in browser environments. We were also able to package some Node.js modules (oniguruma, iconv-lite) to run in web environments.

- When a renderer process cannot use Node.js, work must be delegated to another process where Node.js is available. 
  - One solution in the web context could be to rely on HTTP methods, where a server accepts the requests. 
  - However, this did not feel like the best solution for desktop applications, where running a local server on a port could be blocked by a firewall for security reasons.
  - Electron provides the ability to inject `preload` scripts into the renderer process that execute before the main script executes. 

- Fast inter-process communication via message port
  - Even before working on sandboxing, we were interested in offloading performance intensive code to a background process, the VS Code shared process. This process is a hidden window that all workbench windows and the main process can communicate with.
- communication to the shared process was implemented over Node.js sockets. 
  - This had the advantage that there was zero overhead for the main process because it was not involved in the communication at all. 
  - The disadvantage is that Node.js socket communication is not possible in sandboxed renderers since you cannot use any Node.js APIs.
- Message ports provide a powerful way of connecting two processes with each other by establishing an IPC channel between them. 
  - Even a fully sandboxed renderer process can use a message port because they are provided as a web API in browsers. 
  - Replacing the Node.js socket communication with message ports allowed us to have a sandbox-compatible IPC solution while still preserving the performance aspect of not having to involve the main process.

- when you open VS Code, a window loads with a pre-configured URL to show the content of the workbench.
  - For VS Code, this URL had used the local file protocol pointing to an actual file on disk to load (`file://<path to file on disk>`). As part of the sandboxing work, we revisited this approach because it had severe security implications. Chromium makes certain security assumptions for the local file protocol that are less strict compared to the HTTPS protocol. For example, strict origin checks are not applied for local file protocol URLs.
- With Electron, you can register custom protocols that can be used to load content into the renderer process. 
  - The custom protocols can be configured so that they behave the same as HTTPS protocols with respect to security. 
  - We used this approach to avoid having to run a local web server that serves the content.
  - With the introduction of the custom vscode-file protocol for all our renderer processes, we were able to drop all uses of the file protocol. It is configured to behave like HTTPS and meant we moved closer to how VS Code for the Web actually works.

- Moving processes out of the renderer
  - The diagram below shows our process architecture in late 2022, once we had enabled the sandbox in the renderer process. All Node.js processes have moved to be either a child of the shared process or a utility process from the main process. 
  - Message ports are used for efficient direct process-to-process communication without burdening the main process.

- A new Electron API: UtilityProcess
  - The final and probably most complex task was finding a solution for where to move the extension host. 
  - Like the shared process, communication was implemented via Node.js sockets. There is one extension host process per window and extensions are free to spawn as many child processes as they require.
  - We had thought about moving the extension host into our shared process like file watchers and integrated terminals but felt that we should take the opportunity and build something more flexible that does not require a hidden window as a host.
  - At that time, Electron was not able to provide us with an API that supports these requirements and so we contributed a new utility process API to Electron. 

- Moving off the Electron webview element
  - While not necessarily required to enable sandbox, we took the opportunity to revisit the use of the Electron `webview` tag in VS Code and replace it with the `iframe` tag to more closely align with how VS Code works in the web. 
  - Both tags are similar in that they allow the workbench to host untrusted code from extensions while isolating the workbench from the effects of running this code. 
  - In most cases, we were able to just replace the webview tag with the iframe tag. However one feature was missing from iframes, the ability to perform and highlight textual searches in the content.
  - While Chromium internally implemented this functionality, it was not exported as a web API to use. We made the necessary changes to expose the API in Electron and were able to drop all usages of webview elements.

- Enabling renderer process reuse
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
