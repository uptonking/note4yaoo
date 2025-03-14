---
title: lib-saas-cms-community
tags: [cms, community, saas]
created: 2023-12-15T18:54:44.557Z
modified: 2023-12-15T18:55:05.385Z
---

# lib-saas-cms-community

# guide

# discuss-stars
- ## 

- ## 

- ## 
# discuss-airtable/excel-lowcode
- ## 

- ## 

- ## 

- ## [从 Excel 到 Airtable，从 LowCode 到塞尔达 - 知乎 _202309](https://zhuanlan.zhihu.com/p/649524625)

- [AppSmith 竞品调研 - 知乎 _202404](https://zhuanlan.zhihu.com/p/695067490)
- [伙伴云产品调研 - 知乎 _202404](https://zhuanlan.zhihu.com/p/695067103)
# discuss-lowcode
- ## 

- ## 我身边搞低代码编程（包括无代码编程）的同学，前后就有三四批。但是很奇怪，他们无一例外都失败了。
- https://x.com/ruanyf/status/1900345909348561228
  - 开发出来的低代码工具，开始还有一些好奇的用户，很快就不来了，用户越来越少。

- 低代码也好，无代码也好，要能够发挥作用，必须对业务逻辑很清楚。 这里就讲到了逻辑。 但很多时候甲方或用户是没有正常逻辑的。在这种情况下，什么低代码无代码，都是救不了的。 毕竟，就算没有代码，一样需要逻辑啊
  - AI写代码也是如此。

- 低代码不能降低业务复杂度，用户以为自己只是不会编程，其实是他们搞不定业务

- 首先低代码的使用门槛很高，任何低代码工具对于一个没有接触过低代码的人而言，都需要较高的学习成本
  - 其次低代码普遍是大而全的设计，在这种设计下很难闭环掉某一个具体场景下的整体链路，你总会发现这个链路中某个细节，这低代码平台就是缺少了那么一两个核心关键功能，导致无法使用
  - 除此之外，低代码普遍是saas的，对于企业而言存在数据敏感性，如果私有化部署动辄大几十万
  - 最后，低代码能帮助的大多是做业务但不会代码的人，但大部分人是缺少把业务链条抽象优化成流程链路，解构成低代码组件的能力的，这种能力一旦缺失，哪怕它掌握了低代码平台的使用，也是无法构建出想要的东西
  - 未来的低代码，或许就是一句话生成后，支持用户进一步调整和定义的，这样减少构建成本和思维成本后，低代码可能就更容易普及一些
- 还有另外一个原因：客户。
  - 需要自己定制功能的客户已经算是较有实力的公司，一般有自己的小开发团队，无需使用低代码平台。
  - 更多小公司则不属于此类，花小钱买个SaaS就很费劲，再花一分钱老板都心疼，白嫖是此类客户的首选，技术储备不足以支撑使用低代码平台，也就是你说的第一条。

- 只适用于需求比较确定的简单场景，比如行政管理的工作流。而这些场景很容易被钉钉、飞书、企业微信这些超级办公app覆盖，一个在线文档就能做到，足够轻量、足够易用，自然不需要部署维护单独的低代码软件了。

- 也有相对成功，比如wix、retool等，ai 会加速低代码的发展

- 我个人感受，代码有没有不重要，关键看是否创造多少价值，以及易用性。高代码和低代码并不是产品的成败，人们用软件并不是“我是不是学得会”，而是我能有什么受益？如果受益（金钱，效率，感观，信息，情报）大于学习和使用成本，就会去选择。

- ## [Release Wappler open source (frameworks and builder) - Feature Request - Wappler Community_202306](https://community.wappler.io/t/release-wappler-open-source-frameworks-and-builder/50468)
- open sourcing Wappler could facilitate greater transparency and trust.
  - Noodl app are already on their way

# discuss-saas-platform
- ## 

- ## 

- ## 🚀 [Show HN: I’m building open-source headless CMS for technical content | Hacker News _202306](https://news.ycombinator.com/item?id=36324281)
- If you don't mind some feedback, I'll share some thoughts: My professional and personal experience tells me that markdown and a static site generators are the best workflow for technical writing. I can automate quite a lot, and do proper version control. A GUI CRUD and all the related requirements such as databases, would get on the way to keep the documentation in sync with the actual codebase.

- [Show HN: An open-source, collaborative, WYSIWYG Markdown editor | Hacker News](https://news.ycombinator.com/item?id=36446045)

- From my experience, the benefit of Markdown is that it eliminates the need for WYSIWYG, because WYSIWYG is awful to work with.

- I love Obsidian's WYSIWYG implementation. It is WYSIWYG until you the cursor is touching any formatted element, at which point it reveals the Markdown that makes it appear that way e.g. h1 titles appear large, but clicking on them reveals the # at the start of the line

- Is anyone else using an internal wiki engine like Outline or Wiki.js, for their company or community? I am stuck self-hosting Outline because it has the most intuitive navigation and wysiwyg for non-IT people. I wonder if any better alternatives appeared since then.
  - I'd like to encourage you to check out Vrite as a whole. There's already Kanban for better management of content production process and I'd say the editor is comparable to Outline. Other views and more editor features are on the way.

- generic embeds aren't allowed - only CodePen, CodeSandbox, and YouTube. In Vrite, all the embeds are actually processed separately when auto-publishing to different platforms (e.g. Medium, Dev.to, Hashnode), that's why I don't want to allow generic iframes.
  - That said, I do plan to add some more embeds to the core (e.g. Twitter) but others will likely be supported through custom content blocks and extensions.

- ## [Reviving Sandstorm | Hacker News_202002](https://news.ycombinator.com/item?id=22231922)
- If the failure of Sandstorm has shown one thing, it's that people will not maintain forks of software if the layer you're integrating with is too complex.
  - I'd much prefer if Sandstorm just shipped with an IdP and contributed OIDC implementations to downstream projects.

- For those who dont know what it is: Single Sing On with an App Store.
- Sandstorm is also an extremely security-oriented way of running packaged apps. It uses an advanced sandbox that has defeated many kernel zero-day vulnerabilities. It utilizes the Cap'n Proto serialization + RPC protocol, another security-oriented project of Kenton.
# discuss
- ## 

- ## 

- ## 有没有一种 CMS，可以定义表结构，然后用低代码拖一个可视化编辑器页面和表字段关联的 的 SasS
- https://twitter.com/__oQuery/status/1753273583881867670
- 大部份低代码不都是这样吗？ 不过我觉得对程序员来说这不是最省事的模式。Django Admin 那种写好元数据几乎全部UI可以生出来更省事，不需要可视化
- 感觉绝大多数headlesscms都有这些功能
- 这不就是CMS系统应该做的事情吗？至少10多年前就有了，很多

- ## 快捷指令的编辑体验太屎了，难以想象做 20 行以上的指令有多痛苦。
- https://twitter.com/acghnu/status/1726963155585417612
- No code 所以并不会成为全部的未来
