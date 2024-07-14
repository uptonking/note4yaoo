---
title: lib-editor-vscode-community-ide
tags: [ide, pm, vscode, xp]
created: 2021-06-02T17:28:01.491Z
modified: 2024-05-09T09:35:28.467Z
---

# lib-editor-vscode-community-ide

# guide

- cloud-ide
  - monaco: Codespaces(GitHub绑定), 💡 Gitpod(yml/不支持私有部署), theia(华为CodeArts), OpenSumi/云凤蝶, 💡 StackBlitz, 💡 codesandbox-web
  - codemirror: sandpack, 💡 replit
  - Eclipse Che: OpenShift CDE
  - DevPod: devcontainer-spec + local-and-cloud
  - more: 💡Coder(no-cloud/k8s), AWS Cloud9, codenvy
  - 计算平台的演示场景: jupyter

- vscode-ide基础功能
  - 代码浏览: symbols, sticky-header
  - 编辑调试: LSP, DAP
  - 文件系统: local/remote
  - git版本控制: git-lens
  - 插件扩展: 语法高亮
  - remote repo/ssh
  - test
# draft
- 兼容现有浏览器的扩展
# xp-file-manager
- 难以直接将当前文件移动到父目录
# xp-editor

# discuss-stars
- ## 

- ## 

- ## 👣 Since git is trending again, what does your ideal VCS tool look like?
- https://x.com/LewisCTech/status/1802581515391647750
  - I'd like a git minus minus. No staging area, no editing the history. Also purely whitelist/blacklist based, no manually adding files to the repo like a peasant.
  - And of course a  CLI that made sense. Consistent use of commands, --, - etc.

- There are at least two (Git-compatible) VCS's without a staging area: https://github.com/martinvonz/jj and https://gitless.com

- core interactive smart smartlog equivalent ( tui does not count)
- no staging
- support for use without branches
- scalable refs db
- native large file/ bin support that does not suck
- lazy and fast by default
- default sane “rebase all” with conflict reresultion 
- native pluggable review system integration
- native pluggable check runner integration
- native sane pluggable conflict resolutions with simple to add type plugins
- native monorepo support without 4 competing alternatives that are all broken in a different way
- native sdk that is used by all tooling instead of split between core and @libgit2
- use of sqlite as storage db everywhere for everything except blobs
- native commit identity separate from from the commit hash
- native file move and hunk move match overrides with native storage
- native api for ref log with sync access to force push history
- native permissions
- native branch/ protections and rules
- native differentiation between tracking and non tracking fork

- hg is git minus the staging area， you commit whatever is changed in your working directory, not whatever changes were git added
  - HG's immutable history is fantastic

- git, but where there's only one way to merge (no git rebase), and where merge always deletes the branch. No branches from branches. Instead, something like "little commits", kept on the server, but they're squashed when merged - basically creating one commit per merge.
# discuss-cloud-ide
- ## 

- ## 

- ## 

- ## [Show HN: Chunk – Code sandbox for back-end devs | Hacker News _202207](https://news.ycombinator.com/item?id=32267862)
- Chunk is an all in one web editor (think of the codesandbox experience) that allows you to write, deploy and run a piece of code in the cloud from a variety of triggers: HTTP, WebHook, manual or scheduled (cron).

- I really like yalls website design and UX; especially around scheduling the functions to run. I am working on the same problem in Python space at https://cdevframework.io, but I am building it first as a client side SDK. Mostly chose that way because I don't have much frontend skills! Impressive that you could getting this up and going so quickly!
  - I really like your client side SDK approach, giving users the ability to use their own IDE / tools is always a plus. (+ building a web IDE is a pain haha)

- How do you safely run untrusted user code?
  - In nodejs you can use the `vm` module. 
  - And for extra layers you can run node itself in a linux namespace aka container. Inside a VPS that has selinux. On a dedicated server with no LAN access besides the gateway. In a fireproof datacenter.

- If we were to support more runtimes, I think I'd go for Firecracker (https://github.com/firecracker-microvm/firecracker/) which is what AWS uses for lambdas

- How does this compare to glitch.com? As far as I can tell the only real difference is the support for scheduled jobs, but I feel like I'm probably missing something more fundamental. Maybe it's just trying to be better version? Looks cool none the less, will check it out!
  - Glitch is definitely the closest in terms of usage. We in fact used Glitch ourselves quite a lot. But even running the simplest piece of code on Glitch still requires you to write all the boilerplate code (e.g. setting up a node express HTTP server).
  - And of course, Glitch stops every instances after 5min of inactivity and it takes a solid 30sec to wake them up after.
  - Glitch is unbeatable in the frontend part. But we want to make the backend dev experience more seamless.

- ## 🤔 [Ask HN: Is anyone using cloud dev environments (e.g. Codespaces/Replit) at work? | Hacker News _202310](https://news.ycombinator.com/item?id=37934488)
- My company switched to 100% remote dev envs a couple years ago. 
  - When you cut a branch it spins up a VM and you can connect to it from VS Code (native or browser based) or just plain SSH. It works great. The lag is not noticeable at all. 
  - Dev envs are fully provisioned and up to date with all tooling and dependencies so you don't need to bother with managing any of it locally. 
  - Given a choice I don't think any dev at my company would go back.

- I have not used a full blown online environment. Except maybe VSCode remote using SSH. I repeatedly find anything that requires a network call somewhere in between a serious impediment(阻碍，障碍) disrupting the flow of development. Sometimes I find myself in slow laggy situations with `ssh` to the point I prefer Mobile Shell mosh. VSCode remote (or similar) via ssh obviously becomes painful.
  - Most cloud environments are also limited in terms of what you can do. e.g: issue `sudo` while running a process, attach to a process with a debugger.
  - Usually when these come development environment ready, it also hides away underlying details - i.e, I no longer know the command line etc to should I need to write infrastructure code/automation later on.
  - I guess there are domains where these are non-issues. But for a wide variety of my use-cases local development is going to be preferable, because by design there are limitations in the alternative.

- 👷🏻 I work on CodeSandbox, so that creates some bias. We've been working on our own CDE solution, though we've taken a different spin to improve speed and cost.
  - Our solution is based on Firecracker, which enables us to "pause" (& clone) a VM at any point in time and resume it later exactly where it left of, within 1.5s. This gives the benefit that you won't have to wait for your environment to spin up when you request one, or when you continue working on one after some inactivity
  - there's another benefit to that: we can now "preload" development environments. Whenever someone opens a pull request (even from local), we create a VM for it in the background. We run the dev server/LSPs/everything you need, and then pause the VM. Now whenever you want to review that pull request, we resume that environment and you can instantly review the code or check the dev server/preview like a deployment preview.
  - It also reduces cost. We can pause the VM after 5 minutes of inactivity, and when you come back, we'll resume it so it won't feel like the environment was closed at all.
  - It's kind of like your laptop, if you close it you don't expect it to shut down and boot the whole OS again when you open it. I've written more about how we do the pausing/cloning here

- We've started integrating Codespaces into our team's workflow. It's been a game-changer for onboarding new devs. No more "works on my machine" issues. The ability to jump into any project without the setup hassle is pretty sweet. We're still ironing out some kinks, but overall, I'm pretty bullish on it for professional use.

- Most of the CS classes at my university have moved on to an online Jupyter environment with VS Code preinstalled. It lets students spawn an environment with all the required software for their class preinstalled.

- We use remote dev VMs with VS Code connected via SSH. It works a treat for a small team working on microservices. You can work from any machine while everyone has their own user account. Sharing code is a breeze. It's easy to test APIs in development (no http tunneling). Deploying to a local (on the VM) docker host for longer running services in test works well and it's super cheap to run.

- I'll repost here a comment I made on another HN post about cloud dev environments and why I will never be convinced to use them.
  - > I have never in my career seen a good implementation of cloud development. At every company I've ever worked for, "cloud development" is nothing but a Linux VM that gets provisioned for you in AWS, a file watcher that syncs your local files to the VM, and some extra CLI tools to run builds and tests on the VM. And every time I've used this, the overhead of verifying the syncing is up to date, the environment is consistent between my laptop and VM is the same, all this other mess...every time I end up just abandoning "cloud dev" and doing things on my laptop. God forbid you change a file in your cloud VM and forget to sync in the reverse direction. Not only is local development more reliable, but it's also faster (no remote network hop in the critical path of building things).
- With VS Code remote SSH, there is no "local" you are always on the server so there is also no syncing. They do some tricks to make this seamless and perform and feel as if everything was local.
  - But what do you do when you need to work without internet access, or with limited internet access?

- It is interesting that in the comments on this thread I’m not seeing any mention of nix, which is arguably overlapping the topic at hand with the Venn diagram of “spinning up dev environments”.
  - I've heard some reports that Nix is very painful to get working with Python/ML stack - do you know if this is this still (ever?) the case?

- I thought CDEs were a pretty cool idea years ago until I discovered Nix and specifically "nix shells". 
  - Call me old school but if I can run my tooling locally I typically prefer that in most cases, and Nix does a stellar job of tracking everything deterministically, so sharing amongst the team works great too. 
  - So much so I think replit actually uses it under the hood for some of their environments iirc.

- We use DevPod to work in cloud dev environments in our AWS cloud. I hate it. DevPod brings its own SSH implementation that injects itself into your server and munges CRLF, making ssh sessions to your workspace fraught with difficulty except for basic command line applications. The only terminal that seems to work is the one built in to Visual Studio Code. Maybe Microsoft Windows Terminal also works, I dunno.

- Codespaces user here (I set it up for the teams), for about the last 1.5 years in a large corp setting with teams using it.
  - My experience with is it has been wonderful for getting started and immediatly becoming productive with very complex systems. Most of those systems have 1 (or very few) experts who need to help everyone else with their setups. When problems arise, and they often do, they've become the bottleneck and Codespaces removes that. Those experts can focus on keeping just that up globally versus locally for each individual.
  - Outside of that scenario, complex systems, I've experienced it to be overkill. The negatives that come along with using such systems haven't outweight the benefits.

- Daytona is the enterprise-grade GitHub Codespaces alternative for managing self-hosted, secure and standardized development environments.

- Do things like Wix, Weebly, Wordpress count as CDEs?
  - Nope - those are website builders.

- ## [Microsoft Dev Box | Hacker News _202205](https://news.ycombinator.com/item?id=31493458)
- Would this be a competitor to https://www.gitpod.io/ ?
  - It isn't a match, because this is a full Windows desktop running over Web streams/RDP.
  - It is a competitor to Citrix, VMWare and similar offerings.

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

- ## [Show HN: DevPod – Codespaces but Open Source, Client-Only, and Unopinionated | Hacker News _202305](https://news.ycombinator.com/item?id=35964590)
- DevPod is built on the devcontainer.json standard to create reproducible dev environments. 
- Compared to hosted services such as Github Codespaces, JetBrains Spaces, or Google Cloud Workstations, DevPod has the following advantages:
  - Open Source: DevPod is 100% open-source and extensible. A provider doesn’t exist? Just create your own.
  - Client-only: No need to install a server backend. DevPod runs solely on your computer.
  - Cross IDE support: VS Code and the full JetBrains suite is supported. Other IDEs can be connected through ssh.
  - Rich feature set: DevPod already supports prebuilds, auto inactivity shutdown, git & docker credentials sync, with many more features to come.

- Port-forwarding and using your local IDE is already working in DevPod today. We also added auto-port-forward where it watches what happens inside the container and then starts port-forwarding automagically.

- File sync: That is a great idea. We got that in DevSpace already as you mentioned and we definitely think this could be super valuable in DevPod as well. Right now, a git push and then pull is required to get things from inside DevPod updated on local but with sync this would be even easier and faster.

- I enjoyed using gitpod a few times, this seems similar. How do they compare?
- There are 3 main differences: 
  - 1) DevPod is based on GitHub/Microsoft's devcontainer.json standard while GitPod has their own file format 
  - 2) DevPod is client-only more like Terraform where the client creates/manages things directly using cloud credentials vs GitPod is a server-side solution to manage and provision dev workspaces 
  - 3) DevPod has a provider concept similar to Terraform that allows you to provision dev environments in ANY infra vs GitPod is mostly a hosted solution (they do have the option to host it yourself as well but it's usually you install it to one cloud and then provision in that same cloud vs DevPod is 1 client (no server, see point 2) and then you deploy the dev env in ANY cloud or even locally in Docker or local k8s)

- ## [Ending support for self-hosted Gitpod and moving our source to AGPL | Hacker News _202212](https://news.ycombinator.com/item?id=33907897)
- CEO from Gitpod here. Some background on why we moved to a managed enterprise cloud product: there are parts of Gitpod itself that are closer to a Kubelet then a Kubernetes application. We use much of the Kubernetes surface, interact with containerd, and use bleeding edge Linux features. The only way you make Cloud and Self Hosted co-exist is to have one codebase. What we deployed in SaaS we wanted to deploy in Self-Hosted. But not all Kubernetes are created equal (think GKE node label, EKS custom AMI to get Linux kernels but not other places). Today there are features in SaaS that are not available in Self-Hosted. 

- Open source without self hosting capability is just crowdsourcing your engineering team. The cloud is a prison.

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

- ## [被逼出来的自主可控，从华为自研看国产IDE的未来和商业模式 _202302](https://www.infoq.cn/article/d4613NRodWJEAXqRblEu)
- 时间来到了 2019 年 5 月，由于众所周知的原因，华为内部研发工具需要进行大面积的自研，以保障研发作业的安全性。
  - 面对巨大的生存风险，我们做出了艰难但正确的战略决策：自研 IDE 内核。
  - 到 2021 年底，我们基本实现了内部嵌入式软件开发领域 C/C++ IDE 工具的自研替换，部分能力甚至实现了对原有商业工具的超越。
- 解决自身生存问题的同时，我们也在积极地进行商业化探索。华为云软件开发生产线 CodeArts 就是华为软件研发能力外溢的第一次成功尝试。
- 2019 年 5 月，我们开始做 WebIDE 服务（本文 WebIDE 指代所有在浏览器当中完成编码调试测试的 IDE 产品形态包括后端部署在云端虚机、容器中的 Cloud IDE），当时目标的细分场景是云原生应用快速开发和部署。
  - 2020 年 HDC（华为云开发者大会），我们推出了与华为鲲鹏芯片协同的云端开发环境“华为云 CloudIDE”，成为鲲鹏原生应用开发的首选平台，用户反馈正面。
  - 随着应用现代化、云原生的发展，云端开发场景越来越丰富，CloudIDE 再次被推到舞台中央，这次主打轻量级云原生应用开发部署。我们开发了大量打通云服务开发、调试和部署的插件，并于 2021 年推出了 ToB 的云原生应用集群调试服务 CloudDebugger 和面向云资源租户的 CloudShell 服务
- 单纯从一个效率工具的角度看， WebIDE 的还是有一些明显的痛点：
  - 首先是性能，托管服务的资源规格相对固定，算力可能不如本地环境强大；
  - 其次是灵活性，由于安全合规的要求，云端环境通常不能随意安装组件；
  - 再次是安全感，WebIDE 实例随时创建随时销毁，让开发者担心开发较大项目时数据会丢失。
  - 最后是使用习惯，在浏览器中进行开发作业需要适应，网络连接也要足够稳定。
- 鉴于这些明显的痛点，我认为下一代 IDE 的主流产品形态应该还是类似传统桌面 IDE，但内涵更广泛。
- 具体来说，下一代 IDE 除了具备传统桌面 IDE 的主要特征外还应该具备以下特征：
  - 第一，智能化全面融入编码、浏览、调试、搜索等各个开发环节。
  - 第二，随时创建并连接到短暂的、可扩展的远程异构环境。
  - 第三，技术上同时兼容 WebIDE 和桌面 IDE 两种使用方式。

    - 技术上实现一个 IDE 支持两种模式（服务器和桌面模式）已经成为可能。这种架构可以给开发者提供足够的灵活度，彻底解耦编码和编译构建调试环境

  - 第四，丰富的插件生态、多语言支持和扩展的能力。

    - Visual Studio Code 插件已然成为事实的标准，下一代 IDE 只要能兼容该标准就能迅速获取海量插件。
    - 云原生应用的微服务、容器化、分布式架构等特征也带来了多样化技术栈和多编程语言支持的需求。

- IDE 的核心技术是什么
- 以 Visual Studio Code 为代表的代码编辑器即使搭配语言插件也并不等同于传统桌面 IDE。
  - 代码编辑器以文本编辑为中心，以文件和目录为访问对象，而传统桌面 IDE 以代码编辑为中心，以项目为访问对象，二者有本质区别。
  - IDE作为一个效率工具最核心的部分是代码模型的处理引擎，其处理代码的性能，内存占用，索引大小，API 好坏直接决定了上层特性如语法高亮、浏览、补全、重构、检查等的易用性和整个 IDE 的体验是否“丝滑流畅”。
- 一个完整的代码模型处理引擎至少包括如下四个子系统：
- 一、项目模型（Project Model）。
  - 该子系统主要负责构建项目结构的高级视图，并提供接口访问当前工作空间的项目及其依赖关系、代码在磁盘上的文件夹和文件如何组织的数据结构。
- 二、索引（Index）。
  - 每次打开项目，IDE 都要需要花费时间来解析和处理所有源代码，这种处理的中间结果就存储在索引子系统中。
  - 项目第一次打开将构建完整的索引，一旦索引构建完成，所有后续的项目加载只需要对增量改动进行索引。
  - 索引又分基于文本的索引和基于语义的索引。前者很好理解，创建索引的信息是基于文本的，它不依赖于任何特定于语言的语义。而基于语义的索引就比较复杂，它包含的语义信息可能涉及多个源文件。
- 三、语法（Syntax）。
  - 语法是编程语言的底层结构和规则。IDE 使用抽象语法树（AST）来理解编程语言的源代码，而 AST 的访问是高频操作，所以语法子系统的任务就是提供高效和方便的 AST 访问接口给 IDE 其他模块使用。
- 四、 语义（Semantics）。
  - 一般来说，AST 是一种低层的代码文件结构，用于表示特定的源文件，AST 节点通常不具备具体的类型信息。
  - 还有一类数据称之为符号（Symbol），从 IDE 角度看符号是一类更高层的数据结构，它是从多个源文件的 AST 或者二进制依赖包中生成的，代表的是 AST 节点跨文件的类型信息，它可以告诉你某个方法是否是构造函数，某个变量属于哪个类型申明。
  - 语义子系统会构造完整的符号表并把对应符号附着到 AST 节点上，使之成为具备类型信息的 AST（Typed AST）, 这个过程称为类型绑定（type binding）。而基于 Typed AST 回答上述“如何判断”的问题的过程称为名字解析（name resolution）。

- 下一代 IDE 的代码模型处理引擎是什么样的呢？这个问题我也没想清楚，但我们在探索一种基于统一架构的代码模型处理引擎，架构大致分为三层：
  - 语言解析层：语言相关，不同语言不同的解析逻辑；
  - 语法、语义适配层：语言无关通用接口；
  - 索引持久化层：语言无关，基于索引元数据的高性能存储系统。
  - 这样设计的好处是最大化重用各子系统，并且可以快速支持新编程语言。

- 最后我想聊聊 IDE 未来在我国市场的商业价值和产业机遇。去年（2022 年）是微软 Visual Studio 诞生 25 周年，从第一个版本 Visual Studio 97 到 Visual Studio 2022，其主要商业模式一直都是订阅或者许可售卖。Visual Studio 对于微软的商业价值是否只是销售收入？如果是，后来的代码编辑器 Visual Studio Code 是免费产品，它的商业价值又是什么？
- 微软于 2008 年左右开始做云，2014 年萨提亚成为微软 CEO 后，提出“移动为先、云为先”战略，并且彻底拥抱开源，“Windows is the air we breathe”被扔进历史的垃圾堆，随后. NET 开源，2016 年发布 VS Code 1.0 并开源，2018 年收购 GitHub，最终组成了软件开发工具（VS/VS Code）+ GitHub + Azure 的强大的开发者生态价值链，成为驱动微软营收持续增长的引擎。微软深谙“得开发者得天下”这个道理，在云这个战场开辟了一条新赛道：
  - 云服务供应商必须打通开源软件到云服务的价值链。
  - 软件开发工具（特别是 IDE 或类 IDE 产品）是这条商业和生态价值链的起点，云服务是终点。
  - 在转化率不变的前提下，工具的用户越多，生态入口越大，云的生态越繁荣。
- 我始终坚信：信创基础软件工具链对于我国高科技企业来说是一个巨大的产业机遇

- ## [Cloud IDE 是不是一个伪命题 _张海龙 _202301](https://www.infoq.cn/article/dtkgop7ilvontssfpwrc)
- 2022年11月初，GitPod 在 A 轮融资中获得 2500 万美元，以兑现 Cloud Development Environments 的承诺。
  - 一周后，GitHub 宣布 CodeSpaces 将面向所有 GitHub 用户开放，每周免费使用 60 小时。这让人感觉好像我们突然就发展到了“云端开发元年”。
- 国内 CODING 创始人张海龙在这个领域探索了八年，看过各式各样的产品，对 IDE 技术发展有着深刻的认识，通过这篇文章，他为我们讲述了 Cloud IDE 在发展中的迷茫与希望。

- 最开始做 CODING 的时候，我们想了一个 Slogan，“Coding Anytime Anywhere”。要实现这个梦想得有一个必不可少的工具那就是 WebIDE。
  - 我们从 2014 年底开始做 WebIDE，当时的想象到现在其实也不过时。
  - 当时做的最好的 WebIDE 叫做 Cloud 9，成立于 2010 年。我们当时做的也有部分借鉴了 Cloud 9。可惜的是，Cloud 9 在 2016 年卖给了亚马逊。
- 另外一家叫做 Koding，同样成立于旧金山，不过比 Cloud 9 晚了两年，成立于 2012 年
  - Koding 在探索了几年 WebIDE 的方向以后，彻底转型了。你现在去他们官网，你甚至会发现他们已经从 WebIDE 开发者变成了 WebIDE 的反对者。
- 目前全球范围内编码工具的主要供应商只有两个，微软的 VS 系列以及 JetBrains 的 IntelliJ 系列。微软开源了 VS Code，大量的 Cloud IDE 产品都是基于开源 VS Code 的魔改。有意思的是，这两家似乎对于 Cloud IDE 这个概念一直都是不感冒，迟迟没有动手
- 为什么这两家编程工具巨头都不搞 Cloud IDE 呢？这个问题困扰了我很久。冲动的创业者往往追求的是炫酷，而成熟的企业家追求的是实用。软件工程领域三大问题：开发效率，开发质量，可维护性。任何一个工具的成功必须解决这里的一个或者多个问题。
- 在我们 2015 年对于 WebIDE 的想象视频中，定义了一些场景，例如临时修 Bug，新入职的开发 On board 等等，其实都是很小的 corner case，这些场景占据整个开发场景的时间不到 1%。在这个 1% 里面解决问题能有多大价值呢？
  - 后来我们又尝试了很多场景，例如教育，培训，招聘。这些场景看起来都很性感，但真正深入其中你才发现 IDE 在垂直场景里其实是小问题。
  - 例如招聘，提供一个在线 IDE 让面试者现场编写代码看起来是一个很酷的应用，面试官可以可以跟面试者对着代码交流互动，实际上这个场景的绝大部分问题都可以通过腾讯会议解决，而真正作为生产力工具的 IDE 的核心能力，例如快速创建工程，代码提示，调试等等能力在这个场景下毫无作用。
  - 面试这个场景真正的痛点是简历来源，简历质量，以及考察的问题跟岗位的匹配度等等，所以你看很多做面试的到最后都去做题库，或者去做了猎头。
- 有一个产品叫做 Replit，从编写轻量级的片段式代码起家，Replit 已经吸引了超过 1000 万的用户。
  - Replit 说它是个 IDE，但作为一个专业开发者，你打开 Replit 的界面，你会感觉这个 IDE 简陋到惨不忍睹，要啥没啥。但为啥 Replit 能成功呢？因为它一开始就不是给专业开发者设计的产品。
  - 作为编程新手，Replit 给他很好的编码体验，啥都不用管，上来就可以写代码，并且支持几乎所有语言。有点像美图秀秀和 Photoshop 的关系。
  - 你去看 Replit 的宣传，它一直在强调“Learn”这个关键词，这就是定位。
- 微软收购 Github 以后做的一个跟云结合的大动作是 CodeSpace。你说 CodeSpace 算不算 Cloud IDE？
  - Github 这么大的用户量，事实上 CodeSpace 的用量也就一般。
  - 而且 CodeSpace 还可以对接桌面版的 VS Code，也就是 Web 形态的 IDE 并不是核心。
- 在这个领域探索了八年，看到各式各样的产品熙熙攘攘，来来往往，Cloud IDE 的故事必将继续，新事物的产生必定有很多没有结果的探索

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

- 为什么大家做 Cloud IDE 的时候都会基于 VSCode/类VSCode 这一套体系？
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

# discuss-showcase-ide
- ## 

- ## 

- ## 💫 `<AnimatedIDE />` has been achieved internally.
- https://x.com/delba_oliveira/status/1800211372078141623
  - 行级动画，非字符级动画

- ## 🚀 [必须正式介绍一下: deepin-IDE – 深度科技社区 _202309](https://www.deepin.org/zh/2023-9-4/)
- 深度科技（deepin） 有自己的 IDE 吗？ 为什么要做自己的 IDE
  - deepin-IDE 传承了 deepin “专注自研，贡献开源” 的技术基因，自研代码14万余行。
  - 当然，这一产品的快速发展，是站在了“开源”这个巨人的肩膀上，为了避免重复造轮子，采用了一些开源终端组件、功能组件，在此列出该产品汲取的开源成果，感谢开源社区
  - 在开发库方面，deepin 操作系统已经拥有了自己的 DTK（Development ToolKit）开发套件。DTK 具备4个核心模块、220+个类、2300+函数接口、11个辅助功能模块、10+个扩展接口模块，已经能够满足日常图形应用、业务应用、系统定制应用的开发需求。
  - 目前 deepin 操作系统上自研的浏览器、音乐、邮件等 40 余款原生应用全部使用 DTK 开发。
- deepin操作系统为了解决“一包多用”的问题，推出了“玲珑”软件包管理方案，彻底解决系统与应用、应用与应用之间因升级引起的兼容性问题。
- deepin-IDE 和 VSCode 有关联吗？
  - deepin-IDE根植于开源社区，它依赖于 scintilla 等开源组件，本身也使用了 GPLv3 协议开源，当然也要贡献开源。和其它的基础软件一样，IDE也需要多年的打造与完善，比如 VSCode 至今也发展了八年，所以开发 IDE 确实难度巨大。

- deepin-IDE除了包含IDE常用功能，如智能编辑器、高度可扩展的命令系统、工程管理、构建管理系统、插件系统等之外，还支持多种兼容协议、多种开发语言、代码版本管理集成、低开销的实时性能分析工具等。总体而言，IDE常见功能都在表里

- 支持主流版本控制系统Git、SVN。
# discuss-zed
- ## 

- ## 

- ## 

- ## [[linux] Vulkan ERROR_INITIALIZATION_FAILED _202402](https://github.com/zed-industries/zed/issues/8168)

- ## [run zed error on Ubuntu 24.04 : blade_graphics::hal::init Surface formats are incompatible _202405](https://github.com/zed-industries/zed/issues/11716)
- Update: this error is on WayLand Mode, switch to X11 , zed works!

# discuss
- ## 

- ## 

- ## 

- ## [Ask HN: Is anyone using a web IDE for most of their development work? | Hacker News _201504](https://news.ycombinator.com/item?id=9457973)
- The real benefit is not in the Web IDE per se, but the fact that your dev environment is accessible from anywhere. That is the killer feature. You don't have to setup your environment more than once if you have more than one computer; you can work even with a Chromebook/iPad, and it's easily shareable with your team.
  - The web IDE is great if you want to make quick edits (or want to collaborate in real-time) but in most other cases, native editors have it beat.

- There are 3 other reasons that I use a Web IDE now (started using Cloud9 about 9 months ago)
  - When doing client work it's much easier to show clients what you're working on at any time. Don't need to mess around with a staging server and uploading files + DB changes etc.
  - All client projects are in their own environment with their own config / env vars / DB. So say a client wants changes made 3 months down the line it's super easy to get the project back in the state it was then.
  - When learning new languages can just create a new project of that type and it has everything you need ready to go. 

- Founder of Codenvy. There are 400K projects built on Codenvy hundreds of on-prem cloud installations. When we look through the saas project types, about 60% are Java and the rest are scripted language types. 
  - Our on-prem customers are enterprise. So a lot of WebSphere, WebLogic, maven, ant, node, Oracle DB, SQL Server, Postgres.
- We also have about a dozen OEM customers that use Eclipse Che or its derivatives to create new embedded or hosted IDEs. SAP is adopting Eclipse Che at the core for building new business applications that have dev IDE built in. IBM is doing similar work with Orion on BlueMix. WSO2 is embedding cloud IDEs into their API management servers using Che.

- I use [codebox](https://github.com/CodeboxIDE/codebox) on a digital ocean droplet for nearly all my development. It's a simple-to-install node app, though it's not being actively developed from what I can tell so I'd really like to switch to a local install of cloud9.

- codenvy.com - because java. there is full java support, navigate, autocomplete, outline and even java debugger.
