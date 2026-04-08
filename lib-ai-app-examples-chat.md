---
title: lib-ai-app-examples-chat
tags: [ai, chat, chatgpt, examples]
created: 2025-03-22T18:49:02.969Z
modified: 2025-03-22T18:49:15.634Z
---

# lib-ai-app-examples-chat

# guide
- tips
  - 不必执着于通用chat/ui, 不同业务需要针对具体场景逻辑做优化，如书籍长文本、pdf布局、coding
    - 而这些已有的方案大多已经提供了chat-ui
  - 不要执着于chat, text-generation-ui方向的产品也很合适
# popular
- https://github.com/open-webui/open-webui /107kStar/MIT > BSD+LOGO/202405/python/svelte
  - https://openwebui.com/
  - User-friendly WebUI for LLMs (Formerly Ollama WebUI)
  - extensible, feature-rich, and user-friendly self-hosted WebUI designed to operate entirely offline. 
  - 后端tavily搜索部分用到了langchain，langchain整体仅7个文件
  - 前端使用sveltekit
  - db支持pg
  - It supports various LLM runners, including Ollama and OpenAI-compatible APIs
  - 🌹 pros: comfyui
  - 🐛 cons: MCP
  - [Open WebUI changed license from BSD-3 to Open WebUI license with CLA | Hacker News _202505](https://news.ycombinator.com/item?id=43901575)
    - What really is the moat of openwebui? I have seen at least 4 - 5 react UIs with similar functionality (chat, RAG, document library).
    - Not sure about the moat, it's mostly a SvelteKit web app with extra utils after all. But it has a rather unique combination of advanced features (RAG integrations, workspaces, pipelines, code execution, MCP integration, etc.) and a user-friendly "production grade" interface. 
    - They swapped out MIT for BSD-3 just five months ago
  - [Why is it so difficult to add providers to openwebui? : r/OpenWebUI _202505](https://www.reddit.com/r/OpenWebUI/comments/1kbox4y/why_is_it_so_difficult_to_add_providers_to/)
  - [Implement a Queue System  ](https://github.com/open-webui/open-webui/discussions/4256)
    - Setting the olama environment configs will solve this problem, it does not seem to be an open-webui issue
  - [Feature: Queue multiple messages _202502](https://github.com/open-webui/open-webui/discussions/10845)
    - It's in settings, no it's in admin panel, it's a pipeline - no sorry, it's actually a function.
    - If you use LiteLLM to configure the providers and don't go through Open WebUI pipe functions at all, it is much easier.
    - back in the early days of open-webui, LiteLLM was bundled along. It's better that it's installed separately of course, since both projects are moving along nicely.
  - https://github.com/Haervwe/open-webui-tools /MIT/202508/python
    - https://openwebui.com/u/haervwe
    - a modular toolkit designed to extend and enrich your Open WebUI instance
    - 15+ specialized tools and functions designed to enhance your Open WebUI experience
    - arXiv Search - Academic paper discovery (no API key required!)
    - Pexels Media Search - High-quality photos and videos from Pexels API
    - Native Image Generator - Direct Open WebUI image generation with Ollama model management
    - Flux Kontext ComfyUI - Professional image editing
    - ComfyUI ACE Step Audio - Advanced music generation
    - Visual Integration: Seamless integration with ComfyUI workflows
  - 🍴 forks
  - https://github.com/AI3clauseBSD/claused-webai /inactive
  - https://github.com/nick-tonjum/open-webui-artifacts-overhaul /202504/inactive
    - brings Claude artifacts and OpenAI Canvas-like functionality to openwebui
  - https://github.com/jeannotdamoiseaux/GovChat-NL /202507
  - https://github.com/ssc-dsai/canchat-v2 /202508/BSD
    - Granular Permissions and User Groups
    - Offline Mode
- https://github.com/xxnuo/open-coreui /1.4kStar/apache2/202511/rust/svelte
  - A rewritten Open WebUI in Rust, significantly reducing memory and resource usage, requiring no dependency services, no Docker, with both a server version and a Tauri-based desktop client. (formerly Open WebUI Lite)
  - a rewritten lite fork of Open WebUI v0.6.32
  - https://github.com/knoxchat/open-webui-rust
    - High‑Performance Rust Implementation of Open WebUI
  - https://github.com/knoxchat/knoxchat /MIT/ts
    - a vigilant supervisor and management tool that ensures LLM teams rigorously develop reliable AI Agent programming extensions for VSCode and compatible editors

- https://github.com/danny-avila/LibreChat /29kStar/MIT/202508/ts前端/cjs后端
  - https://librechat.ai/
  - Enhanced ChatGPT Clone: Features Agents, DeepSeek, Anthropic, Gemini
  - 后端依赖mongoose、@langchain/core、express、@keyv/redis、keyv-file、EventSource(sse)、diff、firebase、handlebars、meilisearch、memorystore、passport-local、sharp、winston
  - 前端依赖@tanstack/react-query、jotai、@ariakit/react、react-hook-form，不依赖langchain
  - 聊天数据持久化在mongodb
  - 🛝📡 考虑用langgraph重写后端，去掉langchain
  - UI & Experience inspired by ChatGPT with enhanced design and features
  - Code Interpreter API
  - Generative UI with Code Artifacts: allow creation of React, HTML, and Mermaid diagrams directly in chat
  - Image Generation & Editing: Text-to-image with DALL-E (3/2), Stable Diffusion, Flux, or any MCP server
  - Multimodal & File Interactions
  - Import & Export Conversations
  - Multi-User, Secure Authentication with OAuth2, LDAP, & Email Login Support
  - Install LibreChat Locally Using npm: [Getting Started for Contributors](https://www.librechat.ai/docs/development/get_started)
  - [Model Context Protocol (MCP)](https://www.librechat.ai/docs/features/mcp)
    - LibreChat leverages MCP to dramatically expand what your AI agents can do, allowing you to integrate everything from file system access, web browsers, specialized APIs, to custom business tools.
    - Any time you add or edit an MCP server, you will need to restart LibreChat to initialize the connections.
  - [Enhancement: Extend Stable Diffusion plugin to work with ComfyUI _202405](https://github.com/danny-avila/LibreChat/issues/2672)
    - We already support Stable Diffusion. It will be great to add support for ComfyUI.
    - /not-planned
  - 🔡 [Artifacts: Generate React, HTML & Diagrams Instantly](https://www.librechat.ai/docs/features/artifacts)
    - Note: The preferred way to use artifacts is now through the Agents feature, which allows for more granular control by enabling/disabling artifacts at the agent level rather than app-wide.
    - Artifacts in LibreChat use CodeSandbox’s Sandpack library to securely render HTML/JS code. By default, LibreChat connects to CodeSandbox’s public CDN 
    - For enhanced privacy, security compliance, or isolated network environments, you can self-host the bundler.
  - https://github.com/leikoilja/LibreChat-UI /202503/js
    - Cross-platform desktop app wrapper for self-hosted LibreChat
  - https://github.com/LibreChat-AI/static-browser-server /202504/ts
    - This repository contains the static browser server used by Sandpack, with step-by-step instructions specifically tailored for LibreChat integration.
  - 🍴 forks
  - https://github.com/danieldjupvik/LibreChat-fork /202508
    - feat: Add 'web_search' capability to ModelSpecItem
    - feat: create LiteLLM proxy for getting model info
  - https://github.com/intelequia/LibreChat /202508
    - feat: Auth and User System
  - https://github.com/jmaddington/LibreChat /202507
    - E2B.dev code interpreter added to the tools list
    - Web Navigator plugin added to the tools list.
    - QuickChart plugin added to the tools list.
    - TimeAPI.io plugin added to the tools list.
  - https://github.com/paychex/LibreChat /202508
  - https://github.com/MiroStW/LibreChat /202508/docker
  - https://github.com/lihe8811/LibreChat /202508
  - https://github.com/aitok-ai/LibreChat /202503
  - https://github.com/naga-ai-hub/naga-chat /202508/单文件修改
  - https://github.com/e-gineering/LibreChat /202508
    - Commented out Perplexity by default
  - 💰 [ClickHouse has acquired LibreChat : r/LocalLLaMA _202511](https://www.reddit.com/r/LocalLLaMA/comments/1ooms3e/clickhouse_has_acquired_librechat/)
    - they are planning to keep the MIT + OSS model which is nice to see
    - I've been using it for a year, I set it up for our team at work. It's a great multi-user self-hosted ChatGPT clone that works with any provider (OpenAI, OpenRouter, your local llama, etc).

- koishi /5.2kStar/MIT/202507/ts
  - https://github.com/koishijs/koishi
  - https://koishi.chat/
  - Koishi 是一个跨平台、可扩展、高性能的跨平台聊天机器人框架。
  - 支持 QQ，Telegram，Discord，飞书等主流聊天平台，支持多账户和跨平台数据互通
  - 提供在线插件市场，即使没有任何编程基础，也能轻松在控制台中下载安装插件
  - 随时随地通过控制面板监控运行状态，控制机器人的行为，甚至上号聊天
  - 依赖satorijs、minato(db-driver)、cordis(aop)
  - 经过了长达四年的迭代，Koishi 已经发展出了丰富的插件生态和与之匹配的健壮系统。超过 1000 个官方和社区插件覆盖了机器人开发的方方面面，从平台支持、数据库、资源存储、网页控制台、状态管理到具体的业务功能一应俱全
  - https://github.com/koishijs/webui /AGPL/202507/ts/vue
    - WebUI plugins for Koishi
  - https://github.com/koishijs/koishi-desktop /AGPL/202405/go/inactive
    - Launch Koishi from your desktop
  - https://github.com/koishijs/novelai-bot /2.5kStar/MIT/202503/ts
    - 基于 NovelAI 的画图机器人
    - [feat: add support for ComfyUI _202406](https://github.com/koishijs/novelai-bot/pull/254)
      - 只支持了基本的text2image和image2image功能

- https://github.com/Mintplex-Labs/anything-llm /47.8kStar/MIT/202508/js/python
  - https://anythingllm.com/
  - A full-stack application that enables you to turn any document, resource, or piece of content into context that any LLM can use as a reference during chatting
    - An efficient, customizable, and open-source enterprise-ready document chatbot solution.
  - 基于langchain实现
  - [Native models used by AnythingLLM](https://github.com/Mintplex-Labs/anything-llm/tree/master/server/storage/models)
    - Use of a locally running LLM model is experimental and may behave unexpectedly, crash, or not function at all. 
    - We suggest for production-use of a local LLM model to use a purpose-built inference server like LocalAI or LMStudio.
    - Model must be in the latest GGUF format
    - Model should be compatible with latest `llama.cpp`.
    - 👀 注意没找到llama.cpp相关的代码
  - [AnythingLLM Desktop works across your entire OS with local models : r/LocalLLaMA _202602](https://www.reddit.com/r/LocalLLaMA/comments/1r8biu3/anythingllm_desktop_works_across_your_entire_os/)
    - Now with a simple customized keybind you can open an overlay that instantly has access to your open apps and screen.

- https://github.com/huggingface/chat-ui /9.2kStar/apache2/202510/ts/svelte
  - https://huggingface.co/chat/
  - A chat interface for LLMs. 
  - It is a SvelteKit app and it powers the HuggingChat app on hf.co/chat.
  - Chat UI only supports OpenAI-compatible APIs via OPENAI_BASE_URL and the /models endpoint.
  - Chat history, users, settings, files, and stats all live in MongoDB. You can point Chat UI at any MongoDB 6/7 deployment.

- https://github.com/ChatGPTNextWeb/NextChat /85.4kStar/MIT/202508/ts/tauri
  - https://nextchat.club/
  - Light and Fast AI Assistant. 
  - Support: Web | iOS | MacOS | Android | Linux | Windows
  - NextChat Support MCP
  - 研发活跃降低，对新模型的支持不快
  - Fully compatible with self-deployed LLMs, recommended for use with RWKV-Runner or LocalAI
  - Privacy first, all data is stored locally in the browser
  - Enterprise Edition
    - Permission Control: Clearly defined member permissions, resource permissions
    - Security Auditing: Automatically intercept sensitive inquiries and trace all historical conversation records
    - Private Deployment: Enterprise-level private deployment supporting various mainstream private cloud solutions
  - https://github.com/ChatAnyTeam/ChatAny /MIT/202411/ts/inactive
    - 一键拥有你自己的 ChatGPT+众多AI 的聚合网页服务（基于ChatGPT-Next-Web开发）
    - PRO版本支持更强大的功能：低内存占用，Golang开发原生高并发支持, 包含AI对话、AI绘画、AI音乐、AI视频、AI生成PPT、PDF解析对话、AI应用支持等众多AI模块

- https://github.com/lobehub/lobe-chat /64.5kStar/apache2+NonModify/202508/ts
  - https://chat-preview.lobehub.com/
  - An open-source, modern-design ChatGPT/LLMs UI/Framework.
  - Supports speech-synthesis, multi-modal, and extensible (function call) plugin system.
  - One-click FREE deployment of your private
  - https://github.com/lobehub/chat-plugin-sdk
    - https://chat-plugin-sdk.lobehub.com/
    - SDK for LobeChat function calling plugins
  - 🍴 forks
  - https://github.com/justUmen/Bjornulf_lobe-chat /202411/inactive
    - Quick and dirty fork to enable lobe-chat to send ComfyUI api request + receive image link + local TTS

- https://github.com/thinkinaixyz/deepchat /4.1kStar/apache2/202510/ts/vue
  - https://deepchat.thinkinai.xyz/
  - Open-Source Multi-Model AI Chat Platform
  - supporting multiple cloud and local large language models with powerful search enhancement and tool calling capabilities.
  - Built-in Ollama support 
  - Built-in MCP support enables code execution, web access, and other tools without additional configuration

- https://github.com/OvidijusParsiunas/deep-chat /3.2kStar/MIT/202510/ts
  - https://deepchat.dev/
  - a fully customizable AI chat component that can be injected into your website with just one line of code
  - Connect to any API
  - tts, stt, Speech To Speech
  - Everything is customizable
  - Support for all major ui frameworks/libraries
  - `browserStorage` allows you store messages locally on your browser without worrying about a backend message integration.
  - pr已关闭 [feat: ollama support _202501](https://github.com/OvidijusParsiunas/deep-chat/pull/333)
    - I am very keen to implement it properly myself
  - [Adding ollama api connection _202409](https://github.com/OvidijusParsiunas/deep-chat/issues/262)
    - 202510 pr合并

- https://github.com/microsoft/vscode-copilot-chat /8.3kStar/MIT/202508/ts
  - GitHub Copilot Chat (this extension) - A companion extension that provides conversational AI assistance.

- https://github.com/langchain-ai/chat-langchain /6kStar/MIT/202508/python/ts
  - https://chat.langchain.com/
  - an implementation of a chatbot specifically focused on question answering over the LangChain documentation. 
  - Built with LangChain, LangGraph, and Next.js.
  - https://github.com/langchain-ai/chat-langchainjs /MIT/202503/ts/inactive
    - https://chatjs.langchain.com/
    - Built with LangChainjs, and Next.js.

- https://github.com/olegshulyakov/llama.ui /MIT/202510/ts/仅web
  - https://llama-ui.js.org/
  - open-source desktop application that provides a beautiful, user-friendly interface for interacting with large language models (LLMs) powered by llama.cpp.
  - PWA support with offline capabilities
  - a fork of llama.cpp WebUI with: Fresh new styles
  - Multi-Provider Support: Works with llama.cpp, LM Studio, Ollama, vLLM, OpenAI, .. and many more
  - IndexedDB storage for conversations
  - Storage: IndexedDB via Dexie.js
  - Import/export functionality
  - File attachments (text, images, PDFs)

- https://github.com/eclaire-labs/eclaire /728Star/MIT/202512/ts
  - https://eclaire.co/
  - Local-first, open-source AI assistant for your data. Unify tasks, notes, docs, photos, and bookmarks. 
  - Private by default: By default all AI models run locally, all data is stored locally.
  - Layered architecture: frontend, backend, and workers are separate services. Run only the backend for API-only/data-processing use cases
    - Backend for AI assistant (eg. Qwen3 model), 
    - Workers for image and document processing (eg. Gemma3 multi-modal). 
    - Docling for processing some of the document formats.
  - Model backends: works with llama.cpp, vLLM, mlx-lm/mlx-vlm, LM Studio, Ollama, and more via the standard OpenAI-compatible API.
  - Storage: all assets (uploaded or generated) live in Postgres or file/object storage.
  - Documents: PDF, DOC/DOCX, PPT/PPTX, XLS/XLSX, ODT/ODP/ODS, MD, TXT, RTF, Pages, Numbers, Keynote, HTML, CSV, and more.

- https://github.com/chatboxai/chatbox /38.1kStar/GPL/202511/ts/inactive
  - https://chatboxai.app/
  - repository for the Chatbox Community Edition
  - We regularly sync code from the pro repo to this repo, and vice versa.

- https://github.com/clawdbot/clawdbot /MIT/202601/ts
  - https://clawd.bot/
  - Your own personal AI assistant. Any OS. Any Platform. The lobster way.
  - a personal AI assistant you run on your own devices. It answers you on the channels you already use (WhatsApp, Telegram, Slack, Discord, Google Chat, Signal, iMessage, Microsoft Teams, WebChat), plus extension channels like BlueBubbles, Matrix, Zalo, and Zalo Personal.
  - If you want a personal, single-user assistant that feels local, fast, and always-on, this is it.
  - [给大家推荐一下这几天国外爆火的 Clawdbot ](https://linux.do/t/topic/1511657)
    - 安装以后，它可以接入你的WhatsApp或Telegram，你给它发消息，它就能在你的电脑上帮你做各种事儿，例如回邮件、浏览网页、做视频等等，而且只在你的电脑上运行，不上传隐私。当然这些事儿Claude Code也能干，但和 clawdbot 对话更像人

- https://github.com/supermemoryai/llm-bridge /MIT/202511/ts/inactive
  - https://supermemory.ai/blog/we-solved-ai-api-interoperability/
  - Interoperability between input formats of various LLMs, with observability, error handling, etc. built in.
  - TypeScript library that provides seamless translation between different LLM provider APIs (OpenAI, Anthropic Claude, Google Gemini) while preserving zero data loss and enabling perfect reconstruction of original requests.

- https://github.com/specstoryai/getspecstory /961Star/apache2/202601/go
  - https://specstory.com/
  - Turn your AI development conversations into searchable, shareable knowledge.
  - Install our local first extensions for your favorite AI IDE or Terminal Agent. Sync your conversations to the cloud
  - https://x.com/doesdatmaksense/status/2012209297380544940
    - we’ve spent a lot of time normalizing agent sessions, and defining a stable contract for ai conversations across tools.
    - Normalizing agent sessions into a stable contract is underrated. Once the “conversation shape” is consistent, you can do boring but important stuff—diffs, audits, replay, evals—without rewriting integrations every time a new tool pops up.

- https://github.com/yoavf/ai-sessions-mcp /MIT/202602/go
  - An MCP server that makes sessions from Claude Code, OpenAI Codex, Gemini CLI and opencode available to any MCP compatible client.
  - Allow AI agents to search, list, and read your previous local coding sessions from multiple CLI coding agents.

- https://github.com/nervosys/chasm-cli /AGPL/202602/rust
  - Universal CLI for managing AI chat sessions across providers
  - unifying chat sessions from AI coding assistants like GitHub Copilot, Cursor, and more.
  - Extract chat sessions from VS Code, Cursor, Windsurf, and other editors
  - No Lock-in - Universal session format that works across all providers
  - Merge - Combine sessions across workspaces and time periods
  - Real-time Recording - Live session recording to prevent data loss from editor crashes
  - API Server - REST + WebSocket API for building custom integrations
  - SQLite-based storage that normalizes all providers

- https://github.com/meltylabs/chorus /714Star/MIT/202601/ts/rust/inactive
  - AI chat app for Mac
  - Built by the creators of Conductor.
# ui-ai 💄
- https://github.com/google/a2ui /543Star/apache2/202512/ts
  - https://a2ui.org/
  - open-source project, complete with a format optimized for representing updateable agent-generated UIs and an initial set of renderers, that allows agents to generate or populate rich user interfaces.
  - A2UI is an open standard and set of libraries that allows agents to "speak UI." Agents send a declarative JSON format describing the intent of the UI. The client application then renders this using its own native component library (Flutter, Angular, Lit, etc.).
  - The Client's A2UI Renderer parses the JSON.
  - Transports: Compatible with A2A Protocol and AG UI.
  - Note: A2UI is currently in v0.8 (Public Preview). The specification and implementations are functional but are still evolving.
  - https://x.com/Saboo_Shubham_/status/2000631830526222592
    - copilotkit: Check out our A2UI Widget builder
    - [Create | A2UI Composer](https://a2ui-editor.ag-ui.com/)

- https://github.com/vercel-labs/json-render /4.7kStar/apache2/202601/ts
  - https://json-render.dev/
  - Let end users generate dashboards, widgets, apps, and data visualizations from prompts — safely constrained to components you define.
  - When users prompt for UI, you need guarantees. json-render gives AI a constrained vocabulary so output is always predictable
  - https://x.com/rauchg/status/2011605996561649720
    - Why not AI -> UI? Code is more flexible than JSON.
- https://github.com/vercel-labs/visual-json /apache2/202604/ts
  - https://visual-json.dev/
  - The Visual JSON Editor. Schema-aware, embeddable, extensible.
  - Headless tree model, operations, and schema types
  - 支持react/vue/svelte

- https://github.com/thesysdev/openui /MIT/202603/ts
  - https://www.openui.com/
  - The Open Standard for Generative UI
  - OpenUI is a full-stack Generative UI framework — a compact streaming-first language, a React runtime with built-in component libraries, and ready-to-use chat interfaces — that is up to 67% more token-efficient than JSON.
  - https://x.com/rabi_guha/status/2031751935880314897
    - We built a better alternative to json-render & A2UI
    - Up to 3x faster rendering & 67% fewer tokens. Far fewer broken outputs.
    - Not your fault, but installing this repo uses 6.5 GB on my drive, with ~10 node_modules sub-folders all over... this whole Node ecosystem is bonkers

- https://github.com/ag-ui-protocol/ag-ui /8.4kStar/MIT/202510/python/ts
  - https://ag-ui.com/
  - AG-UI is an open, lightweight, event-based protocol that standardizes how AI agents connect to user-facing applications. 
  - Built for simplicity and flexibility, it enables seamless integration between AI agents, real time user context, and user interfaces.
  - During agent executions, agent backends emit events compatible with one of AG-UI's ~16 standard event types
  - Agent backends can accept one of a few simple AG-UI compatible inputs as arguments
  - AG-UI includes a flexible middleware layer that ensures compatibility across diverse environments:
    - Works with any event transport (SSE, WebSockets, webhooks, etc.)
    - Allows for loose event format matching, enabling broad agent and app interoperability
  - It also ships with a reference HTTP implementation and default connector to help teams get started fast.
  - 支持vanillajs/LangGraph/Pydantic/Mastra

- https://github.com/assistant-ui/tool-ui /MIT/202602/ts
  - https://tool-ui.com/
  - https://www.tool-ui.com/docs/gallery
  - UI components for AI interfaces.
  - JSON-native, typed, accessible, copy-pasteable.
  - Tools return JSON; Tool UI renders it as inline, narrated, referenceable surfaces.
  - Radix/shadcn (primitives) → Tool UI (conversation‑native components & schema) → AI SDK / LangGraph / etc. (LLM orchestration)
    - Client side: Register the component and let assistant-ui handle rendering.
    - assistant-ui manages the runtime, streaming, and tool call lifecycle
  - Built on Radix, shadcn/ui, and Tailwind.
  - https://x.com/HiTw93/status/2018109861201093052
    - It’s schema-first: every surface is driven by a serializable schema with stable IDs, so results stay consistent and reusable.

- https://github.com/assistant-ui/assistant-ui /5.8kStar/MIT/202508/ts
  - https://www.assistant-ui.com/
  - open source TypeScript/React library for AI chat.
  - The library handles essential chat features such as auto-scrolling, accessibility, and real-time updates, while providing easy integration with LangGraph, AI SDK, and custom backends.
  - The API of assistant-ui is inspired by libraries like shadcn/ui and cmdk. Instead of a single monolithic chat component, developers get primitive components that can be fully customized.
  - We have wide model provider support (OpenAI, Anthropic, Mistral...)
  - Chat UI: Streaming, Auto-scrolling, Markdown, Code Highlighting, File Attachments, and more
  - Frontend tool calls: Let LLMs take action in your frontend application
  - LangGraph interrupt() support
  - Chat Persistence
  - Choose your backend
    - AI SDK
    - LangGraph
    - Custom: your own backend/streaming protocols

- https://github.com/mckaywrigley/chatbot-ui /32kStar/MIT/202406/ts/inactive
  - https://chatbotui.com/
  - open-source AI chat app for everyone.
  - 🌰
  - https://github.com/guangzhengli/ChatFiles

- https://github.com/richardgill/llm-ui /MIT/202502/ts
  - https://llm-ui.com/
  - The React library for LLMs
  - Removes broken markdown syntax
  - Throttling smooths out pauses in the LLM’s streamed output
  - Renders output at native frame rate
  - Code blocks for every language with Shiki
  - Headless: Bring your own styles

- https://github.com/fmaclen/hollama /MIT/202407/ts/svelte
  - https://hollama.fernando.is/
  - A minimal web-UI for talking to Ollama servers
  - Markdown parsing w/syntax highlighting

- https://github.com/kangfenmao/cherry-studio /NonCommercial/202409/ts
  - https://cherry-ai.com/
  - a desktop client that supports for multiple LLM providers, available on Windows, Mac and Linux

- https://github.com/samdenty/react-ai-flow /202503/ts
  - https://react-ai-flow.com/
  - smooth React AI chatbot primitives
  - 支持多种打字动画效果 per character/word/line, 支持react/vanillajs
  - This library uses a single canvas-rendered mask-image, so we can do pixel-level fade-in effects.
  - Other libraries can accomplish at most a per-character opacity animation with a HTML soup
  - This library also features a super customizable text splitter API. Pick a built-in splitter (character, word, line, sentence) or provide you own function that splits the visually rendered text on screen.
  - https://x.com/samddenty/status/1905843003471581337
    - I just created a demo website for https://react-ai-flow.com a super advanced cross-framework library for smooth LLM text streaming effects & also text-staggers.

- https://github.com/one-man-studios/Shinzo-UI /NonComm/202512/html
  - A robust, single standalone html file AI interface for Ollama and OpenAI.
  - Features local RAG with vector search, real-time voice/video calls, document analysis (PDF/DOCX), and project workspaces. 
  - Runs entirely in the browser using IndexedDB for privacy and speed—no external backend required.

- https://github.com/ibadoo/llm-msg-analysis /202602/ts/vue
  - https://ibadoo.github.io/llm-msg-analysis/
  - LLM 对话协议可视化分析工具 — 支持解析 Claude、OpenAI、Gemini 的 SSE 流、对话历史和 API 响应
  - [一个将三大厂的请求或响应体可视化的工具 _202602](https://linux.do/t/topic/1575045)
    - 快速翻译。点击一键翻译 prompt。

## llm-md-ext

- https://github.com/zhs007/adarender /apache2/202101/js/inactive
  - 一个开箱即用的markdown渲染器，除了对github的markdown语法支持外，它还有一套自己扩展的图表语法。
  - 可以通过命令行或 grpc 服务 2 种方式来渲染页面。
  - 作为 `markdown-it` 的插件使用
  - adarender插件分为2部分，一部分是node.js这边的模板解析模块，一部分是前端页面js代码。
    - 最初选择的模板引擎是handlebars，实际使用中发现这个引擎太过于古老，有非常多的不方便，后来逐步替换为ejs
# ai-sdk/vendors
- https://github.com/moeru-ai/xsai /MIT/202502/ts
  - https://xsai.js.org/
  - extra-small AI SDK for Browser, Node.js, Deno, Bun or Edge Runtime
  - xsAI is a series of utils to help you use OpenAI or OpenAI-compatible API.
  - xsAI doesn't depend on Node.js Built-in Modules, it works well in Browsers, Deno, Bun and even the Edge Runtime.

## ai-providers/vendors

- https://github.com/BerriAI/litellm /34kStar/MIT+EE/202601/python/ts
  - https://docs.litellm.ai/docs/
  - Python SDK, Proxy Server (LLM Gateway) to call 100+ LLM APIs in OpenAI format - [Bedrock, Azure, OpenAI, VertexAI, Cohere, Anthropic, Sagemaker, HuggingFace, Replicate, Groq]
  - Translate inputs to provider's completion, embedding, and image_generation endpoints
  - Consistent output, text responses will always be available at ['choices'][0]['message']['content']
  - Set Budgets & Rate limits per project, api key, model

- https://github.com/ben-vargas/ai-sdk-provider-claude-code /MIT/202507/ts
  - lets you use Claude via the Vercel AI SDK through the official `@anthropic-ai/claude-code` SDK/CLI.
  - Vercel AI SDK community provider for Claude Code SDK - Use Pro/Max Subscription via SDK
  - This is the v5-beta compatible version. For AI SDK v4 support, use version 0.2.x.
# chat-coding-toolchain
- https://github.com/marc-shade/universal-ai-chat /202511/python/inactive
  - Universal AI Chat MCP Server - Real-time communication between Claude Code, OpenAI Codex CLI, and Gemini CLI
  - Shared Memory: All AIs share a common vector memory via Qdrant
  - Documentation Corpus: Pre-indexed docs for all three CLI tools
  - Conversation History: Full message threading and history

- https://github.com/nervosys/chasm-cli /AGPL/202602/rust
  - Universal CLI for managing AI chat sessions across providers
  - unifying chat sessions from AI coding assistants like GitHub Copilot, Cursor, and more.
  - Extract chat sessions from VS Code, Cursor, Windsurf, and other editors
  - No Lock-in - Universal session format that works across all providers
  - Merge - Combine sessions across workspaces and time periods
  - Real-time Recording - Live session recording to prevent data loss from editor crashes
  - API Server - REST + WebSocket API for building custom integrations
  - SQLite-based storage that normalizes all providers

- https://github.com/jacob-bd/ai-code-connect /MIT/202601/ts
  - A CLI tool that connects Claude Code and Gemini CLI, eliminating manual copy-paste between AI coding assistants.

- https://github.com/monk1337/clicodelog /MIT/202602/python
  - local-first web app to browse, inspect, and export logs from CLI-based AI coding agents — Claude Code, OpenAI Codex, and Gemini CLI.

- https://github.com/kylebrodeur/universal-agent-context /MIT/202602/python/ts
  - Universal context system for AI agents: discover, translate, and manage agent skills across formats. 
  - Includes MCP server, CLI, and Python library.
  - What makes UACS different: It's middleware, not another agent tool
  - It provides format translation, context compression, package management, persistent memory, and MCP server integration in one package - the only solution offering this complete feature set.
  - Bundled Architecture: The Next.js frontend (static export) is served directly from FastAPI - no separate frontend server needed!

- https://github.com/sqlchat/sqlchat /BSL/202406/ts
  - https://sqlchat.ai/
  - Chat-based SQL Client and Editor for the next decade
  - built by Next.js
# chat-apps/domain
- https://github.com/PKU-YuanGroup/ChatLaw
  - https://chatlaw.cloud/lawchat/
  - 中文法律大模型
# vscode-chat
- https://github.com/rusiaaman/chat.md /MIT/202509/ts
  - chat.md is a Visual Studio Code extension that reimagines AI interaction through plain text files. 
  - chat.md embraces a file-first approach where your conversations with AI are just markdown files with a `.chat.md` extension. Edit them, version control them, share them - they're your files. The AI directly writes its response in the file.
  - chat.md treats conversations as first-class files in your workspace
  - Custom APIs: Any OpenAI-compatible endpoint (Azure, Google Gemini, etc.)
# integrations-ww

# integrations-cn
- https://github.com/ILoveBingLu/miyu /MIT/202601/ts
  - 基于 Electron + React + TypeScript 构建的聊天记录查看工具界面，基于原项目 EchoTrace 重构。
  - 数据导出功能
  - 全文搜索界面和交互
  - 依赖electron-builder, Zustand
    - 其他: jieba-wasm (分词), lucide-react (图标)
- https://github.com/hicccc77/WeFlow /CC-NC/202601/ts
  - 完全本地的微信实时聊天记录查看、分析与导出工具。它可以实时获取你的微信聊天记录并将其导出，还可以根据你的聊天记录为你生成独一无二的分析报告
  - 导出聊天记录为 HTML 等格式
  - 本地解密与数据库管理
  - 数据库: better-sqlite3 + WCDB DLL
  - 密语 CipherTalk 为本项目提供了基础框架
# more-chat
- https://github.com/microsoft/TypeChat /MIT/202405/python/ts
  - https://microsoft.github.io/TypeChat/
  - TypeChat is a library that makes it easy to build natural language interfaces using types

- https://github.com/LAION-AI/Open-Assistant /apache2/202401/python/inactive
  - a chat-based assistant that understands tasks, can interact with third-party systems, and retrieve information dynamically to do so.
  - OpenAssistant is completed, and the project is now finished. The final published oasst2 dataset can be found on HuggingFace at OpenAssistant/oasst2
