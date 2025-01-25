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

- [大规模语言模型：从理论到实践](https://intro-llm.github.io/)
  - 复旦大学张奇教授团队写了一本在线免费的电子书，大概有 300 页篇幅，将大模型从理论到实战的每个阶段都描述的较为清楚
# discuss-stars
- ## 

- ## 

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

# discuss-ai-protocol
- ## 

- ## 

- ## We just published a near-term development roadmap for the model context protocol (MCP) _20250103
- https://x.com/alexalbert__/status/1874853921543553147
  - Remote support (and auth!)
  - Reference implementations
  - Better package management
  - Agent support

- ## 聊几点我对 Anthropic MCP 的看法：
- https://x.com/idoubicc/status/1861620206453563446
  - 可以简单理解跟大模型已经支持的 Function Calling 是同一个东西，本质是为了让大模型可以调用外挂的服务，对接更多的数据和能力，再作为补充上下文回答用户的问题；
  - 区别点在于：Function Calling 由大模型通过 HTTP 请求第三方的外挂 API，而 MCP 是由大模型通过 RPC 请求第三方的外挂服务；
  - 从接入方式上看，Function Calling 更简单，第三方只需要写一个 API，再在大模型配置对 API 的请求参数即可。MCP 接入起来要复杂一些，第三方需要写个服务，实现协议里定义的 RPC 方法，再在大模型里面配置服务地址和参数，大模型客户端在启动的时候需要做一次服务发现，再连接到配置的 RPC 服务，才能在后续对话过程调用；
  - Function Calling 和 MCP 的核心和难点都在于大模型侧的意图识别，用户随机提问，如何找到匹配的外挂服务，实现 RAG，这是所有大模型面临的通用难题（比如 ChatGPT 有几百万的 GPTs 应用，如何根据用户提问路由到最匹配的那个 GPTs 来回答问题），MCP 协议并不能解决这个问题。Claude 客户端目前的实现方式，是让用户自己写个配置文件，告诉大模型有哪些可以调用的服务，再由 Claude 在对话时自动识别，跟 ChatGPT 之前让用户选择使用哪些 Plugins 的逻辑一致；
  - MCP 的亮点是定义了一套标准且相对完善的协议，对于大模型和应用的生态协同有很大的指导意义。类似由微软提出并在 VS Code 实现的 LSP 协议一样（定义了编辑器如何与第三方语言服务交互，实现代码补全/类型约束/错误提示等功能）。MCP 协议的适用对象主要是大模型/应用客户端和第三方服务，跟 LSP 不同的是，编程语言的数量相对有限，最多几百个语言服务，社区协同下很快就能全部支持，编辑器可以根据文件的后缀快速定位到要调用的语言服务。MCP 适用的第三方服务是海量的，MCP 的发展取决于有多少第三方服务愿意基于这套协议去实现 RPC 服务，最关键的还是大模型/应用客户端对海量 MCP 服务的路由寻址问题（没有固定的后缀，只能靠意图识别或者人工配置）。
  - OpenAI 最初开放的 API 协议已经成了一个约定俗成的标准，后来的大模型在开放自家 API 时都会选择兼容 OpenAI 的 API，主要原因有两个：一是 OpenAI 的 API 开放的早，很多应用接入了，兼容它对第三方接入友好；二是 OpenAI 的 API 实现的确实很规范，照着模范生抄作业何乐不为。MCP 会不会也跟 OpenAI 的 API 协议一样，成为行业内的新标准，这个问题取决于先有鸡还是先有蛋：如果有足够多的第三方服务基于这套协议开放了自己的服务，其他大模型/应用客户端应该会跟进；如果主流的大模型/应用客户端都支持了这套协议，那么作为一个第三方，也肯定愿意按这套协议开放自己的服务（比起为 GPTs / Coze / Dify 分别写一个 API 给智能体调用，MCP 服务只需要写一次，可以在任意支持 MCP 的客户端调用）。
  - MCP 目前不支持 Remote Server，不能在网页版调用，只能在 Claude 桌面版使用。我写了一个用 Claude 客户端分析群聊记录的程序，结合实例来看 MCP 的应用，很好理解。MCP 的想象空间还是很大的，未来可期。

- 第3点说的不是很严谨？function calling的调用是应用根据大模型的response，由应用本身去调用的，而不是大模型调用。另外function calling并没有限制用HTTP，而是看具体的tool的实现方式，tool用RPC也是可以的。

- openai想通过function call自己统一入口，对客户而言只是个现有业务+AI的硬集成，生态不对。 Anthropic想通了，不走openai老路，从开源开始，期望靠自身和开源届的推力，达成全球agent互通目标。 个人认为战略上比openai更有想象力。 这非常很重要。 如果相信MCP，现在有些特别重要的方向可以开始做了

- 我看完下来，觉得MCP最大的作用是能通过MCP服务端将本地数据传递给LLM而不是整用户数据库(知识库)暴露出去，既保护了一部分企业级用户的隐私性也方便了使用主流客户端去给企业提供官方LLMs直通车的能力

- ## 🚀 Introducing the Model Context Protocol (MCP) _20241126
- https://x.com/alexalbert__/status/1861079762506252723
  - An open standard we've been working on at Anthropic that solves a core challenge with LLM apps - connecting them to your data.
  - No more building custom integrations for every data source. MCP provides one protocol to connect them all
  - Today, every developer needs to write custom code to connect their LLM apps with data sources. It's messy, repetitive work.
  - MCP fixes this with a standard protocol for sharing resources, tools, and prompts.
  - At its core, MCP follows a client-server architecture where multiple services can connect to any compatible client.
  - Clients are applications like Claude Desktop, IDEs, or AI tools. Servers are light adapters that expose data sources.
  - Part of what makes MCP powerful is that it handles both local resources (your databases, files, services) and remote ones (APIs like Slack or GitHub's) through the same protocol
  - An MCP server shares more than just data as well. In addition to resources (files, docs, data), they can expose: - Tools (API integrations, actions) - Prompts (templated interactions)
  - Security is built into the protocol - servers control their own resources, there's no need to share API keys with LLM providers, and there are clear system boundaries.
  - Right now, MCP is only supported locally - servers must run on your own machine. But we're building remote server support with enterprise-grade auth, so teams can securely share their context sources across their organization.
  - Like LSP did for IDEs, we're building MCP as an open standard for LLM integrations. Build your own servers, contribute to the protocol, and help shape the future of AI integrations

- Making it an open protocol like LSP leapfrogged ChatGPT's "Work with Apps".  
# discuss-llama
- ## 

- ## 

- ## Ollama 0.2 is here! Concurrency is now enabled by default.  _20240709
- https://x.com/ollama/status/1810480544976626159
  - Parallel requests: Ollama can now serve multiple requests at the same time, using only a little bit of additional memory for each request.
  - Run multiple models: Ollama now supports loading different models at the same time

- ## So this is an LLM running locally? `ollama run llama3` .
- https://x.com/eatonphil/status/1797039865470570942
  - Asking it to help me with some Postgres C code. It's complete nonsense, but it's impressive complete nonsense
  - `ollama run codestral` looks about right though.
- How much RAM am I supposed to have for the 70B model?
  - B × Q / 8 → RAM requirement for llm inference in GB
  - B: number of parameters
  - Q: quantization (16 = no quantization)
  - useful rule of thumb for RAM requirement for llm inference via hn user CobaltFire
- 3bit quantized should work with 32 GB RAM with other apps closed

- based on the download size that looks like the 7b model (smallest), which are pretty hopeless at anything beyond basic coding in my experience (codestral is a 22b iirc)
  - also if you like using models from the command line i highly rec @simonw 's `llm` cli! i believe it supports ollama

- ## 🐛 [Error: pull model manifest · ollama/ollama](https://github.com/ollama/ollama/issues/3434)
  - Error: pull model manifest: Get "https://registry.ollama.ai/v2/library/codellama/manifests/70b": read tcp 192.168.3.79:64976->172.67.182.229:443: read: operation timed out
- Error: max retries exceeded: Get "https://dd20bb891979d25aebc8bec07b2b3bbc.r2.cloudflarestorage.com/ollama/docker/registry/v2/blobs/sha256/14/1436d66b69757a245f02d000874c670507949d11ad5c188a623652052c6aa508/data?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=66040c77ac1b787c3af820529859349a%! F(MISSING)20240529%! F(MISSING)auto%! F(MISSING)s3%! F(MISSING)aws4_request&X-Amz-Date=20240529T155900Z&X-Amz-Expires=1200&X-Amz-SignedHeaders=host&X-Amz-Signature=cd4472bad19931e399f39a352a4a1b0902857996b7b784b8138f168d70532277": dial tcp 104.18.8.90:443: i/o timeout

- ## [为什么Llama2大模型可以在个人电脑上部署 ？ - 知乎](https://zhuanlan.zhihu.com/p/646939066)
- 我在Meat的官网上看到 llama2 是构建在PyTorch之上的，而ChatGPT是基于TensorFlow Probability框架的，本文里面就简称TFP。

- ## [Meta AI 为什么会开源 Llama2 呢? - 知乎](https://www.zhihu.com/question/613072688/answers/updated)
- 因为所谓的LLM开源只是公布训练好的结构和参数而已，真正重要的数据和训练代码并没有开源，更别说大部分人还没有足够的GPU。
  - 即使如此，目前mistral这样的也只开源7b不开源large，llama后续还得继续观察

- Llama2 开源但不是可以随便用的商用许可。 用户数到了一定程度就不是免费的。
  - 7亿月活

- ## [Allow listening on all local interfaces _202310](https://github.com/ollama/ollama/issues/703)
- If you’re running Ollama directly from the command line, use the
`OLLAMA_HOST=0.0.0.0 ollama serve` command

- Edit the service file: Open `/etc/systemd/system/ollama.service` and add the following line inside the [Service] section:
 `Environment="OLLAMA_HOST=0.0.0.0"`

- sudo systemctl daemon-reload
- sudo systemctl restart ollama
# discuss-ai-api/tools
- ## 

- ## 

- ## We ( @jamesmurdza ) have been building Open Computer Use - 100% open source computer use agent.
- https://x.com/mlejva/status/1877054558481813799
  - The agent is using @e2b_dev 's Desktop Sandbox as virtual computer.
  - The agent is using 3 different LLMs: 🔸Llama 3.2 ( @AIatMeta ) 🔸Llama 3.3 🔸OS-Atlas ( @Alibaba_Qwen )
  - It's slow and makes mistakes but this is a big milestone for OS AI community!

- ## 想要部署本地模型但是不会计算 vRAM 占用 
- https://x.com/tuturetom/status/1842492423848804686
  - https://huggingface.co/spaces/hf-accelerate/model-memory-usage

- ## 看来大家终于达成共识了：langchain 是玩具，如果非要在生产环境用它，那它就会变成工业垃圾。
- https://x.com/beihuo/status/1840058205768167699
  - 看这代码比较，langchain 就像一个没有太多工程经验，但是又看了太多设计模式教程的人写出来的东西。使用它来实现一个生产系统，就是一个灾难。
- 同感 longchain构建思维链不如直接按照工作逻辑人工构建思维链。真正的连思维链都不清楚的创造发明，现在用AI来做为时尚早。

- ## 💄 生成式知识 UI 最核心的基础设施，目前围绕此类形态设计的 http://Me.bot 也比较受欢迎
- https://x.com/tuturetom/status/1835349759848333340

- ## Hugging Face 宣布投入 1000 万美元用于免费共享 GPU，旨在帮助小型开发者、学术界和初创公司开发新的 AI 技术，抗衡 AI 进步的集中化。
- https://x.com/glow1n/status/1791488036259434749
  - CEO Clem Delangue 表示，这一举措将通过 ZeroGPU 计划实现，促进 AI 技术的去中心化发展
  - ZeroGPU 使用 Nvidia A100 GPU 设备，提供高效的计算资源。
  - Hugging Face 的 Spaces 平台已有超过 30 万个 AI 演示。

- ## Cloudflare 的 Workers AI 每天可以免费使用 10, 000 Neurons（相当于生成100-200个LLM响应，500次翻译，500秒的语音转文字音频） ，调用方式兼容 OpenAI 
- https://x.com/scomper/status/1791804644332908646
- 好像都是小模型为主吧

# discuss-ai-knowledgebase
- ## 

- ## 

- ## Excited to share Latticework, a text-editing environment aimed to help synthesize freeform, unstructured documents _202408
- https://x.com/andy_matuschak/status/1828928979656683581 
  - It aims to help with making sense of messy piles of unstructured documents. 
  - The key idea is unifying annotation (direct reaction in context) w/ freeform text-editing (for fluid sensemaking).
- sorry, the PDF story doesn’t really exist in this prototype, but I think the design applies without alteration—just need someone to build it

- https://x.com/MatthewWSiu/status/1828929032718872734
- I explored some closely related ideas with @MagicPaperAI . You guys have pulled off the synthesis of highlights and copied fragments. I’d posit that the next key synthesis is between copied fragments and revisions of a document. Edits are partial copies.
- Great work! I like the flow of adding & organizing snippets -> augmented synthesis. The more snippets you grab under a heading, the clearer a cluster forms. That then generates 'what you're getting at' summaries & gives AI bounds to forage for related snippets. Good loop there.
# discuss-workflow-ai
- ## 

- ## 

- ## 又一个值得学习的爬虫&RPA开源库 Maxun
- https://x.com/yan5xu/status/1881150511220752884
  - 自带低代码后台，轻松抓取任何网页数据，自动提取整理成表格，还能处理滚动分页和验证码
  - 核心用 Playwright 做浏览器自动化，配合 puppeteer-extra-plugin-stealth/recaptcha 插件处理反爬和验证码，再用 adblocker 清理广告干扰

- ## Announcing Flows AI: A light-weight library to build agent workflows, on top of Vercel AI SDK.
- https://x.com/grabbou/status/1882139484994551861
  - Use any LLM and provider of your choice.
  - All patterns from Anthropic article provided out of the box.
  -  we have a branch open and POC of a builder project, where we want to provide a very light-weight flow-based UI for configuring and visualizing this. Standalone and CLI-like, so you can execute those workflows like JavaScript files
- There’s more than on the screenshot, including routers etc. Error handling can be done with a custom agent, overall - very simple, although I am interested to implement the missing blocks!

- No unnecessary abstractions whilst literally abstracting away the AI SDK 

- Is it capable of passing and using structured outputs and objects ?
  - Agent is a function, so simply use generate object inside. The helpers we provide operate on text for now (keeping things slim), but adding that if requested isn’t too much of work

- Does it support streaming?
  - Not yet, keeping scope limited. Theoretically possible
# discuss-multi-agents
- ## 

- ## 

- ## 

- ## 

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

- ## 🎯 Introducing DeepSeek-V3 _20241226
- https://x.com/deepseek_ai/status/1872242657348710721
  - 60 tokens/second (3x faster than V2!)
  - Fully open-source models & papers
  - 671B MoE parameters

- https://x.com/op7418/status/1872469838641406262
  - 他们自测的成绩整体跟 GPT-4o 和 Claude 3.5 对齐了
  - 海外社区普遍惊叹他们用 Llama 405B 十分之一的算力成本训练了一个更大更强的模型
  - Llama 3 405B 使用了 30.8M GPU 小时，而 DeepSeek-V3 看起来是一个更强大的模型，仅使用了 2.8M GPU 小时（计算量减少了约 11 倍）。
  - 并不意味着前沿 LLM 需要要大的计算集群，反而意味着你必须不能浪费你拥有的资源

- https://x.com/amasad/status/1872320808028454976
  - Craziest thing is it took only $5.5m to train. US labs spend one — maybe two — order of magnitude more for frontier models.
# discuss
- ## 

- ## 

- ## 由于DeepSeek-R1 爆火，所以为大家带来什么是LLM蒸馏技术的笔记。
- https://x.com/karminski3/status/1882233538042597423
  - 几个助记词：教师模型，学生模型，软目标，硬目标。

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
