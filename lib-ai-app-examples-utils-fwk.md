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
  - https://github.com/MotiaDev/motia-examples /数据流动画
    - Intelligent Q&A from PDFs with Docling's smart chunking, Weaviate's sca lable vector DB, and OpenAI embeddings & text generation. 
    - Built with TypeScript & Python.

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
  - This project heavily relies on Playwright 
  - Choose when to write code vs. natural language: use AI when you want to navigate unfamiliar pages, and use code (Playwright) when you know exactly what you want to do.

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
# computer-use
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

- https://github.com/mark3labs/mcp-filesystem-server /go
  - Go server implementing Model Context Protocol (MCP) for filesystem operations.
  - 通过这个MCP就可以操作本地文件系统了，由于这个是go编写的，go能交叉编译的架构特别多，所以理论上大部分系统都能运行这个MCP Server。
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
- https://github.com/beuaaa/pywinauto_recorder /MIT/202411/python
  - https://pywinauto-recorder.readthedocs.io/
  - A record-replay tool to automate GUI via pywinauto
  - records user interface actions and saves them in a Python script. The saved Python script can be run to replay the user interface actions previously recorded.
  - "Pywinauto recorder" is a unique inspect/record/replay tool in the open source field because it generates reliable scripts without hard-coded coordinates thanks to Pywinauto.
  - The functions of the generated Python script return Pywinauto wrappers so it can be enhanced with Pywinauto methods.
