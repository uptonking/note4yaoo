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

- ## 📌 LLM 出来之后，在应用层的折腾从未停歇。从 Prompt 调优到 Workflow 配置，再到 Agent 构建，最终目的都是一样的：让 LLM 更好地为人类干活，把机器的性能压榨到极致。
- https://x.com/Barret_China/status/1973188130091180466
- 对 LLM 的压榨，可以分为两个维度。
- 一是帮助它找到最优算法，让推理少走弯路。
  - 为此我们几乎把能想到的路子都走了一遍，让 LLM 学会反思（reflection、self-consistency、self-critics），学会推理和规划（reasoning、planning、chain-of-thought、tree-of-thought）；学会记忆（short-term memory、long-term memory），不至于对话一长就失忆；学会找知识（RAG、knowledge graph），在外部世界里补充事实；学会构建上下文（context building），在有限 token 里塞下更多有效信息；学会用工具（tool-use，function calling，MCP），把事情交给外部程序去跑，而不是光靠自己生成；等等。
  - 这些东西，说到底都是技巧和机制，本质目的是让 LLM 更快理解人类要干啥，围绕目标（goal-oriented）尽可能找到一条代价最小的路，跑到最优解上去。
- 第二个维度，是对时间的压榨，让 LLM 可以做到 7×24 小时不停歇。
  - 当我们对 LLM 有了更深入的理解之后，很容易想到把它打造成属于自己或组织的“数字员工”，它不知疲惫、不会抱怨，可以持续运转、不断学习。
- 大部分人今天用 AI 的方式，还停留在查资料、总结内容、写周报月报这些单点场景上，如果要真正构建一名“不停歇的 AI 数字员工”，光靠这些还不够。我们需要先规划出属于自己的 AI 数字工厂 ——想清楚要造出来的“产品”是什么，是沉淀知识的系统，是自动化的业务流程，还是一个可以长期迭代的服务。
  - 在这座工厂里，AI 是生产线上的执行者，它负责具体的加工与产出；而人类的角色发生了转变，从“亲自干活的工人”变成“监工与管理者”。 人类不再亲手完成每一步，而是要设计流水线，设定规则，制定指标，监控质量，并在需要时调度资源。换句话说，AI 的价值不在于替我们“干一点活”，而在于帮把整条流水线跑起来，而人类更像是“数字工厂的管理者”。
  - 当这两个维度结合起来时，真正的拐点就出现了。LLM 不再只是一个冷冰冰的工具，而是逐渐变成了可以长期协作的伙伴。它既能承担重复性劳动，也能在复杂问题上提供洞见。它不仅仅是“帮你做事”，更是“和你一起做事”。
  - 未来的差距，不在于谁能写出更漂亮的 Prompt，而在于谁能把 LLM 真正融入到自己的时间和组织里，形成稳定的生产方式。
  - 因此，会不会用、用到什么深度、能否持续优化，这些才是长期的竞争力来源。谁能把 AI 运行成“工厂”，让自己从执行者转为监工和管理者，谁就能在未来的日常工作和业务中，获得真正可复用、可累积的优势。

- 代码抽象真实世界的时代快要结束了，欢迎来到token 抽象真实世界的时代。

- 如果TOKEN投入产出是正向的，恨不得他不休息 

- 问题来了，我要做什么，AI要怎么帮我做

- ## 📱 [端侧模型会是 AI 技术演进的下一个 「必争之地」 吗？当前落地面临哪些核心瓶颈？ - 知乎](https://www.zhihu.com/question/1914319403023032351)
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

- ## [Q: When will there be fast and competent SLMs for laptops? : r/LocalLLaMA _202512](https://www.reddit.com/r/LocalLLaMA/comments/1pcurp8/q_when_will_there_be_fast_and_competent_slms_for/)
  - Qwen3-30B-A3B and GPT-OSS-20B both uses Mixture-of-Experts instead of dense layers for their SLM
  - Kimi-Linear and Qwen3-Next-80B-A3B moved along to use "mixed attention" (majority of layers with linear attention) to speed things up AND have longer contexts
  - Not enough people getting into ternary attention like BitNet a4.8 / BitNet v2 or ternary quantization (PTQ)
  - Whatever layer routing is to reduce the amount of RAM needed, including Ouro-2.6B-Thinking these days and Mixture-of-Depths back in 2024
  - Are all of these different techniques conflicting with one another? If it is just a lack of funding for fine-tuning/modding an existing SLM into something fast (assuming QAFT and RL), how much would it cost to crowdfund a project like this?

- It depends on your standards, I believe that for the average Joe, something like Ling Mini 2.0 would already check those requirements (fast -> 1B active is doable for most modern laptops at 20+ tok/s) (Competent -> 16B total parameters makes it decent enough for 99% of the tasks an average person would likely use it for)

- For most people, Llama3 8B was the moment where their laptop could handle a ton of their work and queries locally.

- I use Ling mini to correctly format the ocr result of screenshots. Its the fastest and adheres well to long system prompt. All on cpu.

- We already have that. Llama 3.2 3B for writing. Gemma 3 for multimodal. Qwen 3 4B for stem. Granite 4 for rag.
  - The issue is that the active/ dense parameter count determines the limit of how intelligent the overall model is. The mixture of experts kinda determines how big the model's encyclopaedia is.
  - Its possible to argue that llama 3.2 3B, gemma 3 4B and Qwen 3 30b are around the same level in writing. But Qwen 3 30b is clearly the one with more knowledge.
  - There is also the requirement for AI to have ethics and emotions, which is frankly way too complex to fit into an SLM without lobotomising it.
  - Laptop ram is just too limited in bandwidth and capacity

- I am tempted to suggest RAG-ing an SLM into being better than just being slowed down by a 32B dense model (8B or 14B on higher-performance laptops), and since dense models are "more intelligent" compared to MoE... Maybe BitNet is a more or flexible layer activation is a workaround then?

- Bitnet and ternary are out as they need specific hardware

- ## [I'm surprised how simple Qwen3 VL's architecture is. : r/LocalLLaMA _202512](https://www.reddit.com/r/LocalLLaMA/comments/1pcomhi/im_surprised_how_simple_qwen3_vls_architecture_is/)
- Most machine learning architecture isn’t really that complicated when you look at it in code. Plus, in software development simplicity = better.

- training pipeline probably much more complicated

- To be honest... The entire domain of LLMs and even VLMs are fairly simple... Working in self driving for over 5 years exposed to bespoke perception and multi task models, it shocked me how simple LLMs are, especially training it from the model side.
  - The literal loss function for LLMs during pretraining and finetuning is just cross entropy... Compare that to something more complicated like YOLO, it's actually insane in terms of difference of complexity.
  - Really the solution now.... Stack some transformers, use a LM head, chunk input for VLMs into patches... Pretty damn simple I have to say

- The nicest part of Qwen3-VL is that most of the “magic” comes from small, well-chosen inductive biases rather than a baroque stack. It’s basically ViT → lightweight bridge → plain decoder LLM, with two tasteful upgrades: interleaved 3D positional encoding (i-MRoPE) and DeepStack feature fusion.

- In my experience it is not very good at producing accurate coordinates of items it sees

- ## [Finally DeepSeek supports interleave thinking : r/LocalLLaMA _202512](https://www.reddit.com/r/LocalLLaMA/comments/1pbal3o/finally_deepseek_supports_interleave_thinking/)
  - If a thinking model supports multi-step tool calls and can incorporate thinking from historical steps during these calls, then this model supports interleaved thinking.
  - So far, among open-source models, only GPT-OSS, Kimi K2 Thinking, and MiniMax M2 support it, and I believe this feature is crucial for agents.
  - Interleave thinking lets an AI agent reason, act, and observe in tight loops, so it can adapt step-by-step to new information instead of blindly following a fixed plan.

- Why is special support needed? Each request to an LLM is whole conversation, and you can eliminate previous thinking blocks at each request. What am I missing here?

- ## [Experimenting with Multiple LLMs at once? : r/LocalLLaMA _202511](https://www.reddit.com/r/LocalLLaMA/comments/1p4pre3/experimenting_with_multiple_llms_at_once/)
- I do mostly coding, so different families of models get wildly different python training data. Having each do the same coding task and then have another model pick the best components of the script for a new third script works really well.
  - Open web UI also has channels, which is a discord style chat room. You can tell the models you have to collaborate with each other on a project and they will take turns with sections of code.

- I had them do a few rounds of back and forth checking each other's work. It produced noticably better results than either model could on their own - but the time it took made it pointless. It was faster to just use a larger/slower model, allow a reasoning model to go nuts with thinking tokens, or just iterate myself. 
  - For tasks that aren't time sensitive there's some value there. 

- I like the idea of this and have experimented. I don’t have a great way to have them collaborate in real time, but using two to check each others work just seems smart to me.

- Andrej Karpathy just posted about a vibe coded project he did called LLM Council that seems pretty cool: https://github.com/karpathy/llm-council

- Here's mine: GitHub.com/irthomasthomas/llm-consortium It's cli based but you can also save a multi-model consortium and use it like a regular model. Then you can use llm-model-gateway to serve that on a openai proxy and use it like a normal model in your tools.

- ## [Instead of either one huge model or one multi-purpose small model, why not have multiple different "small" models all trained for each specific individual use case?   r/LocalLLM _202511](https://www.reddit.com/r/LocalLLM/comments/1ovsb2x/instead_of_either_one_huge_model_or_one/)
- This is already how MoE (Mixture of Experts) models work. There are plenty of them on huggingface, though I think the separation of the 'experts' often isn't quite so clean. You also have to consider some other things -- your 20B param 'python only' expert model is almost unusable if it doesn't also understand variable names and comments and instructions in natural language, there does have to be some baseline knowledge to make a coding model actually useful, not *just* code in the training data.
- That's kinda what a MOE model is/does. Each of the "experts" are specialists in different trained things and it picks the active ones to use based on the prompt from the user.

- some people mentioned MoE, but MoE works differently. MoE makes decisions for each token separately, not for whole answers. So training many small, specialized models is not the same thing as using MoE.

- Your idea is exactly what Microsoft is attempting with its Phi series of models. They intend to build an ecosystem of models trained on very specific tasks, and then have an agentic system that uses a simple model to process the users request, decide the best model to use, and use that model to answer the question.
  - I believe Google is doing something similar with Gemini, and there are rumors that GPT 5 functions the same way.

- Perfect routing is not a solved problem. In general you have to get part of the way through solving a problem before figuring out exactly what is necessary to solve it.

- ## Every LangGraph user I know is making the same mistake! They all use the popular supervisor pattern to build conversational agents.
- https://x.com/akshay_pachaar/status/1983874390149484881
  - The pattern defines a supervisor agent that analyzes incoming queries and routes them to specialized sub-agents. Each sub-agent handles a specific domain (returns, billing, technical support) with its own system prompt.
  - This works beautifully when there's a clear separation of concerns.
  - The problem is that it always selects just one route.
  - For instance, if a customer asks: "I need to return this laptop. Also, what's your warranty on replacements?"
  - The supervisor routes this to the Returns Agent, which knows returns perfectly but has no idea about warranties.
  - This gets worse as conversations progress because real users don't think categorically. They mix topics, jump between contexts, and still expect the agent to keep up.
  - This isn't a bug you can fix since this is fundamentally how router patterns work.
  - Now, let's see how we can solve this problem.
  - Instead of routing between Agents, first, define some Guidelines.
  - Each guideline has two parts: - Condition: When it gets activated? - Action: What should the agent do?
  - Based on the user's query, relevant guidelines are dynamically loaded into the Agent's context.
  - This approach is actually implemented in Parlant - a recently trending open-source framework (15k+ stars).
  - Instead of routing between specialized agents, Parlant uses dynamic guideline matching. At each turn, it evaluates ALL your guidelines and loads only the relevant ones, maintaining coherent flow across different topics.
  - Another key advantage is that dynamic guidelines keep the system prompt clean, ensuring the agent receives only the right instructions at the right time.

- Hmm won’t a fully connected sub agent flow with planning enabled work here where one agent can route to any sub agent if it can’t handle the task. So if realize the user needs more than one thing to be done the agent plans the steps and assigns to the required agent , task is executed result return until the final agent and one agent gives a combined answer

- It's written in python, nothing is stopping a string split and route two agents and join intelligently at the end.

- This seems like another form of "skills" that claude just released. Where the different skills are used to solve the flows and problems independently.  Its just making sure that all the parts are handled.
  - Yes the ideas are certainly relatable

- You can have the supervisor select a set of relevant agents instead of just one though
  - I get your point. However, real users don't think categorically. They mix topics, jump between contexts, and still expect the agent to keep up at every turn of the conversation. You need something that can dynamically load context at every turn. That's where @ParlantIO shines!
- I agree that this per turn dynamic context loading for the supervisor is effective however if there are agents added as tools to one of these guidelines then effectively its like dynamically selecting a subset of composite agents and then ReAct on this context. I actually did something very similar in one of my agents about data analysis where the per turn strategy would be selected dynamic (model, prompt and tools). I think as i said subset selection is just one of the possible single route out of all possible subset routes.

- ## [I Built Pocket Flow, an LLM Framework in just 100 Lines — Here is Why _202503](https://medium.com/@zh2408/i-built-an-llm-framework-in-just-100-lines-83ff1968014b)
- After a year of struggling with bloated frameworks, I decided to strip away anything unnecessary. The result is Pocket Flow, a minimalist LLM framework in just 100 lines of code.

- After a year of building LLM applications from scratch, I had a revelation: beneath all the complexity, LLM systems are fundamentally just simple directed graphs.
  -  By stripping away the unnecessary layers, I created Pocket Flow — a framework with zero bloat, zero dependencies, and zero vendor lock-in, all in just 100 lines of code.
- We also support batch processing, asynchronous execution, and parallel processing for both nodes and flows.

- Unlike other frameworks, Pocket Flow deliberately avoids bundling vendor-specific APIs. 
  - No Vendor Lock-in: You’re free to use any model you want, including local models like OpenLLaMA, without changing your core architecture.

- [I Built an LLM Framework in 179 Lines—Why Are the Others So Bloated?  : r/LangChain _202502](https://www.reddit.com/r/LangChain/comments/1iwrhuu/i_built_an_llm_framework_in_179_lineswhy_are_the/)
- I had a look at the code. You've built a simple state machine. 
  - State machine are almost aways the worst time of choice when it comes to composition. 
  - In other words organising everything in flows of Nodes while still writing code is worse then for example carefully providing the data structures yourself and deal with the concurrency and dataflow based on the application specific requirements.
- Thanks for the feedback and example. I opted for a state machine for its simplicity! I'm open to finding a way to balance simple state transitions with tailored data structures though

- how is this different to the approach LangGraph took?
  - We think LangGraph’s approach can feel rigid and tends to enforce a strictly linear, single-threaded execution model! We also want to do more than just manage state transitions!!
  - For example, we can handle asynchronous capabilities—like node cloning to avoid race conditions and dedicated AsyncParallelBatchNodes and AsyncParallelBatchFlows—to enable parallel execution. This means you can run I/O-bound tasks concurrently (such as multiple LLM calls) without being restricted to a single-threaded, linear flow.

- ## 🤔 [I built an AI orchestration platform that breaks your promot and runs GPT-5, Claude Opus 4.1, Gemini 2.5 Pro, and 17+ other models together - with an Auto-Router that picks the best approach : r/LocalLLaMA _202510](https://www.reddit.com/r/LocalLLaMA/comments/1o76n9d/i_built_an_ai_orchestration_platform_that_breaks/)
  - I've been frustrated with choosing between AI models - GPT-5 is great at reasoning, Claude excels at creative writing, Gemini handles data well, Perplexity is best for research - so I built LLM Hub to orchestrate them all intelligently.
  - [LLM HUB - AI Pipeline Orchestration](https://llm-hub.tech/)
  - The Core Problem: Each AI has strengths and weaknesses. Using just one means compromising on quality.
  - 💡 The Solution: LLM Hub coordinates 20+ models across 4 execution modes:
- 4 EXECUTION MODES:
  - Single Mode - One model, one response (traditional chat)
  - Sequential Mode - Chain models where each builds on the previous (research → analysis → writing)
  - Parallel Mode - Multiple models tackle the same task, synthesized by a judge model
  - 🌟 Specialist Mode (the game-changer) - Breaks complex tasks into up to 4 specialized segments, routes each to the expert model, runs them in parallel, then synthesizes everything

- ## Code2Video - 通过代码生成教育视频的 AI Agent 框架，来自新加坡国立大学 Show Lab 的最新研究，论文和开源项目都发布了。
- https://x.com/shao__meng/status/1974280130420961548
  - 通过 AI Agent 的方式生成类似 3Blue1Brown 的视频，很有趣，咱们一起看看。
  - 方法核心：三智能体协作, 设计框架分解任务为三个协作智能体，形成模块化管道：
  - · Planner（规划者）：从学习主题（如“线性变换与矩阵”）生成大纲和故事板，确保时间连贯性（如概念引入、扩展和回顾）。它集成外部数据库，检索参考图像和视觉资产（如图标），并考虑受众水平（如高中生 vs. 大学生），以提升事实准确性和视觉一致性。
  - · Coder（编码者）：将故事板转换为可执行 Manim 动画代码。采用并行合成策略加速生成，并引入 ScopeRefine（范围引导修复）机制：从行级（局部修复错误行）逐步扩展到块级和全局重生，确保代码高效且无语法错误，同时保持跨节一致性。
  - · Critic（批评者）：使用视觉语言模型（VLM）和锚点视觉提示（如占用表和位置网格）迭代精炼渲染视频。针对空间问题（如重叠或空旷区域），它提供具体解决方案（如调整对象位置或缩放），提升布局清晰度和教育吸引力。
  - 整个流程从用户查询输入，到输出教育视频，通常需数分钟渲染，远优于端到端像素生成。

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

# discuss-ai-format/interop
- ## 

- ## 

- ## 

- ## [Use YAML over JSON when dumping into prompts for ~2x token saving : r/ChatGPTCoding _202509](https://www.reddit.com/r/ChatGPTCoding/comments/1nl7xux/use_yaml_over_json_when_dumping_into_prompts_for/)
  - [YAML vs. JSON: Which Is More Efficient for Language Models? _202307](https://medium.com/better-programming/yaml-vs-json-which-is-more-efficient-for-language-models-5bc11dd0f6df)
  - It's been pointed out in the comments (with sass) that minifying your JSON is another, perhaps even better, alternative than transforming to YAML. So now there's two options for saving tokens.

- Does the guy who wrote the article know that you don't need to use whitepaces in JSON and you can minify it to consume less space than YAML? Generally speaking, JSON is more space-efficient and compact than YAML.

- Just remove the spaces and condence the JSON into a single line. LLMs don't care about spaces, it's a visual thing for us.

- Thought LLM's don't count white space as context... or if they did, it would be incredibly minimal
  - They kind of have to, if only to correctly write Python
  - ASCII art too

- Another point is accuracy... some like XML more as well - and there is BAML. If i just wanna save money I could get a cheaper model too.
- xml is also what Claude officially recommends for better accuracy.

- I use YAML and JSON, because i use the CMS Drupal since 2006 - so this fits quite well in my workflow

- TOML is actually more verbose when it comes to complex data structures.
  - Which makes sense since it was designed to be a JSON/YAML mappable language for better human readability.
# discuss-local-llm-usecases
- ## 

- ## 

- ## 

- ## 

- ## [The curious case of Qwen3-4B (or; are <8b models *actually* good?) : r/LocalLLM _202511](https://www.reddit.com/r/LocalLLM/comments/1p76wtf/the_curious_case_of_qwen34b_or_are_8b_models/)
  - how good are the smaller models at answering some of the sort of questions I might ask of them, chatting, instruction following etc?
  - I ran each model's output against the "council of AI elders", then got GPT 5.1 (my paid account craps out today, so as you can see I am putting it to good use) to run a tally and provide final meta-commentary.
  - The results, per GPT 5.1: GPT-OSS 20B and Qwen 3-4B emerged as the strongest overall performers. Mid-tier models like DeepThink 7B and Qwen 2.5 7B produced competent technical content but struggled severely with the style transform, while Phi-Mini 4B showed the weakest combination of accuracy, coherence, and instruction adherence.
  - The results align closely with real-world use cases: larger or better-trained models excel at technical clarity and instruction-following, whereas smaller models require caution for detail-sensitive or persona-driven tasks, underscoring that the most reliable workflow continues to be “strong model for substance, optional model for vibe.”

- I’m using qwen3-4b 2507 instruct for simple tasks such as meeting summarization, keeping track of to-do’s and the likes. So far, it has performed quite well

- ## [My Journey to finding a Use Case for Local LLMs : r/LocalLLM _202511](https://www.reddit.com/r/LocalLLM/comments/1p1xy0q/my_journey_to_finding_a_use_case_for_local_llms/)
  - I have a lot of phone pictures of recipes, and a lot of inherited cookbooks. The thought of gathering the ones I really liked into one place was daunting. The recipes would get buried in mountains of photos of cats (yes, it happens), planes, landscapes etc. Google photos is pretty good at identifying recipe images, but not the greatest.
  - I landed on qwen3-vl:8b. It was able to take the image (with very strict prompting) and output the exact text from the image. I did have to verify and do some editing here and there. I was happy
  - I then turned to GPT-OSS:20b since it is newer, and asked it to convert the recipe text to json-ld recipe schema compatible format.
  - Now I can take a pic of any recipe I want, run it through the qwen-vl:8b model for OCR, verify the text, then have GPT-OSS:20b spit out json-ld recipe schema text that can be imported into the mealie database. (And verify the json-ld text again, of course).
  - I'm not using any system prompts at this time. Here is the prompt

- You could now take this even further and query it with a prompt on your cell phone.

- My use case is that I use local vlm to the content of the download file, then rename following the format I define and use bash script to route it to the its dedicated folder. Now every time a file is downloaded, it is renamed and route to its location automatically.
# discuss-local-llm-xp/tips
- ## 

- ## 

- ## 

- ## 

- ## 

- ## ["We're in an LLM bubble, not an AI bubble" - Here's what's actually getting downloaded on HuggingFace and how you can start to really use AI. : r/LlamaFarm _202512](https://www.reddit.com/r/LlamaFarm/comments/1pb2wr2/were_in_an_llm_bubble_not_an_ai_bubble_heres/)
  - Encoder-only models (BERT family) account for 45% of HuggingFace downloads, nearly 5x more than decoder-only LLMs at 9.5%. 
  - Every one of these model families exists because someone realized the "one model to rule them all" approach was failing for their use case
  - This is "Mixture of Experts" at the application level. Many small, specialized models working together instead of one massive model trying to do everything.

- ## [What broke when you tried to take local LLMs to production? : r/LocalLLaMA _202511](https://www.reddit.com/r/LocalLLaMA/comments/1p91p4k/what_broke_when_you_tried_to_take_local_llms_to/)
- Ollama broke a lot of the time because we dev’d on a Mac but pushed production to nvidia. Switching to vllm has largely solved this and pushed it to more of an interface rather than model problem.

- Hosting several Models on one GPU is always really annoying with vLLM. You basically have to fiddle with the memory utilisation until all models fit. There is no clean way I found to calculate memory usage. You just have two tweak, boot, look at the logs and repeat. And even if you got all models to fit, vLLM sometimes crashes with cuda out of memory exceptions when loading the models since there seems to be a peak in memory consumption on boot up.

- Why doesn't anyone mention tabbyAPI/exllamav3? It's much more memory-efficient than AWQ, also it loads quicker, and the quantization is more optimized. Also K/V cache can be quantized between 2 and 8 bits seperately (=more room for context)

- ## [Why do you use open-source LLMs ? : r/LocalLLaMA _202511](https://www.reddit.com/r/LocalLLaMA/comments/1p16kxx/why_do_you_use_opensource_llms/)
- Freedom. I can do whatever I want without having my data stolen.

- The benefit of open source LLMs for me is that you can access the internal layers to do things like attention injection, intermediate layer feature extraction, attention map extraction, token-wise early stoppage, adaptive layer skips, conversion to latent attention, conversion to mamba or gated delta net hybrid etc
  - This is it. Intervening mathematically in something that can talk like a human is an otherworldly experience. I do it almost every day and it makes me feel like an alchemist tinkering with a homunculus. There’s nothing else like it. Most other intellectual activities feel shallow by comparison.

- I just think it's very cool to have a summary of the vast wealth of human text and knowledge in a 30GB file on my computer.

- I want to own my capabilities. I don’t want my coding skills to be tied to some external service that I have zero control over.

- ## [What do you use local LLMs for? What is your use case? : r/LocalLLaMA _202508](https://www.reddit.com/r/LocalLLaMA/comments/1ms4gmz/what_do_you_use_local_llms_for_what_is_your_use/)
- They are best used for small context tasks like classification/sentiment, asking it summarize, pull out keywords, grammar, etc.
  - Not for long conversations or complex tasks, but system prompt, user request, and then get a single response.
  - For example, I've been experimenting with a local LLM checking chat messages for rule-breaking in a Discord server, flag the suspicious once, and then I checked the flagged messages and take action myself.

- I used it to generate a synthetic dataset for training my first neural network, with successful results.

- Structured data extraction from private documents (millions of documents)
  - We have produced an annotated dataset of a few thousand records. We used this to fine tune a model and evaluate performance. We are getting >0.98 F1 score which is a margin of error we are willing to tolerate given the scale and time saved... It's for a very specific type of short documents. Our extraction pipeline has multiple extraction and validation steps.

- Data extraction and classification.

- ## [What are you using your local models for ? : r/LocalLLaMA _202511](https://www.reddit.com/r/LocalLLaMA/comments/1oz6k5j/what_are_you_using_your_local_models_for/)
- Confidential research. In SillyTavern. Just yet with a quantized Skyfall-31b from Drummer, apparently some blend of Mistral Small or whatever. It's fun.

- Qwen3-VL-30B-A3B-Thinking is heating my home by processing video. I've posted about it before but llm-ffmpeg-edit.bash handles the logic & llm-python-vision-multi-images.py handles sending the images/frames to the LLM backend.
  - I was using Mistral 3.2 (24B dense) before Qwen3-VL got support. The speed increase from 24B -> 30B-A3B has been incredible, while maintaining accuracy.

- I'm bound by the legal terms of my employment to not discuss the technologies we use there, but am free to talk about my personal use-cases.
- STEM research assistant -- I give it my technical notes (usually physics and/or math) and a question, and get back helpful replies. My go-to is Phi-4-25B, and when it's not smart enough I escalate to Tulu3-70B, sometimes Qwen3-235B pipelined with Tulu3-70B.
- Creative writing -- Cthulhu-24B, Big-Tiger-Gemma-27B-v3, or Valkyrie-49B-v2. Mostly sci-fi (space opera or Murderbot fanfic).
- Evol-Instruct and synthetic dataset generation or augmentation -- again, mostly Phi-4-25B or Tulu3-70B, though recently I have been using Valkyrie-49B-v2 to bulk up a RAG database of technical troubleshooting advice/solutions. To my surprise Valkyrie is a lot better at this than Tulu3-70B, even though they are derived from similar models (Tulu3 from Llama-3.1, Valkyrie from Llama-3.3-Nemotron-Super-49B-v1.5 which in turn is based on Llama-3.3).
- Persuasion research -- studying the capacity for LLM inference to change people's minds. Big-Tiger-Gemma-27B-v3 is excellent at this.
- Wikipedia-backed RAG for general question-and-answer. I use Big-Tiger-Gemma-27B-v3 for this as well.
- Describing images so I can index them in a locally hosted search engine. Qwen2.5-VL-72B is still the best vision model I've yet used, but I haven't had a chance yet to compare it against Qwen3-VL-32B. I am hoping Qwen3 is better, despite having fewer than half as many parameters.
- I also run an IRC bot for a technical support channel, which is mostly GOFAI-driven but I've been working on a plugin for it to be RAG/LLM-driven too. That, too, uses Big-Tiger-Gemma-27B-v3.
- Recently I've been trying to use Phi-4 (14B) as a synthetic dataset rewriter, to salvage low-quality inferred data I would normally prune from the dataset. I read a paper suggesting even very small models (4B) are effective at this. So far my results have been mixed. I've been meaning to try Tiger-Gemma-12B-v3 as well; possibly Phi-4 just isn't the right model for this.
- GLM-4.5-Air for slow inference of entire programming projects (which I don't do much, since I don't want my coding skills to atrophy) or to find bugs in my own code.
- Qwen3-Coder-REAP-25B-A3B for fast FIM code inference. The model doesn't have to be smart to figure out what my "for"-statement is going to look like, but it does need to be fast enough that it can suggest a completion before I've finished typing the "for"-statement myself. I use the REAPed version of this model so that it fits in my GPU's VRAM (at Q4_K_M); the original 30B-A3B didn't quite fit.
- I'm also tentatively using Phi-4 as a judge, comparing two replies to the same prompt and telling me which is better. It's early days yet, for this project, and it might not be the right model for this. We will see.
- Sometimes I use Big-Tiger-Gemma-27B-v3 or Phi-4 (14B) for language translation (mostly Spanish to English, but sometimes German or Russian to English). Overall Big Tiger is better at this, though Phi-4 does surprisingly well, and is better than Big Tiger at taking situational context into account with its replies. It's also a lot faster than Big Tiger, which is sometimes important for translation tasks.

- ## [Are any of you using local llms for "real" work? : r/LocalLLaMA _202511](https://www.reddit.com/r/LocalLLaMA/comments/1otnj2k/are_any_of_you_using_local_llms_for_real_work/)
- The most "real" work I've done is that Qwen3-VL-30B-A3B-Thinking is currently going through videos 10-seconds at a time. 
  - Based on the bot's True/False boolean output a wrapping program keeps track of what segments `<thing I'm looking for>` is within. At the end, we're done using Qwen3-VL and the wrapping program uses the segment information to use FFMPEG to make a clipped version where `<thing I'm looking for>` should always be present.
  - A general example is you could have the bot look for every explosion in an action film. Maybe it considers muzzle flash from a gun to be an explosion, not technically wrong as far as I know. So you could prompt that it should only be explosions not from gunfire and try that.

- I use an LLM, a scraper to fetch security vulnerabilities (CVEs), and an internal API that lists my running services, and the LLM generates a daily report for me about whether any of the software I'm running might have been mentioned.

- Using qwen3 vl to parse vids to extract car plate numbers snd other vehicle markings

- I used a local LLM and a vector database to help me with my corporate taxes. I first fed all past 3 or 4 years of expenses along with their categorizations (meals, fuel, office supplies etc.) into a Postgres PG Vector database and embedded the data using the Nomic model. I then classified several hundred transactions for the past tax year using this vector set of data to categorized the transactions.

- I use nvidia/Llama3-ChatQA-1.5-8B to index 2M similar insurance docs using ollama. I load the index into Meilisearch and sell access to it. I did this after a trip to micro center and a little over $3k.

- I use them as zeroshot NER/Classification models. They're pretty decent at it out of the box. Training isn't too complicated, but for small repetitive tasks, they're often good enough.

- ## [Why we shifted to Spec-Driven Development (and how we did it) : r/ClaudeCode _202511](https://www.reddit.com/r/ClaudeCode/comments/1op8b6i/why_we_shifted_to_specdriven_development_and_how/)
  - Over the last few months we came up with our own Spec-Driven Development (SDD) flow that we feel has some benefits over other approaches out there. 
  - Specifically, using a structured execution workflow and including the results of the agent work. 
- In short: you design your docs/specs first, then use them as input into implementation. And then you capture what happens during the implementation (research, agent discussion, review etc.) as output specs for future reference. 
- The cycle is:
  - Input specs: product brief, technical brief, user stories, task requirements.
  - Workflow: research → plan → code → review → revisions.
  - Output specs: research logs, coding plan, code notes, review results, findings.
- By making the docs (both input and output) first-class artifacts, you force understanding, and traceability. The goal isn’t to create a mountain of docs. 
  - The goal is to create just enough structure so your decisions are traceable and the agent has context for the next iteration of a given feature area.
- First, worth mentioning this approach really only applies to a decent sized feature. Bug fixes, small tweaks or clean up items are better served just by giving a brief explanation and letting the agent do its thing.
- How we implemented it (step-by-step)
  - Define your prd.md**:** goals for the feature, user journey, basic requirements.
  - Define your tech_brief.md: high-level architecture, constraints, tech-stack, definitions.
  - For each feature/user story, write a requirements.md file: what the story is, acceptance criteria, dependencies.
  - For each task under the story, write an instructions.md: detailed task instructions
  - To start implementation, create a custom set of commands that do the following for each task
  - Commit these spec files alongside code so future folks (agents, humans) have full context.
  - Use folder conventions: e.g., project/story/task/requirements.md, …/instructions.md etc. So it’s intuitive.
- Bonus: If you want a tool that automates this kind of workflow opposed to doing it yourself (input specs creation, task management, output specs), I’m working on one called Devplan that might be interesting for you.

- Bmad does exactly this: https://github.com/bmad-code-org/BMAD-METHOD

- have you tried any of BMAD, GitHub/Spec-kit or Privacy-AI/spec-kitty for a community fork with extensive git worktree support

- ## [Which model do you wish could run locally but still can’t? : r/LocalLLM _202511](https://www.reddit.com/r/LocalLLM/comments/1omoodc/which_model_do_you_wish_could_run_locally_but/)
- It's not really about particular models at this point. I'm way more interested in the local infrastructure around it. The main thing I'm still missing is simple knowledge-base integration for something like Open-WebUI. I would really like to just point the front-end at my local Kiwix-server and a 1TB-eBook collection, let it index to its heart's content for a few weeks and then have any model be able to reference and integrate all those information.

- Qwen3 Omni, how come no one is talking about a 30B model that can do video and speech?

- Something which I can install with just a dmg or exe file please
  - I tried a couple but I am not tech savvy and had to install a lot of other stuff to my laptop

- For me, it’s not that it’s a single model I can’t run… it’s the fact that I can’t run multiple models.

- ## [What's the missing piece in the LLaMA ecosystem right now? : r/LocalLLaMA _202510](https://www.reddit.com/r/LocalLLaMA/comments/1o5dh3v/whats_the_missing_piece_in_the_llama_ecosystem/)
  - For me, it's the data prep and annotation tools. The models are getting powerful, but cleaning and structuring quality training data for fine-tuning is still a major, manual bottleneck.

- Training-Data is the biggest issue for local ecosystem right now i think. There is so many datasets, but who knows about their real quality.
  - For me personally, finetuning an LLM is like 500x harder than a diffusion model, simply due to the lack of tooling. Unsloth is nice and all, but i dont want to run fucking Jupyter Notebooks, i want something akin to kohya_ss with as many of the relevant hyperparameters exposed.
- Hardware accessibility is only secondary. If you have a small Model, e.g. the Qwen3 0.6B full finetune should be possible on local hardware. If that proves to be effective, renting a GPU machine somewhere for a few bucks shouldnt be the issue.

- llms are very bad at image recognition, give it a civ or other strategy game screenshot and it gets nearly everything wrong.

- Benchmarks. There has been little to no progress in the past two years regarding how LLMs are evaluated. It’s still mostly huge catalogues of questions with predetermined answers. That’s a very poor system for testing intelligence.
# discuss
- ## 

- ## 

- ## 

- ## 

- ## 

- ## 现在所有的大语言模型，无论它号称上下文窗口可以多少，输入是真的可以很长，但是输出不能太长，输出长了就幻觉严重，相对好一些的是 Gemini，
- https://x.com/dotey/status/1995667479377707123
  - 所以使用时，你可以输入很多资料给它参考，但是每次不要输出太多，比如一次最多输出几千字，多了就要分页。
- 可以采用分几步，然后提供一个checklist确保他自己审核
  - 对，todo list有助于拉回注意力好一些，但一样输出内容不能太长

- 说下我的理解：每个token输出都是一个概率，举个例子：比如说“我”这个字后面跟着“们”还是“的”，对llm来说就是取概率高的。但是概率有2个问题：
  1. 就算每次都取最高的，0.9*0.9*0.9…，整体来看，符合预期的概率越来越低，所以输出太多之后没法保证不走偏
  2. 中间某一个位置，两个token的概率相近，llm选择不小心走偏了之后，后面输出的token会一直在这个走偏的token上继续输出
  - 补充一点，现在LLM有温度设置，不是纯贪心取最大概率的。而且算力有限，无法做到全局最优。只能说篇幅越短，越准确。 现在大家做的CoT，以及利用Agentic workflow不断重写，其实都是在逼近全局最优。

- 个人感觉：Gemini 号称有 100 万的上下文，其实一般跑到 20-30 万字左右就不行了

- 输入和输出对模型来说都是一样的，只要上下文过长，模型或多或少都会出现指令不跟随。

- ## ⏳ [A Tribute to MetaAI and Stability AI - 2 Giants Who Brought us so Much Joy... And, 2025 is the Year they Die... So Sad! : r/LocalLLaMA](https://www.reddit.com/r/LocalLLaMA/comments/1p9ah2v/a_tribute_to_metaai_and_stability_ai_2_giants_who/)
- People think the trillion dollar spend is for the r&d and scale. Research is a fraction of the opex, and the scale is not about breaking through new model features but to suck in as much actual human usage data as possible to train exclusively better models.

- ## [China just passed the US in open model downloads for the first time : r/LocalLLaMA _202511](https://www.reddit.com/r/LocalLLaMA/comments/1p7alka/china_just_passed_the_us_in_open_model_downloads/)
- This analysis includes all models on HuggingFace, not just LLMs. The most downloaded models (by far) are smaller stuff like embedding models, classifiers, VAD, etc., and small base models like BERT and GPT-2. The most popular properly large instruction-tuned LLM is Qwen2.5-VL-3B-Instruct in 24th place.
  - I suspect a lot of downloads are coming from poorly configured CI/CD pipelines and stuff, rather than individual users

- I'm surprised this hasn't happened earlier, the only good open weight models from the US in the past like 6 months has been Gpt-oss.

- How tf Germany is third place?
  - They have Black Forest Labs
  - stable diffusion guys (now bfl aka flux) are from germany
- Sentence Transformers (SBERT) is originally German. Gets an ungodly number of downloads, and because the models are small people just grab it directly from HF instead of running a local mirror.
  - (Also LAION (CLAP, some popular CLIP-ViT models) and Stable Diffusion/Black Forest Labs (FLUX), though I don't think those get nearly as many downloads.)

- Chinese users predominantly go to modelscope

- ## 💰 [How are Chinese AI models claiming such low training costs? Did some research : r/LocalLLaMA _202511](https://www.reddit.com/r/LocalLLaMA/comments/1p6cf2p/how_are_chinese_ai_models_claiming_such_low/)
  - deepseek claims $6M training cost. Everyones losing their minds cause ChatGPT-4 cost $40-80M and Gemini Ultra hit $190M.
  - glm-4.6: $8-12M estimated, 357B parameters (thats model size)
  - Kimi K2-0905: $25-35M estimated, 1T parameters total (MoE architecture, only ~32B active at once)
  - MiniMax: $15-20M estimated, Mid-range model, mid-range cost
  - 🧮 Training cost = GPU hours × GPU price + electricity + data costs.
  - 真实的成本数字都应该接近上面的公式
  - deepseeks $6M feels like marketing. You cant rent enough H100s for months and only spend $6M unless youre getting massive subsidies or cutting major corners.
  - glms $8-12M is more realistic. Still cheap compared to Western models but not suspiciously fake-cheap.
  - Kimi at $25-35M shows you CAN build competitive models for less than $100M+ but probably not for $6M.

- One difference could be the accounting methodology. I can for sure guarantee that not every training attempt is successful, and companies spend a fortune of gpu-hours on practice runs training smaller models; and then there might be a rollback or two to earlier checkpoints in the big run. Then imagine one company counting the entire cost, while the other accounts only for the end run, and boom - you got drastically different reported figures while effectively the same amount of spent money.
- In the paper for Deepseek they are actually never claiming 6 million - there saying at an assumed price per GPU hour (can’t remember from the top of my head) the final run would be around 6 million.
  - OpenAI also estimated GPT-OSS final training cost like this too iirc. They just didn't for other models.

- They were very transparent about this, and have stated multiple times that it was just the final training run in that estimate and explicitly did not include prior incremental runs.

- The costs listed are likely just the literal hardware cost for the final training run for the model. Every other aspect of the model training process is ignored.

- metas new ai team are getting 9 figure salaries lol makes it hard to profit when you’re paying people such insane salaries.

- Because they're leveraging Western frontier models. Let's be clear, the Chinese labs aren't doing any hard training. All they're really doing is distilling the hard work done by Western labs.
  - I remember it being reported that Western frontier models trained on copyrighted data (even pirated material).

- [Are Chinese AI models really that cheap to train? Did some research. : r/LLMDevs](https://www.reddit.com/r/LLMDevs/comments/1p77x5k/are_chinese_ai_models_really_that_cheap_to_train/)
  - It’s a combo of all those things, especially lying, plus they used a ton of distillation techniques - i.e. they trained a ton on the output of ChatGPT and other established models. 

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
