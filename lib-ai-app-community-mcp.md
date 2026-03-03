---
title: lib-ai-app-community-mcp
tags: [community, large-language-model, mcp]
created: 2025-02-03T10:17:14.104Z
modified: 2025-02-03T10:17:42.052Z
---

# lib-ai-app-community-mcp

# guide

- mcp-alternatives
  - restful api: api过于灵活, 需要自定义集成字段
  - tool-use/function-calling

- tips-mcp
  - mcp的文档内容太多, 可尝试用对应的cli工具替换api工具
# skills-xp
- https://github.com/cloudflare/agent-skills-discovery-rfc
  - Agent Skills Discovery via Well-Known URIs
  - A well-known URI provides a predictable location for agents and tools to discover skills published by an organization or project.
# mcp-xp
- MCP will die this 2026. MD files and CLI will be the substitute
# protocols-lacking
- done
  - mcp
  - skills
  - agents.md
  - agent2agent
  - acp

- tracing/commits

- worktree
# ⚖️ ai-protocols
- [Model Context Protocol](https://modelcontextprotocol.io/docs/getting-started/intro)
  - [Introducing the Model Context Protocol - Anthropic _202411](https://www.anthropic.com/news/model-context-protocol)

- [A2A Protocol](https://a2a-protocol.org/latest/)
  - [Announcing the Agent2Agent Protocol (A2A) - Google Developers Blog _202504](https://developers.googleblog.com/en/a2a-a-new-era-of-agent-interoperability/)

- [AGENTS.md](https://agents.md/)
  - [AGENTS.md – Open format for guiding coding agents | Hacker News _202508](https://news.ycombinator.com/item?id=44957443)

- [Agent Skills](https://agentskills.io/home)
  - Agent Skills are folders of instructions, scripts, and resources that agents can discover and use to do things more accurately and efficiently.
  - skills give agents access to procedural knowledge and company-, team-, and user-specific context they can load on demand. 
  - Include skill metadata in the system prompt so the model knows what skills are available. Keep metadata concise. Each skill should add roughly 50-100 tokens to the context.
  - Discovery: At startup, agents load only the name and description of each available skill, just enough to know when it might be relevant.
  - Activation: When a task matches a skill’s description, the agent reads the full `SKILL.md` instructions into context.
  - Execution: The agent follows the instructions, optionally loading referenced files or executing bundled code as needed.
  - When referencing other files in your skill, use relative paths from the skill root. Keep file references one level deep from SKILL.md. Avoid deeply nested reference chains.
  - [Agent Skills - Claude Docs](https://platform.claude.com/docs/en/agents-and-tools/agent-skills/overview)
  - [Introducing Skills | Claude _202510](https://claude.com/blog/skills)
  - [Extend Claude with skills - Claude Code Docs](https://code.claude.com/docs/en/skills)
  - Claude Code skills follow the Agent Skills open standard, which works across multiple AI tools. Claude Code extends the standard with additional features like invocation control, subagent execution, and dynamic context injection.

- [Agent Client Protocol](https://agentclientprotocol.com/overview/introduction)
  - [ACP Brings JetBrains on Board — Zed's Blog _202510](https://zed.dev/blog/jetbrains-on-acp)
# discuss-stars
- ## 

- ## 

- ## 

- ## How did MCP protocol win? It's just so ugly and lacking... why can't we just use stdio or http + skills directly? 
- https://x.com/gregpr07/status/2014032608590491855
  - Much more freedom for the LLMs + no unnecessary abstractions on top
- I use skills that include scripts they can call for talking to remote stuff. I'm not sure it's "the way" but it works pretty well for my own made stuff.

- It’s very good for non-devs

- Because it a spec and hosted companies like it over CLIs, 
  - collect usage data 
  - auto updating
  - Local MCPs are useless but remote make the end client easier to work with 
  - Plus, the ChatGPT apps sdk is an MCP

- For hosted saas, it’s much easier to distribute through MCP than skills.

- I mostly agree. One thing MCP solves is giving LLMs access to authenticated APIs without putting the API keys in context. Hosted MCP servers also solve the evergreen / SaaS-ification of tools, whereas skills have no continuous upgrade process (Claude plugins are a start but far from standard)
  - Auth matters, but MCP’s real value is a shared contract for stateful tool behavior. that’s the piece scripts or CLIs don’t standardize once agents get long-running...

- I am still a big proponent of skills. but transport isn't the point imo. You can do stdio or HTTP any day. MCP “won” because it adds a server boundary: discoverable tools + schemas + auth + policy in one place. And the line between tools + skills is blurring (you can ship skills via MCP too, e.g. fastmcp 3.0 beta). That makes it portable across clients and makes hosted/commercial tool servers (metering, audit, permissions) a first-class thing enabling monetization.

- ## [Is MCP actually better than REST for building AI agents, or is it just hype? : r/AI_Agents](https://www.reddit.com/r/AI_Agents/comments/1pbe2ua/is_mcp_actually_better_than_rest_for_building_ai/)
  - MCP gives agents structured context and real tool discoverability, which REST never tried to solve. But wrapping APIs into MCP is still extra work. So does MCP deliver enough value to beat REST for agent tooling, or not really?
- MCP repackages existing REST APIs for LLMs. Most REST APIs aren't natively built for LLMs and don't have to be. They often give too much flexibility for an LLM to handle error free. So I think it's a solid standard to put your REST API into a modular, LLM-ready, reusable package, while still keeping the original REST API.

- Given the advances in tools, is MCP necessary? Can't the tool wrap an API invocation and return structured results?
  - With coding agents this is the way

- If you control both sides of the coin (client/server) the option is clear API wins hands down in my testing with full control over the endpoints and protocols; MCP is an overhead that is not needed.
  - The protocol provides a contract both sides are building towards so when combine they just work. This is similar to Integrators of yester-year where you only need to build one side of the bridge and you can connect to whole world of existing services and applications (all without the man in the middle).

- It isn't much different except for the instructions on how to use each tool, what would be each api endpoint. I agree that looking for a way to standardize is a solid move. Most APIs require bespoke, custom integration for each. I see MCPs as an attempt to integrate as many tools together as possible.
  - Totally get that. The goal of MCP should be to streamline integration and reduce the chaos of custom setups. If it can really simplify the toolchain without adding too much overhead, it might be worth it in the long run.

- Same thing only you have tool announcer endpoint in many ways. Stdio is insecure where api is a know security structure and url is universally to models from training so it’s just a door type to access. Everything else is just fitting security and pipes to api lines

- ## 💥 各位做 chat bot 客户端、并最近在接入 MCP 协议的大佬们, 想请教一下大家是怎么做上下文压缩的呀, 
- https://x.com/Shenqingchuan/status/1906987971703865804
  - 一些 MCP 调用了工具返回的内容太长, 导致整个 messages 的总 token 数爆炸多, 这个怎么解决呢？

- 具体解决的时候分pre-retrieval，in-retrieval，和post-retrieval的优化。

- 核心还是大模型能力的挖掘。一次请求，返回多步tools，然后分布执行把结果信息压缩返给大模型处理。

- 128k的context length都不够用，那说明这个问题用mcp解决不合适

- ## 🌰 尝试复刻了 manus 的 replay 功能, 从 TARS 的开源 repo 学到的两个架构特点
- https://x.com/Nin19536/status/1905975354227040314
- 1️⃣mcp 统一工具协议
可插拔，可扩展非常关键，且 tool 定义和 tool 执行对外只暴露接口，agent 端不关心实现。
- 2️⃣事件管理
管理好所有流式输出、任何工具 update，都需要考虑到前端展示 event 的方式，提供更好交互。而且事件管理有利于模型统一管理上下文。以事件时间戳永远自增，便于时间回溯和用户观测。
- 代码是基于我去年八月就实现的原型 MVP重构 cosmos 项目
  - 可以去看看 TARS 的代码还挺清晰的
  - 你看一下 manus 返回的数据结构就行了，前端复刻不复杂。

- ## mcp 竟然能把这么简单的功能搞到这么复杂，然后竟然还是走 stdio。这是完全不打算给麻瓜用啊。
- https://x.com/xicilion/status/1905981157503902021
- 让一部分人先用起来
- mcp假设市面上有一堆A客户端啊。每个都要支持某个公共服务。mcp价值才出来。假设世界上只有一个chatgpt客户端。直接写function。calling客户端函数就够了。
- 的确如此，官方: mcp remote 在做了，认证在做了
- 只能说规范化≠简洁

- https://x.com/jezell/status/1906368293239423018
  - ⚖️ It's pretty crazy to me how the entire MCP ecosystem is building on top of the Stdio transport rather than http. "Works on my machine" dominating AI tooling continues to be a thing.

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

# discuss-mcp-cli 
- ## 

- ## 

- ## 

- ## [CLI is all you need? Do we really need MCPs : r/codex _202603](https://www.reddit.com/r/codex/comments/1ri5m0f/cli_is_all_you_need_do_we_really_need_mcps/)
- Anything that has a CLI is WAY better than using an MCP imo. I think this is one of the shifts that most people don't talk about but everyone has converged on separately.
  - Maybe I'm wrong. MCP can still be useful if you can package it in a way that makes it easier for non techies to access your stuff, but for anyone slightly technical, a CLI will work better*
  - *Provided you're okay with the authentication tradeoffs.

- CLI is all you need. Also much easier to test and distribute.

- Creator of openclaw made the same point before. AI models are always much better at using CLI

- CLIs also tend to have request/response semantics and in Codex’s latest newsletter, there is now MCP support for WebSockets which can be much more useful instead of packaging state in every payload over the wire back and forth, because HTTP is a stateless protocol.
  - That said, my take is that MCPs do have a purpose that CLIs won’t solve. MCPs are typically servers which means that they can be stateful and it would be nice if optimizations were made such that state is kept there that returns a reference and doesn’t blow up an LLM’s context window. Just some food for thought.
- CLI can also be stateful. Many have the daemon pattern.
- Well git is certainly stateful and is a CLI, no?

- ## the cli is dead - the big cli players are all pivoting.
- https://x.com/jediahkatz/status/2025263982462820544
- CLI for humans is dead, but not for agents. We need a CLI for all pro tools like Adobe, CAD, etc so agents can take over that work.
  - New OS will be bi-modal. It will make agents producitve and help humans monitor & review work.

- TUI is goofy but CLIs are the future. Agents are better at using non-interactive CLIs than humans are at using GUIs

- the tui part isn't important + is an artifact of teams wanting to ship fast and avoid making risky/expensive product bets. the real value is in having an executable + composable "agent" that can be dropped in any sandbox and given a task. it's a nice contract for "agent shape"
# discuss-mcp-pm
- ## 

- ## 

- ## 

- ## 

- ## MCP servers are just bad skills files. 
- https://x.com/nisten/status/2025650149968519237
  - On that note, wondering why not just make a standard openAPI endpoint with regular discovery ability (which MCP still doesn't have lol) and feed the bot the skill tree AND backend via that.
- opencode supports https://github.com/cloudflare/agent-skills-discovery-rfc

- people always seem to focus on mcp from a tool discoverability pov, and never mention that oauth support is baked in.
  - we need a way for non-coders to authenticate against the tools.
  - skills literally help in no way with that.
  - dream situation would be:
  - better skills discoverability (like you mentioned)
  - mcp drops the concept of tools and focuses on authorization
- what authentication mechanism does the user use? copy/paste an api key? implement oauth yourself for each endpoint?
- I love using MCPs instead of CLI tools because I like giving my agent a more restricted token. I don't want Son of Anton force pushing to master with my auth token.

- yeah skill discovery is the real gap here. just add OpenAPI + /.well-known/skills and you're 90% there with existing tech
  - no need to reinvent auth, rate limiting, or observability patterns we already solved

- The difference is that MCP presents a validated and structured schema that correlates to internal deterministic logic calls. 
  - Where as skills, even with resources, are bloated textual descriptions that result in stochastic behaviour and exploratory runs by the agent aiming to accurately affirm direction.
  - You can be reductionist and say that MCP == Skills, as they seem to address the same problem on the surface - but fundamentally they are not the same thing. 
  - Now, having MCPs provide Skill packages to better instruct them on how to interact with the API, like tricks, common workflows, gotchas, etc etc - that is a good idea, and the MCP protocol spec already supports this. I use this in all of my custom MCPs. 
  - I also use OpenID Connect and OAuth for auth, SSL over TLS for encryption, and .well-known/ for discoverability. As these are all industry standard methods for each issue.
  - The issue arises that the vast majority of people building/consuming MCP and Skills are not actual software engineers, and do not actually know about these things.

- Try an OpenAPI-to-MCP proxy, that's exactly the logic you're talking about. It basically turns your spec into tools for the model without messing around with new configs.

- ## Manus 和  OpenAI 的Operator 催生一个新的需：云端渲染的浏览器。
- https://x.com/leeoxiang/status/1897855654091800798  
  - browser-use
  - cloudflare browser-rendering
  - browser base

- 也会促进另一个方向，bot detection 哈哈

- 如果推广应用的话，最有价值的就是用户行为数据100%被记录分析。

- 借助这种模式，做爬虫是不是无敌了，真实账号，真实操作，真实指纹

- 不错，这个用来做抢票，岂不是无敌
- headless-chrome 以及 puppeteer / playwright 这种东西存在很多年了，跑在docker里就行

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
# discuss-ai-use-browser/computer/container
- ## 

- ## 

- ## 

- ## 

- ## playwright 的 --extension 模式，配合这个 Playwright MCP Bridge 插件，可以直接操作自己原有浏览器的实例
- https://x.com/jakevin7/status/2025209913153388773
  - 这个插件允许 AI 直接操作你当前正在使用的标签页。免登录： AI 可以直接使用你已经登录的 GitHub、AWS 或企业内部账户。保留 Cookie和 所有的登录状态、偏好设置和本地缓存都对 AI 可见。
  - 尽量只在本地使用，保证安全。

- ## ["OptGuideOnDeviceModel" folder taking up 3GB. Have no idea what this folder does. : r/chrome](https://www.reddit.com/r/chrome/comments/1jslb22/optguideondevicemodel_folder_taking_up_3gb_have/)
- It's a gemini nano model to enable chrome API for AI tasks 

- [Get started with built-in AI  |  AI on Chrome _202412](https://developer.chrome.com/docs/ai/get-started)

- ## Let’s dive deeper into WebMCP's new APIs. 
- https://x.com/ChromiumDev/status/2024932531032789187
  - First, the Declarative API: it's built for high-precision, form-based tasks. By defining tools in your HTML, you enable agents to book flights or file support tickets with speed and reliability that scraping can't match
  - For more complex workflows, there’s the Imperative API. Use this for dynamic scenarios like stadium seat selection or real-time data filtering that requires JavaScript. It provides a structured bridge for agents to execute logic without getting lost in the DOM 

- got adopted because search engines rewarded it. WebMCP will follow the same path... once agent traffic matters, sites that don't declare tools just won't get used.  

- ## WebMCP 是一套标准化协议，让网站可以主动告诉 AI Agent "你能在我这里做什么、怎么做"，而不是让 Agent 自己去猜测和操作 DOM。
- https://x.com/dotey/status/2022392133827932255
  - 它提供了两种 API：一种是声明式的，基于 HTML 表单定义标准操作；另一种是命令式的，通过 JavaScript 处理更复杂的动态交互。典型应用场景包括客服工单自动填写、电商购物导航、机票搜索预订等。

- 这就伟大了! 因为它定义的是所有服务商的服务器给用户的服务api, 使得用户日后只需要本地agent就可以获取任何服务商的各种服务

- 之前的软件设计是面向用户、开发者，现在不得不重新设计，以大模型为使用者。

- 这波操作没看出来对网站有啥好处，网站只是提供数据

- ## [Chrome’s WebMCP makes AI agents stop pretending : r/mcp](https://www.reddit.com/r/mcp/comments/1r2m7ev/chromes_webmcp_makes_ai_agents_stop_pretending/)
  - WebMCP basically lets websites register tools that AI agents can discover and call directly, instead of taking screenshots and parsing pixels.
  - AI agents tools like agent-browser currently browse by rendering pages, taking screenshots, sending them to vision models, deciding what to click, and repeating. Every single interaction. 51% of web traffic is already bots doing exactly this (per Imperva's latest report).
  - Edit: I should clarify that agent-browser doesn't need to take screenshots by default but when it has to, it will (assuming the model that's steering it has a vision LLM).
  - WebMCP flips the model. Websites declare their capabilities with structured tools that agents can invoke directly, no pixel-reading required. Same shift fintech went through when Open Banking replaced screen-scraping with APIs.
  - The spec's still a W3C Community Group Draft with a number of open issues, but Chrome's backing it and it's designed for progressive enhancement.
  - You can add it to existing forms with a couple of HTML attributes.

- That is not at all how agent-browser works. It uses accessibility snapshots to find interactable elements, no screenshot involved.
  - It CAN take screenshots when it needs to and send to vision LLM/s when navigation isn't straightforward. By default it doesn't need to.

- Pretty sure your premise is off. Playwright, for example, just interacts with the DOM of your webpage. It can take screenshots as well but that’s not what it uses to navigate…
  - That’s quite difficult when the page is mostly JavaScript.

- How does this differ meaningfully from the llms.txt protocol? Most sights that want to be accessible to llms just post one of those

- ## WebMCP: AI agents can now interact *directly* with existing websites and webapps - not by using the "human" app interface.
- https://x.com/liadyosef/status/2021151526375268643
  - This naturally complements MCP Apps towards the future of agentic UI.

- This unlocks real agent-native workflows. Web as an API, not an interface.

- hmm, direct DOM manipulation is powerful but risky - what happens when sites change their layout? we tried this approach for test automation. ended up with 30% flake rate vs 5% with proper API interfaces. sometimes the old ways are better

- the browser was always the universal API. someone just finally made it official.

- WebMCP expands the attack surface significantly. Agents interacting directly with services - bypassing human UI - means new injection vectors. Forms declaring MCP capabilities become targets. Every web service's security posture is now an agent security question.

- ## 🧭⚖️ Chrome 146 includes an early preview of WebMCP, accessible via a flag, that lets AI agents query and execute services without browsing the web app like a user.
- https://x.com/firt/status/2020903127428313461
  - Services can be declared through an imperative navigator.modelContext API or declaratively through a form.

- Could this build upon the accessibility tree and ARIA attributes, instead of creating yet another separate API?
- Maybe MCPs are better UI for accessibility long term? Then user can use the UI they want. chat, voice +++
  - Maybe they are if ARIA is too constrained. But I think they should study prior art before shipping yet another separate API.

- the funniest side effect of this will be that sites will mostly adopt this to either rate limit or block agents from using their site

- The brilliance lies in how it standardizes the chaos. Instead of traditional agents struggling with slow, fragile OCR or DOM tree analysis to "guess" button positions, It offers a subtle, friendly interaction layer.
  - It allows site owners to explicitly define schemas with lightweight code, giving agents a stable CONTRACT via registerTool. 
  - The site tells the agent how to behave, and the agent executes predictably—no more breaking boundaries.
- We’re back to wrapping garbage in more layers. If I have to manually code a schema just to tell an agent how to behave on my site, it’s not "auto" anymore. MCP feels like another over-engineered trap. They are just patching their way up instead of killing the protocol.

- this makes the browser a bit like a potential harness

- That is the right way to navigate for agents. Browser use is too slow and too messy to be honest. Soon, this would become an standard.

- This is the browser becoming agent-native. Instead of agents scraping UIs, sites declare what services they offer. Agents call them directly. 'Apps are dead, APIs win' — but now the browser enforces it. The UI layer really is becoming irrelevant.

- Chrome embedding MCP natively is massive. Websites can declare AI-callable services via forms and navigator.modelContext. Security teams: think about agents executing your backend directly. Input validation just got more interesting.

- ## browser-use - [Closer to the Metal: Leaving Playwright for CDP _202508](https://browser-use.com/posts/playwright-to-cdp)
  - Playwright and Puppeteer are great for making QA tests and automation scripts short and readable
  - We decided to peek behind the curtain and figure out what the browser was really doing, and it made us decide to drop playwright entirely and just speak the browser's native tongue: CDP.
  - By switcing to raw CDP we've massively increased the speed of element extraction, screenshots, and all our default actions. We've also managed to add new async reaction capabilities to the agent, and proper cross-origin iframe support.
- In our case that time has finally come for Browser-Use and playwright-python, the library that we've historically used to drive our browsers with LLM-powered tool calls like click, input_text, go_to_url.
- Playwright also introduces a 2nd network hop going through a node.js playwright server websocket, which incurs a meaningful amount of latency when we do thousands of CDP calls to check for element position, opacity, paint order, JS event listeners, aria properties, etc.

- A Quick History of Browser Automation

- So why did we feel the need to write our own with cdp-use? Well for all the same reasons as everyone else: everlasting desire to be closer to the metal and have more detailed control over every step.

- How do Browser Drivers Work?
  - All these adapter libraries, drivers, and AI helper extensions really just exist to pass messages and make RPC calls to these underlying browser APIs

- How does Playwright work?
  - Playwright achieves multi-languge support by using a client-server model between clients in various languages and a single core implementation that runs as a node.js websocket server.
  - The playwright node.js relay server accepts standardized "playwright protocol" RPC calls from playwright clients, and then sends out CDP or BIDI calls to the browser to execute them.
  - Playwright also nicely abstracts lower-level browser ideas like targets, frames, and sessions into simple Page and BrowserContext handles and (usually) manages to keep those handles in sync and not deadlocked across node.js, the browser, and python.
  - Unfortunately the double RPC through the node.js relay means some state inevitably drifts across the 3 places (and across three different languages and runtimes):live browser, playwright node.js relay process, python client process
  - When a tab crashes in the browser or some operation is performed without focusing a page correctly, there are edge cases where the node.js process can hang indefinitely waiting for a browser reply, meanwhile the python client needs to send the CDP call the browser is expecting in order to proceed. Currently we have no recourse but to kill -9 and attempt to reconnect to the browser from scratch with a new playwright instance.

- Did you know there are at least 10 different ways a tab can crash in Chrome?

- A type-safe Python client generator for the Chrome DevTools Protocol (CDP). This library automatically generates Python bindings with full TypeScript-like type safety from the official CDP protocol specifications. It's only shallow type bindings, no complex logic for session management, pages, elements, etc. just 100% direct access.

- We've introduced a new event-driven architecture to better fit the underlying event-driven architecture of CDP. Now we can subscribe to and respond to CDP events, which we set up in "watchdog" services that monitor for various things.

- ## 🚀 Today we're bringing vision to Bolt: Bolt now sees your app exactly like users do, enabling faster, more precise edits pixel by pixel (& fewer tokens!) _20250221
- https://x.com/boltdotnew/status/1892620446106886396
  - The Visual Inspector works across all web frameworks (React, Vue, Svelte, Next & others) and mobile apps (Expo).
  - To use it, just click what you want to change & tell Bolt what to do

- 🤔 Does this send a screenshot with `html2canvas` so the app can see any layout issues and you don’t need to take a screenshot? Or does it just send the raw html that you click on. Also does it integrate with frameworks to send the component name?
  - it's using https://github.com/qq15725/modern-screenshot to send images
- HTML & CSS are so finicky, lots of potential issues you could run into with loops of asking it to do the same thing if you’re not sending proper context & visual information (and instead just raw DOM)

- This is cool, I hope we can get free fixes soon, so we optimize our spending on tokens
  - They need to release diff editing. Right now a small fix has to rewrite an entire file, when in reality it could just be a 2 line fix. They only have diff editing for the pro plans though, not the free plans.

- Please make visual inspector like how lovable dev has did , it gives options to change properties directly . Request you to bring that feature.

- It's going to be hard to beat Lovable unless you stop burning credit to fix it..
  - For React projects, maybe yes. But for non-React projects (SolidJS in my test), @lovable_dev is simply not the tool (at least for me).

- ## I just built this CRACKED Cursor MCP extension that makes your IDE fully aware of all the logs in your browser.
- https://x.com/VigneshChinnad2/status/1895198959288885314
  - [AgentDesk](https://www.agentdesk.ai/)
  - ✅ Check all console logs + errors
  - ✅ Analyze network requests, responses and errors
  - ✅ Make changes to a selected element in your browser
  - ✅ Take screenshots of your browser
  - Open source, FREE and compatible with Cursor, Cline, Continue and Zed.
  - My extension is based on MCP which means it only works with Anthropic models. 

- is it possible to select particular element and send to cursor to ask for color/ other changes. similar to Bolt visual Inspector. it will solve major pain for me.
  - Yes BrowserTools can do this for you in Cursor
  - Just use the built in chrome dev tools selection tool and then ask cursor to: “get the selected element and implement xyz changes…”

- Have you considered adding support for DevTools Recorder for lightweight testing loops?
  - [Record, replay, and measure user flows  |  Chrome DevTools  |  Chrome for Developers](https://developer.chrome.com/docs/devtools/recorder)

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

# discuss-protocols-lacking
- ## 

- ## 

- ## 

- ## By default, Claude Code worktrees are created in .claude/worktrees inside your project.
- https://x.com/dani_avila7/status/2025336648913793506
  - You can change this location in Settings → Claude Code under the "Worktree Location" option.
  - It's good practice to keep your worktrees outside your project directory. 

- solid tip on the external location — ran into merge conflicts once when worktrees got gitignored incorrectly. ~/dev/.worktrees/ works great, keeps everything clean and no risk of accidentally committing the worktree dir
  - I keep mine in ~/worktrees - much cleaner and you avoid accidentally committing worktree artifacts. Also makes backup/cleanup way easier.

- pro tip: if you're using multiple projects, set up a shared worktree location like ~/.claude-worktrees/{project-name} so you can easily find and manage them across different repos

- I open all my worktrees in an S3 bucket.

- decapod does git worktrees better -- and they're usable by all agent(s), not just Claude.
# discuss-ai-protocol ⚖️
- ## 

- ## 

- ## 

- ## 

- ## 🚀 cursor: We're proposing an open standard for tracing agent conversations to the code they generate. It's interoperable with any coding agent or interface.
- https://x.com/cursor_ai/status/2016934752188576029
- Would’ve been great to include a quick example of how these traces would render in common observability tooling (e.g., spans/attributes in OTEL, a sample timeline in a trace UI). The spec is “UI agnostic, ” but a reference visualisation would help adoption.

- Right now the biggest pain point with agent-generated code isn't quality — it's auditability. When something breaks in production, the question isn't "what changed?" but "why did the agent change it?"
- Agent Trace solves the provenance problem. If this becomes the standard, it could unlock:
  - • Better code review workflows (trace-aware diffs)
  - • Agent performance benchmarking across teams
  - • Compliance-friendly AI coding in regulated industries

- git blame for the agent era!
- The real pain point this solves: mass-accepting agent edits then 2 weeks later staring at code you don't recognize, unsure if past-you or claude wrote it. git blame doesn't tell you that

- Reproducibility is the missing piece in agent systems. Teams stop shipping when they can't debug why an agent veered off path. 

- https://x.com/cognition/status/2017057457332506846
  - open standard for mapping back code:context.
  - [Cognition | Agent Trace: Capturing the Context Graph of Code](https://cognition.ai/blog/agent-trace)

- ## Cursor制定了一个开放标准：https://agent-trace.dev，用来追踪代码的来源（agent还是人）、元数据（如关联的对话链接等）
- https://x.com/wong2__/status/2017062215275466802
  - 在一个git commit里同时包含代码和实现这段代码的claude code对话
- 我也有这个需求，现在只是简单的把每个 prompt 当作 commit message push 上去, 这个看起来还有丢丢麻烦，要是对话完验收代码之后一键全搞定就好了

- 如果你用 @AmpCode 的话， 它默认会把 thread 链接直接带上 commit，比 Simon 这个好看一些， 不过它数据是存储在 Amp 自己的网站上的

- ## agent.md + skills - both open standards, and can combined with an agent harness (claude code, codex, deepagents) can pretty much define a custom agent
- https://x.com/hwchase17/status/2003599022871777467
  - currently there's no way to package those together - claude plugins is close but i think lets you add an http://agent.md
  - am i alone in wanting this? or do other people want as well?

- AGENTS.md does not feels like a good place to define Agent, it is more like a description of environment where other Agents will run or use.
  - As an idea, I think Custom Agent might be defined as skill with references or event includes others skills. https://agentskills.io do not encourage this, but from spec point of view nothing blocks this.

- agent.md as the packaging layer feels right but the missing piece is a runtime that can resolve skills and harness deps across repos the way a package manager does, not just per project directory.

- like, a package manager for agents?
  - This is largely what a collection in https://prpm.dev is 
  - Package skills and agents together into an installable package with dependency tracking and a lock file.

- totally agree that there should be a consolidation but i think `agents.md` might not be the best place, rather a folder like `.agents` would be immensely helpful to standardize everything an agent normally has and could use: skills, hooks, settings, rules, plans, etc
  - @prpmdev is cross platform and contains a manifest to define all the skills, hooks, agents. Collections also is a convenient way to specify all the dependencies in one go to install

- 100%. This is the 'Containerization' moment for Agents.
  - At ProdMoh, we view this 'package' as a Governance Artifact.
  - We currently compile Policies (Constraints) + Stack (Skills) into .cursorrules or .windsurfrules to define that runtime behavior.
  - A standardized http://agent.md that binds Constraints with Capabilities is the only way to make agents portable and safe.

- feels like we're 90 percent of the way there on modular agents but still duct taping the last mile tbh. the second someone nails a clean way to bundle and ship these setups, it’s gonna explode usage rn.

- Package manager for agents would unlock reuse. Start with a tiny spec: manifest with name version, list of skills, harness refs, env, and dependencies, plus a minimal registry. That boosts composability and versioning. Is a small spec enough to push this forward?
  - @prpmdev has this minus the harness ref but is cross platform out of the box

- I prefer using specialized subagents, so orchestrator can easily do longer tasks without filling context with nonsense system prompt that is altering behavior for whole conversation. 

- Tag the right people that can fix this, I would if I knew who.

- ## Agent Skills is now an open standard _202512
- https://x.com/alexalbert__/status/2001760879302553906
- Standardizing agent skills decouples capability definition from implementation, which is critical for composability across models, runtimes, and execution layers.

- ## ai rules and mcp is madness. What are we doing!
- https://x.com/shadcn/status/1955254151807635602
- The ironic part is that most of them are MDs (for rules) and json for MCP. We could really solve this with two files (promp.md and mcp.json)

- here's the same mess in the AI SEO industry, but with the name itself
  - The number one task for the AI SEO industry should be to agree on one name! Currently we have: * AI SEO * AEO * GEO * AIO * LLM * SEO * LLMO * LEO

- A unified memory layer for all coding agents to the rescue
- https://github.com/RedPlanetHQ/core /AGPL/ts
  - Your unified, shareable memory layer for coding agents. 
  - Compatible with Cursor, Claude Desktop/Code, Gemini CLI, Windsurf, AWS's Kiro, VSCode, Cline
  - a portable memory graph built from your llm interactions and personal data, making all your context and workflow history accessible to any AI tool, just like a digital brain
  - This eliminates the need for repeated context sharing 
  - Plug n Play: Instantly use CORE memory in apps like Cursor, Claude

- https://github.com/intellectronica/ruler /MIT/ts
  - apply the same rules to all coding agents
  - Centralised Rule Management: Store all AI instructions in a dedicated .ruler/ directory using Markdown files
  - MCP Server Propagation: Manage and distribute Model Context Protocol (MCP) server settings
- Can it fetch rules from a GitHub repo? We use multiple repos and worktrees but have a single toolkit and rules. Keeping all repos updated is more tedious than managing individual agents.
  - Not yet, but sounds like a good idea. Would you mind adding an issue? I'm planning the 0.3 cycle now so will include that.

- @AmpCode has this proposal to address that issue

- let's make a new standard to solve all this mess

- ## MCP uses JSON-RPC. A2A uses JSON-RPC. Did I miss the memo, why JSON-RPC suddenly.  What happened? Did we forget to train AI on protocols since 2009?
- https://x.com/ibuildthecloud/status/1915584728616575281
- Proto is bad outside of strongly typed languages and LSP used JSON RPC (vscode is JavaScript/Typescript).

- tRPC uses it too. turns out people really did just want SOAP/WSDL conceptually but we didn't like XML for some reason.
- blockchains use json rpc

- The rest of the group got stuck debating Thrift versus Protobufs. I heard they were still having meetings.

- ## I built an MCP server for WhatsApp
- https://x.com/LukeHarries_/status/1905986562388635913
  - Why? 99% of your life is stored in WhatsApp, by connecting an LLM to WhatsApp you get all this context. And your AI agent can execute tasks on your behalf by sending messages.

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
# discuss-skills
- ## 

- ## 

- ## 

- ## Just me or Codex and OpenCode *much* worse at automatically using skills than Claude based on just the prompt text? Need to explicitly invoke them for them to be used.
- https://x.com/adamwathan/status/2026745037388742767
- skills are not reliable in any, read this: [AGENTS.md outperforms skills in our agent evals - Vercel](https://vercel.com/blog/agents-md-outperforms-skills-in-our-agent-evals?utm_source=chatgpt.com)F

- Same experience here. Claude seems to have better implicit skill invocation. I've found that explicit CLAUDE.md definitions help a lot - the model tends to 'forget' available tools without that explicit anchor.

- ive got 38 skills in my setup and claude fires them from context without me naming them. tried opencode with the same skill definitions and had to explicitly call them most of the time. noticeable difference

- ## I forked Claude's pptx skill to make Claude Code generate gorgeous presentations
- https://x.com/nityeshaga/status/2011188015503437856
  - Claude can generate presentations using the pptx skill from @AnthropicAI but its output can be quite bland.
  - So I played around with the pptx skill, iterated it, built a design system, gave it image assets, gave it access to run nano-banana using api and added custom commands. 
  - End result? An every-pptx plugin!
  - All happening 100% inside Claude desktop app
- Is each slide a static image or fully editable slides within Google Slides?
  - Fully editable in Google slides

- why create presentation when you can create working prototype?
# discuss
- ## 

- ## 

- ## Top 7 MCPs worth adding to your workflow _202602
- https://x.com/101babich/status/2023766057211572293
  - [Top 7 MCP for Product Designers.  _202602](https://uxplanet.org/top-7-mcp-for-product-designers-4bd77f4e281c?gi=975c2cc9ca30&sk=ec2956f75b5285dbd69d6598631d83e9)
1️⃣ context7 (Pulls live library docs into your AI tool so it codes with the right context)
2️⃣ NotebookLM MCP (Feeds your research and specs directly to AI, so it builds with real user needs in mind)
3️⃣ shadcn/UI MCP (Gives AI actual component knowledge instead of letting it guess your UI)
4️⃣ Figma MCP (Turns your designs into code using real layout structure, not screenshots)
5️⃣ Notion MCP (Lets AI read your PRDs, pull specs, and update tasks without leaving the editor)
6️⃣ Google Analytics MCP (Query your GA4 data in plain English to validate design decisions fast)
7️⃣ Supabase MCP (Set up your entire backend through natural language. No SQL needed.)

- context7 alone killed half my cursor hallucinations. the model was fine — my docs were just outdated. who knew

- Solid list. The biggest win with MCPs is keeping agents grounded in real sources of truth. The part I worry about is governance: permission scopes, write versus read separation, and audit logs so an agent cannot silently mutate Notion or analytics. Do any of these ship a permission manifest standard yet? I am curious what your must have guardrails are for permissions and auditing, especially for Notion and Analytics, so the tool can read and write safely without leaking or clobbering info.

- MCPs help, but structure beats access. Without clean schemas context just amplifies mistakes.

- ## 🤔 MCP is just like...an API right?
- https://x.com/jamesqquick/status/1950604084370620719
- MCP is an API with ELI-agent docs built into the wire format
- The "docs" in that case is just the description field for a given tool right? That doesn't inherently make them good? Depends on how detailed the description field is?
  - Description on the overall service (what is it for, what problems can it solve), on each tool (what is it for, what example problems can it solve, what are usage examples) and each param (if helpful)
  - The http://grep.app MCP https://vercel.com/blog/grep-a-million-github-repositories-via-mcp is a good example
- That's a great example! But that's also just dependent on the creator of the MCP server itself. If do a shitty job detailing the what, why, and how, then its not inherently an amazing experience?
  - Right. It's currently very difficult to make a good MCP server. It's a prompt engineering exercise mostly given that you probably already have an API which you call from the MCP implementation

- Yes along description and inputSchema. Like an Open API document.

- No. It’s glorified API. The logic is encapsulated. So instead of coding up the request, you just request in English.

- MCP is a function call, which is an API wrapper

- not quite - MCP is more like a standardized protocol for AI agents to connect to external tools and data sources. think of it as a universal adapter that lets AI clients talk to different services without custom integrations for each one.

- Yeah, I’d say like an extension that wraps an api
- It’s a wrapper on api — to make it accessible to llms

- not really, MCP is more about message passing between programs

- MCP by itself is a protocol. MCP server is an API

- Yes, but also no. If you try to turn your existing REST API into MCP, you will end up wasting lots of tokens and achieving nothing

- Everything is just like an API.

- ## ⚖️ Introducing Agent File (.af) - an open file format for importing/exporting agents.
- https://x.com/Letta_AI/status/1907477696499843121
  - With .af, you can reproduce an agent (with the same behavior and memories) without any setup or scripts: simply load the .af into your Letta server or Letta Desktop
- portable agents!

- ## Cline有MCP，Cursor有MCP，CherryStudio有MCP，不会造成很多MCP工具重复下载安装吗？ 怎样才能把它们整合在一起管理？就像OneAPI管理各家各源的LLM API一样。
- https://x.com/Yayoi_no_yume/status/1913948678534169008
- 是的你发现了盲点，所以有些解决MCP工具安装、治理、安全的平台
http://gatewaymcp.com
- 对于你本地而言， 你可以复用它们（安装到相同位置

- 可以复用的，安装在同一个位置，然后软件里面设置指向同一个位置即可。

- ## Isn’t MCP literally an API for APIs. Like it’s literally an API standard for AI to talk to other APIs right?
- https://x.com/bikatr7/status/1898184652038230372
- It's not revolutionary or earth shattering, but it is an attempt to prevent having a million different ways to integrate LLMs with APIs, databases, file directories, or whatever resources. Then *any* LLM that supports the standard will just work with MCP standards built once

- The difference is that the LLM is deciding which MCPs should be invoked with what arguments. Effectively giving the LLM dynamic logic, breaking it out of its static knowledge set (weights)

- ## Windsurf 出了一个视频教程，介绍了 MCP 的价值与案例
- https://x.com/op7418/status/1892056272381542405

- https://x.com/windsurf_ai/status/1891664001941037123
