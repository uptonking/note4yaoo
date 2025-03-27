---
title: lib-ai-app-examples-utils-fwk
tags: [ai, examples, utils]
created: 2025-02-21T18:20:28.621Z
modified: 2025-02-21T18:20:42.624Z
---

# lib-ai-app-examples-utils-fwk

# guide

# popular
- https://github.com/langgenius/dify /82.5kStar/apache2/202503/python
  - https://dify.ai/
  - Dify is an open-source LLM app development platform
  - combines AI workflow, RAG pipeline, agent capabilities, model management, observability features and more
  - 依赖flask-sqlalchemy、beautifulsoup4、celery、gunicorn、langfuse、langsmith、numpy、pandas、pydantic、starlette、unstructured、python-docx、boto3
  - 前端依赖 @dagrejs/dagre、elkjs、elkjs@lexical/react、@next/mdx、zustand、swr、tanstack-query5、ahooks、echarts-for-react、immer、mermaid、react-markdown、react-window、remark-gfm、sortablejs
  - license 💰
    - Unless explicitly authorized by Dify in writing, you may not use the Dify source code to operate a multi-tenant environment.
    - In the process of using Dify's frontend, you may not remove or modify the LOGO or copyright information in the Dify console or applications. 

- https://github.com/open-webui/open-webui /MIT/202405/svelte/python
  - https://openwebui.com/
  - User-friendly WebUI for LLMs (Formerly Ollama WebUI)
  - extensible, feature-rich, and user-friendly self-hosted WebUI designed to operate entirely offline. 
  - It supports various LLM runners, including Ollama and OpenAI-compatible APIs

- https://github.com/cloudflare/agents /MIT/202502/ts
  - https://developers.cloudflare.com/agents/
  - Build and deploy AI Agents on Cloudflare
  - https://x.com/threepointone/status/1895097050439593993
    - an event bus for ai agents
# agent-framework
- https://github.com/MotiaDev/motia /MIT/202503/ts
  - https://motia.dev/
  - Motia lets developers create, test, and deploy production-ready AI agents in minutes, in a framework that will feel familar to software engineering teams. 
  - Motia gives you full, code-first control of your agents and automations with the simplicity of a visual interface, letting you focus on what truly matters: your business logic
  - Motia is built for developers who want to build agentic and intelligent, event-driven systems rapidly and reliably.
  - Use any LLM, vector store, or reasoning pattern without restrictions.
  - Zero Infrastructure Headaches - No Kubernetes expertise required. Deploy agents with a single command
  - Code-First Development - Write agent logic in familiar languages, not proprietary DSLs.
  - Composable Steps with Runtime Validation - Build agents from modular, reusable components with automatic input/output validation.
  - Built-in Observability - Debug agent behavior with visual execution graphs and real-time logging.
  - Instant APIs & Webhooks - Expose agent functionality via HTTP endpoints without extra code.

- https://github.com/mastra-ai/mastra /Elastic/202502/ts
  - https://mastra.ai/
  - Mastra is an opinionated Typescript framework that helps you build AI applications
  - It gives you the set of primitives you need: workflows, agents, RAG, integrations and evals.
  - You can run Mastra on your local machine, or deploy to a serverless cloud.
  - Mastra uses the Vercel AI SDK for model routing, providing a unified interface to interact with any LLM provider including OpenAI, Anthropic, and Google Gemini. 
  - Agents are systems where the language model chooses a sequence of actions. 
  - Tools are typed functions that can be executed by agents or workflows, with built-in integration access and parameter validation. 
  - Workflows are durable graph-based state machines. They have loops, branching, wait for human input, embed other workflows
  - RAG lets you construct a knowledge base for agents
  - Evals are automated tests that evaluate LLM outputs using model-graded, rule-based, and statistical methods.
  - https://x.com/dingyi/status/1893329741060489438
    - 以前非常喜欢且深度使用的 Gatsby，他们团队原班人马做的新产品，The TypeScript Agent Framework
# ai-sdk
- [AI SDK Cookbook](https://sdk.vercel.ai/cookbook)
  - An open-source collection of recipes and guides for building with the AI SDK.
# browser-use

# computer-use
- https://github.com/Aident-AI/open-cuak /apache2/202503/ts
  - https://aident.ai/
  - Open CUA Kit (Computer Use Agent), is THE platform for teaching, hiring and managing automation agents at scale — starting with browsers.
  - Open-CUAK is designed to run and manage thousands of automation agents, ensuring each one is reliable.
  - Run Operator-like automation workflows locally, ensuring full privacy
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
# perf/large
- https://github.com/MoonshotAI/MoBA /MIT/202502/python
  - Mixture of Block Attention for Long-Context LLMs
  - https://x.com/tuturetom/status/1892753818028216717
    - 可以实现近乎无限的上下文窗口，将一整本书或一整个代码库扔进去提问
# agi-text

# agi-image
- https://github.com/joanrod/star-vector /apache2/202503/python
  - https://starvector.github.io/
  - StarVector is a foundation model for SVG generation that transforms vectorization into a code generation task. 
  - Using a vision-language modeling architecture, StarVector processes both visual and textual inputs to produce high-quality SVG code with remarkable precision.
  - It can be used to perform image2SVG and text2SVG generation. We pose image generation as a code generation task, using the power of multimodal VLMs
  - March 2025: StarVector Accepted at CVPR 2025
  - SVGBench and SVG-Stack datasets are now available on HuggingFace Datasets
    - https://huggingface.co/datasets/starvector/svg-bench
    - https://huggingface.co/datasets/starvector/svg-stack
# proxy
- https://github.com/lymanzhao/Ollama-serve /202503/python
  - 一个 Ollama转发代理，用于为原生 Ollama 服务添加 API 密钥认证功能。
  - 该项目解决了 Ollama 官方不提供 API 密钥验证的问题，使您可以更安全地部署 Ollama 服务并防止未授权访问
# ai-devops
- https://github.com/exo-explore/exo /GPL
  - exo: Run your own AI cluster at home with everyday devices
  - exo supports different models including LLaMA (MLX and tinygrad), Mistral, LlaVA, Qwen, and Deepseek.
  - 该项目支持将现有设备统一到一个功能强大的GPU中，支持 iPhone，iPad，Android，Mac，Nvidia，树莓派等等几乎所有设备。
# more
