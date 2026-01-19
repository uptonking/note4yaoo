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
  - require Context7 API Key (Optional) for higher rate limits and private repositories 
  - [Feature Request: Option to Self-Host Documentation Backend _202504](https://github.com/upstash/context7/issues/59)
    - interesting idea. I will think about this. the biggest obstacle would be licensing. we aim to make this service free for developers and open source projects. but we want to commercialize if a company like cursor needs it.
    - but we can keep parser private and web backend open.
    - maybe you can store all the docs in a public database, that way anyone can self-host.
    - Another option is to allow companies to host their documentation on context7's servers privately, and support authentication.

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

## browser-mcp

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
# more
