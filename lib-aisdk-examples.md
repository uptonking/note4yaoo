---
title: lib-aisdk-examples
tags: [aisdk, examples, large-language-model]
created: 2025-08-11T20:15:00.065Z
modified: 2025-08-11T20:15:18.297Z
---

# lib-aisdk-examples

# guide

# popular
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

- https://github.com/vercel/ai-chatbot /17.4kStar/apache2/202507/ts
  - https://chat-sdk.dev/
  - A full-featured, hackable Next.js AI chatbot built by Vercel
  - React Server Components (RSCs) and Server Actions for server-side rendering and increased performance
  - Neon Serverless Postgres for saving chat history and user data
  - Vercel Blob for efficient file storage
  - Auth.js: Simple and secure authentication
  - 🍴 forks
  - https://github.com/ragingwind/ai-chatbot-desktop /202506/ts
    - Next.js 14 and Electron integration
    - Added MCP Integration
    - Add WebLLM for LocalLLM
  - https://github.com/nickscamara/extract-chat /202501/ts
    - Extract information from any website by chatting with AI 
    - Fork of Vercel AI Chatbot w/ Firecrawl Integrated
  - https://github.com/olyaiy/build-your-own-bot /202504/ts
    - Agent Vendor is a marketplace where AI creators build specialized agents and users discover tailored AI solutions
  - https://github.com/supabase-community/vercel-ai-chatbot /202307/ts/inactive
    - Supabaseified Next.js AI chatbot built by Vercel Labs & Supabase
    - 已不维护，大多胶水层
  - https://github.com/ddoonnggee/ai-chatbot /切换中文
  - https://github.com/flybyflo/ai-chatbot /mcp-test-server
  - https://github.com/Kleo-App/ai-chatbot /added the prompt to langfuse and integrated it with the project

- https://github.com/CopilotKit/CopilotKit /22.4kStar/MIT/202508/ts
  - https://docs.copilotkit.ai/
  - React UI + elegant infrastructure for AI Copilots, AI chatbots
  - The Agentic Application Framework: Open source framework and hosted service for AI-assisted applications.

- https://github.com/nickscamara/open-deep-research
  - An open source deep research clone. 
  - AI Agent that reasons large amounts of web data extracted with Firecrawl
  - Powered by the @aisdk
  - https://x.com/nickscamara_/status/1886459999905521912
    - This is an experimental clone of Open AI's Deep Research. Instead of using a fine-tuned version of o3, this method uses Firecrawl's extract + search with a reasoning model to deep research the web.

- https://github.com/nicolasmontone/ai-sdk-agents /202502/ts
  - https://ai-sdk-agents.vercel.app/
  - Tools for Vercel AI SDK
  - Performing comprehensive web searches (Tavily, Perplexity)
  - Managing GitHub repositories, issues, and pull requests
  - Searching and retrieving GIFs through Giphy

- https://github.com/FranciscoMoretti/ai-sdk-deep-research /202508/ts
  - A minimal, end‑to‑end deep‑research agent implemented with AI SDK and Next.js
  - 🏘️ It mirrors the architecture of https://github.com/langchain-ai/open_deep_research while replacing LangChain/Graph with AI SDK’s streaming, tool calling, and structured outputs. 
  - Includes a small UI that surfaces intermediate research updates in real time.
  - Deep research loop with planning, web search, iterative supervision, and final report generation
  - UI components that render intermediate updates (queries, results, thoughts, writing) in the chat
  - Requirements: Tavily, Optional Redis for resumable, persistent SSE streams
# starter
- https://github.com/vercel-labs/ai-sdk-reasoning-starter /202507/ts
  - https://ai-sdk-reasoning.vercel.app/
  - Open-Source AI Chatbot Template Built With Next.js and the AI SDK 

- https://github.com/rarexlabs/electron-ai-starter /MIT/202507/ts
  - full-featured Electron application template with TypeScript, React, Drizzle ORM and Vercel AI SDK
  - Electron + Vite 
  - libsql + Drizzle ORM 
  - Vercel AI SDK + Assistant UI

- https://github.com/khalidkhankakar/Master-Vercel-AI-SDK /202505/ts
  - This repository is a complete hands-on exploration of the Vercel AI SDK, covering all its core features. 
  - Built to deepen my understanding of how to create AI-powered applications 

- https://github.com/vercel-labs/ai-sdk-preview-roundtrips /apache2/202501/ts
  - https://ai-sdk-preview-roundtrips.vercel.app/
  - This example demonstrates how to use the Vercel AI SDK with Next.js and the streamText function to automatically handle multiple tool steps.
  - https://github.com/vercel-labs/ai-sdk-preview-multi-steps
  - https://github.com/deksden/vercel-ai-sdk-v5-tool-streaming-demo

- https://github.com/vercel-labs/ai-sdk-preview-pdf-support /apache2/202412/ts
  - https://ai-sdk-preview-pdf-support.vercel.app/
  - This example demonstrates how to use the AI SDK with Next.js with the useObject hook to submit PDF messages to the AI provider of your choice (Google or Anthropic).

- https://github.com/vercel-labs/ai-sdk-preview-attachments /apache2/202501/ts
  - https://ai-sdk-preview-attachments.vercel.app/
  - This example demonstrates how to use the Vercel AI SDK with Next.js with the useChat hook to create a chat interface that can send and receive multi-modal messages from the AI provider of your choice.

- https://github.com/vercel-labs/ai-sdk-preview-use-object /202501/ts
  - https://ai-sdk-preview-use-object.vercel.app/
  - This example demonstrates how to use the Vercel AI SDK with Next.js with the useObject hook to stream structured object generation to the client with the AI provider of your choice.
  - https://github.com/vercel-labs/ai-sdk-preview-no-schema

- https://github.com/vercel/ai-sdk-rag-starter /202410/ts
  - the starter project for the Vercel AI SDK Retrieval-Augmented Generation (RAG) guide.
  - Postgres with pgvector, Drizzle ORM
- https://github.com/vercel-labs/ai-sdk-preview-rag /MIT/202412/ts
  - https://ai-sdk-preview-rag.vercel.app/
  - A Next.js application, powered by the Vercel AI SDK, that uses retrieval-augmented generation (RAG) to reason and respond with information outside of the model's training data.
  - Vector embedding storage with DrizzleORM and PostgreSQL

- https://github.com/vercel-labs/ai-sdk-preview-internal-knowledge-base /202501/ts
  - https://ai-sdk-preview-internal-knowledge-base.vercel.app/
  - This template demonstrates the usage of the Language Model Middleware to perform RAG and enforce guardrails using the AI SDK and Next.js.

- https://github.com/blaxel-templates/template-vercel-ai-ts /MIT/202508/ts
  - A template implementation of a conversational agent using Vercel AI SDK and GPT-4. 
  - This agent demonstrates the power of Vercel AI SDK for building interactive AI agents with tool integration capabilities and streaming responses.

- https://github.com/blaxel-templates/template-social-post-generator /MIT/202508/ts
  - A template for creating agents that automatically generates engaging social media posts from URLs or themes. 
  - This template leverages web crawling capabilities, intelligent content analysis, and semantic search to create professional social media content. 
  - Built with TypeScript and the Vercel AI SDK for robust performance and seamless integration with the Blaxel platform.
  - Custom web crawling function with markdown conversion

- https://github.com/vercel-labs/ai-sdk-preview-python-streaming /202411/python/ts
  - This template demonstrates the usage of Data Stream Protocol to stream chat completions from a Python endpoint (FastAPI) and display them using the useChat hook in your Next.js application.

- https://github.com/JamesSloan/VercelGenUI_MCP /MIT/202503/ts/inactive
  - Proof of concept chat AI combining the Model Context Protocol (MCP) with Vercel's AI SDK UI

- https://github.com/Quintui/ai-sdk-v5-data-parts-demo /202508/ts
  - implement story generation with OpenRouter AI and chat UI
  - https://github.com/nicoalbanese/ai-sdk-alpha-hacking-data-parts
  - https://github.com/nicoalbanese/ai-sdk-data-parts-july-2025
# image/multi-modal
- https://github.com/vercel-labs/ai-sdk-image-generator /apache2/202501/ts
  - https://ai-sdk-image-generator.vercel.app/
  - open-source AI image generation app template built with Next.js, the AI SDK 
  - A single input to generate images across multiple providers simultaneously.

- https://github.com/xmannii/gemini-ocr-nextjs /MIT/202507/ts
  - a simple nextjs app that uses gemini 2.5 and vercel ai sdk to extract text from images

- https://github.com/nicoalbanese/structured-image-extraction /202408/ts/inactive
  - Extract structured information from images with the AI SDK
  - It uses the experimental_useObject hook and streamObject function to generate structured data based on a Zod schema.

- https://github.com/ncounterspecialist/twick /55Star/apache2+LIMIT/202508/ts
  - https://ncounterspecialist.github.io/twick/
  - an open-source React SDK that helps developers build timeline-based, AI-powered video editors for the web. 
  - It’s a collection of TypeScript packages designed to support canvas rendering, real-time editing, AI-generated captions, and serverless video export — everything you need to build a modern, in-browser video editing experience.
  - Modular React Architecture — Built as composable TypeScript packages tailored for React apps
  - Canvas Timeline Editing — Drag, trim, resize, and layer video/audio tracks on a powerful canvas-based editor
  - Serverless MP4 Export — Render and export videos using AWS Lambda + S3, no server needed
# workflow
- https://github.com/callstackincubator/flows-ai /240Star/MIT/202507/ts
  - https://flows-ai.callstack.com/
  - A lightweight, type-safe AI workflow orchestrator inspired by Anthropic's agent patterns. 
  - Built on top of Vercel AI SDK.
  - Last year, we built Fabrice - an AI agent framework designed to break down complex tasks into smaller steps.
  - We realized that AI agent systems today are essentially modern workflows where each node is an LLM call instead of a traditional function. 
  - The key difference lies not in the framework, but in the nature of these nodes: they have flexible input/output contracts.
  - This insight led us to redefine our approach and focus on an orchestration, so you can connect different (often incompatible input/outputs) together.
  - This library provides a simple, more deterministic way to build AI workflows. You can either explicitly define your workflow with loops and conditionals, or use an orchestrator agent to dynamically break down complex tasks.
  - https://github.com/callstackincubator/fabrice-ai /MIT/202412/ts/inactive
    - A lightweight, functional, and composable framework for building AI agents
# examples
- https://github.com/vercel-labs/semantic-image-search /apache2/202503/ts
  - https://semantic-image-search.vercel.app/
  - semantic image search app template built with Next.js, the Vercel AI SDK, OpenAI, Vercel Postgres, Vercel Blob and Vercel KV.
  - Query caching with Vercel KV
  - Embeddings powered by Vercel Postgres, pgvector, and Drizzle ORM
  - File (image) storage with Vercel Blob

- https://github.com/dryor/translate-app /MIT/202409/ts/inactive
  - https://talk-translate.vercel.app/
  - Translate App using TypeScript, Tailwind CSS, NextJS, Bun, shadcn/ui, AI-SDK/OpenAI, Zod, Vercel Analytics, pdf-parse.
  - pdf-parse - Convert PDF to Text.
  - Translate images.

- https://github.com/patelvivekdev/turso-vector-search /202507/ts
  - https://turso-vector-search.vercel.app/
  - AI chatbot with Vercel AI SDK, Turso as vector DB and google gemini model.
  - This is a simple RAG example of how to use the Turso Vector Search API with Drizzle ORM Google AI.

- https://github.com/admineral/Reactor /202405/ts/inactive
  - https://reactor-dev.vercel.app/
  - Chat with React Code-Editor and Live-preview using Sandpack by Codesandbox

- https://github.com/vercel-labs/ai-sdk-computer-use /202507/ts
  - https://ai-sdk-computer-use.vercel.app/
  - chatbot app template demonstrating Anthropic Claude 3.7 Sonnet's computer use capabilities, built with Next.js and the AI SDK by Vercel.
  - Sandbox environment with e2b for secure execution.

- https://github.com/e2b-dev/e2b-cookbook/tree/main/examples/nextjs-code-interpreter /202508/ts
  - This example shows how to use the E2B Code Interpreter to execute code in Next.js serverless functions.
  - The `evaluateCode` method is the main method that takes Python `code` to be executed and `sessionID`. 
  - Based on the `sessionID` it will try to reconnect to an existing sandbox or create a new one if it doesn't exist. 
  - The code execution is stateful (using Jupyter Notebook underneath) and per session — you can refer to variables from the previous execution, define functions that you will use later, etc.

- https://github.com/vercel-labs/ai-facts /202412/ts
  - https://ai-facts.vercel.app/
  - Real-time fact checking on spoken statements with the AI SDK, Perplexity and DeepGram

- https://github.com/techwithanirudh/discord-ai-bot /MIT/202506/ts
  - A human-like, AI-powered Discord bot built with the Vercel AI SDK and Bun.
  - Exa AI, Mem0

- https://github.com/UjjwalSaini07/Neura-AI /BSD/202507/js
  - https://neura-ais.vercel.app/
  - intelligent AI chat with our voice-enabled chatbot, powered by AI SDK, Groq AI, and Gemini AI. 
  - With built-in speech-to-text, you can easily interact using your voice and get instant, accurate responses.
  - https://github.com/joshivanhilario/Neura-AI

- https://github.com/one-ie/one /79Star/MIT+LOGO/202507/ts/astro
  - https://one.ie/
  - ONE Web is a cutting-edge Astro application that combines AI chat capabilities with professional EPUB book generation.
  - Build AI powered websites with Astro, Shadcn and Vercel AI SDK
  - Markdown-to-EPUB conversion using Pandoc

- https://github.com/NightClover-code/modern-ecommerce /MIT/202401/ts
  - Full-stack eCommerce platform built with Next.js, Nest.js, and MongoDB, featuring AI-powered product creation using Vercel AI SDK.
  - AI Product Creator for generating product listings (Vercel AI SDK)
  - Image generation for product images (using Replicate)
  - Role-based access control (Admin/User)

- https://github.com/alexylon/Sofos /202508/ts
  - https://sofos.vercel.app/
  - A multimodal web chatbot developed using Vercel AI SDK, React (TypeScript), Next.js, NextAuth.js and Material UI. 
  - It can read messages and analyze multiple images simultaneously. Currently, it responds only with text.

- https://github.com/franciscomoretti/sparka /apache2/202508/ts
  - https://sparka.ai/
  - Access every major AI assistant Claude, GPT-4, Gemini, Grok, and 20+ models through one interface.
  - Get capabilities like document analysis, image generation, code execution, and research tools without managing multiple subscriptions. 
  - fork of vercel/ai-bot 🍴
  - 后端依赖 aisdk, drizzle, trpc, pg, redis
  - Attachment Support - Upload and analyze images, PDFs, and documents in conversations.
  - Resumable Streams - Continue AI generations after page refreshes or interruptions.
  - Image Generation - Generate and edit images with advanced AI models.
  - 🌵 Chat Branching - Create alternative conversation paths without losing your original thread.
  - Share conversations with others and collaborate on AI-assisted projects.
  - Deep Research - Comprehensive research with real-time web search, source analysis, and cited findings.
  - Code Execution - Run Python, JavaScript, and more in secure sandboxes.
  - https://x.com/franmoretti_/status/1954915129759338872
    - Loading + Thinking animations
    - Pulse dot (loading) -> [Prompt-kit](https://www.prompt-kit.com/)
    - Shimmer Text (thinking) -> Prompt kit
    - Reasoning (w/ auto-close) -> aisdk

- https://github.com/nicstrong/prompt-dev /MIT/202508/ts
  - A modern AI chat application built with React, tRPC, Express.js and Vercel AI SDK.

- https://github.com/sibiraj-s/ai-chat-example /MIT/202503/ts
  - An CLI based AI chat agent built using vercel ai sdk - demo

- https://github.com/carlyrichmond/travel-planner-ai-agent /apache2/202506/ts
  - Example Travel Planner Application Showing AI Agents Built Using AI SDK by Vercel and Elasticsearch. 
  - It features in the piece Building AI Agents with AI SDK and Elastic in Elasticsearch Labs.

- https://github.com/PerfLab-io/perfagent /apache2/202507/ts
  - https://agent.perflab.io/
  - A performance insights and knowledge assistant agent built on top of Chrome DevTools internals, Mastra, AI SDK and NextJS
  - PerfAgent is an advanced web performance analysis tool that leverages AI to help developers analyze and optimize their web applications. 
  - It provides detailed insights into Core Web Vitals and other performance metrics through interactive visualizations and AI-assisted recommendations.
  - Flame graph visualization for CPU profile analysis
# utils
- https://github.com/jakobhoeg/built-in-ai /apache2/202508/ts
  - https://built-in-ai-provider-next-hybrid.vercel.app/
  - TypeScript library for using in-browser AI models with the Vercel AI SDK, with support for seamless fallback to server-side models
  - @built-in-ai/core package is the AI SDK model provider for your Chrome and Edge browser's built-in AI models.
  - @built-in-ai/web-llm package is the AI SDK model provider for open-source models (using WebLLM) running directly in the browser.

- https://github.com/nicoalbanese/ai-sdk-chrome-ai /202408/ts
  - https://ai-sdk-chrome-ai.vercel.app/
  - open-source chatbot built with Next.js, the Vercel AI SDK, and the Chrome AI provider.
  - Vercel AI SDK for interacting with `window.ai` Gemini Nano model (using Chrome AI provider)

- https://github.com/minpeter/ai-sdk-tool-call-middleware /202508/ts
  - Allows tool calls to be used in the AI ​​SDK framework regardless of the model.

- https://github.com/jagreehal/ai-sdk-guardrails /MIT/202508/ts
  - A powerful middleware for the Vercel AI SDK that adds safety, quality control, and cost management to your AI applications by intercepting prompts and responses.
  - Block harmful inputs, filter low-quality outputs, and gain observability, all in just a few lines of code.

- https://github.com/vercel-labs/ai-sdk-persistence-db /202507/ts
  - This example demonstrates how to persist chat messages using Vercel AI SDK with a Postgres database in a Next.js application.
  - Drizzle ORM for database queries
  - Each chat has an auto-incrementing ID and contains multiple messages with timestamps.

- https://github.com/sslava/ai-sdk-agents /MIT/202507/ts
  - toolkit for building, running, and managing AI-powered agents - built on top of the Vercel AI SDK
  - an extension of the standard Vercel AI SDK API.
  - Extends the Vercel AI SDK API to support new generative app patterns
  - you can define your own agents, compose them together, and call agents as tools within other agents, unlocking complex reasoning and orchestration flows.
  - Define and compose agents (agents can call each other as tools)
  - Context and memory between steps

- https://github.com/samuelkarani/ai-sugar /202508/ts
  - Lodash for AI. A collection of utility functions powered by AI - built on top of Vercel AI SDK
  - A set of 'primitive' functions: isTrue, knows, can shortAnswer complete

- https://github.com/OpenAssistantGPT/chatbot-sdk /apache2/202508/ts
  - https://sdk.openassistantgpt.io/
  - This SDK is an extension of the vercel/ai SDK with more features, addapted to our use case and maintained by the OpenAssistantGPT team.

- https://github.com/VoltAgent/vercel-ai-sdk-observability /MIT/202406/ts/inactive
  - This example demonstrates how to add VoltAgent observability to your existing Vercel AI applications with minimal code changes.
  - Track AI calls, tool usage, and multi-agent workflows in the VoltAgent Developer Console.

- https://github.com/langtail/ai-orchestra /202502/ts
  - Simple orchestration for AI Agents built around Vercel's `streamText`. 
  - Lightweight alternative to LangGraph for agent handoffs and state transitions, similar to OpenAI's Swarm but with more developer control and less magic. 
  - Think of it as a simpler alternative to LangGraph, focused on streaming and agent coordination.
  - Built for Streaming - Native support for Vercel's streamText and AI SDK
  - Similar patterns to OpenAI's Swarm, but more flexible

- https://github.com/stevef24/Agentic-patterns /202504/ts
  - Agentic patterns with Vercel AI SDK

- https://github.com/fkesheh/mcp-ai-agent /MIT/202508/ts
  - A TypeScript library that enables AI agents to leverage MCP servers for enhanced capabilities. 
  - This library integrates with the AI SDK v5 to provide a seamless way to connect to MCP servers and use their tools in AI-powered applications.
  - Connect to multiple MCP servers using different transport methods (STDIO, SSE)
  - Automatically discover and use tools from MCP servers
  - Integrate with AI SDK for text generation with tool usage
  - Agents can call other agents for specific tasks
  - Agent composition - create specialized agents and combine them

- https://github.com/vrknetha/aisdk-mcp-bridge /MIT/202502/ts/inactive
  - Bridge package enabling seamless integration between Model Context Protocol (MCP) servers and AI SDK tools. 
  - Supports multiple server types, real-time communication, and TypeScript.
  - Support for various MCP server types (Node.js, Python, UVX)
  - Multi-server support with independent configuration
  - Flexible configuration through mcp.config.json

- https://github.com/EuclideanAI/mcp-client /202507/ts
  - A custom Model Context Protocol (MCP) Client interface with integrated LLM agent chat capabilities built with Next.js and the Vercel AI SDK

- https://github.com/codebucks27/Deep-Research-AI-Agent /202505/ts
  - A powerful Deep Research AI agent like Gemini or ChatGPT. 
  - Using Next.js, Vercel AI SDK, and Exa Search API
  - Fully Customizable Research Flow
  - Iterative Research Loop
  - Web Search: Exa Search API
  - https://github.com/mhohamad/Deep-Research-AI-Agent

- https://github.com/DracoBlue/a2a-ai-provider /MIT/202508/ts
  - An @ai-sdk compatible AI provider implementation for the A2A Protocol, enabling universal interoperability between LLMs, tools, streaming output, and file-based artifacts.
  - Drop-in ai Provider (v5 and later)
  - Full support for A2A JSON-RPC 2.0 API by using @a2a-js/sdk

- https://github.com/rmay1er/ai-responder /MIT/202507/ts
  - lightweight library using Vercel AI SDK to quickly create and manage AI agents with contextual conversations and real-time responses.
  - Context-Aware Dialog - Advanced conversation management with safe message trimming
  - Flexible Memory Modes - Support for session-based memory or stateless, one-off queries
  - Extensible Tool Support - Incorporate external APIs and custom tools within dialogs

- https://github.com/zaidmukaddam/scira /10.4kStar/apache2/202508/ts
  - https://scira.ai/
  - Scira (Formerly MiniPerplx) is a minimalistic AI-powered search engine that helps you find information on the internet and cites it too. 
  - Powered by Vercel AI SDK
  - using multiple AI models including xAI's Grok, Anthropic's Claude, Google's Gemini, and OpenAI's GPT models
  - Search the web using Exa's API with support for multiple queries, search depths, and topics
  - Extract and analyze content from any URL using Exa AI with live crawling capabilities
  - Search Reddit content with time range filtering using Tavily API
  - Search X posts with date ranges and specific handle filtering using xAI Live Search
  - Advanced multi-step search capability for complex queries
  - Academic search: Search for academic papers and research using Exa AI with abstracts and summaries
  - YouTube search: Find YouTube videos with detailed information, captions, and timestamps powered by Exa AI

- https://github.com/callstackincubator/ai /MIT/202508/ts/kotlin
  - https://react-native-ai.dev/
  - Bring on-device AI to React Native apps. 
  - Compatible with Vercel AI SDK interface.
  - Use instantly available built-in models (Apple Intelligence, Gemini Nano) for immediate AI capabilities, or download and run any model locally with popular runtimes such as MLC Engine.
  - Instant AI - Built-in models work immediately, no downloads or setup required
  - Privacy-first - All processing happens on-device, your data stays local

- https://github.com/IvanAmador/vercel-ai-docs-mcp /202504/ts
  - A MCP server that provides AI-powered search and querying capabilities for the Vercel AI SDK documentation. 
  - Query the Vercel AI SDK documentation index directly using similarity search
  - Automated Indexing: Includes tools to fetch, process, and index the latest Vercel AI SDK documentation
  - VectorStoreManager: Creates and manages the `FAISS` vector index for semantic search
  - AgentService: Provides AI-powered answers to questions using the Google Gemini model
# integrations
- https://github.com/jotaijs/jotai-ai /MIT/202508/ts
  - a utility package compatible with Vercel AI SDK.
  - useChat is the equivalent of vercel ai's useChat hook.

- https://github.com/warmwind/dify-ai-provider /202506/ts
  - A provider for Dify. AI to work with Vercel AI SDK.
  - This provider allows you to easily integrate Dify AI's application workflow with your applications using the Vercel AI SDK.

## providers

- https://github.com/OpenRouterTeam/ai-sdk-provider /apache2/202508/ts
  - The OpenRouter provider for the Vercel AI SDK gives access to over 300 large language models on the OpenRouter chat and completion APIs.
  - https://github.com/ChrisCates/openrouter-ai-sdk
    - Openrouter Vercel AI SDK: Refactor and Rewrite

- https://github.com/vercel-labs/ai-sdk-starter-groq /202507/ts
  - open-source AI chatbot app template built with Next.js, the AI SDK by Vercel, and Groq.
  - Built-in tool integration for extending AI capabilities (demonstrated with a weather tool example).
  - https://github.com/Xeven777/next-groq /202508/ts
    - fast Chatbot made using Vercel AI SDK and Groq AI

- https://github.com/jagreehal/ai-sdk-ollama /MIT/202508/ts
  - Vercel AI SDK v5+ provider for Ollama built on the official ollama package
  - A monorepo containing the AI SDK Ollama Provider and examples demonstrating usage in both Node.js and browser environments.
  - Drop-in replacement for other AI SDK providers
  - Native Ollama features - Access to Ollama-specific options and parameters

- https://github.com/Younis-Ahmed/qwen-ai-provider /202507/ts
  - Community-built Qwen AI Provider for Vercel AI SDK - Integrate Alibaba Cloud's Qwen models 

- https://github.com/ben-vargas/ai-sdk-provider-gemini-cli /MIT/202507/ts
  - Vercel AI SDK community provider for Gemini CLI - Free use via Gemini Code Assist License
  - A community provider for the Vercel AI SDK that enables using Google's Gemini models through the @google/gemini-cli-core library and Google Cloud Code endpoints.
  - Compatible with Vercel AI SDK (v4 and v5-beta)
  - Multimodal support (text and base64 images)
  - OAuth authentication using Gemini CLI credentials
# more
