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
# ui-ai 💄
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
# ai-sdk/vendors
- https://github.com/moeru-ai/xsai /MIT/202502/ts
  - https://xsai.js.org/
  - extra-small AI SDK for Browser, Node.js, Deno, Bun or Edge Runtime
  - xsAI is a series of utils to help you use OpenAI or OpenAI-compatible API.
  - xsAI doesn't depend on Node.js Built-in Modules, it works well in Browsers, Deno, Bun and even the Edge Runtime.

## ai-providers/vendors

- https://github.com/BerriAI/litellm /27.1kStar/MIT+EE/202508/python/ts
  - https://docs.litellm.ai/docs/
  - Python SDK, Proxy Server (LLM Gateway) to call 100+ LLM APIs in OpenAI format - [Bedrock, Azure, OpenAI, VertexAI, Cohere, Anthropic, Sagemaker, HuggingFace, Replicate, Groq]
  - Translate inputs to provider's completion, embedding, and image_generation endpoints
  - Consistent output, text responses will always be available at ['choices'][0]['message']['content']
  - Set Budgets & Rate limits per project, api key, model

- https://github.com/ben-vargas/ai-sdk-provider-claude-code /MIT/202507/ts
  - lets you use Claude via the Vercel AI SDK through the official `@anthropic-ai/claude-code` SDK/CLI.
  - Vercel AI SDK community provider for Claude Code SDK - Use Pro/Max Subscription via SDK
  - This is the v5-beta compatible version. For AI SDK v4 support, use version 0.2.x.
# chat-docs/knowledgebase
- https://github.com/arc53/DocsGPT /17.4kStar/MIT/202511/python/ts/提交多
  - https://app.docsgpt.cloud/
  - https://docsgpt.arc53.com/
  - GPT-powered chat for documentation, chat with your documents
  - open-source AI platform for building intelligent agents and assistants. 
  - 使用langchain的代码不多
  - Wide Format Support: Reads PDF, DOCX, CSV, XLSX, EPUB, MD, RST, HTML, MDX, JSON, PPTX, and images.
  - Web & Data Integration: Ingests from URLs, sitemaps, Reddit, GitHub and web crawlers.
  - Reliable Answers: Get accurate, hallucination-free responses with source citations 
  - Flexible Deployment: Works with major LLMs (OpenAI, Google, Anthropic) and local models (Ollama, llama_cpp).
  - Pre-built Integrations: Use readily available HTML/React chat widgets, search tools, Discord/Telegram bots, and more.
  - Secure & Scalable: Run privately and securely with Kubernetes support
  - Manually updating chunks in the app UI (Feb 2025)
  - [Show HN: DocsGPT, open-source documentation assistant, fully aware of libraries | Hacker News _202302](https://news.ycombinator.com/item?id=34648266)

- https://github.com/PromtEngineer/localGPT /22kStar/MIT/202507/python/ts/提交少/inactive
  - LocalGPT is a fully private, on-premise Document Intelligence platform. 
  - Ask questions, summarise, and uncover insights from your files with AI—no data ever leaves your machine.
  - LocalGPT features a hybrid search engine that blends semantic similarity, keyword matching, and Late Chunking for long-context precision
  - A smart router automatically selects between RAG and direct LLM answering for every query, while contextual enrichment and sentence-level Context Pruning surface only the most relevant content
  - An independent verification pass adds an extra layer of accuracy.
  - The architecture is modular and lightweight—enable only the components you need. With a pure-Python core and minimal dependencies
  - 🏠 The RAG system is pure python and does not require any additional dependencies.
  - models via Ollama.
  - Chat History: Remembers your previous conversations (in a session).
  - API: LocalGPT has an API that you can use for building RAG Applications.
  - GPU, CPU, HPU & MPS Support
  - Multi-format Support: PDF, DOCX, TXT, Markdown, and more (Currently only PDF is supported)
  - Contextual Enrichment: Enhanced document understanding with AI-generated context, inspired by Contextual Retrieval
  - Batch Processing: Handle multiple documents simultaneously
  - Smart Routing: Automatically chooses between RAG and direct LLM responses
  - Query Decomposition: Breaks complex queries into sub-questions for better answers
  - Intuitive Web UI: Clean, responsive design
  - Real-time Chat: Streaming responses for immediate feedback

- https://github.com/Cinnamon/kotaemon /23kStar/apache2/202507/python/提交少/inactive
  - https://cinnamon.github.io/kotaemon/
  - https://huggingface.co/spaces/cin-model/kotaemon-demo
  - open-source clean & customizable RAG UI for chatting with your documents. Built with both end users and developers in mind.
  - This project serves as a functional RAG UI for both end users who want to do QA on their documents and developers who want to build their own RAG pipeline.
  - Minimalistic UI: A user-friendly interface for RAG-based QA.
  - Support for Various LLMs: Compatible with LLM API providers (OpenAI, AzureOpenAI, Cohere, etc.) and local LLMs (via `ollama` and `llama-cpp-python`).
  - Framework for RAG Pipelines: Tools to build your own RAG-based document QA pipeline.
  - Customizable UI: See your RAG pipeline in action with the provided UI, built with `Gradio`.
  - Host your own document QA (RAG) web-UI: Support multi-user login, organize your files in private/public collections, collaborate and share your favorite chat with others.
  - Hybrid RAG pipeline: Sane default RAG pipeline with hybrid (full-text & vector) retriever 
  - Advanced citations with document preview: By default the system will provide detailed citations to ensure the correctness of LLM answers.
  - Extensible: Being built on `Gradio`, you are free to customize or add any UI elements as you like.
  - require `Unstructured` if you want to process files other than .pdf, .html, .mhtml, and .xlsx documents.
    - We support both `lite` & `full` version of Docker images. With `full` version, the extra packages of `unstructured` will be installed, which can support additional file types (`.doc, .docx`, ...)
  - [Kotaemon: An open-source RAG-based tool for chatting with your documents | Hacker News _202501](https://news.ycombinator.com/item?id=42571272)
  - [Kotaemon-papers: an open-source web app to chat with your academic papers | Hacker News _202501](https://news.ycombinator.com/item?id=42603357)
    - Our team has been working on a public demo to showcase the new advanced citation features in our RAG

- https://github.com/h2oai/h2ogpt /11.9kStar/apache2/202503/python/inactive
  - http://h2o.ai/
  - [Gradio Demo](https://gpt.h2o.ai/)
  - [OpenWebUI Demo](https://gpt-docs.h2o.ai/)
  - Query and summarize your documents or just chat with local private GPT LLMs using h2oGPT
  - Private offline database of any documents (PDFs, Excel, Word, Images, Video Frames, YouTube, Audio, Code, Text, MarkDown, etc.)
  - Persistent database (Chroma, Weaviate, or in-memory FAISS) using accurate embeddings (instructor-large, all-MiniLM-L6-v2, etc.)
  - Efficient use of context using instruct-tuned LLMs (no need for LangChain's few-shot approach)
  - Parallel summarization and extraction, reaching an output of 80 tokens per second with the 13B LLaMa2 model
  - Gradio UI or CLI with streaming of all models

- https://github.com/GitHamza0206/simba /1.4kStar/apache2/202505/python/jupyter/inactive
  - https://simba.mintlify.app/
  - Portable KMS (knowledge management system) designed to integrate seamlessly with any RAG
  - Modular Architecture: Flexible integration of vector stores, embedding models, chunkers, and parsers.

- https://github.com/labring/FastGPT /25.5kStar/apache2+LOGO+nonTenant/202508/ts
  - https://fastgpt.io/
  - 一个 AI Agent 构建平台，提供开箱即用的数据处理、模型调用等能力，同时可以通过 Flow 可视化进行工作流编排，从而实现复杂的应用场景
  - 项目技术栈：NextJs + TS + ChakraUI + MongoDB + PostgreSQL (PG Vector 插件)/Milvus
  - ⚖️ License
    - 允许作为后台服务直接商用，但不允许提供 SaaS 服务

- https://github.com/QuivrHQ/quivr /38.4kStar/apache2/202506/python
  - https://core.quivr.com/
  - Opiniated RAG for integrating GenAI in your apps
  - Opiniated RAG: We created a RAG that is opinionated, fast and efficient so you can focus on your product
  - LLMs: Quivr works with any LLM, you can use it with OpenAI, Anthropic, Mistral, Gemma, etc.
  - Any File: Quivr works with any file, you can use it with PDF, TXT, Markdown, etc and even add your own parsers.
  - Customize your RAG: Quivr allows you to customize your RAG, add internet search, add tools, etc.

- https://github.com/pingcap/autoflow /2.6kStar/apache2/202507/python
  - https://tidb.ai/
  - a Graph RAG based and conversational knowledge base tool built with TiDB Serverless Vector Storage.
  - An open source GraphRAG (Knowledge Graph) built on top of TiDB Vector and LlamaIndex and DSPy.
  - UI交互类似chatgpt
  - https://x.com/9hills/status/1862522244527972625
    - RAG Demo 到 RAG Application 难度的完美表现，其实功能不算丰富（增加了 Graph RAG和 Agent RAG 的思想），
    - 代码却不得不做的非常复杂，大部分其实是应用逻辑。 P. S. 代码已经成熟到可以直接抄了，直接复刻就完了

- https://github.com/dontizi/rlama /1.1kStar/apache2/202508/go/js
  - https://rlama.dev/
  - a powerful AI-driven question-answering tool for your documents, seamlessly integrating with your local Ollama models.
  - It enables you to create, manage, and interact with Retrieval-Augmented Generation (RAG) systems tailored to your documentation needs.
  - This project is currently on pause due to my work and university commitments that take up a lot of my time
  - [RLAMA -- A document AI question-answering tool that connects to your local Ollama models. : r/ollama _202503](https://www.reddit.com/r/ollama/comments/1j66pg3/rlama_a_document_ai_questionanswering_tool_that/)
    - I developed RLAMA to solve a straightforward but frustrating problem: how to easily query my own documents with a local LLM without using cloud services.
    - RLAMA extracts text from the documents and generates embeddings via Ollama
    - it uses Tesseract OCR to extract text from image-based PDFs or scanned documents where text can't be directly selected.

- https://github.com/morphik-org/morphik-core /3.2kStar/BSL/202508/python/ts
  - https://morphik.ai/docs
  - The most accurate document search and store for building AI apps
  - We are building the best way for developers to integrate context (however complex and nuanced) into their AI applications. 
  - Morphik provides developers the tools to ingest, search (deep and shallow), transform, and manage unstructured and multimodal documents.
  - Multimodal Search: We employ techniques such as ColPali to build search that actually understands the visual content of documents you provide. Search over images, PDFs, videos, and more

- https://github.com/jorge-armando-navarro-flores/chat_with_your_docs /MIT/202409/python
  - ChatWithYourDocs Chat App is a Python application that allows you to chat with multiple Docs formats like PDF, WEB pages and YouTube videos. 
  - This app utilizes a language model to generate accurate answers to your queries

- https://github.com/zylon-ai/private-gpt /56.5kStar/apache2/202409/python/inactive
  - a production-ready AI project that allows you to ask questions about your documents using LLM
  - Conceptually, PrivateGPT is an API that wraps a RAG pipeline and exposes its primitives.
    - The API is built using FastAPI and follows OpenAI's API scheme.
    - The RAG pipeline is based on LlamaIndex.
  - The design of PrivateGPT allows to easily extend and adapt both the API and the RAG implementation.
    - Dependency Injection, decoupling the different components and layers.
    - Usage of `LlamaIndex` abstractions such as `LLM, BaseEmbedding or VectorStore`, making it immediate to change the actual implementations of those abstractions.
    - Ready to use, providing a full implementation of the API and RAG pipeline.
  - The project provides an API offering all the primitives required to build private, context-aware AI applications. 
  - It follows and extends the OpenAI API standard, and supports both normal and streaming responses.

- https://github.com/thiswillbeyourgithub/WDoc /478Star/GPL/202507/python
  - https://wdoc.readthedocs.io/en/stable/
  - Summarize and query from a lot of heterogeneous documents. 
  - Any LLM provider, any filetype, advanced RAG, advanced summaries, scriptable, etc
  - Created by a medical student who needed a way to get a definitive answer from multiple sources at the same time (audio recordings, video lectures, Anki flashcards, PDFs, EPUBs, etc.). wdoc was born from frustration with existing RAG solutions for querying and summarizing.
  - It uses mostly `LangChain` and `LiteLLM` as backends.
  - High recall and specificity: it was made to find A LOT of documents using carefully designed embedding search then carefully aggregate gradually each answer using semantic batch to produce a single answer that mentions the source pointing to the exact portion of the source document.
    - Use both an expensive and cheap LLM to make recall as high as possible because we can afford fetching a lot of documents per query (via embeddings)
  - Extensible: this is both a tool and a library. It was even turned into an Open-WebUI Tool
  - Web Search: Preliminary web search support using DuckDuckGo (via the ddgs library)

- https://github.com/kqlade/dory-frontend /AGPL/202504/ts/inactive
  - [Dory – AI Knowledge Base Powered by Browser History | Hacker News _202504](https://news.ycombinator.com/item?id=43619021)
  - Dynamic Online Recall for You (DORY) helps you find anything you've seen before online using whatever you remember about it. 
  - DORY also builds a cognitive context graph to organize your work into auto-updating workflows and serve them to you in real time based on your browsing context.
  - DORY uses Neo4j to store browsing data with weighted edge relationships (semantic, behavioral, temporal) then applies stochastic block modeling for community detection and temporal-behavioral profiling.
  - It's an approach similar to how banks analyze transaction networks to detect fraud but works surprisingly well for teasing apart browser workflows.

- https://github.com/Zipstack/unstract /5.9kStar/AGPL/202511/python
  - https://unstract.com/
  - No-code LLM Platform to launch APIs and ETL Pipelines to structure unstructured documents

- https://github.com/Tencent/WeKnora /7.5kStar/MIT/202511/go/ts/vue
  - https://weknora.weixin.qq.com/
  - LLM-powered framework for deep document understanding, semantic retrieval, and context-aware answers using RAG paradigm

- https://github.com/freeCodeCamp/devdocs /37.9kStar/MPL/202511/ruby
  - https://devdocs.io/
  - DevDocs combines multiple developer documentations in a clean and organized web UI with instant search, offline support, mobile version, dark theme, keyboard shortcuts, and more
  - DevDocs was created by Thibaut Courouble and is operated by freeCodeCamp.

- https://github.com/AdyTech99/volo /GPL/202501/python/inactive
  - combining AI with Wikipedia knowledge via a RAG pipeline
  - It utilizes an offline database of Wikipedia created by Kiwix, ensuring fast and reliable access to information without requiring constant internet connectivity.
  - Volo uses a tiny model (Qwen2.5:3b) and gives it the knowledge of nearly 7 million Wikipedia articles, making it a more reliable source of information than giant closed-source models like OpenAI's GPT4o and Anthropic's Claude 3.5 Sonnet, which are prone to hallucinations.
  - Offline Wikipedia Database: Leverages a `.zim` file from Kiwix, offering a snapshot of Wikipedia for offline access.
  - OpenAI-Compatible REST APIs: Use Volo with interfaces like Open WebUI or your own API client.
# chat-excel
- https://github.com/huggingface/aisheets /1.5kStar/apache2/202510/python/ts
  - https://huggingface.co/spaces/aisheets/sheets
  - an open-source tool for building, enriching, and transforming datasets using AI models with no code. 
  - The tool can be deployed locally or on the Hub. 
  - By default, AI Sheets is configured to use the Huggingface Inference Providers API to run inference on the latest open-source models. However, you can also run Sheets with own custom LLMs, such as those hosted on your own infrastructure or other cloud providers. The only requirement is that your LLMs must support the OpenAI API specification.
  - This app has a minimal Expressjs server implementation

- https://github.com/weijunext/smart-excel-ai /MIT/202312/ts
  - https://smartexcel.cc/
  - Generate the Excel formulas you need in seconds using ChatGPT
  - https://twitter.com/weijunext/status/1744225202228089173
    - 这是一个足够简单（调用ChatGPT的API）却又功能俱全（有登录和支付）的demo级产品。
    - 前后端：Next.js+Tailwind+Prisma
    - 登录：Next-Auth
    - 支付：Lemon Squeezy
    - 部署：Vercel
# chat-pdf
- https://github.com/bhaskatripathi/pdfGPT /7.1kStar/MIT/202305/python/过于简单/inactive
  - https://huggingface.co/spaces/bhaskartripathi/pdfChatter
  - PDF GPT allows you to chat with the contents of your PDF file by using GPT capabilities

- https://github.com/shibing624/ChatPDF /801Star/apache2/202409/python/inactive
  - 纯原生实现RAG功能，基于本地LLM、embedding模型、reranker模型实现，支持GraphRAG，无须安装任何第三方agent库。
  - 本项目实现了轻量版的GraphRAG
  - 支持local模式的关系图检索的文档问答
  - 支持Openai API, Deepseek API, Ollama API等，可自行扩展支持更多LLM
  - 支持openai embedding、本地 text2vec embedding、huggingface embedding、sentence-transformers embedding等
  - 本项目支持多种文件格式，包括PDF、docx、markdown、txt等
  - 优化了RAG准确率: Chinese chunk切分优化，适配中英文混合文档
  - 本项目基于`gradio`开发了RAG对话页面，支持流式对话

- https://github.com/mayooear/ai-pdf-chatbot-langchain /15.8kStar/MIT/202502/ts
  - PDF chatbot agent built with LangChain & LangGraph
  - This monorepo is a customizable template example of an AI chatbot agent that "ingests" PDF documents, stores embeddings in a vector database (Supabase), and then answers user queries using OpenAI (or another LLM provider) utilising LangChain and LangGraph as orchestration frameworks.
  - This template is also an accompanying example to the book Learning LangChain (O'Reilly): Building AI and LLM applications with LangChain and LangGraph.

- https://github.com/williamcaseylucas/quill-pdf-chat /202401/ts
  - 依赖prisma, shadcn-ui, react-pdf, AWS S3 buckets
  - https://github.com/khaledmk20/quill
    - Quill redefines PDF interaction with intelligent conversations.

- https://github.com/Byaidu/PDFMathTranslate /29.8kStar/AGPLv3/202511/python 
  - https://pdf2zh.com/
  - 基于 AI 完整保留排版的 PDF 文档全文双语翻译，支持 Google/DeepL/Ollama/OpenAI 等服务，提供 CLI/GUI/MCP/Docker/Zotero
  - Preserve formulas, charts, table of contents, and annotations
  - Support multiple languages, and diverse translation services.
  - https://github.com/PDFMathTranslate/PDFMathTranslate-next /AGPLv3
    - pdf2zh 2.0 does not currently provide an online demo
# chat-workspace
- https://github.com/pipeshub-ai/pipeshub-ai /2kStar/apache2/202511/python/ts
  - https://pipeshub.com/
  - The OpenSource Alternative to Glean's Workplace AI
  - PipesHub AI helps you quickly find the right information using natural language search—just like Google.
  - The platform not only delivers the most relevant results but also shows where the information came from, with proper citations, using Knowledge Graphs and Page Ranking
  - Beyond search, our platform allows enterprises to create custom apps and AI agents using a No-Code interface.
  - Knowledge Graph Backbone – All data is seamlessly structured into a powerful knowledge graph.
  - Enterprise-Grade Connectors – Scalable, reliable, and built for secure access across your organization.
  - Modular & Scalable Architecture – Every service is loosely coupled to scale independently and adapt to your needs.
  - 前端: Material UI、React Hook Form、zod
  - 后端: fastapi, LangGraph, LangChain, Qdrant(vector), ArangoDB(graph), Kafka, Redis, Docling, PyMuPDF, OCRmyPDF
  - 🛢️ 应用层数据在python侧和nodejs侧都大量使用arangodb来存储图结构的关系
  - 🐛 不支持外部搜索引擎如 Tavily/EXA/SearxNG, 但方便纯本地部署
  - [Work AI for all - AI platform for agents, assistant, search](https://www.glean.com/)
  - [Best way to extract data from PDFs and HTML : r/Rag _202510](https://www.reddit.com/r/Rag/comments/1oavnx4/best_way_to_extract_data_from_pdfs_and_html/)
    - At PipesHub, we use docling, pymupdf (faster than docling but need to use layout parser on top of it), ocrmupdf/Azure DI (scanned pdfs).
    - If you are looking for Higher Accuracy, Visual Citations, Cleaner UI, Direct integration with Google Drive, OneDrive, SharePoint Online, Dropbox and more. PipesHub is free and fully open source, extensible. 
  - pr已合并 [Backend Support for Ollama Models · Pull Request _202507](https://github.com/pipeshub-ai/pipeshub-ai/pull/475)
    - [Ollama Embedding model support · Pull Request ](https://github.com/pipeshub-ai/pipeshub-ai/pull/480)

- https://github.com/MODSetter/SurfSense /10.6kStar/apache2/202511/python/ts
  - https://www.surfsense.com/
  - Open source alternative to NotebookLM, Perplexity, and Glean.
  - Connects to search engines, Slack, Linear, Jira, ClickUp, Notion, YouTube, GitHub, Discord, and more. 
  - Save content from your own personal files (Documents, images, videos and supports 50+ file extensions) to your own personal knowledge base .
  - ⛓️ Get Cited answers just like Perplexity.
  - Works Flawlessly with Ollama local LLMs.
  - 后端: FastAPI, SQLAlchemy, pgvector, LangGraph, LangChain, Hybrid Search, Rerankers, Redis
  - 前端: next, Vercel AI SDK Kit UI Stream Protocol, Shadcn, Framer Motion, React Hook Form, tanstack/table
  - ETL Service (choose one)
    - Docling (local processing, no API key required, supports PDF, Office docs, images, HTML, CSV)
    - LlamaIndex API key (enhanced parsing, supports 50+ formats)
  - 👇 xp
    - 跨workspace不能共享source-document
    - 聊天时~~只能选择全部文档或不选文档，不~~可以只选择部分文档
    - 支持根据场景配置不同llm: fast, long, reasoning
    - 🐛 聊天中的内容支持点击跳转到文档的chunk位置，而不是源文件，且中文文档的chunk经常是乱码
  - https://discord.com/channels/1359368468260192417/1359416865939787837/1409642464792412220
    - I was considering installing Surfsense but it needs API keys, doesn't it? How much does it cost to use it?
    - Every service has a local alternative other than Speech to Text service. No need to put any API keys if you use everything local.

- https://github.com/lfnovo/open-notebook /10.2kStar/MIT/202511/python/ts/提交少
  - https://www.open-notebook.ai/
  - Open Source implementation of Notebook LM with more flexibility and features
  - AI-powered note-taking/research platform that respects your privacy

- https://github.com/rmusser01/tldw_server /1.1kStar/GPL/202511/python
  - https://tldwproject.com/
  - Too Long; Didn't Watch - API-first media analysis & research platform
  - tldw_server is an open-source research multi-tool / backend for ingesting, transcribing, analyzing, and retrieving knowledge from video, audio, documents, websites, and more.
  - It consists of a FastAPI API-first server architecture backed by SQLite or Postgres depending on user choice, with OpenAI-compatible Chat and Audio APIs, a unified RAG pipeline, knowledge management, and integrations with local or hosted LLM providers (with cost/usage tracking).
  - https://github.com/the-crypt-keeper/tldw /inactive

- https://github.com/CaviraOSS/PageLM /NonCommercial/202511/ts
  - https://pagelm.spotit.dev/
  - a community driven version of NotebookLM & a education platform that transforms study materials into interactive resources like quizzes, flashcards, notes, and podcasts.

- https://github.com/souzatharsis/podcastfy /5.6kStar/apache2/202510/python
  - Open Source Python alternative to NotebookLM's podcast feature: Transforming Multimodal Content into Captivating Multilingual Audio Conversations with GenAI
  - https://github.com/gabrielchua/open-notebooklm
    - Convert any PDF into a podcast episode

- https://github.com/run-llama/notebookllama /1.6kStar/MIT/202508/python/inactive
  - open-source, LlamaCloud-backed alternative to NotebookLM
  - [NotebookLlama: An open source version of NotebookLM | Hacker News _202410](https://news.ycombinator.com/item?id=41964980)

- https://github.com/xynehq/xyne /635Star/apache2/202511/ts
  - https://xynehq.com/
  - AI-first Search & Answer Engine for work. 
  - Open-source alternative to Glean, Gemini and MS Copilot
  - Your work information has become fragmented — across so many SaaS apps, docs, files, repos
  - Xyne connects to your applications (Google Workspace, Atlassian suite, Slack, Github, etc), securely indexes your data, and maps a graph of relationships.
  - 🐛 必须使用google账户登录才能使用?
    - 似乎不支持上传本地pdf文件
  - Model Agnostic: Plugs into any LLM of your choice. You can even point it to a local Deepseek via ollama.
  - 使用自研ai框架 jaf  结合 aisdk
  - https://github.com/xynehq/jaf
    - functional agent framework built on immutable state, type safety, and composable policies.

- https://github.com/deta/surf /2.7kStar/apache2/202511/rust/ts/svelte
  - https://deta.surf/
  - Personal AI Notebooks. Organize files & webpages and generate notes from them. 
  - built in Svelte, TypeScript and Rust, runs on MacOS, Windows & Linux, stores data locally in open formats 
  - PDF Notes: open a PDF and ask a question
  - Create an applet: use the "app generation" tool and ask for an app
  - [Show HN: Deta Surf – An open source and local-first AI notebook | Hacker News _202510](https://news.ycombinator.com/item?id=45680937)
    - We took inspiration from analog notebooks as a tool for thought, but wanted something for multi-media. We also see NotebookLM as the closest mainstream product to Surf.
    - 🆚 The big difference UX wise between chatbots and Surf is that Surf is built entirely on editable documents that you can mold / craft into an output (vs chat).
      - We actually had a chatbot, but our explorations showed that notes were a more effective in many cases!
    - Is this an open source equivalent to google’s NotebookLM? I can tell. How does it stack up features wise?
      - Surf is built entirely on editable WYSIWYG documents, NotebookLM's main AI is built on chat. Surf is built to be a bit more open, NotebookLM was a bit locked down for our taste.
      - An example I'd highlight is taking notes against a PDF.
      - NotebookLM will convert the PDF to simple text, and the chat responses are read only. NotebookLM also has a lot of strict walls between chat, artifacts & sources. You have to "save" responses as (read only) notes, and move notes to sources.
      - With Surf you can generate notes that deep link to specific pages in the PDF, and Surf will open those pages in the original PDF. You can remove the fluff you don't want in your notes. The intention is to be a little more open -- all notes are sources from the get go, you don't have to save or migrate anything.

- https://github.com/ItzCrazyKns/Perplexica /27.3kStar/MIT/202511/ts
  - Open source alternative to Perplexity AI
  - a privacy-focused AI answering engine that runs entirely on your own hardware. It combines knowledge from the vast internet with support for local LLMs (Ollama) and cloud providers (OpenAI, Claude, Groq), delivering accurate answers with cited sources while keeping your searches completely private
  - Web search powered by SearxNG - Support for Tavily and Exa coming soon
  - Upload documents and ask questions about them. PDFs, text files, images - Perplexica understands them all.
    - 未使用docling/libreoffice
  - Get intelligent search suggestions as you type, helping you formulate better queries.
  - Perplexica also provides an API for developers looking to integrate its powerful search engine into their own applications.
  - Perplexica runs on Next.js and handles all API requests.
  - 🐛 官方未提供外部数据源的集成，如slack/notion/gmail
    - [Add private search connectors _202508](https://github.com/ItzCrazyKns/Perplexica/issues/856)

- https://github.com/zaidmukaddam/scira /11.4kStar/apache2/202511/ts
  - https://scira.ai/
  - Scira (Formerly MiniPerplx) is a minimalistic AI-powered search engine that helps you find information on the internet and cites it too. 
  - Powered by Vercel AI SDK
  - using multiple AI models including xAI's Grok, Anthropic's Claude, Google's Gemini, and OpenAI's GPT models
  - Search the web using Exa's API with support for multiple queries, search depths, and topics
  - Extract and analyze content from any URL using Exa AI with live crawling capabilities
    - Search Reddit content with time range filtering using Tavily API
    - X (Twitter) search: Search X posts with date ranges and specific handle filtering using xAI Live Search
  - Advanced multi-step search capability for complex queries
  - Academic search: Search for academic papers and research using Exa AI with abstracts and summaries
  - YouTube search: Find YouTube videos with detailed information, captions, and timestamps powered by Exa AI
# chat-coding-toolchain
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
# citation/sourcing
- https://github.com/Future-House/paper-qa /7.8kStar/apache2/202511/python
  - https://futurehouse.gitbook.io/futurehouse-cookbook
  - PaperQA2 is a package for doing high-accuracy retrieval augmented generation (RAG) on PDFs, text files, Microsoft Office documents, and source code files, with a focus on the scientific literature.
  - PaperQA2 is engineered to be the best agentic RAG model for working with scientific papers. 
# more-chat
- https://github.com/microsoft/TypeChat /MIT/202405/python/ts
  - https://microsoft.github.io/TypeChat/
  - TypeChat is a library that makes it easy to build natural language interfaces using types

- https://github.com/LAION-AI/Open-Assistant /apache2/202401/python/inactive
  - a chat-based assistant that understands tasks, can interact with third-party systems, and retrieve information dynamically to do so.
  - OpenAssistant is completed, and the project is now finished. The final published oasst2 dataset can be found on HuggingFace at OpenAssistant/oasst2
