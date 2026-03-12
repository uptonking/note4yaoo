---
title: lib-ai-app-examples-utils-protocol-mcp
tags: [agent-client-protocol, agent-skills, ai, large-language-model, mcp]
created: 2026-01-19T04:59:51.283Z
modified: 2026-01-19T05:01:00.055Z
---

# lib-ai-app-examples-utils-protocol-mcp

# guide

- tips-mcp
  - mcp的文档内容太多, 可尝试用对应的cli工具替换api工具
# mcp
- https://github.com/upstash/context7 /34kStar/MIT/202510/ts
  - https://context7.com/
  - Context7 MCP - Up-to-date Code Docs For Any Prompt
  - Context7 MCP pulls up-to-date, version-specific documentation and code examples straight from the source — and places them directly into your prompt.
  - Add `use context7` to your prompt (or set up a rule to auto-invoke)
    - To avoid typing `use context7` in every prompt, add a rule to your MCP client to automatically invoke Context7 for code-related questions
    - Claude Code: CLAUDE.md
    - Cursor: Cursor Settings > Rules
  - require Context7 API Key (Optional) for higher rate limits and private repositories 
  - This repository hosts the MCP server’s source code. The supporting components — API backend, parsing engine, and crawling engine — are private and not part of this repository.
  - [Feature Request: Option to Self-Host Documentation Backend _202504](https://github.com/upstash/context7/issues/59)
    - interesting idea. I will think about this. the biggest obstacle would be licensing. we aim to make this service free for developers and open source projects. but we want to commercialize if a company like cursor needs it.
    - but we can keep parser private and web backend open.
    - maybe you can store all the docs in a public database, that way anyone can self-host.
    - Another option is to allow companies to host their documentation on context7's servers privately, and support authentication.
- https://github.com/vercel-labs/opensrc /apache2/202601/ts
  - Fetch source code for npm packages to give AI coding agents deeper context
  - opensrc automates the process of fetching package source code so your agent can reference it when needed.
  - https://x.com/hyojun_at/status/2025602999994011746
    - i found codesearch is more practically useful than docs search in these days
    - context7 vectorizing docs - not all libs and tools out there are open sourced, sometimes all they provide us with are simple docs.
    - Most AI tools are already capable of going into the `node_modules` folder and read the source code.
    - Docs are for humans, source code is for AIs.
    - everybody uses only npm packages in their projects ? (maven?)
    - what u think about deepwiki

- https://github.com/czlonkowski/n8n-mcp /MIT/202602/ts
  - https://www.n8n-mcp.com/
  - A MCP for Claude Desktop / Claude Code / Windsurf / Cursor to build n8n workflows for you
  - For the best results when using n8n-MCP with Claude Projects, use these enhanced system instructions

- https://github.com/jlowin/fastmcp /MIT/202503/python
  - https://github.com/modelcontextprotocol/python-sdk
  - The fast, Pythonic way to build Model Context Protocol servers
  - 依赖pydantic2、httpx
  - You can now find FastMCP as part of the official Model Context Protocol Python SDK
    - this repository is no longer maintained.

- https://github.com/AIDC-AI/Pixelle-MCP /271Star/MIT/202508/python
  - https://pixelle.ai/
  - Open-Source Multimodal AIGC Solution based on ComfyUI + MCP + LLM
  - An AIGC solution based on the MCP protocol, seamlessly converting ComfyUI workflows into MCP tools
  - Server-side is built on ComfyUI, inheriting all capabilities from the open ComfyUI ecosystem
  - MCP Server provides functionality based on the MCP protocol, supporting integration with any MCP client (including but not limited to Cursor, Claude Desktop, etc.)
  - MCP Client is developed based on the `Chainlit` framework, inheriting Chainlit's UI controls
  - Integrated the LiteLLM framework, adding multi-model support for Gemini, DeepSeek, Claude, Qwen, and more
  - Flexible Deployment: Supports standalone deployment of Server-side only as MCP Server, or standalone deployment of Client-side only as MCP Client, or combined deployment
  - Unified Configuration: Uses YAML configuration scheme, one config file manages all services
  - https://github.com/Chainlit/chainlit /10.5kStar/apache2/202508/python/ts
    - https://docs.chainlit.io/
    - Build python production-ready conversational AI applications in minutes
    - As of May 1st 2025, the original Chainlit team has stepped back from active development.
    - 依赖langchain、LlamaIndex、ChromaDB

- https://github.com/mark3labs/mcp-filesystem-server /go
  - Go server implementing Model Context Protocol (MCP) for filesystem operations.
  - 通过这个MCP就可以操作本地文件系统了，由于这个是go编写的，go能交叉编译的架构特别多，所以理论上大部分系统都能运行这个MCP Server。

- https://github.com/mcpc-tech/mcpc /MIT/202510/ts
  - https://mcpc.tech/
  - MCPC is the SDK for building agentic MCP (Model Context Protocol) Servers.
  - Build Multi-Agent Systems: By defining each agent as a MCP tool, you can compose and orchestrate them to construct sophisticated, collaborative multi-agent systems
  - Compose MCP servers as building blocks, select and customize tools, or modify their descriptions and parameters
  - Logging and tracing: Built-in MCP logging and OpenTelemetry tracing support
  - https://github.com/mcpc-tech/ai-elements-remix-template /MIT/202510/ts
    - https://ai-elements-remix-template.pages.dev/
    - A modern chat interface template built with AI SDK and customizable UI components.
    - React Router V7 - Full-stack React framework
    - ACP Support - Connect to any Agent Client Protocol compatible agent like Gemini CLI, Claude Code, or Codex CLI
    - Uses AI SDK with `acp-ai-provider` to enable seamless integration with ACP-compatible AI agents on the web platform using `streamText` and `useChat`

## office-mcp

- https://github.com/jgraph/drawio-mcp /202602/js
  - The official draw.io MCP (Model Context Protocol) server that enables LLMs to create and open diagrams in the draw.io editor.
  - https://github.com/jgraph/drawio-mcp/tree/main/skill-cli
  - A Claude Code skill that generates native .drawio files, with optional export to PNG, SVG, or PDF (with embedded XML so the exported file remains editable in draw.io). No MCP setup required.
  - Generate draw.io XML for your requested diagram; Write it to a `.drawio` file in your current directory
  - If you requested an export format, export using the draw.io desktop CLI

- https://github.com/magicyuan876/mineru-tianshu /apache2/202601/python/ts/vue
  - 天枢 - 企业级 AI 数据预处理平台，将非结构化数据转换为 AI 可用的结构化格式
  - 支持文档、图片、音频等多模态数据处理 | GPU 加速 | MCP 协议
  - 后端：FastAPI、LitServe、MinerU、PaddleOCR、SenseVoice、SQLite、Loguru
  - 前端：Vue 3、TypeScript、Vite、TailwindCSS、Pinia、Vue Router
  - 多解析引擎: MinerU、PaddleOCR-VL、MarkItDown、格式引擎
    - pipeline: MinerU 标准流程，通用文档解析
    - vlm-transformers/vlm-vllm-engine: MinerU VLM 模式
    - paddleocr-vl: 109+ 语言，自动方向矫正, 仅支持 GPU: PaddleOCR-VL 目前不支持 CPU 及 Arm 架构
  - 文档: PDF、Word、Excel、PPT → Markdown/JSON（MinerU、PaddleOCR-VL 109+ 语言、水印去除）
  - 企业特性: GPU 负载均衡、任务队列、JWT 认证、MCP 协议、现代化 Web 界面
  - MCP 协议: 让 AI 助手（Claude Desktop）直接调用文档解析服务。

- https://github.com/SylphxAI/pdf-reader-mcp /471Star/MIT/202601/ts
  - https://pdf-reader-mcp.sylphx.com/
  - MCP server for PDF processing - 5-10x faster with parallel processing and 94%+ test coverage
  - Extract text, images, and metadata with unmatched performance and reliability.
  - Process 50-page PDFs in seconds with multi-core utilization
  - Absolute & relative paths, Windows/Unix support (v1.3.0)
  - Smart Ordering - Y-coordinate based content preserves document layout
  - Simple API - Single tool handles all operations elegantly

- https://github.com/ivanvanderbyl/pdf-reader-mcp /MIT/202505/go/inactive
  - MCP server for reading and analyzing PDF documents using Google's Gemini API, written in Go. This server enables AI assistants like Claude (Code and Desktop) and Cursor to seamlessly read, extract, and analyze PDF content directly from their interfaces.
# browser-use
- https://github.com/microsoft/playwright-mcp /27.2kStar/apache2/202602/ts
  - A Model Context Protocol (MCP) server that provides browser automation capabilities using Playwright. 
  - This server enables LLMs to interact with web pages through structured accessibility snapshots, bypassing the need for screenshots or visually-tuned models.
  - This package provides MCP interface into Playwright. 
  - If you are using a coding agent, you might benefit from using the CLI+SKILLS instead.
    - Modern coding agents increasingly favor CLI–based workflows exposed as SKILLs over MCP because CLI invocations are more token-efficient: they avoid loading large tool schemas and verbose accessibility trees into the model context, allowing agents to act through concise, purpose-built commands.
  -  MCP remains relevant for specialized agentic loops that benefit from persistent state, rich introspection, and iterative reasoning over page structure, such as exploratory automation, self-healing tests, or long-running autonomous workflows where maintaining continuous browser context outweighs token cost concerns.
  - https://x.com/playwrightweb/status/1904265499422409047
    - we went ahead and built an MCP server for Playwright. Ours is snapshot-based, which makes it faster and more reliable! You can opt into the visual mode too.

- https://github.com/ChromeDevTools/chrome-devtools-mcp /25.6kStar/apache2/202602/ts
  - MCP server, giving your AI coding assistant access to the full power of Chrome DevTools for reliable automation, in-depth debugging, and performance analysis.
  - Uses `puppeteer` to automate actions in Chrome and automatically wait for action results.
  - The MCP server will start the browser automatically once the MCP client uses a tool that requires a running browser instance. 
    - Connecting to the Chrome DevTools MCP server on its own will not automatically start the browser.

- https://github.com/browser-use/agent-sdk /370Star/MTI/202601/python
  - An agent is just a for-loop.
  - https://x.com/gregpr07/status/2012204140714217801
    - We open sourced our tiny agent-sdk, the easiest way to build Claude Code like agents (with any provider)
  - https://x.com/gregpr07/status/2012052139384979773
    - The Bitter Lesson of Agent Frameworks
    - All the value is in the RL'd model, not your 10,000 lines of abstractions
    - An agent is just a for-loop of messages. The only state an agent should have is: keep going until the model stops calling tools. You don't need an agent framework. It's just a for-loop of tool calls.
    - Our first Browser Use agents had thousands of lines of abstractions. They worked - until we tried to change anything. Every experiment fought the framework. 

- https://github.com/browser-use/browser-use /57.9kStar/MIT/202504/python/js
  - https://browser-use.com/
  - Enable AI to control your browser
  - [Pack 拆解 browser-use 项目 ](https://quaily.com/silico-anatomy/packs/110)
- https://github.com/browser-use/web-ui /MIT/202504/python
  - This project builds upon the foundation of the browser-use, which is designed to make websites accessible for AI agents.
  - WebUI: is built on Gradio and supports most of browser-use functionalities.
  - support for various Large Language Models (LLMs), including: Google, OpenAI, Azure OpenAI, Anthropic, DeepSeek, Ollama etc. 
  - You can choose to keep the browser window open between AI tasks, allowing you to see the complete history and state of AI interactions.

- https://github.com/Skyvern-AI/skyvern /AGPL/202506/python/ts
  - https://www.skyvern.com/
  - Skyvern automates browser-based workflows using LLMs and computer vision. 
  - It provides a simple API endpoint to fully automate manual workflows on a large number of websites
  - Instead of only relying on code-defined XPath interactions, Skyvern relies on Vision LLMs to interact with the websites.
  - Skyvern Cloud is a managed cloud version of Skyvern that allows you to run Skyvern without worrying about the infrastructure
    - It allows you to run multiple Skyvern instances in parallel and comes bundled with anti-bot detection mechanisms, proxy network, and CAPTCHA solvers.
  - Skyvern starts running the task in a browser that pops up and closes it when the task is done
  - Skyvern was inspired by the Task-Driven autonomous agent design popularized by BabyAGI and AutoGPT -- with one major bonus: we give Skyvern the ability to interact with websites using browser automation libraries like Playwright.

- https://github.com/browserbase/stagehand /11.3kStar/MIT/202504/ts
  - https://stagehand.dev/
  - An AI web browsing framework focused on simplicity and extensibility.
  - Stagehand is the easiest way to build browser automations. It is fully compatible with Playwright, offering three simple AI APIs on top of the base Playwright `Page` class
  - It works best when your code is a sequence of atomic actions.
  - Stagehand allows you to write durable, self-healing, and repeatable web automation workflows that actually work.
  - https://github.com/browserbase/mcp-server-browserbase
  - https://github.com/browserbase/sdk-node

- https://github.com/browserless/browserless /10kStar/SSPL-NC/202504/ts
  - https://browserless.io/
  - Browserless allows remote clients to connect and execute headless work, all inside of docker. 
  - It supports the standard, unforked Puppeteer and Playwright libraries, as well offering REST-based APIs for common actions like data collection, PDF generation and more.
  - Parallelism and request-queueing are built-in + configurable.
  - Works with unforked Puppeteer and Playwright.
  - An interactive puppeteer debugger, so you can see what the headless browser is doing and use its DevTools.
  - Support for running and development on Apple's M1 machines
  - 💰 If you want to use Browserless to build commercial sites, applications, or in a continuous-integration system that's closed-source, then you'll need to purchase a commercial license.
  - 💡 Browserless listens for both incoming websocket requests, generally issued by most libraries, as well as pre-build REST APIs to do common functions (PDF generation, images and so on). When a websocket connects to Browserless it starts Chrome and proxies your request into it. 
    - Once the session is done then it closes and awaits for more connections. 
    - Some libraries use Chrome's HTTP endpoints, like /json to inspect debug-able targets, which Browserless also supports.

- https://github.com/rebrowser/rebrowser-patches /202506/js
  - Collection of patches for puppeteer and playwright to avoid automation detection and leaks. 
  - Helps to avoid Cloudflare and DataDome CAPTCHA pages. 
  - Easy to patch/unpatch, can be enabled/disabled on demand.
# computer/container-use
- https://github.com/bytedance/UI-TARS-desktop /28.8kStar/apache2/202603/ts
  - https://agent-tars.com/
  - A GUI Agent application based on UI-TARS(Vision-Language Model) that allows you to control your computer using natural language.
  - ❓ agent-tars似乎支持replay，ui-tars是否支持replay
  - 在向cowork方向发展
  - https://x.com/Nin19536/status/1905975354227040314
    - 从 TARS 的开源 repo 学到的两个架构特点
    - 1️⃣mcp 统一工具协议: 可插拔，可扩展非常关键，且 tool 定义和 tool 执行对外只暴露接口，agent 端不关心实现。
    - 2️⃣事件管理: 管理好所有流式输出、任何工具 update，都需要考虑到前端展示 event 的方式，提供更好交互。而且事件管理有利于模型统一管理上下文。以事件时间戳永远自增，便于时间回溯和用户观测。
  - https://x.com/imwritingbugs/status/2000862713594195989
    - 真不错啊，里面一堆好用的沙盒工具。基本上可以复制粘贴就实现 browser use，terminal use
  - [2025-03-18] We released a technical preview version of a new desktop app - Agent TARS, a multimodal AI agent that leverages browser operations by visually interpreting web pages and seamlessly integrating with command lines and file systems.
    - Comprehensive Tool Support: Integrates with search, file editing, command line, and Model Context Protocol (MCP) tools to handle complex workflows.
  - https://github.com/bytedance/UI-TARS /apache2
    - UI-TARS is a next-generation native GUI agent model designed to interact seamlessly with graphical user interfaces (GUIs) using human-like perception, reasoning, and action capabilities. 
    - Unlike traditional modular frameworks, UI-TARS integrates all key components—perception, reasoning, grounding, and memory—within a single vision-language model (VLM), enabling end-to-end task automation without predefined workflows or manual rules.
    - This project builds upon and extends the capabilities of Qwen2-VL, a powerful vision-language model, which serves as the foundational architecture for UI-TARS. 
  - https://github.com/web-infra-dev/Midscene /MIT/ts
    - open-source web automation SDK that has supported UI-TARS model. 
    - Midscene.js lets AI be your browser operator. Just describe what you want to do in natural language, and it will help you operate web pages, validate content, and extract data. 
    - Besides the default model GPT-4o, we have added two new recommended open-source models to Midscene.js: UI-TARS and Qwen2.5-VL. (Yes, Open Source !) 
    - Supports Puppeteer and Playwright integration, allowing you to combine AI capabilities with these powerful automation tools
    - Visual Reports for Debugging 🎞️: Through our test reports and Playground, you can easily understand, replay and debug the entire process.
    - [Midscene.js - Joyful Automation by AI - Midscene.js](https://midscenejs.com/index.html#visualized-report)  
      - Midscene wants to provide a way to make automation more stable and easier to debug, so we provide a visual report after each run. With this report, you can review the animated replay and view the details of each step in the process.

- https://github.com/e2b-dev/open-computer-use /apache2/202503/python
  - A secure cloud Linux computer powered by E2B Desktop Sandbox and controlled by open-source LLMs.
  - Uses E2B for secure Desktop Sandbox
  - Operates the computer via the keyboard, mouse, and shell commands
  - Supports 10+ LLMs, OS-Atlas/ShowUI and any other models you want
  - Live streams the display of the sandbox on the client computer
  - User can pause and prompt the agent at any time
  - Uses Ubuntu, but designed to work with any operating system
  - [How I taught an AI to use a computer _202501](https://blog.jamesmurdza.com/how-i-taught-an-ai-to-use-a-computer)

- https://github.com/Aident-AI/open-cuak /apache2/202503/ts
  - https://aident.ai/
  - Open CUA Kit (Computer Use Agent), is THE platform for teaching, hiring and managing automation agents at scale — starting with browsers.
  - Open-CUAK is designed to run and manage thousands of automation agents, ensuring each one is reliable.
  - Run Operator-like automation workflows locally, ensuring full privacy

- https://github.com/bytebot-ai/bytebot /MIT/202505/ts
  - Bytebot is the container for desktop agents.
  - Bytebot spins up a containerized Linux desktop you can drive programmatically or via VNC—perfect for automation, scraping, CI tasks, and remote work.
  - https://x.com/zhangjintao9020/status/1911379146665603542
    - 实际上是一个 xface 桌面环境的 Ubuntu，通过 VNC 或浏览器来管理访问
    - 结合 CF 即将到来的无状态容器化！

- https://github.com/hangwin/mcp-chrome /9.6kStar/MIT/202511/ts/vue
  - a Chrome extension-based Model Context Protocol (MCP) server that exposes your Chrome browser functionality to AI assistants like Claude, enabling complex browser automation, content analysis, and semantic search.
  - Unlike traditional browser automation tools (like Playwright), Chrome MCP Server directly uses your daily Chrome browser, leveraging existing user habits, configurations, and login states, allowing various large models or chatbots to take control of your browser and truly become your everyday assistant.
  - Chatbot/Model Agnostic: Let any LLM or chatbot client or agent you prefer 
  - Use Your Original Browser: Seamlessly integrate with your existing browser
  - Fully Local: Pure local MCP server ensuring user privacy
  - Streamable HTTP: Streamable HTTP connection method
  - Cross-tab context
  - Built-in vector database for intelligent browser tab content discovery
  - 20+ Tools: Support for screenshots, network monitoring, interactive operations, bookmark management, browsing history, and 20+ other tools
  - Custom WebAssembly SIMD optimization for 4-8x faster vector operations
  - https://x.com/hang49911102/status/2001865778266804264
    - 看了下Claude code里跟Chrome通信的方案，跟我之前实现的是一样的

- https://github.com/vercel-labs/agent-browser /13.2kStar/apache2/202602/rust/ts
  - https://agent-browser.dev/
  - Headless browser automation CLI for AI agents. Fast Rust CLI with Node.js fallback.
  - https://x.com/Jiaxi_Cui/status/2020233150950174833
    - rust写的cli解析层，实际还是有个node daemon，依赖playwright core
    - 通过封装playwright实现浏览器控制，同时对元素进行重新映射，简化元素定位，进而大幅度减少上下文token，想法也不错
    - 这个东西我深度使用了一段时间，目前发现了两个问题，一个是在 Windows 的稳定性不够，经常出现 Daemon 无法启动的情况。在 GitHub 上发现了一个 PR 修复这个问题，不过目前还没有合入。另外就是不能去获取网页的 dom 结构。如果是用来调试一些前端页面问题，或者做一些深入的数据抓取，就不太行了。
    - 不用尝试了，社交媒体网站会屏蔽所有headless浏览器，这种工具毫无意义
    - 我用cdp的模式比较可控
# acp/agent-client-protocol
- https://github.com/mcpc-tech/mcpc/tree/main/packages/acp-ai-provider /MIT/202512/ts
  - https://ai-sdk.dev/providers/community-providers/acp
  - This package bridges ACP agents to the AI SDK. 
  - It spawns ACP agents (Claude Code, Gemini, Codex CLI, and more) as child processes and exposes them through the AI SDK's `LanguageModelV2` protocol.
  - Now you can start building your agent using `streamText` with Claude Code, Codex, OpenCode, and more
  - https://github.com/mcpc-tech/dev-inspector-mcp
    - AI-powered visual debugging for React, Vue, Svelte, SolidJS, Preact & Next.js via MCP and ACP.
    - DevInspector connects your web app directly to your AI agent. Click any element to instantly send its source code, style, and network context to the AI for analysis and fixing.

- https://github.com/RAIT-09/obsidian-agent-client /127Star/apache2/202512/ts
  - Bring AI agents into Obsidian via Agent Client Protocol (ACP), such as Claude Code, Codex and Gemini CLI.
  - This plugin lets you chat with Claude Code, Codex, Gemini CLI, and other AI agents right from your vault.
  - Multi-Agent Support: Switch between Claude Code, Codex, Gemini CLI, and custom agents
  - Note Mention Support: @notename to reference specific notes
  - Use / commands to browse and trigger actions provided by your current agent
  - Permission Management: Fine-grained control over agent actions

- https://github.com/daodao97/acpone /202512/go/ts/vue
  - 基于 ACP 协议 - 同时调度多个 AI Agent 的 ChatBot。
  - 多 Agent 支持 (Claude Code, Codex 等)
  - markstream-vue (Markdown 渲染)
  - 内嵌静态文件 (go:embed)
  - JSON-RPC 2.0
  - https://x.com/daodao97__/status/2000877211197567360
    - 搓了个新玩具 ACPone :  一个基于 ACP 协议的小应用

- https://github.com/marimo-team/use-acp /apache2/202510/ts
  - https://marimo-team.github.io/use-acp/
  - React hooks for Agent Client Protocol (ACP) over WebSockets.
  - Reactive state management

- https://github.com/Areo-Joe/chrome-acp /MIT/202602/ts
  - https://areo-joe.github.io/chrome-acp/
  - A Chrome extension to chat with AI agents. Give them the power to see and interact with your browser.
  - Works with any ACP-compatible agent — Claude Code, OpenCode, Gemini CLI, and more
  - Operates as you — Agents interact with pages using your real browser session 
  - [Built a Chrome extension using ACP - give AI agents control of your browser : r/ZedEditor](https://www.reddit.com/r/ZedEditor/comments/1r73hr3/built_a_chrome_extension_using_acp_give_ai_agents/)
    - a Chrome extension that lets you chat with any ACP-compatible agent (Claude Code, Codex, Gemini CLI, OpenCode, etc.) directly from your browser — and give them the ability to see and interact with your tabs.
    - Apart from the extension, I also build web UI for it. So based on the CS architecture, the backend and the agent can be deployed to anywhere(Mac mini) and you can control the agent remotely (just like OpenClaw).
# multi-agent/a2a

# streaming-llm
- https://github.com/globalaiplatform/langdiff /225Star/apache2/202509/python/ts
  - https://langdiff.readthedocs.io/en/latest/
  - https://globalaiplatform.github.io/langdiff/
  - LangDiff is a Python library that solves the hard problems of streaming structured LLM outputs to frontends
  - LangDiff provides intelligent partial parsing with granular, type-safe events as JSON structures build token by token, plus automatic JSON Patch generation for efficient frontend synchronization.
  - Streaming Parsing
    - Define schemas for streaming structured outputs using Pydantic-style models.
    - Receive granular, type-safe callbacks (on_append, on_update, on_complete) as tokens stream in.
    - Derive Pydantic models from LangDiff models for seamless interop with existing libraries and SDKs like OpenAI SDK.
  - Change Tracking
    - Track mutations without changing your code patterns by instrumenting existing Pydantic models, or plain Python dict/list/objects.
    - Generate JSON Patch diffs automatically for efficient state synchronization between frontend and backend.
  - The Problem with Traditional Streaming Approaches
    - Even partial JSON parsing libraries that "repair" incomplete JSON don't fully solve the issues
  - The Coupling Problem
    - tightly coupling frontend UIs to LLM output schemas.
  - ✨ LangDiff solves these problems through two key innovations:
    - Intelligent Streaming Parsing: Define schemas that understand the streaming nature of LLM outputs. Get type-safe callbacks for partial updates, complete fields, and new array items as they arrive.
    - Change-Based Synchronization: Instead of streaming raw JSON, track mutations on your application objects and send lightweight JSON Patch diffs to frontends. This decouples UI state from LLM output format.

- [Smooth a stream of LLM tokens into a stream of characters while reducing jitter by stabilising output timing. Explorations of different approaches.](https://gist.github.com/sebinsua/76fc5eb6fc498636bc637b9f10b7e6bf)
  - This approach slows the stream down a little and does generally reduce the jitter (such as pauses and bursts in the token stream). The approach was made based on educated guess-work about what might work and evaluated by eye-balling it instead of in a systematic manner. It is not perfect and sometimes the queue is exhausted only to find that we are waiting on a token. 
  - Another approach might be to extend the function that calculates the delay length by looking at the rate of increase/decrease of the queue size, as this would allow the algorithm to consider 'the future' in its decisions.
  - I experimented trying to put this on the back-end using ai in a Next.js app and a client-side React library on the UI. In order to do so, I had to transform to and from AsyncIterator and ReadableStream
# protocols-ai
- https://github.com/agentclientprotocol/agent-client-protocol /871Star/apache2/202510/rust/ts
  - https://github.com/zed-industries/agent-client-protocol
  - https://agentclientprotocol.com/
  - A protocol for connecting any editor to any agent
  - [Bring Your Own Agent to Zed — Featuring Gemini CLI — Zed's Blog _202508](https://zed.dev/blog/bring-your-own-agent-to-zed)
# skills
- https://github.com/PrefectHQ/colin /202602/python
  - https://colin.prefect.io/
  - A context engine that treats skills as software.
  - Write templates that reference live sources—GitHub, Linear, Notion, HTTP endpoints—and other documents. Colin compiles them, tracks dependencies, and rebuilds only what's stale.
  - Run colin run. Colin fetches the Linear issues, resolves the reference to your weekly notes, extracts blockers via LLM, and writes the compiled skill. Run it again tomorrow—if nothing changed upstream, nothing rebuilds. The expires: 1d ensures time-sensitive content stays fresh.
  - [We built Colin, a context engine that can keep agent skills fresh : r/AI_Agents _202601](https://www.reddit.com/r/AI_Agents/comments/1qnns7n/we_built_colin_a_context_engine_that_can_keep/)

- https://github.com/ConardLi/rag-skill /202602/python
  - 专为本地知识库智能检索设计的 AI Skill 演示仓库，展示如何通过分层索引和渐进式检索实现高效的多格式文件问答系统。
  - 分层索引 - 通过 data_structure.md 实现智能目录导航
    - 每个目录都有 data_structure.md 文件，说明子目录/文件的用途
  - 渐进式检索 - 避免全文加载，按需局部读取，节省 token
    - 不要一次性读取整个文件 
    - 使用 grep 定位关键词, 只读取匹配行附近的上下文（limit=200-500）
    - 多轮迭代（最多 5 次）逐步缩小范围
  - 多轮迭代 - 最多 5 轮智能检索，确保找到最相关信息
  - 强制学习机制 - 处理 PDF/Excel 前必须先学习处理方法
    - 遇到 PDF 或 Excel 文件时，必须先读取 references/pdf_reading.md

- https://github.com/op7418/Humanizer-zh /MIT/202601/md
  - Humanizer-zh: AI 写作去痕工具（中文版）
  - https://github.com/blader/humanizer
    - 原项目基于维基百科的 Signs of AI writing 指南

- https://github.com/bobmatnyc/mcp-skillset /MIT/202602/python
  - mcp-skillset is a standalone Python application that provides intelligent, context-aware skills to code assistants through hybrid RAG (vector + knowledge graph). 
  - Unlike static skills that load at startup, mcp-skillset enables runtime skill discovery, automatic recommendations based on your project's toolchain
  - Dynamic Discovery: Vector similarity + knowledge graph for better skill finding
  - On-Demand Loading: Skills loaded when needed, not all at startup
  - MCP Native: First-class Model Context Protocol integration
  - agentskills.io Compatible: Supports both native and agentskills.io specification formats

- https://github.com/comeonzhj/Auto-Redbook-Skills /python/js
  - 一个自动撰写小红书笔记，自动生成图片，自动发布的 Skills
  - 根据既定主题，撰写小红书笔记（提示词自己调整，在 SKILL.md里）
  - 根据内容自动渲染生成图片，包含 cover 和内容详情，支持 Markdown 渲染
  - 提供 Python 和 Node.js 两种渲染方案
  - 支持直接发布到小红书（需配置 Cookie）
  - [[开源]Skills-自动写小红书笔记做图片并发布 _202601](https://linux.do/t/topic/1481151)

- https://github.com/JimLiu/baoyu-skills
  - content-skills: xhs-images, cover-image, slide-deck, comic, article-illustrator, post-to-x, post-to-wechat
  - utility-skills: danger-x-to-markdown, compress-image
  - https://x.com/dotey/status/2013044625238339994
    - Introducing slide-deck skill
    - Turn any article or content into professional slide decks with AI-generated images.
    - 15 styles to choose from
    - the generated slides can be exported as a PPTX file

- https://github.com/assafelovic/skyll /apache2/202602/python/ts
  - https://skyll.app/
  - A tool for AI agents to discover and learn skills autonomously
  - https://x.com/EdenEmarco177/status/2018602082962690511
    - This is the future of agents. Dynamic skill loading
    - I did something similar at https://labs.youware.com/youskill. The difference is it's agentic skill discovery based on your actual request. Should I make this an MCP?

- https://github.com/mcollina/skills /MIT/202603/ts
  - My own collection of skills for modern Node.js development
  - https://x.com/matteocollina/status/2031053418064720273
    - fter years of building with Node.js, I've organized my hard-won knowledge into skills: a collection of best practices, workflows, and deep expertise my AI assistant uses to write code to my standard.
    - fastify: hooks lifecycle, plugin architecture, performance tuning
    - node: event loop, async error handling, streams, test runner
    - nodejs-core: V8 internals, libuv, C++ addons
    - typescript-magician: advanced types, complex generics
    - octocat: GitHub workflows with gh CLI
    - oauth: OAuth 2.0/2.1 + Fastify integration
    - linting: neostandard + ESLint v9 flat config
    - documentation: Diátaxis framework
# utils
- https://github.com/mksglu/claude-context-mode /2.2kStar/MIT/202603/ts
  - https://cc-context-mode.mksg.lu/
  - The other half of the context problem.
  - Inspired by Cloudflare's Code Mode — which compresses tool definitions from millions of tokens into ~1, 000 — we asked: what about the other direction?
  - Context Mode is an MCP server that sits between Claude Code and these outputs. 315 KB becomes 5.4 KB. 98% reduction.
  - This installs the MCP server + a PreToolUse hook that automatically routes tool outputs through the sandbox + slash commands for diagnostics and upgrades.

- https://github.com/apify/mcp-cli /323Star/MIT/202602/ts
  - a CLI client for MCP. It supports persistent sessions, stdio/HTTP, OAuth 2.1, JSON output for code mode, proxy for AI sandboxes, and much more.
  - Works with any MCP server over Streamable HTTP or stdio.
  - JSON output enables integration with CLI tools like jq and scripting.
  - AI sandboxing - MCP proxy server to securely access authenticated sessions from AI-generated code.
  - works on Mac/Win/Linux, doesn't use LLMs on its own.

- https://github.com/philschmid/mcp-cli /892Star/MIT/202602/ts
  - A lightweight, Bun-based CLI for interacting with MCP (Model Context Protocol) servers.
  - Single Binary - Compile to standalone executable via bun build --compile
  - Designed for AI coding agents (Gemini CLI, Claude Code, etc.)
  - Supports both stdio and HTTP MCP servers
  - mcp-cli is designed to give AI coding agents access to MCP (Model Context Protocol) servers. 
  - Traditional MCP integration loads full tool schemas into the AI's context window, consuming thousands of tokens.
  - The CLI approach: Only fetch schemas when needed
    - Shell composable: Chain with jq, pipes, and scripts
    - Scriptable: AI can write shell scripts for complex workflows

- https://github.com/mcpshim/mcpshim /202602/go
  - https://mcpshim.dev/
  - Turn remote MCP servers into local command workflows.
  - A lightweight daemon + CLI bridge that centralizes MCP sessions, auth, discovery, and tool execution behind one local Unix socket.
  - Remote MCP servers are powerful, but each service has its own auth flow, transport expectations, and invocation patterns. Wiring all of that directly into every script or agent loop creates brittle command workflows.
  - dumping raw MCP schemas for every connected server can consume prompt budget before useful work begins.
  - mcpshimd handles MCP lifecycle concerns in one place: session management, discovery, retries, and OAuth flow.
  - mcpshim provides a stable CLI surface over a local Unix socket so tools can be called consistently, with dynamic flags translated to MCP arguments at runtime.
  - [I turned MCP tools into standard CLI commands to solve context pollution : r/ollama _202602](https://www.reddit.com/r/ollama/comments/1rcv5by/i_turned_mcp_tools_into_standard_cli_commands_to/)
    - what difference does it make with direct api calls then ? 
    - Not everything is an MCP wrapped around an API. Not every API is simple. Often times the openapi spec is larger than the MCP tool def.
    - Can you expand the example config to include stuff like local servers using node or npx, etc?

- https://github.com/jx-codes/lootbox /MIT/202602/ts
  - Code mode doesn't replace MCP - it orchestrates it.
  - Lootbox is inspired by "Code Mode" - LLMs write TypeScript code to call APIs rather than using tool invocation.
  - The repository includes example tools for key-value storage, SQLite, knowledge graphs, GraphQL, and filesystem operations that you can copy to your project.
  - [Code Mode: give agents an entire API in 1, 000 tokens](https://blog.cloudflare.com/code-mode-mcp/)

- https://github.com/elusznik/mcp-server-code-execution-mode /GPL/202512/python/inactive
  - An MCP server that executes Python code in isolated rootless containers with optional MCP server proxying. Implementation of Anthropic's and Cloudflare's ideas for reducing MCP tool definitions context bloat.
  - [I developed an open-source Python implementation of Anthropic/Cloudflare idea of calling MCPs by code execution : r/LocalLLaMA](https://www.reddit.com/r/LocalLLaMA/comments/1otkf5e/i_developed_an_opensource_python_implementation/)

- https://github.com/AnEntrypoint/codemode-agent /202510/js/inactive
  - A Claude agent with an execute tool that provides programmatic access to file operations, system commands, and MCP tools. Features interactive mode with real-time typing, persistent execution context, and seamless integration with multiple MCP servers.
  - [I implemented the codemode article that cloudflare published, as an agent and MCP tool : r/aipromptprogramming](https://www.reddit.com/r/aipromptprogramming/comments/1o8vbep/i_implemented_the_codemode_article_that/)
# more
