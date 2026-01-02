---
title: lib-ai-app-examples-utils-fwk
tags: [ai, examples, utils]
created: 2025-02-21T18:20:28.621Z
modified: 2025-02-21T18:20:42.624Z
---

# lib-ai-app-examples-utils-fwk

# guide

# popular
- https://github.com/microsoft/mcp-for-beginners /MIT/202507/python/ts
  - This open-source curriculum introduces the fundamentals of Model Context Protocol (MCP) through real-world, cross-language examples in . NET, Java, TypeScript, JavaScript, and Python.

- https://github.com/langgenius/dify /82.5kStar/apache2/202503/python
  - https://dify.ai/
  - Dify is an open-source LLM app development platform
  - combines AI workflow, RAG pipeline, agent capabilities, model management, observability features and more
  - 依赖flask-sqlalchemy、beautifulsoup4、celery、gunicorn、langfuse、langsmith、numpy、pandas、pydantic、starlette、unstructured、python-docx、boto3
  - 前端依赖 @dagrejs/dagre、elkjs、elkjs@lexical/react、@next/mdx、zustand、swr、tanstack-query5、ahooks、echarts-for-react、immer、mermaid、react-markdown、react-window、remark-gfm、sortablejs
  - license 💰
    - Unless explicitly authorized by Dify in writing, you may not use the Dify source code to operate a multi-tenant environment.
    - In the process of using Dify's frontend, you may not remove or modify the LOGO or copyright information in the Dify console or applications. 
  - https://github.com/YFGaia/dify-plus /dify-lic
    - Dify-Plus 是 Dify 的企业级增强版，集成了基于 gin-vue-admin 的管理中心，并针对企业场景进行了功能优化。
    - Dify-Plus = 管理中心 + Dify 二开 
    - 在原有 Dify 的基础中，该项目做了一些二开以及新增了管理中心的功能，原先这些功能只是在我们企业内部使用，对外交流后发现很多伙伴也遇到我们相同一些痛点，故将我们的二开内容进行开源
    - 新增：用户额度
    - 新增：密钥额度设置
    - 新增 ：Web 公开页登录鉴权
    - 新增：后台创建用户，自动邀请进管理员空间
    - 新增：sandbox-full，以放开代码执行节点函数限制
  - 🐛 [Token Limit for full Document (10000 Token cut) _202506](https://github.com/langgenius/dify/issues/20604)
    - Dify's Retrieval-Augmented Generation (RAG) module, especially when utilizing the Parent-Child mode with a full document, appears to have a rigid limitation of 10,000 tokens per document. This constraint means that any content exceeding this token count is effectively ignored or truncated before it enters the retrieval process.
    - There is currently no apparent configuration option (for example, in the .env file) that allows users to adjust this maximum token length for RAG processing. 
    - there is no configurable option (neither in .env nor in the UI) to increase the 10,000-token limit in Parent-Child mode.
  - [Help： How to deal with the Doc Extractor output is too big in Knowledge template ](https://github.com/langgenius/dify/discussions/28889)
    - If the pdf file content is too large and it exceed the max context length of LLM. How to deal with it? 

- https://github.com/cloudflare/agents /MIT/202502/ts
  - https://developers.cloudflare.com/agents/
  - Build and deploy AI Agents on Cloudflare
  - https://x.com/threepointone/status/1895097050439593993
    - an event bus for ai agents

- https://github.com/mozilla-ai/any-agent /1kStar/apache2/202511/python
  - https://mozilla-ai.github.io/any-agent/
  - A single interface to use and evaluate different agent frameworks.
  - Multi-agent can be implemented using Agents-As-Tools.
# agent-framework/backend
- https://github.com/langchain-ai/langchain /113kStar/MIT/202508/python
  - https://python.langchain.com/
  - https://python.langchain.com/docs/introduction/
  - LangChain is a framework for building LLM-powered applications. 
  - langchain-core: Base abstractions for chat models and other components.
  - langchain: Chains, agents, and retrieval strategies that make up an application's cognitive architecture.
  - langgraph: Orchestration framework for combining LangChain components into production-ready applications with persistence, streaming, and other key features
  - LangSmith: Trace and evaluate your language model applications and intelligent agents

- https://github.com/langchain-ai/langchainjs /15.4kStar/MIT/202508/ts
  - https://js.langchain.com/docs/
  - a framework for developing applications powered by language models
  - can be used in: nodejs, Browser, Cloudflare Workers, Deno, VERCEL
  - [Is LangChainJS possible without NodeJS? · langchain-ai/langchainjs _202504](https://github.com/langchain-ai/langchainjs/discussions/4494)
    - 支持在浏览器纯前端运行

- https://github.com/langchain-ai/langgraph /17.1kStar/MIT/202508/python
  - https://langchain-ai.github.io/langgraph/
  - a low-level orchestration framework for building, managing, and deploying long-running, stateful agents.
  - LangGraph does not abstract prompts or architecture
  - Durable execution: Build agents that persist through failures and can run for extended periods, automatically resuming from exactly where they left off.
  - Human-in-the-loop: Seamlessly incorporate human oversight by inspecting and modifying agent state at any point during execution.
  - both short-term working memory for ongoing reasoning and long-term persistent memory across sessions.
  - [Feature request: Source code? · Issue · langchain-ai/langgraph-studio _202410](https://github.com/langchain-ai/langgraph-studio/issues/154)
    - we're currently not considering open-sourcing the project, as it depends on some parts of LangSmith.
  - [[Docs] Add LangGraph integration examples to JS/TS documentation _202507](https://github.com/orgs/langfuse/discussions/7709)
    - Currently, the Langfuse JS/TS documentation lacks guidance on integrating with LangGraph. 

- https://github.com/langchain-ai/langgraphjs /1.9kStar/MIT/202508/ts
  - https://langchain-ai.github.io/langgraphjs/
  - LangGraph library enables agent orchestration — offering customizable architectures, long-term memory, and human-in-the-loop to reliably handle complex tasks.
  - JavaScript port of LangGraph. The architecture is the same conceptually — a durable graph of tasks/agents
  - Reliability and controllability. LangGraph persists context for long-running workflows, keeping your agents on course.
  - Low-level and extensible. Build custom agents with fully descriptive, low-level primitives 
  - First-class streaming support. With token-by-token streaming and streaming of intermediate steps, LangGraph gives users clear visibility into agent reasoning and actions as they unfold in real time
  - LangGraph is inspired by Pregel and Apache Beam. The public interface draws inspiration from NetworkX.

- https://github.com/langfuse/langfuse /14.8kStar/MIT+EE/202508/ts
  - https://langfuse.com/docs
  - Langfuse is an open source LLM engineering platform. 
  - It helps teams collaboratively develop, monitor, evaluate, and debug AI applications. 
  - 系统元数据存储在pg, 观测数据存储在clickhouse，附件存储在s3
  - Observability: tracking LLM calls and other relevant logic in your app such as retrieval, embedding, or agent actions
  - Prompt Management 
  - Evaluations: supports LLM-as-a-judge, user feedback collection
  - Datasets enable test sets and benchmarks for evaluating your LLM applications
  - LLM Playground is a tool for testing and iterating on your prompts and model configurations
  - [All Langfuse Product Features now Free Open-Source : r/LangChain _202506](https://www.reddit.com/r/LangChain/comments/1l36tte/all_langfuse_product_features_now_free_opensource/)
    - 💡 Langfuse is an open-source LangSmith alternative that helps teams collaboratively build, debug, and improve their LLM applications
  - [Self-host Langfuse (Open Source LLM Observability)](https://langfuse.com/self-hosting)

- https://github.com/K-Mistele/swarm /GPLv3/202501/ts/inactive
  - Model-agnostic typescript implementation of OpenAI's Swarm framework with the Vercel AI SDK
  - model-agnostic library for creating and managing multi-agent AI systems
  - This package is loosely based off of OpenAI Swarm, but please note that APIs are not identical, and they are not intended to be. 
  - This package is intended to provide the same functionality, but with better patterns
- https://github.com/joshmu/ts-swarm /MIT/202507/ts/deprecated
  - Minimal agentic library mixing the simplicity of OpenAI Swarm with the flexibility of the Vercel AI SDK
  - Option to run locally with the ollama-ai-provider.

- https://github.com/microsoft/autogen /48.5kStar/MIT/202508/python
  - https://microsoft.github.io/autogen/
  - a framework for creating multi-agent AI applications that can act autonomously or work alongside humans.
  - 未主打workflow
  - The framework uses a layered and extensible design.
  - Core API implements message passing, event-driven agents, and local and distributed runtime for flexibility and power. 
  - AgentChat API implements a simpler but opinionated API for rapid prototyping. 
  - Extensions API enables first- and third-party extensions continuously expanding framework capabilities.
  - AutoGen Studio provides a no-code GUI for building multi-agent applications.
  - AutoGen Bench provides a benchmarking suite for evaluating agent performance.

- https://github.com/crewAIInc/crewAI /35.5kStar/MIT/202508/python
  - https://crewai.com/
  - a lean, lightning-fast Python framework built entirely from scratch—completely independent of LangChain or other agent frameworks.
  - CrewAI's Advantage: CrewAI combines autonomous agent intelligence with precise workflow control through its unique Crews and Flows architecture. 
  - CrewAI Crews: Teams of AI agents with true autonomy and agency, working together to accomplish complex tasks through role-based collaboration
  - CrewAI Flows: Enable granular, event-driven control, single LLM calls for precise task orchestration and supports Crews natively
  - Flexible Low Level Customization: Complete freedom to customize at both high and low levels - from overall workflows and system architecture to granular agent behaviors, internal prompts, and execution logic.
  - Ideal for Every Use Case
  - 🆚 How CrewAI Compares
    - While LangGraph provides a foundation for building agent workflows, its approach requires significant boilerplate code and complex state management patterns. The framework's tight coupling with LangChain can limit flexibility when implementing custom agent behaviors or integrating with external systems.
    - Autogen: While Autogen excels at creating conversational agents capable of working together, it lacks an inherent concept of process.
    - ChatDev: ChatDev introduced the idea of processes into the realm of AI agents, but its implementation is quite rigid. Customizations in ChatDev are limited

- https://github.com/mastra-ai/mastra /15.8kStar/apache2/202508/ts
  - https://mastra.ai/
  - 💫 https://mastra.ai/en/docs/server-db/local-dev-playground
  - an opinionated TypeScript framework that helps you build AI applications and features quickly.
  - It gives you the set of primitives you need: workflows, agents, RAG, integrations and evals.
  - 不依赖langchain/langflow
  - You can run Mastra on your local machine, or deploy to a serverless cloud.
  - Mastra uses the Vercel AI SDK for model routing, providing a unified interface to interact with any LLM provider including OpenAI, Anthropic, and Google Gemini. 
  - Agents are systems where the language model chooses a sequence of actions. 
  - Tools are typed functions that can be executed by agents or workflows, with built-in integration access and parameter validation. 
  - Workflows are durable graph-based state machines. They have loops, branching, wait for human input, embed other workflows
  - RAG lets you construct a knowledge base for agents
  - Evals are automated tests that evaluate LLM outputs using model-graded, rule-based, and statistical methods.
  - https://github.com/mastra-ai/mastra/blob/main/examples/crypto-chatbot/lib/editor/diff.js
    - 使用diff_match_patch计算差异
  - https://x.com/dingyi/status/1893329741060489438
    - 以前非常喜欢且深度使用的 Gatsby，他们团队原班人马做的新产品，The TypeScript Agent Framework
  - 🎯 [The next evolution of Mastra streaming _202509](https://mastra.ai/blog/mastra-streaming)
    - When we first built Mastra, we relied entirely on Vercel's AI SDK for streaming. It was a pragmatic choice that let us focus on what made Mastra unique: the orchestration layer that sits above language models.
    - But as developers started building more complex apps with Mastra, we kept hitting the same limitations. What happens when an agent calls another agent? How do you stream results from a workflow that contains multiple agents? 
    - Our old implementation worked beautifully for single model calls, but Mastra needed something more.
    - So we built our own streaming layer.
    - The new `format` option we're introducing (like `format: 'aisdk'`) establishes a pattern where Mastra can output streams in whatever format your frontend needs. Today it's AI SDK v5. Tomorrow it could be `copilotkit`, assistant-ui, or a format we haven't even imagined yet.
    - We've written before about nested streaming, but it bears repeating: modern AI applications are compositional. Agents call other agents. Workflows orchestrate multiple models. Tools can be entire applications themselves. Our custom streaming protocol makes these patterns not just possible but elegant.

- https://github.com/MotiaDev/motia /5.8kStar/MIT/202508/ts
  - https://motia.dev/
  - Modern Backend Framework that unifies APIs, background jobs, workflows, and AI agents into a single cohesive system with built-in observability and state management.
  - a modern backend framework for building event-driven applications with built-in observability and state management.
  - Motia gives you full, code-first control of your agents and automations with the simplicity of a visual interface, letting you focus on what truly matters: your business logic
  - 不依赖langchain/langflow
  - 执行时进度动画显示在任务画布下方的水平条形图，ux设计不符合主流
    - 但支持在水平条形图显示各节点的执行时间，数据更具体
  - Use any LLM, vector store, or reasoning pattern without restrictions.
  - Zero Infrastructure Headaches - No Kubernetes expertise required. Deploy agents with a single command
  - Code-First Development - Write agent logic in familiar languages, not proprietary DSLs.
  - Composable Steps with Runtime Validation - Build agents from modular, reusable components with automatic input/output validation.
  - Built-in Observability - Debug agent behavior with visual execution graphs and real-time logging.
  - Instant APIs & Webhooks - Expose agent functionality via HTTP endpoints without extra code.
  - https://github.com/MotiaDev/motia-examples /数据流动画
    - Intelligent Q&A from PDFs with Docling's smart chunking, Weaviate's sca lable vector DB, and OpenAI embeddings & text generation. 
    - Built with TypeScript & Python.

- https://github.com/gensx-inc/gensx /507Star/apache2/202508/ts
  - https://gensx.com/
  - The TypeScript framework for agents & workflows with react-like components.
  - GenSX takes a lot of inspiration from React, but the programming model is very different - it’s a Node.js framework designed for data flow.
  - 不依赖langchain/langflow
  - Pure Functions: Components are pure TypeScript functions that are easily testable, reusable, and sharable
  - Parallel by Default: Components execute in parallel when possible while maintaining dependencies
  - Full TypeScript support with no DSLs or special syntax - just standard language features
  - Streaming Built-in: Stream responses with a single prop change, no refactoring needed
  - https://x.com/_Evan_Boyle/status/1892590845485895730
    - GenSX components are reusable by default and are easy to consume and share. 

- https://github.com/google-gemini/gemini-fullstack-langgraph-quickstart /apache2/202506/python/ts
  - Get started with building Fullstack Agents using Gemini 2.5 and LangGraph
  - https://x.com/JvShah124/status/1933016336113791159
    - Gemini 2.5 + LangGraph = Build Research Agents That AUTONOMOUSLY Crawl the Web, Cite Sources & Solve Complex Queries.
    - Backend: Python (FastAPI) + LangGraph for orchestrating multi-step workflows
    - Pluggable AI: Gemini 2.5 by default, but swap in Claude/Mistral via API keys
    - Tools: Google Search API + room to add LlamaIndex, custom APIs, etc.

- https://github.com/huggingface/smolagents /22.5kStar/apache2/202509/python
  - https://huggingface.co/docs/smolagents
  - smolagents is a library that enables you to run powerful agents in a few lines of code.  
  - Simplicity: the logic for agents fits in ~1, 000 lines of code (see agents.py). We kept abstractions to their minimal shape above raw code
  - First-class support for Code Agents. Our CodeAgent writes its actions in code. we support executing in sandboxed environments via E2B, Modal, Docker, or Pyodide+Deno WebAssembly sandbox.
  - Hub integrations: you can share/pull tools or agents to/from the Hub for instant sharing o
  - Model-agnostic: smolagents supports any LLM. It can be a local transformers or ollama model
  - support text, vision, video, even audio inputs
  - Tool-agnostic: you can use tools from any MCP server, from LangChain, you can even use a Hub Space as a tool.

- https://github.com/apocas/restai /431Star/apache2/202508/python
  - https://apocas.github.io/restai/
  - an AIaaS (AI as a Service) open-source platform. 
  - Built on top of LlamaIndex & Langchain. langchain仅用于dalle_image_generator, LlamaIndex用得多
  - Supports any public LLM supported by LlamaIndex and any local LLM supported by Ollama/vLLM/etc
  - Built-in image generation (Dall-E, SD, Flux) and dynamic loading generators.
  - Image Generation: Supports local and remote image generators. 
    - Local image generators are run in a separate process. 
    - New generators are easily added and loaded dynamically.
    - 本地的图片生成基于diffusers实现， 如 `from diffusers import DiffusionPipeline`;
  - Proxy: Allows management of an OpenAI compatible proxy. LiteLLM is supported out of the box.
  - Projects: There are multiple project types, each with its own features. (rag, ragsql, inference, vision, router, agent)
  - The API is a first-class citizen of RestAI. All endpoints are documented using Swagger.
  - There are two vectorstores supported: ChromaDB and RedisVL
  - https://github.com/apocas/restai-frontend /202505/js/inactive
    - 依赖mui.v5、@reduxjs/toolkit、echarts、mui-datatables、react-d3-tree、recharts

- https://github.com/The-Pocket/PocketFlow /8.2kStar/MIT/202508/python
  - https://the-pocket.github.io/PocketFlow/
  - Pocket Flow is a 100-line minimalist LLM framework
  - Lightweight: Just 100 lines. Zero bloat, zero dependencies, zero vendor lock-in.
  - Expressive: Everything you love—(Multi-)Agents, Workflow, RAG, and more.
  - Agentic Coding: Let AI Agents (e.g., Cursor AI) build Agents—10x productivity boost!
  - https://github.com/The-Pocket/PocketFlow-Typescript
  - https://github.com/The-Pocket/PocketFlow-Go
  - [I Built Pocket Flow, an LLM Framework in just 100 Lines — Here is Why _202503](https://medium.com/@zh2408/i-built-an-llm-framework-in-just-100-lines-83ff1968014b)
  - [Streaming LLM Responses — Tutorial For Dummies (Using PocketFlow!) _202505](https://medium.com/@zh2408/streaming-llm-responses-tutorial-for-dummies-using-pocketflow-417ad920c102)

- https://github.com/Osly-AI/Pocket-Flow-Framework /664Star/MIT/202502/ts/inactive
  - https://Osly-AI.github.io/Pocket-Flow-Framework
  - Enabling non‑developers to create custom AI workflows with natural language.
  - The original core abstraction behind the Pocketflow Platform
  - This repo contains the original Pocketflow Framework—the Nested Directed Graph engine that underpins one‑shot workflow generation on Pocketflow. Workflows on the platform wrap around this framework, providing a consistent execution model and state management layer.
  - Nested Directed Graph: Breaks complex tasks into reusable nodes with branching and recursion.
  - One‑Shot Assembly: Core abstraction powering prompt‑based workflow creation.
  - Modular Nodes: Each node is an independent processing unit.
  - Vendor‑Agnostic: Integrate any LLM or API without extra wrappers.
  - Debug-Friendly: Inspect state and trace execution paths easily.

## deep-research

- https://github.com/bytedance/deer-flow /16.1kStar/MIT/202508/python/ts
  - https://deerflow.tech/
  - community-driven Deep Research framework, combining language models with tools like web search, crawling, and Python execution
  - DeerFlow implements a modular multi-agent system architecture designed for automated research and code analysis. 
  - The system is built on LangGraph, enabling a flexible state-based workflow where components communicate through a well-defined message passing system.
  - DeerFlow uses LangGraph for its workflow architecture. You can use LangGraph Studio to debug and visualize the workflow in real-time.
  - DeerFlow now includes a Text-to-Speech (TTS) feature that allows you to convert research reports to speech.

- https://github.com/langchain-ai/local-deep-researcher /8kStar/MIT/202508/python
  - a fully local web research assistant that uses any LLM hosted by Ollama or LMStudio.
  - By default, it will use DuckDuckGo for web search, which does not require an API key. But you can also use SearXNG, Tavily or Perplexity by adding their API keys to the environment file
  - [Building a fully local research assistant from scratch with Ollama - YouTube _202412](https://www.youtube.com/watch?v=XGuTzHoqlj8)

- https://github.com/langchain-ai/open_deep_research /7.4kStar/MIT/202508/python
  - a simple, configurable, fully open source deep research agent that works across many model providers, search tools, and MCP servers.
  - By default it uses the Tavily search API.
  - [Local Open Deep Research with Offline Wikipedia Search Source : r/LocalLLaMA _202510](https://www.reddit.com/r/LocalLLaMA/comments/1nx5w8m/local_open_deep_research_with_offline_wikipedia/)
    - I created my own branch of the deep research repo and added functionality to enable fully offline Wikipedia search to decrease the per-report cost even further
    - [Wikipedia Deep Research](https://publish.obsidian.md/neutron/Published/Projects/10-03-25+Wikipedia+Deep+Research)

- https://github.com/assafelovic/gpt-researcher /24.1kStar/apache2/202511/python/ts
  - https://gptr.dev/
  - An LLM agent that conducts deep research (local and web) on any given topic and generates a long report with citations.

## router/gateway

- https://github.com/ssrsgaga/API-Check /MIT/202601/ts
  - https://api-check-beta.vercel.app/
  - 快速的大模型 API 连通性测试工具。纯前端运行，支持 OpenAI 格式，数据仅在本地存储。
  - [API Check大模型批量测活助手【多功能免费开源/Vercel一键部署/纯前端 _202601](https://linux.do/t/topic/1384242)

- https://github.com/ulab-uiuc/LLMRouter /400Star/MIT/202512/python
  - https://ulab-uiuc.github.io/LLMRouter/
  - Open-Source Library for LLM Routing
  - an intelligent routing system designed to optimize LLM inference by dynamically selecting the most suitable model for each query
  - Unified CLI: Complete command-line interface for training, inference, and interactive chat with Gradio-based UI.
  - Complete pipeline for generating training data from 11 benchmark datasets with automatic API calling and evaluation.
  - [We open-sourced LLMRouter: the first unified LLM routing library  _202512](https://www.reddit.com/r/LocalLLaMA/comments/1q06z2l/we_opensourced_llmrouter_the_first_unified_llm/)
    - The current LLM routing landscape feels a lot like early GNN research: many promising router algorithms exist, but each comes with its own input/output format, training pipeline, and evaluation setup. This fragmentation makes routers difficult to use, hard to reproduce, and nearly impossible to compare fairly.
    - Over the past year, we worked on several LLM routing projects, including GraphRouter (ICLR’25), Router-R1 (NeurIPS’25), and PersonalizedRouter (TMLR’25). Through repeatedly implementing and benchmarking different routers, we realized that the main bottleneck is not algorithmic novelty, but the lack of standardized infrastructure.
    - Unified support for single-round, multi-round, agentic, and personalized routing
    - Integration of 16+ SOTA LLM router algorithms
    - One-line commands to run different routers without rebuilding pipelines

- https://github.com/Egham-7/adaptive-ai-provider /202510/ts
  - https://llmadaptive.uk/
  - The Adaptive AI Provider for the AI SDK contains language model support for adaptive provider selection across multiple AI services
  - Intelligent Model Selection - Automatically picks optimal models
  - Multi-Provider - OpenAI, Anthropic, Google, DeepSeek, Groq, etc.
  - [Adaptive AI Provider for the Vercel AI SDK — real-time model routing using UniRoute (Google Research) : r/vercel _202510](https://www.reddit.com/r/vercel/comments/1o5itci/adaptive_ai_provider_for_the_vercel_ai_sdk/)
    - It’s based on `UniRoute`, Google Research’s new framework for universal model routing across unseen LLMs.
    - Adaptive automatically chooses which LLM to use for every request based on prompt complexity and live model performance.
    - It runs automated evals continuously in the background, clusters prompts by domain, and routes each query to the smallest feasible model that maintains quality.
    - it performs live eval-based routing using UniRoute’s cluster-based generalization method, which can handle unseen LLMs without retraining.
    - Typical savings: 60–90% lower inference cost.
    - Routing overhead: ~10 ms.

- https://github.com/maximhq/bifrost /718Star/apache2/202510/go/ts
  - https://www.getmaxim.ai/bifrost
  - Fastest LLM gateway (50x faster than LiteLLM) with adaptive load balancer, cluster mode, guardrails, 1000+ models support & <100 µs overhead at 5k RPS.
  - Bifrost is a high-performance AI gateway that unifies access to 12+ providers (OpenAI, Anthropic, AWS Bedrock, Google Vertex, and more) through a single OpenAI-compatible API.
  - Multi-Provider Support - OpenAI, Anthropic, AWS Bedrock, Google Vertex, Azure, Cohere, Mistral, Ollama, Groq, and more
  - Automatic Fallbacks - Seamless failover between providers and models with zero downtime
  - Multimodal Support - Support for text, images, audio, and streaming, all behind a common interface.

- https://github.com/Dominic-Shirazi/ConductorAPI /MIT/202512/python/js
  - a powerful organization layer for your local AI API traffic. 
  - A single OpenAI-compatible endpoint that routes AI API requests and spins local models up or down to manage VRAM
  - Run Multiple Automation Tasks: Execute coding agents, chat bots, and summarizers simultaneously without conflict. The orchestrator queues them and switches models instantly.
  - Resource Management: Only one VRAM-heavy model runs at a time. The system automatically unloads idle models and loads the next one required.
  - Route Aliases: Use stable names like route:coding or route:chat. If your primary model is down or overloaded, the system can automatically fall back to another model (local or cloud).
  - Extensibility: Add any OpenAI-compatible provider (Groq, weak-to-strong-generalization rigs, custom RAG APIs) just by dropping a YAML file in the providers/ folder.
  - [Local AI: Managing VRAM by dynamically swapping models via API : r/LocalLLaMA](https://www.reddit.com/r/LocalLLaMA/comments/1pm36fl/local_ai_managing_vram_by_dynamically_swapping/)
    - Dynamically loads and unloads models on demand (easy to add additional runtimes)
      - Runs one request at a time using a queue to avoid VRAM contention, and groups requests for the same model together to reduce reload overhead
      - The next step is intelligently running more than one model concurrently when VRAM allows.
      - The core idea is treating models as on-demand workloads rather than long-running processes.
    - 🤔 This is now natively supported by llama.cpp.
      - llama.cpp can run image generation, video generation, audio generation and text generation?
    - I'd want to 'set' the limit to be 92GB so I still have VRAM for the system, and for it to close down applications. I've been thinking how to make it more efficient.
      - This is where I'm looking for either V2 or V3 to go. Although my system is much lighter, that assigned to this with concurrency and VRAM monitoring insight.

- https://huggingface.co/katanemo/Arch-Router-1.5B /LlamaLic/qwen2
  - [I built the HuggingChat Omni Router : r/ollama _202510](https://www.reddit.com/r/ollama/comments/1odn14n/i_built_the_huggingchat_omni_router/)
  - HuggingFace relaunched their chat app called Omni with support for 115+ LLMs.
  - The critical unlock in Omni is the use of a policy-based approach to model selection. I built that policy-based router: https://huggingface.co/katanemo/Arch-Router-1.5B
  - The core insight behind our policy-based router was that it gives developers the constructs to achieve automatic behavior, grounded in their own evals of which LLMs are best for specific coding tasks like debugging, reviews, architecture, design or code gen
  - Essentially, the idea behind this work was to decouple task identification (e.g., code generation, image editing, q/a) from LLM assignment.
  - The model is also integrated as a first-class primitive in archgw: a models-native proxy server for agents. 
  - https://github.com/katanemo/archgw /4.2kStar/apache2/202510/rust/python
    - https://archgw.com/
    - Arch is a models-native proxy server that handles the plumbing work in AI: agent routing & hand off, guardrails, end-to-end logs and traces, unified access to LLMs from OpenAI, Anthropic, Ollama, etc.
    - Arch handles the pesky plumbing work in building AI agents — like applying guardrails, routing prompts to the right agent, generating hyper-rich information traces for RL, and unifying access to any LLM.
    - Arch runs alongside app servers as a containerized process, and builds on top of `Envoy`'s proven HTTP management and scalability features to handle ingress and egress traffic related to prompts and LLMs.
    - Arch was built by the contributors of Envoy Proxy with the belief that: Prompts are nuanced and opaque user requests, which require the same capabilities as traditional HTTP requests including secure handling, intelligent routing, robust observability, and integration with backend (API) systems to improve speed and accuracy for common agentic scenarios – all outside core application logic.

- https://github.com/songquanpeng/one-api /27.7kStar/MIT/202502/go/js/inactive
  - LLM API 管理 & 分发系统，支持 OpenAI、Azure、Anthropic Claude、Google Gemini、DeepSeek、字节豆包
  - 支持配置镜像以及众多第三方代理服务。
  - 支持令牌管理，设置令牌的过期时间、额度、允许的 IP 范围以及允许的模型访问。
  - 🍴 forks
  - https://github.com/MartialBE/one-hub /apache2/202510/go/js
    - https://one-hub.xiao5.info/
    - OpenAI 接口管理 & 分发系统，改自songquanpeng/one-api。支持更多模型，加入统计页面，完善非openai模型的函数调用。
- https://github.com/QuantumNous/new-api /11.7kStar/AGPL+LOGO/202510/go/js
  - https://www.newapi.ai/
  - AI模型聚合管理中转分发系统，支持将多种大模型转为统一格式调用，支持OpenAI、Claude、Gemini等格式，可供个人或者企业内部管理与分发渠道使用
  - 新一代大模型网关与AI资产管理系统
  - 在One API的基础上进行二次开发
  - [有没有什么能够聚合中转站api的项目呢？ - 开发调优 - LINUX DO](https://linux.do/t/topic/1172062)
  - https://github.com/Veloera/Veloera /GPL/202510/go/js
    - 优秀的 AI API 网关系统
    - 原汁原味的 New API 体验, 对界面无大改动, 遵循 GPL 3.0 协议, 无商用限制
    - 支持礼品码, 全局每用户一次, 可控制总使用次数
    - 渠道 Key 不再加密, 发送到前端显示
    - 本程序基于 new-api 二开, 数据库结构基本兼容, 会自动运行迁移.

- https://github.com/deanxv/done-hub /apache2/202510/go/js
  - 基于one-hub二次开发而来的
  - [基于 One-Hub 的二开项目 Done-Hub ](https://linux.do/t/topic/712560)
    - 支持 /gemini 原生生图请求的额外参数透传
    - 支持 gemini-2.0-flash-preview-image-generation 文生图 / 图生图，并兼容 OpenAI 对话接口

- https://github.com/james-6-23/new_api_tools /202512/python/ts
  - NewAPI-Tool 是一个专为 NewAPI (One API 分支) 设计的现代化增强管理中间件。
  - 它通过直观的 Web 界面，补全了原版系统在数据可视化、充值记录审计、批量兑换码管理等方面的功能，帮助管理员更高效地运维系统
  - 实时概览：用户数、Token、渠道、模型、兑换码等关键指标一目了然。
  - 兑换码增强管理
  - 充值记录审计
  - 独立认证：拥有独立的管理后台登录机制，支持 JWT Session。
  - 多数据库支持：完美支持 MySQL 和 PostgreSQL。

- https://github.com/tbphp/gpt-load /5.4kStar/MIT/202510/go/ts/vue
  - https://www.gpt-load.com/
  - 智能密钥轮询的多渠道 AI 代理

- https://github.com/eraycc/API-Gateway-Manager /202511/ts
  - 基于 Next.js 的 AI API 中转站管理系统
  - 支持多用户、API 站点管理、模型测试与统一认证
  - 双系统登录：用户系统 + 管理员系统, 管理员可无缝切换用户/管理系统
  - 多站点支持：管理多个 AI API 中转站
  - 额度查询：实时查询 API 使用额度（目前仅限 newapi）

- https://github.com/fruitbars/simple-one-api /2.3kStar/MIT/202506/go/js
  - OpenAI 接口接入适配，支持千帆大模型平台、讯飞星火大模型、腾讯混元以及MiniMax、Deep-Seek，等兼容OpenAI接口，仅单可执行文件，配置超级简单，一键部署，开箱即用
  - 目前市面上免费的使用国产的免费大模型越来越多，one-api对于个人用起来还是有点麻烦，就想要一个不要统计、流量、计费等等的适配程序即可。
  - 即使有些厂商说兼容openai的接口，但是实际上还是存在些许差异的
  - simple-one-api主要是解决以上2点，旨在兼容多种大模型接口，并统一对外提供 OpenAI 接口。

- https://github.com/jwy87/SimpleHub /MIT/202601/js
  - 多站点管理：统一管理多个 AI 中转站，支持 NewAPI、Veloera、DoneHub、VOAPI 等主流平台
  - 模型变更检测：自动追踪模型列表的增删改，精确记录每次变化
  - 智能签到：支持 NewAPI、Veloera 平台自动签到，每日自动领取奖励
  - [[开源]小白搓了一个API聚合管理站（含自动签到） ](https://linux.do/t/topic/1095754)

- https://github.com/qixing-jk/all-api-hub /722Star/AGPL/202601/ts
  - http://all-api-hub.qixing1217.top/
  - 统一管理第三方 AI 聚合中转站与自建 New API：自动识别账号、查看余额、同步模型、管理密钥，全平台与云端备份
  - 站点信息管理 - 多方式获取真实站点名称，支持签到状态检测和自动签到，可手动添加任意 AI 聚合中转站点
  - 每个站点支持多个账号，账号分组与快速切换，余额和使用日志一目了然
  - 查看站点支持的模型列表和价格信息
  - 提供 New API 渠道管理 Beta 界面，直接在插件内维护渠道与重定向
  - 全平台兼容 - 支持 Chrome、Firefox 浏览器，可在 Kiwi Browser 等移动端使用，支持深色模式自动切换
  - WXT 负责多浏览器扩展工具链与构建流程
  - [All-API-Hub：开源AI中转站集中管理和自己的New API增强管理，基于 one-api-hub 大幅重构增强 _202511](https://linux.do/t/topic/1001042)
  - 最初基于 One API Hub 开发，现已大幅重构扩展。数据格式保持兼容，支持直接导入
  - https://github.com/fxaxg/one-api-hub /MIT/202509/ts/inactive
    - https://fxaxg.github.io/one-api-hub/
    - 一个开源的浏览器插件，聚合管理AI中转站账号的余额、模型和密钥，告别繁琐登录
    - [[开源] One-API-Hub：管理您的所有AI中转站账号的余额、模型和密钥，告别繁琐登录 _202507](https://linux.do/t/topic/833269)

## router-image 🖼️

- https://github.com/Amery2010/peinture /392Star/MIT/202512/ts
  - https://peinture.9th.xyz/
  - A general-purpose AI image generation framework that supports Hugging Face, Gitee, Model Scope, and more.
  - [【开源】派奇智图，AI 图片生成服务，合理白嫖各大平台的算力资源 _202512](https://linux.do/t/topic/1290598)
    - 目前 Hugging Face 对于匿名用户，每天有 2分钟的算力资源，使用 Token，可以获得额外的 3.5 分钟算力资源。
    - 目前 Gitee AI 使用 Token 每天都可以获得 100 次的 API 调用次数，理论上可以生成 100 张图片。需要注意的是，提示词优化也会计算入 API 调用次数
    - 目前 Model Scope 使用 Token 每天都可以获得 2000 次的 API 调用次数，对于单个模型的调用官方限制为 500 次，理论上可以生成 500 张图片。
    - 根据用户反馈 Hugging Face 与 Gitee AI 可以生成无审核的 NSFW 图片，我没有在 Model Scope 上试过，因此无法确定 Model Scope 是否存在审核机制
    - 题外话：Gitee AI 与 Model Scope 的提示词优化使用的是 DeepSeek 3.2 这个模型，这个模型在生成中文描述上十分惊艳。
  - [【即将开源】 诚邀大家试用派奇智图服务端 API - 开发调优 - LINUX DO](https://linux.do/t/topic/1368202)
    - 随着项目的完善，不少佬友希望可以分享给朋友们用，经过几天的努力，终于开发了 Peinture 服务端，可以直接以 API 的形式直接给项目提供图片生成服务。

- https://github.com/lianwusuoai/img-router /MIT/202512/ts
  - 三合一图像生成 API 中转服务- 一个接口，多渠道图像生成
  - 三渠道支持 - 火山引擎、Gitee (模力方舟)、ModelScope (魔塔)
  - OpenAI 兼容 - 完全兼容 /v1/chat/completions 接口格式
  - 图片参考 - 支持上传参考图片进行图生图
  - 开箱即用的容器化部署方案
  - [开源：豆包和Z-Image对话生图/改图全免费且自由 ](https://linux.do/t/topic/1358465)

- https://github.com/coulsontl/uni-image-api /202512/python
  - 将第三方图像生成/编辑 API 转换为 OpenAI 兼容格式的代理服务。
  - 可扩展架构: 基于 Provider 模式，易于添加新的第三方服务
  - 基于 FastAPI 和 httpx 的全异步实现
  - 支持将图片上传到 S3 兼容存储（AWS S3、MinIO、阿里云 OSS 等）
  - 碰到了有相同想法的佬友；之前我也做了一个，不过我只做了一个魔搭，但是支持了图生图

## agent-fwk-vendors

- https://github.com/cuga-project/cuga-agent /341Star/apache2/202512/python/ts/ibm
  - https://huggingface.co/spaces/ibm-research/cuga-agent/tree/main
  - https://cuga.dev/
  - CUGA is an open-source generalist agent for the enterprise, supporting complex task execution on web and APIs, OpenAPI/MCP integrations, composable architecture, reasoning modes, and policy-aware features.
  - High-performing generalist agent — Benchmarked on complex web and API tasks. 
  - integrate tools via OpenAPI specs, MCP servers, and Langchain, enabling rapid connection to REST APIs, custom protocols, and Python functions
  - Integrates with Langflow — Low-code visual build experience for designing and deploying agent workflows
  - composable — Built with modularity in mind, CUGA itself can be exposed as a tool to other agents, enabling nested reasoning and multi-agent collaboration
  - Configurable policy and human-in-the-loop instructions (Experimental)
  - Save-and-reuse capabilities (Experimental) — Capture and reuse successful execution paths (plans, code, and trajectories) for faster and consistent behavior across repeated tasks
  - Cuga supports isolated code execution using Docker/Podman containers for enhanced security.
  - [CUGA on Hugging Face: Democratizing Configurable AI Agents _202512](https://huggingface.co/blog/ibm-research/cuga-on-hugging-face)

- https://github.com/firebase/genkit /5.2kStar/apache2/202512/ts
  - https://genkit.dev/
  - open-source framework for building full-stack AI-powered applications, built and used in production by Google's Firebase
  - It provides SDKs for js/python/go
  - It offers a unified interface for integrating AI models from providers like Google, OpenAI, Anthropic, Ollama, and more. 
# ai-api

# browser-use
- https://github.com/browser-use/browser-use /57.9kStar/MIT/202504/python/js
  - https://browser-use.com/
  - Enable AI to control your browser
  - [Pack 拆解 browser-use 项目 ](https://quaily.com/silico-anatomy/packs/110)
- https://github.com/browser-use/web-ui /MIT/202504/python
  - This project builds upon the foundation of the browser-use, which is designed to make websites accessible for AI agents.
  - WebUI: is built on Gradio and supports most of browser-use functionalities.
  - support for various Large Language Models (LLMs), including: Google, OpenAI, Azure OpenAI, Anthropic, DeepSeek, Ollama etc. 
  - You can choose to keep the browser window open between AI tasks, allowing you to see the complete history and state of AI interactions.

- https://github.com/microsoft/playwright-mcp /apache2/202503/ts
  - A Model Context Protocol (MCP) server that provides browser automation capabilities using Playwright. 
  - This server enables LLMs to interact with web pages through structured accessibility snapshots, bypassing the need for screenshots or visually-tuned models.
  - https://x.com/playwrightweb/status/1904265499422409047
    - we went ahead and built an MCP server for Playwright. Ours is snapshot-based, which makes it faster and more reliable! You can opt into the visual mode too.

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
- https://github.com/bytedance/UI-TARS-desktop /9.6kStar/apache2/202503/ts
  - https://agent-tars.com/
  - A GUI Agent application based on UI-TARS(Vision-Language Model) that allows you to control your computer using natural language.
  - ❓ agent-tars似乎支持replay，ui-tars是否支持replay
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
# protocols-ai
- https://github.com/agentclientprotocol/agent-client-protocol /871Star/apache2/202510/rust/ts
  - https://github.com/zed-industries/agent-client-protocol
  - https://agentclientprotocol.com/
  - A protocol for connecting any editor to any agent
  - [Bring Your Own Agent to Zed — Featuring Gemini CLI — Zed's Blog _202508](https://zed.dev/blog/bring-your-own-agent-to-zed)
# crawler-ai
- https://github.com/mendableai/firecrawl /AGPLv3/202502/python/rust/ts
  - https://firecrawl.dev/
  - Turn entire websites into LLM-ready markdown or structured data. 
  - Scrape, crawl and extract with a single API.
  - The hard stuff: proxies, anti-bot mechanisms, dynamic content (js-rendered), output parsing, orchestration
  - Batching (New): scrape thousands of URLs at the same time with a new async endpoint.
  - open-version: scrape, extract, map, formats, sdk
  - cloud-version: anti-bot, dashboard, actions, browserless, enterprise
  - This project is primarily licensed under AGPLv3
    - However, certain components of this project are licensed under the MIT 
    - The SDKs and some UI components are licensed under the MIT License. 

- https://github.com/getmaxun/maxun /AGPL/202503/ts
  - https://www.maxun.dev/
  - Open-source no-code web data extraction platform. 
  - Maxun lets you create custom robots which emulate user actions and extract data. A robot can perform any of the actions: Capture List, Capture Text or Capture Screenshot. Once a robot is created, it will keep extracting data for you without manual intervention

- https://github.com/dylan-sutton-chavez/llm-web-crawler /202510/python
  - A horizontally scalable web crawling engine designed for structured content extraction. 
  - It performs URL normalization, HTML parsing, Markdown conversion, and LLM post-processing (using xai_sdk with grok). 
  - Output is serialized in line-delimited JSON (`.jsonl`).
  - A crawler functions similarly to how a graph works. Basically, each web page behaves like a node, where a single node can point to n number of websites, and multiple nodes can point to the same website. The navigation of a crawler is based on the same principle as a graph traversal; in this case, I will base it on a breadth-first search (`BFS`) model.
  - The Crawler module implements a horizontal-scalable architecture, where you can create one Crawler module with hundreds of nodes (sharing the same memmory, but managing hundreds of asynchronous processes).
  - 依赖 requests、html-to-markdown、jsonlines、xai_sdk
# github-repo
- https://github.com/ahmedkhaleel2004/gitdiagram /MIT/202503/python/ts
  - https://gitdiagram.com/
  - Turn any GitHub repository into an interactive diagram for visualization in seconds.
  - Powered by Claude 3.5 Sonnet for quick and accurate diagrams
  - Public API available for integration (WIP)
  - Frontend: Next.js, TypeScript, Tailwind CSS, ShadCN
  - Backend: FastAPI, Python, Server Actions
  - Database: PostgreSQL (with Drizzle ORM)
  - Deployment: Vercel (Frontend), EC2 (Backend)
  - Analytics: PostHog, Api-Analytics
# perf/large
- https://github.com/MoonshotAI/MoBA /MIT/202502/python
  - Mixture of Block Attention for Long-Context LLMs
  - https://x.com/tuturetom/status/1892753818028216717
    - 可以实现近乎无限的上下文窗口，将一整本书或一整个代码库扔进去提问
# utils
- https://github.com/Olow304/memvid /MIT/202506/python
  - https://pypi.org/project/memvid/
  - Video-based AI memory library. 
  - Store millions of text chunks in MP4 files with lightning-fast semantic search. No database needed.
  - Memvid revolutionizes AI memory management by encoding text data into videos, enabling lightning-fast semantic search across millions of text chunks with sub-second retrieval times. 
  - Unlike traditional vector databases that consume massive amounts of RAM and storage, Memvid compresses your knowledge base into compact video files while maintaining instant access to any piece of information.
  - Video-as-Database: Store millions of text chunks in a single MP4 file
  - Efficient Storage: 10x compression compared to traditional databases
  - PDF Support: Direct import and indexing of PDF documents
  - Built-in Chat: Conversational interface with context-aware responses
  - Pluggable LLMs: Works with OpenAI, Anthropic, or local models
  - Offline-First: No internet required after video generation

## streaming-llm

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
# eval/prompt
- https://github.com/promptfoo/promptfoo /9.6kStar/MIT/202512/ts
  - https://promptfoo.dev/
  - promptfoo is a developer-friendly local tool for testing LLM applications. 
  - Stop the trial-and-error approach - start shipping secure, reliable AI apps.
  - Test your prompts and models with automated evaluations
  - Compare models side-by-side (OpenAI, Anthropic, Azure, Bedrock, Ollama, and more)
# model-proxy
- https://github.com/lymanzhao/Ollama-serve /202503/python
  - 一个 Ollama转发代理，用于为原生 Ollama 服务添加 API 密钥认证功能。
  - 该项目解决了 Ollama 官方不提供 API 密钥验证的问题，使您可以更安全地部署 Ollama 服务并防止未授权访问
# model-2api
- https://github.com/star5o/reverse-check /MIT/202504/js/vue
  - https://reverse-check.no-reverse-api.com/
  - LLM API 逆向检测工具
  - 本工具是一个基于是否支持官方参数的逆向检测工具。不能通过本工具检测的API极大概率是逆向的。
  - 目前项目处于初步阶段，暂时需要人工对比响应结果与示例进行判断。
  - 支持多种模型提供商的API检测: OpenAI, Claude, Gemini

- https://github.com/router-for-me/CLIProxyAPI /3.4kStar/MIT/202512/go
  - Wrap Gemini CLI, Antigravity, ChatGPT Codex, Claude Code, Qwen Code, iFlow as an OpenAI/Gemini/Claude/Codex compatible API service, allowing you to enjoy the free Gemini 2.5 Pro, GPT 5, Claude, Qwen model through API
  - A proxy server that provides OpenAI/Gemini/Claude/Codex compatible API interfaces for CLI.
  - It now also supports OpenAI Codex (GPT models) and Claude Code via OAuth.
  - https://github.com/router-for-me/Cli-Proxy-API-Management-Center /MIT/202601/ts
    - a WebUI interface based on CLI-Proxy-API, designed to simplify configuration modifications and runtime status monitoring.
    - Since version 6.0.19, the WebUI ships with the main program; access it via `/management.html` on the API url
  - https://github.com/router-for-me/CLIProxyAPIPlus /MIT/202512/go
    - the Plus version of CLIProxyAPI, adding support for third-party providers on top of the mainline project.
    - Added GitHub Copilot support (OAuth login)
    - Added Kiro (AWS CodeWhisperer) support (OAuth login)
- https://github.com/automazeio/vibeproxy /688Star/MIT/202512/swift
  - Native macOS menu bar app to use your Claude Code & ChatGPT subscriptions with AI coding tools - no API keys needed
  - native macOS menu bar app that lets you use your existing Claude Code, ChatGPT, Gemini, Qwen, and Antigravity subscriptions with powerful AI coding tools like Factory Droids – no separate API keys required.
  - Built on CLIProxyAPIPlus, it handles OAuth authentication, token management, and API routing automatically. One click to authenticate, zero friction to code.

- https://github.com/zhalice2011/ProxyLLM /MIT/202601/ts
  - Electron 应用，用于捕获 LLM 网站的浏览器会话，并在本机暴露 OpenAI 兼容 API
  - OpenAI 兼容 API：POST /v1/chat/completions、GET /v1/models，以及 Anthropic 原生 POST /v1/messages。
  - 多站点控制面板：添加/删除站点、打开/刷新窗口、查看请求并选择凭据。
  - 适配器体系：将不同站点协议转换为 OpenAI 格式，内置多种特定适配器。
  - 凭据捕获：Electron webRequest、CDP（HTTP + WebSocket），以及可选本地 MITM 代理。
  - Claude Code 接管/恢复：将 Claude CLI 指向本地代理。

- https://github.com/justlovemaki/AIClient-2-API /1.9kStar/GPL/202512/js
  - an API proxy service that breaks through client limitations, converting free large models originally restricted to client use only (such as Gemini, Antigravity, Qwen Code, Kiro) into standard OpenAI-compatible interfaces

- https://github.com/aiclientproxy/proxycast /632Star/GPL/202512/rust/ts
  - https://aiclientproxy.github.io/proxycast/
  - 把你的 AI 客户端额度用到任何地方
  - https://x.com/geekbb/status/2002235372345122842
    - 服务是中午部署的，号是下午封的

- https://github.com/axibayuit-a11y/2apifare /CC-NC/202512/python
  - 将 GeminiCLI 转换为 OpenAI 和 GEMINI API 接口
  - 多种认证方式：支持 Authorization Bearer、x-goog-api-key 头部、URL 参数等
  - 多种流式支持
  - 自动记录 IP 请求统计（仅统计成功的 AI 响应）

- https://github.com/lza6/zai.is-2api-python /apache2/202512/python
  - 解锁 Zai.is 的无限潜能 (Python版)

- https://github.com/lza6/Qwen-2api /apache2/202510/python
  - 通义千问高性能API代理
  - 需自备 Cookie、采用 Nginx + FastAPI 高性能架构、支持粘性会话与多账号轮询、原生流式 API 转换、Docker 一键部署

- https://github.com/BlueSkyXN/AI2API /GPL/202508/go
  - Many AI-> API (OpenAI/DeepSeek)

- https://github.com/ben-vargas/ai-sdk-provider-opencode-sdk /MIT/202512/ts
  - A community provider for the Vercel AI SDK that enables using AI models through OpenCode and the @opencode-ai/sdk. 
  - This provider enables you to use OpenCode's AI capabilities through the familiar Vercel AI SDK interface, supporting generateText(), streamText(), generateObject(), and streamObject().

- https://github.com/lza6/notion-2api /apache2/202510/python
  - 将你强大的 Notion AI 体验，无缝转换为兼容 OpenAI 格式的 API 服务的神奇项目。这意味着，你可以将 Notion AI 作为后端，驱动任何支持 OpenAI API 的应用程序、脚本或服务。
# more
- https://github.com/beuaaa/pywinauto_recorder /MIT/202411/python
  - https://pywinauto-recorder.readthedocs.io/
  - A record-replay tool to automate GUI via pywinauto
  - records user interface actions and saves them in a Python script. The saved Python script can be run to replay the user interface actions previously recorded.
  - "Pywinauto recorder" is a unique inspect/record/replay tool in the open source field because it generates reliable scripts without hard-coded coordinates thanks to Pywinauto.
  - The functions of the generated Python script return Pywinauto wrappers so it can be enhanced with Pywinauto methods.
