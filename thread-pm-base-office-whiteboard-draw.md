---
title: thread-pm-base-office-whiteboard-draw
tags: [office, whiteboard]
created: 2023-05-30T21:36:19.919Z
modified: 2023-05-30T21:36:55.391Z
---

# thread-pm-base-office-whiteboard-draw

# guide

- [Rendering like Butter - a Confluence Whiteboards Story - Atlassian Engineering_202308](https://www.atlassian.com/engineering/rendering-like-butter-a-confluence-whiteboards-story)
  - Great insight into building high performance whiteboard for the Web
  - Finite State Machine
  - Entity Component System
  - WebGL
  - Tiling
  - While the essay concluded that the most efficient way to render things was using WebGL, the benchmark also showed that DOM+React was not that bad (3~4x slower than Raw WebGL)—small products and personal projects may not need the burden of WebGL.

- [Figma已被替代, Miro还会远吗？——无限白板大全 - 知乎 _202205](https://zhuanlan.zhihu.com/p/512318494)
# discuss-stars
- ## 

- ## 🤔 [Why Are LLM Chats Still Linear When Node-Based Chats Are So Much Better? : r/LLMDevs _202511](https://www.reddit.com/r/LLMDevs/comments/1oxrz24/why_are_llm_chats_still_linear_when_nodebased/)
- I think you could have a nice UI where it expands to a tree view with path summaries expose style. Getting the experience right would be a lot of work and it's such a niche workflow that I don't know if any company would put in the effort to build it.

- I built something similar for myself but it's based on highlights in a message. You highlight, a popup appears that provides custom prompt choices (e.g elaborate / simplify / critique etc), it takes you to a new chat window that can link back to the chat window where the original message was branched from. Then you can click on that highlight anytime to go back to the branched view

- It’s just a UX problm, not really an engineer issue. Basiclly you’re expecting the AI to talk to you in one singe chat, remember everything forever, jump back and forth between topics and still never halluciante or loose track of your ideas. But LLMs aren’t built like that. They proces context in a linear way because that’s how language input works, but it’s not how we actualy think. So the thing you want isn’t something AI can do in that format. Still, your idea is cool — build more stuf like this, make the AI enhance your knowldge, not think instead of you.

- I think it's too unintuitive to use, I'll also easily lose my train of thought and not be able to keep track of things after a while as I'll definitely open too many branches and then I'll need to re-organize. I think the current system of projects is good enough, better than unlabeled chats and not too messy as this format.

- Linear chat kicked off the current AI hype cycle. Therefore most people could only make the obvious leap from that into sequential workflow automation and more unthreaded chat-centric designs.
  - AI applications that diverge into many path like this are seriously overlooked. There is a UX part to this, but the AI aspects of this branching behavior are very interesting.

- If you use obsidian there is a plugin called cannoli which implements this. I use it a lot.

- ## What if a graph view and text editor were just two ends of a continuous spectrum? 
- https://twitter.com/OrionReedOne/status/1790263523857019227
  - You get consistent semantics, intermediate views, and some other benefits by blending structurally-compatible representations.
  - Here's a 'semantic zoom' in @tldraw
  - 类似大纲视图作为网状节点图的节点
- This could be a great alternative to the outliner as a notetaking system ... Incidentally, I've also been playing with defining graph models from within the text itself, and linking them together ...

- i want all of my code editing to be like this
  - we are not in the stage of editing yet, currently only for code navigation, but we will be full blown editor ultimately
  - [Spectral Beta - Visual Studio Marketplace](https://marketplace.visualstudio.com/items?itemName=SenecaFron.spectral-beta)
- Yes I need this in my ide
- If only something like @orgpad_official had a free version that i could run as an app offline or sync manually, that wouldn't cost me lifetime decency on non-trustable company.

- Knowledge graph? Or token linkage based on similarity?

- ## 有朋友问我Miro好在什么地方。
- https://twitter.com/PenngXiao/status/1739195961199800601
  - Miro有一个非常难用的地方，比如Table只难看有点不可思议。除此之外，完全没有一个地方支持Markdown也有点令人费解。
  - 除此之外，Miro的每个细节都完美的符合我的预期。
- 这样的产品单独说它好很难解释，就拿BoardOS做个对比，我用了几分钟发现的几个细节差距（不称为问题）：
  1. Sticky note里面的换行
  2. 触摸板移动无限画布不符合直觉
  3. 缩放速度太快、太敏感
  4. Mindmap选中之后不能独立缩放
  - BoardOS是一个非常优秀的产品，以上完全可能是我习惯了Miro之后的不适，并非产品的问题。

# discuss-workflow-pm
- ## 

- ## 

- ## 一直想寻找一套简单代替 Dify 的工作流框架。
- https://x.com/ZeroZ_JQ/status/1872456529691258935
  - 最后找到了知名工作流库 Prefect 推出的 ControlFlow。

# discuss-mindmap/flow
- ## 

- ## 

- ## 

- ## 

- ## Xmind 现在被ai冲击的厉害，已经改赛道了
- https://x.com/siantgirl/status/2034465468086669824
- Xmind创始人去年我还见过 说是他们目前在搞AI塔罗牌产品
  - 说是本来计划面向白领用户 定价比较高，但是实际发现初高中大学女生是主力用户，后面调整的价格和产品
- xmind创始人在介绍的时候 引用了一句网友点评 xmind除了好看一无是处

# discuss
- ## 

- ## 

- ## 

- ## 🤼🏻 无限画布不是一个好的内容组织产品形态。
- https://x.com/ahshengchen/status/1869654634756989110
  - 虽然提供了自由和灵活性，但它缺乏结构化，容易导致内容混乱和难以管理，尤其是在大量信息和多人协作的情况下。它不适合需要明确分类和层次的内容组织，且在性能和导航上也可能存在问题。 所以不是一个好的组织工具，如果所有的设计稿都在一个 Figma page 里如果不维护很容易乱吧

- 笔记守恒定律：输入越自由，维护越困难，白板这种形态看起来可以一股脑流畅地输出，维护起来就是地狱难度，只不过大多数人都因为输出的流畅用直觉投票了，忽视了长尾价值，吃两次亏就好了。个人认为 heptabase 已经是白板产品中可维护性的天花板了，但我还是懒得给那些随手拖出的卡片打标签。
  - 或许提供一键（在自由度高的画板布局和线性瀑布流布局之间）切换可以缓解这个问题@AFFiNEOfficial有类似的尝试，但是这种切换要符合用户的预期，感觉要解决的问题不少
- 输入会变得很难，因为要做好大纲和白板结构的对应。目前最权衡的方案是 ob 的 canvas，大纲是大纲，白板是白板，白板不是笔记的核心底层，只是一个功能

- 但是无限画布会给人一种掌控全局的很爽的感觉。

- 几千个元素在一个白板，看起来很震撼，但管理起来是噩梦。所以，我引入“项目-子画布”结构，可以想象成无边画布版的PPT
- 我倒是觉得不能嵌套才是对的。

- 快去试试tldraw，特别是要把他10来个用例教程走一遍

- 画布很好，但是我对无限画布的感受只有“初见惊艳”，在目前的物理显示器中没多大用。但是有更合适的VR或者空间显示器的话，体验可能会有天壤之别。

- 对于整理思路的我来说，还挺好用的。我常想，要是它是立体的，多维的就更好了；当我找出眉目的时候，我还能把中间更明确的重点给点亮，就像科幻片里的一样。但是，我的画布别人看不懂。

- 看啥场景，Figma和Figjam用来整理思路就很好用，如果说无限画布不好用，问题可能出在对要解决问题的定义不清晰、SOP不清晰、抽象出来的模版不清晰

- 这么说搞个 space 画布好吗，跟 Arc 一样分区

- ## We've shipped follow mode
- https://twitter.com/excalidraw/status/1737130730587603053
  - 适合画板类应用，当一个人操作时，另一个人的可见区域和focus跟随主要操作人

- ## 请考究派同学帮忙解释一下这个现象——为啥用户放着正规的图不用，喜欢手写风格。这个值得做成一个收费的特性吗？
- https://twitter.com/PenngXiao/status/1735204643138134241
- 不想为了几个像素的对齐，来回折腾。
  - diagram as code类产品没有这个问题，反正也不是用户控制布局
- 常用 plantuml，但这类工具和贴图里面所见即所得的画图工具是两种产品形态。
- 涂鸦符合人性。人就喜欢这种符合直觉但不准确的表达方式。
- 手写风格的ui设计图是有价值的， 不是喜欢而已，因为图是拿来沟通的，你的沟通对象可能是用户（客户）或其他非专业人士， 手写风格潜移默化给对方灌输 和强化 “这是草稿” 的概念，避免讨论沟通时跑题到当前不需要关注的细节去。 
  - 举个例子，讨论功能时，面对一个精美的按钮，有些客户会说按钮太大了
  - 但是面向一个手绘风格的按钮，讨论对象都知道最终ui肯定不是这样，所以不会提出样式上的建议意见而浪费大家讨论的时间。

- 自由，不受限制，才有创意产生。

- ## Added a timeline view to the @remix_run DevTools! (WIP) made with @vite_js
- https://twitter.com/aryan__deora/status/1725909619644461144
  - A neat way to visualize link prefetches too!
  - 页面fetch时序动画
  - 上面是页面，下面是devtools

- ## new discovery! use numbered figures (e.g. fig 1, fig 2) to describe different stages of an interaction
- https://twitter.com/tldraw/status/1726047257403830736
- Wait until I can import my figma into this
  - just copy a screenshot and paste it in 

- ## What if @figma had a cursor video chat?
- https://twitter.com/alexeinars/status/1706333517242618342
  - 鼠标光标移动时，光标旁显示用户视频界面而不是偷笑

- ## Do you prefer @tldraw to @excalidraw ?
- https://twitter.com/jitl/status/1643764436660899840
  - Excalidraw is ahead on features, TLDraw is ahead in my heart
- I like the code a lot more than the Excalidraw code, and I've learned a ton from following @steveruizok's work over the years

- ## meeting Steve and spending the day understanding @tldraw ’s vision (not as “another excalidraw”, but an embeddable canvas for everyone) 
- https://twitter.com/swyx/status/1598558782388256768

- ## A tangent thread is about how spatial canvases come into play. 
- https://twitter.com/chrisshank23/status/1663296920150999040
  - Particularly thinking about @tldraw 's early vision to provide a platform for other to build spatial canvases...
- I see a gap between unstructured spatial canvases and meaningful, structured diagramming tools. Spatial canvases nudge you to create your own conceptual framework for a task. Diagramming tools are domain-specific and have little extensibility.
  - The unstructured nature of a spatial canvas likely manifests in its implementation of a bunch of lines/shapes with coordinates that you move around. These shapes have no inherent relationship or meaning in the data representation only the human perceiving the canvas.

- What's cool is that the "nextgen" spatial canvases like @excalidraw and @tldraw are starting to explore this a little. 
  - For example, both have the first-class concept of arrows/lines connecting shapes together!
