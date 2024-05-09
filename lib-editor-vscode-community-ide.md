---
title: lib-editor-vscode-community-ide
tags: [ide, pm, vscode, xp]
created: 2021-06-02T17:28:01.491Z
modified: 2024-05-09T09:35:28.467Z
---

# lib-editor-vscode-community-ide

# guide

# draft
- 兼容现有浏览器的扩展
# xp-file-manager
- 难以直接将当前文件移动到父目录
# xp-editor

# discuss-ide-ai

- ## 

- ## 

- ## 

- ## [AutoDev for VSCode 预览版：精准 AI 编程提示词与编辑器的完美融合 - 知乎 _20240506](https://zhuanlan.zhihu.com/p/696080970)
- 我们将 AutoDev for Intellij IDEA 平台的非凡开发者体验带到了 VSCode 平台。在 IDEA 版本中通过构建非常精准的提示词，以及与编辑器的完美融合， 以帮助开发者更好地编写代码。
- 在设计 IDEA 版本时，我们一直致力于避免使用聊天窗口，以提供更好的用户体验。在 VSCode 版本中，我们将这一理念继续发扬光大。
- 不断地重构我们的架构，以实现精准测试生成所需要的上下文件：
  - 输出准确的测试文件路径
  - 与编辑器的完美融合
  - 函数的相关代码类（输入和输出）表示
  - 基于依赖工具的测试框架分析
- 如下是基于上述的设计理念的 Prompt 示例：
  - 通过读取依赖文件，如build.gradle，我们能够准确地知道项目的依赖，以及测试框架的使用。
  - 通过对函数的上下文分析，我们能够准确地知道函数的输入和输出，以及函数的相关代码类。
  - 通过精准的上下文，可以有非常高的信心直接生成测试代码。

- 在当前的 VSCode 0.1.0 版本中，我们实现了以下的核心功能：
  - 自定义 AI 指令，即通过自定义 prompt 来实现自定义的 AI 指令。
  - 测试生成，即通过 AI 生成测试代码。
  - 注释生成，即通过 AI 生成注释。
  - 语义化搜索核心逻辑，尚未集成到功能中。
# discuss-cloud-ide
- ## 

- ## 

- ## 

- ## [How to code, build, and deploy from an iPad using Gitlab and Gitpod | Hacker News _202204](https://news.ycombinator.com/item?id=31060363)
- Gitpod is VSCode front running on the browser and the backend is in a Linux container on their cloud. 
  - They have a running script you can commit which lets you run any command while starting up or even specify your own docker (which inherit from theirs). 
  - This allows you to create dev environment for most common languages. This article also shows how to use Gitlab CI/CD on every push.
- Pros: No need for high end laptop/pc (Shared on 16cores). Free HTTPS exposing for every port on the machine. Docker included. Standardize you dev environment (including VSCode extensions). Amazing if you are handling multiple projects and context switch between them a a lot (K8s, Dockers, nodejs, React and more) or for education with no hassles.
- Cons: Not all VSCode extensions are supported, as some are proprietary. Only support Gitlab, Github, Bitbucket. Free tier limited with 50 hours/month

- The moment you want to do web development or create iOS apps you hit a wall. The form factor is great but the software is terrible for coding.
- It's a strange situation where, in order to code on an M1 iPad, you might end up phoning into a box either you own or in the cloud, and that box is likely much slower than the M1 is on a single-thread.

- I started using their product last year, but ended up coming back to VS Code + .devcontainers. 
  - I've found their configuration scheme (`.gitpod.yml`) confusing and lacking documentation. 
  - I couldn't get trivial stuff like Prebuilds to work correctly.

- I'm currently using my iPad as a VNC client for a headless Mac mini, it's pretty close to a laptop. But need to figure out how to get a better wifi connection from my home office to my bed room btw.
  - See https://Ghuntley.com/internet for ideas.

- So far the best solution I saw using a tablet for coding was connecting the tablet to a rapsberry pi and sing network over usb-c and doing the work in the Pi with ssh connection. Is jenk but it does work.

- GitPod uses vscode, and vscode uses monaco. Monaco is very mobile unfriendly.

- Gitpod is thin client for hipsters. Unlike Virtual Desktop Infrastructure which is all about unburdening system administrators at the expense of developer happiness. Cloud-based, reproducible developer environments like Gitpod are all about developer experience and sparking joy for software engineers.

- ## 🚀 [devpod: Codespaces but open-source, client-only, and unopinionated | Hacker News _202306](https://news.ycombinator.com/item?id=36407477)
- I'm glad this space is expanding. This is created by the authors of Loft.sh and Devspaces, both really great solutions to the most common problems of developing natively in a K8s cluster.
  - DevPod is basically Vagrant but with containers, which brings a ton of benefits over the former VM-centric design. You can maintain an entire team (or organization) with one immutable development environment, to get away from the constant toil of fixing random problems on random people's dev environments that happened because they changed something locally and don't have an immutable environment to restore.
  - The fact that it's self-hosted means you can take it anywhere (your laptop, GCloud, AWS, Azure, etc). Containers means you can save resources or scale it, reuse public containers and container ecosystem tools. Unopinionated means you aren't forced to use one IDE or platform. Open Source means you can read the source to figure out what's going on and hack in a solution if needed.

- DevPod is another implementation of the devcontainer spec, the most used one being the aforementioned devcontainer cli which vscode uses, or supplies, via its integration.

- 🆚️ What are some of the competitors in this space?
  - Gitpod, a SaaS competitor to Codespaces. 
  - Coder, which I guess is the more enterprisey self-hosted Codespaces alternative? 
  - This project, Devpod, seems to be a polished experience but not centralized like Coder.
  - I recently stumbled upon Recode, which looks like a more indie take on the problem.

- It's a lot older but I would say Vagrant intersects with this space https://github.com/hashicorp/vagrant
- Vagrant was fantastic pre-Docker and is still arguably more useful for certain cases, but I recall having issues running it last I tried. Based on the website, VirtualBox still lacks stable ARM64 support. Would "boxes" downloaded from the Vagrant cloud need to be built for ARM64 as well, or does it emulate?
  - It does not emulate. My org has been deprecating Vagrant ever since IT started issuing Apple Silicon as an option. Replacement is Docker Compose, or cloud VMs for software with heavy disk I/O.

- I've been using devenv for new projects. I like it so far. Some might find nix (which it requires) to be overkill, but I think that's underestimating how devilish of a problem it's solving.
  - devbox is a similar idea, but is more approachable for those who don't know nix.

- Bridge to K8s, CloudShell Editor, Cloud Code, Coder, DevSpace, Eclipse Che, Garden, GitPod, GitHub Codespaces, ksync, Kubectl-warp, Nocalhost, Okteto, Squash, Stern, Skaffold, Telepresence, Tilt

- Coder’s big difference is that it uses Terraform for provisioning, so it can do Docker/Kubernetes as well as VMs

- At CodeSandbox we're also working on this! Main focus of us is that we're running the environment in Firecracker microVMs, which allows us to snapshot and clone environments very quickly. 
  - This enables us to create a VM for every branch, which comes with the added advantage that every branch automatically has a snapshotted preview environment that can resume in ~2 seconds.

- DevBox is a full VM with everything installed. Codespaces is a container with a web or SSH interface.

- Toolbox is not a developer environment, but rather a tool to provide 'a toolbox' to a container host, like the older Atomic, or CoreOS releases that are immutable. Dsitrobox is close to toolbox, but also not similar in providing a coder setup.

- Looks like a nix-env clone, cool nonetheless

- What would you say are the main differences between devpod and DevSpace. Do they compliment each other? Should devpod at one time in the future displace DevSpace? Would love to get your view on that.
  - Yep, as we see it they compliment each other quite well. DevPod takes your workspace to the cloud and DevSpace let's you develop against your Kubernetes cluster - potentially the same one you used to start your workspace.
  - Internally we use both in our development setup, spinning up remote workspaces using DevPod, installing DevSpace and kind into the devcontainer, then using DevSpace to develop against the cluster. See the vcluster setup as an example

- ## [Ending support for self-hosted Gitpod and moving our source to AGPL | Hacker News _202212](https://news.ycombinator.com/item?id=33907897)
- CEO from Gitpod here. Some background on why we moved to a managed enterprise cloud product: there are parts of Gitpod itself that are closer to a Kubelet then a Kubernetes application. We use much of the Kubernetes surface, interact with containerd, and use bleeding edge Linux features. The only way you make Cloud and Self Hosted co-exist is to have one codebase. What we deployed in SaaS we wanted to deploy in Self-Hosted. But not all Kubernetes are created equal (think GKE node label, EKS custom AMI to get Linux kernels but not other places). Today there are features in SaaS that are not available in Self-Hosted. 

- Open source without self hosting capability is just crowdsourcing your engineering team. Documented and supported or bust. The cloud is a prison.

- Interested to see if they can successfully pivot to full SaaS. It seems like with the recent AWS announcement of CodeCatalyst and Github CodeSpaces (both of which are free with an additional easy to use paid model), Gitpod has been backed into a corner. I hope they do well, but the odds are stacked against them as the enterprise selling machines that are Amazon and Microsoft are incredibly difficult to fight as a startup. 
  - With Gitlab also apparently working on their version of CodeSpaces, it seems like maybe the best position for Gitpod is an acquisition (possibly by Atlassian).

- Still self hosted alternative https://coder.com and Eclipse Che https://www.eclipse.org/che/.

- Is there enough of a community around Gitpod for it to be supported that way?
  - Unfortunately no. It is stupidly complex to be able to contribute to Gitpod as the build tooling (werft) automation is only accessible to employees thus a community never formed. During my time there I tried to get this resolved and implement some form of automation around community contribution w/CLA but both of these problems went no-where/were not prioritised.

- i dont understand. gitpod self hosted is gone and source is agpl so can someone continue a fork of gitpod self hosted?
  - I think the point is that they no longer support self-hosting. You can still self-host it, since it's AGPL after all, but they probably won't help you nor document how to self-host. This effectively pushes enterprises from self-hosting to their new Dedicated offering.

- ## [Is there a simple self hosted alternative to Github Codespaces/Gitpod? : r/selfhosted _202302](https://www.reddit.com/r/selfhosted/comments/10z04tk/is_there_a_simple_self_hosted_alternative_to/)
- Yes, code-server allows you to develop remotely on a different machine which is what I'm looking for. The problem is with managing code-server and setting up full development environments. This is what Hocus aim's to solve - it will provision and manage code-server/jetbrains-gateway for you so you don't have to think about it. You install one app on your desktop and suddenly you get all the benefits of gitpod/github codespaces including prebuilds 
- Coder is nice but they unfortunately don't support prebuilds like Gitpod/Github Codespaces

- Gitlab also has a web ide. I am using it for code hosting, issue tracking, ci/CD and a docker registry. Code server might be the better ide, but I'm loving my gitlab for all it's features.

- ## 如果有哪位熟悉 web 前端开发的同学有兴趣，可以一起来做个这样的东西：就是集成一个类似 vscode 的源码显示，加一些交互调试的控制功能，再使用 vscode 一致的调试接口。
- https://twitter.com/cloudwu/status/1787723615720681846
  - 这样就可以直接打开浏览器调试 Ant Engine 开发的游戏了。当然也可以不只用在 Ant Engine 上，可以扩展到一切 Lua 开发的项目。
- 实现一个 DAP（Debug Adapter Protocol）就行了，找一个支持 dap 的前端，比如 vscode，不用写一行代码就能可视化调试你的游戏了
  - 已经实现了。我只是想把前端直接集成在引擎内。
  - Lua 调试器其实是集成在 app 内部的，对外暴露了若干调试接口。这部分 Ant Engine 已经很完善了。只需要一个调试器客户端使用这些接口，展示给程序员看：比如下断点、显示变量状态、输入一些交互指令，等等。目前已经可以和 vscode 对接调试。上面这个想法只是锦上添花做点好玩的东西，或许也更方便。

- 单步调试需要实现gdb那样的远程调试协议api，代码生成还需要适配devtools的source map规范，inspector的话也同样需要一套基于json的远程协议

- 阿里就有这个东西，我们自己的游戏引擎也是基于这个做的 OpenSumi

- ## 🆚️ [如何看待华为云 Cloud IDE 和 VSCode online 高度相似？ - 知乎](https://www.zhihu.com/question/383168806)
- 无论是vs code还是theia都开源了，那么只要遵守开源相关协议，就没关系

- 华为云CloudIDE 是基于 Eclipse Theia 开发，而不是 VS Code。
- Eclipse Theia 与 VS Code 相似的地方
  - Eclipse Theia 使用了 Monaco Editor
  - Eclipse Theia 支持 Language Server Protocol（LSP）
  - Eclipse Theia 支持 Debug Adapter Protocol（DAP）
  - Eclipse Theia 支持运行 VS Code 的插件（支持大部分的 VS Code 插件 API）

- 为什么大家做 Cloud IDE 的时候都会基于 VSCode/类 VSCode 这一套体系？
  - 因为 VS Code 丰富的生态（Monaco Editor、LSP、DAP 和插件生态）。

- ## 🆚️ [如何评价阿里 & 蚂蚁自研 IDE 研发框架 OpenSumi？ - 知乎](https://www.zhihu.com/question/519740662)
- 对比一下OpenSumi和Theia，最近都用过。
  - 一样的应用场景：给公司做IDE定制。
  - 一样的技术栈：依赖注入，react。
  - 一样可以兼容vscode插件。
  - 都可以扩展/插件/模块。
  - 都可以发布页面端和桌面端。
  - UI都和vscode一样，但是细节没有vscode好看流畅。
- OpenSumi多了一个web worker模式，可以纯前端运行。这个比较有吸引力。

- 如果你需要定制IDE的话，我建议是：尽量写vscode插件(vscode写插件真是太爽了)。然后把插件集成到OpenSumi或者Theia。当然了，兼容性需要踩很多坑。

- ## 🆚️ [微软 VSCode 和 Eclipse Theia 是什么关系？ - 知乎](https://www.zhihu.com/question/383479657)
- VSCode和Theia用的都是Monaco editor。 
- Theia是在VSCode出来之后复用了很多VSCode的轮子和接口，主要是为了给第三方开放工具提供一个更便于开发的环境。
- Theia复现了VSCode的插件API，这样**VSCode的插件也可以被安装到Theia上**，但是因为这个API的支持不是很彻底，导致很多插件运行起来有点问题。

# discuss-web-ide
- I think the only difference between them is http://vscode.dev supports azure devops repositories. http://github.dev only github ones.

- ## 

- ## 

- ## Google 的 Web 版 VSCode - Project IDX 今天开放了公众测试版， _202308
- https://twitter.com/indigo11/status/1694497731832951265
  - 快速感受了一下，界面几乎和 VSCode 一样，完全在浏览器中运行，
  - 集成了很多云端的 Runtime 环境，导入项目很方便
- 相比codespace有优势吗

- ## GH CodeSpaces = Backed by a VM, vscode.dev = backed by a virtual FS 
- https://twitter.com/orta/status/1431925117555257345
  - It's kinda like code sandbox vs the typescript playground

- ## VS Code is now live as a web app for good: https://vscode.dev._202110
- https://twitter.com/tomayac/status/1450861305108340738
  - It uses the File System Access API and the Async Clipboard API
