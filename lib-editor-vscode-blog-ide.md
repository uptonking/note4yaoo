---
title: lib-editor-vscode-blog-ide
tags: [blog, ide, vscode]
created: 2024-05-09T09:39:24.099Z
modified: 2024-05-09T09:39:33.338Z
---

# lib-editor-vscode-blog-ide

# guide

# ide-products
- [关于IDE，你想知道的都在这! 文章合集 - 掘金 _202303](https://juejin.cn/post/7209472157502668860)

## ide/cde

- https://github.com/styfle/awesome-online-ide
  - An "Online IDE" has the features mentioned above but runs in a web browser instead of installing as a native application.
  - AWS Cloud9, codenvy, Theia

## [Theia - Cloud and Desktop IDE Platform](https://theia-ide.org/)

- Cloud & Desktop
- designed in a modular way to allow extenders and adopters to customize and extend every aspect.
- vendor-neutral and developed by a diverse community.
- provides language support via LSP and DAP. Further, it can host VS Code extensions and provides full terminal access.
# blogs-vendors

## 

## 

## [李亚飞: 我这 5 年技术创业对云端 IDE 的理解与预测 _202402](https://new.qq.com/rain/a/20240222A04Z3B00)

- IDE 是指本地集成开发环境，也就是包罗开发人员所需要的、与编写代码相关联的一系列环境及配置。 
  - 而云端 IDE 即是简单放在浏览器上，就可以直接运行的 IDE 环境。但云端 IDE 技术实现上有很多差异，针对场景不同，功能会有取舍考量。
- 2022 年底，随着 Gitpod 拿到 2500 万美金的 A 轮融资，整个市场进入了全新的元年，重新把云端 IDE 定义 CDE（Cloud Development Environment）

- 说到 CDE，我们必须从海外的市场开始讲起。
- Coder 是一个先从开源出发（code-server），允许开发者用 VSCode 连接到任一的远程服务器，进而演化出来完整的 CDE（coder）环境的发展模式。也是开发者生态经典的发育模式。
  - 其核心定位是为开发者提供云端的资源配置管理、复用，开发者仍然可以复用本地开发环境。目标画像是在实际开发工作场景的开发者。（PV 4.9 万，UV 2.4 万）
  - 值得讲一下，他们三个联创都特别年轻，现在才 20 出头，但已经创业 5 年了。在 2022 年宣布拿到了 3000 万美金。
- Gitpod 的定位也是为开发者提供生产力工具，替代本地开发。
  - 目前增长比较明显，很多开源项目的托管平台选择都有他们的影子。
  - 目标画像：在实际开发工作场景的开发者。（PV 67.3 万，UV 15 万）
  - 目前融资情况：Github 的创始人领投了最新一轮 2500 万美金。
- Glitch.com 仅支持 Web 类项目开发的 IDE 环境
  - 核心定位：练习 Node，React，Vue 等偏前端的 Web 项目。目标画像是泛开发者，学习成长的前端开发者。（PV 59.8 万，UV 32.5 万）
- Stackblitz 前身是 Facebook 的工程师出来创立的公司，与 Glitch 类似，仅 Web 类项目开发的 IDE 环境的核心定位有所不同，为实际企业内开发者所准备。
- CodeSandbox.io 相对来说是一个更加老牌一点的，功能全面的 CDE 平台，目前也是生产力方面流量最大的玩家。
  - 核心定位：早期 Glitch 很接近，现在采用 MicroVM 技术支持到 Web 类外全开发框架。
  - 目标画像：早期与 Glitch 类似，目前与 Gitpod 接近。
- CoderPad 2015 年成立，早期定位于技术面试，2021 年开始收购了 CodinGame，推出技术测评。
  - 公司规模不大，但发展良好。是一家特别优秀的产品驱动的企业
- CodeSignal 2014 年开始成立，早期叫 CodeFight，做代码竞赛，2017 年开始转入做技术面试与测评。
  - 目前发展良好。也是技术测评领域推出最早真实编程环境的公司。2022 年拿到 5000 万美金 C 轮融资。
- TestGorilla 印度出来的一家公司，这两年增长尤其快。岗位很全，100 多个岗位。支持软技能和 IT 技能测评。
- HackerRank 与 HackerEarth 这是两家同时具备 C 端与 B 端的技术测评公司，流量也是比较大。
- Replit.com 一直在快速迭代，定位于泛开发者（全领域）的用户体验良好的 IDE 环境 支持的范围很广：几乎所有的应用程序，主 Web 框架，采用 VNC 支 Android/iOS，3D 应用等。
  - 核心定位：泛开发者。Replit 覆盖人群巨大，流量在 2000 万左右，用户量也突破了 2000 万。目前估值 12 亿美金，融资额 8000 万美金。
  - Replit 的 IDE 满足两个核心，一是真正以实时互动协同为核心，二是打造了一套面向泛开发者（高体验）、类真实开发场景支持丰富的轻协同 IDE，并且有一定程度的外围开发者体验兼容的能力。
  - 然后基于这个基础构建一个爱好者生态，UGC 内容生成，这是比较独特的体验。导致其增长快的底层原因。

- 国内的玩家主要还是大厂。
- OpenSumi（阿里）自研，兼容 VSCode，是由内部研发效能团队自主研发，拥有自主的技术栈体系。其主要需求场景来自支付宝小程序。
  - 团队继续推出了 Codeblitz，轻量级前端化容器（Browser VM 技术），提升了加载环境的速度，但限制就在于只支持 Web 类。
- Cloud Studio（腾讯）基于 VSCode Web 开源系统进行改进。原创业公司 Coding 的产品，后整合进腾讯云体系。
- CodeArts（华为）10s 启动，基于 VSCode Web 系统进行改进。2022 年发声是很好的，但 2023 年 3 月后没有看到太多更新动作。
- 大厂研发这类产品，本质上都是内部研发人员已经够多，需要有一些 CDE 需求的场景，例如小程序开发、代码 review、代码 diff 等，云上开发当然也很好，但整体来看国内的技术能力还没有能打造出匹配美国像 Gitpod、CodesandBox 这种实力的产品。
- 国内创业公司还有像 Lightly（TeamCode）、TitanIDE（行云创新）等探索者，也有各自一些特点。

- 技术实现侧分析
- 技术实现上大致分了几种情况，一个是 VM 技术的区别、一个是基础用的是否是 VSCode Web 开源改进。
- Coder 的重点在于取代或提升开发者本地开发环境，所以形成一套重云 IDE，与本地 IDE 形成竞争。
- CodesandBox 主打快速启动，早期仅支持 Web 项目构建（采用 Browser VM 技术），现在转向 MicroVM。
- Stackblitz 2017 年，源自 Facebook，采用 Browser VM 技术，支持大前端项目。
- Glitch 采用 Browser VM 技术，目前专注于 Node 大前端类项目。
- Gitpod 一开始就采用 VM 技术，定位于开发者生产力。
- Replit 完全自研的 CDE 环境，全视图可定制，也融合了更多 AI 技术。
- 几乎 70% 的玩家直接选择了 VSCode Web 开源改进，运行内核部分采用 Browser VM 技术，大多采用 VM 技术，CodesandBox 则是从 Browser VM 过滤到了 MicroVM 技术（这是一个由亚马逊工程师贡献的一套轻量级虚拟化容器技术）。

- 目前主要有三大类 CDE 的应用场景是主要战场：
  - 第一类是生产力工具，直接帮助专业的开发者提高研发效率。代表产品是 Gitpod 和 CodesandBox，Gitpod 最新的融资情况是 2022 年底，2500 万美元，估值 8 亿人民币，根据活跃数据，开发者几十万。CodesandBox 听闻也在 2022 年底拿到了更多融资但没有公布。目前活跃数据比 Gitpod 高 2 倍左右。同时他们在 CDE 的核心技术上都有明显的突破点。
  - 第二类是开发者能力测评，帮助企业识别技术人才的能力。这里面又分为带有 C 端支持的，和专业为 B 端服务的。前者的代表是 HackerRank 和 HackerEarth，HackerRank 在 2022 年拿了 D 轮 7000 万美元，实际活跃开发者用户预测在 100 万。HackerEarth 也融到了 1000 万美元，用户量折半。后者专注于 B 端，像 CodeSignal、CoderPad、CoderByte、Codility，目前大家的节奏和情况还是蛮类似的，市场竞争比较激烈。这里面技术上有明显突破的是 CodeSignal，它是第一家提出真实开发环境的公司，其他几家都正在跟进。
  - 第三类是面向泛开发者，或者说是由兴趣驱动的编程爱好者，其中 Replit 是其中最优秀的代表，目前活跃用户突破 1000 万，这个规模在编程垂直领域很难想像。也在 2022 年拿到了 8000 万美元的融资，估值超过 12 亿美元。下一步的关键点是在商业化的发力上。

- 综上，CDE 云端协同式编程环境给生产力革新、技能测评、编程学习提供了全新的用户体验，拥有的发展空间很大。
- 但中国环境大不一样，市场的成熟度，用户的习惯都有较大的区别。国内原 Coding 的创始人张海龙，华为的 CodeArt 负责人王亚伟也都有互联网上发表了一些自己深度的看法。
- 所以结论比较明显，除非程序员的平均工资被打回正常位置，否则编程的需求会一直变多。

- 总结来看需要以下几个能力要极大的突破就有可能创建出成功的产品：
  - 冷启动要足够快
  - 编程体验接近本地
  - 创建全新的体验，深度集成 CI/CD，Code Review 在线化，协同能力
  - 资源成本足够低

- CDE 是一个极其技术密度的工程复杂度很高的项目。注定了它的发展周期比想像的要长不少，比如上述提到的技术测评产品大多在 2012-2013 年成立，像 Replit 也是 2013 年成立。只有深刻思考上述问题并提出更优解决方案，才有可能做出成功的产品
  - 首先，我这十年的创业经历告诉我，核心能力一定自主可控，所以从一开始，我们便立志自研完全属于自己全协同的云端 IDE（CDE），首先就是放弃了 VSCode 二次的思路，从零开始构建自己的云 IDE 引擎。
- 我们在 2021 年下半年开始组建自己的 CDE 研发团队，从以下几个关键点进行了架构设计：
  - PaaS 架构，提供 SDK，让应用层充分响应各种需求。极速冷启动，采用分布式 COW 存储架构，双阶段（ready_1 和 ready_2）分阶段加载代码和容器环境，启动进入理论极限：2S。甚至切换环境速度被优化的更快，平均只有 700ms。这超出了世界上最优秀的 CDE 的表现。
  - 全协同性，天然支持多人实时协同，不等同于传统 IDE 只能协同编辑区，我们还有文件树、终端、控制台、甚至浏览器均默认协同与共享，并特有视角跟随功能。
  - 可控的成本和低延迟设计，全自研可控的容器调控技术，容器随启随关不影响到用户使用，整体的成本与延迟要比同类低 50% 以上。
- 我非常同意前 Coding 创始人张海龙的那句话：“机会很可能不是简单的把 IDE 上云，机会更可能来自全新的云端编程体验”。目前来看最可能的方式是 AI 原生的在线编程体验，提供 L3 甚至 L4 以上辅助编程能力，并且需要把 CI/CD、Review 等流程结合 AI 更好的协同起来，创造一个超出目前本地编程几倍的全新体验

## 🆚️ [Comparing Coder vs. Codespaces vs. GitPod vs. DevPod _202309](https://loft.sh/blog/comparing-coder-vs-codespaces-vs-gitpod-vs-devpod/)

- Coder promotes itself as a “Self-Hosted Remote Development Platform” which is open source and focuses on “shifting software development from local machines to the cloud”. 
  - You provision the underlying infrastructure with Terraform on Kubernetes, Docker or VMs, as required. 
  - This can be done locally or remotely in the cloud. 
  - Coder does not offer a hosted solution, so everything is self-hosted.

- Codespaces is a Software as a Service (SaaS) remote development environment that hosts Docker containers on Azure VM. 
  - the product is the only one in the list that is not open source and is tied to GitHub, with limited 3rd party source-code host integration.

- GitPod was launched as a SaaS product in 2019, making it one of the early startups in this space. 
  - GitPod operates with containers on Kubernetes cluster on Google Cloud, but they require a `gitpod.yml` file instead of the `devcontainer.json` to be present which is the standard.
  - It can be difficult to switch to other tools, such as Codespace, Coder, and DevPod, because they rely on the devcontainer.json file. 
  - This can result in vendor lock-in since you would also need to migrate the instructions in gitpod.yml.
  - Also, the important to note that GitPod does not offer GPU options, making it less ideal for AI/ML workloads.

- DevPod is one of the latest projects in the ecosystem, which is an open source alternative to GitHub codespaces. 
  - It is also based on the `devcontainer.json` standard, so you can easily move your projects from Codespaces to DevPod without the need for modification.
  - The main advantage of DevPod is that it supports client-side development with the DevPod CLI (there is also a lightweight GUI version). 
  - This allows you to use any git repositories, as DevPod simply checks out your repos using git with the backend of your choice through providers.
  - DevPod works with the provider concept which defines how your target environment needs to be set up anywhere else. 
  - By using DevPod providers, you can create your dev environments on various backends - including your local computer, a Kubernetes cluster, any accessible remote machine, or a virtual machine in the cloud.

- GitPod and Codespaces are SaaS services that offer 50 free hours and 30 free hours, respectively, on standard 4-core machines, which is quite appealing. However, as a developer commits more hours and scales up, it can become more expensive, being approximately two times the price of Azure Compute Pricing.
  - Alternatively, solutions like Coder and DevPod provide the flexibility to pay for cloud and take advantage of committed usage discounts when needed or use the local system for simplicity. The tools themselves are free which allows for a more cost-effective and practical approach to managing costs as well as isolation, both in the cloud and locally.

- Coder and DevPod, can be used for VMs/Docker/Cloud which brings more components under your control. 

- Ease of Usage
- Coder requires everyone to understand a bit of Terraform and templates, since that’s how the infrastructure is deployed.there’s no internal API for provisioning VMs, which can be challenging to deploy on infrastructure with no Terraform providers.
  - GitPod and Codespaces are user-friendly platforms that require only a sign-up process for easy access. However, it is important to be mindful of data sharing and compliance when using them, as an internet connection is always required.
  - DevPod operates on native APIs, making it easy to interact with new providers and requiring no internet connection if you’re in an air-gapped environment. If you’re using a cloud provider then of course you’ll need the connection. One added benefit is that the complete client-side nature simplifies the process of propagating user-level secrets to the system and allows for easy development and testing both locally and on the cloud.

- if you’re using DevPod or Codespaces, they are only compatible with Multi Devcontainers support for mono repos, which can be necessary for some software teams.

- Team collaboration is crucial, and having the right tools to support development is essential and Codespaces and DevPod are at the forefront of the industry with their production devcontainer.json support.

- Coder also has a way to support community-provided providers, but it has a limitation with Terraform.
- The success of DevPod is indeed not unexpected, given the track record of the team at Loft Labs and their previous involvement in the open-source community. 
  - Their prior projects, such as vCluster and DevSpace, have been highly successful and have contributed significantly to the developer ecosystem.

## [Thanks Microsoft for open-sourcing VS Code Server _202111](https://www.gitpod.io/blog/vscode-server)

- After Gitpod launched OpenVSCode Server in September, Microsoft now open-sourced the server code powering VS Code remote development and GitHub Codespaces
  - Within a few days we switched Gitpod VS Code and OpenVSCode Server Insiders builds to the upstream implementation

- OpenVSCode Server adds some much-needed, yet minimal changes on top of VS Code to:
  - enable the marketplace using Open VSX
  - enable HTTPS and WebSocket Secure (wss) by default

## ⌛️ [gitpod: From Theia to OpenVSCode Server - A history of Cloud IDEs - Blog _202110](https://www.gitpod.io/blog/cloud-ide-history)

- We learned the intricacies of different desktop IDEs (Eclipse, IntelliJ, VS Code) and web editors (Monaco, Ace, Orion, and CodeMirror) - and eventually ended up building Gitpod.
- While IDEs are an important building block, platforms such as Gitpod are so much more. Think orchestration, provisioning, operating system, databases, compilers and all other tools you require to be productive.
- Back in late 2017 VS Code could not run in a browser and was not (yet) refactored to support remote development. 
- Because we wanted to offer a VS Code-like developer experience in Gitpod, we started the open-source project `Theia` under the roof of the Eclipse Foundation. 
  - The idea was to use VS Code technology (i.e. Monaco editor, LSP, DAP protocols, Xterm.js) to implement a vendor-neutral, remote-first IDE framework accessible from both browser and desktop. 
  - The framework was widely adopted by companies such as Gitpod, Google, Ericsson, SAP, RedHat, ARM, Arduino, and several others. 
  - While we at Gitpod moved to VS Code in late 2020 (more on that below), today Theia powers online IDEs such as Eclipse Che, Stackblitz, Google Cloud Shell Editor, Acquia Cloud IDE and several others.

- From the start the number one feature request for Theia was to support VS Code extensions out of the box.
  - Building that required a steep learning curve as you need to understand the semantics behind all VS Code extensions APIs and port them to Theia. 
  - By early 2020, Theia was compatible with the most important APIs.
- To fill that gap we built and released the Open VSX marketplace as an open-source alternative, which we also donated to Eclipse. 
  - Today OpenVSX has almost extension parity for the most popular VS Code extensions and is used by Gitpod, OpenVSCode Server, code-server, Eclipse Che and can be Self-Hosted on your own infrastructure.

- By 2020 the brilliant team behind VS Code added remote support and the web workbench ultimately powering github.dev was already open-sourced.
  - However, they decided to not open-source the server implementing the remote protocol. 
  - In summer 2020, while porting a new VS Code file system API in Theia, I began to understand how the internal remote protocols are working and decided to build a quick prototype for a server implementation of stock VS Code. 
  - After 4 days of focused work we had a first working version at the beginning of September. There were still many missing pieces (auto-sync settings, port forwarding etc.), but it became clear that we can run stock VS Code in Gitpod.

- Gitpod is an open-source orchestration and provisioning platform for developer environments. 
  - The goal was always to open Gitpod to all IDEs as soon as they support remote development
- I admit that it was a hard decision to stop supporting Theia after almost 4 years, but the maintenance and catch-up effort required to support the ever growing and changing API surface became increasingly a burden. 
  - And more importantly: Theia did not allow us to provide the best developer experience we could.
- We spent the next months polishing the server implementation and added missing pieces such as the setting sync server and port tunneling via the local companion app. 
  - In December 2020 we started giving users the choice between Theia and VS Code and officially switched to VS Code as the default editing experience in Gitpod in early 2021.
- our server implementation still was bound to Gitpod services. For example, we had a custom remote terminal implementation while MS open-sourced its pty service. 
  - After the requests became more and more frequent we decided to separate concerns and provide a clean-cut between the server and parts which we add to integrate with Gitpod. OpenVSCode Server was born.
  - Within several days we were joined by large companies such as GitLab, VMware, Uber, SAP, Sourcegraph, RStudio and SUSE. 
- By imposing constraints such as never changing Microsoft code, we enabled a straightforward, fully automated upgrade path
  - As the project’s scope is to keep the changes to upstream VS Code as minimal as possible we will not bloat the server, but (similar to upstream VS Code) use their extension model and external services to add missing functionality. 

- With Gitpod you can provision, automate and orchestrate those workloads for yourself and your team with the least friction possible. 

## [Gitpod is now Open Source - Blog _202008](https://www.gitpod.io/blog/opensource)

- Gitpod Self-Hosted is free for unlimited users. 
- Organisations using Gitpod Self-Hosted can purchase an enterprise license in order to get additional features like:
  - Snapshots (share a reproducible workspace with your team)
  - Live Share (invite others into your running workspace)
  - Unlimited Prebuilds (making ephemeral dev environments possible)
  - Admin Dashboard

## [A first look at the new GitLab Web IDE and remote development experience _202212](https://about.gitlab.com/blog/2022/12/15/get-ready-for-new-gitlab-web-ide/)

- A little while back I wrote about the future of the GitLab Web IDE and our decision to rebuild the Web IDE on top of the open source VS Code project
  - Today, I am happy to announce that we are preparing to launch the new Web IDE experience as a beta
- We're working on adding support for VS Code extensions and enabling project-wide search

- [The Future of the GitLab Web IDE _20205](https://about.gitlab.com/blog/2022/05/23/the-future-of-the-gitlab-web-ide/)
  - [Replace Web IDE with client-only VS Code (&7683) · Epics · GitLab.org · GitLab](https://gitlab.com/groups/gitlab-org/-/epics/7683)
    - Replace the current Web IDE, which is based on the open sourced Monaco editor, with a client-side instance of VS Code and implement custom extensions for creating commits and interacting with MRs.
# blogs

# more
