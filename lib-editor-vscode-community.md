---
title: lib-editor-vscode-community
tags: [community, editor, ide, vscode]
created: 2023-01-21T18:49:01.333Z
modified: 2023-01-21T18:53:04.519Z
---

# lib-editor-vscode-community

# guide

# discuss-stars
- ## 

- ## [Why VS Code should switch to CodeMirror for default text editing abilities _202105](https://github.com/microsoft/vscode/issues/123826)
- Our plan is to continue with the monaco editor and to improve the support for mobile, this will be significant less effort than to replace the entire editor implementation.

- ## 又读了一遍 matklad 的这篇文章，感觉很有意思： 为什么 LSP 成功了？
- https://twitter.com/roifex/status/1747340928090877966
  - 因为微软成功把 GitHub，VScode，TypeScript，LSP，webdev，RemoteDev 牢牢绑定在了一起；其中核心是 TS 和 VScode
- 但我觉得JetBrain的语义分析和IDE功能做的明显比vscode好，而TS的性能是真的不行。所以长远来看，vscode的LSP只是一种穷人的IDE，最后估计还是JetBrain会赢。
  - 只需要做到功能相近就足以让大家选 vsc 了，而且 JB 现在还没搞定远程编辑的问题…
- Fleet 的远程开发体验特别好。高延迟下效果比idea好很多，而且plugin不需额外开发就支持远程
- WebStorm next 重写了 Typescript engine。

# discuss-web
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
