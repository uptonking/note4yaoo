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

- ## [Am I the only one who feels that, with all the AI boom, everyone is basically doing the same thing? : r/LocalLLaMA _202601](https://www.reddit.com/r/LocalLLaMA/comments/1qk8zj1/am_i_the_only_one_who_feels_that_with_all_the_ai/)
- The AI was trained to regress to the mean and now everything is built by AI so everything now is gonna regress to the mean. You and I and everyone.

- A bunch of amateurs ( or just lazy programmers ) just got their hands on a new toy and they're going down the dunning-kruger curve and they think their prototype is a finished product.

- I find that AIs best use case for me personally is the role of a teacher or an advisor. So damn handy to be able to bounce dumb questions off it while you’re learning something new. Contextual awareness is fantastic for my learning style.

- ## The best way to learn in the new AI era is to use open source projects as references and ask Codex or Claude to re-implement them, 
- https://x.com/LiMzba/status/2013096172752392584
  - it will let you to learn much more deeply and thoroughly than simply reading secondhand knowledge from elsewhere.

- ## 为什么 AGI 必然会私有化部署？
- https://x.com/naki2012/status/2003081645067550888
  - 在今天的讨论中，很多人还在纠结一个问题： AGI 会不会有泡沫？会不会被高估？会不会最终只是云端的一个高级服务？
  - 但如果把视角从“产品”和“商业模式”移开，真正的问题其实是：当智能具备长期记忆、连续人格与自我修正能力时，它还可能是“公共云服务”吗？答案是否定的。不是因为技术不允许，而是因为结构不允许。
  - 一、先说结论：AGI 一旦成立，就必然走向私有化部署
  - 这里的“私有化”，不是指“每个人都买得起超级算力”，而是指一件更关键的事： AGI 的核心节点——记忆与记忆连接机制——必须由个人或极小主体持有。 能力可以外包， 计算可以租用， 但记忆与人格生成逻辑，无法托管。 这是 AGI 与此前所有软件系统的本质分水岭。
  - 二、云端智能为什么天然不可能成为“个人 AGI”
  - 目前所有云端 AI，本质上都具备三个结构特征： 1. 会话式存在： 每一次调用都是“临时生成”，不存在真正的长期连续状态。 2. 记忆不可控： 即便存在“长期记忆”，其存取逻辑、优先级与删除权，始终不在用户手中。 3. 目标不一致： 云端系统的第一责任对象，永远是平台、合规、规模与风险控制，而不是个体的认知连续性。
  - 云端 AI 可以很聪明， 但它永远只能是“助手”，而不是“共生体”。 AGI 一旦具备人格连续性，这种结构就会直接失效。
  - 三、真正敏感的不是“数据”，而是“记忆之间的连接权”
  - 多讨论把焦点放在“隐私数据”“信息安全”上，其实这只是表层。真正不可外包的，是：•哪些记忆会被激活•激活顺序如何变化•冲突记忆如何被调和•哪些经验被强化、哪些被遗忘•错误如何被标记为“羞耻”“警惕”或“教训”
  - 这些并不是数据问题，而是：人格生成函数的问题。
  - 一旦这个函数不在你手里，你面对的就不是“你的 AGI”，而是一个持续解释你、塑造你、却不属于你的系统。 这在结构上是不可接受的。
  - 四、为什么“主脑”必须是本地、私有、持续存在的
  - •物理与主权上都属于个人
  - 五、这不是技术理想主义，而是历史规律的重演
  - 回看历史，每一次关键能力都会经历同样的路径：
  - •计算：从大型机 → PC → 个人设备
  - •存储：从中心服务器 → 本地硬盘 → 私有 NAS
  - •通信：从国家系统 → 运营商 → 个人终端
  - 凡是与“自我连续性”强相关的能力，最终都会下沉到个体。
  - AGI 如果长期只存在于云端，那它注定只是“高级自动化”，而不会成为“个体智能延展”。
  - 六、真正的分界线，其实已经出现了
  - 未来人与 AI 的差异，不在于“用不用 AI”，而在于： •有些人使用的是随时可被替换、被升级、被重置的智能服务 •有些人拥有的是一个长期存在、与自身记忆闭环绑定的智能核心
  - 前者是用户，后者是共生者。这条分界线一旦形成，将比“是否联网”“是否付费”更深刻。
  - 七、结语：AGI 私有化，不是选择，而是必然
  - 记忆主权不可外包，人格生成不可托管。
  - 所以，AGI 的未来形态，不是“更大的云”， 而是： 私有主脑 × 外部能力 × 协作式智能网络。

- 不是，而是。我现在看到这个，第一反应就是这段话是AI生成的，或者至少是人和AI聊出来的内容。

- ## 💡 下午给人做了一个小小的展示。一个Chatbot，其实也就三四百字的提示词，定义了七八个工具。
- https://x.com/wwwgoubuli/status/2001256235296022575
  - 演示的时候，我让对面放开尝试，也提前声明了目前还是Demo阶段，会有些问题。但对方仍然被我这个演示中体现的自主寻找工具解决问题的行为震惊了。
  - 以为我定义了一个很复杂的工作流，我说没有工作流，其实就只有一层。
  - 对方百思不得其解。所以说，认知差肯定是真实存在的。
  - 这是一个垂直领域的Agent。原先客户的问题是，在他们之前所做的AI的尝试中，有一部分已经发挥得很不错了。但是当有的时候不得不处理超长的数据的时候，丢给LLM总是有各种错误出现。
  - 我找他们的研发问过，提取了几个在使用AI之前的，他们处理的工具。然后将这些工具的描述、作用、限定范围等交给了LLM， 并告诉模型不要自己试图解决问题，而是要用工具解决问题。 没了

- 事实上很多公司所做的agent或者chatbot连prompt的上限都没有达到，就开始考虑搞sft，搞RLHF，一个小小的需求为了所谓的优化指标搞的臃肿不堪

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

- ## [Your thoughts on "thinking" LLMs? : r/ollama _202602](https://www.reddit.com/r/ollama/comments/1qv1yey/your_thoughts_on_thinking_llms/)
  - almost all of the ollama-ready models released in recent months have been "thinking" or "chain of thought" or "reasoning" models -- you know, the ones that force you to watch the model's simulated thought process before it generates a final answer.

- thinking models are created because they work. RL is used during post-training to train it to think in a way that increases performance.

- It’s good for long prompts where you’re asking the LLM to complete multiple tasks. The thinking tokens allow the model to work out the intricacies of what you are asking. Simple prompts like “hello” and “summarize this:” isnt where these models excel. If the use cases correct, it’s great!

- The smaller models thinking process does work for certain things, like solving puzzles, but it's generally much flimsier than a SotA model's thoughts.

- There’s a huge difference between my qwen3 30b thinking vs non thinking models. It’s the difference between right and wrong answers.

- It's not fake, thinking tokens were created because in a lot of scenarios they help steering the model for a better answer without polluting the contex.

- ## [Files For AI Agents: Context, Search, Skills Guide | LlamaIndex _202601](https://www.llamaindex.ai/blog/files-are-all-you-need)
- 
- 
- 

- ## [[RELEASE] ARC Protocol v2.1: The Parallel Engine. Zero-Hallucination Engineering is here. : r/GoogleAntigravityIDE](https://www.reddit.com/r/GoogleAntigravityIDE/comments/1qmjrjo/release_arc_protocol_v21_the_parallel_engine/)
  - https://github.com/AshishOP/arc-protocol /MIT/python
  - ARC Protocol v2.1 (Analyze. Run. Confirm.) is the complete rebuild. It’s no longer just a workflow; it's a Parallel Engineering Engine that turns your AI into an autonomous fleet.
  - True Parallelism: Spawn specialized subagents (Alpha-Researcher, Beta-Coder, Gamma-Auditor) via the MCP Bridge. While you architect, they build.
  - Premium TUI Dashboard: A high-fidelity mission control to watch your fleet's heartbeat in real-time.
  - IDE Auto-Linker: A new script to automatically link the ARC bridge to Cursor, Windsurf, ClaudeCode, and VS Code.

- This is a vibe coded mess Like even the instructions to install it and set it up are vibe coded and not how the project actually works

- ## the most capable coding agents don't have hundreds of specialized tools
- https://x.com/vimota/status/2015823598577975453
  - they have three: read a file, write a file, run code
  - filesystem plus code execution is why Cursor and Claude Code can work autonomously for hours. 
  - But it only works when the agent runs on your machine, where you control security through approvals.
  - if you try to build it into products, you need a sandbox VM to avoid getting your files rm -rf'd
  - localsandbox is our exploration into an alternative that uses user-land isolation via a virtual filesystem, a bash interpreter, and WASM-sandboxed python execution.

- ## [I reverse-engineered Microsoft AutoGen’s reasoning loop and cut agent latency by 85% (13.4s → 1.6s). Here is the architecture. : r/LocalLLaMA _202601](https://www.reddit.com/r/LocalLLaMA/comments/1qn2n4p/i_reverseengineered_microsoft_autogens_reasoning/)
  - I’ve been building voice agents using AutoGen, and the "awkward silence" during the Chain-of-Thought (CoT) phase was killing the UX. 
  - The standard sequential loop (Think → Wait → Execute Tool → Wait → Speak) just doesn't work for real-time interaction.
  - Instead of waiting for a v2 update, I dug into the ConversableAgent class and implemented a module for Speculative Reasoning Execution (SRE).
  - Standard Speculative Decoding predicts tokens. I adapted this to predict Tool Calls.

- ## 📌 [Unrolling the Codex agent loop | OpenAI _202601](https://openai.com/index/unrolling-the-codex-agent-loop/)

- ## 🧩 这个 Ralph Loop 现在这么流行吗？我今天才仔细去了解一下，原来是一种方法论啊：用一个 bash 无限循环反复喂 prompt 给 AI 编码工具，直到任务完成。
- https://x.com/vikingmute/status/2013607905040400520
  - * 每次迭代 AI 都从干净上下文开始（避免上下文污染）。
  - * 通过 git 历史、progress.txt、PRD.json 等文件持久化状态和学习（比如上轮学到的坑、下轮自动避开）。
  - * 强调小步迭代：大任务拆成 5-10 分钟可完成的子任务，每次循环只处理一个。
  - * 程序员只监督了：写好 PRD 和 prompt 后，睡一觉让 Ralph 通宵干活，早上 review PR。

- 我选择用 planning-with-files，除了不能自动循环，同样能持久化状态和经验，自己把关当前态来决定是否重拾，关键还是SOTA模型自己真得烧不起token

- 我试过，有两回都是卡在那不停地写文档，我没有任何命令让他写，他就是写个不停。宁愿去用sdd。

- ## The Bitter Lesson of Agent Frameworks
- https://x.com/gregpr07/status/2012052139384979773
  - All the value is in the RL'd model, not your 10, 000 lines of abstractions.
  - An agent is just a for-loop of messages. The only state an agent should have is: keep going until the model stops calling tools. You don't need an agent framework. You don't need anything else. It's just a for-loop of tool calls.
  - Our first Browser Use agents had thousands of lines of abstractions. They worked - until we tried to change anything. Every experiment fought the framework. The agents weren't failing because the model was dumb. They were failing because we were.

- I almost completely agree with this except you don't even need tool calls. Just executable code fences.

- No, it's more than just loop. 
  - 1) Sessions are stateless. Smart framework will keep permanent memory without having to tell agents 101th time the same stuff.
  - 2) They try every possible trick to save tokens, to save costs for those who use API to access tokens
  - 3) Smart multiagent collaboration. Models are not equal, some are better in one specific area than others. That's why having two or three specialized agents working as a team will always beat single agent trying to comp thru massive codebases

- ## [Speculative Decoding: Turning Memory-Bound Inference into Compute-Bound Verification (Step-by-Step) : r/LocalLLaMA _202601](https://www.reddit.com/r/LocalLLaMA/comments/1qg2592/speculative_decoding_turning_memorybound/)
  - Most of us assume LLM inference is slow because "matrix multiplication is hard." That’s actually false.
  - For a batch size of 1 (which is standard for local inference/chat), your GPU is almost entirely Memory Bandwidth Bound. The bottleneck isn't doing the math; it's moving the 70GB+ of weights from VRAM to the compute units. The Arithmetic Logic Units (ALUs) are spending most of their time idle, waiting for data.
  - Speculative Decoding exploits this idle time to give us a "free lunch"—2x-3x speedups with mathematically identical outputs.
  - This converts a memory-bound operation (waiting for weights) into a compute-bound operation (doing more math on loaded weights), maximizing hardware utilization without retraining.

- Welcome to 2 or so years ago (which is eons in LLM). Speculative decoding using draft models looked great back then, but the problem is the limited practical usage. In order to get good speed ups there needs to be a huge difference between the draft model size and the target model size like 1B to 70B. Gains with smaller differences are smaller. In addition the models of that size are MoE now so speculative decoding is not needed. The last setup it did bring something to the table was probably Qwen2.5 where you could use the 0.5B model as draft for the 32B for example. I find limited usage for it nowadays, but it may just be my usage and there may be scenarios where people still use and like it.

- Recently I was reading Nvidia's Nemotron 3 paper. They have used speculative Decoding idea in their latest models. 
  - Except MTP is not the same speculative decoding you wrote about. It is also still only coming with the Super and Ultra models which have not been released yet.

- Works fine with models with a MTP layer

- Sad that vLLM does not fully support smaller drafter models (atleast last I checked) because my gemma-3-270m is screaming to boost my gemma-3-27B token generation speeds
  - Works with llama.cpp though so that's pretty good :). vLLM is next level though. Wish it supported that

- ## 🏘️ [Alternative to Transformer architecture LLMs : r/LocalLLaMA _202509](https://www.reddit.com/r/LocalLLaMA/comments/1nk58yc/alternative_to_transformer_architecture_llms/)
  - I wanted to ask if there are any other possible LLM architectures instead of this transformer.
- State Space Models (SSMs) are not using standard transformer architecture and they are getting some attention from various research institutes (look for Mamba paper on arxiv).
  - There is also RWKV that (depending on the version) looks more like a standard RNN.
  - Both of them have some advantages and disadvantages compared to transformers. Definitely cool research area

- There is some research towards using diffusion architecture for LLMs. LLaDa is one

- Hybrids are the latest thing, Nemotron Nano is only 8% transformer! Also Qwen3-Next is a hybrid.

- RWKV uses an RNN.

- [GFN v2.5.0: Verified O(1) Memory Inference and 500x Length Extrapolation via Symplectic Geodesic Flows : r/LocalLLaMA](https://www.reddit.com/r/LocalLLaMA/comments/1qgogis/gfn_v250_verified_o1_memory_inference_and_500x/)
  - We present GFN (Geodesic Flow Networks), an architecture that reformulates sequence modeling as particle dynamics on a learned Riemannian manifold. Unlike Transformer-based architectures—which exhibit O(N^2) memory scaling due to the attention mechanism—or standard RNNs that suffer from vanishing gradients, GFN achieves O(1) memory complexity during inference and exhibits infinite-horizon stability through symplectic integration.
  - In our v2.5.0 release, we demonstrate perfect zero-shot generalization on algorithmic tasks with sequences up to 10, 000 tokens while maintaining a strictly bounded memory footprint of ~60MB.

- ## Release the VSC extension design for the local coding model: 
- https://x.com/LiMzba/status/2011106168136220739
  - Reasons for creating a new one instead of using the existing code harness:
  - Make the requests as sequential as possible to avoid overwhelming the local LLM server.
  - Optimize the tools to accommodate the instability of the local model
  - Remove timeout, so you can run it against your slowest model
  - It's fun to build agents
  - mlx-lm server as a first-class citizen, as I can only use mlx-lm to host models

- ## 📌 [Ratios of Active Parameters to Total Parameters on major MoE models : r/LocalLLaMA _202601](https://www.reddit.com/r/LocalLLaMA/comments/1q401ka/ratios_of_active_parameters_to_total_parameters/)
Model	Total Params	Active Params	% Active
GLM 4.5 Air	106	12	11.3%
GLM 4.6 and 4.7	355	32	9%
GPT OSS 20B	21	3.6	17.1%
GPT OSS 120B	117	5.1	4.4%
Qwen3 30B A3B	30	3	10%
Qwen3 Next 80B A3B	80	3	3.8%
Qwen3 235B A22B	235	22	9.4%
Deepseek 3.2	685	37	5.4%
MiniMax M2.1	230	10	4.3%
Kimi K2	1000	32	3.2%

- having more knowledge memorized, means the model has access to a broader library of reasoning strategies, even if it's not as effective at applying them as a higher active parameter count model. 
  - Pretty much every task will exist on the spectrum of "reasoning" versus "memorization" (even creative writing), and almost everything will be some combination of them. The more it is one end, the closer it'll perform to that parameter count. Ie: a pure reasoning task might depend basically only on active parameter count, whereas a pure memorization task scales basically 1:1 with total parameters.
  - In the end, far more important than the architecture is really the data, and training compute. With good data and compute, the difference between parameter ratios is pretty small, actually (under a fixed compute budget), while with bad data, it doesn't matter if you have a good architecture, it won't perform well.
  - The part you are maybe not taking into account is the the models with lower active parameter ratios are typically trained on more data, effectively, because on the same compute budget you train more tokens than the "dense equivalent" model, so it's not like you would magically have a model better for your usecase just because it's dense.
  - You have to evaluate every individual model, not just from its architecture, but in how it performs for you.

- In my case, granite-4.0-h-small (32B-A9B) is slow(10 t/s) on my 8GB VRAM(Tried to use Q4) due to A9B. Similar size Qwen3-30B-A3B is decent speed(30 t/s) for Q4. GPT-OSS-20B is good with 40 t/s. 

- One interesting thing could be comparing this ratio against dense models having similar benchmarks, across different time periods and empirically find out the formula we used to have to map the dense model size equivalent to MOE.

- ## Context Engineering 面试题：在 XX 业务场景下面，read_file, write_file 如何设计？ 面试中遇到这题我估计临场发挥不会太好
- https://x.com/dotey/status/2007524872629387382
  - 首先得分析场景，然后看场景需要的上下文，还要看怎么管理上下文
- 我会说在新的 ai时代，我会将这个问题问 opus 4.5，让他给几个解决方案思路，每个思路列出优缺点，之后让我来判断
  - 不过我觉得这思路在真实工作场景还可以, 面试当然不行，面试要达到造火箭的水平

- 我猜要考察的是应聘者对于一个tool的设计会考虑哪些事情，我粗略想了下应该有：1. 参数顺序如何控制才能防止参数顺序带来的UI渲染的奇怪问题 ； 2.  除了功能字段比如path, content字段之外是否需要加入一些description字段提升UI体验； 3. 除了tool功能本身之外，可以有哪些tool call 异常error增强和牵引设计 4. 大文件读写如何处理，比如是否要分层加载或流式读取  5. 不同场景下的read_file, write_file考虑的点是否不一样。 6. 如果要做checkpoint，是否要放到tool里还是hooks里。 7. 不同环境如何设计，比如远程沙箱环境，本地环境等 8. 某些场景是否需要做业务旁路逻辑

- 不同业务状态下，同样是“文件操作”，语义不同。能把这些场景、业务状态说出来，解释对应的语义以及对应的技术诉求、约束，应该是好的回答。

- 这个问题还有个加倍，就是远程虚拟环境的read_file、write_file如何设计，我被这个折磨好久，最后放弃了，和本地差不多得了

- ## 随手写写我当前认识的 coding agent orchestrator /多agent编排器。
- https://x.com/LotusDecoder/status/2007292223864353071
  - 预感这个会是2026开年最火的概念。类似于2024的cursor，2025年的claude code。
  - 首先这是AI agent性能提升发展后的必然趋势，从chatbot查查手册，到cursor改文件，再到claude code cli式一次成型整个项目，到了现在单个agent已经成熟之后，自然开始进入多agent分工协作，然后多个agent如何沟通、运筹、管理，这就很需要新的范式了。
  - 最基础的是claude code里内部语法启动subagent，用bash命令或文档来管理各自的任务目标、日志、成果。
  - vaguel其次，比较友好的是 opencode 的 oh my opencode，有一个初始的默认编排器配置 西西弗斯系统，一次性缝合Opus-4.5 Gemini-3-pro Gpt-5.2，各自干各自擅长。设计了查文档、前端、后端、总控台等多个角色，把model依次接入进去，由总控台来自行分配任务。
  - 还有声音也比较大的 conductor，这个还没用过。 优点是可视化界面管理多个 agent，每个 agent 在独立 git worktree 中工作。还有支持codex。
  - 现在最激进的元旦刚发布的 gas town，作者说展示给anthropic公司内部看的时候，吓到他们了。这个项目直接把所有的cli 形式agent一揽子包了进来做编排，主流的 claude code 、codex之外 Gemini CLI 、amp 等等全部囊括了进来。
  - orchestrator的大发展将会是AI性能提升后，走到下一步的必然，并发并行多个多种agent干活，再AI测试合并，完成一个大型项目，这不是一个未来很遥远的事情，甚至很快又会成为一种标准范式吧。当然，这对人的要求更高了，需要很系统的软件工程能力，对钱包的要求也变高了，以前一个agent，orchestrator是一群agent烧token

- conductor 值得一试，我这两天在用的，多 workspace/分支并行。 Claudecode/codex 订阅可以直接用

- ## [Local model registry to solve duplicate GGUFs across apps? : r/LocalLLM _202512](https://www.reddit.com/r/LocalLLM/comments/1pygyhi/local_model_registry_to_solve_duplicate_ggufs/)
  - I'm running into storage issues with multiple local LLM apps. I downloaded Olmo3-7B through Ollama, then wanted to try Jan.ai's UI and had to download the same 4GB model again. Now multiply this across Dayflow, Monologue, Whispering, and whatever other local AI tools I'm testing.
  - Each app manages its own model directory. No sharing between them. So you end up with duplicate GGUFs eating disk space.
  - Feels like this should be solvable with a shared model registry - something like how package managers work. Download the model once, apps reference it from a common location. Would need buy-in from Ollama, LMStudio, Jan, LibreChat, etc. to adopt a standard, but seems doable if framed as an open spec.
  - I'm guessing the OS vendors will eventually bake something like this in, but that's years away. Could a community-driven library work in the meantime? Or does something like this already exist and I'm just not aware of it?

- They're just files. You can remove duplicates yourself and replace them with symlinks to whichever copy you choose to make the "primary".

- Jan has Import option(to use downloaded GGUF files from any folder).
  - Koboldcpp also does this just with browse GGUF option.
  - For Oobabooga, I used symlinks option.
- I found that buried in the Jan.ai UI under Settings / Model Providers / Llama.cpp / import.

- 
- 
- 
- 
- 
- 
- 
- 

- ## 🤔 [How do you make agents deterministic? : r/AI_Agents](https://www.reddit.com/r/AI_Agents/comments/1pv2gfk/how_do_you_make_agents_deterministic/)
  - I have been talking to many business and a common concern has been lack of reliability of ai agents.
- In my experience, determinism does not come from the model, it comes from the system design around it. You cannot prompt an LLM into behaving like a rule engine. Business rules need to live in code or configuration, not in free text prompts. The agent’s job is to interpret context and propose actions, not decide what is allowed.
  - What works well is separating concerns very clearly. Rules, policies, and exceptions are encoded as deterministic logic or tables.
  - For reliability, many teams also constrain where and how agents can act. When agents need to interact with real systems, running them in predictable environments like hyperbrowser helps keep execution consistent and auditable, which is critical in regulated workflows.

- Typically variance results from ambiguous instructions or situations. Use this method to identify specific points in your conversation and see how you can improve the context.
  - Use something like Langfuse to run experiments and trace execution
  - Run the same experiment multiple times.
  - Use python to scrape the data and compare outputs across runs
  - Compute deltas in your outputs
  - Check if specific inputs prove to have more variance in output
- Correct. In fact you should be focusing more on the sad paths because those are the edge cases you need to test.

- Use regular workflow automation tools instead of agents. Or make your tools highly deterministic and have obvious tool selection criteria.

- 90% of it is prompt engineering and a feedback loop. You have another AI at the end that is fed the last AIs user, systems messages and outputs and feeback from client "like i expected it to do this", this will give you a feedback loop on what went wrong in prompt.

- I have been trying to achieve this with my own framework. Its possible. Not in the sense of 1:1 deterministic responses but the core logic of agent output can be deterministic. People have written some methods which I mostly followed. Plus my framework has agent driven, smart retries, which enforces responds to be constrained. As a result my framework, I can deliver basic crud applications with different domain with exact same gaps and similar bugs. They all look very identical. After I get back from holiday I will announce my work. Looking forward to hear your feedbacks.

- ## 🏘️🧩 [Agents | OpenCode](https://opencode.ai/docs/agents/)
- Agents are specialized AI assistants that can be configured for specific tasks and workflows. 
- There are two types of agents in OpenCode; primary agents and subagents.
- Primary agents are the main assistants you interact with directly. 
  - These agents handle your main conversation and can access all configured tools.
  - OpenCode comes with two built-in primary agents, Build and Plan. 
  - Build is the default primary agent with all tools enabled. This is the standard agent for development work where you need full access to file operations and system commands.
  - Plan is a restricted agent designed for planning and analysis. We use a permission system to give you more control and prevent unintended changes. This agent is useful when you want the LLM to analyze code, suggest changes, or create plans without making any actual modifications to your codebase.
- Subagents are specialized assistants that primary agents can invoke for specific tasks. 
  - OpenCode comes with two built-in subagents, General and Explore. 
  - General is a general-purpose agent for researching complex questions, searching for code, and executing multi-step tasks. Use when searching for keywords or files and you’re not confident you’ll find the right match in the first few tries.
  - Explore is a fast agent specialized for exploring codebases. Use this when you need to quickly find files by patterns, search code for keywords, or answer questions about the codebase.

- ## 为什么现在 AI 写前端一下子这么强了，小米的 MiMo 论文的这段介绍了他们如何训练模型写前端的，关键是这句：
- https://x.com/linexjlin/status/2002383307414409514
  - 我们的基于视觉的验证器通过对录制的视频片段执行情况进行评分，综合评估视觉质量、功能准确性和可执行性，从而确保奖励机制能够同时兼顾外观表现与行为效果。
  - 原理上就是模型根据 prompt 写好代码后再用 Playwright 操作录制成视频，然后，交给一个视觉验证器（应该是一个专门训练的视频理解模型） 进行打分，以提供奖励信号。

- 还在捣鼓XXPO的我觉得自己望尘莫及了
  - 重复性工作交接 AI  是对的，人多出的精力可以用在审美把关上。

- 应该是训了一个很小的视觉判别模型，前期加了很多人工评判的数据，还是挺扎实的

- 所以现在清楚了，其实还得依靠人为创建很多训练数据

- 这次经过了多少工程师多少小时的打磨

- ## [Is direct tool use a trap? Would it be better for LLMs to write tool-calling code instead? : r/LocalLLaMA _202512](https://www.reddit.com/r/LocalLLaMA/comments/1px089u/is_direct_tool_use_a_trap_would_it_be_better_for/)
- Look into smolagents from HF, it uses something pretty similar to this.

- "better" is defined by what's model was trained on. Code path is definitely more scalable, but also more unsafe. Currently, most models are primarily trained on direct calls mode, so code calling requires taking context space with explanations and represents another failure mode for the model.
  - Source: agents in my company can decide to call their tools via code, it's pretty hard to make them choose it, unless very specifically targeting to do so.

- Scales much better to give the ai access to a virtual folder structure with code for calling different functions. Just dumping everything into context is silly.

- I use each approach. Function calling API’s are my approach pretty much 100% of the time if I am building an agent which is integrating with another system with a contract and the job of the agent is to talk to the other system(s).
  - A sandbox is better for broader use cases where the work is all internal.
  - I often define APIs using tool calls that map to python functions running inside the sandbox which is a mix of the two.
  - My opinion is that it completely depends on the situation 

- if you are going to allow a model to write and run arbitrary code, it is riskier and should be sandboxed in most situations. I think smolagents does have the option to constrain to just the functions you are given it or write and run other things as well. I am not 100 percent sure they can guarantee this.

- Yes, this is true. I've had great success providing a restrictive JS environment and typescript definition files and using this instead of JSON tool calls, especially when executing steps which would otherwise require multiple tool calls. However, it does depend on having a model that has been trained extensively on code.

- ## 💡 [anthropic blog on code execution for agents. 98.7% token reduction sounds promising for local setups : r/LocalLLaMA _202512](https://www.reddit.com/r/LocalLLaMA/comments/1powhy6/anthropic_blog_on_code_execution_for_agents_987/)
  - instead of direct tool calls, model writes code that orchestrates tools
  - basic idea: dont preload all tool definitions. let model explore available tools on demand. data flows through variables not context
  - for local models this could be huge. context limits hit way harder when youre running smaller models
  - the privacy angle is interesting too. sensitive data never enters model context, flows directly between tools
  - cloudflare independently discovered this "code mode" pattern according to the blog
  - main challenge would be sandboxing. running model-generated code locally needs serious isolation
  - tools like cursor and verdent already do basic code generation. this anthropic approach could push that concept way further
  - wondering if anyone has experimented with similar patterns locally

- FYI, this pattern already exists in HFs smolagents, they use model-generated code to execute tools instead of JSON tool calls
  - yep, smolagents is definitely already using this pattern.
- it's up to you how you execute this. The whole approach should depend on strong sandboxing. smolagents can run generated code in a restricted executor, same assumption Anthropic makes in the blog
- The searchable filesystem approach to tool definitions was the most interesting bit for me, very clean way to avoid preloading huge schemas, whether you use code or JSON

- Yes, though in my case I have the model generating a DAG of steps it wants to run instead of arbitrary code, which reduces the sandboxing needed, avoids non-terminating constructs, etc.
  - Token-efficiency is a side-benefit from my perspective. Moving to the plan->execute pattern also makes problems tractable for smaller models, many of which are able to understand instructions and produce "code" of some sort, but which may struggle to pluck details out of even a relatively short context window with the needed accuracy.
- I really like the DAG / plan→execute approach , especially for sandboxing and small models. It feels aligned with the same idea of keeping data and state out of the model context, just with tighter structure. Do you generate the full DAG upfront, or refine it during execution?
  - 2 modes. The model can propose a dag using a planning tool and then the user can discuss/iterate it, or auto mode where it just runs.

- if you are writing the function why call an MCP server? Why not just do what the MCP does?
  - MCP is more easily reusable.
- I'd second that; any reasonably shaped API should work really, but this way you avoid installing any packages and browsing for the API docs. It's a way for the model to discover the API instead of being fed how to use it.

- ## Use Anthropic's tool search to give your agent hundreds of tools without filling its context window.
- https://x.com/aisdk/status/2000886249306120473
- Or you could use http://mcpz.it which came out in Feb this year and was the first tool to actually identify and solve the tooling issues with MCPs 

- Game-changer for multi-tool agents  Tool search + deferLoading = hundreds of tools without context explosion? Claude-Sonnet-4.5 agents just scaled massively—Vercel AI SDK making production agents real. 

- ## 🤔 [How to make LLM output deterministic? : r/LocalLLaMA](https://www.reddit.com/r/LocalLLaMA/comments/1plbe8i/how_to_make_llm_output_deterministic/)
  - I am working on a use case where i need to extract some entities from user query and previous user chat history and generate a structured json response from it. The problem i am facing is sometimes it is able to extract the perfect response and sometimes it fails in few entity extraction for the same input ans same prompt due to the probabilistic nature of LLM. I have already tried setting temperature to 0 and setting a seed value to try having a deterministic output.
  - does setting seed value really work? In my case it seems it didn't improve anything.

- Because of certain GPU optimizations, LLMs are technically random even at temperature = 0 IIRC. llama.cpp has a similar issue. And you can run into something similar in training as well for a given training seed unless you configure some knobs if I'm not misremembering.

- Here's a really good blog post around LLM determinism: https://thinkingmachines.ai/blog/defeating-nondeterminism-in-llm-inference/
  - If you were to host your LLM locally, both vLLM and SGLang have done work on providing deterministic / batch invariant inference

- change your mindset, when you work with llm it is non-deterministic, whatever you do there is still tiny chance that it can't deliver deterministic response. always handling the non-deterministic part is crucial in all llm base application
  - for me personally, try to prompt the model to wrap the anser around xml tag is quite reliable like `<Answer>what ever llm response</Answer>` and going from there

- Literally impossible to make them fully deterministic because input itself affects the inference matrix.

- The problem with using cloud LLM APIs is that your requests will get batched with others which introduces nondeterminism, even with temperature sampling disabled.
  - It’s relatively easy to achieve this if you run a model yourself and set the batch size = 1, however.

- ## [Claude Skills are just .cursorrules, change my mind : r/ClaudeAI](https://www.reddit.com/r/ClaudeAI/comments/1oj109n/claude_skills_are_just_cursorrules_change_my_mind/)
- It's all just prompt really. Basically an LLM only has prompt and output.

- Cursor rules are like CLAUDE.md files. They are loaded into context on every AI interaction. Claude Skills are executable capabilities that can be invoked _when needed_. 
  - Nope, cursorrules have markdown header thingies with a description and can either be auto-loaded, or invoked by the LLM which will only see their descriptions before invoking them.

- They can run packaged scripts when needed.

- The marketplace/plugin system is the big differentiator, imo

- 💡 I think it was presented as revolutionary because it's adaptable for more than just coding. It can execute the scripts and call tools to use for specific purposes. I think the fact that it's accessible to Claude that AI web means that it's accessible to more individuals that may not be using cursor or something else for coding so available for other use cases

- I wish Claude Code could lazy load MCPs as same as skills.

- I'm a Cursor user and I'd love to replicate what I see people getting out of skills.
  - cursor rules are only loaded at the start of a chat. You can have 50 rules, and logic for which ones to load so that cursor only ever loads a few per chat, but it's still always at the start of a chat.
  - My understanding of Claude Skills is that they can be accessed more-or-less at any time. If I want to e.g. file a bug midway through a chat, if the "File a bug" rule wasn't included at the start, Cursor doesn't seem to re-read its Cursor rules and pick up the newly-needed ones, whereas it sounds like Claude Code will.

- ## [如何看Anthropic最新发布的Claude Skills？会替代MCP吗？ - 知乎 _202510](https://www.zhihu.com/question/1962512846630941008)
- 说个暴论，AI Agent想要落地，需要的只有强大的模型基座，什么Skill、MCP、... 都只是添头，通过代码很容易实现。
- Skill就是一个标准化的文件夹，用来打包Agent完成特定任务所需的知识和工具。
  - 可以把它理解成给模型的说明书或标准作业程序（SOP，或者之前比较火的概念：SPEC的增强版）。
  - Anthropic这次不仅发布了概念，还直接开源了一个GitHub仓库, 里面包含了所有20个左右的官方Skill的源码示例
- 一个Skill文件夹通常包含这几部分：
  - SKILL.md：核心文件，必须存在。里面用YAML写元数据（名字、描述），用Markdown写详细的指令，告诉Claude在什么情况下、以及如何使用这个Skill。
  - scripts/：存放可执行的Python、Shell脚本。比如PDF处理Skill里，就有fill_fillable_fields.py这种确定性极强的代码。
  - references/：存放参考文档。比如API文档、数据库Schema、公司政策等，这些是给Claude看的知识库。
  - assets/：存放资源文件。比如PPT模板、公司Logo、React项目脚手架等，这些是Claude在执行任务时直接使用的文件，而不是阅读的
- 一个Skill = 任务说明书 SKILL.md + 工具代码 (scripts) + 专业知识 (references) + 素材资源 (assets)。
  - 它把完成一个特定任务所需的一切都打包好了，本质上就是一种代码和资源的组织方式，一种约定优于配置的理念。
- 💡 Claude Skills设计的精髓，也是它和简单RAG/MCP/FunctionCalling的最大区别。它就是一套聪明的，为了节省上下文窗口而设计的分层加载策略。 
  - 第一层：元数据（Name + Description）。这部分信息非常简短，会常驻在Claude的脑海里。当用户提出一个任务时，Claude会快速扫描所有可用Skill的描述，判断哪个可能相关。这是第一道筛选，成本极低。
  - 第二层：SKILL.md。当Claude认为某个Skill相关时，它才会去加载SKILL.md里的详细指令。这部分内容告诉Claude完成任务的具体步骤、应该遵循的规则、以及如何使用文件夹里的其他资源。这步的上下文消耗中等。
  - 第三层：脚本和参考文档。只有当SKILL.md里的指令明确要求，或者Claude在执行中判断需要时，它才会去读取scripts/里的代码或references/里的文档。这步的上下文消耗是按需的，避免了一次性把所有东西都塞进去。
- 这个机制的好处显而易见，极大地节省了宝贵的上下文窗口。它先凭经验判断用哪个SOP，然后翻开SOP照着做，遇到具体问题再查阅附录或工具手册。这套逻辑，我们用代码当然也能实现，但Skills把它标准化了。

- 它和MCP是什么关系，会替代吗？直接回答，完全不是一回事，不会替代，甚至是互补的。
  - MCP是一种通信协议。它定义了Agent（客户端）如何与一个暴露了工具的服务（服务端）进行标准化的交流。它解决的是Agent与外部工具如何对话的问题。
  - Claude Skills是一种能力封装格式。它定义了Agent自身应该具备哪些知识、工作流和内部工具。它解决的是Agent如何思考和行动的问题。
  - Skill里的知识可以指导Agent如何更有效地去使用一个遵循MCP协议的工具。一个Agent完全可以加载一个Skill，然后根据Skill里的指令，去调用一个远程的MCP服务器

- 最大的价值是：Anthropic把他们在生产环境中打磨出的一套Agent能力管理的设计模式开源了。我们完全可以把这个模式借鉴过来，用在自己的Agent体系里，不管你用的是Qwen、Deepseek，还是别的模型
  - 当你的Agent能力越来越多时，怎么管理？一个几千行的System Prompt？一个包含几十个工具函数的大杂烩文件？这些都很难维护。
  - 而Skills提供了一种解耦的、模块化的方案。你团队里的Agent不再是依赖一个巨大的、难以维护的system_prompt.txt，而是一个由几十个标准化的Skill文件夹组成的能力库，每个Skill都可以独立版本控制、测试和迭代。

- 在字节实习做通用Agent研发的时候，Agent需要支持几十种不同 工具/接口/平台 来完成五花八门的任务，对此，同事们对知识的管理提出了一个knowledge范式：
  - 每个knowledge定义好title, description, used when（在什么任务/工具/平台出现时，使用该knowledge）。这些作为metadata，每个knowledge的metadata也就三行字左右。knowledge的正文是一个markdown，会包含SOP、Dos、Don'ts、甚至简单的脚本。
  - Agent启动一次任务时，先根据prompt让LLM根据提供的metadata主动召回其认为用得上的knowledge，再通过工程手段把完整的md拼进prompt里，支持完成后续任务。
  - 看完Anthropic提出的Claude Skills，感叹当时同事理念的先进，也感叹行业霸主的生态话语权——如果是豆包或者seed提出这样一个范式，肯定得不到如此巨大的关注和跟进。
  - 同时也承认，Claude Skills的定义内涵和规范比当时我们团队提出的knowledge更加全面和可循，只不过本质上没有太多进步，仍然是context engineering的一种。要想让模型充分发挥好Skills的能力，最终还是要依赖更好的模型，更强的推理。

- 这种范式是开发AGENT的常规方式，没啥先进的。工程量大一点的AGENT都会构建自己的知识库范式，核心就是结构化自己的内容

- 写 function call 的时候就会用到呀，不同的是只考虑到代码层面的封装

- 从skill的文档描述来看 它就是单纯地把描述丢给大模型 至于大模型实际会不会follow 那就完全看心情了 从这一点来说 skill方案在性能与确定性这块必然是比真正的tools差不少的
  - 总体来说 skill基本可以算是prompt之上的初级语法糖 虽然比较鸡肋 但对用户而言 总归是能解决一些场景下的问题的 起码有了一套指导大模型使用新工具的临时解决方案了

- ## [OpenAI 谷歌联手推出 AGENTS.md，能否成为编程 Agent 的「官方说明书」？ - 知乎 _202508](https://zhuanlan.zhihu.com/p/1941669020068709122)
- 争论一：AGENTS.md vs. CONTRIBUTING.md
  - README.md 或 CONTRIBUTING.md 不够用吗？
  - 这整件事本该在 CONTRIBUTING.md 里解决。AGENTS.md 里的内容，和人类贡献者想了解的东西没什么两样。
  - 给 Agent 的文档必须 高度精炼，因为过多的内容会消耗宝贵的 API token，增加成本，甚至降低输出质量。

- 争论二：文件 vs. 文件夹，单体 vs. 结构化
  - 有经验的开发者提出，对于大型复杂项目，一个巨大的 Markdown 文件很快会变得难以维护。
  - 许多开发者建议采用更有组织的文件夹结构，例如一个隐藏的 .agents 目录

- 争论三：根目录污染问题

- 争论四：继承还是覆盖？
  - AGENTS.md 支持在子目录中嵌套，但其规则是 「最近文件优先」。

- [告别混乱，用 AGENTS.md 统一你的 AI 开发工具规则 - 知乎](https://zhuanlan.zhihu.com/p/1951785160124109343)
  - AGENTS.md 只是一个单独的文件，没法像 Cursor 的 `.cursor/rules` 一样支持非常多的独立的规则。
  - 我的建议是，你可以和团队商定一个存放各类规则的公共目录，比如 `.ai/rules/`。 然后你可以在 AGENTS.md 中补充 rules 信息内容。

- [Switching to AGENTS.md : r/cursor](https://www.reddit.com/r/cursor/comments/1nqwz02/switching_to_agentsmd/)
  - Don't dump all rules into this file. You can link to other rules from this file. Agents should be able to reason about it and read the right documentation.

- [Claude Code and Claude.md: Should you spread your product doumentation and plans and agent instructions over multiple files? : r/ClaudeAI](https://www.reddit.com/r/ClaudeAI/comments/1lr1g0d/claude_code_and_claudemd_should_you_spread_your/)
  - Yes, progressively split the knowledge across multiple md files.
  - Rule of thumb that works for me. Claude.md is for nouns. Slash commands are for verbs. Meaning Claude.md is about where and what things are, and then slash commands are about how to do the thing.

## 🌰 [How to write a great agents.md: Lessons from over 2, 500 repositories - The GitHub Blog _202511](https://github.blog/ai-and-ml/github-copilot/how-to-write-a-great-agents-md-lessons-from-over-2500-repositories/)

- We recently released a new GitHub Copilot feature: custom agents defined in agents.md files. Instead of one general assistant, you can now build a team of specialists: a @docs-agent for technical writing, a @test-agent for quality assurance, and a @security-agent for security analysis

- What works in practice: Lessons from 2, 500+ repos
  - Put commands early: Put relevant executable commands in an early section: npm test, npm run build, pytest -v. Include flags and options, not just tool names.
  - Code examples over explanations: One real code snippet showing your style beats three paragraphs describing it. 
  - Set clear boundaries: Tell AI what it should never touch (e.g., secrets, vendor directories, production configs, or specific folders). “Never commit secrets” was the most common helpful constraint.
  - Be specific about your stack: Say “React 18 with TypeScript, Vite, and Tailwind CSS” not “React project.” Include versions and key dependencies.
  - Cover six core areas: Hitting these areas puts you in the top tier: commands, testing, project structure, code style, git workflow, and boundaries. 

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
- resources
  - [Use Cases | Claude](https://claude.com/resources/use-cases)

- ## 

- ## 

- ## [Getting OpenClaw to work with Qwen3:14b including tool calling and MCP support : r/LocalLLaMA](https://www.reddit.com/r/LocalLLaMA/comments/1qrywko/getting_openclaw_to_work_with_qwen314b_including/)
  - I got local tool calling working on Qwen3:14b with ~40 tools, accessible through WhatsApp. 
  - OpenClaw is an AI assistant framework that supports multiple messaging channels. It talks to its LLM backend via an OpenAI-compatible API (/v1/chat/completions).
  - Why a bridge instead of adding tools directly in OpenClaw? OpenClaw supports custom tools natively. You could write each MCP tool as an OpenClaw extension. But I have multiple apps that need the same tools: OpenClaw for WhatsApp, Engram (my personal knowledge system), Jan.ai, etc. Writing each tool as a per-app extension means duplicating everything. With the bridge as a shared MCP layer, you configure your tools once, and any OpenAI-compatible client gets them. Just point it at :11435 instead of :11434.
  - I tested both qwen3:8b and qwen3:14b on an M4-series Mac Studio with 64GB of RAM
  - The 8b model is 3-5x faster but basically treats every message as a new conversation when there are 40 tool schemas in the context. OpenClaw sends the full message history (confirmed via logging: messages=16), so the problem isn't missing context. The model just can't follow it alongside those massive tool definitions.
  - Verdict(裁定，判决): qwen3:14b. Quality over speed for now.
  - The patch code is available as a GitHub Gist. Running this as a daily driver via WhatsApp and it's surprisingly capable for a 14b model.

- I am having looping tool call issues with glm 4.7 flash 8bit running on lm studio with mlx. I just ask open claw ‘use browser to open google.com’ and it goes into a loop. I have tried all sampling combinations but nothing works. Please help

- ## 🤔 [Why we went desktop and local-first for agents 6 months ago : r/LocalLLaMA _202601](https://www.reddit.com/r/LocalLLaMA/comments/1qr5v9d/why_we_went_desktop_and_localfirst_for_agents_6/)
  - We’ve been thinking a lot about first principles when building agent project, and one conclusion we keep coming back to is this: The first thing you should optimize for is the agent’s capability ceiling.
  - From that perspective, a desktop-first agent architecture makes a lot of sense. A few reasons why:
- Context access
  - If you want agents to be genuinely useful, they need real user context. On desktop, an agent can natively and seamlessly access local files, folders, running apps, logs, configs, and other artifacts that are either impossible or extremely awkward to reach from a purely web-based agent.
- Permissions equal intelligence
  - Powerful agents need powerful permissions. Desktop agents can read and write the local file system, control native software like IDEs, terminals, browsers, or design tools, and make system-level calls or interact with hardware. This isn’t about being invasive, but about enabling workflows that simply don’t fit inside a web sandbox.
- Web parity without web limitations
  - A desktop agent can still do everything a web agent can do, whether through an embedded Chromium environment or via browser-extension-style control. The reverse is not true: web agents can’t escape their sandbox.
- An often overlooked point is that desktop agents run on user-owned compute. Browsers, terminals, and local tools all execute locally, which significantly reduces backend costs and makes high-frequency, long-running agents much more viable.
- This line of thinking is what led us to build Eigent, the opensource alternative to cowork

- ## [现在高智商人群都是如何利用AI的?(咨询贴, 疑问句) _202507](https://linux.do/t/topic/779052)
- 我有时候写东西没思路了，会让AI给我多列几组提纲，然后从中选一组满意的，自己开始拓展写
  - 很少用它生成长文，太长了它就会有幻觉，甚至跑题，而且也不符合要求它做的原意

- 和网页版的区别是你可以用不同的提示词让ai去做不同的事情，比如翻译，归纳，润色邮件。

- 知识库坑更大……新技术层出不穷不说，都不成熟。单一个rag就够研究好久, 然后高质量的数据源又从哪来, 来了以后又如何处理这些数据片, 断最后才到高质量的ai能不能组合这些数据，得到你想要的东西几个都是大坑，都不完美，要达到生产力感觉甚至差得远。

- 帮你提升效率，自己核心竞争力保持住就可以了，搞钱才是王道 其他都是虚的

- ## [What are you building with sub-4B LLMs in early 2025? Real-world use wins? : r/LocalLLaMA _202601](https://www.reddit.com/r/LocalLLaMA/comments/1qewdza/what_are_you_building_with_sub4b_llms_in_early/)
- Been running a Qwen 2.5 3B on my Pi 4 for basic home automation - it parses voice commands from my cheap USB mic and controls lights/temp through Home Assistant API. Nothing fancy but beats yelling at Alexa when the internet's down
  - Works surprisingly well for stuff like "turn off bedroom lights" or "what's the temp upstairs" - just had to keep the vocab simple and train it on my specific device names

- a Raspberry Pi monitors IP cameras and sensors. A tiny LLM processes live feeds in real-time to detect intruders, leaks, or hacks alerting you via push notifications or automated responses (e.g., locking doors).

- We used https://huggingface.co/unsloth/gemma-3n-E4B-it-GGUF for an on premise Graph-RAG System and it worked pretty well. The Model showed promising results in not hallucinating with the right prompt and context.

- I previously looked at them for simple classification tasks, I am now using FunctionGemma in a Mobile App I am building as a function caller/info extractor where a LLM call is way overkill.

- ## [Why aren't more people using local models? : r/LocalLLaMA _202510](https://www.reddit.com/r/LocalLLaMA/comments/1oj7ts7/why_arent_more_people_using_local_models/)
- Two reasons that I could think of:
  - Average consumer HW isn't just there yet to run something universally useful
  - Consumer mindset forbids to start doing things on your own
  - free time
  - Most people probably don't have the time, willingness or patience to get into the matter just far enough for using local models. The average user has no clue about how to compile llama.cpp and is also not intrigued to get into this. Things have changed a lot since the 80's.

- The problem with edge devices is simple. Battery life. Yeah, I can use a local model on my phone, and yeah, it works mostly relatively well. But I'm not willing to lose 20% of my battery on a short conversation

- Because graphics cards cost a kazillion dollars and you need 10 of them to get claude quality which is good enough but nothing less is..

- Because it's a huge pain in the ass and requires decently expensive hardware to do well.

- I love using local models and it's a great feeling having control over my privacy but honestly it's a fuckton of work. If you just wanna chat and load up LM Studio it's fine but if you want more you basically have to build everything yourself. Research mode, STT and TTS, RAG, MCP or tool use. All these are small building blocks you have to integrate yourself. It really gets messed-up if you also want these in your native language other than english. When showing my setup to my normie friends everyone quickly comes to the same conclusion.

- ## [We tried to automate product labeling in one prompt. It failed. 27 steps later, we've processed 10, 000+ products. : r/LocalLLaMA _202601](https://www.reddit.com/r/LocalLLaMA/comments/1qcsmww/we_tried_to_automate_product_labeling_in_one/)
  - We built an AI agent to localize imported food products for a retail client. The task sounds simple: extract product info, translate it contextually (not Google Translate), calculate nutritional values for local formats, check compliance with local regulations.
  - First attempt: one detailed prompt. Let the AI figure out the workflow.
  - Result: chaos. The AI would hallucinate numbers even with clean images. It would skip steps randomly. At scale, we had no idea where things broke. Every error was a mystery to debug.
- So we broke it down. Way down. 27 steps.
  - Each column in our system handles one thing: Extract name/weight/desc/...
- What changed:
  - 1. Traceability. When something fails, we know exactly which step. No more guessing.
  - 2. Fixability. Client corrects a number extraction error once, we build a formula that prevents it downstream. Errors get fixed permanently, not repeatedly.
  - 3. Consistency at scale. The AI isn't "deciding" what to do. It's executing a defined process. Same input, same process, predictable output.
  - 4. Human oversight actually works. The person reviewing outputs learns where the AI struggles. Step 14 always needs checking. Step 22 is solid. They get faster over time.
- The counterintuitive part: making the AI "dumber" per step made the overall system smarter. One prompt trying to do everything is one prompt that can fail in infinite ways. 27 simple steps means 27 places where you can inspect, correct, and improve.
  - We've processed over 10, 000 products this way. The manual process used to take 20 minutes per product. Now it's 3 minutes, mostly human review.
  - The boring truth about reliable AI agents: it's not about prompt engineering magic. It's about architecture that assumes AI will fail and makes failure easy to find and fix.

- This is case with 90% of real world AI use for non coding currently. It always requires human quailty control and intervention.

- Good example of human in the loop. I've been talking with my CEO about how the best use of LLM's at least for the foreseeable future will be wtih humans in the loop. The problem will always be getting humans to actually do the human in the loop process as the error rate begins to plummet.

- same attempt and result I had. Found Nemotron nano solved any output quality issues once it was all broken down.

- ## [Llama 3.2 1B Instruct – What Are the Best Use Cases for Small LLMs? : r/LocalLLaMA _202501](https://www.reddit.com/r/LocalLLaMA/comments/1i4cfpz/llama_32_1b_instruct_what_are_the_best_use_cases/)
- Llama 3.2 1B Instruct can work as speculative decoding model for Llama 3.2-11B/90B or 3.3-70B.

- Code completion and autocomplete

- With a bit of fine tuning they can be really good at task specific things, including structured output (do not try llama 1b for structured output without fine tuning).
  - Long term my hope is local models built into the OS, with small task specific Lora adapters. iOS is doing it, but not open to 3rd parties yet.

- For research it's nice to have a dirt cheap model to prototype datasets when evaluating LLMs I usually use 8B for that though

- ## [Real world use cases for small LLM on edge devices : r/LocalLLaMA _202409](https://www.reddit.com/r/LocalLLaMA/comments/1ffzsy0/real_world_use_cases_for_small_llm_on_edge_devices/)
- Small local models can make many factual mistakes, because it's impossible to compress the entire world model into 2 GB. However, they can be great analyzers (for their size) of the existing text.
  - Summarizing news articles, extracting insights from long web pages, finding a fact that you're searching for in a long text (a book?) and so on. Imagine it as a personal assistant in daily activities.

- Function calling. If it can do basic language to function translation, this is a perfect use. So it allows human voice or text interaction with complicated systems that would otherwise require custom coding. Also, text to structured responses, like using embeds or RAG to return well-defined SQL queries that might result from a wide variety of human specifications.

- All of these tasks involve LLM now, and are simple enough that they can be done on edge. In fact, most of them already do. Sure a cloud service can also do them, sometime better, but with a recurring cost that scale with usage. Most business that sell hardware, and user that buy it, will prefer the fixed upfront cost for R&D that small model.
  - OCR
  - Live transcription and translation
  - Summarization
  - Autocorrect
  - Basic voice control

- Analysis of secured data in offline mode . Maybe finance data , healthcare data , research data. Embed it on drone and check for suitable usecases

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

- ## We've been exploring the value of letting agents use CLIs vs just navigating a REST API directly. 
- https://x.com/dhh/status/2012543705161326941
  - The smartest models can do without a CLI, but take longer and cost more. Even small models can succeed when given CLIs. But the puck keeps moving!
- AI does better with CLIs because it's a human interface. It's designed with self-discovery in a logical way. 

- We realized this very early on. Our first party integrations with Ci providers are clis we purpose built for our vertical agent workflows. Mcps are terribly inefficient even if tools are lazy loaded for multi turn agentic conversations

- Everyone who’s been early to using coding agents, figured this out a few months ago

- Yeh my personal assistant is all CLI driven (a cli for open code to use, so I say "Plan out my day" and it goes and uses it to do that).  Super useful.  At @agentuity , we've really had to make sure our sdk, api's, and CLI are FOR agents as much as developers. Mindshift change.

- Using the same CLI for both humans and agents turned out to be surprisingly practical.

- The CLI abstraction buys you something else too: versioning. REST APIs change endpoints, parameters, auth flows. A stable CLI surface means your agent skills don't break when the underlying API shifts. That durability matters more as you scale agent count.

- This is why I recently converted my Basecamp MCP connector to a Basecamp CLI.

- ## [I benchmarked 7 Small LLMs on a 16GB Laptop. Here is what is actually usable. : r/LocalLLaMA _202512](https://www.reddit.com/r/LocalLLaMA/comments/1pzxtnr/i_benchmarked_7_small_llms_on_a_16gb_laptop_here/)
  - I tested Qwen 2.5 (14B), Mistral Small (12B), Llama 3 (8B), and Gemma 3 (all 4-bit quants) to see which ones I could actually run without crashing my laptop.
  - Qwen 2.5 (14B): The smartest for coding, but it eats 11GB System RAM + Context. On a 16GB laptop, if I opened 3 Chrome tabs, it crashed immediately (OOM).

- They are all ancient models by llm age so its kinda an invalid test. The king of low spec ram is mamba2 and sliding window attention. Try Granite 4, or Nemotron Nano 2

- I'm not considering 1-2 tokens/s "usable". Even 10 tokens/s is barely usable for the most part.

- ## [I'm curious whether people ask for the model's name in their prompts when testing on LMArena (ChatBot Arena). : r/LocalLLaMA _202504](https://www.reddit.com/r/LocalLLaMA/comments/1jtfzci/im_curious_whether_people_ask_for_the_models_name/)
  - After all, by doing this, users can know the names of the models being A/B tested beforehand, which could bias the ongoing test to some extent.

- Models never know a thing about themselves; no serious LLM user in 2025 will ask model about itself.

- well, the model's output might not be correct at all: deepseek sometimes call itself gpt. so you never now who these models actually are.

- ## [Hard lesson learned after a year of running large models locally : r/LocalLLaMA _202512](https://www.reddit.com/r/LocalLLaMA/comments/1pvxq2t/hard_lesson_learned_after_a_year_of_running_large/)
  - I’m running everything off a workstation with a single RTX 3090, Ubuntu 22.04, llama.cpp for smaller models and vLLM for anything above 30 B parameters.
  - My goal has always been to avoid cloud dependencies and keep as much computation offline as possible, so I’ve tried every quantization trick and caching tweak I could find.
  - The biggest friction point has been scaling beyond 13 B models.
  - My takeaway so far is that local first inference is viable for small to medium models, but there’s a hard ceiling unless you invest in server grade hardware or cluster multiple GPUs.
  - Quantization helps, but you trade some quality and run into new bugs.
  - For privacy sensitive tasks, the trade‑off is worth it; for fast iteration, it’s been painful compared to cloud based runners.

- vLLM works great if model + context fit into VRAM, but it doesn't do CPU offloading well - use llama.cpp for anything that spills over to RAM.

- instead of trying to use "smarter bigger" models to achieve whatever youre trying to achieve, its more reliable to use multiple parallel instances (via vllm for example) of smaller model that can communicate with each other in distinct roles to create a system that produces accurate results.

- You can also rent a card in the cloud for near local inference.

- ## [Useful patterns for building HTML tools _202512](https://simonwillison.net/2025/Dec/10/html-tools/)
- https://x.com/vista8/status/2003803470449787263
  - 用大模型两年做了150个工具。这不奇怪，强的是他只用单页HTML做！
  - 一个 HTML 文件，打开就能用，不需要安装，不需要注册。
  - 他特别强调 "不要用 React"。 因为 JSX 需要构建，这会让整个流程变得麻烦。 保持简单，就是保持可维护。
- 优势也很明显：
  - 可以直接从 ChatGPT 或 Claude 里复制粘贴出来
  - 扔到 GitHub Pages 上几秒钟就能用
  - 不需要 npm，不需要构建步骤
  - 两年后还能打开，不会因为依赖过期崩溃
- 状态存在哪里？ 没有后端数据库怎么办？Simon 有两个办法：
  - 把状态存在 URL 里。 比如，他做了一个 24x24 的图标编辑器，你画的图标直接编码在 URL 里。这样你可以收藏，可以分享，打开链接就能继续编辑。
  - 把关键的信息存在 localStorage 里。 比如 API key 这种敏感信息，不能出现在 URL 里，也不能发到服务器。 localStorage 让数据只存在用户的浏览器里。 他还用 localStorage 做自动保存。 写字数统计工具时，每次输入都会保存，这样不小心关掉标签页也不会丢内容。
- CORS（跨域资源共享）听起来很技术，但理解它很重要。
  - iNaturalist 可以查动物的观察记录
  - PyPI 可以获取 Python 包的信息
  - GitHub 的公开仓库内容都可以直接获取
  - Bluesky 和 Mastodon 的 API 也很开放
  - Simon 甚至用 GitHub Gists 来持久化数据。 因为 Gist 的 API 支持 CORS，你可以做一个纯前端工具，把用户的数据保存到他们自己的 Gist 里。
- 文件不需要上传 `<input type="file">` 不只是用来上传文件。 JavaScript 可以直接读取文件内容，在浏览器里处理。
- Python 和 WebAssembly 这是最让人兴奋的部分。 Pyodide 让 Python 可以在浏览器里运行。
  - 不是玩具级别的运行，是真正的 Python，包括 Pandas 和 matplotlib。
- Tesseract OCR、SQLite、图片压缩库，这些原本用 C 或 C++ 写的软件，现在都能在浏览器里跑。
- 这些工具真可以解决问题。更重要的是，这种方式让你能快速实验。想法到原型可能只需要几分钟。不用担心部署，不用担心维护，不用担心成本。
- 怎么起步尝试？ 一个 GitHub 仓库，开启 GitHub Pages。 然后就可以开始了。 用 ChatGPT 或 Claude 生成一个工具，复制粘贴到仓库里，几秒钟后就能在网上访问。 不需要完美，不需要复杂。 从一个解决你自己问题的小工具开始。 然后慢慢积累，慢慢改进。 两年后你可能也会有几十个甚至上百个这样的工具。 每一个都在某个时刻帮到你，每一个都让下一个更容易做出来。
- 这就是 HTML 工具的魅力：简单、实用、可持续。

- ## [Senior engineer struggles with learning LLMs foundations : r/LLMDevs _202512](https://www.reddit.com/r/LLMDevs/comments/1plxnq0/senior_engineer_struggles_with_learning_llms/)
  - I've been using ollama and openai to create some interesting side projects and to learn more about LLMs, but I think I'm hugely lacking solid foundations. Please provide me with a structure learning material for a senior engineer with some knowledge of LLMs, thanks
- Andrej Karpathy’s series on YouTube and Stanford’s CME course on LLMs and Transformers which is published to YouTube for free.
  - I had a quick look at the Stanford's course and I think it's exactly what I needed, thanks

- You need to learn four critical things
  - Your agent's core product logic is the prompt/instructions you send to an LLM. You will be spending time here with domain experts too to construct good instructions so that the model aligns to your policy. There is no magic bullet. You iterate and evaluate until you are satisfied. Making investments in evals is worth it.
  - If you want to build an agentic application, then you need to expose tools to different models. These are essentially APIs that you have today, both internal or external which the model will instruct you to run and return its results as string. 
  - There are two agentic loops, one is called the inner loop where you agent interacts with an LLM until the LLM is done (stop_reason=finish). There is an outerloop which runs to route traffic to/from agents (if you have a multi-agent architecture), ensure that only good traffic is reaching your agents and that if multiple agents need to be engaged it would be handled outside your core product logic.
  - You need exceptional observability to know what happens, how things fail, etc. And you need to account for different models in your stack so that you can easily improve performance, and/or latency and/or cost.

- ## [和AI对话，不要使用“你” ](https://linux.do/t/topic/1293395)
- AI 大神 Karpathy 分享了一个反直觉的观点：跟大模型聊天时，不要使用 “你” 这个字，也就是不要把它们当 “人”。
  - Karpathy 指出，这种问法其实是在给 AI 降智。因为 LLM 本质上并没有自我意识，它更像是一个拥有海量知识的模拟器。
  - 当使用 “你” 这个字的时候，比如问 “你的看法”，模型就会立刻被触发一种特定的人格嵌入。
  - 它会强行让自己扮演一个礼貌、安全但有点无聊的 AI 助手。这时候它吐出来的往往是那些四平八稳、滴水不漏，但实际上没啥深度的车轱辘话，也就是大家常说的 “Al 味”。
  - 相反，Karpathy 建议我们要转变思路，要想解锁 AI 真正的实力，就把 AI 当成模拟器用。
  - 举个例子，不要问 “你怎么看”，而是要设定具体的情境和角色。你可以问 “如果是三位资深产品经理坐在一起讨论这个功能，他们会提出哪些尖锐的批评”，或者 “请以一位诺贝尔经济学奖得主的视角分析这个现象”。
- 评论区也有不少高手补充，不仅要少用 “你”，也要少用 “我”。
  - 因为当你表达 “我觉得.” 的时候，AI 为了讨好用户，往往会顺着你的话说，这就导致了所谓的阿谀奉承现象，而不是基于客观事实给出答案。
- 下次写提示词的时候，试试戒掉 “你” 和 “我” 这两个字。让 AI 去模拟那些具体的专家、团队甚至反方辩手，你会发现它的回答质量能提升好几个档次。

- 那么比如 “你是一个物理学领域专业人士”、“你是一个穿小裙子的算法高手”、“你是一个猫娘” 的 prompt，到底该不该用呢？以前我看很多人鼓励在需要特定工作场景时这么做，这里面有你，但是指定了人格的类型
  - 我也在想这个问题，可以改写成 “作为一个 xxx”，“扮演一名 xxx”，然后后面全部用祈使句试一下
- “你” 的话感觉是已经指定了一个人，而用 “请以” 的话感觉会从该领域中每个人不同视角来思考，可能会更全面一点？

- 省流，多用角色扮演法。 此事在脑筋急转弯中亦有记录。 非思考模型你直接提问 脑筋急转弯类型的题目 大多模型很可能被欺骗。 但你强调这是脑筋急转弯， 让他去扮演类似领域的高手， 即使是非思考模型也能破解陷阱

- “你是一个专业的 swift 程序员”  →  “请作为一个专业的 swift 程序员，xxxx” 这么理解对吗

- 这些技巧直接调用 api 效果最明显吧？网页版的大模型和其他工具里调 API，基本都预设了角色。即使不用第一二人称，效果提升也不大吧？

- ## [8 local LLMs on a single Strix Halo debating whether a hot dog is a sandwich : r/LocalLLaMA _202512](https://www.reddit.com/r/LocalLLaMA/comments/1pdh0sm/8_local_llms_on_a_single_strix_halo_debating/)
  - https://github.com/lemonade-sdk/lemonade
  - Lemonade v9.0.6 came out today, making it really easy to run many models at the same time... and this is the best demo I could think of. Hope it makes someone laugh today!
  - This is a Ryzen AI MAX 395+ (aka Strix Halo). The models are between 3 and 8B parameters (size on disk is visible at the start of the video).
  - Lemonade is a free and open local LLM server made by AMD to make sure we have something optimized for AMD PCs. Today we released a new version that lets many LLMs run at the same time.
  - I made this quick HTML/CSS/JS app to demo the capability. It loads 8 LLMs, has them share a chat history, and then keeps prompting them until they vote yes or no on the user's question.
  - In the backend, there are 8 llama-server processes running on the Strix Halo's GPU. The web app talks to lemonade server at http://localhost:8000, and then lemonade routes the request to the right llama-server process based on the model ID in the request.
  - I thought it was funny the LLMs couldn't come to a final decision on this question. Just like people!

- A tie? That's no good. There should have been 9 LLMs, like the Supreme Court.

- Are they debating each other? Seems like they don’t spend much time disagreeing. I want to see one where they are forced into consensus or it doesn’t end (or maybe time it out and score it then)
  - There’s 5 rounds of debate. First round they are supposed to give a hot take. Rounds 2 and 3 they’re supposed to react to each other (shared chat history). Rounds 4 and 5 they’re supposed to vote.

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

- ## [你对AI最常敲的指令是啥 ](https://linux.do/t/topic/1536540)
- 还是无法运行
- 还是有问题
- continue

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
