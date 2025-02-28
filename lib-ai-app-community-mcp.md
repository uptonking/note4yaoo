---
title: lib-ai-app-community-mcp
tags: [community, large-language-model, mcp]
created: 2025-02-03T10:17:14.104Z
modified: 2025-02-03T10:17:42.052Z
---

# lib-ai-app-community-mcp

# guide

# discuss-stars
- ## 

- ## 

- ## [MCP Server Registry · modelcontextprotocol · Discussion _202501](https://github.com/orgs/modelcontextprotocol/discussions/159)

# discuss-ai-marketplace
- ## 

- ## 

- ## Cline发布MCP MarketPlace，替代人的AI员工人才市场来了
- https://x.com/aigclink/status/1892521008386773016
  - MCP协议基本上可以确定为AI Agent新时代的http协议了，这次的发布开启了Agent互联网协议的第一步，实实在在吊打封闭式的coze
  - 区别于gpts store、coze的重要的特点是可以完全本地化，可以基于他调用各种ai agent供自己本地化驱使，每个人未来都可以基于cline快速落地自己的AI员工。

- ## The AI world just got its App Store moment with Cline's MCP Marketplace. _20250220
- https://x.com/cline/status/1892351055108985126
  - This is how AI tools finally become mainstream -- when regular humans can use them without becoming developers first.

# discuss-ai-devtools
- ## 

- ## 

- ## 所以我觉得小框架（llama.cpp/ollama）对自己的定位还是准确的，我就主打单机。多机随缘，我本身也不打算做企业级。
- https://x.com/karminski3/status/1892283333192634630
- 开源推理框架这边KTransformers虽强，但几乎没有并发能力只能和llama.cpp一起座小孩那桌高性能桌的vllm和sglang虽然用8卡H200或MI300X也能把满血Deepseek-R1跑起来，但用顶级训练卡跑推理服务显然没有经济价值。何况高性能训练卡还是稀缺资源。算法部门还得炼自己的模型呢，凭啥给你拿去跑竞品模型

- ## You've probably heard of MCP (Model Context Protocol) servers, but if you're not quite sure what they are or why they matter, this thread is for you.
- https://x.com/cline/status/1890187359024730188
  - Think of pre-MCP Cline like a computer without internet — powerful but isolated in your IDE. Adding MCP is like not just giving it internet access, but also an app store where each new app gives it new capabilities.
  - An MCP server is like a menu of tools

- ## Is there a decent chunking algorithm library on NPM?
- https://x.com/mattpocockuk/status/1885264480344355136
  - Chunking: chunking text documents to be fed into a RAG system.
  - I know Langchain and LlamaIndex have some, but figured there were probably some unbundled from frameworks.

- You can test out a few chunkers here: https://chunkers.vercel.app

- Actually the LangChain splitters (which is quite good) is not bundled, it's available as a separate package @langchain/textsplitters
# discuss-ai-use-computer/browser
- ## 

- ## 

- ## 

- ## [How I taught an AI to use a computer _202501](https://e2b.dev/blog/how-i-taught-an-ai-to-use-a-computer)
- 
- 
- 

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
# discuss
- ## 

- ## 

- ## Windsurf 出了一个视频教程，介绍了 MCP 的价值与案例
- https://x.com/op7418/status/1892056272381542405

- https://x.com/windsurf_ai/status/1891664001941037123
