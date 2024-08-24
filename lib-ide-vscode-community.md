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

- ## 

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
