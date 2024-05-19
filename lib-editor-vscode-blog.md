---
title: lib-editor-vscode-blog
tags: [blog, vscode]
created: 2023-08-19T16:36:56.571Z
modified: 2023-08-19T16:37:13.736Z
---

# lib-editor-vscode-blog

# guide

# architecture
- [从 VSCode 看大型 IDE 技术架构 - 知乎 _201912](https://zhuanlan.zhihu.com/p/96041706)
  - 为什么要去看 VSCode？ 因为我们团队在做的中后台快速研发平台云凤蝶也是一款类似 Web IDE 形态的产品
  - 谈起 Web IDE，没人能绕开 VSCode，它非常流行，同时又完全开源，总共 350000 行 TypeScript 代码的巨大工程，使用了 142 个开源库。
  - 市面上选择基于 VSCode 去修改定制的 IDE 比比皆是：Weex Studio、白鹭Egret Wing、快应用IDE

- [hullis 博客系列](https://github.com/wzhudev/blog/issues?q=is%3Aissue)
  - [vscode 源码解析 - 依赖注入 · hullis/blog](https://github.com/hullis/blog/issues/25)
  - [vscode 源码解析 - 插件系统](https://github.com/hullis/blog/issues/37)
# extensions/插件系统
- [vscode插件原理浅析与实战 - 掘金](https://juejin.cn/post/7099838116789387295)
# web
- [vscode.dev Visual Studio Code for the Web_202110](https://code.visualstudio.com/blogs/2021/10/20/vscode-dev)
# server/remote
- 对我来说 vscode 最好用的功能，remote dev 是闭源的。
  - 当然你可以扒压缩混淆过后的 js 源码。

- [Visual Studio Code Server](https://code.visualstudio.com/docs/remote/vscode-server)
  - The Visual Studio Code Server is a service you can run on a remote development machine, like your desktop PC or a virtual machine (VM). 
  - It allows you to securely connect to that remote machine from anywhere through a local VS Code client, without the requirement of SSH.
  - The VS Code Remote Development extensions install a server on the remote environment, allowing local VS Code to smoothly interact with remote source code and runtimes.
  - We now provide a standalone "VS Code Server, " which is a service built off the same underlying server used by the remote extensions, plus some additional functionality, like an interactive CLI and facilitating secure connections to vscode.dev.
  - Access to the VS Code Server is built in to the existing code CLI.
  - an instance of the server is designed to be accessed by a single user.
  - hosting it as a service is not allowed, as specified in the VS Code Server license.
# license
- [Differences between the repository and Visual Studio Code](https://github.com/microsoft/vscode/wiki/Differences-between-the-repository-and-Visual-Studio-Code)
  - Visual Studio Code is a distribution of the Code - OSS repository with Microsoft specific customizations, including additional source code and extensions, released under a traditional Microsoft product license.
# blogs-collab

## [Collaborative Editing with React Monaco Editor: Best Practices _202405](https://www.dhiwise.com/post/collaborative-editing-with-react-monaco-editor) 

- 没有涉及协同编辑
# blogs

# more
