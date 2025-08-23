---
title: lib-ai-app-examples-chat
tags: [ai, chat, chatgpt, examples]
created: 2025-03-22T18:49:02.969Z
modified: 2025-03-22T18:49:15.634Z
---

# lib-ai-app-examples-chat

# guide

# popular
- https://github.com/open-webui/open-webui /107kStar/MIT > BSD+LOGO/202405/python/svelte
  - https://openwebui.com/
  - User-friendly WebUI for LLMs (Formerly Ollama WebUI)
  - extensible, feature-rich, and user-friendly self-hosted WebUI designed to operate entirely offline. 
  - 后端tavily搜索部分用到了langchain，langchain整体仅7个文件
  - It supports various LLM runners, including Ollama and OpenAI-compatible APIs
  - 🌹 pros: comfyui
  - 🐛 cons: MCP
  - [Open WebUI changed license from BSD-3 to Open WebUI license with CLA | Hacker News _202505](https://news.ycombinator.com/item?id=43901575)
    - What really is the moat of openwebui? I have seen at least 4 - 5 react UIs with similar functionality (chat, RAG, document library).
    - Not sure about the moat, it's mostly a SvelteKit web app with extra utils after all. But it has a rather unique combination of advanced features (RAG integrations, workspaces, pipelines, code execution, MCP integration, etc.) and a user-friendly "production grade" interface. 
    - They swapped out MIT for BSD-3 just five months ago
  - 🍴 forks
  - https://github.com/AI3clauseBSD/claused-webai /inactive
  - 🔧
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

- https://github.com/danny-avila/LibreChat /29kStar/MIT/202508/ts
  - https://librechat.ai/
  - Enhanced ChatGPT Clone: Features Agents, DeepSeek, Anthropic, Gemini
  - 后端依赖@langchain/core、express、keyv、EventSource(sse)、diff
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
  - [Model Context Protocol (MCP)](https://www.librechat.ai/docs/features/mcp)
    - LibreChat leverages MCP to dramatically expand what your AI agents can do, allowing you to integrate everything from file system access, web browsers, specialized APIs, to custom business tools.
    - Any time you add or edit an MCP server, you will need to restart LibreChat to initialize the connections.
  - [Enhancement: Extend Stable Diffusion plugin to work with ComfyUI _202405](https://github.com/danny-avila/LibreChat/issues/2672)
    - We already support Stable Diffusion. It will be great to add support for ComfyUI.
    - /not-planned

- https://github.com/Mintplex-Labs/anything-llm /47.8kStar/MIT/202508/js/python
  - https://anythingllm.com/
  - A full-stack application that enables you to turn any document, resource, or piece of content into context that any LLM can use as a reference during chatting
    - An efficient, customizable, and open-source enterprise-ready document chatbot solution.
  - 基于langchain实现

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

- https://github.com/microsoft/vscode-copilot-chat /8.3kStar/MIT/202508/ts
  - GitHub Copilot Chat (this extension) - A companion extension that provides conversational AI assistance.

- https://github.com/samdenty/react-ai-flow /202503/ts
  - https://react-ai-flow.com/
  - smooth React AI chatbot primitives
  - 支持多种打字动画效果 per character/word/line, 支持react/vanillajs
  - This library uses a single canvas-rendered mask-image, so we can do pixel-level fade-in effects.
  - Other libraries can accomplish at most a per-character opacity animation with a HTML soup
  - This library also features a super customizable text splitter API. Pick a built-in splitter (character, word, line, sentence) or provide you own function that splits the visually rendered text on screen.
  - https://x.com/samddenty/status/1905843003471581337
    - I just created a demo website for https://react-ai-flow.com a super advanced cross-framework library for smooth LLM text streaming effects & also text-staggers.

- https://github.com/langchain-ai/chat-langchain /6kStar/MIT/202508/python/ts
  - https://chat.langchain.com/
  - an implementation of a chatbot specifically focused on question answering over the LangChain documentation. 
  - Built with LangChain, LangGraph, and Next.js.
  - https://github.com/langchain-ai/chat-langchainjs /MIT/202503/ts/inactive
    - https://chatjs.langchain.com/
    - Built with LangChainjs, and Next.js.
# ui-ai 💄
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
# ai-sdk
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

## port-lang

- https://github.com/python-ai-sdk/sdk /MIT/202508/python
  - https://pythonaisdk.mintlify.app/
  - The Vercel AI SDK, in Python
  - A pure Python re-implementation of Vercel's popular AI SDK for TypeScript. 
  - Zero-configuration functions that work consistently across providers with first-class streaming, tool-calling, and structured output support.
  - Strong Pydantic types throughout: Strict structured-output generation and streaming via Pydantic models
  - Provider-agnostic embeddings with built-in batching & retry logic
  - Tiny dependency footprint - no bloated external frameworks

- https://github.com/jetify-com/ai /115Star/apache2/202508/go
  - https://www.jetify.com/
  - a unified interface for interacting with multiple AI providers including OpenAI, Anthropic, and more. 
  - Inspired by Vercel's AI SDK for TypeScript, we bring a similar developer experience to the Go ecosystem.
  - Provider abstraction - Common interfaces for language models, embeddings, and image generation
  - Multi-modal by default - First-class support for text, images, files, and structured outputs across all providers
  - Extensible architecture - Clean interfaces make it easy to add new providers while maintaining backward compatibility

- https://github.com/ClickHouse/ai-sdk-cpp /87Star/apache2/202507/cpp
  - a modern C++ toolkit designed to help you build AI-powered applications with popular model providers like OpenAI and Anthropic. 
  - [Show HN: A modern C++20 AI SDK (GPT‑4o, Claude 3.5, tool‑calling) | Hacker News _202506](https://news.ycombinator.com/item?id=44412726)
    - inspired by Vercel's AI SDK, and litellm
# chat-docs/knowledge-base
- https://github.com/labring/FastGPT /25.5kStar/apache2+LOGO+nonTenant/202508/ts
  - https://fastgpt.io/
  - 一个 AI Agent 构建平台，提供开箱即用的数据处理、模型调用等能力，同时可以通过 Flow 可视化进行工作流编排，从而实现复杂的应用场景
  - 项目技术栈：NextJs + TS + ChakraUI + MongoDB + PostgreSQL (PG Vector 插件)/Milvus
  - ⚖️ License
    - 允许作为后台服务直接商用，但不允许提供 SaaS 服务

- https://github.com/jorge-armando-navarro-flores/chat_with_your_docs /MIT/202409/python
  - ChatWithYourDocs Chat App is a Python application that allows you to chat with multiple Docs formats like PDF, WEB pages and YouTube videos. 
  - This app utilizes a language model to generate accurate answers to your queries

- https://github.com/arc53/DocsGPT /MIT/python/ts
  - https://docsgpt.arc53.com/
  - GPT-powered chat for documentation, chat with your documents

- https://github.com/pingcap/autoflow /apache2/202411/python
  - https://tidb.ai/
  - a Graph RAG based and conversational knowledge base tool built with TiDB Serverless Vector Storage.
  - An open source GraphRAG (Knowledge Graph) built on top of TiDB Vector and LlamaIndex and DSPy.
  - UI交互类似chatgpt
  - https://x.com/9hills/status/1862522244527972625
    - RAG Demo 到 RAG Application 难度的完美表现，其实功能不算丰富（增加了 Graph RAG和 Agent RAG 的思想），
    - 代码却不得不做的非常复杂，大部分其实是应用逻辑。 P. S. 代码已经成熟到可以直接抄了，直接复刻就完了

- https://github.com/dontizi/rlama /202503/go
  - RLAMA is a powerful AI-driven question-answering tool for your documents, seamlessly integrating with your local Ollama models. 
  - It enables you to create, manage, and interact with Retrieval-Augmented Generation (RAG) systems tailored to your documentation needs.
# chat-excel
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
- https://github.com/mayooear/ai-pdf-chatbot-langchain /15.8kStar/MIT/202502/ts
  - PDF chatbot agent built with LangChain & LangGraph
  - This monorepo is a customizable template example of an AI chatbot agent that "ingests" PDF documents, stores embeddings in a vector database (Supabase), and then answers user queries using OpenAI (or another LLM provider) utilising LangChain and LangGraph as orchestration frameworks.
  - This template is also an accompanying example to the book Learning LangChain (O'Reilly): Building AI and LLM applications with LangChain and LangGraph.

- https://github.com/williamcaseylucas/quill-pdf-chat /202401/ts
  - 依赖prisma, shadcn-ui, react-pdf, AWS S3 buckets
  - https://github.com/khaledmk20/quill
    - Quill redefines PDF interaction with intelligent conversations.
# chat-coding-toolchain
- https://github.com/sqlchat/sqlchat /BSL/202406/ts
  - https://sqlchat.ai/
  - Chat-based SQL Client and Editor for the next decade
  - built by Next.js
# chat-apps/domain
- https://github.com/PKU-YuanGroup/ChatLaw
  - https://chatlaw.cloud/lawchat/
  - 中文法律大模型
# more-chat
- https://github.com/microsoft/TypeChat /MIT/202405/python/ts
  - https://microsoft.github.io/TypeChat/
  - TypeChat is a library that makes it easy to build natural language interfaces using types

- https://github.com/LAION-AI/Open-Assistant /apache2/202401/python/inactive
  - a chat-based assistant that understands tasks, can interact with third-party systems, and retrieve information dynamically to do so.
  - OpenAssistant is completed, and the project is now finished. The final published oasst2 dataset can be found on HuggingFace at OpenAssistant/oasst2
