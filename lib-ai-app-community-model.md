---
title: lib-ai-app-community-model
tags: [ai, community]
created: 2023-10-30T07:33:56.233Z
modified: 2023-10-30T07:34:03.602Z
---

# lib-ai-app-community-model

# guide

- tips
  - 大模型相关的产品研发，原理的可解释性很差，效果的可解释性也差

- model-features
  - 🤼: speed, quality, size
  - reasoning/thinking
  - tool-use/function-call
  - vision
  - embedding
  - moe
  - 注意有些社区量化的模型可能遗漏标注了部分features, 可在本地测试来确定是否支持

- 移动端大模型
  - 参考google-gemma-1b

- [大规模语言模型：从理论到实践](https://intro-llm.github.io/)
  - 复旦大学张奇教授团队写了一本在线免费的电子书，大概有 300 页篇幅，将大模型从理论到实战的每个阶段都描述的较为清楚
# discuss-stars
- ## 

- ## 

- ## 🤔 [端侧模型会是 AI 技术演进的下一个 「必争之地」 吗？当前落地面临哪些核心瓶颈？ - 知乎](https://www.zhihu.com/question/1914319403023032351)
- TO C场景应用最大特点是硬件参差不齐。性能差能大到10多倍以上。
  - 技术栈必须满足所有主流硬件结构差异和性能性能下，保持相对一致的使用体验。这是一件极累的活儿。
  - 服务端下个开源模型搭个WEB服务写个HTML就能卖服务了。端侧想内嵌AI模型产品化，同时还要解决实时性，要解决的工程问题要多10倍不止。要自己优化模型。甚至要自己搭建模型结构，自己准备数据训练。
- 目前看端侧完全谈不上AI演进必争之地。一来硬件较弱且参差不齐，导致TO C工程保障体验极度困难和复杂。二来PC高算力硬件完全不是大众消费级的售价和定位，最后，还没有什么端侧AI落地产品的应用范式。
  - 从应用体验上，那些允许延迟500毫秒以上，对带宽需求不大的应用，都可以放到云端。
- 真需要做到端侧的，其实是那些需要即时响应的应用场景。
  - 为数不多的应用类别，比如即时交互影像相关，语音相关的，诸如游戏，需要即时交互的数字人，3D虚拟AI人，虚拟人直播等，可能会对端侧AI有部分需求
- 这类应用有3个特征： 
  - 1 即时性直接影响体验，不能等。 
  - 2 对算力要求相对低，运算本地算力能够满足，并不一定非要云算力支持。 
  - 3 对带宽要求较大，云服务的成本过高使得商业模式不成立，所以需要放入本地。
- MOBILE离端侧可能更远。 由于算力极为低下，只有很少的情况才需要手机上即时响应AI推理给出的结果。即那些把手机作为信号传感器，即时对信号运算的场合：比如表情捕捉、手势、肢体动作捕捉和识别，语音、运动数据处理和生物信号处理等。 
  - 如果手机没有专用神经/张量芯片，GPU还需要承担渲染3D图形，那么能跑的AI模型会更加受限。
  - 目前测试，某手机用NPU跑模型比不用最多能快10倍。 
  - 手机芯片商是否有动力发展，要看手机作为数据传感器即时处理数据能带来多大的应用市场。

- 本地部署模型的优势在于低延迟，这在我看来其实也是个相对偏伪的优势。
  - 事实上，现代网络环境实际上以及足够快速和稳定，无论是流量还是WiFi，辅以CDN边缘节点优化后，绝大多数主流AI应用的云端响应都能稳定在几十毫秒以内。
- 端侧设备受限于功耗、热量、算力等物理条件，往往只能部署轻量化模型

- 移动设备上长期运行一个有竞争力的大模型仍然不现实，负载、资源占用、电量消耗、发热等等问题，很难做到好的体验，更不要说物联网设备、智能音箱等低功耗产品了。
  - 很多声称自己用了端侧大模型的，实际上仍然离不开云端的协同配合，或者说主要靠云端，备用方案可能是端侧，但把端侧拿出来大肆宣扬，来做广告而已。

- 🐛 端侧模型的劣势
  - 端侧模型仍然受限于设备本身的内存、功耗和算力
  - 云端模型可以随时升级，热更新机制保证所有用户第一时间享受新一代模型
  - 端侧模型对于不同设备和硬件架构需要分别适配

- 端侧适合的场景还是隐私、极低延迟，或者全天候。

- 如果完全跑在端侧，那商业模式怎么做？现在的主流是订阅制，但完全本地的订阅制，吸引力比较低，破解风险比较高吧

- ## deepseek 3fs 其实不是很理解这样的意义是啥… 已经脱离 FS 的通用接口了，为啥要硬挂一个 FUSE VFS 层… 直接摒弃 VFS 走个私有的 protocol 不干净多了…
- https://x.com/silsrc/status/1895390926098571505
- > Most applications use FUSE client, which has a low adoption barrier. Performance-critical applications are integrated with the native client.

- 我的第一反应是现有框架应该没办法大批量改用私有的 API，比如在 Python 我就是要用 pathlib. Path 对文件做点简单操作，那确实只能是挂 FUSE 上去了

- ## 聊一聊国内大模型的安全机制： 一般是两套，分别作用于train-time和test-time。
- https://x.com/9hills/status/1840786446153921017
  - 训练的时候增加安全和价值观对齐的SFT和偏好对齐数据。最终效果类似开源的Qwen2模型，有点用但是很容易被Jailbreak。
  - 推理时增加安全算子，具体有几种
- 技术难点有两个：
  1. 训练分类器的大量非安全数据，所以说你先成为反贼才能识别反贼。
  2. 模型要做的足够小足够快，最小化影响模型ttft和tps。
  3. 流式很难，某模型最早是一句句输出的，后来才改成token级流式。
- 请教一下，现在市场上的大模型，怎么知道他们的训练数据是多久的呢？
  - 可以问一些特定时间的新闻来验证，但是其实没关系。模型的精确知识不重要，也充满幻觉。

- ## Attention is *Not* All You Need，还是有人在尝试 transformer 以外的架构，
- https://x.com/liumengxinfly/status/1835251398692508114
  - 毕竟 transfermor 推理复杂度在数学上是无法线性扩展的，早晚会走到瓶颈

- ## 国产188个大模型的excel文档： 北京69 上海22 杭州15 广东26个 江苏15个
- https://twitter.com/FinanceYF5/status/1730912502312296935
  - [国产大模型188个list - Feishu Docs](https://zw73xyquvv.feishu.cn/wiki/WXLmwBbYuiTobkkJ6Ojc2cxqnj0?sheet=2XjJlJ&table=tblS2Jv7isKtSODz&view=vewfCdOf0U)

# discuss-llm-architecture
- ## 

- ## 

- ## 

- ## 

- ## [如何看待观点：AI 的关键点不是prompt，而是Context Engineering？ - 知乎](https://www.zhihu.com/question/1923364519964545063)
- Context远不止是一句prompt，它包括：
  - 指令/系统提示：定义模型行为的初始指令
  - 用户提示：来自用户的即时任务或问题
  - 状态/历史：当前对话的短期记忆
  - 长期记忆：跨多次对话收集的持久
  - 知识库检索信息(RAG)：来自文档、数据库或API的外部知识
  - 可用工具：模型可以调用的所有功能定义
  - 结构化输出：对模型响应格式的定义
- 这其实就是在构建一个完整的「AI工作环境」，而不是简单地给AI下指令。

- 即使你写不好prompt，市面上也有很多AI工具可以帮你做prompt enhancement
  - 期待AI能「有记忆，懂用户」。因此，Context Engineering（上下文工程）就开始被关注到。
  - context engineering, 是指通过系统性构建、管理和优化 AI 模型的输入上下文，以提升模型在复杂任务中的理解与输出能力。
  - 第一是历史交互数据。
  - 第二，是context的总结。对话可以一直延续，但模型的上下文窗口有限，怎么记住之前的对话？当然是压缩，例如把最近5条对话的内容原封保留，再之前的内容总结一下。
  - 但更重要的，是领域知识与背景信息。
- AI的能力来源于两个方面 in-weights memory（训练集里学到的） 和 in-context memory（参考资料里学到的）。 in-weights memory基本上是很难修改的, 但in-context memory 更容易修改和更新，你只要提供新的资料，正确的资料，模型就能有「新知」

- 复杂的AI应用，不是靠chat输入提示词这么简单，而是需要自动化多次和大模型的交互，这个自动的过程中，需要能够自动产生给大模型的提示词。

- Agent = LLM + Prompt + 工具调用，但从工程视角来看，这些本质都是Context Engineering，也就是上下文工程。
  - Context Engineering就是在每次调用里，把模型完成任务所必需的信息按对的格式、在对的时机准确打包进去。

- 上下文工程，AI绘图用户早就天天在用了
  - 当你使用 Inpaint（局部重绘） 功能时，AI不是凭空想象，而是基于你留下的画布、边缘线条、光线方向、已有画风来补全区域，这就是“图像上下文”
  - 当你进行 Outpaint（图像扩展） 时，AI必须参考原图的构图逻辑、色彩渐变、风格纹理、人物透视来生成自然衔接的部分。这种对上下文的“理解”和“建模”，比提示词本身更重要
  - 当你用 Photoshop内置的Firefly进行局部修改创成式填充时，真正起决定作用的不是你说了“给我加一个灯塔”，而是AI是否准确读取了当前画面是夜晚、是水边、有光源投射、有透视消失点。
  - 上面这些功能，哪怕你根本不写提示词，好的工具也能给你脑补好，比如我现在根本放不开订阅的Photoshop AI。

- 
- 
- 
- 
- 

- ## DeepSeek最大的创新，是不需要大量的人工标注，而是直接从其他大模型蒸馏或者使用群体相对策略优化算法（GRPO）、CoT（自我反思）来给大模型反馈，
- https://x.com/seclink/status/1888011462008005030
  - 就相当于完全使用RL（或者另一个基础大模型）来替代人工标注了。
  - 这实际上是抢了Scale AI 这种公司的蛋糕，DeepSeek牛X之处在于，很多老外一开始不信，然后照着论文里的方法快速（局促地）复现，却发现竟然也能复现成功。

- cot和蒸馏之前，就通过grpo进行rl获得了相当不错的推理能力。。你这整理的不清晰。

- 这没有任何创新，GPT1就用了同样的方法，而且现在不使用是有理由的。因为deepseek模型本身不行，一个query需要RL chain才能达到可接受的答案，致使inference 效率低到可怕，虽然training便宜，但是operation cost要多好几倍，得不偿失

- 你这个说的完全不对，CoT是GPT发明的，蒸馏也早就有了，RL也早就有了，deepseek是发明了RL里的GRPO

- ## I read up on DeepSeek’s learning algo, GRPO. GRPO: group relative policy optimization
- https://x.com/virattt/status/1885102056546910672
- How GRPO works:
  1 • model generates a group of answers
  2 • compute score for each answer
  3 • compute avg score for entire group
  4 • compare each answer score to avg score
  5 • reinforce model to favor higher scores
  - This process is repeated, allowing the model to learn and improve over time.
- Other methods like PPO, use a value function model to do reinforcement learning.
  - GRPO does not, which reduces memory and computational overhead when training.

- GRPO was proposed for the first time in Feb 2024 in DeepSeekMath paper. It is not new.
  - Back then they used Neural Networks for Rewards (PRM/ORM). The magic happened when DeepSeek  replaced PRM/ORM with the exact reward (Verified Reward).

- ## 🔡 OpenAI's Deep Research is just a search+read+reasoning in a while-loop, right? here is my replicate of it in nodejs, using gemini-flash and jina reader
- https://x.com/hxiao/status/1886250705415229627
- If it includes evaluating js driven websites, including images Then yes 
  - To really replicate that, you'd probably wanna just use puppeteer, save the whole page as an image, extract the info from that, and then crunch that data

# discuss-multi-agents 🏘️
- ## 

- ## 

- ## 

- ## 🆚 今天很有趣，两家知名的公司各出了一篇文章，争论要不要使用多智能体系统。
- https://x.com/oran_ge/status/1933754019010539923
  - Claude 的官方 Anthropic ：如何构建多智能体系统
  - Devin 的官方 Cognition ：不要构建多智能体系统
- 这核心的争议点在于：Context 上下文到底应该共享还是分开？
  - Claude 这边的观点是，搜索信息的本质是压缩，单个智能体的上下文有限，面对无限的信息，压缩比太大就会失真。这是集体智慧，一起协作获得的胜利。
  - Devin 这边的观点是，多个智能体的上下文不一致，会导致信息割裂、误解、他们汇报给老板的信息经常充满了矛盾。
  - 这让我想到，软件工程从来不是追求完美，而是持续迭代。

- 没啥矛盾的。看需求。open-ended 的问题比较适合 multi-agent；目标很具体的话，就比较适合单个 agent

- 感觉和现实中的两家不同策略运营的公司差不多，没有绝对的对和错，都能走出来的可能性也超大。

- ## @KuraAIAgents 通过创新的五重 Agent 架构（规划、执行、评估）实现了 87% 的浏览器自动化准确率，超越 Claude 计算机操作 28 个百分点，同时支持低成本模型替换方案
- https://x.com/shao__meng/status/1857586562588094918
  - 包含5个专门的 Agent，其中3个核心 Agent 形成一个循环系统
  - 在 WebVoyager 基准测试中取得 87% 的成绩
  - 比 Claude 的计算机操作高出 28%
- 五个核心 Agent：
a) 初始规划者(Initial Planner)
- 负责制定高层次计划
- 使用 OpenAI o1 模型进行推理
b) 循环规划者(Agent Loop Planner)
- 评估任务是否完成或不可能完成
- 为执行者提供下一步指令
- 根据需要修改计划
c) 执行者(Executor)具备三项核心技能：
- 网址导航和返回
- 读取当前页面数据
- 执行屏幕操作(点击、滚动、输入)
d) 循环评论者(Agent Loop Critic)
- 评估执行者的表现
- 特别在复杂界面操作中起关键作用
e) 最终评论者(Final Critic)
- 评估整个任务轨迹
- 必要时提供反馈并启动新的循环

- ## OpenAI 发布多 Agent 编排框架背后的思考以及实践过程
- https://x.com/tuturetom/status/1845634978530693494
  - 核心是 OpenAI 的工程师在思考  Agent 的「路由」 + 「移交」等能力时拓展出来的一个示例，进而发现这个示例原语很普适，所以开发了 Swarm 框架
  - 所有伟大的思考都源于周末业余工作

- ## OpenAI 悄悄开源了构建多代理智能体协同框架：Swarm
- https://x.com/aigclink/status/1844936446416912628
  - 用于构建、编排和部署多代理

# discuss
- ## 

- ## 

- ## 

- ## 做产品级搜索以后发现 3.7 效果特好但是特别贵，所以必须得做 content cache 降低成本。
- https://x.com/arvin17x/status/1896922111505285484
  - 但为了做 context cache ，发现必须得记录 token usage，不然感知不到 cache 的效果。

- 可以分享下 Context Cache 的原理么，我还以为这种东西只能在模型供应商侧做。
  - 就是在模型供应商侧做。只是 OpenAI 和 DeepSeek 做的是静默方案，而 Anthropic 和 Google 是需要开发者手动开的
- 应该是 prompt caching 吧
  - Anthropic家自己的说法是 prompt Caching. 但我感觉行业里感觉还是习惯叫 context caching 的。
  - 不过 OpenAI 官方和 Anthropic 官方都称之为 prompt caching

- 很奇怪，这玩意为啥不默认开启。
  - 某些场景下的确不一定适合，因为写入 cache 的成本是原价的 1.25倍

- ## It is common to generate train and validation sets using random splitting.
- https://x.com/_avichawla/status/1898622288737767785
  - However, in many situations, it can be fatal for model building.
  - Consider building a model that generates captions for images.
  - Group shuffle split solves this.

- ## 由于DeepSeek-R1 爆火，所以为大家带来什么是LLM蒸馏技术的笔记。
- https://x.com/karminski3/status/1882233538042597423
  - 几个助记词：教师模型，学生模型，软目标，硬目标。

- https://x.com/ShanghaoJin/status/1882679738789216456
  - 你听说过什么叫“蒸馏”么？说个大白话：就是拿人家算出来的模型参数，跳过所有数据清洗、训练，做最后一程。其实没有任何创新
  - 好像人家证明了π=3.14，他拿结果去算了圆面积。让他再自己去证明算一个e，他又抓瞎了
- 千万不要用“大白话”来解释自己都没完全理解的概念， 只能让外行拍手，懂的人只会笑话你。 你完全不知道蒸馏是在干什么。如果你知道的话，那就是完全不知道Deepseek 在做什么。
- “蒸馏”说法不正确。1. 蒸馏效果一般不会超过原模型 2. deepseek的 reasoning行为和市面上其他模型不一致(有超越人类标注的奇妙行为) 3. 开智对再训练模型有禁止并会监控 API滥用

- ## 我日常用 Cursor 写代码的场景之一：“请参考代码 @ XXX1 @ XXXn 做 YYY 事。”
- https://x.com/dotey/status/1869436413600731146
  - 简单来说就是让 AI 照葫芦画瓢，重要的是给出充足的上下文，让 AI 可以学习和模仿。剩下的就是 Review + Accept，很简单高效。
  - 特别要注意的是第一个“葫芦”要打磨好，这样后续的“瓢”才不会画歪。

- 更简单的做法有时候可以直接 @ git 某次提交

- 我现在是新项目里创建一个txt文件，里面写上想法和gpt对我想法的建议，然后让cursor 参考这个文件来开发，里面我也有时会写上步骤，首先实现什么，然后实现什么，做一段了，让cursor根据这个文件检查一下项目完成度，列出来哪些没做，这样反复迭代向前

- LM 充分证明了人类的本质就是复读机。 哪里有什么指令遵循，推理，大家都是从不同的维度用不同的方式在复读一些东西而已

- ## 如果想要让 LLM 稳定生成 JSON 对象，最简单的方式就是使用 zod 定义 schema 并配合 @vercel ai sdk的 generateObject使用，比如这里我想要从网页文本内容提取结构化的信息。
- https://x.com/FeigelC35583/status/1819558128297648412
  - 这种方式和当初 langchain 在 prompt 里写一大堆json 定义有本质区别，在于使用了 function call 的能力
  - 从请求中可以看到，本质上是在调用模型的时候，构建了一个名为 json 的 函数, 描述是 respond with a json object, 其中参数是自己定义的 schema，然后在 tool_choice 中限制必须要使用这个 json 函数，那么模型就会返回调用json 函数的参数，即你定义的 schema
  - 示例代码来自于https://github.com/DiscovAI/DiscovAI-crawl 我正在 building 的一个面向 RAG 应用的爬虫平台
- 应该只有GPT系列能用吧
  - 支持function call就可以，deepseek应该也可以的
- 在这基础上。我会考虑使用jsonrepair这个包，手动修复下，增加容错
- 如果大模型没有没有返回对应要求的字段数据，或者返回错了类型，它会怎么样，会自己补充空的，或者自动转换类型吗？
  - 不会补充，会throw error，也可以用上面推友推荐的jsonrepair手动fix

- 能支持开源模型吗
  - 取决于模型支不支持function call，支持的话就可以，效果的话要看模型的能力
- 用 function call 感觉模型的能力降了一个维度，不如直接给文本，我还是更喜欢用xml自己提取。

- 我是用伪代码➕类型声明, 也是一样的稳定输出 json
- langchain框架中有Pydantic json 解析器可以直接用，本质也是生成schema，再配合重试解析器也可以稳定生成json格式

- ## 💡 LLMs are literally the most unreliable technology of all time (followed by **ing bluetooth)
- https://x.com/Steve8708/status/1819448686424084892
  - After an absurd amount of trial and error, we've internally created a set of rules for make LLMs considerably more reliable
  - our secrets: restrict the llm to only what rag provides

- what's your stance on AI for no-code? Do people prefer drag-and-drop vs prompting?
  - i think the winning move is combining both

- Bluetooth is hell and causes frustration daily.

- ## 🌰 Firefox will use Transformers.js to power on-device features
- https://x.com/osanseviero/status/1797291569348751848
  - In their PDF Editor to generate alt text for images
  - Improve translations
  - Fully offline, open-source and with <200M models
- [Experimenting with local alt text generation in Firefox Nightly - Mozilla Hacks - the Web developer blog _202405](https://hacks.mozilla.org/2024/05/experimenting-with-local-alt-text-generation-in-firefox-nightly/)
  - https://huggingface.co/Mozilla

    - 提供了数据集和模型

- Offline and open-source is a big win for privacy-focused tools

- ## [langchain到底该怎么使用，大家在项目中实践有成功的案例吗? - 知乎](https://www.zhihu.com/question/609483833)
- LangChain之所以大火，是因为它提供了一系列方便的工具、组件和接口，大大降低了 AI 应用开发的门槛，也极大简化了大模型应用程序的开发过程。
  - LangChain框架背后的核心思想是将自然语言处理序列分解为各个部分，允许开发人员根据自己的需求高效地定制工作流程。
- Langchain有6大核心模块：
  - Models：模型，是各种类型的模型和模型集成。
  - Prompts：提示，包括提示管理、提示优化和提示序列化。
  - Memory：记忆，用来保存和模型交互时的上下文状态。
  - Indexes：索引，用来结构化文档，以便和模型交互。包括文档加载程序、向量存储器、文本分割器和检索器等。
  - Agents：代理，决定模型采取哪些行动，执行并且观察流程，直到完成为止。
  - Chains：链，一系列对各种组件的调用。
- LangChain 通常被用作「粘合剂」，将构建 LLM 应用所需的各个模块连接在一起。使用Langchain中不同组件的特性和能力，可以构建不同场景下的应用，如聊天机器人、基于文档的问答、知识管理、个人助理、Agent智能体等等。

- 你的这个认识存在一些偏差，首先，依赖API key 是为了你使用大模型厂商的服务和鉴权，这没有什么拉跨的。很多第三方的服务都需要鉴权验证，这是比较主流的方式。
- 可以企业自己部署大模型，这种成本是很高的。从我们自己的实验效果来看，13B 以下的大模型基本就是玩具，优化半天费时费力，而 34B 或者更大的模型，公司部署成本又很高。
- langchain 中的特色是它的 langchain expression language (LCEL），是一种类似 linux 管道形式的调用方式，可以很简单的实现它的 chain 相关的功能。这个，在我实际使用的时候，没有想象的那么好用，可以根据实际情况去学习。
- 最后，langchain 中还有一个叫做 langgraph 的组件，能够和 pytorch 一样用搭积木的方式去构造一个有向无环图、循环的链，比 LCEL 更高级。

- 
- 

- ## LLM搞反编译，.not care和Jvav用户再也不用折腾什么混淆了，都没用了
- https://twitter.com/geniusvczh/status/1774053196039962758
  - 文章里反编译的是x86, x86都可以，IL难度只会更低
- 大概看了一下，就是把编译出的汇编跟源代码做了一个简单的seq2seq的fine tune，训练集连混淆都没有，离让所有混淆都没用那更是还差得远。
- 17年google那篇transformer的论文就靠这样完成了自然语言的翻译，这些都是迟早的事，反编译和反混淆的训练数据都是可以批量生成的，做起来简单多了
  - 我觉得LLM对于反编译和反混淆，可能更大的作用在于生成人类友好的变量/程序结构。毕竟反编译和反混淆是猫鼠游戏，总可以想出新点子，人类的干预还是必不可少的，这种情况下，基于规则/程序分析的传统方法可能更好，然后再用LLM猜变量名
- 为了拉资金而已，钱申请到了论文就没啥用了……处理屎山留给巨头的程序员就行了，还轮不到学术圈来指点江山
- 这种局限于函数的反混淆啥用都没有，对付点三脚猫功夫的混淆还差不多

- ## 🪧 研究了一下本地大模型的场景：
- https://twitter.com/changmingY/status/1773336179296887162
  1. 不能联网的国内用户
  2. 一般用户机器配置达不到，效率太差
  3. 本地知识库算是一个刚性需求
  4. 垂直领域模型越来越多, 一个hub集中使用
  5. 小而美的模型会越来越多，完成一个特定功能

- ## ollama 的编译玩的太花了，先是吧 llama.cpp 在不同 cpu 和 gpu 的动态链接库都编译了出来避免用户在运行时再去编译，
- https://twitter.com/liumengxinfly/status/1767073319956971891
  - 然后用 go 的 embed 特性直接把这些动态库全都打包到 go 的二进制里，然后在用 cgo 和 dlfcn 加载和调用 llama.cpp，实现了一个二进制文件免编译，免安装的解决所有问题

- https://twitter.com/holegots/status/1767427148506431665
  - 不过这个本质也是 llama.cpp 套壳吧 , 底层还是 cpp, golang 并不参与实际的推理.

- ## 最新版的 OpenAI Translator 已经无缝支持本地大模型了（Ollama），无需联网，快速便捷，安全稳定！再也不怕 OpenAI 账号被封了！翻译效果对比大家可以看一下截图，大家快来下载体验一下吧！ _202402
- https://twitter.com/yetone/status/1761607398819840511
- 现在好像还不支持自定义模型？只有有限的几个模型可供选择，最好是有一个文本框可以自定义输入
- 这是Mistral多大的模型，7B的吗？
  - 是的

- 不知道这些7b 13b的小模型哪个翻译质量更高

- ## 阿里云竟然支持这么多模型了
- https://twitter.com/yihong0618/status/1746745371441967540
- http://ai.azure也包含了好多模型，昨天惊到了

- ## 越来越觉得 RAG 这东西有意思。
- https://twitter.com/wwwgoubuli/status/1737471851654160548
  - 半年前接触到这个词的时候开始我还有些不屑，搜索内容插入到提示词算什么嘛，小学二年级都能明白。尤其是看到随便丢向量库都能跑出个七七八八，越发觉得这个简单。
  - 但现在真的搞了半年，我越发的觉得这才是下一个大多数人可以参与的风口。它有门槛。
- 技巧很多 所以好玩 但风险是大部份技巧都被模型提供商玩过，80%需求都可能被他们直接覆盖
  - RAG不就是query transformation/rewrite/expanding, hybrid search, reranking, etc吗？当然还有些其他技巧啥IAG之类的。数据ingestion也有些技巧，不过我看主要还是在query上。 这些大部分OAI, Baichuan, 月之暗面内部都探索过了吧
- RAG一看就是一个有问题的区域，大模型随时下一次升级可能就会改变整个框架，3.5还胡说八道，4已经很多都是有根有据的了
- 搞到最后，还是清洗数据，RAG只用简单策略解决大多数问题，可观测。前提是所有复杂策略都要试过才知道。

- ## LangChain开源了AnythingLLM：可以与任何内容聊天的私人 ChatGPT，应该就是他们自己文档系统用的那一套。
- https://twitter.com/op7418/status/1733893368974073873
  - An efficient, customizable, and open-source enterprise-ready document chatbot solution.
  - https://github.com/Mintplex-Labs/anything-llm /MIT/js/python

- 有没有详细说明？最大可以支撑多大的文档？
  - 应该是不限大小的，拆开就好了
- 说没说硬件需求？

- ## 大模型的这些 benchmark 应该是全宇宙最没用的 benchmark 了吧？
- https://twitter.com/yihong0618/status/1721401347533324688
- 也不是全没用，也有一些有用的, 尤其细分任务上的，还是挺有用的。当前相比其他benchmark，可操作空间确实大
- 公开的只能全看自觉

- ## 中文开源模型虽多，数据集却很少开源。
- https://twitter.com/9hills/status/1718828132046942218
  - 目前英文 7B 规模的 SOTA 模型是 zephyr-7b-beta。它放弃了质量参差不齐的开源数据集，使用ChatGPT和GPT-4 全新标注了 UltraChat 和 UltraFeedback 数据集（已开源）。是 llama-index 项目实测出来唯一能够支持 Agent 的小参数模型。
- 中文数据集都是拿来卖钱的
