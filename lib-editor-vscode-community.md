---
title: lib-editor-vscode-community
tags: [community, editor, ide, vscode]
created: 2023-01-21T18:49:01.333Z
modified: 2023-01-21T18:53:04.519Z
---

# lib-editor-vscode-community

# guide

# discuss
- ## 

- ## 

- ## 

- ## 💡 Most sandboxes in CodeSandbox are stored in a Postgres database.
- https://twitter.com/CompuIves/status/1667148424389566465
  - 40M+ sandboxes and 400M+ files stored in Postgres, and we still have performant load times.
  - When going with Postgres, I thought "this is the first thing we'll have to replace". Still didn't happen after 6 years
- Generally, the three technologies that exceeded my expectations in scale and performance:
  - Postgres
  - Elixir
  - Rust
- Now we're seeing that the database is growing very big (leading to long & big backups), so we started archiving sandboxes to GCP to save space. We're considering moving our DB from k8s to a managed instance. But still, Postgres has exceeded all my expectations.
- Curious, which components are written in Rust vs Elixir? Did you find that Elixir was better suited for some tasks than Rust?
  - Yah, Elixir is doing everything with the API (including websocket message handling).
  - Rust is doing computationally expensive things, or things that require a lot of string manipulation.
  - For example, we use Elixir to handle WS OT messages, but we use Rust then to apply the OT operations on the string. We first did this with Elixir, but (partly because of my implementation) it started to eat a lot of memory as every mutation created a new string.
  - Elixir + Rust interop is fantastic, so it's nice if you can pull out Rust for these kind of things while maintaining the concurrency/robustness of Elixir for the server.
- Erlang/Elixir under load is just amazing. Incredibly resilient. One of the many reasons I became a fanboy of CouchDB. Still love Postgres but there is something beautiful about storing everything in a giant B-tree

- 🤔 How is the Postgres DB structured.  Is it single node or shareded across multiple nodes?  And do you store files in Postgres as blobs?
  - Single DB (with a R/O replica). Files are stored as text, binary files are uploaded to GCP and we store a link in the db.
- Wow, just single DB for such huge workload!  Must be a huge machine.
  - It's not huge! 4 cores and 24GiB RAM (actually I believe 16GiB would be fine too). Plus we also store sandbox pageviews (hourly, daily, weekly, monthly)/users/teams etc...
- Incredible!  I am using a little bigger machine for a much lesser scale application.  Likely I am doing something wrong.
# discuss-web
- I think the only difference between them is http://vscode.dev supports azure devops repositories. http://github.dev only github ones.

- ## 

- ## 

- ## Google 的 Web 版 VSCode - Project IDX 今天开放了公众测试版，
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

# discuss-ide
- ## 

- ## 

- ## 

- ## [如何看待华为云 Cloud IDE 和 VSCode online 高度相似？ - 知乎](https://www.zhihu.com/question/383168806)
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

- ## [微软 VSCode 和 Eclipse Theia 是什么关系？ - 知乎](https://www.zhihu.com/question/383479657)
- VSCode和Theia用的都是Monaco editor。 
- Theia是在VSCode出来之后复用了很多VSCode的轮子和接口，主要是为了给第三方开放工具提供一个更便于开发的环境。
- Theia复现了VSCode的插件API，这样**VSCode的插件也可以被安装到Theia上**，但是因为这个API的支持不是很彻底，导致很多插件运行起来有点问题。

# discuss-random
- ## 

- ## 

- ## 

- ## [微软研发并开源 vscode 的动力是什么？ - 知乎](https://www.zhihu.com/question/519996636/answers/updated)
- 有利于巩固Windows生态。
  - 借助vscode的remote插件，可以非常方便地开发、调试Linux程序！
  - 原理就是，Windows上跑vscode的UI，wsl或者虚拟机里跑linux代码。

- 我觉得是为了建立云生态，推广 Azure

- reputation

- ## [微软为何要开源并维护 VS Code？ - 知乎](https://www.zhihu.com/question/271868289/answers/updated)

- 微软自身很赚钱，并不依靠Visual Studio Code 这一款产品养活开发团队。
  - 微软强调的是如何影响开发者，让更多的开发者来微软的平台(并不是指狭义上的平台也就是Windows，还有云平台啊，游戏平台啊，物联网平台啊)上开发更棒的软件。
  - 之前是为了繁荣Windows生态，现在是为了Azure生态。

- 到了微软这种规模的企业，利润计算不是看单个产品有没有利润
  - 这些巨头的利润来自于行业地位，地位越接近垄断，利润越大
  - 所以越是巨头越容易在单个项目上赔本赚吆喝
  - 搞开源，弄免费字体，扶持中小企业和个人，都属于这一类
  - 维护行业地位，保持知名度，这样才能整体而言有更大的利润

- Microsoft 开源 VS Code 本质上跟 Google 开源 Chromium 一样。
  - 首先，这个产品竞争的是免费市场，不可能直接从用户手上赚钱，只能通过影响力从别处把钱赚回来。chrome通过广告
  - 其次，开源不代表帮助了竞争对手。绝大多数人不会去读，绝大多数人甚至无法配置好编译环境本地编译
  - 最后，开源能换个好的口碑

- 重要原因1：微软从Linux服务器直接获利开始超过100亿美元量级
  - Azure大部分是Linux服务器，带来超过100亿美元的年收入。
  - . NET Core也借此支持Linux，实现了官方跨平台。
  - VS Code填补了工具链重要的一环，间接可以促进这部分收入。
- 重要原因2：微软在免费开发工具占位，增强外势和品牌地位
  - 大部分VS Code在Windows上运行，可稳固Windows的地位。

- 对我来说 vscode 最好用的功能，remote dev 是闭源的。
  - 当然你可以扒压缩混淆过后的 js 源码。

- 之前微软没有做 pylance 的时候，py 最好用的一个语言服务器是收费的。
- vscode copilot 也是收费的。
- 平台免费其实不影响收入。
- ssh插件闭源，pylance闭源，c#插件闭源，这和jetbrain家社区版开源有什么大的区别吗？

- VS Code 这个项目最初是Erich Gamma 开始做的。三十年前人家写过《设计模式》是设计模式四人帮之一。他后来更著名的是Eclipse Foundation 的核心成员
