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

- https://github.com/github/copilot-sdk /5.9kStar/MIT/202601/ts
  - Embed Copilot's agentic workflows in your application—now available in Technical preview as a programmable SDK for Python, TypeScript, Go, and . NET.
  - The GitHub Copilot SDK exposes the same engine behind Copilot CLI: a production-tested agent runtime you can invoke programmatically. No need to build your own orchestration—you define agent behavior, Copilot handles planning, tool invocation, file edits, and more.
  - All SDKs communicate with the Copilot CLI server via JSON-RPC
  - a GitHub Copilot subscription is required to use the GitHub Copilot SDK. 
  - [GitHub introduces Copilot SDK (open source) – anyone can now build Copilot-style agents : r/LocalLLaMA](https://www.reddit.com/r/LocalLLaMA/comments/1qoa9h5/github_introduces_copilot_sdk_open_source_anyone/)

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
  - [streaming v2  _202507](https://github.com/mastra-ai/mastra/pull/5965)
    - A new streaming protocol that allows us to stream all mastra primitives, agent, tools, workflows. (soon networks). Our old protocol was based on Vercel's AI sdk datatprtocol which works great for agents but not for workflows, networks and the future of Mastra.
    - The new protocol allows us to nest streams and calculate usage values of all primitives.

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

- https://github.com/strands-agents/sdk-python /5kStar/apache2/202601/python
  - https://strandsagents.com/
  - A model-driven approach to building AI agents in just a few lines of code.
  - Strands Agents is a simple yet powerful SDK that takes a model-driven approach to building and running AI agents
  - Lightweight & Flexible: Simple agent loop that just works and is fully customizable
  - Model Agnostic: Support for Amazon Bedrock, Anthropic, Gemini, LiteLLM, Llama, Ollama, OpenAI, Writer, and custom providers
  - Advanced Capabilities: Multi-agent systems, autonomous agents, and streaming support
  - Built-in MCP: Native support for Model Context Protocol (MCP) servers, enabling access to thousands of pre-built tools

- https://github.com/badlogic/pi-mono /4.5kStar/MIT/202602/ts
  - AI agent toolkit: coding agent CLI, unified LLM API, TUI & web UI libraries, Slack bot, vLLM pods
  - [Pi: The Minimal Agent Within OpenClaw | Armin Ronacher's Thoughts and Writings _202601](https://lucumr.pocoo.org/2026/1/31/pi/)
  - https://x.com/shao__meng/status/2017745045156467003
    - Pi 可能是当今系统提示词最短的编程 Agent——只有 Read、Write、Edit、Bash 四个工具，但它支撑了本周互联网上最火的项目 @openclaw
  - https://x.com/mitsuhiko/status/2017604638137012335
    - Self-extending agents are exciting, but the moment they can rewrite their own tools you need change control like a real system: pinned versions, eval gates, and a rollback path. Otherwise “it got better” turns into “it drifted.”

## deep-research

- https://github.com/666ghj/BettaFish /34.1kStar/GPL/202601/python
  - https://deepwiki.com/666ghj/BettaFish
  - 微舆：人人可用的多Agent舆情分析助手，打破信息茧房，还原舆情原貌
  - 构建了从 BettaFish（数据收集与分析）到 MiroFish（全景预测）的完整链路
  - 💡 不一定要做通用research, 细分场景的产品也有优点

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
# router/gateway
- https://github.com/BerriAI/litellm /34kStar/MIT+EE/202601/python/ts
  - https://docs.litellm.ai/docs/
  - Python SDK, Proxy Server (LLM Gateway) to call 100+ LLM APIs in OpenAI format - [Bedrock, Azure, OpenAI, VertexAI, Cohere, Anthropic, Sagemaker, HuggingFace, Replicate, Groq]
  - Translate inputs to provider's completion, embedding, and image_generation endpoints
  - Consistent output, text responses will always be available at ['choices'][0]['message']['content']
  - Set Budgets & Rate limits per project, api key, model

- https://github.com/ssrsgaga/API-Check /MIT/202601/ts
  - https://api-check-beta.vercel.app/
  - 快速的大模型 API 连通性测试工具。纯前端运行，支持 OpenAI 格式，数据仅在本地存储。
  - [API Check大模型批量测活助手【多功能免费开源/Vercel一键部署/纯前端 _202601](https://linux.do/t/topic/1384242)

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

- https://github.com/songquanpeng/one-api /27.7kStar/MIT/202502/go/js/inactive
  - LLM API 管理 & 分发系统，支持 OpenAI、Azure、Anthropic Claude、Google Gemini、DeepSeek、字节豆包
  - 支持配置镜像以及众多第三方代理服务。
  - 支持令牌管理，设置令牌的过期时间、额度、允许的 IP 范围以及允许的模型访问。
  - 🍴 forks
  - https://github.com/MartialBE/one-hub /2.6kStar/apache2/202601/go/js
    - https://one-hub-doc.vercel.app/
    - https://one-hub.xiao5.info/  /demo
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

- https://github.com/deanxv/done-hub /574Star/apache2/202601/go/js
  - https://github.com/MartialBE/one-hub/wiki/Deployment
  - 基于one-hub二次开发而来的
  - 优先级大的优先调用，同优先级，基于权重轮询； 想要轮询的话还是同优先级设置权重
  - 目前与原版(最新镜像)的区别
    - 支持反代渠道
    - 支持批量删除渠道
    - 支持自定义渠道使用Claude原生路由 - 接入ClaudeCode
    - 新增邀请码设置模块
  - [基于 One-Hub 的二开项目 Done-Hub ](https://linux.do/t/topic/712560)
    - 支持 /gemini 原生生图请求的额外参数透传
    - 支持 gemini-2.0-flash-preview-image-generation 文生图 / 图生图，并兼容 OpenAI 对话接口
  - [同渠道多API轮询功能 ](https://github.com/MartialBE/one-hub/issues/791)
    - 用tag就行了
    - 在一个tag下的渠道，是随机还是轮询？
    - 随机，但是特定条件失败的渠道回冻结一定时间并切换渠道
  - [feat(openai)：适配一些兼容openai接口的url，但是版本号不是v1的  · Pull Request · MartialBE/one-hub](https://github.com/MartialBE/one-hub/pull/546)
  - [已有渠道的模型映射无法正删改查，整个呈现灰色 · Issue · MartialBE/one-hub](https://github.com/MartialBE/one-hub/issues/380)
    - 是不是填写了 标签。 把标签删了
    - 这是用于批量管理的。 你添加后要去 渠道标签 修改
  - [有接入豆包的计划吗?  ](https://github.com/MartialBE/one-hub/issues/323)
    - 直接用 openai + 模型映射就可以了
    - 渠道API地址 Base URL 填入 https://ark.cn-beijing.volces.com
    - ChatCompletions地址 填入 /api/v3/chat/completions
  - [new-api、one-api、chatnio对比以及令牌限制可用模型 ](https://github.com/MartialBE/one-hub/issues/332)
  - [通过OneHub接入字节火山引擎教程 ](https://linux.do/t/topic/412857)
  - [[Bug] 无法对相同模型不同名称(deepseek-r1和deepseek-ai/deepseek-r1)的模型负载均衡调用 ](https://github.com/songquanpeng/one-api/issues/2170)
  - [希望日志同时记录“用户请求模型”和“实际转发模型” ](https://github.com/MartialBE/one-hub/issues/581)
    - 配置映射的时候在实际模型名字前面添加＋号log就记录的请求名称
  - [一站式多模型管理：One API实用指南](https://gameapp.club/post/2024-06-10-oneapi-and-models-tips/)
  - [不同模型厂商, 同一模型名称 的处理 ](https://github.com/MartialBE/one-hub/issues/562)
    - 202503: 不同模型厂商, 同一模型名称 这个不行， 因为请求的时候 是通过模型名称来查找渠道的， 用户不能指定 供应商，或许可以用分组来解决
  - [请教oneapi负载均衡问题 ](https://linux.do/t/topic/108049)
    - 楼主想要的是一个渠道里多个 key 负载均衡，批量创建完是分成多个渠道
  - [one-api负载均衡疑问 ](https://linux.do/t/topic/210397)
  - [百度文心模型调用异常 ](https://github.com/MartialBE/one-hub/issues/208)
    - failed to get token encoder for model ERNIE-Speed: no encoding for model ERNIE-Speed, using encoder for gpt-3.5-turbo 这个报错是只没有找到这个模型的tokens计算，可以无视

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

- https://github.com/looplj/axonhub /1.3kStar/LGPL+apache2/202601/go/ts
  - https://axonhub.onrender.com/
  - AI gateway system that provides a unified OpenAI ( Chat Completion, Responses), Anthropic, Gemini and AI SDK compatible API
  - 后端：Go + ent + gqlgen
  - 前端：React + TypeScript + Shadcn + Graphql
  - 本项目和 new-api 等项目的不同，本项目目标用户是 AI 产品开发者，不是中转服务商，所以会有更多开发监控相关能力，比如 Trace。
  - [分享自己开源的一个肝了一段时间的 AI 网关项目 _202511](https://linux.do/t/topic/1153975)
    - OpenAI/Anthropic 请求格式互转
    - 渠道管理，项目管理，权限控制，用户管理，API Key 管理
    - 低侵入 LLM API Trace ，支持不需要 SDK 就可以 trace 一次对话的多个 request，以及保存 Request 和 Response 内容，方便排查问题

- https://github.com/jwy87/SimpleHub /MIT/202601/js
  - 多站点管理：统一管理多个 AI 中转站，支持 NewAPI、Veloera、DoneHub、VOAPI 等主流平台
  - 模型变更检测：自动追踪模型列表的增删改，精确记录每次变化
  - 智能签到：支持 NewAPI、Veloera 平台自动签到，每日自动领取奖励
  - [[开源]小白搓了一个API聚合管理站（含自动签到） ](https://linux.do/t/topic/1095754)

- https://github.com/qixing-jk/all-api-hub /722Star/AGPL/202601/ts
  - http://all-api-hub.qixing1217.top/
  - 开源浏览器插件，统一管理第三方 AI 聚合中转站与自建 New API：自动识别账号、查看余额、同步模型、管理密钥，全平台与云端备份
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

- https://github.com/Sponge-Lu/API_detect_tools /MIT/202601/ts
  - 管理API公益站的桌面端，可签到可添加福利站，专为管理和监控多个 API 中转站而设计。
  - 基于 Electron + React + TypeScript 构建。
  - API Key 管理：在桌面端直接创建、删除、分组管理 API Key，支持批量操作

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
  - https://github.com/Amery2010/imagine-server /MIT/202601/ts
    - 基于 Hono 构建的统一 AI 图像生成 API 服务，支持多个 AI 提供商（Hugging Face、Gitee AI、ModelScope），提供文生图、图生图、图生视频、图像放大等功能。
    - 模块化的 Provider 系统，轻松扩展新的 AI 服务提供商
    - 集成 Peinture 提供友好的图形界面
    - 自动切换和管理多个 API Token，配额耗尽时自动切换
    - 使用 Unstorage 支持 Redis、Cloudflare KV 等多种存储后端
    - 多平台部署 - 支持 Cloudflare Workers、Vercel、Node.js 等多种部署环境
    - Token 统计 - 实时查看各提供商的 Token 使用情况
    - [【开源】Peinture（派奇智图） 的服务端 Imagine Server 正式开源 ](https://linux.do/t/topic/1404399)
      - 如何加载本地部署的qwen image edit
      - 本地部署的，我目前没做兼容，您可以根据文档描述，自己写一个自定义的本地渠道
      - 目前开发精力有限，只能选择优先级更高的需求进行开发。后续会增加 nano banana 、gpt-image 这类对话型 AI 模型的支持，本地模型由于 API 类型太多多样化，暂时没办法一一适配。
      - 怎么和热门开源聊天ui比如openwebui/librechat结合使用啊
      - 后面会增加 OpenAI 兼容格式的 API 输出
  - [【开源】这款免费不限量的 Z-Image 网站，支持 A4F 免费模型，同时增加了 99% 没听说过的 OPFS 支持，允许用户在浏览器中长期保存大量文件（无服务器使用画廊功能） ](https://linux.do/t/topic/1498882)
    - 图片生成后会默认下载并保存到临时的 OPFS 存储空间，这样在本地查看或操作图片时就无需再从网络上下载文件，也无需担心文件短时间内过期的问题

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

## model-router

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
# perf/large
- https://github.com/MoonshotAI/MoBA /MIT/202502/python
  - Mixture of Block Attention for Long-Context LLMs
  - https://x.com/tuturetom/status/1892753818028216717
    - 可以实现近乎无限的上下文窗口，将一整本书或一整个代码库扔进去提问
# filesystem
- https://github.com/tursodatabase/agentfs /2.2kStar/MIT/202602/rust
  - https://www.agentfs.ai/
  - AgentFS is a filesystem explicitly designed for AI agents. Just as traditional filesystems provide file and directory abstractions for applications, AgentFS provides the storage abstractions that AI agents need
  - AgentFS Specification - SQLite-based agent filesystem specification.
  - [pg-fs: Postgres backed filesystem for AI Agents : r/VercelAISDK](https://www.reddit.com/r/VercelAISDK/comments/1qzbfcv/pgfs_postgres_backed_filesystem_for_ai_agents/)
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

- https://github.com/mohamad-tohidi/texttools /MIT/202601/python
  - a high-level NLP toolkit built on top of LLMs.
  - utilities for translation, question detection, categorization, NER extraction, and more
# eval/prompt
- https://github.com/promptfoo/promptfoo /9.6kStar/MIT/202601/ts/对比表/code-first
  - https://promptfoo.dev/
  - promptfoo is a developer-friendly local tool for testing LLM applications. 
  - Stop the trial-and-error approach - start shipping secure, reliable AI apps.
  - Test your prompts and models with automated evaluations
  - Compare models side-by-side (OpenAI, Anthropic, Azure, Bedrock, Ollama, and more)
  - thinking模型的`<think>`内容会算在`max_tokens`范围内，所以可能取不到内容
  - 通过promptfoo测试多个模型的翻译能力, 鼠标hover在表头列可以看到模型信息, prompt不变时只会增量请求新加的prompt
  - promptfoo eval --output mt2601-results.html --output mt2601-results.json
  - https://github.com/promptfoo/promptfoo/tree/main/examples/lm-studio
    - This example demonstrates how to use Promptfoo with LM Studio for prompt evaluation. It showcases configuration for interacting with the LM Studio API using a locally hosted language model.
  - The above examples create a table of outputs that can be manually reviewed. By setting up assertions, you can automatically grade outputs on a pass/fail basis.
  - [Does promptfoo accept multimodal input _202407](https://github.com/promptfoo/promptfoo/issues/1164)
    - Yes, it does, and we have several examples.
    - Local Models via LM Studio can easily be adapted for image input too.

- https://github.com/Laszlobeer/llm-tester /202507/python/inactive
  - benchmarking tool for evaluating Ollama language models. 
  - Measure performance metrics including latency, throughput, and token generation speed through a sophisticated PyQt5 GUI.
  - Concurrent Benchmarking: Test with up to 10 simultaneous requests
  - 100+ Diverse Prompts: Pre-configured benchmark questions
  - Summary table shows aggregate metrics
    - Latency
    - Tokens/s
    - Throughput
  - [Introducing OllamaBench: The Ultimate Tool for Benchmarking Your Local LLMs (PyQt5 GUI, Open Source) : r/ollama _202507](https://www.reddit.com/r/ollama/comments/1mbdd4a/introducing_ollamabench_the_ultimate_tool_for/)
    - What would be cool is to run a test prompt on several LLMs at once. Grid Search does it, but we don’t have the benchmarks (and it’s broken right now for OS X).

- https://github.com/dezoito/ollama-grid-search /896Star/MIT/202511/rust/ts
  - [Grid Search on Large Language Models using Ollama and Rust  _202312](https://dezoito.github.io/2023/12/27/rust-ollama-grid-search.html)
  - multi-platform desktop application to evaluate and compare LLM models, written in Rust and React.
  - This project automates the process of selecting the best models, prompts, or inference parameters for a given use-case, allowing you to iterate over their combinations and to visually inspect the results.
  - It assumes Ollama is installed and serving endpoints, either in localhost or in a remote server.
  - Automatically fetches models from local or remote Ollama servers; 
  - A/B test different prompts on several models simultaneously; 
  - Allows limited concurrency or synchronous inference calls (to prevent spamming servers); 

- https://github.com/ianarawjo/ChainForge /2.9kStar/MIT/202510/python/ts
  - https://chainforge.ai/docs
  - https://chainforge.ai/play/
    - The web version of ChainForge has a limited feature set.
  - open-source visual programming environment for battle-testing prompts to LLMs.
  - ChainForge is a data flow prompt engineering environment for analyzing and evaluating LLM responses. It enables rapid-fire, quick-and-dirty comparison of prompts, models, and response quality that goes beyond ad-hoc chatting with individual LLMs.
  - Query multiple LLMs at once to test prompt 
  - Compare response quality across prompt permutations, across models, and across model settings to choose the best prompt and model for your use case.
  - Setup evaluation metrics (scoring function) and immediately visualize results across prompts, prompt parameters, models, and model settings.
  - Use AI to streamline this entire process: Create synthetic tables and input examples with built-in genAI features, or supercharge writing evals by prompting a model to give you starter code.
  - ChainForge is built on ReactFlow and Flask.

- https://github.com/Arize-ai/phoenix /8.2kStar/Elastic/202601/python/ts/对比表/lowcode
  - https://arize.com/docs/phoenix#evaluation
  - open-source AI observability platform designed for experimentation, evaluation, and troubleshooting

- https://github.com/vibrantlabsai/ragas /12.2kStar/apache2/202601/python/code-first
  - https://docs.ragas.io/
  - toolkit for evaluating and optimizing Large Language Model (LLM) applications. 
  - Test Data Generation: Automatically create comprehensive test datasets covering a wide range of scenarios.
  - Seamless Integrations: Works flawlessly with popular LLM frameworks like LangChain and major observability tools.

- https://github.com/confident-ai/deepeval /13kStar/apache2/202601/python/code-frist
  - https://deepeval.com/
  - open-source LLM evaluation framework, for evaluating and testing large-language model systems. 
  - It is similar to `Pytest` but specialized for unit testing LLM outputs
  - DeepEval incorporates the latest research to evaluate LLM outputs based on metrics such as G-Eval, task completion, answer relevancy, hallucination, etc., which uses LLM-as-a-judge and other NLP models that run locally on your machine for evaluation.

- https://github.com/truera/trulens /3kStar/MIT/202601/python
  - https://www.trulens.org/
  - TruLens helps you objectively measure the quality and effectiveness of your agent using feedback functions.

- https://github.com/Helicone/helicone /4.9kStar/apache2/202601/ts
  - https://www.helicone.ai/
  - Open source LLM observability platform. One line of code to monitor, evaluate, and experiment. YC W23
  - Playground: Rapidly test and iterate on prompts, sessions and traces in our UI.
  - Prompt Management: Version prompts using production data. Deploy prompts through the AI Gateway without code changes. Your prompts remain under your control, always accessible.

- https://github.com/agenta-ai/agenta /3.7kStar/MIT+EE/202601/python/ts/无对比表
  - http://www.agenta.ai/
  - LLMOps platform: prompt playground, prompt management, LLM evaluation, and LLM observability all in one place.
  - Interactive LLM Playground: Compare prompts side by side against your test cases
  - Multi-Model Support: Experiment with 50+ LLM models or bring-your-own models
  - Version Control: Version prompts and configurations with branching and environments
  - Pre-built and Custom Evaluators: Use LLM-as-judge, one of our 20+ pre-built evaluators, or you custom evaluators
  - LLM Tracing: Debug complex workflows with detailed traces
  - [Changes to Agenta's Open Source and Commercial Features _202503](https://github.com/Agenta-AI/agenta/discussions/2527)
    - We are updating our open-source model starting v0.36 to better support production-ready deployments and to ensure sustainable development of the Agenta platform. 
    - We are introducing the Model Registry feature into the open-source version.
    - All evaluation features (Human Evaluation, Automatic Evaluation, Custom Workflows) are now available exclusively in our commercial offering.

- https://github.com/stellarlinkco/ai-eval /AGPL/202602/go
  - [【开源】 AI-Eval：Prompt 评估系统，用单元测试跑 prompt 评估  _202602](https://linux.do/t/topic/1577572)
  - Go 写的 Prompt 评估系统。把 Prompt 测试当单元测试跑 —— 写 YAML 定义用例，配评估器（模式匹配、LLM Judge、RAG、Agent、安全检测），跑 pass@k 处理 LLM 的不确定性。
  - 带 Web API、Leaderboard、CI 集成，
  - 支持 MMLU/GSM8K/HumanEval 标准 Benchmark。
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
  - [API Key issue _202510](https://github.com/router-for-me/CLIProxyAPI/issues/181)
    - 🍎 mac上通过homebrew安装后配置文件在 `/opt/homebrew/etc/cliproxyapi.conf`
  - [fix: Implement fallback log directory for file logging on read-only system _202512](https://github.com/router-for-me/CLIProxyAPI/pull/772)
    - macOS 下面，打开 logging-to-file: true 之后，homebrew services 启动失败，排查后是日志无法写入导致的。
  - [gemini oauth in droid cli: unknown provider _202511](https://github.com/router-for-me/CLIProxyAPI/issues/258)
    - If you just close the terminal / window or don’t pick a real project (or ALL), no Gemini credential file gets written into ~/.cli-proxy-api, and later requests from Droid will hit unknown provider.
    - brew services restart cliproxyapi
  - [CLIProxyAPI配置 Gemini CLI最后一步失败：Google账号权限设置不够 ](https://github.com/router-for-me/CLIProxyAPI/issues/480)
    - 大陆网友请在config.yaml中设置proxy-url或开启tun模式的代理
  - [目前发现的一些Cli Proxy API问题的解决方法 _202602](https://linux.do/t/topic/1592398)
  - https://github.com/router-for-me/Cli-Proxy-API-Management-Center /MIT/202601/ts
    - a WebUI interface based on CLI-Proxy-API, designed to simplify configuration modifications and runtime status monitoring.
    - Since version 6.0.19, the WebUI ships with the main program; access it via `/management.html` on the API url
  - https://github.com/router-for-me/CLIProxyAPIPlus /MIT/202512/go
    - the Plus version of CLIProxyAPI, adding support for third-party providers on top of the mainline project.
    - Added GitHub Copilot support (OAuth login)
    - Added Kiro (AWS CodeWhisperer) support (OAuth login)
  - https://github.com/dongshuyan/CPA-Dashboard 
    - 控制面板 - 服务管理与账户监控 Web 界面
    - 启动 / 停止 / 重启 CLIProxyAPI 服务
- https://github.com/automazeio/vibeproxy /688Star/MIT/202512/swift
  - Native macOS menu bar app to use your Claude Code & ChatGPT subscriptions with AI coding tools - no API keys needed
  - native macOS menu bar app that lets you use your existing Claude Code, ChatGPT, Gemini, Qwen, and Antigravity subscriptions with powerful AI coding tools like Factory Droids – no separate API keys required.
  - Built on CLIProxyAPIPlus, it handles OAuth authentication, token management, and API routing automatically. One click to authenticate, zero friction to code.
  - 👀 注意 msty studio 内置并自动开启了Vibe CLI Proxy, 会导致通过系统包管理器安装的cliproxyapi出现端口冲突而不可用

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
