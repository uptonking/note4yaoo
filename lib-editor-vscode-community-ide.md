---
title: lib-editor-vscode-community-ide
tags: [ide, pm, vscode, xp]
created: 2021-06-02T17:28:01.491Z
modified: 2024-05-09T09:35:28.467Z
---

# lib-editor-vscode-community-ide

# guide

- cloud-ide
  - monaco: Codespaces(GitHub绑定), Gitpod(yml), theia, OpenSumi, StackBlitz, codesandbox-web
  - codemirror: sandpack, replit
  - Eclipse Che: OpenShift CDE
  - DevPod: devcontainer-spec + local-and-cloud
  - more: Coder(no-cloud/k8s), AWS Cloud9, codenvy

- vscode-ide基础功能
  - 编辑调试相关: LSP, DAP
  - 代码浏览: symbols, sticky-header
  - git相关: git-lens
  - 文件系统
  - remote repo/ssh
  - test
  - 插件相关: 语法高亮
# draft
- 兼容现有浏览器的扩展
# xp-file-manager
- 难以直接将当前文件移动到父目录
# xp-editor

# discuss-stars
- ## 

- ## 

- ## 
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

- I thought CDEs were a pretty cool idea years ago until I discovered Nix and specifically "nix shells".

- We've started integrating Codespaces into our team's workflow. It's been a game-changer for onboarding new devs. No more "works on my machine" issues. The ability to jump into any project without the setup hassle is pretty sweet. We're still ironing out some kinks, but overall, I'm pretty bullish on it for professional use.

- Most of the CS classes at my university have moved on to an online Jupyter environment with VS Code preinstalled. It lets students spawn an environment with all the required software for their class preinstalled.

- We use remote dev VMs with VS Code connected via SSH. It works a treat for a small team working on microservices. You can work from any machine while everyone has their own user account. Sharing code is a breeze. It's easy to test APIs in development (no http tunneling). Deploying to a local (on the VM) docker host for longer running services in test works well and it's super cheap to run.

- I'll repost here a comment I made on another HN post about cloud dev environments and why I will never be convinced to use them.
  - > I have never in my career seen a good implementation of cloud development. At every company I've ever worked for, "cloud development" is nothing but a Linux VM that gets provisioned for you in AWS, a file watcher that syncs your local files to the VM, and some extra CLI tools to run builds and tests on the VM. And every time I've used this, the overhead of verifying the syncing is up to date, the environment is consistent between my laptop and VM is the same, all this other mess...every time I end up just abandoning "cloud dev" and doing things on my laptop. God forbid you change a file in your cloud VM and forget to sync in the reverse direction. Not only is local development more reliable, but it's also faster (no remote network hop in the critical path of building things).
- With VS Code remote SSH, there is no "local" you are always on the server so there is also no syncing. They do some tricks to make this seamless and perform and feel as if everything was local.
  - But what do you do when you need to work without internet access, or with limited internet access?

- It is interesting that in the comments on this thread I’m not seeing any mention of nix, which is arguably overlapping the topic at hand with the Venn diagram of “spinning up dev environments”.
  - I've heard some reports that Nix is very painful to get working with Python/ML stack - do you know if this is this still (ever?) the case?

- I thought CDEs were a pretty cool idea years ago until I discovered Nix and specifically "nix shells". Call me old school but if I can run my tooling locally I typically prefer that in most cases, and Nix does a stellar job of tracking everything deterministically, so sharing amongst the team works great too. So much so I think replit actually uses it under the hood for some of their environments iirc.

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

# discuss
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
