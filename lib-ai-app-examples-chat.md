---
title: lib-ai-app-examples-chat
tags: [ai, chat, chatgpt, examples]
created: 2025-03-22T18:49:02.969Z
modified: 2025-03-22T18:49:15.634Z
---

# lib-ai-app-examples-chat

# guide

# popular
- https://github.com/ChatGPTNextWeb/NextChat /MIT/202503/ts/tauri
  - https://nextchat.club/
  - Light and Fast AI Assistant. 
  - Support: Web | iOS | MacOS | Android | Linux | Windows
  - NextChat Support MCP
  - Fully compatible with self-deployed LLMs, recommended for use with RWKV-Runner or LocalAI
  - Privacy first, all data is stored locally in the browser
  - Enterprise Edition
    - Permission Control: Clearly defined member permissions, resource permissions
    - Security Auditing: Automatically intercept sensitive inquiries and trace all historical conversation records
    - Private Deployment: Enterprise-level private deployment supporting various mainstream private cloud solutions

- https://github.com/lobehub/lobe-chat /apache2+NonModify/202406/ts
  - https://chat-preview.lobehub.com/
  - An open-source, modern-design ChatGPT/LLMs UI/Framework.
  - Supports speech-synthesis, multi-modal, and extensible (function call) plugin system.
  - One-click FREE deployment of your private
  - https://github.com/lobehub/chat-plugin-sdk
    - https://chat-plugin-sdk.lobehub.com/
    - SDK for LobeChat function calling plugins

- https://github.com/LAION-AI/Open-Assistant /apache2/202401/python
  - a chat-based assistant that understands tasks, can interact with third-party systems, and retrieve information dynamically to do so.
  - OpenAssistant is completed, and the project is now finished. The final published oasst2 dataset can be found on HuggingFace at OpenAssistant/oasst2

- https://github.com/microsoft/TypeChat /MIT/202405/python/ts
  - https://microsoft.github.io/TypeChat/
  - TypeChat is a library that makes it easy to build natural language interfaces using types
# aisdk
- https://github.com/vercel/ai /16.5kStar/apache2/202508/ts
  - https://ai-sdk.dev/docs/introduction
  - Build AI-powered applications with React, Svelte, Vue, and Solid
  - Vercel AI SDK abstracts away the differences between model providers, eliminates boilerplate code for building chatbots
  - AI SDK Core module provides a unified API to interact with model providers like OpenAI, Anthropic, Google, and more.
  - AI SDK UI module provides a set of hooks that help you build chatbots and generative user interfaces. These hooks are framework agnostic, so they can be used in Next.js, React, Svelte, and Vue.
  - https://vercel.com/templates/ai
    - We've built templates that include AI SDK integrations for different use cases, providers, and frameworks.
  - https://x.com/nicoalbanese10/status/1806680358093541401
    - this is all you need to use chrome's built in ai model with the vercel ai sdk
    - no api keys, no configuration, running locally in the browser

- https://github.com/vercel/ai-chatbot /apache2/202503/ts
  - https://chat-sdk.dev/
  - A full-featured, hackable Next.js AI chatbot built by Vercel
  - React Server Components (RSCs) and Server Actions for server-side rendering and increased performance
  - Neon Serverless Postgres for saving chat history and user data
  - Vercel Blob for efficient file storage
  - Auth.js: Simple and secure authentication

- https://github.com/CopilotKit/CopilotKit /22.4kStar/MIT/202508/ts
  - https://docs.copilotkit.ai/
  - React UI + elegant infrastructure for AI Copilots, AI chatbots
  - The Agentic Application Framework: Open source framework and hosted service for AI-assisted applications.

- https://github.com/langtail/ai-orchestra
  - a lightweight TypeScript library for orchestrating AI agents
  - No magic, just simple patterns built around @aisdk 's `streamText` for managing agent handoffs and state transitions.
  - A lightweight alternative to `LangGraph` without the complexity.
  - State lives outside the library - you control everything.

- https://github.com/nickscamara/open-deep-research
  - An open source deep research clone. 
  - AI Agent that reasons large amounts of web data extracted with Firecrawl
  - Powered by the @aisdk
  - https://x.com/nickscamara_/status/1886459999905521912
    - This is an experimental clone of Open AI's Deep Research. Instead of using a fine-tuned version of o3, this method uses Firecrawl's extract + search with a reasoning model to deep research the web.

- https://github.com/nicolasmontone/ai-sdk-agents /202502/ts
  - https://ai-sdk-agents.vercel.app/
  - Tools for Vercel AI SDK

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

## aisdk-examples

# chat-docs/knowledgebase
- https://github.com/jorge-armando-navarro-flores/chat_with_your_docs /MIT/202409/python
  - ChatWithYourDocs Chat App is a Python application that allows you to chat with multiple Docs formats like PDF, WEB pages and YouTube videos. 
  - This app utilizes a language model to generate accurate answers to your queries

- https://github.com/arc53/DocsGPT /MIT/python/ts
  - https://docsgpt.arc53.com/
  - GPT-powered chat for documentation, chat with your documents
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
- https://github.com/mayooear/ai-pdf-chatbot-langchain /MIT/202502/ts
  - LangChain & LangGraph AI PDF chatbot agent

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
