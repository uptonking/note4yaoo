---
title: thread-blog-work-living-xp
tags: [blog, work]
created: 2024-01-08T14:54:25.356Z
modified: 2024-01-08T14:55:24.631Z
---

# thread-blog-work-living-xp

# guide

# blogs

# yearly-office-saas

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
# more
