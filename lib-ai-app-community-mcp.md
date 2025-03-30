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

- ## 各位现在用到MCP最实用的场景是什么？
- https://x.com/wong2_x/status/1904793226713706653
- 工具自动发现+接入。
  - 我说完整一点：假设你是dify这样的ai应用平台开发者，你通过coding agent+mcp协议 理论上可以自动发现并接入各种你想使用的工具（基于关键词/类型订阅，指定订阅源）。以后agent/workflow的用户理论上基本没有工具接入这件事了。

- Sequential thinking提升规划能力，搭配Tavily等搜索引擎，实现低配版Deep Research。

- 目前看没有比较落地的场景

- ## why mcp won
- https://x.com/swyx/status/1905000926127313217
  - based off successful LSP
  - dogfooding
- dogfooding is probably the winning factor
  - best abstractions come from actually using them, not from theoretical design commitees
- I feel like cursor adopting it was a huge bump

- ## 🏘️🆚️ [[RFC] Replace HTTP+SSE with new "Streamable HTTP" transport · Pull Request · modelcontextprotocol/specification _202503](https://github.com/modelcontextprotocol/specification/pull/206)
- https://x.com/jaredpalmer/status/1901633502078226565
  - This PR introduces the Streamable HTTP transport for MCP, addressing key limitations of the current HTTP+SSE transport while maintaining its advantages.
  - This approach can be implemented backwards compatibly, and allows servers to be fully stateless if desired.
- As compared with the current HTTP+SSE transport:
  - We remove the `/sse` endpoint
  - All client → server messages go through the `/message` (or similar) endpoint
  - All client → server requests could be upgraded by the server to be SSE, and used to send notifications/requests
  - Client provides session ID in headers; server can pay attention to this if needed
  - Client can initiate an SSE stream with an empty GET to `/message`

- Remote MCP currently works over HTTP+SSE transport which:
  - Does not support resumability
  - Requires the server to maintain a long-lived connection with high availability
  - Can only deliver server messages over SSE

- Benefits
  - Stateless servers are now possible—eliminating the requirement for high availability long-lived connections
  - Plain HTTP implementation—MCP can be implemented in a plain HTTP server without requiring SSE
  - Infrastructure compatibility—it's "just HTTP, " ensuring compatibility with middleware and infrastructure
  - Backwards compatibility—this is an incremental evolution of our current transport
  - Flexible upgrade path—servers can choose to use SSE for streaming responses when needed

- 🤔 Why not WebSocket?
  - Wanting to use MCP in an "RPC-like" way (e.g., a stateless MCP server that just exposes basic tools) would incur a lot of unnecessary operational and network overhead if a WebSocket is required for each call.
  - From a browser, there is no way to attach headers (like Authorization), and unlike SSE, third-party libraries cannot reimplement WebSocket from scratch in the browser.
  - Only GET requests can be transparently upgraded to WebSocket (other HTTP methods are not supported for upgrading), meaning that some kind of two-step upgrade process would be required on a POST endpoint, introducing complexity and latency.
- We're also avoiding making WebSocket an additional option in the spec, because we want to limit the number of transports officially specified for MCP, to avoid a combinatorial compatibility problem between clients and servers. (Although this does not prevent community adoption of a non-standard WebSocket transport.)

- ## [MCP Server Registry · modelcontextprotocol · Discussion _202501](https://github.com/orgs/modelcontextprotocol/discussions/159)

# discuss-news-mcp
- ## 

- ## 

- ## A new version of the MCP spec was finalized today. _20230326
- https://x.com/alexalbert__/status/1904908450473324721
  - Auth framework based on OAuth 2.1
  - ✨ Replaced the previous HTTP+SSE transport with Streamable HTTP transport
  - Support for JSON-RPC batching
  - Tool annotations for better describing tool behavior

# discuss-mcp-pm
- ## 

- ## 

- ## 

- ## 我收集了MCP市场的1000多个AI Agent MCP Server做了分析：
- https://x.com/CFC4N/status/1903090673454112828
  1. 数据管理与分析 (占比30%)
  2. 开发运维工具 (占比22.8%)
  3. 智能体自动化 (占比19.3%)
  4. 知识管理 (占比15.3%)
  5. 垂直领域应用 (占比12.5%)
  - 整体来看，提升效率的工具居多。你觉得，面向普通用户，未来哪个方向的产品，更受他们欢迎？
- 我觉得讲故事，写作，角色扮演和情感支持的最受欢迎（？ 不过这方面的产品虽然有不少，但是目前要么场景简单依赖基础模型，还不太有 mcp 的需求（比如简单的角色扮演）, 要么技术还不太成熟，我们还不知道什么技术方案更好用，需不需要 agent（比如长篇小说写作和交互式游戏）
- 以后家用电器会不会出厂自带mcp?

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

- ## 具体研究了browser-use的底层代码才发现，其网页可交互部分的结构化数据是完全靠DOM数据分析得来的而不是靠视觉模型，这也证明了为什么在普通机器上也能快速得到结果了
- https://x.com/uptonking2/status/1904040163229200491

- https://x.com/GanymedeNil/status/1904877695336395123
  - 在之前我发了一篇关于browser-use，
  - 首先网页交互的数据确实是基于playwright执行buildDomTree.js脚本而得到的，然后controller层调用browser层的playwright的一些动作的封装，其中比如点击就是基于buildDomTree.js 脚本返回的数据中的xpath来执行的。
  - 然后Agent是如何知道要点击哪个地方的呢？这里有两个部分：
  - 第一个是基于视觉，这部分是默认开启的，那么模型是怎么知道要点击的呢，上文说到js脚本解析了所有DOM节点构成了一个DOM树并且标注了DOM节点是否可以点击并且是可视的，这个脚本还做了另一件事就是将可交互的所有DOM节点进行了数字标记。每次执行任务都会提交对应的网页截图其中也包含了数字标记。
  - 第二个是基于DOM结构化数据中将可视化的数据转换成了一个如下格式的文本串： `[索引]<DOM标签名 属性 标签内所有文本/>` 直到下一个可点击元素之前的所有文本, 然后当模型接收到如上数据之后，会执行对应的funcation_calling，然后把索引传递给对应的方法，这样就成功执行了一次点击。
  - 当然Agent也可以关闭视觉的参与，然后纯靠如上第二部分的数据来进行推理，根据我的实验，如果网页视觉结构非常复杂，当关闭视觉参与可以得到不错的效果。当然Agent中执行操作是很重要的一部分，历史数据记录也是不容忽视的。这我会在之后的文章中分享。

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
# discuss-mcp-dev-impl 🚧
- ## 

- ## 

- ## Here is a step-by-step introduction to building a workflow with a custom AI agent that uses MCP.
- https://x.com/svpino/status/1904523106628059315
  - I explain every component in the video:
  1. Building the MCP server
  2. Building the agent and an MCP client
  3. Building a workflow that uses the agent
  - The goal is simple: Generate a dialogue between two people and make one yell and the other answer with sarcasm.

- ## Did you know that when you're running MCP severs locally, you can't console.log?
- https://x.com/mattpocockuk/status/1899049658883645798
  - Your MCP server connects via the same channel console.log uses (stdio). So the logs get swallowed.
  - To stay sane, I use a mcp-server.log instead

- Should be possible with the Server Sent Events (SSE) transport which is offered as alternative to Stdio, but I haven't tried it yet. Maybe something for your nest tutorial?
  - Yeah I've tried it and it works out of the box

- Why not something like pino with a file-transport and pino-pretty?
Don’t want/can’t have external dependencies?
  - Yep, could totally work - but a bit healthier to not have a dep

- Function Calling is enough… this MCP proposal is not a flexible standard nor low level.

- ## 🔡 浏览了2个MCP server的源码，对MCP server的构建有了基本的了解：
- https://x.com/jasonzhouu/status/1900220494697423202
- mcp-playwright 这个比较简单，很适合入门了解MCP server的构建，创建的server提供了这么几种情况：
  - list resource
  - read resource
  - list tools
  - call tool
  - resource用于提供资源，比如截图、浏览器控制台的日志；
  - tools提供各种功能，比如导航、点击、填写表单之类的；
  - MCP server需要给LLM提供它的功能的列表，类似于API文档，对每一个功能和参数都需要做文字介绍；
  - 以及通过调用外部资源去实现这些功能，这里就是调用playwright进行一些浏览器操作。
- browser-tools-mcp
  - 这个项目也是进行浏览器操作，但是提供了更多功能，除了可以操作浏览器进行导航、截图等功能之外，还可以可以进行对网页进行debug、性能审计，
  - 他操作浏览器的方法和上面mcp-playwright不一样，他是通过浏览器插件操作的，从而可以让LLM直接在我们日常使用的浏览器里，而不是由playwright另外开一个浏览器。
  - 为了实现这个功能，它需要建立MCP服务器和浏览器插件之间的通信，以及给浏览器插件开了很多权限。
  - MCP服务器：负责提供MCP的接口，以及调用Node服务器的功能
  - Node服务器：作为中间层，响应MCP 服务器的请求，通过websocket通信方式向chrome扩展发送请求，以调用chrome内的功能。以及调用puppeteer和lighthouse，对网页进行审计（性能、SEO等）。
  - Chrome扩展：响应websocket通信的请求，调用chrome的功能，其中包括debug功能。

- ## ⚖️ 围绕 MCP 生态可以做的一套基建方案
- https://x.com/idoubicc/status/1899666072107880839
  - mcprouter 网关，暴露统一的 http 接口给到上游调用，转发请求到 omcp 启动的下游服务，通过 apikey 鉴权，计费，类似 openrouter。

- https://x.com/idoubicc/status/1901531705678405844
  - 用 go 实现了一个 mcprouter 服务，代理了几个MCP Servers，可以在线调试，也能添加到其他 MCP 客户端使用。
  - mcp 一天一个样，得一段时间跟着跑
  - https://github.com/chatmcp/mcprouter

- https://x.com/idoubicc/status/1900469666402976234
  - MCP Server 使用 SSE Transport 实现消息传输，用的是双通道响应机制。
  - 按照这个交互流程可以实现一个 MCP Server Proxy, 对上游暴露 HTTP 接口，下游调用任意的后台服务
  - mcprouter 未来可期。

- 我觉得 还是 agent router 这个路线更靠谱

- 不想打击, 几十年前就有web service的概念和实际规范了, 所以大部分web service的问题也会是mcp的问题, 甚至其实走http的mcp就是一种web service。更很点就是wcf的一种 
  - 做出来不会没意义的, 并且显然会推动一些东西, 不过上限是看得见的

- 两个多月前我的开源项目就实现了http的中转机制，可以参考一下。楼上那个mcp-proxy项目是实现sse与stdio的转换，原理不同。

- smithery.ai 上 host 的 mcp server 差不多是类似的实现。给每个 mcp server 添加一个 Dockerfile 和一个配置文件，然后就可以在上面 host了。暴露给上游的是websocket，然后上游通过统一的 smithery mcp server 通信。
# discuss
- ## 

- ## 

- ## 

- ## Isn’t MCP literally an API for APIs. Like it’s literally an API standard for AI to talk to other APIs right?
- https://x.com/bikatr7/status/1898184652038230372
- It's not revolutionary or earth shattering, but it is an attempt to prevent having a million different ways to integrate LLMs with APIs, databases, file directories, or whatever resources. Then *any* LLM that supports the standard will just work with MCP standards built once

- The difference is that the LLM is deciding which MCPs should be invoked with what arguments. Effectively giving the LLM dynamic logic, breaking it out of its static knowledge set (weights)

- ## Windsurf 出了一个视频教程，介绍了 MCP 的价值与案例
- https://x.com/op7418/status/1892056272381542405

- https://x.com/windsurf_ai/status/1891664001941037123
