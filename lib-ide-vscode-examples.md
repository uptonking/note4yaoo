---
title: lib-ide-vscode-examples
tags: [examples, monaco-editor, toc, vscode]
created: 2023-01-21T18:57:55.760Z
modified: 2024-08-24T16:15:54.137Z
---

# lib-ide-vscode-examples

# guide

# popular
- https://github.com/microsoft/vscode /MIT/202501/ts
  - https://code.visualstudio.com/
  - This repository ("Code - OSS") is where we (Microsoft) develop the Visual Studio Code product together with the community.
- https://github.com/VSCodium/vscodium
  - https://vscodium.com/
  - binary releases of VS Code without MS branding/telemetry/licensing
  - This is not a fork. This is a repository of scripts to automatically build Microsoft's vscode repository into freely-licensed binaries with a community-driven default configuration.
  - [Extensions + Marketplace - VSCodium](https://vscodium-next.netlify.app/docs/extensions)
    - Open VSX Registry is the pre-set extension gallery in VSCodium
    - The `VSIX Manager` extension provides a powerful and user-friendly interface for managing `.vsix` files directly within VSCodium. Its author is the main maintainer of VSCodium
  - [Run vscodium in browser](https://github.com/VSCodium/vscodium/discussions/1469)
    - is there a definitive answer for a web version of vscodium?
    - AFAIK, the code-server seems to be the best option for now
  - [Switching between marketplaces](https://github.com/VSCodium/vscodium/issues/519)
    - If it helps anyone, there's a AUR (Archlinux User Repository) that adds the VSCode marketplace to VSCodium.
  - https://github.com/zokugun/vscode-vsix-manager /43Star/MIT/202508/ts
    - Install extensions from your own sources
    - `> VSIX Manager: Install extensions`: install the extensions in the config json
    - [Cannot find extension in official Marketplace _202309](https://github.com/zokugun/vscode-vsix-manager/issues/17)
  - 🧩 [What are reh and reh-web archives?](https://github.com/VSCodium/vscodium/blob/master/docs/others.md)
    - Remote Host (`reh`) is the server component for remote ssh/wsl which runs it on a "remote" computer and makes that remote computer accessible via VSCodium.
    - Web Host (`reh-web`) is the server component of the command `codium serve-web` which runs it locally and makes VSCodium accessible via a browser.
  - [Provide REH & web builds _202305](https://github.com/VSCodium/vscodium/issues/1518)
    - While the REH builds are great to interface with an existing VS Code installations, in very constrained environments where one is unable to even install a local build of VS Codium, it would be great to have access to the web variant of the REH builds mention in #1099 (comment) so that the setup could be fully self-contained, i.e. the web-variant of REH is deployed and made accessible via secured TLS connection and the user can immediately start working by accessing the web UI served by the REH host via a well-known URL.
    - I support that,The vscode's server and `server-web` are different. May vscodium do same as vscode? 
  - [Web UI not working _202510](https://github.com/VSCodium/vscodium/issues/2578)
    - I have this same issue when installing from the snap

- https://gitlab.com/gitlab-org/gitlab-web-ide-vscode-fork /MIT/202405/ts
  - GitLab Web IDE - VSCode Fork
  - An internal fork of the VSCode project, used to power GitLab's Web IDE
  - This fork is used for building tools-injector for remote development

- https://github.com/opensumi/core /2.7kStar/MIT/202405/ts
  - https://opensumi.com/
  - https://preview.opensumi.com/
  - https://opensumi.github.io/ide-startup-lite/
  - https://opensumi.com/zh/docs/develop/basic-design/core-idea
  - https://opensumi.com/zh/docs/develop/module-samples
  - 一款帮助你快速搭建 CloudIDE 及 桌面端IDE 产品的底层框架
  - 示例使用node.v16, 切换文件内容时，websocket会send当前内容数据文本
    - ❓ 或许是先receive二进制数据，再send文本数据
    - id:"CLIENT_ID_vEVx63rFu_uSoPAc2q4kt:ExtMainThreadConnection"
  - web和lite示例都不使用http通信，web示例使用socket，lite纯前端，web和lite的数据都存在localStorage
  - 提供了一个强大的插件生态系统，兼容 VS Code 的插件系统，支持 LSP/DAP 等主流协议，我们也有着自己的 OpenSumi API 用于进一步拓展 IDE 界面及能力
  - OpenSumi是前后端分离的设计，不论是在 Web 还是 Electron 环境下，浏览器/窗口中展示的界面部分我们称之为 OpenSumi 的前端，
    - 而对于文件读写、终端连接、插件进程等功能则运行在 OpenSumi 的后端。
    - 与传统的 B/S、C/S 架构不同的是，OpenSumi 前后端之间的通信仅由一个长链接连接实现。
      - ✨ 在 Web 环境下，前后端会建立一条 WebSocket 连接
      - 在 Electron 环境下，则会建立一条 Socket 连接进行进程间通信(IPC)
    - 核心功能的代码都是可以在 Web/Electron 端复用的，因为 connection 模块屏蔽了大部分平台、底层通信协之间的差异, connection 模块基于 JSON-RPC 2.0 实现了一个 RPC 框架，将 Web 与 Electron 端通信过程通过 RPC 协议来封装起来
  - 🔀 支持使用 3-way merge editor 新交互来解决代码冲突, (vscode本身支持)
  - 提供了ai模块
  - 🤝 协同编辑模块目前只支持 Browser + Node 的 Cloud IDE 场景, 当前的设计考虑的是客户端(Browser)/服务端(Node)一对一的架构
    - 不支持纯前端与 Electron 平台
    - 不支持 IDE 编辑器外的协同编辑功能（如终端）
    - 不支持 IDE 内跨文件的修改（如使用 vscode 插件进行变量重命名重构）
  - 不提供针对特定端的以下能力
    - Desktop IDE 场景下的窗口管理
    - Cloud IDE 场景下的容器/虚拟机管理
  - 前端与后端通过 RPC 的方式通信，与调用一个异步方法没有太大区别
    - 我们将模块划分为 核心模块 、功能模块。核心模块是指组成 IDE 核心功能的一些必选模块，如layout、browser、node
    - 功能模块一般是可插拔的，也就是在集成代码中可以将这些模块去除，或者重新替换实现，并不会影响其他功能
  - OpenSumi 插件系统是 VS Code 插件的超集，除了兼容 VS Code 官方的 API 之外，我们还有自己扩展的一些插件 API，以及包括前端、WebWorker 的插件等
    - 插件可以有 3 个入口，分别是 main 、browserMain 以及 workerMain
    - Browser 插件是 OpenSumi 特有的，通过 Contributes 来声明注册点，代码中导出对应的 React 组件来实现的
  - 贡献点这一概念源自 VS Code 中的一个设计理念，即通过一个基础的贡献点定义，可以让一个能力的完整实现，分散到各个子模块的贡献点文件之中。
    - 可以在公共模块中只进行 贡献点 机制下逻辑的执行
    - 通常我们在使用贡献点实现相应功能后，需要通过在模块内进行声明，同时在集成侧引入才能生效
  - CodeBlitz主要在读、写、运行和提交等方面进行了探索，与带有容器的标准版本进行了对标
  - [chore: add NOTICE.md ](https://github.com/opensumi/core/pull/558)
    - EPL2.0 属于文件级别的Copyleft许可证，即 EPL-ed 代码具有Copyleft 属性的，其“衍生作品”的包围也比较明确。EPL2.0追求的是EPL-ed代码的Copyleft和代码开源，且 MIT和EPL2.0许可证兼容。OpenSumi 本身是开源的，同时并未改变EPL2.0组件的许可，项目符合MIT和EPL2.0各自要求。
  - [离线部署 | OpenSumi](https://opensumi.com/zh/docs/integrate/universal-integrate-case/offline-deployment)
    - OpenSumi天然支持离线部署场景，只需要将内部的一些网络资源如（icon、onig-wasm）等通过浏览器端的配置替换成内网的资源地址即可
  - [快速开始（纯前端） | OpenSumi](https://opensumi.com/zh/docs/integrate/quick-start/lite)
    - 纯前端版本使用 BrowserFsProvider 替换 OpenSumi 内的 DiskFileSystemProvider, 改动在于由原来的本地文件服务改成 http 接口服务。
    - 代码修改后，会先调用对应方法同步到集成方的服务端，之后浏览器端也会在内存中缓存一份新的代码，刷新后失效。
  - [[FEATURE] 关于多用户](https://github.com/opensumi/core/issues/560)
    - 202203: 我们有在做一些多人协作的探索，比如 sumi-collaboration 是基于 Yjs 的一个简单的多人协作模块，现在处于调研阶段，后面会逐步完善
  - [如何评价阿里 & 蚂蚁自研 IDE 研发框架 OpenSumi？ - 知乎](https://www.zhihu.com/question/519740662)
    - 高性能、高定制性的双端（Web 及 Electron）IDE 研发的框架
    - 设计之初就是要兼容 VS Code 插件生态，我们计划每三个月时间去完成一次 VS Code 插件 API 的适配工作
  - [vscode扩展放进去后webview不能正常显示 _202311](https://github.com/opensumi/core/discussions/3315)
    - 我自己修改编写的vscode插件放进去extensions后，图标和相关的webview都没有显示
    - 我们的 webview 是基于 iframe 做的，因为 iframe 的一些通信的限制，我们需要通过加载 /webview/index.html 来包裹一层 webview，你这里的报错看起来是加载不到这个地址。
  - 📡 待实现 [[FEATURE] 支持离线安装插件 _202307](https://github.com/opensumi/core/issues/2873)
    - 增加导入本地插件的功能，类似于theia
  - https://github.com/opensumi/codeblitz /MIT/202401/ts/inactive
    - https://codeblitz.opensumi.com/
    - https://codeblitz.cloud.alipay.com/zh
    - 基于 OpenSumi 的纯前端 IDE 基础框架
    - Pure front-end IDE framework based on OpenSumi
  - [极速版 IDE 框架 CodeBlitz 开源啦！ - 知乎_202309](https://zhuanlan.zhihu.com/p/656515617)
    - 在OpenSumi的基础上对文件系统、通信系统、插件机制等模块进行扩展，以更好地适用于没有容器、本地客户端环境的纯浏览器环境
    - CodeBlitz提供了一种只需使用浏览器即可体验IDE的场景。与github.dev和vscode.dev不同的是，CodeBlitz是一个框架，通过OpenSumi模块和插件的方式，可以为上层产品量身定制符合其业务场景的WebIDE。

- molecule /811Star/MIT/202312/ts/仅web/不支持桌面
  - https://github.com/DTStack/molecule
  - https://dtstack.github.io/molecule/
  - https://dtstack.github.io/molecule/zh-CN/docs/introduction
  - https://dtstack.github.io/molecule-examples/
  - 受 VSCode 启发，使用 React.js 构建的 Web IDE UI 框架
  - 设计了类似 VSCode 的扩展(Extension)机制，可以帮助我们使用 React 组件快速完成对 Workbench 的自定义
  - 依赖tapable、tsyringe、react-dnd、monaco-editor、immer、rc-menu
  - 不依赖antd，总体依赖不多
  - 示例采用c/s架构, fileTree请求的响应内容包含文件列表和文件具体内容
  - 内置 React 版本的 Visual Studio Code Workbench UI
  - 内置 Monaco Editor Command Palette、Keybinding等模块，并支持扩展
  - 内置默认的 Explorer, Search 等组件，并支持扩展
  - 内置一个简单的 Settings 模块，支持在线编辑修改以及扩展
  - ⚖️ [vscode插件市场支持](https://github.com/DTStack/molecule/issues/879)
    - 有没有什么方法可以比较方便的移植vscode的插件，或者考虑后面的版本中增加对vscode插件进行支持
    - 并没有，考虑到大部分的 vscode 的插件增强的是 vscode 所实现的功能。其相关逻辑强依赖于 vscode。所以针对大部分的 vscode 插件无法做到方便的移植。
    - 而针对除此之外的小部分 vscode 插件，诸如 icons，themes 倒是可以参考 文档
  - [Write a Molecule demo with Electron _202203](https://github.com/DTStack/molecule/discussions/709)
    - great idea
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
# apps

# vscode-web/client
- https://github.com/Felx-B/vscode-web /MIT/202311/js
  - This project is aimed to build a web version of VSCode, this is not a fork, simply a web compilation of the VSCode project.
  - Microsoft recently open sourced VSCode web compilation, so I simplified the build process to use the official compilation (no more tweak needed).

- https://github.com/antfu/vscode-browse-lite /ts
  - Embedded browser in VS Code

- https://github.com/nightmare-space/code_lfa /BSD/202412/ts
  - Implementation of the VS Code editor natively on Android.
  - This is an Android version of VS Code implemented using code-server. Some have already implemented similar solutions, and this is one of them.
  - The principle is to run code-server and then use a webview to load the view. There might be some bugs, but it performs reasonably well.
  - Fully local operation of Code Server
  - Can run without an internet connection
# vscode-server
- https://github.com/pithings/coderaft /MIT/202604/ts
  - Run VS Code on any machine anywhere and access it in the browser.
  - A redistribution of `coder/code-server` bundled into a single zero-dependency package (~25 MB). 
  - Native modules are shimmed with better alternatives (zigpty, ripgrep-node, ...more).
  - Fully portable across platforms and architectures, unlike `code-server` (platform-specific binaries) and `openvscode-server` (Linux only)
  - Works everywhere Node.js runs, including minimal images like node:slim and node:alpine
  - https://x.com/_pi0_/status/2041682533906055594
    - A fully functional VS Code packed into a ~25MB, zero-dependency, platform-agnostic npm package.
    - node-pty replaced with slimmer zigpty
    - bundled ripgrep replaced with ripgrep-node (wasm)

- https://github.com/coder/code-server /68.8kStar/MIT/202411/ts
  - https://coder.com/
  - Run VS Code on any machine anywhere and access it in the browser.
  - Requirements: Linux machine with WebSockets enabled, 1 GB RAM, and 2 vCPUs
  - 👍🏻 pros: auth, patch-vscode, 通过第三方支持collab, terminal, easy to self-host, production-ready
  - 👎🏻 cons: slow to dev/build
  - code-server --auth none --port 8080
  - https://github.com/coder/coder /AGPLv3/go
    - Provision remote development environments via Terraform
  - 🆚 [Difference to OpenVSCode Server _202109](https://github.com/coder/code-server/discussions/4267)
    - code-server isn't a Docker image, although Docker images for code-server exist. 
    - I'd prefer code-server since Gitpod's VS Code Web Server doesn't allow me to use `sudo` command
    - since code-server is used on Coder(dev workspaces) but I don't think code-server will be dead. I think for collaborating with multiple people simultaneously, Open VS Code is best but for individuals, code-server is recommended since it has protection.
    - ~~One little known gotcha is that OpenVSCode does not let you pre-install extensions in a non-interactive mode (e.g. during docker build to ship after security scanning for use on air-gapped servers)~~ . This does not appear to be the case anymore.
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

- https://github.com/gitpod-io/openvscode-server /5.1kStar/MIT/202411/ts
  - This project provides a version of VS Code that runs a server on a remote machine and allows access through a modern web browser. 
  - It's based on the very same architecture used by Gitpod or GitHub Codespaces at scale.
  - in 2019 the VS Code team started to refactor its architecture to support a browser-based working mode. While this architecture has been adopted by Gitpod and GitHub, the important bits have not been open-sourced, until now. As a result, many people in the community still use the old, hard to maintain and error-prone approach.
  - At Gitpod, we've been asked a lot about how we do it. So we thought we might as well share the minimal set of changes needed 
  - [VS Code in the browser for everyone - Blog _202109](https://www.gitpod.io/blog/openvscode-server-launch)

- https://github.com/xaberus/vscode-remote-oss /MIT/202405/ts
  - Remote development for OSS Builds of VSCode like VSCodium
  - This extension allows you to use the existing remote extension host (REH) machinery of VSCode for OSS builds
  - Note: If you want an alternative that is limited to either SSH tunnels or WSL, you can try the extensions open-remote-ssh or open-remote-wsl instead.
# vscode-collab
- https://github.com/eclipse-oct/open-collaboration-tools /MIT/202408/ts
  - https://www.open-collab.tools/
  - ⚖️ Open Collaboration Tools: live-sharing solution for Eclipse Theia, VS Code and other editors and IDEs
  - This is how it works: one person starts a collaboration session as host and invites others to join. The IDE extension distributes the contents of the hostʼs workspace and highlights text selections and cursor positions of other participants. 
  - A public instance of the collaboration server is available at open-collab.tools.
  - [Announcing the Open Collaboration Tools | TypeFox _202407](https://www.typefox.io/blog/open-collaboration-tools-announcement/)
    - It's a collection of libraries and tools for live-sharing of IDE contents, designed to boost remote teamwork with open technologies.
    - The basic idea is simple: one person starts a collaboration session as host and invites others to join. The IDE extension distributes the contents of the hostʼs workspace and highlights text selections and cursor positions of other participants. 
    - A VS Code Extension available on Open VSX and the VS Code Marketplace

- https://github.com/sekassel-research/vscode-collab-plugin /202306/ts/archived
  - Collaborative editing plugin for VSCode/code-server/fulib.org Projects
  - This extension is designed to work with code-server and allows for real-time synchronization of work on projects. 
  - However, it's important to note that this synchronization only works when users are working on the same directory. 
  - The extension does not support synchronization between different directories or projects

- https://github.com/kainzpat14/code-collab /202107/ts/inactive
  - provides collaboration via Teletype and YJS to vscode and code-server.
  - Only YJS-Websocket is supported, all other YJS communication methods are not supported
  - Teletype support is limited, it can only share one editor at a time. I do not recommend using it
  - https://github.com/kainzpat14/code-server-collab

- https://github.com/PeerCodeProject/PeerCode /MIT/202402/ts
  - Realtime Collaborative Code Editor extension for vscode
  - Extension is based on CRDT`s concrete implementation YJS.
  - For peer to peer connection is used webRTC

- https://github.com/hanz-archer/VSCode-Live-Collab /MIT/202501/ts
  - A VS Code extension for real-time collaboration, allowing multiple users to edit the same file simultaneously. 
  - It syncs changes across instances using a unique document ID, making collaborative coding seamless.
  - 依赖firebase
# vscode-integrations
- https://github.com/betatim/vscode-binder /python
  - VS Code on Binder, because sometimes you need a real editor.
# utils(extracted)
- https://github.com/lzy19926/lzy-VSCode-Editor /202310/ts/inactive
  - 模仿VSCode原理与架构实现的简易版桌面端代码编辑器

- https://github.com/webdriverio-community/wdio-vscode-service /MIT/202502/ts
  - https://webdriverio-community.github.io/wdio-vscode-service/
  - A service to test VSCode extensions from end to end using WebdriverIO
  - This project was highly inspired by the vscode-extension-tester project which is based on Selenium. This package takes the idea and adapts it to WebdriverIO.
# LSP
- https://github.com/TypeFox/monaco-languageclient /MIT/202502/ts
  - monaco-languageclient: to connect Monaco editor with language servers.
  - vscode-ws-jsonrpc: which implements communication between a jsonrpc client and server over WebSocket.

- https://github.com/yioneko/vtsls /ts
  - This is an LSP wrapper around TypeScript extension bundled with VSCode. All features and performance are nearly the same.
  - Unlike other similar projects, this is implemented by filling VSCode APIs and applying minimal patches onto the extension to make it possible to keep up with the upstream updates and drastically reduce the burden of maintenance.

- https://github.com/hrsh7th/vscode-langservers-extracted /js/zed
  - HTML/CSS/JSON/ESLint language servers extracted from vscode.
  - Microsoft provided awesome Language Servers for the community but it didn't update for a long time.
    - Currently, the latest css-language-server is improved a bit than vscode-css-langserver-bin.

- https://github.com/zardoy/typescript-vscode-plugins /MIT/202410/ts
  - Use next-Gen TypeScript features in VSCode today
  - our main goal is to provide most customizable TypeScript experience for IDE features.
# more
- https://github.com/noworneverev/react-vscode-portfolio /MIT/202501/ts
  - https://noworneverev.github.io/
  - A vscode inspired portfolio website
  - The project is inspired by Visual Studio Code and caglarturali.github.io. The pages of the portfolio are powered by markdown, which make them easy to modify or add your own contents.
