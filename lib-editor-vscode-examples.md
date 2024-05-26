---
title: lib-editor-vscode-examples
tags: [examples, monaco-editor, toc, vscode]
created: 2023-01-21T18:57:55.760Z
modified: 2023-01-21T18:58:29.846Z
---

# lib-editor-vscode-examples

# guide

# popular
- https://github.com/DTStack/molecule /811Star/MIT/202312/ts
  - https://dtstack.github.io/molecule/
  - https://dtstack.github.io/molecule-examples/
  - 受 VSCode 启发，使用 React.js 构建的 Web IDE UI 框架
  - 我们设计了类似 VSCode 的扩展(Extension)机制，可以帮助我们使用 React 组件快速完成对 Workbench 的自定义
  - 依赖tapable、tsyringe、react-dnd、monaco-editor、immer、rc-menu
  - 不依赖antd，总体依赖不多
  - 内置 React 版本的 Visual Studio Code Workbench UI
  - 内置 Monaco Editor Command Palette、Keybinding等模块，并支持扩展
  - 内置一个简单的 Settings 模块，支持在线编辑修改以及扩展
  - 内置默认的 Explorer, Search 等组件，并支持扩展
  - ⚖️ [vscode插件市场支持](https://github.com/DTStack/molecule/issues/879)
    - 有没有什么方法可以比较方便的移植vscode的插件，或者考虑后面的版本中增加对vscode插件进行支持
    - 并没有，考虑到大部分的 vscode 的插件增强的是 vscode 所实现的功能。其相关逻辑强依赖于 vscode。所以针对大部分的 vscode 插件无法做到方便的移植。
    - 而针对除此之外的小部分 vscode 插件，诸如 icons，themes 倒是可以参考 文档
  - [我们开源了一个轻量的 Web IDE UI 框架 - 知乎 _202112](https://zhuanlan.zhihu.com/p/446147101)
  - [我们开源了一个轻量的 Web IDE UI 框架 - Molecule - V2EX_202112](https://www.v2ex.com/t/823289)
    - 与其他开源的 Web IDE 的区别？
    - 🧐 Molecule只是一个单纯的 Web IDE UI 交互框架，不涉及例如文件系统、版本管理、LSP、DAP、Terminal 等更复杂的 IDE 功能，需要开发者自己手动实现
    - React.js 应用无缝接入, 基于 React.js 的组件库，更好的 UI 自定义能力
    - 基本兼容了 VS Code 上千种 ColorTheme 扩展
    - 有类似交互场景的 Web 应用，如果搞不懂 VS Code 可以试试这个，比较简单一些
    - 和 jupyter lab 比如何？我还是比较期待 jupyter lab 演化出的 IDE 的扩展，像 jupyterlab-lsp 之类的
  - https://github.com/DTStack/molecule/tree/2.x
    - [feat: 2.x search ](https://github.com/DTStack/molecule/pull/872)
      - 新增 Search 组件
    - [Feat/folder tree 2.x dilu ](https://github.com/DTStack/molecule/pull/873)
      - 新增 FolderTree 组件; 重写拖拽逻辑，不限制拖拽文件，交给用户去限制
    - https://github.com/DTStack/dt-react-monaco-editor
      - https://dtstack.github.io/dt-react-monaco-editor/
      - 基于开源 monaco-editor，根据业务使用场景进行二次封装
      - 支持通过 props 传递的方式自定义自动补全项和需要高亮的关键字

- https://github.com/opensumi/core /2.7kStar/MIT/202405/ts
  - https://opensumi.com/
  - https://preview.opensumi.com/
  - 一款帮助你快速搭建 CloudIDE 及 桌面端IDE 产品的底层框架
  - 提供了一个强大的插件生态系统，兼容 VS Code 的插件系统，支持 LSP/DAP 等主流协议，我们也有着自己的 OpenSumi API 用于进一步拓展 IDE 界面及能力
  - 不提供针对特定端的以下能力
    - Desktop IDE 场景下的窗口管理
    - Cloud IDE 场景下的容器/虚拟机管理
  - CodeBlitz主要在读、写、运行和提交等方面进行了探索，与带有容器的标准版本进行了对标
  - [离线部署 | OpenSumi](https://opensumi.com/zh/docs/integrate/universal-integrate-case/offline-deployment)
    - OpenSumi 天然支持离线部署场景，只需要将内部的一些网络资源如（icon、onig-wasm）等通过浏览器端的配置替换成内网的资源地址即可
  - https://github.com/opensumi/codeblitz /MIT/202401/ts/inactive
    - https://codeblitz.opensumi.com/
    - https://codeblitz.cloud.alipay.com/zh
    - 基于 OpenSumi 的纯前端 IDE 基础框架
    - Pure front-end IDE framework based on OpenSumi
  - [如何评价阿里 & 蚂蚁自研 IDE 研发框架 OpenSumi？ - 知乎](https://www.zhihu.com/question/519740662)
    - 高性能、高定制性的双端（Web 及 Electron）IDE 研发的框架
    - 设计之初就是要兼容 VS Code 插件生态，我们计划每三个月时间去完成一次 VS Code 插件 API 的适配工作
  - [极速版 IDE 框架 CodeBlitz 开源啦！ - 知乎_202309](https://zhuanlan.zhihu.com/p/656515617)
    - 在OpenSumi的基础上对文件系统、通信系统、插件机制等模块进行扩展，以更好地适用于没有容器、本地客户端环境的纯浏览器环境
    - CodeBlitz提供了一种只需使用浏览器即可体验IDE的场景。与github.dev和vscode.dev不同的是，CodeBlitz是一个框架，通过OpenSumi模块和插件的方式，可以为上层产品量身定制符合其业务场景的WebIDE。

- https://github.com/VSCodium/vscodium
  - https://vscodium.com/
  - binary releases of VS Code without MS branding/telemetry/licensing
  - the Open VSX Registry is the pre-set extension gallery in VSCodium. Using the extension view in VSCodium will therefore by default use it.
  - [Run vscodium in browser](https://github.com/VSCodium/vscodium/discussions/1469)
    - is there a definitive answer for a web version of vscodium?
  - [Switching between marketplaces](https://github.com/VSCodium/vscodium/issues/519)
    - If it helps anyone, there's a AUR (Archlinux User Repository) that adds the VSCode marketplace to VSCodium. 

- https://gitlab.com/gitlab-org/gitlab-web-ide-vscode-fork /MIT/202405/ts
  - GitLab Web IDE - VSCode Fork
  - An internal fork of the VSCode project, used to power GitLab's Web IDE
  - This fork is used for building tools-injector for remote development.
# apps

# vscode-web
- https://github.com/Felx-B/vscode-web /MIT/202311/js
  - This project is aimed to build a web version of VSCode, this is not a fork, simply a web compilation of the VSCode project.
  - Microsoft recently open sourced VSCode web compilation, so I simplified the build process to use the official compilation (no more tweak needed).
# vscode-server
- https://github.com/coder/code-server /MIT/202405/ts
  - https://coder.com/
  - Run VS Code on any machine anywhere and access it in the browser.
  - Requirements: Linux machine with WebSockets enabled, 1 GB RAM, and 2 vCPUs
  - https://github.com/coder/coder /AGPLv3
    - Provision remote development environments via Terraform
  - [Difference to OpenVSCode Server _202109](https://github.com/coder/code-server/discussions/4267)
    - code-server isn't a Docker image, although Docker images for code-server exist. 
    - I'd prefer code-server since Gitpod's VS Code Web Server doesn't allow me to use `sudo` command
    - since code-server is used on Coder(dev workspaces) but I don't think code-server will be dead. I think for collaborating with multiple people simultaneously, Open VS Code is best but for individuals, code-server is recommended since it has protection.
    - ~~One little known gotcha is that OpenVSCode does not let you pre-install extensions in a non-interactive mode (e.g. during docker build to ship after security scanning for use on air-gapped servers)~~. This does not appear to be the case anymore.
  - Here is my summary of differences:
    - 🔒 code-server support auth (protect the editor with password) while OpenVSCode doesn't
    - OpenVSCode installs extensions from open-vsx, while code-server is in the process of switching to open-vsx
    - TAB is working in the code-server's terminal. Doesn't work in the OpenVSCode. This difference may seem small, but significant to my day-to-day use
    - I figured how code-server handles user account in Docker, but haven't figure out yet how OpenVSCode does it in the Docker
  - [FAQ](https://github.com/coder/code-server/blob/main/docs/FAQ.md)
  - 🤔 Why can't code-server use Microsoft's extension marketplace?
    - The core of VS code is open source, while the marketplace and many published Microsoft extensions are not. 
    - Microsoft prohibits the use of any non-Microsoft VS Code from accessing their marketplace. 
    - Instead, we use the Open-VSX extension gallery
  - 🆚️ What's the difference between code-server and Theia?
    - Theia is a browser IDE loosely based on VS Code. It uses the same text editor library (Monaco) and extension API, but everything else is different. Theia also uses Open VSX for extensions.
  - 🆚️ What's the difference between code-server and OpenVSCode-Server?
    - OpenVSCode-Server is a direct fork of VS Code with changes committed directly while code-server pulls VS Code in via a submodule and makes changes via patch files.
    - OpenVSCode-Server is scoped at only making VS Code available as-is in the web browser. 
      - code-server contains additional changes to make the self-hosted experience better 

- https://github.com/gitpod-io/openvscode-server /MIT/202405/ts
  - This project provides a version of VS Code that runs a server on a remote machine and allows access through a modern web browser. 
  - It's based on the very same architecture used by Gitpod or GitHub Codespaces at scale.
  - in 2019 the VS Code team started to refactor its architecture to support a browser-based working mode. While this architecture has been adopted by Gitpod and GitHub, the important bits have not been open-sourced, until now. As a result, many people in the community still use the old, hard to maintain and error-prone approach.
  - At Gitpod, we've been asked a lot about how we do it. So we thought we might as well share the minimal set of changes needed 
  - [VS Code in the browser for everyone - Blog _202109](https://www.gitpod.io/blog/openvscode-server-launch)
# vscode-collab
- https://github.com/sekassel-research/vscode-collab-plugin /ts
  - Collaborative editing plugin for VSCode/code-server/fulib.org Projects
  - This extension is designed to work with code-server and allows for real-time synchronization of work on projects. 
  - However, it's important to note that this synchronization only works when users are working on the same directory. 
  - The extension does not support synchronization between different directories or projects
# vscode-integrations
- https://github.com/betatim/vscode-binder /python
  - VS Code on Binder, because sometimes you need a real editor.
# more
