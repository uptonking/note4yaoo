---
title: lib-ide-vscode-community
tags: [community, editor, ide, vscode]
created: 2023-01-21T18:49:01.333Z
modified: 2024-08-24T16:15:47.613Z
---

# lib-ide-vscode-community

# guide

# discuss-stars
- ## 

- ## [Are there apps built on top of VSCode open source base? - Stack Overflow](https://stackoverflow.com/questions/68100375/are-there-apps-built-on-top-of-vscode-open-source-base)
  - VSCode has a very customizable UI with Activity Bar, Sidebar, Tabs, Status Bar etc
  - It is well maintained, works in different OSes and has automatic updates.
  - Even if we remove the code-editor part, there is a lot of work in that.
  - This makes me wonder if it is possible to write a totally different app (not a code editor) on top of VSCode. For example a Slack-like messaging app, an Obsidian-like knowledge base app, etc.

- One thing that VS Code gives you that Electron doesn't is a distribution model - the marketplace and how new versions of your app can be detected and downloaded automatically etc. This is a big deal.


- I think the disadvantages are that a very fancy UX may not be possible directly - but you have to "work around" by putting HTML within a Web View perhaps. 


- 
- 
- 
- 
- 

- ## [Vscode设置选项过多，是否反人类？ - 知乎](https://www.zhihu.com/question/646432493)
- VSCode 的设置项整体是基于 JSON 的，Ctrl+, 打开的图形化界面只是一层很薄的封装而已。我认为这实际上反而是很容易配置的。我其实是建议大多数时候不要依赖于图形化界面的配置，直接去改 settings.json
  - JetBrains IDE 的配置文件实际上是依赖于 XML 的, JetBrains 显然也知道 XML 反人类，所以全部配置项都是能够通过图形界面改的
- VS Code 是自身设置 + 扩展设置集中在一起了，扩展安装越多，要配置的也就越多。

- ## [Why VS Code should switch to CodeMirror for default text editing abilities _202105](https://github.com/microsoft/vscode/issues/123826)
- Our plan is to continue with the monaco editor and to improve the support for mobile, this will be significant less effort than to replace the entire editor implementation.

- ## 又读了一遍 matklad 的这篇文章，感觉很有意思： 为什么 LSP 成功了？
- https://twitter.com/roifex/status/1747340928090877966
  - 因为微软成功把 GitHub，VScode，TypeScript，LSP，webdev，RemoteDev 牢牢绑定在了一起；其中核心是 TS 和 VScode
- 但我觉得JetBrain的语义分析和IDE功能做的明显比vscode好，而TS的性能是真的不行。所以长远来看，vscode的LSP只是一种穷人的IDE，最后估计还是JetBrain会赢。
  - 只需要做到功能相近就足以让大家选 vsc 了，而且 JB 现在还没搞定远程编辑的问题…
- Fleet 的远程开发体验特别好。高延迟下效果比idea好很多，而且plugin不需额外开发就支持远程
- WebStorm next 重写了 Typescript engine。

# discuss-electron
- ## 

- ## 

- ## 
# discuss-news
- ## 

- ## 

- ## Visualize your repo's history... now directly built into @code
- https://x.com/code/status/1837540563710615757
- Turned this feature off because it made the entire git history tab insanely slow and unusable... If your history is rather large it's slow and distracting.

- there's an extension called "Git Graph"

- To all terminal users, I couldn't recommend lazygit enough. If you prefer not to leave your editor, there's also a plugin that integrates it directly into VS Code
# discuss-vscode-api
- ## 

- ## 

- ## 

- ## [Why Did Microsoft Build VSCode? Turns Out, GitHub Copilot | Hacker News _202306](https://news.ycombinator.com/item?id=36329370)
- AI chat API isn't public yet.
  - "In-editor chat" is mentioned as an example (the only example in the post, as far as I can tell) of a restricted API feature. i am curious as well as to what exactly is a "restricted API" and how MSFT prevents plugins to use it while allowing github copilot to use it.

- ## [Microsoft is introducing hidden APIs to VS Code only enabled for Copilot? | Hacker News _202410](https://news.ycombinator.com/item?id=41907350)
- I don’t see any problem here. They spend money, effort, time to develop their products. Why do they need to give that products for free to everyone, or even their competitors?

- I discovered that VSCode has a set of APIs for adding SSH tunneling, and under normal circumstances you must launch vscode with special flags to be able to use them. Somehow their built-in JavaScript debugging extension can use these APIs without any issues.
  - And you can hardly find any public information about these APIs. Well, unless someone asks -- As of 2 years ago, they didn't have any plans to "finalize" these APIs, i.e. make them public. You are advised to find other workarounds (which do work).

- Microsoft has been very clear about their business model of VSCode -- similar to Chromium, the base product is free and you can do whatever you want, but extension marketplace/remote/GitHub Copilot are proprietary.

- they have a number of "inline completion" APIs standardized as both VSCode APIs and LSP protocol (upcoming).
# discuss
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
