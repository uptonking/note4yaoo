---
title: toc-saas-ide
tags: [ide, pm, toc]
created: 2020-08-18T09:18:24.127Z
modified: 2021-05-14T15:06:46.615Z
---

# toc-saas-ide

# ide-local

- vscode
- atom
- visual studio
- intellij idea
- eclipse
- geany
- jedit
- qt-creator
  - https://github.com/mervick/Qt-Creator-Darcula
- hbuilder

- https://github.com/eranif/codelite /GPL/202405/cpp
  - https://codelite.org/
  - A multi purpose IDE specialized in C/C++/Rust/Python/PHP and Node.js. Written in C++
# ide-cloud
- https://github.com/styfle/awesome-online-ide
  - https://styfle.dev/projects/awesome-online-ide
  - An "Online IDE" has the features mentioned above but runs in a web browser instead of installing as a native application.
  - AWS Cloud9, codenvy, Theia

- eclipse-theia-ide
  - https://theia-ide
  - VSCode和Theia用的都是Monaco editor
  - VSCode虽然也是开源的但是他对第三方的支持不是很好

- https://github.com/gitpod-io/gitpod /AGPLv3/202405/go/java/ts/不支持私有部署
  - https://www.gitpod.io/
  - The developer platform for on-demand cloud development environments to create software faster and more securely.
  - Run any language on a full Linux VM complete with terminals, GitHub and Git integration
  - 支持生态: gitlab
  - [Introducing Gitpod Enterprise - Blog _202212](https://www.gitpod.io/blog/introducing-gitpod-enterprise)
    - We no longer actively support self hosting Gitpod
    - We will move all of our source code to open-source AGPL and remove the proprietary Enterprise License from our source code.
    - The focus on Gitpod SaaS and Gitpod Enterprise enables us to ship improvements much faster
  - [Ending support for self-hosted Gitpod and moving our source to AGPL | Hacker News _202212](https://news.ycombinator.com/item?id=33907897)
    - Open source without self hosting capability is just crowdsourcing your engineering team. The cloud is a prison.

- https://github.com/coder/coder /AGPLv3/202405/go
  - https://coder.com/
  - Coder enables organizations to set up development environments in their public or private cloud infrastructure.
  - ⚖️ Coder/Coder is AGPL. Coder/Code-Server is MIT
  - Cloud development environments are defined with Terraform, connected through a secure high-speed Wireguard® tunnel, and are automatically shut down when not in use to save on costs.
  - Define cloud development environments in Terraform: EC2 VMs, Kubernetes Pods, Docker Containers, etc.
  - The most convenient way to try Coder is to install it on your local machine and experiment with provisioning cloud development environments using Docker (works on Linux, macOS, and Windows).

- https://github.com/loft-sh/devpod /MPLv2/202405/go
  - https://devpod.sh/
  - Codespaces but open-source, client-only and unopinionated: Works with any IDE and lets you use any cloud, kubernetes or just localhost docker.
  - DevPod is a client-only tool to create reproducible developer environments based on a devcontainer.json on any backend. 
  - Each developer environment runs in a container and is specified through a devcontainer.json. 
  - Through DevPod providers, these environments can be created on any backend, such as the local computer, a Kubernetes cluster, any reachable remote machine, or in a VM in the cloud.
  - DevPod reuses the open DevContainer standard (used by GitHub Codespaces and VSCode DevContainers) to create a consistent developer experience no matter what backend you want to use.
  - No vendor lock-in: Choose whatever cloud provider suits you best, be it the cheapest one or the most powerful, DevPod supports all cloud providers. 
  - Cross IDE support: VSCode and the full JetBrains suite is supported, all others can be connected through simple ssh.

- https://github.com/hocus-dev/hocus /Elastic/202308/ts/inactive
  - https://hocus.dev/
  - Hocus is a self-hosted application that spins up ready-to-code, disposable development environments on your own servers in seconds. 
  - It's a self-hosted alternative to Gitpod and GitHub Codespaces.
  - You define your dev environments as code and launch them instantly from your browser. 
  - Hocus integrates with any Git provider that uses the SSH protocol, like GitHub, GitLab, BitBucket, or Gitea. 
  - It prebuilds dev environments on every commit for all branches like a CI system, enabling your team members to start coding with fresh, fully configured dev environments right away.
  - [hocus: We replaced Firecracker with QEMU | Hacker News _202307](https://news.ycombinator.com/item?id=36666782)
  - [VScode in browser _202304](https://github.com/hocus-dev/hocus/issues/10)
    - We plan to add a code server integration in the future, but it's not high on our priority list. We would like to first address performance, reliability, and usability for large teams
  - [Happy to help to deploy Hocus in Kubernetes env _202305](https://github.com/hocus-dev/hocus/issues/68)
    - I have already deployed Hocus in a hacky way on my dev cluster. Of course, at the moment, Hocus isn't designed to work with k8s and I need to have a DinD side-car to be able to have something on my screen.
  - [Integration with Nix development environments _202304](https://github.com/hocus-dev/hocus/issues/7)
    - Hocus builds a new VM for your project based on what you specify in hocus.yml.
    - All VM's are built using plain dockerfiles. I see no problem with creating a nix base image as long as some assumptions Hocus makes are fullfilled
    - We're thinking of introducing per team/project buildkit builders. Instead of using docker we would use buildkit directly. Buildkit has support for mutiple frontends, especially for nix.

- https://github.com/eclipse-theia/theia /EPLv2/202405/ts
  - http://theia-ide.org/
  - Theia is a cloud & desktop IDE framework implemented in TypeScript.
  - Eclipse Theia is an extensible framework to develop full-fledged multi-language Cloud & Desktop IDE-like products with state-of-the-art web technologies.
  - Support VS Code Extension protocol

- https://github.com/c9/core /NonCommercial/201802/js/archived
  - https://c9.github.io/core/
  - https://c9.io/
  - [c9/core Wiki](https://github.com/c9/core/wiki)
  - This is the core repository for the Cloud9 v3 SDK. 
  - The SDK allows you to run a version of Cloud9 that allows you to develop plugins and create a custom IDE based on Cloud9.
  - 🍴 forks
  - https://github.com/nerusnayleinad/core
  - https://github.com/furidngrt/c9
  - https://github.com/BrianFlannery/c9core
  - https://github.com/lexavey/c9core
  - https://github.com/idec9/core
  - [Common Node.js APIs](https://cloud9-sdk.readme.io/docs/using-common-nodejs-apis)
    - Cloud9 is build on top of Node.js on the server. We experienced the benefits of using the same language on the server and on the client. 
    - After learning from the 1st and 2nd version of Cloud9, we decided to make our plugins client side only. 
  - [What does the future Cloud9 license look like? _201810](https://github.com/c9/core/issues/523)
    - similar c9 service also open source their core product like che, koding etc
    - che -> Is based on Theia -> so Monaco
    - koding -> They use Ace but promote the use of our own IDE
  - [Is this project dead? _201904](https://github.com/c9/core/issues/536)
    - there are already some decent open-source alternatives in active development, like Theia and Code-Server to name two
    - Has this project ever been open source? The applied license is not much for the spirit of "free as in beer" software.
    - i have moved away from cloud9 to Theia. I recommend everyone to do the same.
    - 💰 Cloud9 did start out as a GPL v3 project. A GPL version of Cloud 9 v2 lives on as Pylon. With version 3, the core license was changed to non-OSS to align with their business goals 
  - [How can i manage more than one workspaces C9, like c9.io/ did?](https://github.com/c9/core/issues/237)
    - use `-w /path/to/workspace` flag when launching the server
    - I run multiple instances on different ports. Awkward, but it works.
    - It turns out a single c9 server can be used for multiple workspaces after all. I guess it's not a new feature, just poorly documented so I only found out after poking a bit in the sources.
    - Ps. Consider also VS Code server instead of c9. Together with Taisun could be a golden combi!
  - https://github.com/pylonide/pylon /GPLv3/202307/js/inactive
    - Pylon IDE, a Cloud9 v2 descendant with some added extras 
    - Pylon is a web based integrated development environment built with Node.js as a backend and with a supercharged JavaScript/HTML5 frontend, licensed under GPL version 3. This project originates from Cloud9 v2 project.
    - High performance ACE text editor with bundled syntax highlighting to support a wide range of programming languages.
    - Additional plugin dockpanel view

- https://github.com/eclipse-che/che-theia /EPLv2/202303/ts/archived
  - Eclipse Che provides a default web IDE for the workspaces which is based on the Theia project. 
  - It’s a subtle different version than a plain Theia as there are functionalities that have been added based on the nature of the Eclipse Che workspaces. 
  - We are calling this version of Eclipse Theia for Che: Che-Theia.
  - So, Che-Theia is the default Che editor provided with developer workspaces created in Eclipse Che 7
  - Che-Theia contains additional extensions and plugins which have been added based on the nature of Eclipse Che workspaces and to provide the best IDE experience of Theia within Che.
- https://github.com/codenvy/codenvy /EPL/201802/java/inactive
  - Cloud workspaces for development teams. One-click Docker environments to create workspaces with production runtimes. 
  - Codenvy is customized using Eclipse Che including stacks, templates, commands, IDE extensions, server-side extensions plugins, assemblies, RESTful APIs, and editors.

- https://github.com/newsnowlabs/dockside /apache2/202401/perl/inactive
  - https://dockside.io/
  - Dockside is a tool for provisioning lightweight access-controlled IDEs, staging environments and sandboxes - aka devtainers - on local machine, self-hosted on-premises on bare metal or VM, or in the cloud.
  - By provisioning a devtainer for every fork and branch, Dockside allows collaborative software and product development teams to take lean and iterative development and testing to a highly parallelised extreme.
  - Powerful VS Code-compatible IDE.

- https://github.com/CodeboxIDE/codebox /4.1kStar/apache2/201504/js/inactive
  - https://www.codebox.io/
  - Codebox is a complete and modular Cloud IDE. It can run on any unix-like machine (Linux, Mac OS X). 
  - It is an open source component of codebox.io (Cloud IDE as a Service).
  - The IDE can run on your desktop (Linux or Mac), on your server or the cloud. 
  - Codebox is built with web technologies: node.js, javascript, html and less. The IDE possesses a very modular and extensible architecture, that allows you to build your own features with through add-ons. 
  - Codebox is the first open and modular IDE capable of running both on the Desktop and in the cloud (with offline support).
  - 🍴 forks
    - https://github.com/codespaces-io/akurath /apache2/201702/js
      - Cloude IDE Frontend for Codespaces
      - https://github.com/codespaces-io/codespaces /202102
      - Codespaces is a tool created by School of Devops to simplify your learning environment setup and offers an IDE with integrated workspace, editor, terminal and nodes.
  - [What happened to codebox? _201604](https://github.com/CodeboxIDE/codebox/issues/518)
    - They sold the assets to a commercial company, but have not been maintaining it. You may want to look at some other open source projects like Eclipse Che
    - Similar to service codebox c9.io; Compile the SDK for similar use as codebox c9/core
  - [Intent to Fork Codebox _201701](https://github.com/CodeboxIDE/codebox/issues/521)
    - 👷🏻 I (the original Codebox authors), no longer own the open and closed source IP related to Codebox. Codebox was sold ~2 years ago, because Samy and I wanted to focus on GitBook. 
    - since it's open-sourced under the fairly liberal Apache 2.0 license, you should be able to safely fork it.
    - I would recommend two alternatives: che, c9
    - Building a world-class IDE, business and open-source project, requires a champion/leader, @TylerJewell is a good leader, Codebox currently has no leader or champion which hinders it's success moving forward.

- https://github.com/koding/koding /AGPLv3/201710/go/coffeescript/inactive
  - https://www.koding.com/
  - Koding is a development platform that orchestrates your dev environment. 
  - Developers get everything they need to spin up full-stack, project-specific environments in seconds. Share them, update them, and manage infrastructure from a simple interface.

- https://github.com/wasdk/WebAssemblyStudio /MIT/201901/ts/inactive
  - http://webassembly.studio/
  - Run C, Rust, Wat, or AssemblyScript code as WebAssembly in the browser.

- https://github.com/Atheos/Atheos /202402/php/js
  - https://www.atheos.io/
  - Atheos is an updated and currently maintained fork of Codiad, a web-based IDE framework with a small footprint and minimal requirements. 
  - Atheos has been completely rewritten from the original Codiad project to utilize more modern tooling, cleaner code, and a wider arrange of features.
  - https://gitlab.com/xevidos/codiad /202003/inactive
    - This is the Telaaedifex team's custom version of Codiad. 
  - https://github.com/Codiad/Codiad /201906/js/php/inactive

- https://github.com/Coding/WebIDE /BSD/201808/inactive
  - https://github.com/coding/WebIDE-Frontend /BSD/201808/js
  - https://github.com/Coding/WebIDE-Backend /BSD/201712/java
  - WebIDE 现已全面升级为 Cloud Studio
  - webjar 项目，用于将 WebIDE 前端打包成 webjar

- https://github.com/facebookarchive/atom-in-orbit /BSD/201612/js/archived
  - The goal of this project is to produce a version of Atom that runs in Chrome from Atom's source that is as faithful to the desktop version as possible.
  - https://github.com/facebookarchive/nuclide /NuclideLic/201812/js/python
    - An open IDE for web and native mobile development, built on top of Atom
# playground-snippet
- https://github.com/netgusto/nodebook /ISC/202002/go/ts/inactive
  - Nodebook - Multi-Lang Web REPL + CLI Code runner
  - Useful to practice algorithms and datastructures for coding interviews.
  - If `--docker` is set on the command line, each of these environments will run inside a specific docker container. Otherwise, the local toolchains will be used.
  - Do not run the Web UI on a port open to public traffic! Doing so would allow remote code execution on your machine.

- https://github.com/SmartIDE/SmartIDE /GPLv3/202303/go/inactive
  - https://gitee.com/SmartIDE/SmartIDE
  - https://smartide.cn/
  - https://smartide.dev/
  - SmartIDE可以帮助你完成开发环境的一键搭建
  - 如果你熟悉命令行操作，那么么安装我们的cli，然后你只需要学会一个命令 smartide start 就可以在自己所需要的环境中，使用自己喜欢的开发工具进行编码和开发调试了，不再需要安装任何工具，SDK，调试器，编译器，环境变量等繁琐的操作
  - 如果不喜欢命令行操作，也可以使用 SmartIDE Server 通过网页完成全部操作。
  - 当前SmartIDE包括4个组件：
  - CLI: 一个简单易用的命令行工具，可以运行在Windows/MacOS/Linux上，开发者使用一个简单的指令 smartide start 即可一键搭建开发环境，直接打开环境内置的WebIDE开始进行编码和调试。
  - Server: 支持私有部署的开源容器化开发环境管理服务。Server版继承CLI的所有能力，但是提供网页化的操作，同时针对团队使用进行扩展和支持。
  - Marketplace: SmartIDE插件市场是 open-vsx.org 的一个fork，我们进行了汉化并提供中国本地部署和插件自动同步服务。企业也可以选择在内网部署 SmartIDE插件市场，为内部开发者提供安全可控的VSCode插件管理服务。
  - 开发者镜像和模版: 开发者镜像是一系列预先构建好的开发环境容器，我们提供7种开发语言的开发者镜像，并且同时托管在国内的阿里云和DockerHub，方便全球的开发者使用。

- https://github.com/gcodecloud/geekcode.cloud /NonOpen
  - https://geekcode.cloud/
  - Cloud IDE是基于云的集成开发环境。IDE主要工作是编写、运行、调试和打包代码。传统的方式是开发者在本地的电脑上设置IDE，但Cloud IDE 允许开发者使用浏览器设置云开发环境，在浏览器中完成开发程序。
  - 编译代码时热更新主机配置，提高CPU的数量、内存大小以提高编译速度。

- https://github.com/adarshaacharya/CodeTreats /MIT/202110/ts
  - In-browser IDE for running, collaborating, saving and sharing code snippets

- https://github.com/zhblue/hustoj /GPL/202405/js/php
  - http://www.hustoj.com/?cat=2
  - 开源OJ系统

- https://github.com/devarend/mina-playground
  - https://minaplayground.com/
  - Mina Playground, an innovative interactive learning platform that allows you to follow step-by-step tutorials, run zkApps and Smart Contracts directly in your browser
# ide-ai
- https://github.com/e2b-dev/e2b /apache2/202405/ts/python
  - https://e2b.dev/docs
  - Secure cloud runtime for AI apps & AI agents. Fully open-source
  - E2B Sandbox is a secure sandboxed cloud environment made for AI agents and AI apps. Sandboxes allow AI agents and apps to have long running cloud secure environments. 
  - The E2B sandbox can be connected to any LLM and any AI agent or app.
  - Cloud browsers
  - We have built a dedicated SDK for building custom code interpreters in your AI apps. It's build on top of E2B and our core E2B SDK.
  - sdk支持python、js、cli
  - [Show HN: We are building an open-source IDE powered by AI | Hacker News _202304](https://news.ycombinator.com/item?id=35440552)
# ide-paid
- sublime text
- ultra edit
# examples-ide
- https://github.com/withfig/autocomplete
  - https://fig.io/
  - IDE-style autocomplete for your existing terminal & shell
# discuss
- ## 
