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

- https://github.com/cloudflare/agents /MIT/202502/ts
  - https://developers.cloudflare.com/agents/
  - Build and deploy AI Agents on Cloudflare
  - https://x.com/threepointone/status/1895097050439593993
    - an event bus for ai agents
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
  - Observability: tracking LLM calls and other relevant logic in your app such as retrieval, embedding, or agent actions
  - Prompt Management 
  - Evaluations: supports LLM-as-a-judge, user feedback collection
  - Datasets enable test sets and benchmarks for evaluating your LLM applications
  - LLM Playground is a tool for testing and iterating on your prompts and model configurations
  - [All Langfuse Product Features now Free Open-Source : r/LangChain _202506](https://www.reddit.com/r/LangChain/comments/1l36tte/all_langfuse_product_features_now_free_opensource/)
    - 💡 Langfuse is an open-source LangSmith alternative that helps teams collaboratively build, debug, and improve their LLM applications

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

- https://github.com/MotiaDev/motia /5.8kStar/MIT/202508/ts
  - https://motia.dev/
  - Modern Backend Framework that unifies APIs, background jobs, workflows, and AI agents into a single cohesive system with built-in observability and state management.
  - Motia gives you full, code-first control of your agents and automations with the simplicity of a visual interface, letting you focus on what truly matters: your business logic
  - 不依赖langchain/langflow
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
# mcp
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
# protocols-ai
- https://github.com/zed-industries/agent-client-protocol /871Star/apache2/202510/rust/ts
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
# proxy
- https://github.com/lymanzhao/Ollama-serve /202503/python
  - 一个 Ollama转发代理，用于为原生 Ollama 服务添加 API 密钥认证功能。
  - 该项目解决了 Ollama 官方不提供 API 密钥验证的问题，使您可以更安全地部署 Ollama 服务并防止未授权访问
# more
- https://github.com/beuaaa/pywinauto_recorder /MIT/202411/python
  - https://pywinauto-recorder.readthedocs.io/
  - A record-replay tool to automate GUI via pywinauto
  - records user interface actions and saves them in a Python script. The saved Python script can be run to replay the user interface actions previously recorded.
  - "Pywinauto recorder" is a unique inspect/record/replay tool in the open source field because it generates reliable scripts without hard-coded coordinates thanks to Pywinauto.
  - The functions of the generated Python script return Pywinauto wrappers so it can be enhanced with Pywinauto methods.
