---
title: lib-editor-vscode-theia-docs
tags: [docs, theia]
created: 2024-05-25T16:57:05.004Z
modified: 2024-05-25T16:57:45.541Z
---

# lib-editor-vscode-theia-docs

# guide

- pros
  - architecture is more modular and extensible
  - designed for desktop, browser, remote-server
  - openvsx extensions

- cons
  - theia is licensed under EPL, not as friendly as vscode/MIT

- features
  - ?

- who is using #theia
  - eclipse-che
  - ide: Arduino Pro IDE, 华为CodeArts
  - more: Google Cloud Shell

- tips
  - gitpod早期参与研发了theia，但2020年vscode开源remote和web后，gitpod将ide替换到了vscode
# blogs

## 🎯 [Theia: An Open Source Alternative to Visual Studio Code _202004](https://eclipse-foundation.blog/2020/04/01/theia-an-open-source-alternative-to-visual-studio-code/)

- With the release of Eclipse Theia 1.0, organizations and vendors that build cloud and desktop integrated development environments (IDEs) have a production-ready, vendor-neutral, and open source framework for creating customized development environments for both desktops and browsers. 
- Theia is an all-new code base with independent governance from the Eclipse desktop IDE.
  - Theia delivers an open source, extensible and adaptable platform that provides all of the capabilities of VS Code but which can be tailored to specific use cases. 
  - It can also leverage all of the extensions available for Microsoft Visual Studio (VS) Code
- Theia project was started in 2016 by Ericsson and TypeFox. In addition to Eclipse Che using Theia as its web IDE, many organizations of all sizes rely on Theia as the foundational building block for their development environments
  - Google Cloud Shell runs Theia as its editor
  - The default IDE for Red Hat CodeReady Workspaces is based on Eclipse Theia
  - The frontend of Arduino Pro IDE is based on Theia

- Theia’s more than an alternative to VS Code. 
  - The main differentiator between Theia and VS Code is that Theia is specifically intended to be adopted by other companies and communities to build and deploy a modern web-based developer experience. VS
  - Code is great, but it is only ever going to be a Microsoft product.
- Theia is intended to be modified, extended, and distributed by folks who want to create developer tools that look as great as VS Code (including using the same Monaco Editor) and can make use of the VS Code extension ecosystem.
- Theia’s architecture is designed to be more modular and extensible than the VS Code so developers have a greater ability to customize their solutions for specific requirements. 
  - VS Code enables a great extension ecosystem. Theia goes beyond that and is designed to be modified and extended at all levels of its architecture.
- Theia is designed from the ground up to run in both desktop environments as well as in browser and remote server environments. 
  - IDE developers can write the source code for their development environment once, then build a desktop IDE, a cloud IDE, or both, without rewriting any code.
- Theia uses the Eclipse Open VSX Registry, an open-source alternative to the Microsoft Visual Studio marketplace.
  - the extensions available in this free marketplace can be used in VS Code as well as in Theia.

## [Eclipse Theia技术揭秘——初识Theia _202209](https://xie.infoq.cn/article/ef9d31c5165a5d5bdccd5e372)

- Theia被设计成一个桌面应用程序，也可以在浏览器和远程服务器的环境中工作。
  - 为了支持这两种情况，Theia 在两个单独的进程中运行。这些进程分别称为前端和后端，它们通过 WebSocket 上的 JSON-RPC 消息或 HTTP 上的 REST API 进行通信。
  - 对于 Electron，后端和前端都在本地运行，而在远程上下文中，后端将在远程主机上运行。前端和后端进程都有它们的依赖注入（DI）容器方便扩展功能。
- 插件开发：VS Code 提供扩展注册命令、菜单、视图、语言服务器等相关功能，目前只能通过 VS Code 提供的 API 进行扩展，无法更换 logo，移除默认菜单、命令，创建复杂视图等功能。
  - 💡 而 Theia 其实提供了两种插件机制，一种是类似于 VS Code 的插件开发机制， Plugin，它依赖于 Theia 提供的 API 进行插件开发，用户可在 IDE 运行时进行插件的安装、卸载。
  - 另外一种是 extension，这是直接构建在了我们工具当中，用户无法进行修改，它可以访问 Theia 内部的所有方法，我们可以对 Theia 所有的功能进行个性化开发。这种插件开发的缺点是，对开发人员要求相对而言比较高，需要了解 Theia 的内部机制，现有文档基本上也无法满足高定制化的开发需求。

## 🌰 [如何在团队内快速落地WebIDE - 知乎 _202109](https://zhuanlan.zhihu.com/p/411030285)

- 在云音乐团队内部的WebIDE终于落地了。目前功能上覆盖前端正常的业务开发已无问题，期间也踩了不少坑，故写此篇文章
- 在发起WebIDE这个项目之初，很多人，上级、同事、部门领导，都会对项目发起质疑：意义在哪？能带来什么业务价值？
1. 激发团队活力，提升新人留存率。本身作为一项不太普及的技术，其实或多或少能够激发团队的思考，增加团队活力。而作为一项未来可能成为前端基建的技术，对于新人的留存是有帮助的。基建不完善，那么新人招来了，内心必定会吐槽，流失也就理所当然。
2. 切换项目更方便。对于multirepo的前端团队，相信不少同学经常会在3-4个项目间切换，项目启动关闭一次较麻烦不说，对电脑的电量，内存都是不小的负荷。而webide将这一部分负荷转移到远程容器，省去了本地的负荷和每次启动打开的不便(finder -> terminal -> run dev -> open vscode)，说实话，个人感觉开发起来更方便。毕竟启动项目就是打开一个网页，而关闭项目也无需担心进度未保存。
3. 团队配置化的统一。统一化插件、ide配置，代码移交更顺畅
4. 远程办公。疫情之下，不多说，不必合适的设备即可写代码，便利性极大提升
5. 代码更加安全。稍加限制，即可防止代码被拷贝，同时从公司层面，衡量程序员的工作时间会更加方便（ps：我是不会把这个功能做进去的，程序员使用IDE的时长对衡量程序员的价值没有多少参考意义）
6. demo编写方便。开源的公开的工具很多，但是往往需要私有包，这一点外部开源项目基本无能为力
7. 研发平台的整合，闭合研发链路。团队大了，各个平台层出不穷，开发过程中往往会伴随多个平台的切换，将IDE嵌入网页，同时整合各个研发平台，避免反复切换平台带来的繁琐与不便
8. 私有插件。当然避免团队插件发布共有域的方案也有，但是直接搭建私有插件市场，更加方便直观。

- 个人认为，讨论一项还未落地的技术的意义，不见得是一个有意义的讨论。WebIDE的意义有多大，更多的取决于团队能把，或者说想把这个事做的多大。对IDE感兴趣？干就完事了。

- 虽然WebIDE本身还未流行，但是在各大云厂商，各大国内大厂均已有落地产品，谈不上一个比较新的技术，而其实现方案，也基本明确并且成熟，此处挑几个进行简单介绍。

- vscode流派
  - 比较流行的方案，代表有coder，code-server，vsonline。
  - 这一类IDE产品，基于vscode进行web端的一些修改，同时贴合github，实现个人项目的webide开发。
  - 但是缺点很统一：收费且团队难以接入使用（团队登陆检验，gitlab接入），代码安全也难以保证

- Theia
  - 比较流行的方案。
  - 一部分功能复用vscode，但是设计初衷便是为了扩展，所以私有化部署，定制化功能极其方便。
  - 目前有的产品有：gitpod，阿里系ide（自研kaitian不是基于theia），华为云ide，google云ide。
  - 在扩展能力上，远超vscode，同时具备全开源，社区活跃度较高，接入改造成本低，不收费的优点
  - 本人在团队内落地的IDE也是基于该框架。

- stackblitz
  - 本来个人认为他是与codesandbox一个流派的，但是他推出了web container的概念，提供了非容器化方案的纯前端node环境，可以说非常有价值。
  - 目前该方案不开源，目前猜测较多的是service worker实现请求拦截，webassembly提供了node的环境，从而实现不需要远程机器，全部都跑在浏览器的一个IDE。
  - 整体来讲，其技术方案的优点在于不消耗远程资源，但是缺点，一个是不开源，一个是毕竟是模拟的node环境，在各个系统的一些层面可能会有所缺失（猜测）。

- 还有一些其他的方案：
  - 基于前端构建的codesandbox，这个网上分析的文章比较多，此处不赘述，其缺点在于没有完整的命令行，跑跑基于webpack的前端页面还行，node代码不能跑起来的，更多的是拿来写ui demo的一个工具。
  - 阿里的kaitian，纯自研的一款IDE，尝试取代THEIA的一款纯自研的IDE，目前未开源
  - coding团队的webide，coding，曾经开过源，目前不明

- 整体对比
  - vscode流派：付费，接入不便，扩展不易
  - theia流派：业内流行的开源方案，成熟落地产品多，扩展非常容易
  - Stackblitz: 技术方案独特，纯前端的WebIDE，但是目前看除了写demo快，团队接入和扩展都没有提供方案
  - codesandbox: 前端构建的，更多用来写demo
  - kaitian, coding等自研，不开源，具体不太清楚

- 对于团队需要的WebIDE，个人认为满足日常的开发是必须的。所以易扩展，一定是排在第一位的，这一点非theia莫属。而开源、不收费、稳定性好、社区活跃也是theia的长处。长期来看，theia的接入成本低、扩展性好，社区活跃方便后期维护，是一个非常棒的方案。本人在云音乐团队落地的也是最终采取的这一方案。

- 在笔者看来，一个自行车版WebIDE所需要具备的基础能力有：
  - 团队成员管理系统 or oa接入
  - 团队gitlab接入
  - 私有包安装的能力
  - IDE管理，新建，关闭，删除等基本功能
  - 支持前端项目运行

- 出于满足上述能力的需求，笔者最初（后来也只是新增了一些独立的工程）将项目划分为4个工程：
  - Ide-studio: 前端管理后台，负责IDE的新建，关闭，后期可拓展出插件市场等功能
  - Ide-studio-backend: 纯nodejs后台，一方面负责管理后台的接口，另一方面接入团队成员管理系统，后期可用来拓展私有插件以及共有插件等功能，同时处理和容器化部署平台的协作。
  - Ide-extension: 用于开发theia扩展，定制团队特有功能，比如接入团队成员管理系统，记录活跃时间，集成团队内部研发平台等
  - Ide-docker: 用于存放ide的docker相关文件。由于theia本身是为拓展而生，只需要一个package.json即可生成ide相关，所以单独将docker镜像的构建伶出来

- theia本身已有容器启动方案，已经提供了dockerfile文件，可以直接使用该docker进行部署，笔者团队使用的是基于theia-docker进行的修改。

- 笔者基于egg.js搭建了IDE的后台，主要承载的能力有：
  - IDE管理，比较常规的后台接口
  - 插件管理，私有插件的自存储，公有插件进行转发到openvsx
  - 处理网易轻舟云容器部署、域名转发等服务的交互（网易轻舟，个性化等用下来体验还不错）
  - 处理IDE容器内，插件安装/搜索时需要的一些服务处理
  - 基本的成员登陆/注销
  - 整体来讲，代码基本跟平时的node服务无差。不再赘述

- VSX_REGISTRY_URL，这是插件市场的插件源改动，默认是指向openvsx，要实现私有插件，直接改变其到自己的私有市场并实现相关接口即可

- webide作为一项成熟的技术，团队落地整个流程下来，笔者认为回头去看，其实没有什么特别大的坑点以及技术上的难点。

- 原本题目准备起：前端小白如何在团队内落地webide，但是后来想想，这就有点误人子弟了，虽然前端相关的代码确实没写几行，但是对其他的一些知识需要一定的储备，比如容器化、node、运维等知识。

- 最后，笔者在建立了完备的webide之后，自己的业务都已经在webide上进行开发，但是团队的大部分成员还是持保守态度。后续会继续提升开发体验，让越来越多的成员接纳这个套了老技术的新IDE。

- 👥 
- 感觉这8点都不是很有必要。。总觉得很多时候都是先上了再说，上完再给 PPT 找点理由
- 团队配置化的统一还是很重要的，依赖本地环境经常出现各种难以想象的问题，找个docker扔进去实在是省掉太多事了，也方便跨团队合作，并且能有效减少没有意义的文档工作
- webide就是个噱头，实际上本地研发才是效率第一。什么配置统一、远程办公、项目切换等，本地研发也都可以。webide 没有啥优势，反而在文件上传、操作交互、打开率等方面不友好
  - 可以解决团队重复配置和多电脑切换问题。管理者才有这种思考
- 个人感觉vscode remote可能是更平滑可用的选择
- 你要是推荐Theia，那国内的华为要气死了，人家自己基于Theia套壳了一个IDE说是自研的，你直接把人家底裤给扒开了。
- 只是UI 作用不大 持续自动测试 持续自动发布 集成在一起就有意思了
- web ide配置vim插件容易出问题

### [如何打造轻量级 WebIDE - 知乎](https://zhuanlan.zhihu.com/p/471476313)

- https://github.com/yuzai/base-editor /MIT/202210/ts/inactive
  - https://blog.maxiaobo.com.cn/base-editor/build/index.html

- 之前在团队中基于 theia，搭建了一套 CloudIDE 平台，其本质是将 IDE 的前端运行在浏览器 or 本地 electron，而文件系统，多语言服务等，运行在远端容器侧，中间通过 rpc 进行通信从而完成整个 IDE 的云端化。
- 而目前团队在低代码平台的建设中，发现还是需要一些简单的 IDE 场景，如果采用容器化的方案，那么每一个 IDE 可能就需要一个容器，不论是启动速度，还是资源的占用，都不太合适。
- 团队急需一款轻量级的 IDE 来嵌入低代码平台中，故近期着手开发了一款基于 monaco-editor 的轻量级且不依赖后端容器的 IDE。

- 对于依赖容器化技术，能够提供完整终端能力的 IDE，在本文中，称之为 CloudIDE，而仅仅依赖浏览器能力的 IDE，本文称之为 WebIDE。本文想要分享的 IDE 属于后者。

- 预览沙箱 这一部分由于公司内有基于 codesandbox 的沙箱方案，故实际在公司内部落地时，本文所述的 WebIDE 仅仅作为一个代码编辑与展示的方案，实际预览时走的是基于 codesandbox 的沙箱渲染方案。
  - 除此之外，得益于浏览器对 modules 的天然支持，也尝试过不打包，直接借助浏览器的 modules 支持，通过 service worker 中对 jsx, less文件处理后做预览的方案。该方案应对简单场景可以直接使用，但是实际场景中，存在对 node_modules 的文件需要特殊处理的情况，没有做更深入的尝试。

- 整体来讲，monaco-editor 本身的能力比较完善，借助其基础 api 再加上适当的 ui 代码，可以非常快速的构建出一款可用的 WebIDE。但是要做好，并不是那么容易。
  - 本文在介绍了相关 api 的基础上，对多文件的细节处理、ESLint 浏览器化方案、Prettier 与 monaco 的贴合及代码补全的支持上做了更为详细的介绍。希望能够对有同样需求的同学起到帮助的作用。

## more-blogs

- [theiaide - 博客园](https://www.cnblogs.com/theia-ide)
  - [Theia 事件 - theiaide - 博客园](https://www.cnblogs.com/theia-ide/p/16532995.html)
# docs

# more
