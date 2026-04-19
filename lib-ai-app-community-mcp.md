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

- ## 

- ## Google Chrome 正式推出浏览器中的 Skills 功能
- https://x.com/shao__meng/status/2044259225610924222
  - 用户在 Gemini in Chrome 聊天中输入过一次的高频 Prompt，可以直接从聊天历史“保存”为 Skill。以后不需要重复输入，只用在浏览器侧边栏 Gemini 界面中键入“/”或点击“+”按钮，就可以一键调用。
  - 同时上线官方 Skills 库，包含一系列预置模板（如 “Protein maximizer 蛋白质最大化器” “Gift concierge 礼物管家” ），用户可直接保存并自定义修改提示词。

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

- ## [CLI 替代 MCP 的技术实践分析以及好用的CLI+Skill分享 - LINUX DO _202604](https://linux.do/t/topic/1907405)
- MCP（Model Context Protocol）本质上是把工具调用标准化成 JSON Schema + RPC 式的协议。早期（2024-2025 年）被很多 Agent 框架采用，看起来规范、类型安全。但实际运行中暴露了几个硬伤：
  - 工具描述必须完整塞进上下文，导致 Token 占用膨胀（社区实测 4-32 倍不等）；
  - 模型每次规划都要重新解析 Schema，复杂任务时容易出现幻觉或参数错误；
  - 配置门槛高，小白容易在 Schema 编写和维护上翻车。
- CLI（Command Line Interface）则完全相反。它利用 Agent 天生对 Shell 命令的理解（训练数据里命令行内容占比极高），让模型直接生成可执行的 Shell 语句，通过 exec 类工具交给系统运行。优点是：
  - 上下文干净，按需加载 --help 或参考文档即可；
  - Token 效率高，链式操作（管道、脚本）更自然；
  - 调试直观，输出实时可见，失败后可直接在终端复现。
- 以下这些工具在 OpenClaw 中都有成熟的 bundled skills，安装后重启 gateway 或执行 openclaw skills reload 即可自动识别：
  - git：仓库克隆、提交、推送、分支管理等基础操作；
  - gh（GitHub CLI）：issues、PR、仓库列表、认证等；
  - pandoc：Markdown 与 DOCX、PDF、HTML 等格式转换；
  - jq：JSON 解析、过滤、格式化；
  - curl / wget：API 调用、文件下载；
  - docker / docker-compose：容器启动、镜像管理；
  - ffmpeg：音视频转码、剪辑；
  - npm / pnpm / yarn：Node.js 包管理；
  - 以及 ripgrep（rg）、fd、tar、unzip 等系统级搜索和压缩工具。
  - 这些工具的 Skill 描述由官方或社区维护，稳定性较高。实际使用时，只需在对话中明确说明“用 gh CLI 列出我的仓库”或“用 pandoc 把当前 README.md 转为 PDF”，Agent 就会自动调用。
- Claude Code 同样支持直接运行 Shell 命令，但机制上没有 OpenClaw 那样完善的自动检测 + bundled skills。它依赖内置的 run command 能力，简单任务可直接描述命令执行。但要达到稳定可用，通常需要补充一个简短的 Skill（或直接复用 OpenClaw 的 SKILL.md 文件，稍作修改放入 ~/.claude/skills/）。
- 个人当前做法是分层使用：OpenClaw 负责整体规划和多工具协调，Claude Code 专注精细的代码/文档编辑任务。两者都走 CLI 路线后，整体成功率比纯 MCP 高出不少。

- 提醒
  - 任何涉及 exec 的操作都建议保持审批机制，尤其 git push、rm、docker 等高风险命令；
  - 从 gh、pandoc、git、jq 这四个工具开始练手，够覆盖日常 80% 的文档和代码场景；
  - 需要扩展时再用 CLI-Anything 生成新 Skill，避免一开始就堆太多工具占用上下文；

- ## CLI 这波热点，是流量逻辑。因为 for agents 的述事成了硅谷的吹捧，同时确实有 agents 想通过 CLI 来调用工具，
- https://x.com/lifesinger/status/2035010592981852213
  - 于是传统工具们纷纷穿上新衣服，希望被调用，来获取流量或资本关注。
- 然而 CLI 化有很难解决的问题：
  1. 参数爆炸问题。GUI 的功能远胜 CLI，要压缩成 CLI 参数，只能疯狂做减法。能敢于做减法的，已经是有认知的老板。没认知的老板，只会强压团队：所有功能都必须 CLI 化。可悲的是，用户根本不这么想。比如用户会在 IM 里按照自己对传统工具的 GUI 用法来描述需求，结果 agent 会发现：CLI 只能骗用户，或调调最基础的功能，稍微复杂的，还得是 computer use. 可用户已经急躁得骂娘了。
  2. 更严重的问题上，CLI 化很难跑通商业模式。此处太敏感，省略一万字。
- 更好的解法，是别安装本地软件了，一切云端 API 化。Agent 也很擅长调用 API 的，而且很考验 API 的接口易用性和商业模式设计。越易用的 API，能有越多模型能调用成功。商业模式越好的 API，则越能更长久为用户提供性美价廉甚至免费的服务。
- 提供 API 最有经验的公司，就是 SaaS 公司。优秀 SaaS 公司最核心的资产，也是 API。并不是界面。
- Agent 时代， 需要 CLI，然而更需要的，是优秀的 API 型 SaaS 服务。

- 不矛盾，现在大部分cli就是api的入口

- 无脑瞎上CLI短期可能会搞到流量，但长期来看作用不大。但也能理解吧，不是所有公司都有 SaaS 化能力的。
  - 合理的架构应该是CLI作为入口，API承载商业化，GUI补充。三者有机结合

- cli一定程度上解决了api认证的问题，并且缓解了注意力的分散，cli的help也是天然的动态注入。我更愿意看作gui是把api封装成人类友好的交互，cli把api封装成agent有好的交互

- 这个前提是平台愿意做 API。现实是中国互联网大量平台根本不提供公开 API，或者 API极其残缺。这种情况下 CLI 不是退而求其次，而是唯一可行路径

- 也不是 我看 有人往 CLI 参数塞 JSON 了

- ## 做了一个 AI Native 的 CLI ，OpenCLI 可以对接所有的网站转换成 CLI
- https://x.com/jakevin7/status/2032936880115736883
  - https://github.com/jackwener/opencli
  - 操控 chrome 无风控风险，复用登录，CLI 化全部网站。 并且可以让龙虾/AI agent直接替你做想要的接口
  - 目前是 AI native 的 CLI ，也就是能够让 AI 直接去挖掘网站里存在的功能，或者你想要的功能，然后变成 CLI 的命令。把所有的网站全部变成CLI！让 AI Agent 和你的龙虾可以无缝接入所有的网站访问所有信息。
  - 目前 bilibili 里面的  favorite history feed search user-videos .... 等等，就是我告诉 AI agent，然后他实现的。
  - 根据你自己想要的功能随便定制化开发。实现了动态命令注册中心，随意组合实现各种命令。
  - 利用了 Playwright MCP bridge 插件，直接操作浏览器本身。直接操作你浏览器本身，无风控问题。
  - 利用（Accessibility Tree) 的处理逻辑提供了高效的 filter 能力，节约token。

- ## 当mcp来的时候，我们说mcp最终会死，因为mcp的模式是全量上下文，而不是渐进式披露结果
- https://x.com/yangyi/status/2032745539025129815
  - 但skill也不够本质，因为skill当前没有一种自我迭代的infra，它是个一次性的，它缺少目标奖励函数的输入
  - 如果skill无法自我持续迭代 改进 优化， 那么它就仍然还是一个中间态， 最终被吞噬 被封装
  - mcp死了, skill也快了，不过不重要，能用就好
  - 这就是事物发展过程必然经历的阶段

- 我看到新的 skill-creator 增加了一个自测、迭代的机制，但是还是需要人工要求去迭代，这个一定程度上是否可以解决持续迭代的问题
  - 还不够，它是依托一个外力在更新skill， 应该是这个东西本身就有元能力自主更新

- agent应该可以根据实际干活的过程和结果，自我迭代？纯文本改起来还是比较容易的？
- 感觉agent四要素都应该可以依照目标奖励函数持续迭代
  - LLM大脑
  - Prompt指令
  - Memory记忆
  - Tools工具

- ## Skill替代不了MCP。你觉得MCP垃圾，只是你不需要、不理解而已。它们解决的是两个不同层面的问题。
- https://x.com/huangyihe/status/2032722428103925960
- Skill擅长的：非确定性的知识交付
  - 提供最佳实践、代码示例、决策指南
  - 自适应上下文管理，LLM 按需取用
  - 灵活、轻量、易创建
- MCP擅长的：确定性的动作执行
  - 工具有严格的输入/输出Schema，调用结果可预测
  - 工具之间可以可靠地组合编排（Skill触发时机不确定，组合起来不稳定）
  - 有完整的SDK基础设施：测试、共享代码、持久连接、OAuth认证
  - 支持远程托管、跨宿主复用
- 用一句话概括：Skill是让Agent知道该做什么，而MCP是让Agent真正去执行。

- 替代不了。CLI要求Agent预先知道命令名。如果环境里有上千个工具，你不可能把所有命令都塞进Prompt。
  - 结合skill补充cli的manual不就行了，这个简单
- cli在服务端跑stateless鉴权可没有mcp好用

- mcp就是不够灵活…工具全部常驻context，然后只是一个api服务还需要单独搞个mcp服务部署。反观skills，api server不用重新开了，还有动态上下文，毕竟不用作为工具常驻context了。 但是复杂的类似那种需要agentic 反复调用的 mcp还是必要的吧，这一点我还没有尝试。

- ## [Perplexity drops MCP, Cloudflare explains why MCP tool calling doesn't work well for AI agents : r/mcp _202603](https://www.reddit.com/r/mcp/comments/1rrviz4/perplexity_drops_mcp_cloudflare_explains_why_mcp/)
  - Perplexity's CTO just said they're dropping MCP internally to go back to classic APIs and CLIs.
  - Cloudflare published a detailed article on why direct tool calling doesn't work well for AI agents (CodeMode). 
  - Every intermediate result passes back through the neural network just to be copied to the next call. It wastes tokens and slows everything down.
  - The alternative that Cloudflare, Anthropic, HuggingFace, and Pydantic are pushing: let the LLM write code that calls the tools.
  - Intermediate values stay in the code, they never pass back through the LLM.
  - MCP remains the tool discovery protocol. What changes is the last mile: instead of the LLM making tool calls one by one, it writes a code block that calls them all. Cloudflare does exactly this — their Code Mode consumes MCP servers and converts the schema into a TypeScript API.
  - As it happens, I was already working on adapting Monty and open sourcing a runtime for this on the TypeScript side: Zapcode — TS interpreter in Rust, sandboxed by default, 2µs cold start. It lets you safely execute LLM-generated code.
  - Code Mode = Cloudflare's integrated solution. You're on Workers, you plug in your MCP servers, it works. But you're locked into their infra and there's no suspend/resume (the V8 isolate runs everything at once).
  - Monty = the original. Pydantic laid down the concept: a subset interpreter in Rust, sandboxed, with snapshots. But it's for Python — if your agent stack is in TypeScript, it's no use to you.
  - Zapcode = Monty for TypeScript. Same architecture (parse → compile → VM → snapshot), same sandbox philosophy, but for JS/TS stacks. Suspend/resume lets you handle long-running tools (slow API calls, human validation) by serializing the VM state and resuming later, even in a different process.

- note: it’s impossible for a large language model to be properly trained on every single possible business domain. However, MCP allows for prompts, which is the closest thing to providing extra training data to a model so that it knows how to use the tool/resource for your MCP

- MCP standardizes auth on Oauth DCR. This is a way better auth experience than anything else (especially copy-pasting API keys which non-engineers will struggle with)

- ## [MCP Is up to 32× More Expensive Than CLI. : r/mcp _202603](https://www.reddit.com/r/mcp/comments/1rr31ee/mcp_is_up_to_32_more_expensive_than_cli/)
  - Scalekit published an MCP vs CLI report about their 75 benchmark runs to compare CLI and MCP for AI agent tasks.
  - CLI won on every efficiency metric: 10x to 32× cheaper, and 100% reliable versus MCP’s 72%.

- The benchmarks are not correct for what's currently available. Claude Code has tool search automatically now for MCPs making the tool schemas dynamic discovery, essentially making the costs the same as skills. And Codex's mcps are also dynamic discovery by default. Or you can use docker mcp gateway which has also made mcp tool schemas dynamic discovery for months now.
  - Even with tool search the token usage metrics are brutal, I've done a lot of benchmarking. Tool search isn't a magic bullet but I don't agree with scalekits's approach here either.

- tl; Dr: What they actually did was benchmarking (of questionable quality/accuracy) on the GitHub Copilot MCP Service vs the GitHub CLI. They then claimed those results apply to "MCP" (a protocol, not a service) in general and wrote a sensationalist headline about it.

- This is funny because it completely takes away from where MCP shines - multi-user multi-agent workflows.

- ## Google has shipped a CLI for Google Workspace (Drive, Gmail, Calendar, Sheets, Docs, …) Huge!
- https://x.com/rauchg/status/2029356560494018956
  - Written in Rust, distributed through npm & http://skills.sh
  - This is a very well implemented CLI. It's so thorough. It dynamically registers commands, it's designed for a browser-wielding agent to automate the setup steps, it can start a MCP daemon…
  - https://github.com/googleworkspace/cli /MIT/202603/rust
- i've been using the google workspace CLI (gog) through an openclaw skill for weeks — gmail, calendar, drive all from terminal. agent reads inbox, drafts responses, files things by label, checks calendar conflicts before scheduling.

- my openclaw agent reads gmail and manages calendar through a workspace CLI every day. once auth is cached, email is just another shell command to the agent — no SDK needed. distributing that setup as a skill means someone else skips the 2 hours of oauth config i spent.

- It still needs the user to create a project in cloud console, which is such a nofly zone for any nontechnical person. Such a brutal blocker - I hope they figure a way around that
  - I think he's considered this, not sure how this plays out specifically tho

- ## 看到大家纷纷把http api包装成cli给agent用，我有个疑问：为什么不是api文档+curl呢
- https://x.com/wong2__/status/2029381003614286311
- curl 要把所有的命令都展示一遍，参数说明一遍，skill 会很长。cli 可以按子命令通过 --help 渐进式展开。推荐我做的一个通用的 cli 工具，可以给任意的带 schema 发现功能的 api 提供 cli。
  - skill会很长，这个可以用references来解决

- 做个cli相当于再封装了一层。多一层逻辑空间，可以做更多提效的工作。

- cli更容易做端侧的聚合，也可以保存state。api是无状态的。
  - 也就是说cli是新的面向agent的application，容易进行认证、复杂交互、业务逻辑的抽象。写skills的时候也更加简短。你可以决策到底哪些内容是要暴露给agent的，哪些应该内涵到程序规则去。

- CLI 本身是 stateless 的，当任务复杂度提升时，核心问题就不再是工具调用，而是 state management 和 workflow orchestration

- CLI 工具可以封装非常多的 API，结合 help 命令来做指令的渐进式披露。 如果使用 HTTP 去 curl 的话，描述内容会非常多，其实还是有比较多的干扰信息的。所以 CLI 工具给 agent 使用是一个非常方便可靠的一个方案。

- 存量业务经常多个 http api 组合才能完成一个业务操作，cli（和 web ui）就是那个裱糊匠

- api doc + curl 才是标准模式，一行代码都不用写。 我现在都是先进到项目里，然后问codex： 现在客服的问题是XXXXX， 你帮我利用现有的API 找到最佳查询路径，如果无法查询请规划新的API，最后生成操作手册。 十分完美

- 我就是用的 api，另外还整了个 api 网关服务，解决鉴权和一些身份问题，可以使用统一的接口，比 cli 更灵活好用，ai 也能更自由的组合。

- skills实际上就是DSL换壳
  - 我对 Skill 的第一反应也是 DSL，只不过刚好它是自然语言 + 命令行

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

- ## 每个 MCP 都要在用户本地跑一个 Node 进程，内存占用不说，光是进程启动和通信的延迟就非常明显，这是设计的问题
- https://x.com/Jiaxi_Cui/status/2040800132073967631
  - 所以只有 Figma、工业软件这类本身就很重的大型应用，MCP 才有可能长期活下去。
  - 另一种思路是把 MCP 进程放到服务器上，虽然延迟还是会增加，但起码不污染用户本地环境。我通过这样的方案部署了 Remote MCP 的 Cerul， 单次请求延迟多了大概 200ms，高并发状态还容易报错
  - MCP 的核心优势在于调用稳定，适合参数复杂的服务。用 MCP 包装后，模型调用更可靠
  - 但如果参数简单，还是 Skill 更合适。

- CLI 目前其实也是局限的，CLI 现在操作大部分是单个操作，每次执行一个 command 用完就没了。 
  - CLI 对于service 形态的服务，实现起来感觉并不好。还是需要类似MCP的形态。就看以后怎么发展了

- 我曾经探索过 在 AI  agent 和操作的对象之间建立一个简单的观测和动词协议 并两者独立维护状态, 至少在保留 cli 的简洁性和 MCP 的状态性上得到同时提升

- ## [What's your "must-have" MCP server that you use daily? : r/mcp _202604](https://www.reddit.com/r/mcp/comments/1s94a85/whats_your_musthave_mcp_server_that_you_use_daily/)
- We have our documentation platform integrated via MCP: Claude or ChatGPT. You can ”talk” to it like it’s a team member: make edits, updates, add back links, ask about view metrics and more.
  - I have been doing this with Atlassian MCP for Confluence. I built a bunch of agents after reinforcing its context with the code for our product. It’s quite amazing how well it understands the code base and how concise it documented it. It’s pretty wild and a must have

- Serena, context 7, firecrawl, jcodemunch, jdocmunch

- ## [MCP’s biggest missing piece just got an open framework : r/mcp](https://www.reddit.com/r/mcp/comments/1rm6plf/mcps_biggest_missing_piece_just_got_an_open/)
  - If you've been building with MCP you've probably hit the same realization we did. It's incredible at connecting agents to real systems, but it has absolutely no concept of identity.
  - There's no way to say "This agent is acting on behalf of John from accounting, and John explicitly authorized it to book travel under $300." No way to blame and fire John.
  - The agent has access, so it acts. That's it. And honestly if you're prototyping or running stuff internally, fine. But the moment agents start booking travel, managing accounts, completing transactions on someone's behalf, that's a problem. You can't audit it. You can't scope it. You can't revoke it mid-action. OAuth, API keys, JWTs, all of these assume a human is on the other end. They weren't designed for an agent acting on behalf of someone else, which is a totally different trust model.
  - So... we've been working on MCP-I (Model Context Protocol, Identity) at Vouched to fill this gap, and it just officially got donated to the Decentralized Identity Foundation. Meaning it's now being stewarded under open governance by DIF's Trusted AI Agents Working Group instead of staying proprietary. That part matters a lot to me because the whole point is that this becomes a standard and not product lock-in.
  - We also built Agent Checkpoint (vouched.id/know-your-agent) which is the product layer that actually enforces this. It sits at the control plane between your services and inbound agent traffic, detects it, classifies by risk, and lets you define exactly what agents are allowed to do.

- authorization (what you're describing) is already part of oauth and token auth

- the delegation + revocation piece is the real unlock. without it you cannot do policy-based approvals at the MCP layer at all. peta (peta.io) is tackling a related piece -- vault + audit trail + policy enforcement as the control plane between services and agent traffic.

- ## 🤼 [MCP servers are the real game changer, not the model itself : r/ClaudeCode _202603](https://www.reddit.com/r/ClaudeCode/comments/1rm367e/mcp_servers_are_the_real_game_changer_not_the/)
  - Once I connected Claude Code to our internal tools (JIRA, deployment pipeline, monitoring dashboards) through MCP, the productivity jump was insane. Instead of copy-pasting context from 5 different browser tabs, Claude just pulls what it needs directly.
  - A few examples:
  - MCP server that reads our JIRA tickets and understands the full context of a task before I even explain it
  - One that queries our staging environment logs so Claude can debug production issues with real data
  - A simple one that manages git workflows with our team's conventions baked in
  - The model is smart, but the model + direct access to your actual tools is a completely different experience. If you're still just using Claude Code with the default tools, you're leaving a lot on the table.

- biggest unlock for me was building an MCP server that wraps macos accessibility + screen capture. the AI can literally see what's on screen and click things without me copy-pasting anything. went from "here's a screenshot, what do I do" to "just do it" overnight. the JIRA integration sounds great too — half my time used to be reading tickets and translating them into context for the model.

- True. I turned Claude off entirely and I don't even use LLMs anymore. I just connect manually to the mcp server and do the work myself because it's the real game changer. Made me work 1000x faster

- You don't need MCPs half the time. Claude Code can just use the AWS CLI and it can create scripts to interact with the JIRA API which, given the Atlassian MCP is so crap, is usually the better option.
  - MCPs are a reminder to keep your —help or openapi spec up to date and sound. In best case it’s a token/auth interface…

- I ditched MCP’s for Skills and never looked back. 

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
# discuss-ai-use-computer/container
- ## 

- ## 

- ## 

- ## 

- ## [OpenLobster – for those frustrated with OpenClaw's architecture : r/openclaw _202603](https://www.reddit.com/r/openclaw/comments/1rum56j/openlobster_for_those_frustrated_with_openclaws/)
- What OpenClaw got right:
  - Dead simple to deploy
  - Great concept (self-hosted AI agent)
  - Vibrant community (you're all awesome)
- What broke for us:
  - MEMORY.md conflicts when running multiple users
  - Scheduler reading a .md file every 30 minutes felt like a hack
  - MCP integration wasn't production-ready
  - 40K+ instances exposed (not your fault, just happened)
- The fork decision: We reviewed the codebase. These weren't bugs—they were architectural choices that made sense for a v0.1 PoC, but didn't scale.
  - We could patch it, or rebuild it right. We chose the latter.
- What's different in OpenLobster:
  - Neo4j graph database (proper memory system, not .md files)
  - Real multi-user support (RBAC per user per channel)
  - 200ms startup, 30MB RAM (vs ~3s, 150MB+)
  - Encrypted secrets backend
  - Task scheduler with cron + ISO 8601
- Same philosophy:
  - Self-hosted (your data, your infra)
  - GPL-3.0 (forever open)
  - Supports Telegram, Discord, Slack, WhatsApp, SMS
  - Any LLM provider
- This is the guide for migrating from OpenClaw 

- Claude code with auto mode is the better claw

- ## [How I taught an AI to use a computer _202501](https://e2b.dev/blog/how-i-taught-an-ai-to-use-a-computer)
- 
- 
- 

# discuss-ai-use-browser
- ## 

- ## 

- ## 

- ## 

- ## Browser Use 团队开源发布「Browser Harness ♞」：让 LLM 获得对浏览器的完全控制自由，且具备自我进化能力
- https://x.com/shao__meng/status/2045657138119549006
  - Browser Harness 是一个极简的 Chrome DevTools Protocol 桥梁——仅用约 592 行 Python，构建了一个 LLM 直接操作真实浏览器的最小化 harness。
  - 传统浏览器自动化工具（如 Selenium、Playwright、甚至 browser-use 本体）往往预设了人类的操作逻辑：封装点击、填写、等待等 API，让开发者按剧本编排流程。
  - 而 browser-harness 走了一条相反的路：
  - 不封装能力：只提供一个 websocket 连接到 Chrome，LLM 直接发送 CDP 命令
  - 不预设流程：没有"等待元素→点击→输入"这类剧本，LLM 自己决定如何与页面交互
  - 无中间层：只有一个薄层把 LLM 的输出翻译成浏览器能理解的协议
  - 自修复机制（Self-healing）-- 独特创新点 项目包含一个 helpers. py，里面存放了一些基础的浏览器操作函数。但关键在于：这个文件不是给人类维护的，而是给 LLM 自己维护的。

- 这个其实和现在基于 file system 的 agentic search 的理念有点类似: 给予 ai 合适的自由，反而能更快找到目标的路径

- ## Browser Use 在 Online-Mind2Web 取得 97% 的最高成绩，团队采用了 Karpathy 的 Auto-Research 方案
- https://x.com/shao__meng/status/2036978751834042524
1. Browser Agent 框架升级为 Coding Agent
传统 Browser Agent 仅依赖有限的工具（如 click、type、scroll），在数据提取和边缘场景中极易卡住。Browser Use 的核心创新是将 Agent 框架升级为 Coding Agent：
· Claude Code 直接改造了 Browser Agent 的 harness，新增 Python 代码执行能力。
· Agent 不再局限于预定义动作，而是可以实时编写并执行 Python 代码，直接在浏览器上下文中解析 HTML、提取结构化数据。

1. 基础设施优化：最隐蔽浏览器环境 + 真实用户日常任务训练信号
单纯算法优化不够，Browser Use 同步对底层执行环境进行了极致打磨：
· 最隐蔽的浏览器基础设施：他们从真实生产数据构建了一个专属的 stealth benchmark，对市面上所有主流云浏览器进行全面测试，最终选用了隐蔽性最强的方案。
· 真实用户日常任务作为训练信号：每天将 power users 在生产环境中提出的新任务和修复需求，直接纳入 Auto-Research 循环的训练/优化信号。

1. 评判器升级：从截图 Judge 到基于 Claude Agent SDK 的 Agentic Judge
整个 Auto-Research 闭环能够高效运转的最关键一环。
· 传统截图 Judge 的失效：早期评测依赖截图比对，但新一代代理大量使用代码执行、API 调用、提取数千条数据，这些行为在截图中完全不可见或被误判为“幻觉”。
· 新 Agentic Judge：完全基于 Claude Agent SDK 重新构建，让 Judge 本身也成为一个具备 agentic 能力的智能体。
· 对齐机制：通过精心设计，已与人类专家评判高度一致。

- 这三项与 Auto-Research 形成闭环：
· Coding Agent 提供探索空间；
· 隐蔽基础设施 + 真实任务提供高质量信号；
· Agentic Judge 提供可靠评估。

- Auto-Research这个思路厉害 让agent自己跑eval循环改进产品 比人手动调参数快太多

- ## 🎯 Introducing: Browser Use CLI 2.0
- https://x.com/browser_use/status/2035081807209931153
  - 2x the speed, half the cost (compared to other browser automation CLIs)
  - Easily connect to running Chrome
  - Uses direct CDP
- Popular use cases:
  - Form filling
  - QA/Pentesting
  - General web automation

- Is this opensource?
  - yes

- Direct CDP is powerful, but maintaining those selectors is the real bottleneck.

- direct CDP is the right call been burned by playwright overhead way too many times. does the 2x speed hold when youre running multiple concurrent sessions?
  - yes

- The Claude Chrome extension is free to use with Claude CLI. Honest question: what does this improve over that setup?
  - Don’t need to install a Chrome extension
  - Can be used with any CLI agent
  - Fast and token efficient

- can it run headless and do the same thing as this video demo?
  - Yes

- what's the difference between this and agent-browser?
  - 2x the speed for half of the cost with half of the commands

- 那本地都能做了，它家的 cloud 服务可以做什么？
  - Cloud gives you access to our agent-ready browsers and browser subagents
  - Massive parallelization

- https://github.com/ulpi-io/benchmark-browse-vs-agent-browser-vs-browser-use
  - Benchmark: browse vs agent-browser vs browser-use
  - It's definitely a bit better than agent-browser, but would't say it's the "fastest" or the most token efficient. 

- btw you can do this with chrome Dev MCP too with any cli/browser/client https://github.com/ychampion/chrome-for-agents

- https://x.com/shao__meng/status/2035163988674454017
- Browser Use CLI 2.0 发布
- 新版本采用持久化后台守护进程架构，每条命令通过 Unix socket（或 Windows TCP）通信，响应延迟低至约 50ms。
- 这与传统 Playwright 等框架形成鲜明对比——后者往往因抽象层导致启动慢、token 浪费和状态不稳定。
- 无需 Chrome 扩展，即可与任何 CLI Agent 无缝集成，尤其擅长表单填写、数据提取等复杂交互。

- 支持三种浏览器模式：
  - 本地托管无头 Chromium
  - 连接真实 Chrome（含现有登录与扩展）
  - 云浏览器（可选，通过 Cloud API）

- https://x.com/sitinme/status/2035944377336439098
- 以前你让 AI 帮你点网页，基本就三条路：要么看截图瞎猜，要么上 MCP 背一堆工具描述，要么老老实实写 Playwright/Python 脚本。不是不能做，但都很别扭。
- Browser Use CLI 2.0 把这件事一下拉回到一个很顺手的状态：AI 直接在命令行里调浏览器，跟执行 ls、git 一样自然。这个体验上的变化，我觉得比“多了一个功能”重要得多。
- 它不是靠截图让模型“看图猜按钮”，也不是把整页 HTML 一股脑塞给模型，而是把页面翻译成一份精简、可操作的元素清单。按钮、输入框、链接，全都编号
- 现在如果能直接复用你本机 Chrome 的账号状态，那很多原来“理论可自动化、实际上懒得做”的事，就真的能交给 AI 去跑了。

- 一直在用browser-use 2.0确实是质的飞跃 之前截图识别太慢了 现在DOM直接操作 配合Claude Code的skill系统 浏览器自动化终于不再是玩具了

- ## WebMCP 反过来：让网页应用主动告诉 AI「我能做什么」，AI 直接调用。不用模拟键鼠，不用找 DOM，一步到位。
- https://x.com/runes_leo/status/2033479932601565464
- DOM 选择器脆弱性太高。WebMCP 这种声明式 API 的方向确实更稳定，对 AI 更友好——直接告诉它"我有哪些能力"，比让它去猜测

- ## PageAgent AI 可以直接操作网页。
- https://x.com/IndieDevHailey/status/2032428337877205254
  - 它最打动我的一点是：把最烦人的数据录入干掉了。
  - 很多公司每天都在做这种重复工作： 复制数据 → 打开系统 → 填表 → 提交
  - 以后可能只需要一句话：“帮我填写客户信息。” AI 就会自动识别网页结构，把整个流程全部做完。
- 几个非常实用的场景：
1. 自动填写网页
CRM 表单、注册表单、订单系统
直接让 AI 帮你把网页表单填好。
1. AI 网站助手（Web Copilot）
用户可以直接说：
- 帮我找订单
- 生成报表
- 搜索商品
AI 自动在后台页面完成操作。
1. 企业系统自动化
ERP、CMS、内部管理系统
AI 可以直接操作后台 UI，把复杂流程自动化。
1. 无障碍辅助
语音 → 操作网页
用户说话就能完成网页操作。
- 和很多 Agent 不一样的是，它 不靠截图识别界面，而是直接读取 HTML DOM，所以：
  - 更快
  - 更稳定
  - 成本更低
- 而且整个系统 直接运行在浏览器里，不需要：
  - Puppeteer
  - Playwright
  - Python 自动化
- 这东西直接读DOM真的稳多了，我之前用截图Agent搞内部系统老是卡，换这种方式应该能省一大堆时间。 独立开发者做自动化工具的话，这个方向现在超有搞头。

- 试过了，速度奇慢无比，体验太差了

- 解析Dom运行js一定是慢到爆的那种体验

- ## 新产品@dokobot正式上线
- https://x.com/supezen/status/2032824859227771011
  - AI agent 读网页这个难题，现有方案各有各的缺陷：
  - Jina Reader / Firecrawl：转 Markdown 不错，但过不了 Cloudflare 反爬，登录页也读不了
  - Browserbase / Steel 这类云浏览器：能渲染 JS，但读不了你登录过的 Gmail 和 Notion，输出还是原始 HTML
  - Agent-browser / Chrome CDP 方案：权限太大，能注入脚本、读 cookie、操控 DOM，安全隐患多
  - Dokobot 在 Chrome CDP 基础上增加一层，让 Agent 可以高效且安全的通过你的浏览器来读网页，试图彻底解决这个难题。
  - Dokobot 利用 CDP 和 Treewalker 技术预处理好页面内容，提供一条安全的通道供 agent 随时查询，避免 agent 直接操作 CDP 注入动态脚本带来安全隐患。
  - 总之你登录了什么它就能读什么，反爬天然免疫，被网站屏蔽的风险也最低，同时输出 AI 可直接消费的 Markdown，最多可节省 99% token。

- 痛点太真实了，我跑 browser automation 也踩过一模一样的坑。最后走的本地 Chrome + CDP 路线才算稳定。好奇 dokobot 的架构是怎么处理登录态同步的？是 browser extension 还是有别的方案？
  - 是的，基于浏览器插件

- Treewalker + CDP 这个组合有点意思。本地预处理再让 agent 查询，确实比直接暴露 CDP 安全很多。好奇 token 节省 99% 这个数字是怎么测的？是对比直接用原始 HTML 还是对比 Jina Reader 这类方案？
  - 原始HTML，如果已经是markdown就差不多了

- 可以cloud用吗？ 还是不许是local才可以用？
  - 可以远程访问，龙虾在云端也可以

- 如果网页需要一定交互才能显示需要的内容..  但是网址都没变 能获取么
  - 交互的方式太多了，暂时不支持。

- ## bb-browser，badboy browser，可以用 bb-browser site 的方式直接拉到任何网站的信息，
- https://x.com/yan5xu/status/2032858943874281782
  - 目前支持 Reddit、Twitter、GitHub、Hacker News、小红书、知乎、B站、微博、豆瓣、YouTube，50+ 个命令，我会持续更新。
  - 当然能做到信息获取这件事不稀奇，我也是看到 @jakevin7 的 twitter-cli 的启发，才做的。
  - 但 bb-browser 的实现方式非常丧良心 — 我是通过 Chrome 插件 + CDP 直接操控你真实的浏览器。不是无头浏览器，不是偷 Cookie，不是模拟请求。你已登录了，它就直接用你的登录态。它直接在浏览器 console 里面跑 eval，以前爬虫最麻烦的登录态、还有各种鉴权都没有了。（这种方式真的。。。太作弊了，我都能想到哪些大厂前端发现我在这么搞，会怎么骂我，因为真的很难防）
  - 另外我还在命令行里面埋了 guide 命令，也就是说你只要装了 bb-browser CLI 或 MCP，跟你的 Agent 说"我需要把 XX 网站 CLI 化"，它就能帮你做了！！
  - 真的，大家去看看 repo 里面每一个网站 api 的代码只有几十行，就能把网站逆向出来
  - 强调一下！！在 guide 命令指导下，基本 10 分钟就可以把一个网站转成 cli！！强烈建议把自己的网站 cli 化！
  - 架构对了，转化真的。。。非常快，bb-browser site已经添加了 35 个网站，97 个命令

- 以前的爬虫为啥不这样做

- 我以前也这样爬内容 但是问题是频率 要封号呢

- 这个实现很狠但很实用。我以前也试过用 CDP 借登录态，省掉鉴权地狱，但权限边界要想清楚。

- 我写的twitter extension也是一样的. 不过没你们这么适配 因为这个就是成本最低、最自然的方案

- ## Chrome 最新146版本正式加入了WebMCP支持，也就是你的任何Web网站/应用都可以以MCP形式对外提供功能服务。
- https://x.com/nash_su/status/2033053457733853394
  - 这个意义很大，当越来越多人用AI帮助干活，当你的Web网站有MCP支持的时候，AI不再需要复杂的模拟点击->截屏->分析->操作这样复杂的工作，而是直接用你标准化的MCP接口进行快速调用。

- 基本上所有的互联网公司靠广告活着，使用mcp的话这些公司会失去很多经济来源，他们大概率不会主动去断臂吧
  - 这不是由他们决定的，百度能不让大家用问AI取代搜索吗？大趋势如此

- 怎么诱使用户买入更多额外服务 获利
  - 那是另一个问题，可以诱导AI一定要下单额外服务

- ## Chrome最新版146 终于可以方便的让agent操控当前浏览器了（之前要么启动一个单独的Chrome实例，要么安装第三方浏览器扩展来实现）。
- https://x.com/wong2__/status/2032697322451382324
  - 1. 打开 chrome://inspect/#remote-debugging 开启 Remote debugging
  - 2. 安装 agent-browser skill 或 chrome-devtools-mcp，都支持自动连接到已有的Chrome实例
- 这个 144 就支持了，用了好久了
  - mac的145好像还有问题，146可用了

- 终于不用 headless 绕一圈了，agent 直接寄生在你日常浏览器里，细思极恐

- 用的时候还是需要手动确认一下，不太适合纯远程
- 还是会弹一个对话框要求同意。

- 这个权限太大了，而且非常费token，我做了一个只允许读取网页的产品，网页输出 markdown 

- 以后端到端可以直接用9222端口

- ## [Anyone moved off browser-use for production web scraping/navigation? Looking for alternatives : r/LangChain _202603](https://www.reddit.com/r/LangChain/comments/1rm5lx8/anyone_moved_off_browseruse_for_production_web/)
  - Been using browser-use for a few months now for a project where we need to navigate a bunch of different websites, search for specific documents, and pull back content (mix of PDFs and on-page text). Think like ~100+ different sites, each with their own quirks, some have search boxes, some have dropdown menus you need to browse through, some need JS workarounds just to submit a form.
- It works, but honestly it's been a pain in the ass. The main issues:
  - Slow as hell. Each site takes 3-5 minutes because the agent does like 25-30 steps, one LLM call per step. Screenshot, think, do one click, repeat. For what's ultimately "go to URL, search for X, click the right result, grab the text."
  - Insane token burn. We're sending full DOM/screenshots to the LLM on every single step. Adds up fast.
  - We had to build a whole prompt engineering framework around it. Each site has its own behavior config with custom instructions, JS code snippets, navigation patterns etc. The amount of code we wrote just to babysit the agent into doing the right thing is embarrassing. Feels like we're fighting the tool instead of using it.
  - Fragile. The agent still goes off the rails randomly. Gets stuck on disclaimers, clicks the wrong result, times out on PDF pages.
- What I actually need is something where I can say "go here, search for this, click the best result, extract the text" in like 4-5 targeted calls instead of hoping a 30-step autonomous loop figures it out. Basically I want to control the flow but let AI handle the fuzzy parts (finding the right element on the page).
- Has anyone switched from browser-use to something else and been happy with it? I've been looking at:
  - Stagehand: the act/extract/observe primitives look exactly like what I want. Anyone using the Python SDK in production? How's the local mode?
  - Skyvern: looks solid but AGPL license is a dealbreaker for us
  - AgentQL: seems more like a query layer than a full solution, and it's API-only?
  - Or is the real answer to just write Playwright scripts per site and stop trying to make AI do the navigation? Would love to hear what's actually working for people at scale.

- I can’t imagine using llms for browsing. I just write and directed a bunch of playwright python to open and browse and scrape sites. Occasionally they break and I go and fix them.
  - You can use llms to write and update the script and then run it.

- We ran into the same problem. The autonomous browser agent loop (screenshot -> DOM -> LLM -> one click -> repeat) looks great in demos but is painful in production. It’s slow, expensive, and hard to control. You end up writing a ton of prompt scaffolding just to keep the agent on track.
  - What worked better for us was flipping the model to have deterministic control flow and small AI calls only where ambiguity exists.
  - We’ve been building an open-source project around this idea called Actionbook and a skill called extract. It's basically reusable “actions” for agents so you don’t have to write site-specific prompt logic everywhere. Curious what kind of sites you’re scraping, gov portals, filings, etc.

- The answer is kind of both. Playwright scripts for the deterministic flow (go to URL, click search, type query) and LLM calls only for the fuzzy bits like picking the right result or extracting structured data from messy pages. That takes you from 25-30 LLM calls down to 2-3 per site.
  - Stagehand's act/extract/observe primitives are designed for exactly this split.

- Yeah, the “autonomous browser agent” thing sounds great on paper, but once you’re at 100+ sites, you’re basically debugging a very slow intern every run.
  - What’s worked best for me is leaning into boring determinism and using AI only where humans would squint. I use Playwright as the backbone and define per-site flows as small, explicit scripts: go_to(url), maybe_login(), run_search(query), open_top_result(), extract(). All timing, retries, JS hacks, and PDF handling live there, not in the model.
  - Then I let the LLM handle the fuzzy selectors and heuristics in tight loops: given a DOM snapshot or a constrained element list, pick the search box, pick the best result row, decide if a page “looks like” the target doc. That’s 2–4 calls per site, not 30.
  - Key tricks: pre-normalize pages (kill popups/consent banners with hard-coded selectors), cache per-site strategies, and log HTML + chosen selectors so you can quickly patch a site when it changes instead of retraining prompts. Over time the AI part shrinks and the stable Playwright layer does most of the work.

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
# discuss-protocols-lacking
- ## 

- ## 

- ## 

- ## 

- ## If you are using MCP to access your data, you are trusting that third party with unencrypted access to your data.
- https://x.com/kepano/status/2033195271220597215
  - Third-party MCPs are not an option if you value privacy. 
  - End-to-end encryption makes MCP effectively useless.
  - Obsidian Sync is end-to-end encrypted. An MCP for it would be useless. Unless you mean a local MCP in which case why not use the CLI?

- Yeah, I wrote an article about exactly that. To work with MCP securely, you need to implement a real client and an orchestrator that you own, but it's not easy because no one explains how. They push you toward their “clients.” I built a vanilla MCP orchestrator client from scratch and figured it out.

- ## 最近终于各大公司都开始说mcp没啥用了。奇怪的是这个事情竟然过了一年才被广泛承认，有基本软件工程知识和架构经验，第一天就应该知道它是错误的设计。
- https://x.com/virushuo/status/2032432024506474991
  - 可以回头看看我一年前发的这条，并无挖旧账的意思，但是看看当时大家的讨论可以避免下一次掉进无谓的热概念中。
- 可是这并没有被广泛认同，也有很多支持 MCP 的声音。

- mcp仍然有用。只是目前加强了对于cli、管道、渐进式披露的认识。openclaw内置小工具mcporter就是其中有意思的代表。

- mcp最终和llm集成的时候也还是把工具的schema放请求里，怎么看都只是把openapi重新发明了一遍。
  - 后来思路变了，提供执行cli的元工具bash，再追加cli怎么用的信息，这就是skill了
  - 暴论一下，我看厂商也别训练基于json schema的tool call ，直接训练xml标签包裹cli调用得了，还省点转义字符的token

- 完全同意这个多余的设计没啥用，我觉得本质上是系统集成 + 协议设计的事情，传统软件领域解决过无数次这类问题，标准软件工程领域的事情非要套一个AI的理念强行AI，各个底层基础都有具体固定的开放协议和文档，搞成什么包一层全新的AI标准协议。

- https://x.com/Jiaxi_Cui/status/2032394929448874078
  - skill 和 MCP 是不同的，MCP太繁琐了，要这要那的，哪怕对于开发者来说也很不友好。但是 skill 不仅友好，而且有用
  - 目前最大的问题只是如何让 skill 的贡献者赚到钱，这个商业模式应该是怎样的，这个生态才可能持续下去
- 基本不可能，别人一复刻就完了，比如腾讯 skill hub

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

- ## New @code version 1.116 is out  _202604
- https://x.com/OrenMe/status/2044637007108850040
  - The Agents app is now officially available in the Stable release. It’s fully powered by the CLI as its agentic engine, which is a pretty major shift
  - We’ve been in a relatively long phase without obvious, visible leaps, but under the hood there’s serious groundwork being laid for the Agents app and the Agent Host protocol

- The Agent Host protocol is the real story here. Multi-agent coordination inside the IDE could fundamentally change how we think about tool approval surfaces and security boundaries for agentic workflows.

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

- ## 

- ## [Skill 开发踩坑：相对路径解析问题 - LINUX DO _202604](https://linux.do/t/topic/1894042)
  - Claude Code 和 Qoder Cli 中，Skill 无法感知自身目录，导致 Skill 脚本的第一次调用都会出错，然后才会搜索正确目录，影响 scripts/ 和 reference/ 的使用。
  - 不管 Skill 在用户级目录 (~/.agents/skills/xxx/scripts) 还是项目目录都会出现问题。
  - 解决思路: 在 Skill 调用时，注入 Skill 目录的绝对路径，如 “Base directory for this skill: /xxx/xxx/”。 注入方法通过 PreToolUse Hook 实现。

- ## Introducing @tan_stack Intent (alpha) _202603
- https://x.com/tan_stack/status/2029973163455766769
  - Ship agent-readable "skills" inside npm packages
  - Composable - mix core + framework-specific skills
  - Oh, and if you're a maintainer of a library, we ship *skills* for you to: - Generate skills - Audit skills - Get feedback on skills from users (using skills of course)
  - And you can automate all of this via CI

- This is very dangerous to automatically discover and use skills from node_modules because malicious package might easily compromise your machine. Sooner or later it will be blocked.
  - Aren’t you already vulnerable to prompt injection any time an agentic coding tool reads files from dependencies into its context?
- package management distribution risks have been a thing for a long time before this. The way we see it, it's better to bet on the security and provenance of an already established (and continually improving) mode of distribution (NPM) instead of inventing yet another one.
- Yeah, I don't think this is a new surface area. This should already be a concern. If a package is malicious, it can attack in multiple ways. Same as always.
  - Maybe with bun/pnpm or in our cli we could add a filter or safeguard to only use on packages with provenance or something like that.

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
# discuss-examples 🌰
- ## 

- ## 

- ## 

- ## [MCP Manager: Tool filtering, MCP-as-CLI, One-Click Installs : r/mcp _202603](https://www.reddit.com/r/mcp/comments/1rtwip7/mcp_manager_tool_filtering_mcpascli_oneclick/)
  - I built a rust-based MCP manager that provides: HTTP/stdio-to-stdio MCP server proxying
  - Tool filtering for context poisoning reduction
- OAuth tokens stored plaintext in SQLite: Access tokens, refresh tokens, and even client_secret are serialized as plain JSON into SQLite. The vault only protects API keys. Long-lived refresh tokens for GitHub etc. are sitting unencrypted on disk.
  - Access tokens, refresh tokens, and client secrets are now stored in the encrypted Stronghold vault alongside API keys. SQLite retains only non-sensitive metadata (token type, expiration timestamp, client ID, scopes, endpoint URLs) — just enough for the UI to show connection status and expiry without touching the vault.

- ## 百度把PaddleOCR-VL-1.5做成OpenClaw Skills了，也上架到ClawHub了，配置好后就可以直接解析文档了。
- https://x.com/aiwarts/status/2032685663418568704
  - 每天有解析几万页数的文档额度，应该是目前唯一免费高精度读PDF的Skill。

# discuss
- ## 

- ## 

- ## 

- ## 

- ## [I genuinely don’t understand the value of MCPs : r/mcp _202603](https://www.reddit.com/r/mcp/comments/1rw7z6l/i_genuinely_dont_understand_the_value_of_mcps/)
  - When MCP first came out I was excited. I read the docs immediately, built a quick test server, and even made a simple weather MCP that returned the temperature in New York. At the time it felt like the future — agents connecting to tools through a standardized interface.
  - Wait… I could have just called the API directly.
  - A simple curl request or a short script would have done the exact same thing with far less setup. Even a plain .md file explaining which endpoints to call and when would have worked.
  - As I started installing more MCP servers — GitHub, file tools, etc. — the situation felt worse.
  - Why not just tell the agent to use the GitHub CLI? It’s documented, reliable, and already optimized.
  - Skills are basically structured .md instructions with tooling around them. When I saw that, it almost felt like Anthropic realized the same thing: sometimes plain instructions are enough.
  - But Anthropic still insists that MCP is better for external data access, while Skills are meant for local, specialized tasks.
  - Why is MCP inherently better for calling APIs? From my perspective, whether it’s an MCP server, a Skill using WebFetch/Playwright, or just instructions to call an API — the model is still executing code through a tool.

- Think of an MCP like a pre-defined set of instructions for HOW an AI calls APIs or other tools. 
  - It's a structured way for AI to see what's available and easily see what params are needed to call an API and it guarantees that it's executed the same way every time.
  - MCP also allows you to control what's returned to the agent so you can be more context aware.
  - MCP also provides authentication layers for AI to be able to access and read/write from databases. Otherwise, you'll have to expose your database credentials to AI to tell them to read/write from a database. MCP is that middle layer that provides auth and a structured, guaranteed way to access databases without letting AI hallucinate what fields they should fill out.

- There’s a few reasons to use MCP over skills. Security is probably the biggest one

- there are good reasons to not always allow these powerful and potentially dangerous capabilities and might better only configure tools to access exactly what you need. 

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
