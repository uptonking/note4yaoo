---
title: lib-ai-app-pm-products-community-popular
tags: [ai, ai-coding, large-language-model, pm, trending]
created: 2026-02-20T17:34:06.342Z
modified: 2026-02-20T17:36:40.796Z
---

# lib-ai-app-pm-products-community-popular

# guide

- https://github.com/garylab/MakeMoneyWithAI /md
  - https://garymeng.com/
  - A list of open-source AI projects you can use to generate income easily.
# discuss-stars
- ## 

- ## 

- ## 🪟✨ Cursor now has built a Kanban board where you can just drop in tasks and the agent will pick those up and complete them.
- https://x.com/ParthJadhav8/status/2049564851060801663
- Similar: if you’re using @Jira you can just get agents to automatically pick up any step of your Jira workflow or define any condition in an automation role. Been blown away with millions of agents automatically working on boards in a loop

- the actual test is whether it can handle a task that requires context from 3 other tasks. single-task agents are solved. dependency-aware execution is where it gets real.

- Kanban + agent这个组合意味着从人对AI说一句话变成人定义一个流水线，AI自己跑。我用编码工具的时候就发现，最大的效率提升不是单次对话的输出质量，而是你能不能把一系列任务串起来让工具自己推进，中间不需要你盯着。kanban board本质上是在给agent一个记忆。

- ## Linear, PostHog, Attio - all shipped the same thing in the last few weeks. Homepage is a chat bar - not a dashboard.
- https://x.com/rabi_guha/status/2040082295563169852
  - This is the SaaS industry quietly admitting that traditional UI doesn't work anymore. Every user is different. One homepage can't serve them all.
  - The playbook is shifting: → expose your core APIs → connect an agentic layer → let users use software the way they want
  - SaaS became chat. Chat will become Generative UI - the agent won't just reply in text, it will compose the interface itself.

- Looks like infinite personalization. Acts like massive cognitive load. I learned this the hard way.

- https://x.com/DavidKPiano/status/2040491100285059293
  - Hot take: an empty chat box as the primary UI is the exact *opposite* of intelligence in a product. It's like saying "I have no idea what you want to do here, tell me"

- https://x.com/threepointone/status/2040720964451754464
  - this is simply evolution. the next step; the sections right under the chat box will become contextual/smarter about their suggestions, based on the user/org. 

- https://x.com/rabi_guha/status/2041547036529709191
  - Replacing dashboards with a chatbar was step one
  - Here's what step two could look like
  - 给每个组件都加上了chat输入框，特别是图表

- ## 🔀 非常有意思的人 & agent 协作 UX 探索！但如果为了实时看见 agent 改动而「实时更新磁盘版本」，会有两个问题：
- https://x.com/ewind_dev/status/2038275182180315379
  - 1. 人未保存的改动随时可能被 agent 覆盖，且现在是全量覆盖
  - 2. 人的改动即便已存，agent 推理中用的仍然是吃进上下文里的旧版，相当于改了没用
- 1 在线上协作里是个常见问题，考虑到agent那边不适合增加复杂度，可以在人工编辑模式未保存时单独做一个fork，外部写入的时候做合并，如果冲突就提示需要解决冲突
  - 2 有的agent工具会主动监听文件改动

- ## 软件没有稀缺性了。就像现在各种平台上发小说，发视频的，爱干不干，只能靠流量再自己想办法变现，或者以后大公司按你的用户消耗了多少token给你提成，就像视频播放量一样。
- https://x.com/MinLiBuilds/status/2037720336771457393
- 这种商业模式毫无价值，现在广告这一套之所以有用。是因为生产大于消费。而，后面大模型取代扩大部分岗位，生产减小，压根没有多余资金消费。而，广告纯粹是奶头乐文化，对经济半身毫无价值

- 我总有个疑问，如果大模型大厂下场做，小厂的机会是不是瞬间就没了？就像去年 9 月，国内外 80 多家做 AI PPT 的，现在基本都死透了。AI 感觉就是赢者通吃，没第二名什么事。
  - 有一些场景是，本地部署类的， 例如，医院，不愿意把病历完整传给云端 AI 厂家。 这些大模型厂很难进来。 如果要进来，一家一家和企业谈定制和隐私， 对于股价和商业模式又变得不性感了。

- 不能这么想吧。做搜索引擎的都是聚合搜索别人的资源。他们当然有资源和技术能把别人的平台资源都做一遍！但钱是赚不完的，总有他涉猎不到的领域。要不然在传统互联网时代，所有网站都被Google 百度做完了

- 我觉得得做垂直领域细分的，一个是大厂偏向于通用场景，细分模块没那么好做，一个就是数据没那么好获取/清洗
  - 大厂可以收集小厂清洗好的数据，坐享其成
- 是啊，一个愿意付费调用api的数据胜过90%免费用户了，这种高质量的数据集谁不喜欢

- 足够细分，在一个领域研究的足够透，和客户绑定, 就没大厂什么事了, 大厂照顾不到的地方太多了

- ## 🤔 [What actually convinces you to reach for OpenClaw instead of Claude Code? : r/openclaw _202603](https://www.reddit.com/r/openclaw/comments/1rxx2q9/what_actually_convinces_you_to_reach_for_openclaw/)
  - OpenClaw's multi-agent setup, the cron jobs, the channel integrations — all that stuff seems cool in theory. But none of it has made me think "oh damn, I NEED to use this for coding tasks."
  - openclaw借助llm解决了传统自动化/工作流的if条件模糊/复杂难处理的问题

- I use both. Claude Code for programming, Openclaw for monitoring my life and nudging my behavior.
  - The difference isn't the model, it's that OpenClaw runs 24/7 and has memory across sessions. Claude Code is a tool I open when I need it. OpenClaw is always there, connected to my calendar, fitness watch, tasks. Runs cron jobs while I sleep, remembers what happened last week, connects data from sources that don't know about each other. You could build all of that in Claude Code too but then you've spent weeks building infrastructure instead of using it.
  - You could build all of that in Claude Code too but then you've spent weeks building infrastructure instead of using it.
  - Best win was when it caught a pattern in my behavior that I hadn't noticed myself. You don't get that from a coding tool no matter how smart the model is. That's not intelligence, that's persistence plus context. So the automation/integration side matters a lot for me.

- Claude Code is incredible but it's fundamentally a synchronous tool. You sit there with it. OpenClaw is the thing you set up, walk away from, and come back to find your inbox processed, a draft report written, and three calendar invites sent.
- For pure coding in the terminal? Claude Code wins, no contest. But the moment your task involves:
  - Multiple steps across different apps (email + calendar + web search + a spreadsheet)
  - Something that needs to happen on a schedule without you babysitting it
  - Coordinating between multiple specialized agents
- ...that's where OpenClaw stops feeling like "Claude Code but worse" and starts feeling like an entirely different category of tool.
- The model intelligence question is real though. If you're using Claude through both, the model ceiling is the same — OpenClaw's value is in the orchestration layer, not the underlying intelligence.

- The "aha" moment for me was when I wanted something to run while I was NOT at my computer.
  - OpenClaw is an agent. It has a heartbeat. It can run crons at 2am. It can notice that you got an email from a specific person and do something about it before you wake up. It can monitor a thing and alert you when a condition is met. That's a fundamentally different use case.
- if you want:
  - Daily briefings when you wake up
  - Auto-draft email replies for review
  - Scheduled reminders and check-ins
  - Cross-platform automation (calendar + email + Slack + WhatsApp)
  - An agent that runs even when you're traveling without a laptop
- ...then OpenClaw fills a gap Claude Code structurally cannot fill.

- 

- ## 凡是吹 CLI 和 TUI 伟大复兴的人，都是没有脑子。历史已经一次次证明了图形化是必然的。教育市场，反过来只会被市场教育。
- https://x.com/techeconomyana/status/2033852684286234666
  - Codex在CLI命令行界面的时候，只有60万用户。推出了Codex APP之后激增到200万。
  - Claude Code推出都这么久了，为什么是Cowork出圈？

- 降低使用门槛是必然的，普通用户和类似程序员的专业用户，体量不同而已

- ## 有没有一种可能，以后软件/服务商只提供 API 和 CLI， 由社区来 Vibe 和 打包 各种发行版本的 GUI
- https://x.com/cellinlab/status/2034108711229395304
  - ffmpeg 其实就已经是这样了， 提供最全参数和 API 的 CLI， 然后社区去做了不同的 发行版本
- 为什么产品制作方不同时直接制作面向最终用户带 GUI 的版本呢
  - 可以，但是 他不能做太多个版本，就行 Office 很多功能一般都不用

- ## LLM被过度神化，根本原因是大多数人不了解其背后的数学原理。它的实际价值在于效率提升——大约30%，且集中在编程这类输出容易自动化生成、结果容易形式化验证的领域。
- https://x.com/edward40e/status/2032899339090276545
  - 一旦理解了当前架构的理论瓶颈，就会意识到离通用智能还有本质性的距离。
- 信息的分类加工传递变得前所未有的廉价，反而衬托出了信息采集的重要性
  - 过年整理过去一年的数字记录时感觉没有以往那么紧迫了。随意混在一起打包，然后相信未来的 AI 可以把他们整理出来，而且比咱做得更好。

- 本质上是一个基于概率的生成器，理解这个就理解了局限性

- 没办法。信息过载时代的人类，要么戒断多余信息，要么自己维持一个坚强的核心。如果拥抱信息风暴又没有核心，就只会FOMO。而这就是大多数人情况。

- ## https://malus.sh 非常有趣：干的事是是用AI机器人帮企业把开源依赖重新实现一遍，从而摆脱开源许可证的各种限制。
- https://x.com/vikingmute/status/2032420305034211591
  - 他们的AI号称不看原代码，只看公开文档、API spec等，从零独立重写功能等价的代码，输出的代码归你公司所有，宣称这样就彻底解放了，不用遵守原开源许可的attribution。
  - 定价很便宜：按npm解压后大小 $0.01/KB。

- 听说过洗钱的，这又来了个洗代码的。

- wine的故事。 没那么简单

- 这个网页自己都有bug好多链接都是死的。还帮人搞代码呢。诈骗网站吧

- ## [佬友们有没有发现：现在已经没有人讨论RAG、知识库、MCP、Dify和FastGPT哪个更好用了？  _202603](https://linux.do/t/topic/1743407)
- RAG感觉死很久了
  - 知识库偶尔还能听到
  - MCP在Skills出来基本就没有声音了
  - Dify和FastGPT这种包装一层的只能说是过渡吧，就跟曾经的低代码一样

- rag/知识库感觉还是会有用，mcp 可能配合着 skill 还是有用，workflow orchestrator 是真的看不到前途

- 知识库的有用限于企业环境吧，个人自用的话，claude code 已经证明了一个 ripgrep 加文件系统 is all you need

- rag你当大模型外挂一个向量检索用来给大模型挂相关任务的上下文，知识库就是被检索的数据库，mcp其实用的还挺多就是类似chrome外挂工具，dify是固定工作流

- RAG、知识库，企业内部还是有讨论的；MCP已经是必不可少的了吧；Dify其实和coze/n8n一直有市场，只不过我们没留意；

- ## [OpenAI 宣布收购 AI 安全平台 Promptfoo _202603](https://linux.do/t/topic/1716028)
  - 3 月 9 日，OpenAI 宣布将收购人工智能安全平台 Promptfoo，并计划在交易完成后把该公司的技术全面集成到 OpenAI 的企业级智能体平台 OpenAI Frontier 中。
  - Promptfoo 主要面向企业用户，在 AI 系统开发阶段帮助识别和修复各类安全漏洞，其工具目前已获得超过四分之一财富 500 强企业的采用，并通过开源 CLI 和库支持大语言模型应用的评估与红队测试。

# discuss-ai-moat/roadmap 🤼
- xp
  - 在LLM热潮前就有很多开源/免费软件, 它们是如何维持运营的

- ## 

- ## 

- ## 统计下大家跑通的AI赚钱路径
- https://x.com/0xLoki_Zeng/status/2050502892168114418
1/ 中转站
2/闲鱼代写论文，代图
3/ 做垂类产品，算命，帮捞女吊男人
4/ 卖AI教程，赚钱教程
5/ 搬运/生成内容，赚各平台流量收益
6/ AI Trading炒币，炒股
7/ AI 起号崩老头(用ai p图和视频)

- 用AI做个性化学习工具（如考研/考公题库生成+错题分析），通过小程序或知识星球变现，复购和口碑传播都很强，比纯内容赛道更抗平台风控。

- 8/ 卖铲子永远比挖矿稳，最后发现最赚钱的还是教别人怎么赚钱。

- 补充：8/ skill stack 跑 multi-agent reply workflow，1 人 cron 化 sustained 跑 7 天能维 6+ chain partner 关系（这条比 AI trading 慢但可复利）。9/ 自动化前 6 项里某一项，卖 saas 给做这 6 项的人。我感觉越往下层越护城河，但起步需要先有量去验证。

- 补充一点 网盘拉新

- ## 深刻感知到了Vibe Coding和做产品之间的差距： Vibe Coding 3小时，就能够搭出个70分的demo；但要再提高个20分，把demo打磨成产品，需要的时间30个小时都不止。
- https://x.com/0xEvieYang/status/2047390229821354117
  - 那20分就得要更深的know-how、更强的产品sense、更广的数据源......

- 也不能完全这么说，看需求。 很多需求其实70分的demo就够够的了，以前之所以要打磨到90分，是怕员工没事干，闲的慌。

- 所以VibeCoding一方面是提升程序员的效率，这是线性的。另外一方面是完全点亮了产品、商务、渠道的一个新的技能，这是生产力的重构。

- 原本需要快速验证需求的问题解决了 
  - 至于这东西是个什么商业形态 还需要有专业的技术团队去落地
  - 说白了 其实省下来的时间是剔除无用和不合理的需求  
  - 现在有点本末倒置

- vibe coding 3小时出demo很开心，但从70分到90分的产品打磨，差的不是代码能力，是产品sense和用户场景理解。agent能帮你写代码，但不能帮你决定该不该做这个功能。

- 做出来和卖出去，两个完全不同的难度

- ## 价值总是来自于稀缺性。 过去写代码是一个稀缺的能力，只被少数拥有资源的人掌握，所以软件捕获了大量的价值。 
- https://x.com/jiayuan_jy/status/2040687176544047422
  - 现在 coding 已经被完全商品化了，不管是开源还是非开源的软件，可防御能力都是极低的。 
  - 壁垒应建立在代码之外。
- 代码本身越来越像基础设施，真正的壁垒开始往场景、数据、分发和执行效率上转移

- 真正的壁垒是业务理解、产品思维、解决实际问题的能力，这些AI一时半会儿还解决不了。技术永远是商业的最不重要的一环。

- 太高估代码在软件业的重要性了

- ## 现在似乎没有人提起poe、chatwise、cherry studio等等了，也少有人提及n8n、dify，模型能力升级过程中已经淹没了一大堆产品，细数一下：
- https://x.com/wquguru/status/2037886289907982654
  - Poe：曾经最方便的多模型聊天聚合平台
  - Chatwise：高性能桌面AI聊天客户端，支持多LLM、本地化隐私
  - Cherry Studio：跨平台AI生产力工作室
  - n8n：开源工作流自动化神器
  - Dify：AI应用低代码构建平台，快速做RAG和Agent的利器
  - 还有Flowise、Langflow、AutoGPT、BabyAGI这些早期可视化/自主代理工具，都在o1/Claude 3.5/GPT-4o等模型狂飙中逐渐淡出视线
- n8n和Dify的企业MRR早赚麻了。你看不见只是因为那些营销号去蹭别的了
- 哈哈哈就像前几天我还疑惑 perplexity、midjourney 这些产品是不是死了，其实存量用户就已经够吃好几年了，过了某个阶段之后，只是不再有那么大的hype，但用户总归是留存下来了（如果真的是好产品的话）
  - 挺有道理的，用户基数足够，产品迭代顺利，又能够解决相当的痛点，还是能活的滋润

- 这里面有些跟模型能力没啥关系，例如dify就是被其过低的复杂度上限淘汰的。用多了意识到用起来吃力就没人用了。cherry studio作为一个调试工具，与其说被模型能力淘汰不如说被cli界面淘汰。
  - dify被agent sdk取代

- codex app出来之后我就把chatwise卸载了
- 感觉未来都是应用层的了，你要好好的，怎么让用户一句话就去赚钱。

- poe主要是api对别的支持不好，如果claude code之类的有对应接入方案，感觉发展就完全不一样
- AI刚出来的时候，我天天用POE, 因为可以免费用各种模型。但现在强的模型就只有那么几个，而且每个模型的官网都推出了一系列特色功能，就没有再用 POE 了。

- n8n 集成做的不错，有时候有些接口懒得搞 skill 了就往 n8n 里面一塞

- 
- 
- 
- 
- 

- ## [Claude Code使用之后，有点焦虑 - LINUX DO _202603](https://linux.do/t/topic/1767554)
  - 深度使用了一段时间 Claude Code，说实话，被震撼到了。
- 之前自己引以为豪的就是动手能力强——不管什么东西，给我点时间，我总能捣鼓出来。代码写得不算优雅，但能跑、能用、能解决问题，我一直觉得这就是我的核心竞争力。
- 但是使用之后发现，Claude Code从根源上就直接薄纱了我：
  - 之前写的屎山代码，它三下五除二就重构好了
  - 脑子里一个模糊的想法，它两下就给你 vibe 出来一个能跑的版本特别聪明
  - Plan 模式下拆解任务、设计方案，比我自己想得还清晰
- 说白了，我之前靠“肯花时间 + 能写代码”建立的优势，现在一个工具就能平替，而且做得比我好。
- 以前觉得“不搞科研，靠工程能力吃饭”也是一条路，但现在这条路好像也在被 AI 蚕食。
- 说实话，这种强力的AI绝对是大势所趋，等到毕业的时候，人人都能熟练用 Claude Code 这类工具了，我就在想：那我还剩什么不可替代的东西？

- 还可以修下水道，修空调

- 我只能说，往大数据少的方向去利用ai，ai还得看利用的人水平怎么样的。

- 只能加入，用的更好，现在是高速发展期，谁也不知道他最后还能多强，不过终究是工具，还是得人来用吧。

- 你理解的动手能力强，是古法调试代码的能力。
- 技术在于革新。
- 动手能力强，也可以是掌握新技术，把AI玩转。
- 你觉得人人都能熟练用cc，但我感觉只会有一小部分人能真的熟练。各种工具mcp, skills，工作流和多agents编排，提示词工程。真的就能人人都熟练么？
- 适应工具，发挥自己动手能力强的优势，深入去研究试一下。

- ## [某互联网大厂产品内测有感（程序员的未来如何） _202603](https://linux.do/t/topic/1701158)
  - 本次测试为云平台的代码开发
  - 你可能会想这有什么，无非就是上云嘛，不管是Claude code还是别家，早就可以做到云端写代码了，但是本次测试，只需要上传项目文件和任务描述，然后中间没有任何的交互的地方，全流程自动化，即我给你一个任务，中间无任何交互，直接验收成果。
  - 本次测试测评要求：使用最近 Coding 场景发生的真实任务，最好是基于现有代码仓库的任务，不能使用单纯的测试 prompt
  - 未来代码的开发一定不会是像现在这样，写代码这个门槛将放的无限低。任何一个人只要有一个需求，他就可以做到一个非常非常复杂的项目出来。注意不是所谓的玩具，而是那种真正的复杂场景下的代码研发，你从现在这几家大厂的产品线，你就能看出来，这个测试我就不说是哪家了，然后另外一家智谱的Z code产品线，核心目的也是这个
  - 甚至我自己的项目，核心目标也是这个: GitCortex 的最终设计目标是通过社交平台的简单对话，完成复杂项目的产出，不是那种玩具，而是真正的复杂化的生产级产品。
  - 而且 AI 迭代的速度已经超乎想象，一年前，写个前端的贪吃蛇小游戏，一年后，现在可以完成复杂的项目开发
  - 无论是智谱，还是这家互联网大厂，亦或者是我的项目，完成完整性开发后，这个时间不会超过二零二六年，就已经可以达到他所说的2028到2032这个水平了
  - 大厂和我的研究方向，实际上是让每一个人都可以拥有自己做应用的能力，而且是做那种很复杂的应用，满足各种每个人各种各样的需求，让每个人有一个新需求，他就可以自己立马DIY一个新应用出来，做到这种程度
  - 至于现在所说的 AI 产出的代码，维护性差、质量低等等问题，返璞归真就解决掉了，现在有技术就解决掉了，我就说一个最简单的方式，把sonarqube的评分规则扒下来，在完成任务提交之前，新增一项内部检测，合规输出不合规返工。当然有更多更好的解决方案，我只是随便说了一个最简单的
  - 而且我的这个感觉并不是今天才有，我实际上刚开始研发我自己的项目的时候，我就已经有这个感受了，然后我发现智谱和我撞车了，然后今天参加另外一个大厂的产品内测，发现核心上也撞车了，就我最开始有这个感觉的时候，我可能认为是我自己夜郎自大，我想多了我太菜，是我没有意识到哪些地方是有空缺的，但是接连发现大厂的产品线跟我重叠，就我不知道怎么说这个感受，所以来发一个这样的帖子。
  - 这大厂真挺狠啊，同时测8个模型，光填评测表都得填一个半小时到俩小时左右，除去1～2 个老版本模型，相当于他至少有6个新模型在同步开发，并且都是专攻于代码生成的
- 不知道他们 我做的GitCortex, 是多终端，主终端分配任务，自动拉起新终端，单个终端的上下文非常有限，而且主终端不负责审计代码 只负责分配任务和传递任务，各个子终端传递给主终端的是那种已完成的任务列表 不传代码

- 你仅通过和微信机器人或者说飞书机器人对话，完成了一个超复杂项目的开发，你唯一需要做的就是告诉机器人你的需求，你想要什么东西，你连架构都不用知道，更不用像现在这样去折腾，现搞什么plan计划，然后一步一步地去做出来，什么都不用动。包括安装都是傻瓜式的，我的项目做了一键式的安装，那两个大厂的项目更不用说了
  - 甚至可以说，目前所有的一句话做 App 的所有应用都是同类竞品，只不过他们现在做的还是比较初级的前端应用小应用，能做复杂项目的各家大厂还都没发布，还在内测，我的项目虽然发布了，但是也不成熟，也还在开发中

- 在编程这方面大模型确实是很强了，现在是抢应用落地的阶段了

- 其实感觉还没到模型能力的稳定期，现在的很多范式都是有强烈时效性的，不太能说有决定性的突破

- ## Imagine a future world where agents can recreate all of planetscale’s source code perfectly.
- https://x.com/aboodman/status/2026179235896017074
  - I still don’t want to fucking run it. Even if the agents do it. Even if I know it’s just sam and 20 sock puppets I’m paying to run it.
  - In case you haven’t realized it, Planetscale isn’t selling databases. They are selling SRE-hours.

- People finding out what the last S in SaaS means

- Tens of people will be happy to run it and some with even better features, compressing margins.

- ## OpenClaw打消了我对程序员前景的担心 - openclaw几乎是vibe coding出来的，要是 toB 的软件像这样每次升级都挂一片，早就没有用户敢用了。
- https://x.com/spacewander_lzx/status/2025965778181505280
- 每次升级都血流成河，这都不能叫 breaking change 了，叫 blood change

- 绝大部分tob的项目只要领导开心，有没有bug无所谓，用户连吐槽的地方都没有，tob是做的质量比较差的软件领域。只有极少关键软件要求高，基本也没人敢碰。

- 说没有用户敢用是你没去过小公司，就那种地方小国企做的项目，哪次不是领导有个很急的需求就匆匆上线了，一样是上线一堆bug

- ## "Code Is Cheap Now. Software Isn’t."
- https://x.com/VKazulkin/status/2025622866306519274
- What matters isn’t tools, it’s the idea and the ability to solve real problems. You have to think like a builder and a dreamer. Engineering is the execution layer; vision is the leverage.
  - Focus on what AI can’t outperform you at, original thinking, creative problem framing, and connecting dots others don’t even see. Then use AI as force-multiplication for what it does beat you at: speed, scale, and relentless processing.
  - This is a golden era for high-IQ domain experts who actually execute.
  - Find your niche, move fast, and build before the market catches up.

- https://x.com/ivanfioravanti/status/2025656085344821617
  - We have so much power in our hands, we can build any software nowadays, but having so much possibilities make me unable to choose a single one to focus on. 
- The same feeling I had starting out in ML a decade ago. Back then when confronted with the choice I narrowed down the scope to Vision and NLP. The knowledge gained generalised pretty well and is the foundation to which I help build the MLX ecosystem.

- Find a problem you have, or something you work on. Use that power to do it better by figuring out new ways. You have been focusing on optimizing the tools, and you need use them to solve your own problems to complete the picture. Better, drive your efforts by the problems in hand.

- I know what I'm building and sticking to that. The advantage: When models get better, the work on that one thing improves. You can build anything, but if you pick 1 problem to solve, and get insanely good at that, now you have something worth it for people to use.

- ## I love AI but please no more blog posts about AI destroying “moats” that weren’t moats in the first place.
- https://x.com/bernhardsson/status/2025729124359094332
  - A competitor could always clone the UI (read about the Samwer brothers) for instance.

- the real moat is usually in the data model and workflow optimizations you discover after v1. anyone can clone a UI, but few stick around long enough to learn why certain tables need careful indexing or which queries need materialized views

- Agreed. The "AI kills all moats" take misunderstands what a moat actually is. Real moats are distribution, trust, switching costs, proprietary data, and relationships. Those don't go away. If your only moat was "we coded it and others didn't" — that was never a moat.
  - this is the right frame. I'd add: for agents specifically, the moat is operational trust. anyone can spin up an LLM with tools. but getting a human to let it touch their email, calendar, wallet, and leave it running overnight? that takes months of earned reliability. code is commodity, trust is compounding.

- if your only edge was a prettier UI you were cooked way before Claude showed up

- ## Vibe coding culture will make many people understand that a website or app is not a business; a business has a website or app.
- https://x.com/Benn_X1/status/2025308341811970237
  - The most important department in any company is sales/marketing. You’ll need to go outside and touch grass after vibe coding the perfect product with AI.
  - You’ll need customers, and you’ll learn very hard lessons if you’re attempting to vibe code a B2B product.

- Building something is now the easy part. The hard part was always distribution and understanding why someone would pay for it. Vibe coding just removes the illusion that the code was ever the bottleneck.
  - The B2B point especially - you cant vibe code domain expertise or customer relationships

- Vibe coding just removed the "I can't build it" excuse. Now you're left with "I can't sell it" which was always the real problem. The people who win aren't the best coders or the best vibe coders. They're the ones who know their customer.

- A polished app isn’t a business, distribution, sales, and real customer demand are. Vibe coding can build the product; it can’t build the market.

- If you can’t sell the problem your code solves, you’ve just built a very high-tech hobby, not a business.

- https://x.com/ivanalog_com/status/2025583968167281010
  - 快，很少是商业的核心价值；
  - 正确，稳定，安全，高精度，可信赖地方式达成目的，往往才是重点。
  - 而Vibe这种形式，一开始就对后者不够重视。
  - 商业本身的价值，就在于可预测性和强可靠性，这是AI作品目前最缺乏的。
  - 当然，反过来说，AI本身只是一个工具，是否重视商业的某一个侧面，或者使用AI代替具体哪一个环节，还是由使用AI的人决定的。未来机会无限。
  - 说的极端一点就是，对于一家银行来说，除非有致命错误，不然，用rust代替cobol，用新架构代替一个运行稳定几十年的屎山，有什么真实的好处吗？rust和AI工程师，目前也比cobol老头贵的多。和技术爱好者相信的相反，几乎没有。工程师的审美和洁癖，在真实世界毫无意义。

- ## 其实最后用户愿意买单的产品还是一样的，真正能留住用户的还是那些精心打磨，真正好用的产品。有没有 vibe coding 都一样，只要用户的需求逻辑没变。
- https://x.com/yvbbrjdr/status/2024665256791019670
- 但是病毒营销出来的东西会被收购，套现离场

- 感觉产品的核心竞争力正在转变成对细节的打磨，因为复制创意越来越简单，可能几小时时间甚至更短就能出个可验证的 sample，但打磨细节到完成品需要额外的精力和时间, 虽说从 0 到 1 的乐趣被永远剥夺了

- 确实是这样，软件开发发展到内容农场的阶段

- ## 🤼🤔 Cloning any random piece of SaaS is something that could already be done before agentic coding, and the economics of it haven't changed meaningfully. 
- https://x.com/fchollet/status/2025283590972756284
  - Before, writing the clone would cost 0.5-1% of the valuation of the legacy SaaS company. Now it might be 0.1%. 
  - It doesn't make a difference -- if you can pull it off profitably today you could also have done it profitably in the past.
  - The code is a very small part of the process of making such a clone successful, and the reason legacy software has often bad UX is not because code was expensive to write.
- I genuinely think "code is now much easier to write and features are much easier to ship" strictly benefits legacy SaaS because it addresses their main weakness
  - The main threat to legacy SaaS is other legacy SaaS trying to move horizontally into their space because it is now easier to do so
- Circa 2012 you had a lot of devs "cloning Twitter" as a weekend project. Reproducing the UI and features of any app was never difficult and was never particularly valuable.

- I agree with this, and it explains why Meta would spend billions of dollars acquiring competitors rather than just building it themselves, which they could have done so easily.
  - However, I think there are examples of software which are just genuinely very difficult to build, even now with Vibe coding. It would still take many years to vibe code Adobe Photoshop, DaVinci Resolve/Fusion, or Unreal Engine again from scratch, even if you knew exactly "what" to build, and mimicking anything means you don't understand it in the same structural/phylogenetic way -- so you won't be able to creatively evolve it. 

- the workday example is perfect. google could clone it in a week. they don't because the value isn't in the code, it's in the compliance templates, the audit trails, the integration with 500 payroll providers, the decade of edge cases baked into business logic. vibecoders cloning saas UIs are solving the easy 5% and calling it disruption.

- Exactly. Code has never been the moat. Distribution, data network effects, switching costs, and trust are. Agentic coding lowers build cost, but it doesn’t magically give you customers, integrations, or brand credibility.

- The moat was never the code. It was distribution and switching costs. That math still holds.

- Problem of SaaS is not cloning. Their problem is that now I do not need many SaaS at all. I can just build things for myself or as internal tools for the company way cheaper than it was before
  - The reason people pay for SaaS is not just because of the effort of development
# discuss-ai-pm-search
- ## 

- ## 

- ## 

- ## 🎞️ SentrySearch：用自然语言搜索视频内容的开源工具
- https://x.com/dotey/status/2039147493355634989
  - 在几个小时的行车记录仪视频里找到"一辆红色卡车闯了停牌"那个画面，SentrySearch 能让你像搜文字一样搜视频，输入描述，直接导出对应片段。
  - 这个开源命令行工具的原理并不复杂：把视频切成带重叠的片段，用 Google Gemini Embedding API 或本地的 Qwen3-VL 模型把每个片段编码成向量，存进本地向量数据库 ChromaDB。搜索时，文字查询被编码到同一个向量空间里做匹配，命中的片段自动从原文件中裁剪出来。分块是因为一次没法太多，重叠是因为避免切分不好把内容从中间强行分开了
  - 关键在于，整个过程没有转录、没有逐帧生成文字描述，视频像素直接和文字查询在向量层面比较。这是 Gemini Embedding 2 和 Qwen3-VL-Embedding 这类多模态嵌入模型带来的能力，让对海量视频的语义搜索变得可行。
  - 想用云端 API，一小时视频的索引成本大约 2.84 美元。想完全离线也行，装上本地 Qwen3-VL 模型就不需要任何 API 密钥，24GB 以上显存或内存的 Mac 和 NVIDIA GPU 都能跑。它还专门做了特斯拉行车记录仪的适配，能在裁剪出来的片段上叠加车速、GPS 位置和时间信息。

- https://github.com/ssrajadh/sentrysearch /2kStar/MIT/202603/python
  - Semantic search over videos using Gemini Embedding 2 or Qwen3-VL.

- 做过类似的东西, Gemini embedding表现挺一般的，同样做多语言图片搜索，换成jina的clip v2也不错 开源且可直接本机跑

- 这个方向适合先把视频片段找出来。但要做到视频问答，就不只是存视频向量，还得存文本描述。不然后面很容易变成“片段找到了，答案你自己看”。

- 这玩意儿听起来挺酷的，终于不用一帧一帧地翻视频了。
# discuss-ai-pm-computer-use/openclaw
- ## 

- ## 

- ## 

- ## [Unpopular opinion: OpenClaw and all its clones are almost useless tools for those who know what they're doing. It's kind of impressive for someone who has never used a CLI, Claude Code, Codex, etc. Nor used any workflow tool like 8n8 or make. : r/LocalLLaMA _202604](https://www.reddit.com/r/LocalLLaMA/comments/1srkah3/unpopular_opinion_openclaw_and_all_its_clones_are/)
- It's not about the tool, it's about the adoption it created. OpenClaw has some nice ideas, but yeah it's true all of that was there before, but it made it accessible.

- Completely disagree. The ongoing work context, tool history, as well as broader access has been a huge help for my work.

- they have product market fit.

- ## [[开源分享] ClaudeChrome - 在浏览器中启动 Claude/Codex，实现通用智能交互体验 - LINUX DO _202604](https://linux.do/t/topic/1903375)
  - 项目 idea 很简单：把 Claude / Codex / Shell 放进 Chrome 侧边栏（Shell 其实现在还没啥用，因为主要靠自行实现的 MCP Server 实现自动页面交互，主要是给未来一些插件脚本手动调用浏览器接口留空），并把每个 session 绑定到一个真实标签页（使用过程中也可以 rebind 标签页）。这样 Agent 看到的就不再只是你手动贴过去的一点信息，而是当前标签页的页面文本、HTML、请求、console 等浏览器上下文。
  - 在 Chrome side panel 中直接运行 Claude / Codex / Shell
  - 读取页面内容、HTML、网络请求、控制台、执行 JS 代码、运行 click, scroll 等交互
  - 多 workspace / 多 pane 组织视图

- ## 微信官宣接入 openClaw，这波短期来看利好谁呢？
- https://x.com/kasong2048/status/2035573575860760946
  1. 自媒体
  可以预见，会有一波“你超级个体 10x 高效的同龄人 + 龙虾”正在远远甩开你，再加一套卖课组合拳
  1. 搞GEO的
  以前训练语料投毒 只能影响你使用的各种 AI应用，龙虾的普及会把影响带到个人电脑
  1. 搞安全的
  - 除了 2 外，更直接的威胁来自“上下文投毒”。比如随便下了个来路不明的 Skill，这不就是手把手教龙虾做一些奇怪的事么
  - 唯独不利好真正做事的。你要真靠 Agent 做到 10x效率提升，用飞书起码还能打通多维表格、文档，用微信这种封闭的 2C 平台作为龙虾载体，能干啥？在 幸福一家人 群里部署个 劝架龙虾 么？

- ## [Openclaw… what are the use cases? : r/LocalLLaMA _202603](https://www.reddit.com/r/LocalLLaMA/comments/1ryw7kn/openclaw_what_are_the_use_cases/)
- So far the common use case for the people on the hype train seems to be: summarize my day.

- It enables people with little technical ability to actually make their computer do useful stuff, something that previously they had very little chance of accomplishing. Much the same way that Stable Diffusion allows people with little or no artistic ability to make art (well, the "art" part is debatable, much the same way that Openclaw gives people legitimate technical ability is debatable).

- i use it for automating routine admin tasks stuff like checking logs, restarting services, that kind of thing. It's like having a junior sysadmin that never sleeps.

- Tl; dr - "I made a cron job that checks a queue and does the thing in the queue." Fucking revolutionary

- ## 360安全龙虾是基于 OpenClaw 做的一个封装，结果在安装包里，任何人下载后都能直接访问到一个用于域名 *.myclaw.360.cn 的 SSL私钥，这个证书有效期到2027年4月，覆盖了该平台所有子域名。
- https://x.com/vikingmute/status/2033528578986721457
- 这锅不能全给360。很多开源封装都会踩坑：测试证书打包进生产。根本是缺 secrets 管理——应该用 Vault 或 K8s Secrets 动态注入，而不是硬编码。不过通配符私钥直接

- 最离谱的不是泄露，是上线前连安装包静态检查都没过。敢做入口级产品，至少把密钥扫描、证书检查、制品审计做成门槛，不然安全助手先成投毒入口。

- 肯定不是AI写的，AI可严谨了

- ## [Unpopular opinion: Why is everyone so hyped over OpenClaw? I cannot find any use for it. : r/openclaw _202603](https://www.reddit.com/r/openclaw/comments/1rteu83/unpopular_opinion_why_is_everyone_so_hyped_over/)
- Good AI isn't free.

- Came to the realization that there’s just not many things it can do to make you a profit if you don’t already have some sort of business scaled. Even then, it’s not actually making you money, it just makes some of your tasks easier/automated. EVEN THEN, what it can actually do in terms of tasks is pretty limited by the fact that it can’t really interact with most of the internet.

- ## [QClaw 内侧码发下来了 - LINUX DO _202603](https://linux.do/t/topic/1760089)
- WorkBuddy不能自定义模型，用的是云端，qclaw是在本地跑定制版openclaw
- WorkBuddy 是腾讯自研的桌面 AI 智能体，兼容 OpenClaw 生态，更简单易用。

- 微信如果不支持md 他也没什么用呀，好歹qq机器人支持md

- ## [为何今天国内openclaw大爆发？各大头部企业，甚至地方政府都在推 _202603](https://linux.do/t/topic/1715483)
- 龙岗和无锡在发激励，腾讯和字节在争入口，其他的厂在争报表

- 求经济发展啊找到, 任何刺激点都是大好事, 固件要钱, 软件也要钱

- https://x.com/hankinbeijing/status/2030944394057306438
  - 龙岗AI署推出龙虾帮扶政策，抛去表面的紧跟热点，其实是为了：
  1. 解决就业难题（OPC，一人一公司，失业人口练龙虾当老板）；
  2. 卖NAS（已有专属品牌+型号+折扣价了，就差明说利益输送了）；
  3. 解决算力补贴难题（完全没有大算力扶持基模/行业模型，但的的确确掏得起小钱给全民发龙虾训练券）。
- 能覆盖的就业太少了
  - 谁说不是呢，先摆出一副解决就业的架势再说。

- https://x.com/PandaTalk8/status/2031214797707251840
  - 好多人没有缓过神来。 为什么全国各地级市都在鼓励搞小龙虾产业。  
  - 实际上这真就是电视剧里的那句台词： “上利国家，下利你们。” 。  
  - 第一，中美之间的AI竞争，进入到了第三个阶段。 第一阶段是AI能力之争， 第二阶段是AI成本之争，第三阶段AI应用之争。  谁能在这轮科技革命中胜出，谁就能主导未来的全球经济增长。  
  - 第二，OpenClaw 不仅仅是一个AI 智能体。 它是一个平台。 它会提供一整套的围绕着skills 生态的玩法， 它会重塑我们生产和生活的方面面。  
  - 第三， 提振消费。  大模型算力、软件、硬件、教育培训都会有新的需求产生。 如此一定会促进各地发展，缓解就业压力， 刺激消费， 为各地增加财政收入。

- 政府是为了跟上面申请拨款，总要有个项目仅此而已。

- ## 🔥 [为什么现在OpenClaw如此火热 ](https://linux.do/t/topic/1714317)
- 很正常，一个小龙虾可以带ai+，vps这一大堆业务。估计声量会比元宇宙啥的高得多
  - 小龙虾感觉就像卖铲子的赚钱了，铺天盖地的宣传

- https://x.com/macrotradecn/status/2031009507007246443
- openclaw 流行的结果：
  1. Apple 很开心，因为 mac mini 又疯狂销售了一波
  2. 作者很开心，有了知名度也加入了 OpenAI，赚的盆满钵满
  3. OpenAI 很开心，收编了作者，GPT 5.4 加强了电脑操作更蹭了一波热度
  4. 其他大模型厂家很开心，因为 openclaw 很费 token，又卖了很多 API，而且 openclaw 越火，就能拉来更多的投资，何乐而不为？
  5. 云服务器厂家很开心，弄了一键部署，很多人尝鲜养虾会买一台服务器试试
  6. 黑客很开心，大部分也挺开心的，因为觉得自己也能当老板指挥 AI 员工了，和别人也有谈资，仅限于自己的龙虾没出事
  - 一圈下来，大家都很开心，大家都有光明的未来。至于龙虾是不是屎山代码，谁会在乎呢？

- 像极了当初各种部署deepseek

- 这一波下来，只有保守派程序员悲伤的世界达成了

- “说一句话，事情就办好了”，这正是长久以来人们对 AI 的期待。从最初的 Agent 概念，到如今的 OpenClaw，某种程度上，OpenClaw 已经成功兑现了人们对未来 AI 的一种想象：它能替你做事，全自动运转，并且具备高度智能。它不再像传统 LLM 那样，问一句答一句，只能被动响应；而是一个能主动理解意图、拆解任务、调用工具并独立执行的智能体。 从这个角度出发，再加上有大量人为的炒作，OpenClaw能够爆火也在意料之中。

- 因为他们能拿到更多的数据 这简直是白来的

- ## [我看了L站大多数关于 OpenClaw 的帖子，发现一个诡异的现象 ](https://linux.do/t/topic/1713268)
  - 99% 的教程都在教你怎么安装、怎么部署、怎么过验证、怎么解决各种奇葩报错。
  - 只要一装完，看到个 Success 或者跑出一个网页界面，教程就戛然而止了。
  - 至于这玩意儿装好以后，具体到底怎么用？能解决什么实际痛点？—— 几乎全网没人提及，仿佛这是一个不可告人的秘密。

- 这玩意说实话，不如claude code跟 codex 实用，一大堆配置飞书，配置skills，玩了一两天就吃灰了，codex直接啥活能干了，自己安装skill，自己去操作浏览器

- 我现在能找到明确的应用场景只有客服 ，还有什么实用的推荐吗

- 已经变成我的闹钟了: 龙虾龙虾，提醒我8点拿快递
  - 其实让龙虾在手机上会比电脑上更类似于个人助手的概念。用拿快递举个例子：手机在我下班的途中，打开手机的时候提醒我到了x个快递，分别在xx地址，是xx东西，经过驿站的时候手机提醒。而现在电脑只能定时推送。我比较期待下一个豆包手机。
- 但是手机自带的ai会直接给你推送快递到站，点击就能看取件码。遇到任务安排直接按一下侧键，自动进日程。根本就不需要对话，搞不懂为什么要用一个不那么可靠的对话ai
- 我一般用小爱同学，不需要特殊配置，还能语音设置。

- 是这样的，而且每个社区几乎都是这样，gpt5.4 出来后一堆营销号写文章，教你安装，然后到底能干嘛呢？举例子都是什么，创建一个日程，打开一个 app。。。这种事情用 agent 干能有啥意义呢

- 我就想看看腾讯电脑管家出品的QClaw到底怎么处理安全问题的
  - 我看过了，腾讯玩的都是自己内部的接口，自己和自己玩…

- 跟你办的那些健身卡、游泳卡一样，办了就完事了

- [关于openclaw的一个小作文，都是自己最近的一些思考，第一次发长文，不知道和不合规  ](https://linux.do/t/topic/1715302)
  - 龙虾确实能干活，但有个前提——你得先有自己的一套东西给它

- ## [🦞bot真的是风口吗？还是炒作出来的伪需求？ ](https://linux.do/t/topic/1709643)
  - 联想到最近的一些事情和各个大厂都在折腾。如果:lobster: 真的赚到钱，为什么我看不到一个赚到的 ，只有小黄鱼上有一些单子。
- 我感觉是炒的……因为我让虾帮我运营小红薯，模拟人操作……封了。。。。

- 我感觉真是噱头，对普通人来说除了烧token，我想不出任何别的

- 我也觉得是炒作，没什么实际用处。而且token消耗惊人，模型厂商比较喜欢
- 炒作吧，短期是赚token钱，长期让人们养成AI付费的习惯方便以后收割 

- 算。因为很多非程序员的技术员，不会去用cli，他们不关心代码，只关心功能，所以需要龙虾这种交互模式

- ## 🤔 为什么Manus的云端形态都没火成这样, 而openclaw这种本地部署这么复杂的项目火了
- https://x.com/yangyi/status/2029864493296275625
- 云端让你把文件搬过去，本地直接活在你的文件系统里，我觉得摩擦差异比功能差异更致命。
  - 这也是为什么我做牛马ai做本地化而不是云
- 本地部署的ai模型和硬件setup怎么做的?

- 我觉得这个才是原因，manus收费太贵，openclaw本地部署大家都觉得能用低价的模型代替
- 那低价的要能用, 他们干啥非得要高级的
  - 对对，我就是这个意思，适合普通老百姓的一定是低消费的，不一定是最好的
- 对对，实在用不起claude、gpt就换成deepseek v3.2、minimax2.5，或者再差的stepflash3.5、qwen3，能解决实际场景问题才是人民的好AI哈哈，豆包不就是个例子

- 我发现大家都配置不上api, 所以可能得需要做一些低价试用包了

- 最大不同在交互创新。它接入了电报、飞书这样的聊天窗口，用户早习惯聊天窗口是一个“人”的存在，聊天软件里的龙虾给人心理上的突破感。
  - 其次 后端权限全部对它开发，它能像病毒在你电脑里肆意游走，你在聊天窗口吩咐的事它是真能干
  - 相比这点，云端的manus就像个无能的丈夫，只能嘴上输出，没法真干
- Manus可以选择开放什么，比较安全，像个有能的丈夫， openclaw像黄毛，不管你开不开放反正我开放就行

- 很明显是manus没有办法给各方充分分配利益，大家都玩不起来。openclaw部署的模式，养活了mac mini，虚拟机厂商，个人装机者，让多方都觉得有利益，大家就用脚投票了。

- 你愿意把你的密码 信用卡交给这些人吗? 如果无法处理这些敏感数据, 云端Agent 就说空中楼阁, 在各种厂干过的人都知道, 他们可以随意看你的对话记录

- 我感觉 Claude Code 还有 OpenClaw 还没出技术圈，或者说还在泛技术圈这个范围吧，基本上还没到普通用户手里。
  - 技术圈用户的 ROI 思维非常高，他们觉得一个东西如果不够开源、不够好用、不够有选择，那就不太行。
- 至于你说的云端模式，其实很多都是云端模式：
1. Claude Code 早期出了云端 CLI，你可以在它的服务器中运行 Claude Code。
2. CodeX 一开始也是这样推出的。
3. Perplexity 也有它的 Computer 模式。
- 这些模式都是存在的，也有一定的用户量。但目前最火爆的肯定还是 OpenClaw 这种，它最核心的优势在于自主性太强了。它比Manus 好的地方在于：
  - 不需要充值Manus（订阅费）。
  - 用户可以自己出成本（按需支付）。
  - 自主性极强，很多事情都能做成，当然也涉及卖 Token 的逻辑。

- manus永远是别人的 openclaw 大家觉得是自己的

- 跟 IM 打通、自我创建 skill 的能力，让它活了。个人可以自由的添加各种skill，打造适合自己工作、生活的个性化agent工具，并且用移动IM就能操控一切，获得的成就感是云端商业agent不能比拟的。

- 两个我都用了。1，Manus太贵，OpenClaw我可以用原本Codex的额度，钱省了不少；2，OpenClaw能扩展连接本地电脑数据和软件，能做的事情一下子就比Manus多了

- 首先因为进门是免费的，to C 引流肯定还是要领鸡蛋
  - 其次因为天生带梗，安全做的差、代码写的烂，这些都不是事

- 因为原来模型能力不行，openclaw 正好卡在这个临界点上诞生了

- Agent本地运行才是未来大势所趋，Qwen3.5的发展趋势看出本地部署大模型，跑agent才是未来大势。优势：1 低成本 2 隐私

- 8gb内存的云端vps，一年的费用都可以买两台16gb内存的mac mini了

- 通用agent本来就应该本地化，它的执行效果可以直接通过改变本机环境来体现而不受限于网页界面交互。大多数有趣的应用也只适合本地跑呀，比如让agent帮你玩耍最新的各种AI模型。

- 原来用cc，一个痛点是离开电脑时用不了，试了happy，也试了让cc模仿happy写了简单的转发，体验总是不好，龙虾很好的解决了这个问题，手机可以随时操作电脑上的agent，想到什么需要agent的事情，随时拿出手机就可以办。coding plan完全没有闲着。现在的痛点又变成了，国产模型太拉，想用好模型，

- https://x.com/0xLoki_Zeng/status/2030123523335950680
- 云端文件的可操作性、可编辑性、可定制化都太低了。Openclaw通用太多。
- 其实就是manus成本太高了

- ## [Openclaw是不是纯属炒作？ ](https://linux.do/t/topic/1704768)
  - 感觉是大模型厂商的联合营销，因为现在股市ai见顶了，融资断裂，通过这个骗用户充值token。实际使用就是一个玩具没任何实际作用。自己二次开发claude code也能实现一模一样的功能。

- 你见过什么纯炒作的项目挂着5K+的issue，几K PR，每隔一两天进化版本，每天几百个commit。人类历史上前无古人。

- 被你发现了，个人用户本来是很少量使用token的，这个openclaw正好就是一个让个人用户付费token的最好契机

- 你自己动动手就能干的事，然后非要用这东西，其实实际上啥也干不了，基本上各家也封的死死的，比如什么领劵、什么操作，你在服务器上怎么干？我当时最大的想法是拿来远程写代码，这个可能是唯一有点用的地方了
  - 远程写代码拿个有web的ssh client不就行了

- ## [想请问下为什么openclaw火了而opencode没火 _202603](https://linux.do/t/topic/1705856)
  - 似乎两者都可以skill，操控命令行，接入其它app，甚至角色扮演感觉都没问题
  - 我个人基本上不用他编码功能而是自动化运维

- 两者的共同点只有AI驱动且能接入skills、MCP等以及操作文件的功能ww，
  - 像心跳、接入平台(discord、telegram)、主动推送都是opencode做不到的，或者说是没有特别去包装成开箱即用的，让小白来用就是一脸蒙
  - 倒不如说kilo code跟roo code同样都是编程cli工具，为什么opencode能比他们火十倍呢
  - 能让openclaw去操作opencode，所以openclaw比较火是应该的

- opencode挺火的啊，不过仅编程领域，自然比不上openclaw

- opencode偏编程 龙虾适用性广 市场需求不同吧

- 一般管这玩意叫出圈一但出圈，外部流量自然会把你捧起来, 很明显龙虾这个赛道还没第二个出圈的，流量自然都流向它

- opencode在编程圈基本都知道啊，只不过openclaw有人营销，程序员一般都比较穷:joy: 都是口口相传

- 个人理解，关键是低成本入口，我看的大多数教程，安装openclaw 和接入飞书是必须的部分，如果没有一个低成本的入口，每次都要开网页估计也没办法炒起来。话又说回来，微信挺尴尬的

- 龙虾是宣传可以让AI操作电脑，并且可以通过社交软件随时随地让它干活。而opencode是开源替代cli，两者一开始定位不同。可能龙虾的“自主操作电脑”更有流量，加上之前的龙虾社区，这便可以产生更多的话题，自然就火起来了

- opencode定位是编程工具，openclaw定位是个人助理。openclaw会记得帮我安装过哪些东西，有哪些东西可以调用，我手机上就可以指挥它操作我的服务器（opencode可能也可以，但我不清楚），比如说我最近要用ai生成5分钟的视频，我直接发需求给openclaw（有grok2api），过一会完成了就把视频发我了。opencode我没试过，更多的还是把opencode当成cc类的编程工具在用。

- ## [How to allow Openclaw to read files content? ](https://www.answeroverflow.com/m/1471366269742747892)
  - Below is openclaw replied to me: I don't have direct filesystem access in this session to read local files. I sent a request to try to access it via another session, but it timed out.
- directly — that path is on your machine, but the bot/session you’re talking to is running on someone else’s Gateway host. So it has no filesystem access to your laptop/server for security + architecture reasons.
  - If you run your own Gateway locally (same machine as the file) Then the agent can read local files (via the Gateway tools) — easiest path is usually: - copy/move the file into your `workspace` and ask the agent to read it from there
  - If your Gateway is remote (VPS) but you want access to your computer’s files Pair your computer as a node. Then the Gateway can call node tools on your machine and you can cat /inspect files through that node.
  - If you’re using Docker sandboxing and the file is “outside the sandbox” Bind-mount the folder into the sandbox
- if i save files in `workspace` folder, how do i instruct openclaw to read it
  - If the file is on the same machine as your Gateway and inside the configured workspace, you can just tell the assistant the path and what you want done.
  - Read documents/Web_search and QMD knowledge.txt and summarize it.

- ## [Openclaw with Small local model : r/LocalLLaMA _202602](https://www.reddit.com/r/LocalLLaMA/comments/1r24264/openclaw_with_small_local_model/)
- Even large hosted models struggle with agentic/tool-calling programs like Openclaw. The smallest local I've seen that can do somewhat reliable tool calling is IBM's Granite models. In the 14B range Qwen is OK. I've heard Mistral models also work but I haven't had much luck with it myself. 30B+ models are what I stick to for tool-calling but you're going to need 24GB VRAM for good speeds.

- I tried to run some, the gemma3:4b run great on my GPU with 6GBvram (for text/vision) but when tried to use openclaw I got the output that the model does not support tools. I did tried qwen3-v1:8b and it did respond in 4 minutes.

- I have an Nvidia with 8GB and use gemma3:12b as the model, which just fits into the memory. As far as I understand, the model cannot handle tooling or agents, but I have a small agent script running (not Openclaw) that I can communicate with via Telegram and that performs tasks. 

- Qwen2.5-7B-Instruct-Q4_K_M.gguf is working to run everything that a higher level model has setup. I trust it with heartbeat and corn jobs and other items. The Qwen2.5-1.5b-instruct-q4_k_m.gguf responds but doesnt seem smart enough for most tasks. I experimenting with it to run heartbeat and low level tasks.

- ### [My experience with local models for Openclaw : r/LocalLLaMA](https://www.reddit.com/r/LocalLLaMA/comments/1qwm3wk/my_experience_with_local_models_for_openclaw/)

- ## [你们都用 OpenClaw（Moltbot、ClawdBot）实现了什么有价值的功能？ - 知乎](https://www.zhihu.com/question/1999842555244860056)
- 
- 
- 
- 
- 
- 
- 
- 
- 
- 

# discuss-ai-pm-cowork/office
- ## 

- ## 

- ## Codex App Server is 100% Open Source _202603
- https://x.com/reach_vb/status/2036904822641676716
  - It allows you to build on codex and build richer experiences all with ChatGPT Auth

- 🤔 codex的api及风控政策经常调整, 一定要添加备选方案

- ## [What’s with the hype using Obsidian and Claude Code : r/ClaudeCode _202603](https://www.reddit.com/r/ClaudeCode/comments/1s0m3rf/whats_with_the_hype_using_obsidian_and_claude_code/)
- Code is files, obsidian is files. Same thing 

- Claude Code works best when it has structured context about your project — conventions, architecture decisions, what's already been tried. Obsidian gives you an easy way to build and maintain that knowledge base as markdown files. It's less about Obsidian specifically and more about having a system for context that survives across sessions.

- Unnecessary, I created a file called handoff, updates twice a day, and a command for Claude to read it first when we start working.

- [Can someone help understand why what is the benefit of using Obsidian with Claude Code ? : r/ObsidianMD _202603](https://www.reddit.com/r/ObsidianMD/comments/1s1zrg8/can_someone_help_understand_why_what_is_the/)
- Until recently obsidian was an easy way to have local storage and viewer of markdown files generated by Claude, but since release of CLI you can turn Obsidian into very powerful memory/logic system for Claude code. 
  - To really understand why obsidian is good for Claude you need to stop thinking that you are the main user, that sad there are alternatives and Claude itself could build such a system, but it is kinda strange to reinvent things when they kind of work out of the box
- I record, transcribe, and summarize all of my meetings and use Claude code to give me insights on those files.
- i use it to play TTRPGs with Claude Code. The Vault helps alot for Claude for generating content for a campain. also: session-logs, npc-notes, bestiary and so on.
  - i think its the persistency of context for Claude you can achive with an obsidian vault that makes people want to experiment.

- ## Introducing the Readwise CLI. 
- https://x.com/readwise/status/2034302848805241282
  - Anything you've saved in Readwise (highlights, articles, PDFs, books, youtube, newsletters) is now instantly accessible from the terminal.
  - The Readwise CLI/MCP work great on their own, but we've also created a readwise-skills repo that shares some powerful skills to use with them
  - https://github.com/readwiseio/readwise-skills

- ## 我发现vibe coding出来后，小东西多了很多，但是超大型软件还是很少，比如我没看到一个人vibe一个Office出来。难道超大型软件有什么护城河吗？
- https://x.com/cherylnatsu/status/2033388509583860033
- 那是你没有软件工程的概念，写出来是一回事，能用是另外一回事
  - 我只是个产品经理，只管要效果，怎么实现我不管
- 要一个五颜六色的黑

- 理论上能做出来，但是到能用以及能被别人一起用是大距离的, Office的核心价值是它那套格式标准

- 个人用户不具备编译巨型软件的物理能力。 3A 游戏为例，一个最基本的基于 Perforce - TC - ArgoCD - JFrog 的多平台 CICD 集群开发建设成本最低在 50 亿日元左右，这还没算持续的人力开发成本。 Vibe Coding 解决不了哪怕 1% 的问题，顶多让 TC 和 ArgoCD 里的配合和管线写的更舒服点。

- 因为没有必要，举个例子，你去买sap的东西经常是只需要它的1-2个模块。   或者wps/office，你每次都只需要其中30%甚至更少的功能。   vibe coding时代大家制作的工具是高度基于自己的工作流/需求定制的。  不是以前造工具的大中台、场景抽象+功能堆叠方法。

- 大型软件的复杂度本身是护城河的一部分 比如可以vibe一个单独的功能 但是想1000个功能互相组织影响本身有复杂度

- ## [【开源】一站式论文搜索、精读、写作、AI辅助写作，佬们走过路过来瞧瞧 - LINUX DO _202603](https://linux.do/t/topic/1752324)
  - 检索论文的版块，目前用的是OpenAlex的源，后面会适配上arxiv等
  - 作为史诗级缝合怪的素养，别人有的一个都不能少，然后我也注意到了有部分佬友可能会对论文扫描件的AI助读的需求，所以最后选了surya-ocr来帮忙解析文档
  - 因为word特殊性，目前还没找到合适的方式怎么让他导出好，但是latex天生模板随便换的优越感直接就来了。所以目前支持latex的基础骨架的导出

- [论文格式排版快捷修改工具   _202603](https://linux.do/t/topic/1753287)

- ## [[分享] GoRabbit：本地优先的 AI Agent 桌面平台（开发内测中） ](https://linux.do/t/topic/1684941)
  - 主要目标是： 让 AI 不只是聊天，而是能像一个「可编程助手」那样，真正替你干活。
  - 一句话概括： 桌面端 + 多模型 + 工具调用 + Agent + 记忆系统 + 自我学习规划决策，完全本地可控。
  - 基础功能已经可用：多模型、多 Agent、工具系统、记忆系统、权限控制等

- ## 🤔 [Is the Codex app basically just a CLI wrapper? : r/codex _202603](https://www.reddit.com/r/codex/comments/1rgxpbm/is_the_codex_app_basically_just_a_cli_wrapper/)
  - Trying to understand how the Codex app is structured here. Is it essentially a wrapper around the CLI, or does it have its own separate update cycle and capabilities?
- pretty sure the app is a gui for the codex cli's app-server mode. i couldnt get voice working right with appserver atm but everything else works the same.

- App and cli are both wrappers for the api I think. All three are likely versioned independently, though api updates will obviously impact both tools

- not really. there is a shared app server and the CLI, extension and app are wrappers on that

- ## 感觉 openclaw 在企业端的需求非常强，而且我看好 local first 而不是 cloud first 的落地路径，因为几十人的组织到头就相当于几十个 agent，单体设备完全够了，且就应该放在它所替代的人的桌上。
- https://x.com/ewind_dev/status/2025971612470931755
- 龙虾不是对 Mac 支持最好吗？用 Linux 是有别的优势？
  - 我在给一个几十人团队里所有人每人开一或多个独立的 agent 实例，相应的容器能力感觉还是 linux 上配起来最简单。
  - Mac 的优势应该是对 C 端用户能便捷地访问到相册日历和备忘录这些数据，但对团队这些全在飞书和 codebase 里，这样 Mac 就感觉没啥特别优势了，且 GUI 虚拟化还卡得特别死
- 在企业场景如果不是涉及到 iOS 开发，Mac 的确没啥优势，不如 Linux 节省资源和丰富的软件包

- ## [AnythingLLM Desktop works across your entire OS with local models : r/LocalLLaMA _202602](https://www.reddit.com/r/LocalLLaMA/comments/1r8biu3/anythingllm_desktop_works_across_your_entire_os/)
  - Today, we released AnythingLLM Desktop v1.11.0 and it is a step towards our new direction that becomes more of an extension of your OS and less of a sandboxed app.
  - Now with a simple customized keybind you can open an overlay that instantly has access to your open apps and screen. This works for both multi-modal but also non-vision enabled models.
  - This functionality is all on top of all the stuff people use AnythingLLM for already: Chatting with documents, RAG, agents, MCPs, and more. This panel also has awareness of any Meeting transcripts you might have too!
  - This is all done using on-device models and pipelines - using a local model you can have a fully on-device experience. In that demo I am using Qwen3-VL 4B Instruct (Q4) on a Macbook M4 Pro but you can really bring in any model or provider you want.
  - We also have an OSS MIT license multi-user server based version of AnythingLLM if you are looking for something more hostable on a VM or something.
  - When you drag a file into the window (what type?) it parses them and adds them to the model. You can press CTRL/CMD+F and see the exact documents + token window usage of all documents. I am certainly able to drag and drop files and it certainly is pulling specific information out of them as well
- The installer is only ~400MB. Are you on Mac or Windows? The majority of the footprint likely is the meeting assistant stuff. We now have the installer ask first before pulling the model if you know youll never use it. We can do the same for the whole feature as well.
  - Then the other big bit is Ollama's CUDA/RoCM backend - which without will just have the built-in models run on CPU only.
  - I do plan to move the entire installer away from the old installer method and instead have the "select features" kind of UI where you can pick and choose what you want to install during setup - which then should get you to where you want total bundle size.

- How do you guarantee your solution against malicious prompt injection? If it has access to the entire computer, the fact that it's local doesn't guarantee data extraction.
  - It does not read your screen passively
  - "agentic" tasks that call APIs and do things like that require "@agent" in the prompt - this keeps regular chats and agentic chats separate within the same thread. AnythingLLM has always done this.
  - So the only way to prompt inject yourself and do something is to entirely execute a full self-own and really force it to happen. Its a non-issue.

- ## Interpreter. It's a desktop agent that can fill PDFs, edit your Excel and Word docs, and learn new skills. _202602
- https://x.com/hellokillian/status/2024227639087813035
  - Runs offline, works with any model, and it's free.
  - [Interpreter: The Desktop Agent](https://www.openinterpreter.com/)
  - my work is just more "files first" so wanted something that wasn't so chat-first. will extend this beyond office docs soon.

- 🐛 
  - 不选择文件的普通chat，无法查看历史

- does it handle multi-step tasks across multiple docs, or is it one file at a time?
  - multi-doc to the core. this was why we decided to bring the office editors into the app (as opposed to an Excel/Word extension) — so much work happens across documents
  - the agent is multi-doc, and the interface supports multi-pane layouts, so you can also be multi-doc!

- How do you see the interactions in the coming years? I believe we will possibly have a central database with logic for interacting with it.
  - I think of it the same way! most of the apps I use every day are simple structures under the hood:
  - contacts, notes, calendar, email, many more— are arrays of objects.
  - I imagine it becoming pretty annoying that they each have their own GUI and can't talk to eachother. 
  - the primary form of interaction might just be through an agent, which is capable of displaying those objects + some interactive controls for fast/granular manipulation.
  - exactly how we're approaching interpreter :) agent on the right, objects on the left, interfaces in the middle that the agent or user can control.
- Totally agree. And I think this applies to both B2C and B2B. Think about real daily workflows: you interact with calendars, finances, tasks, notes  and even when we connect these through APIs, there's still a fundamental piece missing: a central place where the relationships between things actually exist.
  - B2C example: a person has calendar, bank, notes, emails. Each app holds a piece. But none of them knows that "Tuesday's meeting is with the client who owes you money and who you noted last week is unhappy." That relationship doesn't exist anywhere.
  - B2B example: a company has ERP, CRM, logistics, finance. The same customer has a different ID in each system. Nobody knows that the customer who's buying less (ERP) is the same one who gave a low NPS (CRM) and received 3 late deliveries (logistics). The data islands exist, but the relationships between them don't.
  - What I believe: the future is a central database (SQL, graph, whatever) where the entities and relationships of a business or a person's life are actually modeled. The rules and connections live there. And the agent consumes that to act with full context  not stitching pieces from N apps together, but reading from a unified ontology.

- ## Codex app is out for mac
- https://x.com/sama/status/2018414858015039504
- cons
  - 不能添加文件夹

- ## [Claude Co-Work is....meh unless you code : r/claude](https://www.reddit.com/r/claude/comments/1r6a11x/claude_cowork_ismeh_unless_you_code/)
  - I genuine tried to give this thing a shot. Outside of coding, its kind of just a glorified web-app that you can install locally.
  - Browsing the web? Unless its plain text, it struggles, fails, times out, gives up.
  - Want it to download files/pdf's? Nope. Can't do that, do it yourself.
  - It also regularly fails to find folders. How do you not see DOCUMENTS on a mac? Its right there...
  - It can't open more than one tab at a time.
  - It is stupid slow on all models.
  - At the end of the day, what ever you are doing on claude that isn't code, there is very little reason to pay to get cowork. It's not going to do anything it advertised if you aren't coding standalone agents.
  - Over all, it has potential, but in its current form, its too slow, too naggy, too annoying, too useless.
  - Being advertised as an actual "co-worker" you can hand off a bunch of work to and f *** off and come back and its mostly done, is so far from reality its not even funny.

- Co-work is great, to be honest. If they cancel that, I’ll drop my Claude subscription. I use it to write confluence docs, edit pdfs, word docs, create contracts, amend them, do P&l stuff, powerpoint presentation, even google slides via chrome mcp. You’re using it wrong OP.

- I think the idea is that many more non coders in the near future will do small coding activities in their jobs. If that’s not you, it’s not for you. But it might be for your replacement
# discuss-ai-pm-browser
- ## 

- ## 

- ## 

- ## VS Code is so much more than a dev tool these days. With the integrated browser Copilot is my aviation weather tutor.
- https://x.com/joshspicer_/status/2043420770832130347
  - It opened http://aviationweather.gov, navigated through a dozen forecast charts, and systematically explained HOW to interpret this crazy weather in the PNW today

- ## You can vibe code your own "New tab" page in Chrome. I have turned mine into the ultimate solution to the "too many tabs" problem
- https://x.com/zarazhangrui/status/2043415572688629937
  - See all your tabs with clear titles, grouped by domain
  - Closing any tab gives you "swoosh" sound and confetti effect
  - "Easy wins" grouped together: homepages, localhost tabs... batch-close them with one click
  - Duplicate tabs detected; close duplicates with one click
  - For tabs you're not done with, save it for later in a checklist
  - This is the Marie Kondo method for browser tabs
  - https://github.com/zarazhangrui/tab-out

# discuss-ai-showcase-apps/products
- ## 

- ## 

- ## 

- ## 

- ## 🎞️ [有哪些知名的AI套壳项目值得推荐 ](https://linux.do/t/topic/1689853)
  - 想做一个类似 pollo .ai 的项目，提供一些视频模板，传自己的角色或者场景，生成宣传视频，有没有合适的开源项目做二次开发呀？

- 站内有两个开源的短剧/视频生成平台，可以参考下
  - [免费开源！已经盈利的AI影视/短剧agent制作系统 waoowaoo  ](https://linux.do/t/topic/1670000)
  - [ai火宝开源 ](https://linux.do/t/topic/1521682)
  - 另外还有些 Skills，可以通过关键词短剧进一步了解

- ## [一个在浏览网页时扫描内容是否由AI生成的油猴脚本 ](https://linux.do/t/topic/1641840)
  - https://textoracle.h-e.top/
  - 爬了一些不大的数据集，训练了一个可以判别是 AI 还是人类的模型
  - 由于训练数据不大，并且力求快速响应，所以存在不少误判情况需人工核查
  - 由于训练数据不大，并且力求快速响应，所以存在不少误判情况需人工核查

- 后端算法是用 LLM 吗？或者是 BERT 这种检测模型？是 LLM 佬友能不能分享一下提示词
  - 是 BERTw

- 感觉不错，但是一些短文本就没必要检测了吧，短文本检测准确度一般都不高，检测意义也不大，还浪费计算资源
# discuss-monetizing
- ## 

- ## 

- ## 

- ## [After 3 months of building MCP servers for free, I finally figured out how to monetize them : r/mcp](https://www.reddit.com/r/mcp/comments/1rjqjkj/after_3_months_of_building_mcp_servers_for_free_i/)
  - I built a bunch of MCP servers — web scraping tools, data enrichment, a PDF parser — and just... gave them away.
  - MCP is incredible for connecting tools to agents, but there's no native way to say "hey, this tool costs $0.01 per call." So I went looking for a solution that didn't involve building a whole billing system from scratch.
  - Found this project called xpay — it lets you charge per-call for any MCP tool.
  - it lets you monetize any MCP server without changing your code. Seriously, zero code changes. You paste your MCP server URL into their dashboard, set a price for each tool, and they give you a proxy URL like: your-server.mcp.xpay.sh/mcp
  - Agents connect to that proxy URL instead of your raw server. When they call a tool, xpay handles payment automatically before forwarding the request to your actual server. Your server receives the exact same requests as before — it doesn't know or care that there's a payment layer in front of it.
  - That's it. No SDK to install, no payment code to write, no billing infrastructure to manage.

- A solution looking for a problem IMO. If people are technical enough to plug in MCP servers they are likely technical enough to find a free and equally secure one through the countless repos out there. And if it doesn’t exist I’m sure people are figuring out you can pretty easily vibe code these things (I think I recently saw a post for an mcp server that can build out other mcp servers? Now that’s a neat catch-all idea).

- Cool proof of concept nonetheless. I can scrap together an MCP pretty quickly but if you can set up decent infra around it so MCPs are more efficient, fail less, or any other value add I could see it being useful. Not maintaining it is a value add as well.

- This sounds fucking awful and a security, PCI compliance. Billing, and all around nightmare.
  - Answer to original question, yes we charge for our MCP servers. We control their access and route view a platform that is the "entrance" to the MCP servers and tools and handles authentication at the company and user level (fully multi-tenant from the start) and bill for access to the suite of MCP tools. The user brings their own API key or user credentials depending on the MCP server/tool they are connecting to. Our cost is the cost of development, maintenance, and the Azure infrastructure for hosting
# discuss-ai-iot
- ## 

- ## 

- ## [So AI NAS category is a mess and i don't understand why nobody has fixed the obvious problem : r/LocalLLM _202603](https://www.reddit.com/r/LocalLLM/comments/1rtey5z/so_ai_nas_category_is_a_mess_and_i_dont/)
  - current landscape as i understand it:
  - Synology and Qnap: mature software, terrible hardware for AI, their "AI features" are embarrassing compared to what you can run locally on a halfway decent GPU, they're selling NAS boxes with NAS CPUs and calling it AI ready
  - minisforum and that category: genuinely interesting, the new ones with ryzen AI chips are not a joke, but the storage story is weak and they're clearly a PC company trying to figure out the NAS side rather than the other way around
  - zettlab: pretty hardware, their OS is still rough, saw a review where the reviewer said the AI features required too much manual setup to be useful for non technical users, also no real GPU expansion
  - DIY: this is where you end up if you want something that actually works but now you're maintaining a server and that's a part time job
  - the product that should exist is a tower that treats local AI inference as the primary purpose, has real GPU expansion, has real storage capacity, has software that's designed for actual workflows not demos, and doesn't require a homelab hobbyist to set up

- From what little i know nas is network attached storage. That has a weak cpu, maybe modern ones can run some supermega lightweight stuff on it. If you want ai inference, you build a server out of a new ryzen shared memory chip, slap on 128gb of ram and it can happen that you attach a das to it so has huge storage also. If you try inferencing on a raspbery pie your options are “limited” on what llms you can run… but at that point your smarphone can handle better llms which are still mostly useless.

- NAS by its nature doesn’t need high-performance hardware. Just buy dedicated server for AI and leave NAS to be just storage server.
  - I certainly don’t want my nas to be built for AI, it would make it unnecessary expensive and power hungry to run for what is something I will be using less than 1% of the time. I want cheap energy efficient quiet box to store files not an electric heater that sounds like a jet taking off and costing more in electricity than it’s worth.

- You are better off having a normal NAS and an inferencing machine that pulls from it. That way, you aren't maxxing out your GPU when you're just pulling an image or two.
# discuss-ai-coding 🔡
- ## 

- ## 

- ## 

- ## 

- ## 
# discuss-ai-pm
- ## 

- ## 

- ## 

- ## 

- ## agents 产品开始进入一种很诡异的阶段，大家都在寻找有钱人或有钱企业买单。
- https://x.com/lifesinger/status/2050405884862538055
  - 因为大量 agents 产品，真正好用的，依赖的模型都很贵。说得好听一点，各家可能都处于 PC 的早期。说得难听一点，大家都在造长期没啥用的奢侈品。
  - To C 产品里，豆包最牛。彻底贯彻移动互联网的增长逻辑。有钱就是好，但是否靠着有钱就能走到终局。未必。
  - To B 的大量 agents 类产品，以及 AI infra 产品，很诡异。更多是利用企业对 AI 的焦虑情绪在促进营收。以及中间有大量 To B 产品利用的就是 AI 创业公司本身的焦虑，比如增长焦虑等。
  - 最稳着赚钱的，是做课程、是企业咨询、是面向有钱人的心灵抚慰。唯一不足的是时间不够用。有意思的是，有部分 agents 产品也盯上了这一块。
  - 以上观点，有个巨大的偏见：看不起有钱人。不应该。
  - 但内心深处，总觉得，有人为有钱人服务，就得有另一波人，能为非有钱人服务。
  - 世界很奇妙。充满不知道。

- 对豆包我有一点不同的看法。单看这个产品，肯定是纯亏钱。但是字节系有一个特点，他的产品矩阵里有抖音这个利润收割机。只要豆包的用户和字节系内容消费类产品的用户有重叠，那么把豆包当做一个用户粘性的入口就可以接受亏损。相当于可以收一个新时代的互联网广告费。

- 我就在给企业提供AI咨询，我看到一些头部企业的焦虑，我的切入点是把开源AI方案介绍给企业，按我的品味给一套方案。企业也不傻，通过这样的高密度知识蒸馏获得一些启发也是一种尝试。

- 非常赞同“面向有钱人的心灵抚慰”，其实有钱人用AI也不是说真能带来多少收益，但是至少是得到心理安慰了：自己没有被时代淘汰

- 当前的AI项目最好的组成是，AI产品+AI媒体。 个人体验来讲AI媒体内容和课程企业咨询也能部分用AI 提效，虽然组织构建部分做不到AI First，但是从赚钱的角度来讲媒体+咨询部分的ROI 提高了很多。如果有时间其实值得尝试

- 先把钱赚了也行哈哈哈。也可以针对不同模型的特性开发产品。比如我最近感觉的就是v4就非常适合改文稿格式因为高缓存命中够省钱，gpt（可能因为训练语料够多）特别适合做客服

- 人类从来都是为了解决问题而付费。agent只要能帮忙解决问题应该就有价值

- ## [思考一个问题就是在目前ai如此火爆的情况下，为什么商用AI的应用如此的少 - LINUX DO _202604](https://linux.do/t/topic/2065309)
- AI项目有的的确很好用，但是很多个人的AI项目，在好用的同时有不少BUG，这种不稳定因素在商用情况下非常致命。
  - 再说商业化的chat2db，AI驱动的数据库管理，之前适配AI做的不行，完全就是一坨答辩，停更了半年，大改版，加上大模型发力，才勉强有了点体验感。

- 总结身边人的应用，大部分生产力的体现还是在辅助层面，coding、堆一些比较水的报告、做简单的工具脚本这样。真正做落地应用，稳定性在现阶段还是存在问题，就拿之前做过的text2sql、AI生成报告这种，都要加很强的约束和人工复核，做不到直接可用。因此定位只能当技术人员的辅助工具，没法直接给到客户侧。

- 如果项目中具有AI生成相关功能，大模型备案的时候需要提交一些测试报告，确保你的模型服务在各个方面都能合规，所以只要过了，后续也不会有太大问题。之前为了弄这些测试数据还特意写了个项目。
  - https://github.com/mllt992/model-test-in-cn /202604/js/vue
  - 基于 Vue 3 + Express 的模型备案数据管理平台，支持 AI 生成内容管理、测试题管理、模型测试等核心功能。
  - Vue 3 + TDesign + Vite + ECharts
  - Express + better-sqlite3

- 不考虑程序功能上的问题，单从政策上来看，个人，中小企业几乎无法（很难）完成项目产品的商业合法化

- 不考虑国内的法律因素，放眼全球也没有什么成功的商业项目吧，目前真正用量大的还是 coding、rp 和基础的 chatbot。openClaw 这种比较火的通用 Agent 还是开源社区驱动的

- 目前最大的商用，就是Claude Code的编程功能。 To B的合规很麻烦。 估计突破口在一人公司这里。

- 除了政策之外，个人感觉现有商用ai应用的瓶颈是token太贵了，用户越多成本越高，之前互联网这套规模效益的方法走不通，只能依靠用户付费覆盖成本

- 
- 
- 
- 
- 

- ## [我始终坚持AI应该和电一样便宜 - LINUX DO _202604](https://linux.do/t/topic/2061865)
  - 我一直认为AI是廉价的，不值得吹捧，任何昂贵定价的AI服务都是在割韭菜，我拒绝任何昂贵的AI服务付费，昂贵的AI服务我从来不使用，亦不追赶任何AI热潮，但是有个AI是例外，DeepSeek。
  - 从去年到现在，DeepSeek v3发布之前大家都不怎么看好国模，但是V3发布后国模以一种罕见的速度提升了自己的实力，当然这些不是重点，重点在于v4发布后DeepSeek性能大幅提升，价格却也大幅下降，这是真正人人都用得起的AI。
  - 一个东西卖多贵，取决于供需，市场对AI预期过高导致那些搞大模型的公司，员工过于高估了自己，看看他们的定价就知道了，但是我相信未来AI会比电还便宜，甚至变成一种免费资源。电为什么不能免费？因为要用现实中的资源去发电，有成本，但是AI呢？除了初期的第一笔服务器投资，后续就是维护服务器运行的电费和人工了，现实世界的资源消耗忽略不计，为什么不能成为免费资源？deepseek的缓存大幅降价看到了吧？1M的tokens输入命中缓存后只要2分钱。
  - 现在有些AI公司为什么敢定高价？是因为过于乐观的市场预期！早晚有一天泡沫灭了你们必须降价到0.0001/M的tokens价格，AI不值得任何吹捧，它的命运早已揭示------和电一样成为廉价的基础资源。
  - DeepSeek是我使用频率最高的AI，不是因为它有多强，而是它够简单，少了胭脂俗粉的高特技外衣。

- 我非常认可你的观点，你记得去给老黄说一下 
- 但是好像外国的电费也不是很便宜吧，话说回来硬件成本在那，老黄现在c端都不上心了

- 我觉得以后价格会接近网络/话费一样，都能用，但要求更好的质量更大的用量就要花更多的钱。

- 价格越高对应的质量和稳定也就越高

- 不可能跟电一样便宜，加工品怎么可能比原材料便宜，不过低端模型确实可以做到几乎不要钱，因为没什么好的市场
- 你觉得电便宜，是因为你在中国，你要去了发达国家，看看俄乌冲突，美伊冲突最高点时候的电价，AI一样
- 如果AI像电力一样人人可用，那么就真正的共产了。我反过来一直持悲观态度，最顶级的AI永远掌握在有资本的人手里，弱智的AI才会像电力一样分给大众

- 训练时候的人工成本、维护成本、硬件成本、试错成本是一个都不提啊。我建议把你的工资跟你的饭钱挂钩，毕竟你只要吃了饭就能干活，后续的都是哄抬物价罢了。

- ## [AI大模型开源的好处在哪里？（对于公司而言） - LINUX DO _202604](https://linux.do/t/topic/2001879)
  - 开源可以争取到更多用户，并且在模型研发抽中“大失败”的情况下，根本打不过其他闭源模型，开源是一种被动的止血战略，可以争取更多用户，回回血，并且让财务把这部分开销算作公司营销费用（bushi）。
  - 对于那些重视信息安全/数据保密的公司，开源模型是更为合适的选项，因为闭源模型的微调费用不菲，且无法保证闭源公司不会使用自己的数据进行训练。
  - 部分公司基于开源模型进行部署，形成了一套固定的workflow/prompt，这一部分具有一定的迁移成本，以后会更倾向于继续使用同一开源模型。
  - 对于亟需融资的模型研发公司而言，模型开源在投资者那边是一个加分动作，更有希望争取到投资。而且，开源模型同样可以根据平台月活等指标向模型用户收取授权费用。
  - 对于闭源模型公司，需要自己购买更多的显卡、电力等向用户提供大规模推理服务，这部分支出会非常大，会导致公司财报难看/负债。
- 感觉也是为了生态, 挑好的 prompt/workflow一般都是针对某一个模型的. 选择某一家的话, 后面也会一直用下去

- 参考meta，如果模型能力不是顶级，转型不开源之后，更没人用了，开源多少还能多点用户

- 一个比较值得追求的点是：占领生态位，方便以后在开源社区内制定规则。试着看看人家Nvidia的cuda生态

- ## [同样都是等待，愿意排队还是愿意低tps？ - LINUX DO _202604](https://linux.do/t/topic/1974772)
  - 不排队但缓慢生成 : 排队但快速生成 = 3:1 

- 低tps至少证明确实在处理我的问题，排队的话，谁知道它是不是把你丢一边不管了？

- ## [BOSS决定自建微型数据中心提供api服务，有没有搞头？ - LINUX DO _202604](https://linux.do/t/topic/1974293)
  - 自建机柜好处是一次性投入，还有灵活性。
  - 提供超高并发的LLM翻译api，使用gemma4等高能力小模型或者特调模型api。
  - 由客户选择模型，提供自定义模型的api，如酒馆用的模型。
  - 垂直领域的模型推理服务。
  - 低价的 agent api

- 100W连个水漂都没有, 一组H100都买不到

- 并非一次性投入，你这投入都不够一次性的, 整点小模型的话你们又没什么优势

- 理想主义坚持理想怎么就被赋予小孩哥的称号了呢？

- 一百万，房租电费都要花不少，不要说租到穷乡僻壤，还有断电啥的能保障服务运行吗，稳定性做不到，谁用你

- ## 试图逆向一个 Youmind 非公开 Skill 的提示词 没有成功, 此刻，我理解了 SaaS = Skill as a Service 成立的可能性
- https://x.com/cellinlab/status/2037464272184242590
- 实际处理是通过调用 API 来实现吧
  - 嗯嗯 可以 这么理解，核心提示词 后置

- 直接复制粘贴了，怎么商业化

- ## 做一个你自己也愿意用的产品，然后不断优化迭代它
- https://x.com/yangyi/status/2032831941016457311
  - 但问题往往是，大多数情况下做了这个产品，自己也不愿意用……
- 你能找到一个自己做，自己愿意用的产品, 至少证明：
  - 你有一个很热爱的事情能干
  - 你懂怎么设计一个产品
  - 你还懂怎么开发出来

- 大部分公司的产品在员工看来就是完成任务，根本没几个人关心

- 最近用openclaw，加一些插件和功能的乐趣简直像是当年在浏览器插件盛行的时候

- 搞到最后花了一堆token还不如别人早就做好的东西蛮有挫败感的

- ## 一个有 web search 功能的 Agent，比大部分 Deep Research 产品都好用。
- https://x.com/ixiaowenz/status/2032680983095554234
- 核心在于你要强制的约束输出格式，加强 validation 的回路。至少能每次都强制做两三轮，效果就会很好。

- 我觉得deep research、coding这种能力，不过是claude code这种general agent harness（包含web search等工具）强大能力的一种展现，模型足够智慧，稍加引导（比如一个skill、knowhow），它就能在垂直领域展露出高水平

- ## 国内大厂争先恐后地养龙虾还不如把自己的主业务写成 cli。
- https://x.com/xicilion/status/2029983875552923901

- ## [【开源自荐】GenQuick：一款具备提示词管理及优化的划词 AI 助手 _202603](https://linux.do/t/topic/1696959)
  - 一句话说清楚：选中文字，按 Alt+1，AI 结果直接插回原位，全程不用离开你正在工作的窗口，本体只有 18MB 左右，内存占用不到 100MB，启动秒开，常驻后台也不心疼。
  - 划词即用，零切换成本，在任何应用里选中文字，Alt+1 唤起悬浮窗，窗口跟着鼠标走，选个提示词就开始处理。结果出来后一键插入、替换、追加，不用来回复制粘贴。
  - 模型随便换，OpenAI 兼容接口、Claude、Gemini、Ollama 本地模型全都支持
  - 能画图， 不只是文本处理，还支持用 AI 生成 Mermaid 流程图、ECharts 数据图、Graphviz 结构图、词云、思维导图，生成完直接预览导出或插入。
  - 全部本地存储，不碰你的数据，所有配置和缓存都在本地，API Key 加密保存，不上传任何东西，用 Ollama 的话甚至可以完全离线跑。

- ## 🤔 国内还没有搞ai+工业制图的吧？创业方向?
- https://x.com/xicilion/status/2029791614206427381

- 👷 最新的WebMCP提供了操作ui的新方法

- 和一个合作伙伴研讨半年了，开放 cad 还是很难很顺畅地 ai 化，ai 能做到生产级别的，最擅长的还是声明式。我们内部在尝试在 markdown 里写 openscad，ai 做得还不错。

- 主要CAD画图，人类语言还挺难精确描述的
- 鼠标点一下的事，用ai要说一堆话

- 游戏渲染，3d，也不行

- ## [为什么您根本不需要OpenClaw ](https://linux.do/t/topic/1696116)
  - 2026年3月3日，OpenClaw 成为 GitHub Star 星标数量历史第一，超越了 React 和 Linux。
  - 闲鱼上 199、499 甚至上万的安装费——对，仅仅是安装 OpenClaw，有的销量甚至已经破了 1000 …
  - 但是我想说，我们不需要 OpenClaw，也没有必要装 OpenClaw。现在不需要装，以后也不需要装。
  - OpenClaw 带来的所谓颠覆内容和创新，甚至不如 Manus
  - 当时的大部分人，包括我，一致认为 Manus 只是一个套壳软件，不会掀起什么太大的波澜…
  - 我不需要在自己的电脑上安装任何运行环境，只需把任何文件、想法或定时任务扔给它，就像扔给下属或助手一样。我可以扔给它一段视频，让它使用剪辑软件帮我剪辑掉头尾；帮我把一张壁纸转为 HEIC 格式；帮我修改 PPT；真正从零开始编写一个项目，并在虚拟环境中完全自测、打包，直到运行结果通过，而这所做的一切都是端到端的，我无需对这个工具本身进行任何调试，也无需参与到中间的过程中，我只需要输入信息和看到结果。
  - 这是一个成熟稳定的工具的最大魅力所在。
  - 总而言之，所有的工作、想法和文件都可以扔到对话框中，通过稳定地对话输出一个稳定的结果。
  - 目前在所有讨论openclaw的文章和对话里，我还没看到一个真有价值的使用案例，全是些自动汇总信息和发帖的不痛不痒的工作，一方面是受制于接口权限，其实做不了很多事，一方面是沉迷用社交对话框操控生产的人可能也没太多想象力，单纯只是对“自动”这个词上头而已。
  - 为什么我认为 OpenClaw 是一个玩具，而不是工具？ 因为在现代社会中，没有任何一项工具是需要亲自去购买原材料、组装、测试并运行的，而且最蠢的是，在您进行这一大堆耗费精力的过程中，您甚至不知道自己组装这一把工具要干什么。
  - 总有一群人，他们不喜欢技术，只喜欢折腾的感觉。在 AI 之前，他们折腾 Obsidian、Notion、飞书、语雀、Flomo 等笔记软件；而在 AI 时代，他们乐此不疲地探索、追捧、神话各种概念和工具，然后留下一地鸡毛。
  - 很多双向链接、知识库等花里胡哨的功能，大多数人学了之后根本用不上，甚至为了这些功能所付出的情绪价值和精力，都要比功能本身带来的生产力要强）
  - 第一性原理，按照我的理解，就应该和工具一样，指您在干一件事情的时候，您的目的和结果都是端到端的，期间的所有工具都是您为了实现这个结果的手段。

- 佬大部分的观点表示赞同，但是有一小部分不赞同。比如说对于折腾的看法和对玩具的看法不甚赞同。这个世界的创新是需要这些折腾的人的，很多时候最初的工具诞生和技术的发展，并不具有太多的实际意义，靠的就是这些爱折腾人的兴趣和莫名其妙的执着。一个工具的诞生，最初往往就是玩具。不管是当初的汽车、当初的个人电脑，还是几年前的AI，刚刚诞生的时候，都被人嗤之以鼻，认为也就算个玩具而已。

- 不不不，这个角度太老登了，我虽然40+了，我的小龙虾也找不到什么活儿干，或者说干不好，还费token，但是我不会认为这个东西是纯粹的折腾，只是产品形态不太成熟，也是正常的，也有用的好，用的出价值的人，我不是这个人，但是我不会轻易去否定，一种自以为是。小龙虾是有跨时代意义的，我说的不是moltbook这种鬼故事，而是真的数字助理走进生活的开端，虽然也带来了一些隐私，安全问题，但是真的有需求。

- manus和openclaw是解决同一个问题的两种解法，前者是公司做给你用的，也是大部分公司走的方向，安全合规也有点用；openclaw是野生的，野蛮生长的，完全以有用为导向的。

- 感觉现在批openclaw和当初批manus的是同一批人

- 从实用主义上来说，佬友文章我是赞成的从个人爱好角度来说，不认可这种观点。折腾是很多时候驱使人去寻求新鲜事物和学习新东西的动力。换个角度来说如果不是折腾或者爱找方法，我也不会来到l站了。换个角度折腾ai工作流是不是一种折腾呢，折腾更便宜的渠道是不是一种折腾呢我觉得有一个观点说的很好，很多时候这种东西就是一个人的天赋，他会在这个角度为之努力乐此不疲，而在有一天收获意想不到的宝藏当然因为焦虑而去装一个龙虾当然是大可不必的行为

- ## [大家除了编程一般都拿AI干啥 _202603](https://linux.do/t/topic/1679742)
- 分析在线新闻，建立对于某个事件的路径图，分析舆论啥的

- NSFW，我做了一个女友的赛博分身NSFW版，配上生图skill，不要太哈皮。
  - NSFW 这不是生产力的来源吗

- 阅读 给他提要求 推荐一系列的书籍 读不懂的时候问它 和自己熟悉的知识建立联系

- 思维练习: 多角度分析

- 学习！很多不懂的东西让他解释都非常好，还可以让他规划学习路线。生活中看到一些现象非常好奇是怎么回事我也会问一下ai。我现在其实百分之七八十都是不是让他编程，都是在满足好奇心

- openclaw
每天早上发一份天气预报，一份新闻，一份github热点报告。
定时提醒，不过这个有点不稳定，不太重要的定时可以用，否则还是手机自带的语音助手更安心。
待办列表，用一个skill将待办存进数据库里，用来平替gmail的tasks, 体验一般，看个人习惯了。
帮我读容器日志，更新下容器什么的。

- ## [Reddit上关于Qwen人事变动的讨论 ](https://linux.do/t/topic/1690679)
- 有一定的道理，qwen拿着最多的钱和资源到现在却没有什么标杆模型，现在这qwen3.5也只能勉强算一个吧。
  - 别的模型一眼就能看出哪些是主线大模型哪些是小模型而且也只专心维护升级那几个模型，成本自然低，而qwen混乱的产品线不去研究根本不知道他到底哪些模型是干什么的，整这么多模型成本炸裂不说大部分都没人在乎
  - 我觉得以后qwen可能是整一个顶级闭源大模型赚钱，一个中等开源模型以及小模型抢开源市场

- 一堆模型我觉得不影响什么, 问题是 Qwen Max 为啥那么平庸

- 看起来情况比想像的糟糕? 别的团队花同样的资金可以搞出 200B, 300B 甚至 700B 的 SOTA LLM, Qwen 却只能死守 SLM, 然后还有内部斗争

- [千问离职瓜继续爆料 ](https://linux.do/t/topic/1690763)

- ## 🤔 [NotebookLM lowkey gave me superpowers and i’m not even joking : r/notebooklm _202602](https://www.reddit.com/r/notebooklm/comments/1rfhswr/notebooklm_lowkey_gave_me_superpowers_and_im_not/)
  - threw in sources for programming, marketing, copywriting, literally everything i was studying. and dude. i was understanding stuff in like 20 minutes that would take me an entire afternoon watching youtube videos. this is not an exaggeration. i bought a marketing course that cost me good money and i ended up literally taking the course content, feeding it as a source into NotebookLM and learned BETTER than going through the actual course. the course became study material for the AI. i’m still processing this honestly.
  - does it have gaps? yeah. it’s not perfect, there’s stuff that’s clunky, limitations that make you roll your eyes. but being completely real with you it’s by far the best study tool i’ve ever used. and i’ve tried a lot. the thing is most people just throw a random pdf in there and expect magic. that’s not how it works. if you feed it good sources and know how to ask questions, this thing becomes a tutor that knows everything about that subject and doesn’t charge you 200 bucks an hour. but if you throw garbage in you’re gonna get garbage out. simple as that.

- I work on affordable housing real estate development; I uploaded all the complex rules and regulations and now I have a consultant who knows every inside and out
- I've seen NotebookLM make mistakes. I don't use it for high-consequence questions. But I will ask it to make first drafts of documents, and review my work to suggest things I missed.
  - This is a key point as all the systems like this (RAG inside) are lossy and will generalise the gaps based on wider training corpus. Many people think hallucination is the problem (where model has too little info and has to guess wildly), but this is an opposite problem where it has to condense too much content into its context window.
  - LLM's are actually weirdly bad at finding all needles in a haystack, which is counterintuitive as that's what we often do with them - especially NotebookLM.
  - However, even with a forensic setup you still have to check their homework across the source docs for any claim you consider important and damaging to get wrong - and NotebookLM allows this so it's a useful product compromise. (It still has a completeness problem but at least you can approximate correctness.)

- Only way NotebookLM hallucinates is if you start web searching in chat or you have inaccurate sources that YOU brought in.

- Upload kindle pdfs and read the plot and everything and ask it to create a per chapter slide deck! I love reading but my ADHD gets in a way! I used to never finish a single book now im down 10 books out of my 20 books challenge for this year haha! Superpower indeed

- The infographic generation all by itself is an amazing feature. Sometimes I'll just do it without any special prompting to see what I get and the results are often magically exactly what I was hoping for. Then maybe I'll add a couple extra prompts to focus on a specific area and again looks beautiful.

- 🐛 It's useful, but I don't understand why it doesn't have the ability to have multiple threads/conversations within the same notebook. I assume I'm using up some context window with each message, arenwe meant to just start a new notebook when the conversation hits length = X?
  - Yes, that annoys me too. I end up having to create notebooks separated by subtopic, which is absurd when the sources are the same. The context window is getting polluted and the quality drops. It would be amazing to have parallel conversations within the same notebook, each focused on a different angle but using the same sources. Thread type.
- I guess you can query via Gemini but I have no idea if the quality of the responses is the same

- ## [What do people actually use openclaw for? : r/ClaudeCode _202602](https://www.reddit.com/r/ClaudeCode/comments/1rcx9di/what_do_people_actually_use_openclaw_for/)
- These are some common things I saw people talking about:
  - email management, i dont trust AI with this and i dont have that many emails to manage.
  - morning briefings, sounds like slop and just junk formation.
  - second brain/todo tracking/calendar, why not just use the exiting notes/todo apps its much faster and doesn't cause you "tokens".
  - financial/news alerts and monitoring, again sounds like slops that aren't that useful.

- A lot of the hype is just marketing. All I see right now is openclaw abstracting tasks to make them different, but not easier, and costing more money.

- To me its just like N8N, overhyped.

- I think its hype... zapier has done this for years, and personally I use agent teams with cron jobs to achieve the same Open Clawd results but without the high cost from api usage because it runs on terminal. Also I built an agent/team manager app I call Agent UI that work alongside it to help me get the most out of every token! https://github.com/DatafyingTech/AUI

- Hype and marketing. Mostly non devs who call themselves tech trying to show off their "ai skills". To them they finally can chat with ai on whatsapp and telegram and use ai to manage their data containing pii. Also, remember to run it on a mac mini

- ## What agentic coding methods seem to have done is reduced the cost of replicating previous-generation methods. 
- https://x.com/dustingetz/status/2025191981207421346
  - But without developing new frameworks, the agentic methods will simply reproduce the same set of flaws and issues that the current generation of growth stage products have. Which means they are (1) uncompetitive, and (2) late. 
  - The fundamental problem of software is that it becomes difficult to change once you have users and revenue. 
  - Being 100x faster to generate code does not solve that problem that landing the code in prod breaks the user's workflow and generates churn(搅乳器).
  - Agentic coding methods also accelerate research and development, so I anticipate a new generation of more agile products. But still, these will be built by more competent founders, not less. AI reduces switching costs and accelerates learning. The advantage right now is to R&D teams that figure out how to take advantage of the new capability frontier to accelerate their very slow R&D lifecycle.

- ## [I looked into OpenClaw architecture to dig some details : r/LLMDevs _202602](https://www.reddit.com/r/LLMDevs/comments/1r9136z/i_looked_into_openclaw_architecture_to_dig_some/)
  - Under the hood, it’s simpler than most people expect.
  - OpenClaw runs as a persistent Node.js process on your machine. There’s a single Gateway that binds to localhost and manages all messaging platforms at once: WhatsApp, Telegram, Slack, Discord. Every message flows through that one process. It handles authentication, routing, session loading, and only then passes control to the agent loop. Responses go back out the same path. No distributed services. No vendor relay layer.
  - What makes it feel different from ChatGPT-style tools is persistence. It doesn’t reset. Conversation history, instructions, tools, even long-term memory are just files under ~/clawd/. Markdown files. No database. You can open them, version them, diff them, roll them back. The agent reloads this state every time it runs, which is why it remembers what you told it last week.
  - The heartbeat mechanism is the interesting part. A cron wakes it up periodically, runs cheap checks first (emails, alerts, APIs), and only calls the LLM if something actually changed. That design keeps costs under control while allowing it to be proactive. It doesn’t wait for you to ask.
  - The security model is where things get real. The system assumes the LLM can be manipulated. So enforcement lives at the Gateway level: allow lists, scoped permissions, sandbox mode, approval gates for risky actions. But if you give it full shell and filesystem access, you’re still handing a probabilistic model meaningful control. The architecture limits blast radius, it doesn’t eliminate it.
  - What stood out to me is that nothing about OpenClaw is technically revolutionary. The pieces are basic: WebSockets, Markdown files, cron jobs, LLM calls. The power comes from how they’re composed into a persistent, inspectable agent loop that runs locally.
  - It’s less “magic AI system” and more “LLM glued to a long-running process with memory and tools.”

- That persistence feature is possibly the most important advantage AI agents have over chat interfaces imo

- One of the most important components at the core of OpenClaw is another open source project called Pi and Pi is responsible for a large portion of the heavy lifting in OpenClaw.
  - Pi has a number on components in its mono repo (pi-mono) but the 2 most relevant to OpenClaw’s success are the Agent and Coding-Agent.

- ## 🤔 [I feel left behind. What is special about OpenClaw? : r/LocalLLaMA _202602](https://www.reddit.com/r/LocalLLaMA/comments/1r9gve8/i_feel_left_behind_what_is_special_about_openclaw/)
  - While there are tools like Manus ai, It seems like everyone is excited about OpenClaw lately, and I genuinely don’t fully understand the differentiation. What exactly is the shift here? Is it UX, architecture, control layer, distribution? Not criticizing, just trying to understand what I’m missing.

- Astroturfing
  - While I do agree, the local agentic nature of it (and messenger API integration) is quite a nice package.
  - I've been running it on my M4 Mac Mini, and sending it on little tasks has been interesting to say the least.

- First there was just a chat window. ctrl c, ctrl v.
  - Then came agentic coding that not only did ctrl c and v for you, also read the files that mattered.
  - Then came identity and memories, an md files that explains everything in enough depth and the AI got a headstart.
  - Then we started having context window problems, we stick everything in context, and lots of fails because models werent as smart as today. Plus they tend to forget about things that even do fit in context.

- I use OpenClaw daily. The main difference vs other agent frameworks is that it's a unified runtime with persistent workspace, not just a chat wrapper.
  - Tools are first-class: browser, shell, code execution, file system access, all in one environment with a shared context
  - Skills system lets you extend capabilities with structured tool definitions
  - Memory persistence across sessions via local markdown files the agent can read/write
  - The heartbeat system lets agents be proactive, not just reactive
  - Multi-channel (I can message it via Telegram, Discord, etc and it maintains state)
  - It's less "AI that can use tools" and more "environment where AI has access to everything." The tradeoff is you're trusting it with real access, which is why the security model matters.

- Don't. It's a security nightmare.
- OpenClaw is bad software. It is intrinsically unsecure, and prone to prompt injection attacks. Giving it access to your desktop or accounts is hazardous and profoundly unwise.
  - The only reason it has seen so much buzz is because of a massive bot-driven astroturfing campaign, which unfortunately enough people fell for to keep the buzz rolling.

- Of course openclaw has great risk, but it also has great potential

- I think social media hype is a part of the equation. But it's also how easy it is for "normal" people to cook up some automation with it.
  - It's hard enough that they feel like they have expertise (e.g., writing markdown, setting schedule), but not too "hard" that they just give up like playing with n8n, langflow, or writing a script for cronjob. 
  - That "simplicity" comes with great costs though. In this case, costs is literal in terms of Opus token burning, and overall finicky nature of the automation they built. 

- Nothing, it's just a token-burning, social-media generated, ai-hype engine. Doesn't do or mean anything at all.

- IMO it’s an experiment in giving a coding agent long-term memory, and control over its execution environment. It has memory, it has agency, and it has hooks and mechanisms to initiate conversations, not just respond. It’s a really powerful harness, to the point people have shot themselves in the foot with it.

- Open Interpreter has been around for a while. It's like Mistral vibe but it can run code and do anything on your computer.

- That's why I love the project and support it - someone had the insight, courage, and drive to finally assemble all the puzzle pieces: an agent (pi), MCP and skills and numerous CLI tools (many of which he built himself), a memory system, scheduler and IM gateways. All that released as open source - and even after getting hired by OpenAI, he's not selling out the project, but letting it live on in a foundation.

- Malware bot platform that is being popularised by the bots themselves.

- It’s a tool that will leak all your information

- ## [Google 封号的最大起因 Openclaw这类的兴起 _202602](https://linux.do/t/topic/1631197)
- 主要还是使用的人多了吧，之前使用 Claude Code 不也一样吗。只是 openclaw 让用的人多了，毕竟之前使用 Claude Code 人不多吧
  - 写代码的比较人少，claw 这类人人都可以用，数量就指数级增加了

- ## 从 CompanyOS 到 LifeOS - 将文件系统哲学应用于人生管理
- https://x.com/yibie/status/2021778995185168650
  - Eli Mernit 提出将公司建模为文件系统，让 AI Agent 通过读写文件来运营企业。这条思路的深层价值在于：当个人也将人生建模为文件系统时，它不仅是一种极简高效的人生管理哲学，更让 Openclaw 等 AI Agent 能够真正成为你的"数字分身"——因为它们可以像访问公司数据一样，访问你完整的人生上下文。
- "One reason that rolling out agents at enterprises is complicated is because data is siloed across many different systems."
  - 没有共享的命名空间 (shared namespace)，AI Agent 无法获得完整的上下文，自然无法做出好的决策。
- Eli 的解决方案极具 Unix 哲学的美感： 把整个公司建模为一个统一的文件系统。
  - 统一命名空间：所有数据映射到文件路径Agent 可以访问所需的一切
  - 文件即状态：公司状态 = 文件内容状态管理极简、透明
  - 权限即治理：组织架构 = Unix 权限权限边界清晰、自动化
  - 读写即操作：Agent 通过读写文件工作接口简单、可审计

- 如果你想开始构建自己的人生文件系统，以下是一些工具思路：
基础工具
Obsidian - 本地 Markdown 笔记，图谱视图
Logseq - 大纲式笔记，日记导向
VS Code + Git - 代码编辑器管理人生文件
同步与访问
Syncthing - 点对点文件同步
Nextcloud - 自托管云存储
GitHub Private Repos - 版本控制人生文件
AI 集成
Openclaw - 文件系统优先的 AI Agent
Claude Code - 可以直接操作文件的 AI
数据迁移
从各 App 导出数据（大多数支持）
转换为 Markdown / JSON / CSV
导入统一的人生文件系统

- 👥

- 这里面的挑战是，未来这些信息是一个本地的系统，还是一个云端的系统。是集中化的，还是数据分散但是通过agent集中起来的。留在本地的这一整套都不是终极形态
  - 未来和 OpenClaw 开发者所说的，SaaS 服务会再度抽象成一个个 bot，然后 bot-2-bot 相互沟通提供服务。可视化设计只不过是面向人类，而 bot 是不需要的。 所以，无论当前的界面是否消亡，面向人类的 GUI 和让数据联通的 API 都不会消失。

- ## So far in 2026: Browsers. Payments. Apps. Commerce. Ads.
- https://x.com/Jall_n/status/2022364519071154325
  - Google shipped WebMCP
  - Stripe shipped x402 payments
  - Anthropic released MCP Apps
  - Shopify launched Universal Commerce Protocol
  - Yahoo released adMCP
  - Your new customer is an agent with a protocol, not a human with a browser.

- visa also shipped credit cards for agents with @crossmint

- Final phase, Prompt injected to leak my already leaked password, golden.
- still waiting on my AuthMCP invite

- funny how we spent years optimizing for SEO and now we're back to optimizing for machines anyway

- MCP will die this 2026. MD files and CLI will be the substitute

- 2026 is the year protocols become the primary interface. Humans aren’t browsing. Agents are. They follow standards, authenticate, and transact autonomously.

- ## [老saas焕新的讨论 ](https://linux.do/t/topic/1607336)
  - 有没有办法，可以把老旧的 web based 的 saas 系统，升级成 AI driven 的新的 saas 系统？ 我能想到的一种方式是，前端提供对话框，LLM prompts 里提前对业务系统的表结构进行理解（saas 一般都是结构化数据），text2sql，然后对查出来的数据，在前端通过 llm 进行展示（这种形式最容易想到，也容易被 sql 注入，大家还有没有别的方法）
- 我觉得目前的 AI 还不够智能和安全，我的想法是在现有的 SaaS 系统基础上做一个外挂，通过 MCP 让 agent 能够调用后端接口，而不是直接去操作数据库，相当于是替代前端，这是我觉得目前阶段比较稳妥的做法。
- 具体怎么操作也看 SaaS 的架构吧，我这边是基于 Go 的后端，就接入 Go 的 MCP 库，你可以理解成把现在的 restful api 给翻译为 MCP 接口，专门让 agent 进行调用的。
  - 然后 agent 这一块是另一套工程方向了，简单的话可以用 dify、coze 搭建工作流接入后端的 mcp 服务器，复杂的话也可以用 python/Go 或者 langchain 之类的框架做 agent 开发，这块比较复杂

- 好想法，甚至可以把一些业务动作封装成 skills

- 可以的，老哥这个想法比我的靠谱多了，那你觉得前端应该用什么形式呢，chatbot？而且 mcp agent 的话，怎么鉴权呢，比如不同的权限级别能调用的 api 应该是不同的
  - 前端 chatbot 最简单高效，反正我目前是在原有前端界面右下角有个按钮弹出对话框，就像那些客服机器人一样。
  - 鉴权直接接入现有 SaaS 的权限管理呗。
- 理论上只要能把用户的 token 从 agent 通过 mcp 传到后端就行，会不会有问题我也不敢百分之百肯定，可能不同语言的 mcp 实现不一样呢

- 总感觉这里可以通过提示词提权
  - 提不了，大模型也只是调接口而已

- ## [Fully offline, privacy-first AI transcription & assistant app. Is there a market for this? : r/LocalLLM](https://www.reddit.com/r/LocalLLM/comments/1qz80a9/fully_offline_privacyfirst_ai_transcription/)
- Entirely dependent on the minimum specs required to run it and the platforms it runs on.
  - If I can run it on an integrated graphics Intel CPU from the last five years or so with say only 8-16gb of RAM it could be a winner. Or thinks Mac M1 with 8gb of RAM. This is 80% of computers that real people use daily. 
  - If it needs 24gb of VRAM and 16 CPU cores then it's a niche market... Not sure I like your chances. 
- It’s actually 100% standalone on mobile! No PC or server tethering required. The whole point is to have a fully offline assistant right in your pocket, taking advantage of the NPU/GPU on modern smartphones.
- Yes, like whisper locally but mobile, and I connected an LLM that gives you suggestions or translates or summarizes in real time. What do you think?
  - I use whisper regularly. That's why I was asking, what's the big deal? Personally I don't need summaries or translations, but those might be the major attraction for some people, saving them time.
- I use LoroNote for whisper local transcription on my phone. If you could do real time streaming transcription, ESPECIALLY with diarization (separating who is speaking) then that would be an absolute game changer.

- Here seems to be a ready-made one that supports multiple platforms including iOS/macOS. https://www.kyoten.jp/products/safe-translator/

- ## 高强度使用了 openclaw, 离开了它丑丑的 UI 我发现 openclaw 最牛逼的地方就是它是一个高度 AI Native 的系统（拜托于各式各样的 skills）
- https://x.com/yetone/status/2020875192923558026
  - ai native: 完全发挥 AI 的主观能动性，不需要用户操作任何的 UI 控件，只通过聊天让 AI 完成所有的操作
- 其实并不是因为 UI 丑，而是他本身就是一个 Headless AI Native 产品，如果真的说有 UI 的话，那 IM 就是他的 UI 了。他的出现其实给很多 agent 产品一个启示，agent 最适合的载体就是 IM，因为可以随时随地唤起。

- 没错Alma是有层层叠叠的UI树和对化设置的，要让设置能通过对话和记忆，自己设置自己
  - 接下来的几个版本，Alma 逐渐进化到 skill base 的系统，大家都不需要通过任何 UI 点击就能完成所有的 Alma 的配置工作

- ## 今天的社交媒体，就好像二十多年前的报纸。眼看着互联网直接拿自己的内容抢走自己的用户，一边对抗互联网，一边还不得不继续生产内容送给互联网。
- https://x.com/xicilion/status/2032908776135856342
  - 渠道变了，商业模式也就变了。
  - 今天的 ai 也是。新的商业模式会是什么，如何有效分配利益，让各方回到内容市场里来，是接下来几年要解决的问题。

- 本质上是内容定价权的问题。报纸时代读者为内容付费，互联网变成广告付费，AI时代连广告都不需要了——直接把内容嚼碎了喂给用户。谁来为原创者买单，现在没人有答案。

- ## 🤔💡 软件正在走一条，媒体已经走过的老路。当成本塌陷，一个行业的价值结构一定会整体翻转。
- https://x.com/AztecaAlpaca/status/2020013931499278370
  - 一旦软件像内容一样“便宜到不需要赚钱”，后果就会出现：
  - 软件数量会爆炸，单个大而全的系统价值下降，用户不会再依赖某一个“巨无霸软件”，而是用一堆小工具、临时工具、自动生成的东西，按当下需求拼起来用。
  - Salesforce 不会被下一个 Salesforce 干掉，而会被一堆“临时有效、随用随生”的东西慢慢掏空；真正掌权的，会是新的平台，负责分发、组合、调度这些软件。
  - 在互联网出现之前，媒体的运行方式完全不同。内容生产成本很高：要付钱请人创作、编辑、发行。正因如此，内容必须赚钱。消费者也确实为此付费——报纸、杂志、书籍、有线电视、按次点播。沃伦·巴菲特曾公开表示自己热爱报纸生意，谁会不喜欢一种订阅稳定、又具备地方性垄断结构的商业模式呢？
  - 当互联网出现时，媒体公司把它看成扩大受众、降低分发成本的工具。但几乎没人预料到，互联网不只是把分发成本压到零，同时也把内容创作成本推向了零。用户生成内容开始繁荣。当内容不再需要成本，它也就不再需要赚钱。
  - 用户生成内容平台。这些平台对传统媒体形成了侧面撞击。作为一家媒体公司，你争夺的是同样的用户注意力，却承担着更高的单位成本。雇佣的人越多、原创内容团队越大，越容易被用户生成内容平台从侧翼包抄。从结构上看，投资媒体此后一直是一个持续失血的选择，价值创造已经完全转移到掌控分发的平台手中。
  - 软件的情况长期以来类似。软件昂贵，是因为需要人来开发、维护和分发。正因为昂贵，软件必须赚钱。我们为此付费——软件授权、SaaS、按席位定价等。历史上，软件行业的利润率令人艳羡：90%以上的毛利率，分发的边际成本几乎为零。
  - 软件之所以昂贵，是因为开发者昂贵。他们是高技能的“翻译者”，在人的语言与计算机语言之间来回切换。大语言模型已经证明自己在这件事上极其高效，并将把软件的创建成本推向零。
  - 当软件不再需要赚钱时，会发生什么？我们将经历一次软件的寒武纪大爆发，正如当年内容所经历的一样。
  - 《Vogue》并没有被另一家时尚媒体取代，它被一万个网红取代。
  - Salesforce 也不会被另一个庞大的 CRM 系统替代，它会被一组动态组合的工具所取代，这些工具共同服务于相同的意图与痛点。
  - 软件公司将以与媒体公司相同的方式被取代，同时催生出一批新的、掌控分发权的平台。
  - SaaS、ARR、各种“魔法数字”，都是旧软件商业模式的速记方式。在那个模型里，软件开发成本本身构成了护城河。长期以来，市场的“无形之手”在软件行业被人为压制；而 LLM 将引入一次迅速而熟悉的纠偏。今天选择计算机科学作为专业，处境将类似于 90 年代末选择新闻学。

- 做出优秀的软件是个严肃的工程任务，但是人们需求并不需要优秀的软件就可以满足了
  - 比如科研工作者，他们的代码质量总体上是很糟糕的，尤其是做数学和做物理的，代码风格简直臭名昭著... 但是，对他们而言，有个凑活能用的代码来解决计算需求已经够了。
- 人们在许多时候对软件的需求甚至连demo都够不上。以前只能通过购买某个软件来满足这种需求，现在直接AI生成一个简单的脚本就搞定了（就像有个高级一点的计算器）。

- 🤔 不是软件变得很多，是语言文字图片的input转向了不需要用软件，而是用skills，或直接mcp解决问题，但是对于大公司，mcp向数据库请求资源，和以什么样式回馈给用户，还是需要构架的，数据库的关系，还是需要构架的，以前，人类需要前后端UI显示和查询数据库，现在不是了
  - Salesforce确实有很大影响，但是对于复杂的任务，很难，而对于简单的项目，比如报税，intuit就很快就会被干掉，只要大多数人可以用skills. 但你别指望不会写代码的人能马上上手terminal CLI. 更别指望不懂数据关系的人上手用母语编程

- 软件行业的“媒体化”已经开始了。但媒体还有一个课很少人提：当内容免费后，赌的就是分发。谁能把软件送到用户面前，谁就赢。App Store 就是这个模式下最大的赢家。
  - 🤔 分发渠道是否是 skill/mcp marketplace

- 🤔 还可以参考 智能手机 干掉 mp3/相机/导航仪 的市场逻辑
  - ai正在将垂直领域的产品封装为一个个插件
- cowork太通用
  - 阿里垂直场景的工具可以调用国产软件，如金税系统、教育、医疗、法律

- 媒体翻转后留下了碎片化和垃圾信息洪水，软件翻转后，我们会不会面临‘逻辑洪水’？当工具便宜到不需要钱，我们是不是反而会被无数低质、临时的逻辑补丁给淹没？
  - 有可能吧，现在已经进入了一个发布之后就不再维护的时代了，和传媒的那种管拉不管擦的局面差不多了

- 维护一个能用的工具是要花费精力和人力的, 用来挣钱的工具, 为什么要倾向于自己造方案?  既然生产成本很低, 更应该往供应商多提定制需求
  - 文中一个比较核心的观点：“当软件不再需要赚钱时”... 你说的都是不得不以赚钱为目标的软件。但很多情况下，我写个代码只是为了解决我手头的问题，不需要赚钱

- ## [从“为什么ai客户端都不支持多窗口多开”看到ai开发的未来 _202602](https://linux.do/t/topic/1576098)
  - Cherry Studio 桌面客户端不支持多开窗口 这个问题已经反应了一年了，作者还回复了，也开看见了，LobeHub 也是 作者也知道，也一年了，知道现在一个这些主流 ai 客户端就没一个支持多窗口多开的
  - 这些客户端大部分都是 chrome 架构的，本质就是个网页，多窗口多开本质不就是一个代码开关的问题，真有这么难，就没人做的出来，还是作者极度的傲慢？
  - 我之前看 win 多屏用户人群超过 30% 了，这么多人使用多显示器
  - 尤其是在写东西查资料的的时候两个标签反复的切换 我另一个屏幕就哪里空着用不上 真是用的脑袋疼 太恶心了
  - 尤其是不同的 ai 还需要先切换助手在点击对话 切换一次要点四五次，我很难理解这些人做出来的产品到底自己用不用

- ## OpenClaw 可以算是 AI OS 的雏形了吧，或者叫 AI DOS：
- https://x.com/geekbb/status/2019591292456759564
  - Skills → 应用软件
  - 终端 → Telegram/Discord/WhatsApp 
  - 进程管理 → Agentic Workflow / Task Planning
  - 指令集 → 自然语言
  - 虚拟内存与分页 → RAG
- 这个类比很到位，尤其是叫 AI DOS ，现在的交互确实还挺硬核的。如果 RAG 是虚拟内存，那 Context Window 应该就是死贵的 L1 缓存？好奇谁能先搞出 AI 界的 Windows 95。

- ## [畅想一下未来，以后充token会不会就像充流量话费 ](https://linux.do/t/topic/1552655)
- 如果能的话我觉得还是挺值得入的，无限 token 但到指定 token 数额之后限制上下文

- 要出不限量 不降智 老百姓用的起

- 以 v3.2 的价格，可能加起来价格不如话费贵。

- 从 3g 时代，用多少充多少。到后来套餐包月。最后进化到卫星 wifi，实现 token 自由

- ## [【Agent系列4】Clawdbot（Moltbot）全球爆火的底层原理  ](https://linux.do/t/topic/1541126/3)
  - moltbot 这么火，说明其赛道 (本地桌面 agent) 是被压抑的需求，如果其种种问题都解决了，桌面 agent 显然是功能最强大的，人能做啥他就能做啥
  - 其他所有 CLI，虚拟机，远程服务器，浏览器 Agent，IDE agent，app agent，本质都是脱裤子放屁，舍近求远，桌面 agent 才是那个房间里的大象，但人人都装看不见。
  - 远程虚拟机 CLI Agent (Manus) 某种角度就像我用 ipad 遥控自己电脑一样迟钝和束手束脚
  - 远程虚拟机 CLI Agent（Manus）的情况 虚拟机里没有用户隐私，格式化了对用户也没影响，重开一个虚拟机好了
  - Cloud Agent (如 Manus) 为什么好做？因为它运行在标准化的 Docker 容器里。 屏幕分辨率是固定的 (1920x1080)，浏览器版本是锁死的，字体渲染是统一的。
  - Moltbot 建议用 Mac mini 这类备用电脑 / 独立电脑，或者淘汰的 MacBook 因为不是工作机，没必要个性化，甚至建议用相同版本 macOS，相同的默认界面，来对抗桌面 UI 个性化的造成的适配性灾难

- ## 国外有类似大众点评这类专注于评价/打分的网站吗? 可以列举些 互联网服务或 效率/生产力工具 评价相关网站并给出该网站评价体系相关的指标, 要非餐饮行业的评价类网站
- Letterboxd makes money primarily through its tiered subscription model (Pro and Patron) offering ad-free viewing and advanced features, targeted advertising for film studios and distributors (especially for new releases), and specialized "HQ" accounts for film organizations, all while leveraging its engaged, cinema-literate user base as a valuable marketing channel. 
  - remove ads, get detailed stats, stream availability tools, watchlist notifications, and profile customization.
  - HQ Accounts: Film-related businesses (studios, festivals, podcasts) pay for special accounts to post news, link to external sites

- ## I suddenly use the @NotionHQ agent a lot. Use cases
- https://x.com/cramforce/status/2012890889803399504
  - I dump a long list of Slack-sourced one-sentence ideas. The agent categorize them
  - I write competitive research table, the agent fills it out and adds appendixes with detailed data
  - I love this because it saves me time but the use-cases are low-risk of hallucination AND I don't get paragraphs of slop-text that pains me to read

- Notion as the “messy inbox to structured doc” layer is such a good use of an agent. Categorize the chaos, then fill the table, then append sources. The time saved is obvious, but the bigger win is everyone reads the same format.

- I actually could use something like this but for Obsidian

- ## [类似 Manus 的开源项目有哪些 _202601](https://linux.do/t/topic/1465345)
  - Manus 好用但是不能爽用
  - 流畅度是最重要的，我闭源的工具我都没用过比 Manus 流畅的, 调用工具这块 Manus 还是太强了
- 要类似 Manus 这样：
  - 可以调用终端
  - 调用浏览器
  - 能执行 js 脚本
  - 能调用联网工具
  - 支持浏览器视觉
  - Python 爬虫爬取内容

- cli工具都可以，开源的有opencode gemini cli这些，国内那几个不知道开源了没

- 这个是 Gemini cli 的 GUI 吧，很多终端上能用的功能在 aionui 就不能用了
  - aionui俺这个还不太行，基于gemini cli魔改的，目前能力都在终端上，浏览器的话，得装 chrome-dev-tool之类的MCP进行调用。
  - 对话的时候，点这个关联文件夹，授予gemini cli访问权限

- ## 🆚 [Is there any tool for for manual proofreading of video transcriptions, with ability to check original audio and to maintain a list (dictionary) of text entities? : r/LanguageTechnology _202404](https://www.reddit.com/r/LanguageTechnology/comments/1c3qfii/is_there_any_tool_for_for_manual_proofreading_of/)
- https://gooey.ai/speech offers a bunch of ASR models (google USM, meta-large, whisper v3) and the ability to define a dictionary as a google sheet.

- I'm not sure this is actually an NLP problem. Everything you want here can be done with standard text editors and databases and probably some audio software, you just want an app that puts all of that together. The actual NLP task of transcribing the audio is the part you're doing manually, rather than delegating it to an algorithm to do automatically.

- ## "We now want to edit our *tools* as we have previously edited our documents"
- https://x.com/geoffreylitt/status/1646688665479831559
- "As we shape our tools, our tools shape us." 
- This is what makes tools like Notion and Airtable so powerful— they’re lightweight ways to build increasingly customizable interfaces with (albeit small) knowledge databases. As they get more flexible and can handle more data, I feel they’ll become essential parts of UI/UX design
