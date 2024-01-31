---
title: thread-blog-work-living-xp
tags: [blog, work]
created: 2024-01-08T14:54:25.356Z
modified: 2024-01-08T14:55:24.631Z
---

# thread-blog-work-living-xp

# guide

# blogs

# office-saas

## [doodlewind: 创业第二年：风浪中前进的 2023 - 知乎](https://zhuanlan.zhihu.com/p/678400477)

- 二月的 0.4 版本支持了多种对 block editor 而言必须的 UI 控件，也引入了为白板实现的新 canvas 渲染器。
- 四月的 0.5 版本支持了双链，补全了许多缺失的白板功能，并将富文本编辑器从 quill 替换为了自研的 virgo（即现在的 @blocksuite/inline 富文本编辑器）。
- 六月的 0.6 版本支持了带独立选区的表格与白板上的 canvas 文字编辑，继续完善了大量白板功能细节，并抽离出了 @blocksuite/lit 作为适配 UI 框架的中间层。
- 七月的 0.7 版本实现了新版的白板 UI，支持了类似 git submodule 的 CRDT 子文档按需加载能力，以及新的 block spec API 供标准化地定义 block。
- 八月的 0.8 版本重写了数据驱动的选区系统，这是 BlockSuite 创建以来最大的技术改造之一。同时这个版本也支持了附件、演示模式和表格看板视图等产品需求。
- 十月的 0.9 版本支持了表格的 group / filter 功能，允许扩展更多元素类型出现在白板顶层，并设计了新的 block transformer 机制供兼容第三方格式。
- 十一月的 0.10 版本支持了白板元素的组合，允许将任意白板区域嵌入文档模式中。这个版本也重构了文档加载和更新时的事件流，并优化了白板批量操作时的性能。
- 刚刚发布的 0.11 版本实现了更多的编辑器周边 UI 组件。从这个版本起，BlockSuite 终于分离出了用于搭建编辑器的通用框架层，为此其文档指南也已经重写。

- 我确实在之前的工作中一直尽量规避介入管理，但对于自己创建的项目，确实只有自己上心才能最好地促进它的发展，而这需要实际掌握并合理运用对项目的控制才行。

### [Mirone's 2023 in ToEverything](https://insider.affine.pro/share/3a8e7255-0d20-4820-a71b-da3acd81a15c/AF4AicjVsjgb3a87B1Jwy)

- In this year, I rewrote nearly every part of the editor to make it maintainable and scalable.
- Refine Store
- Sub-Doc
- blocksuite's selection was in a mess
- Event Dispatcher
  - Control all events fired in one place is necessary for building editor. 
  - Because that can help you to resolve hotkey conflicts and provide different features for same gesture in different blocks. 
- Block Spec, Widget and Fragment
# yearly

## [jlongster: Where have I been? A short reflection on 2023.](https://twitter.com/jlongster/status/1747486287307645348)

- I did a lot less in 2023, which allowed me to focus more.
  - To sum up: "Sure, I could sacrifice something here. I could get up earlier, I could exercise less. But any sacrifice means I’m reducing my presence with either my job or family. Maybe you can do it, but I’m out."

- [Where have I been?](https://jlongster.com/where-have-i-been?x)
- 2023 was the year of “deceleration” for me and is the first year I finally found a satisfying balance and focus.
- Over last year I started realizing how overcommitted I was.
- You might be wondering where I have been, and I’ve been quietly focusing on my family and job, and rarely using social media, checking discord, replying to emails, etc.
- Doing this made me realize just how overcommitted I was.
  - I feel like I had space to finally process life: to think about things going on around me, and to actually come to conclusions about what I thought about it. 
  - To take the time to discuss it with people and grow relationships.
- Last spring I became Tech Lead for the Design Systems team at Stripe. 
  - The technical problems my team faces are incredibly hard, and on top of that I really wanted to work on learning how to grow relationships on a team and help everyone do their best work. To do this I really need to focus.
- In my personal world, I have a wife, 3 kids, and friends. Keeping up with these relationships trumps everything else.
- The biggest reality that hit me is that once you have a job and kids, you really don’t have much time for anything else. 
- Sure, I could sacrifice something here. I could get up earlier, I could exercise less. But any sacrifice means I’m reducing my presence with either my job or family. Maybe you can do it, but I’m out.

## [小树的 2023 年终总结](https://yeshu.cloud/posts/annual-summary-2023)

- 在 AI 大潮的推波助澜之下，兼职担任了 4 个月的产品经理，负责表格 AI 从零到一的产品设计和落地
  - 我一直自诩为一名产品工程师，但在这段经历之后，我意识到我当前更擅长把确定性的需求实现得尽可能好，而不是做出创造性的产品方案。
  - 另外，在业务面对巨大的不确定性时，说服其他人要付出的极大的努力，会始终陷在对结果的焦虑中，如果再叠加上沟通的内耗，会让人开始怀疑人生。
  - 虽然很多预想中的结果没有拿到，或者被同行捷足先登有些遗憾，但我还是很感恩能有一次尝试的机会。
  - 我最终决定在国庆之后转回全职的开发角色，深度参与到多维表产品的建设中。目前感觉一切都好，在吸取新鲜业务和技术知识的同时，慢慢找回了自己想要把产品做好的感觉。

- 我开始思考，我是否有在市场中直接实现价值交互的能力，简单来说，就是离开公司我是否还有能力赚到钱。
  - 我发现这条路和在大厂拧螺丝对个人能力的要求几乎是背道而驰的。
  - 大厂拧螺丝要求是专，是能解决某个领域的复杂问题。
  - 在市场中打滚需要的是全，什么都要会一点，能找到愿意付费的客户，帮他们解决问题。

- 这一年，开始精简自己的精神开支。
  - 尽可能减少让自己觉得拧巴的事情，减少形式大于实际效用的事情。
  - 我开始有意识地减少在社交媒体上停留的时间，把更多的时间放在读书上。
  - 我停止了事无巨细的记账方式。因为我意识到我并不会去回顾每一笔钱花在什么地方，每一类开支占比多少。我已经建立了对自己资产的掌控感，知道自己的开销是否在预算内，我现在只需要明确总资产的具体数额，而不需要关注变动的过程。

- 播客的形式注定了内容的信息密度是不够高的，同时，我自己的主要场景是通勤和运动，我是为了减轻眼睛的压力和放松才去听，所以我把它当作是一种娱乐消遣的方式。
  - 如果真的有很好的内容，我会选择用工具把音频转成文字，再消化其中的关键内容。
# career

## [回顾我这三年，都是泡沫 - 掘金 _202310](https://juejin.cn/post/7289718324857880633)

- 平台和好奇心一样重要。
  - 大部分人智商条件不会有太多的差距，尤其是程序员这个群体，而好奇心可以让你比别人多迈出一步，经过长时间的积累就会拉开很大的差距。
  - 而平台可以让你保持专注，与优秀的人共事，获得更多专业的经验和知识、财富，建立自己的竞争壁垒。

- 我觉得是时候阶段性地总结和回望回顾我过去这三年，却发现大部分都是泡沫。跨端、业务、质量管理、低代码、领域驱动设计... 本文话题可能会比较杂

- 2020 年七月，口罩第二年。我选择了跳槽，加入了一家创业公司
  - 进来后接手的第一个项目是原生小程序迁移到 Taro 2.x。
  - 技术的发展就是这么快，不到 5 个月时间，Taro 2.x 就成为了技术债。
  - 升级 3.x 我同样通过编写自动化升级脚本的形式来进行，这里记录了整个迁移的过程。
- 21 年底，随着后端开启全面的 DDD 重构(推翻现有的业务，重新梳理，在 DDD 的指导下重新设计和开发)，我们也对 C 端进行了大规模的重构，企图摆脱历史债务，提高后续项目的交付效率
  - 时至今日，我们吹嘘许久的“一码多端”实际上并没有实现；

- 比一码多端更离谱的事情是“一码多业态”。指的是一套代码适配多个行业
  - 这是我过去三年经历的最大的泡沫，又称屎山历险记。不要过度追求复用，永远不要企图做一个大而全的 2B 产品

- 2021 年，低代码正火，受到的资本市场的热捧。
  - 我们是 2B 赛道，前期项目交付是靠人去堆的，效率低、成本高，软件的复利几乎不存在。
  - 也有可能是为了追逐资本热潮，我们也规划做自己的 PaaS、aPaaS、iPaaS… 各种 “aaS”(不是 ass)。
  - 但是我们都没做成，规划和折腾了几个月，后面不了了之，请来的大神也送回去了。
  - 在我看来，我们那时候可能是钱多的慌。但并没有做低代码的相关条件，缺少必要的技术积累和资源。就算缩小范围，做垂直领域的低代码，我们对领域的认知和积累还是非常匮乏。
- 不管经过这次的折腾，我越坚信，低代码目前还不具备取代专业编程的能力。
  - 大型项目的规模之大、复杂度之深、迭代的周期之长，使用低代码无疑是搬石头砸自己的脚。简单预想一下后期的重构和升级就知道了。
  - 低代码是无代码和专业编码之间的中间形态，但这个中间点并不好把握。比如，如果倾向专业编码，抽象级别很低，虽然变得更加灵活，但是却丧失了易用性，最终还是会变成专业开发者的玩具。

- 2021 年四月，我开始优化前端开发质量管理
  - 人工 CodeReview 的重要性不能被忽略，毕竟很多事情机器是做不了的。
  - 然而，这场运动仅仅持续了几个月，随着公司组织架构的优化、这些事情就不再被重视。
  - 不管是多么完善的规范、工作流，人才是最重要的一环，到最后其实是人的管理

- DDD / 中台的泡沫
  - 我们在 2021 年底也进行了一次轰轰烈烈的 DDD 重构战役，完全推翻现有的项目，重新梳理业务、重新设计、重新编码。
  - 其实既然开始了 DDD 重构, 就说明我们已经知道 ’怎么做 DDD‘ 了，在重构之前，我们已经有了接近一年的各种学习和铺垫，且在部分中台项目进行了实践。
  - 但我至今还是觉得 DDD 很难落地，且不说它有较高的学习成本，就算是已落地的项目我们都很难保证它的连续性(坚持并贯彻初衷、规范、流程)，烂尾的概率比较高。

- 2022 下半年，我们开始了 ’DDD 可视化建模‘ 的探索之路
  - 最终，建模的结果通过“代码生成器”生成代码，真正实现领域驱动设计，而设计驱动编码。

- 重构了又重构，技术的债务还是高城不下
  - 推翻了再推翻，我们竟然是为了‘复用’？
- 降本增效的大刀砍来，泡沫破碎，回归到了现实
  - 我又走到了人生的十字路口，继续苟着，还是换个方向？
# more
