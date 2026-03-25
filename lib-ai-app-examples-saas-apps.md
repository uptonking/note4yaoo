---
title: lib-ai-app-examples-saas-apps
tags: [ai, examples, large-language-model, saas]
created: 2025-02-21T17:16:46.331Z
modified: 2025-02-21T17:17:42.225Z
---

# lib-ai-app-examples-saas-apps

# guide

- tips
  - bpmn + ai
# popular
- https://github.com/OpenHealthForAll/open-health /AGPL/202502/ts
  - https://www.open-health.me/
  - AI Health Assistant | Powered by Your Data
  - Smart Parsing: Automatically parses your health data and generates structured data files.
  - Contextual Conversations: Use the structured data as context for personalized interactions with GPT-powered AI.

## starter/boilerplate

- https://github.com/ArjunDivecha/mlx-finetune-gui /202509/python/ts/inactive
  - A modern desktop application for fine-tuning Large Language Models using Apple's MLX framework on macOS. 
  - Built with Electron, React, TypeScript, and FastAPI.
  - MLX environment already set up at: `/Users/macbook2024/Library/CloudStorage/Dropbox/AAA Backup/A Working/Arjun LLM Writing/local_qwen/.venv`.
  - Training process management with MLX integration
  - Datasets: File picker for JSONL training data
# open-canvas
- https://github.com/refly-ai/refly /apache2/202503/ts
  - https://refly.ai/
  - an open-source AI-native creation engine powered by 13+ leading AI models. 
  - Its intuitive free-form canvas interface integrates multi-threaded conversations, multimodal inputs (text/images/files), RAG 
# workflow-ai
- https://github.com/FlowiseAI/Flowise /42.5kStar/apache2+EE/202510/ts
  - https://flowiseai.com/
  - https://docs.flowiseai.com/
  - Drag & drop UI to build your customized LLM flow
  - Open source low-code tool for developers to build customized LLM orchestration flow & AI agents
  - 大量使用 LangchainJS, 支持langchain的各种组件

- https://github.com/simstudioai/sim /17.1kStar/apache2/202510/ts
  - https://www.sim.ai/
  - Open-source platform to build and deploy AI agent workflows.

- https://github.com/browser-use/workflow-use /AGPL/python
  - Create and run workflows (RPA 2.0)
  - https://x.com/gregpr07/status/1923595378286268812
    - we started Workflow Use (Playwright on steroids):
    - Show browser once, run forever
    - 10x faster, ~90% cheaper than pure LLM agents
    - Self-healing via LLM fallback 

- https://github.com/gradio-app/daggr /MIT/202601/python
  - a Python library for building AI workflows that connect Gradio apps, ML models (through Hugging Face Inference Providers), and custom Python functions
  - [Introducing Daggr: Chain apps programmatically, inspect visually _202601](https://huggingface.co/blog/daggr)

- https://github.com/langflow-ai/langflow /109kStar/MIT/202508/python/ts
  - http://www.langflow.org/
  - a powerful tool for building and deploying AI-powered agents and workflows.
  - It provides developers with both a visual authoring experience and a built-in API server that turns every agent into an API endpoint that can be integrated into applications built on any framework 
  - 大量使用langchain

- https://github.com/1Panel-dev/MaxKB /15.5kStar/GPL/202504/python/ts/vue
  - https://maxkb.pro/
  - 基于大模型和 RAG 的开源知识库问答系统
  - it is a ready-to-use RAG chatbot that features robust workflow and MCP tool-use capabilities. 
  - 依赖django、langchain、pgvector、Vue
  - Flexible Orchestration: Equipped with a powerful workflow engine, function library and MCP tool-use, enabling the orchestration of AI processes to meet the needs of complex business scenarios.

- https://github.com/PySpur-Dev/PySpur /5.4kStar/apache2/202507/python/ts
  - https://www.pyspur.dev/
  - A visual playground for agentic workflows: use it to build agents, execute them step-by-step and inspect past runs.
  - Build the agent in Python code or via UI
  - Human in the Loop: Persistent workflows that wait for human approval.
  - Structured Outputs: UI editor for JSON Schemas.
  - RAG: Parse, Chunk, Embed, and Upsert Data into a Vector DB.
  - Multimodal: Support for Video, Images, Audio, Texts, Code.
  - Python-Based: Add new nodes by creating a single Python file.
  - By default, this will start PySpur app at http://localhost:6080 using a sqlite database.
  - Using Local Models with Ollama: PySpur only works with models that support structured-output and json mode. Most newer models should be good
  - [ComfyUI for LLMs : r/comfyui _202412](https://www.reddit.com/r/comfyui/comments/1hgfy3g/comfyui_for_llms/)

- https://github.com/nocode-js/sequential-workflow-designer /1.2kStar/MIT/202502/ts/NoDeps
  - https://nocode-js.com/
  - Customizable no-code component for building flow-based programming applications or workflow automation
  - written in pure TypeScript and uses `SVG` for rendering
  - This designer is not associated with any workflow engine. 
  - the definition is stored as JSON
  - https://github.com/nocode-js/sequential-workflow-editor /MIT/vanillajs
    - Mainly designed to work with the Sequential Workflow Designer
  - https://github.com/nocode-js/sequential-workflow-machine /MIT/202408/ts
    - Powerful sequential workflow machine for front-end and back-end applications.
    -  It provides a simple API for creating its own step execution handlers (activities). It supports multiple types of activities. 
    - Internally it uses the `xstate` library.
    - This machine uses the same data model as the Sequential Workflow Designer.
  - [Pricing of Sequential Workflow Designer Pro](https://nocode-js.com/sequential-workflow-designer-pro-pricing)
    - Pro Step Components
    - Custom Theme
# ai-figure/数字人/avatar
- https://github.com/Alibaba-Quark/LiveAvatar /apache2/202512/python
  - https://liveavatar.github.io/
  - 阿里夸克开源的实时虚拟人模型能实时生成虚拟人视频，能生成无限长度的视频且画质不降低。
  - 项目介绍写的推理需要 4090/A100，训练用了8个A100
    - Sorry不是的，当前得用5*H800才能推理。但我们还在持续推进更友好的消费级方案，希望可以尽快降低使用门槛。

- https://github.com/taoofagi/easegen-front
  - 开源的数字人课程制作项目：easegen，它提供从课程制作、视频管理、智能课件生成到智能出题全套方案
  - 支持ppt课件批量自动生成、数字人克隆、声音克隆、数字人课程设计、数字人视频渲染等
  - https://x.com/aigclink/status/1847102226088841648
# ai-designer/lovable
- https://github.com/Amery2010/open-builder /GPL/202603/ts
  - https://builder.u14.app/
  - Open Builder is an open-source AI-powered app generator. Build web applications through natural language conversations.
  - [【开源】Open Builder v1.2.0 发布，用了 $400 多 opus 4.6 额度完全重构了整个项目，完美复刻 AI Studio Build 体验的自部署 AI 应用构建平台  _202603](https://linux.do/t/topic/1699622)
    - 集成tauri，增加了桌面客户端
    - 目前是纯前端实现，用不了 skill 和 mcp，除非完全专注于开发服务端或客户端版本。但项目一开始是向轻量级方向开发的，所以对于后续的开发规划，我还得好好想一想…
    - 跟 manus 这类通用型的 agent 还是不太一样的，跟 bolt 会比较接近，但 bolt 部署存在难度，且项目资源消耗比较大，本质上不是给个人用户用的。这个项目更像是一个给普通人用的 AI 网站生成工具。
  - [【开源】Open Builder 一款轻量级 AI 生成应用框架（文本转APP），通过自然语言描述快速生成网页应用 _202602](https://linux.do/t/topic/1663809)
    - 这几天在研究 Google AI Studio Build 的实现原理，了解到目前市面上的 Text2Code 一般是通过 AI 后端+SandBox（项目隔离）实现项目生成和及时编译。普通用户想要架设一套完整的 AI 项目生成系统会比较麻烦。
    - 在调研了一些方案后，我最终采用了 AI 代码生成+Sandpack 这套架构方案，Sandpack 底层由 CodeSandbox 提供技术支持，可以很轻松的实现项目云端编译，实时预览的效果，而且没有任何费用。
    - AI 代码生成其实有很多中实现方案，比如像 manus 那样在项目中通过任务的形式一步步执行，也可以通过 tool call 让 AI 自己选择工具进行操作。我在项目中采用了第二种方案。项目的核心代码位于 src/lib/generator.ts，本质上是利用 tool call 让 AI 自主选择工具，对代码进行项目初始化、管理项目依赖、列出所有项目文件、批量读取文件内容、创建或覆写文件、精确搜索替换文件内容、删除文件、全局搜索文件内容，以及可选的联网搜索与网页内容读取。这些操作可以让 AI 精准的操作虚拟文件系统中的项目文件，实现云端项目生成。
    - 本项目无后端架构，是一个静态页面，因此您可以将此项目部署到任何服务器上。所有的项目参数都保存在本地，因此您也无需担心数据泄漏的问题。由于是无后端的架构模式，您可能无法与朋友共享此项目。

- https://github.com/ZSeven-W/openpencil /477Star/MIT/202603/ts
  - https://op.zseven.tech/
  - https://openpencil.dev/
  - first open-source AI-native vector design tool and the first to feature concurrent Agent Teams. Design-as-Code. 
  - Turn prompts into UI directly on the live canvas.
  - OpenPencil is built around AI from the ground up — not as a plugin, but as a core workflow.
  - Text-to-design — describe a page, get it generated on canvas in real-time with streaming animation
  - File format: `.op` — JSON-based, human-readable, Git-friendly
  - Orchestrator — decomposes complex pages into spatial sub-tasks for parallel generation
  - Design modification — select elements, then describe changes in natural language
  - Vision input — attach screenshots or mockups for reference-based design
  - 依赖 Fabric.js v7, Zustand, React 19, TanStack Start, Nitro, Tailwind CSS v4, shadcn/ui
  - Native macOS, Windows, and Linux via Electron
  - Code Generation
    - React + Tailwind CSS
    - HTML + CSS
  - [【开源自荐】OpenPencil：首个开源AI原生矢量设计工具，支持Agent Team，可导入Figma，一键导出React/Vue代码 - LINUX DO _202603](https://linux.do/t/topic/1773258)
    - 自然语言生成设计稿，支持 Claude Code/Codex/OpenCode 等主流CLI
    - 支持 MCP 实时操作画布，可局部修改元素
    - 支持 Agent Team，多Agent并发完成设计
    - 兼容 .pen，支持 .fig 导入，还原度相当高
    - 一键导出React/Vue等8种原生代码，还原度接近100%

- https://github.com/TesslateAI/Studio /apache2/202510/python/ts
  - Open Source Locally Hosted Lovable with Full Stack Support
  - Includes support for llama.cpp, LM Studio, Ollama, Openrouter, and any provider you choose.
  - Run anywhere: Your machine, your cloud, your datacenter
  - Container isolation: Each project runs in its own sandboxed Docker container
  - Subdomain routing: Clean URLs (`project.studio.localhost`) for easy project access
  - Tool Registry: File operations (read/write/patch), persistent shell sessions, web fetch, planning tools
  - Multi-agent orchestration: Built on TframeX framework - agents collaborate across frontend, backend, database concerns
  - What Makes Tesslate Studio Different?
    - Tesslate Studio isn't just another code generation tool - it's a complete development platform architected from the ground up for self-hosting and data sovereignty
  - https://github.com/TesslateAI/TFrameX /MIT/python
    - TFrameX empowers you to build sophisticated, multi-agent LLM applications with unparalleled ease and flexibility.
  - [Self hosted Multi User Loveable with Full Stack Support : r/selfhosted _202510](https://www.reddit.com/r/selfhosted/comments/1ok5gde/self_hosted_multi_user_loveable_with_full_stack/)
    - I built Tesslate Studio. Its open sourced, Apache 2.0. Bring your own models
    - Bring your own agents (you can define the system prompt or tools or add in a new agent with the factory), and bring your own github urls to start with.
    - Would this be also a tool for python code or other types? Specific to web applications?
      - You can put whatever container + runtime + initial starting repository. The default development container supports python so that works out, just pull in your github repo and you're good to go
  - [Locally hosted Loveable with full stack support and llama.cpp, and more : r/LocalLLaMA](https://www.reddit.com/r/LocalLLaMA/comments/1ok5rn2/locally_hosted_loveable_with_full_stack_support/)
    - I'm surprised that tesslate ai is a one-man project.
    - Its not one man! We have a few people on discord training models now and Ernest and I built Studio. We've had other contributors help us for our other projects like: Agent Builder, TframeX, Designer

- https://github.com/firecrawl/open-lovable /8.3kStar/MIT/202508/ts
  - https://github.com/mendableai/open-lovable
  - Clone and recreate any website as a modern React app in seconds
  - Chat with AI to build React apps instantly. Made by the Firecrawl team.
  - 基于e2b sandbox实现
  - 🍴 forks
  - https://github.com/fstandhartinger/chutes-webcoder
    - A Chutes-flavoured fork of firecrawl/open-lovable that keeps pace with the upstream features (Vercel sandboxing, GitHub integration, new builder UI) while defaulting to the Chutes LLM platform.

- https://github.com/buildermethods/design-os /MIT/202512/ts
  - https://buildermethods.com/design-os
  - Design OS is a product planning and design tool that helps you define your product vision
  - The core issue: we're asking coding agents to figure out what to build and build it simultaneously. Design decisions get made on the fly, buried in code, impossible to adjust without starting over. There's no spec. No shared understanding. No source of truth for what "done" looks like.
  - https://x.com/CasJam/status/2001675739930964199
    - the missing design process between your idea and codebase.
    - Step 1: Set your product vision
    - Step 2: Design your screens
    - Step 3: Export production-ready components

- https://github.com/dyad-sh/dyad /14.2kStar/apache2/202508/ts
  - https://dyad.sh/
  - Free, local, open-source AI app builder 
  - v0 / lovable / Bolt alternative 
  - Easy to run on Mac or Windows.
  - https://github.com/dyad-sh/sandpack-bundler /apache2
    - The new bundler/runtime powering client-side sandpack sandboxes

- https://github.com/11cafe/jaaz /2.3kStar/NonComm/202508/python/ts
  - https://jaaz.app/
  - AI design agent, local alternative for Lovart. Canva + Cursor. 
  - Infinite Canvas & Visual Storyboarding Plan scenes with an unlimited canvas
  - 社区许可证： 面向个人及组织有限使用的免费许可证。
  - 商业许可证： 任何内部团队部署，或对代码的任何二次开发或修改，都必须获取商业许可证。
  - [Jaaz's "completely" self-hosted? _202508](https://github.com/11cafe/jaaz/issues/252)
    - if you use ollama and add comfyui workflows for image generations, it will be fully self hosted. Or add your own replicate api key, you can also self host
  - [Self-hosted image generation and LLM API _202506](https://github.com/11cafe/jaaz/issues/21)
    - you want to local host your stable diffusion models or Flus models? Yea we will support that through local comfyui image generations
  - [WIP: support ComfyUI  _202506](https://github.com/11cafe/jaaz/pull/7)
    - add ComfyUI installation & install dialog, add adm-zip
    - Get the latest ComfyUI release information from GitHub
    - refactor: Standalone comfyUI installation logic

- https://github.com/chatfire-AI/huobao-canvas /202601/js/vue
  - 一个基于 Vue Flow 的可视化 AI 创作画布，支持文生图、视频生成等 AI 工作流的节点式编排。 
  - 撤销/重做 - 完整的操作历史记录
  - 类似comfyui的文生图
  - [【开源自荐】花两天时间做了一个无限画布，开源了一个 乞丐版 lovart _202601](https://linux.do/t/topic/1438600)

- https://github.com/onlook-dev/onlook /apache2/202502/ts
  - https://onlook.com/
  - The open source Cursor for Designers. 
  - Design directly in your live React app and publish your changes to code.

- https://github.com/Flame-Code-VLM/Flame-Code-VLM /apache2/202502/python
  - Flame: 一个基于数据合成提升多模态大模型前端开发能力的解决方案
  - 为提升多模态模型在生成依赖特定前端框架代码方面的能力，我们提出了一套解决方案，包含数据合成管线、模型训练及评估套件。基于该方案，我们构建了Flame模型，可根据图文信息生成特定框架的前端代码。
  - [数据合成] 最关键的挑战在于构建高质量的图-文（代码）数据。我们提出的智能体工作流驱动的数据合成管线能够提取、渲染并注释自包含的前端代码片段。该管线确保了生成的大规模、多样化且高保真的数据集，支持单图像和多图像输入，并提供详细的图像描述（可用于视觉思维推理开发）。
    - 我们的数据合成方法包括三种策略：基于进化思想的合成、基于瀑布流模型的合成以及基于增量式开发思想的合成，过程中通过DeepSeek API接入DeepSeek V2和V3模型进行数据构建，生成的图文（代码）数据将全部开源。
  - [模型训练] 我们通过两层MLP将Siglip图像编码器与Deepseek的代码模型连接，构建Flame模型，并采用三阶段训练策略。第一阶段预热两层连接器（使用公开的图文数据）；第二阶段训练图像编码器及连接器（使用我们合成的数据）；第三阶段进行SFT，训练所有参数（同样使用合成数据）。我们发现，在针对特定场景的数据下，这种训练方案表现出更好的效果。
  - [评估套件] 为确保生成代码符合实际开发标准，我们构建了一个全面的评估套件，评估生成代码的三个关键因素：语法精确性、功能正确性和视觉一致性。该评估方法将为未来的多模态模型代码生成能力提供可靠的测评标准。
  - 目前，该框架针对基于React的开发进行了设计和优化。该方法和管道具有高度可扩展性，只需进行少量修改即可适应其他前端框架，如Vue和Angular。
  - 注：Flame只关注React代码生成，非通用VLM。

- https://github.com/opactorai/Claudable /3.4kStar/MIT/202512/ts/electron/inactive
  - an open-source web builder that leverages local CLI agents, such as Claude Code, Codex, Gemini CLI, Qwen Code, and Cursor Agent, to build and deploy products effortlessly.
  - Instant Preview: See your changes immediately with hot-reload as AI builds your app
  - Zero Setup, Instant Launch: No complex sandboxes, no API key, no database headaches - just start building immediately
  - Deploy to Vercel: Push your app live with a single click
  - Supabase Database: Connect production PostgreSQL with authentication ready to use
  - Desktop App: Available as Electron desktop application for Mac, Windows, and Linux

## ai-webapp

- https://huggingface.co/spaces/enzostvs/deepsite/tree/main
  - DeepSite is a coding platform powered by DeepSeek AI, designed to make coding smarter and more efficient. 
  - Tailored for developers, data scientists, and AI engineers, it integrates generative AI into your coding projects to enhance creativity and productivity.
  - Multi Pages: Create complex websites with multiple interconnected pages
  - [How to run 🐳 DeepSite locally](https://huggingface.co/spaces/enzostvs/deepsite/discussions/74)
  - [Request for License Information for the DeepSite Project](https://huggingface.co/spaces/enzostvs/deepsite/discussions/119)
    - DeepSite is using the MIT License
  - https://github.com/marlenezw/deepsite-python
    - A Python version of DeepSite

- https://github.com/schuerstedt/DeepSite /202509/ts/inactive
  - https://github.com/schuerstedt/DeepSite/blob/main/lib/prompts.ts
  - this is a clone from https://huggingface.co/spaces/enzostvs/deepsite with some enhancements
  - Multiple AI Providers: DeepSeek, Fireworks AI, Nebius, SambaNova, Together AI, Groq, Hyperbolic
  - Two Generation Modes: Enhanced (with strategic planning) and Classic (direct generation)
  - Real-time Streaming: Watch AI think and generate code with live updates
  - Smart Follow-up Editing: Precise diff-based modifications with SEARCH/REPLACE blocks
- https://github.com/MartinsMessias/deepsite-locally /202508/ts/inactive
  - https://github.com/MartinsMessias/deepsite-locally/blob/main/lib/prompts.ts
  - AI website builder with local hosting support. Run DeepSite on your own server or offline.
  - a fork of the original DeepSite by enzostvs on Hugging Face Spaces.

- https://github.com/admineral/Reactor /202405/ts/inactive
  - https://reactor-dev.vercel.app/
  - Chat with React Code-Editor and Live-preview using Sandpack by Codesandbox
  - An experimental preview of AI SDK 3.0 with Generative UI support

- https://github.com/asj9469/Reactonaut /13Star/NALic/202308/js/inactive
  - an online React code editor with an AI assistant. 
  - Live code editing with Ace Editor
  - React-Live for real-time rendering of React components
  - OpenAI's ChatGPT API integration for code suggestions
  - Reactonaut is the general/public version of his original project Reactor with a new UI and enhanced features. It was developed during our collaboration in an AI Startup Hackathon.

- https://github.com/Nutlope/llamacoder /6.5kStar/MIT/202508/ts
  - https://www.llamacoder.io/
  - open source Claude Artifacts – generate small apps with one prompt. 
  - Powered by Llama 3 on Together.ai.
  - Sandpack for the code sandbox
  - Next.js app router with Tailwind
  - 🍴 forks
  - https://github.com/Hassanrkbiz/llamacoder-any-llm /202412/inactive
    - Multiple LLMs & Providers Added
    - Local LLMs (Ollama & LM Studio) Added
    - Image Support

- https://github.com/etrobot/nextArtifacts /MIT/202409/ts/inactive
  - https://github.com/etrobot/nextArtifacts
  - A Next.js version of Claude Aritfacts , inspired by llamacoder
  - generate small applications using any Large Language Model (LLM) API compatible with the OpenAI format. 
  - This project is inspired by and modified from llamacoder, which uses Llama 3 405B & Together.ai.
- https://github.com/xKevIsDev/GenUAI /202408/ts/inactive
  - AI to UI generation app that uses Shadcn, Aceternity, MagicUI, SyntaxUI built in components to generate websites.
  - forked and adapted from llamacoders

- https://github.com/iotserver24/pollin-coder /MIT/202508/ts
  - https://pollin-coder.megavault.in/
  - open-source AI code generator that lets you create small apps with a single prompt
  - Powered by advanced AI models and the Pollinations.ai platform
  - Generate full-stack apps or code snippets from a single prompt
  - Uses state-of-the-art models for code and text generation
  - Live code sandbox powered by Sandpack
  - Built with Next.js, Tailwind CSS, and modern web tech
  - Pollinations AI for LLM inference

- https://github.com/TesslateAI/Builder-Lite /202504/ts/inactive
  - A web application that allows you to generate React components using an AI chat interface and view/edit them live in a Sandpack sandbox environment.
  - Describe the component you need, and the AI will attempt to generate the code, which is then rendered instantly for preview.
  - Live Sandbox Environment: Uses `@codesandbox/sandpack-react` to provide an instant preview
  - Integrated Code Editor: View and modify the generated Component.tsx code directly in the 'Editor' tab.
  - Dependencies Included: The sandbox automatically includes react, react-dom, framer-motion, and @heroicons/react for richer component possibilities.
  - Optional Proxy: Built-in logic to route API requests through a local proxy (/llm-proxy) if the target API is not on localhost (requires separate proxy setup).

- https://github.com/cameronking4/nextjs-ai-page-generator /apache2/202403/ts/inactive
  - https://nextjs-page-generator.vercel.app/
  - Design, generate, iterate and live preview Nextjs pages with GPT
  - Quick hack to generate & serve Next apps quickly in the browser using Next, Prisma, OpenAI & Sandpack

- https://github.com/ragultv/WebAgent /202511/python/js
  - AI-driven full-stack application that generates responsive websites from simple text prompts or uploaded design mockups. 
  - Backend: FastAPI, Python, SQLAlchemy, Pillow
  - Frontend: React, Vite, Tailwind CSS
  - Database: SQLite (dev), PostgreSQL (prod-ready)
  - Text-to-Website: Generate complete websites from simple natural language prompts.
  - Image-to-Website: Upload UI mockups to generate frontend code automatically.
  - Live Code Preview: Edit and preview the website in real time using an in-browser code editor.

## ai-gen-ui

- https://github.com/itzcrazykns/epoch /MIT/202511/ts
  - Epoch transforms traditional text-based AI conversations into interactive, component-driven experiences. 
  - Every response is rendered as a living interface with clickable elements, dynamic forms, live data visualizations, and explorable UI
  - Epoch eliminates llm text constraint through a structured component architecture. The LLM generates type-safe JSON schemas representing UI component trees, which are recursively rendered into fully interactive React interfaces.
  - 此方案和主流框架兼容性不好，memory/rag的pipeline都要定制处理
    - 但用来实现固定布局layout的card/bg等局部组件很方便
  - 依赖 aisdk, shadcn/ui + Radix UI, recharts
  - This architecture transforms LLMs from text generators into interface compilers, where every response is a composable tree of interactive components rather than static markup.
  - It's bidirectional. You can click a button or submit a form -> that interaction gets serialized back into conversation history -> LLM generates new UI in response.
  - streaming: Server-Sent Events stream partial object updates as the LLM generates component trees, with progressive rendering on the client
  - UIRenderer recursively traverses component trees, maintaining form state and action handlers through the entire tree depth
  - Local LLM Support: Run completely offline with Ollama integration
  - [Epoch: LLMs that generate interactive UI instead of text walls : r/LocalLLaMA _202511](https://www.reddit.com/r/LocalLLaMA/comments/1oqc01w/epoch_llms_that_generate_interactive_ui_instead/)
  - Structured output schema doesn't take context, but I also included it in the system prompt for better performance with smaller Ollama models (system prompt is a bit bigger now, finding a workaround later)
  - Interesting, but the LLM can already spit it HTML if you instruct it. what is the failure rate on these? I presume you append all info in the system prompt to assure the LLM doesn't write poorly formatted interface, but it could easily output straight up wrong commands? Would it just error out? 
    - LLMs can spit out HTML but you cannot be sure of the consistency, styling, layout and everything but in my approach I used grammar (to force the model in generating in the format I want) which significantly reduces the error rate and can perform quite well without taking up much context (I can remove the entire examples from the system prompt and it'd still work on larger models since they have better attention distribution).
    - The error rate is very low, in my testing models less than 4B-6B params gave a few errors (that too bad UI not a failure), larger models and cloud models never really generated a bad UI. 
  - HTML itself is a structured declarative syntax. If you think about what the training corpus for a particular model looks like, it has seen WAY more HTML than a custom structured grammar. Don't overengineer for the sake of it. See if you can accomplish the same thing with simpler methods.
  - Can this support standard OpenAI Compatible API?
    - If your inference provider fully supports the OpenAI format and `grammar enforced decoding` then it can be used.
  - i tried more or less the same, but in some cases output generated would have valid schema, but maybe contain null values, which kind of defeats the whole purpose
  - Where does it take images?
    - The images are fetched via the serp API. I plan to add SearxNG support.
  - Arent ag-ui frameworks like copilotkit exactly for this?
    - Copilotkit renders predefined components in predefined style via function calling. I gave it the ability to generate how it wants the user to see its responses and it is done via grammar enforced decoding (structured outputs). 
    - In copilotkit, you might see the same structure again but with my approach you cannot say

- https://github.com/reidbarber/gen-ui /202312/ts/inactive
  - Use text or image prompts to generate UI components and apps built with React. 
  - Powered by OpenAI's Assistants API and CodeSandbox's Sandpack.

## ai-gen-mtv

- https://github.com/waoowaooAI/waoowaoo /MIT/202602/ts
  - 首家工业级全流程可控协作式专业AIagent影视生产平台，从短片到漫剧到真人级影视剧一站搞定，采用好莱坞专业制作团队思路，让你拥有虚拟制片场
  - [免费开源！已经盈利的AI影视/短剧agent制作系统 waoowaoo _202602](https://linux.do/t/topic/1666777)

## ai-card-ui

- https://github.com/Rpeng666/Ant-Card /apache2/202510/ts
  - 现代化的在线卡片编辑器 - 支持多种精美模板，实时预览，PDF导出，AI 智能生成
  - 15+ 精美模板 - 从简约到创意，满足各种场景需求
  - 实时编辑 - 所见即所得的卡片编辑体验
  - AI 集成 - 智能内容生成和优化
  - 多格式导出 - PNG、JPEG、PDF 等多种格式
  - 支持 Model Context Protocol，可在 Claude Desktop 等工具中使用
  - 本地存储 - 支持保存和加载卡片项目
# ai-apps-amazing
- https://github.com/originalankur/maptoposter /MIT/202601/python
  - Generate beautiful, minimalist map posters for any city in the world.
  - MapToPoster lets you create and export visually striking map posters with code.
  - https://x.com/ImSh4yy/status/2013023687943860324
    - I forked this repo and had Opus 4.5 optimize the code and Gemini 3 to create more themes.
    - looks familiar to https://makemap.co/

- https://github.com/THU-MAIC/OpenMAIC /10.7kStar/AGPL/202603/ts
  - OpenMAIC (Open Multi-Agent Interactive Classroom) is an open-source AI platform that turns any topic or document into a rich, interactive classroom experience.
  - [THU-MAIC/OpenMAIC 开源多智能体互动教室 - LINUX DO _202603](https://linux.do/t/topic/1765092)
# ai-apps
- https://github.com/iOfficeAI/AionUi /18.4kStar/apache2/202603/ts
  - https://www.aionui.com/
  - https://github.com/iOfficeAI/AionUi/wiki
  - open-source GUI app for Gemini CLI — Better Chat UI, multi-agent support, multi-LLMs & apikey polling, Workspace Management, AI image editing & more
  - While the official Gemini CLI is powerful, its command-line interface has limitations for daily use. 
  - 🐛 
    - 不支持rag
  - Seamlessly integrate multiple terminal AI agents - Gemini CLI, Claude Code, Qwen Code, Codex and more
    - [ACP Setup · iOfficeAI/AionUi Wiki](https://github.com/iOfficeAI/AionUi/wiki/ACP-Setup)
    - Gemini CLI Mode: Built into AionUi, users get it by default
    - Multi-Agent Mode: Requires users to download and install
  - Handle Multiple Tasks at Once: Multiple conversations, no task confusion, independent memory, double efficiency
  - 📱 WebUI Mode: Access AionUi from any device on your network
  - Batch renaming, auto organization, smart classification, file merging
  - image generation, editing, and recognition powered by Gemini 2.5 Flash Image Preview
  - AI helps you create, organize, analyze, and beautify Excel files
  - MCP Tool Management

- https://github.com/multica-ai/multica /apache2/202601/ts
  - A native desktop client that brings coding agent capabilities to everyone through a visual interface.
  - ⚖️ Support for multiple AI agents through the Agent Client Protocol (ACP)
  - 支持 cc, opencode, codex
  - Local-first: your data never leaves your machine
  - Session management with history and resume capabilities
  - Built-in CLI for power users and testing
  - https://x.com/jiayuan_jy/status/2012040329407713404
    - 分享我们最近实现的一个开源版本 Claude Cowork
    - 目标是成为 coding agent 和终端用户的中间层，有点类似 Obsidian 的模式，每个人都可以根据自己的工作流使用插件的方式来定制化。

- https://github.com/accomplish-ai/openwork /758Star/MIT/202601/ts
  - https://www.accomplish.ai/openwork/
  - open source Al coworker that lives on your desktop
  - https://x.com/_orcaman/status/2011492458023305394 _202601
    - Today we are launching @openwork_ai , an open-source (MIT-licensed) computer-use agent that’s fast, cheap, and more secure.
    - the result of a short two-day hackathon our team decided to hack, which brings together some of our favorite open source AI modules into one powerful agent
    - does it use @opencode in some way?
      - It certainly does! opencode is the agent harness here, sort of like Claude Code CLI is at Anthropic's Cowork app
    - any plan on sandbox or isolation?
      - Yes, coming up in the next couple of days.
    - Is it computer-use or browser-use?!
      - Both. It has file system access and can manipulate your computer. For browsing tasks it has a browser tool. Both are operated by the same agent

- https://github.com/different-ai/openwork /1.1kStar/MIT/202601/rust/ts/tauri
  - https://openwork.software/
  - open-source alternative to Claude Cowork, powered by OpenCode
  - Built on OpenCode and utilizes OpenPackage for plugins installation.
  - [I built an open-source alternative to Claude Cowork (on top of opencode!) : r/ClaudeAI _202601](https://www.reddit.com/r/ClaudeAI/comments/1qcf8mu/i_built_an_opensource_alternative_to_claude/)
    - it’s basically an alternative gui for opencode, which (at least until now) has been more focused on technical folks.
    - the goal with openwork is to bring the kind of workflows i’m used to running in the cli into a gui, while keeping a very deep extensibility mindset. ideally this grows into something closer to an obsidian-style ecosystem, but for agentic work.
    - open by design: no black boxes, no hosted lock-in.
    - extensible: skills are installable modules via a skill/package manager, using the native opencode plugin ecosystem.
    - non-technical by default: plans, progress, permissions, and artifacts are surfaced in the ui, not buried in logs.
  - [Show HN: OpenWork – An open-source alternative to Claude Cowork | Hacker News](https://news.ycombinator.com/item?id=46612494)
    - I don't understand the point when opencode desktop already exists.
    - it's fully integrated with Claude Skills.
    - What's the security boundary here - there's no mention of a VM or anything to isolate the agent from the file system?

- https://github.com/DevAgentForge/Claude-Cowork /MIT/202601/ts
  - A desktop AI assistant that helps you with programming, file management, and any task you can describe.
  - fully compatible with the exact same configuration as Claude Code, which means you can run it with any Anthropic-compatible large language model.
  - [开源版本Claude Cowork？ ](https://linux.do/t/topic/1446736)

- https://github.com/langchain-ai/openwork /MIT/202601/ts
  - A desktop interface for deepagentsjs — an opinionated harness for building deep agents with filesystem capabilities planning, and subagent delegation.
  - openwork gives AI agents direct access to your filesystem and the ability to execute shell commands.
  - we should be able to use local open source models
  - https://x.com/LangChain_JS/status/2011863256223400360 _202601
    - We just released 𝚘𝚙𝚎𝚗𝚠𝚘𝚛𝚔, our completely open source take on Claude cowork built on the 𝚍𝚎𝚎𝚙𝚊𝚐𝚎𝚗𝚝𝚜𝚓𝚜 harness.
    - A desktop interface with multi-step planning, filesystem access, and subagent delegation for tactical control over your agents.
  - https://github.com/langchain-ai/deepagentsjs /MIT/202601/ts
    - Using an LLM to call tools in a loop is the simplest form of an agent. This architecture, however, can yield agents that are "shallow" and fail to plan and act over longer, more complex tasks.
    - Applications like "Deep Research", "Manus", and "Claude Code" have gotten around this limitation by implementing a combination of four things: a planning tool, sub agents, access to a file system, and a detailed prompt.
    - deepagents is a TypeScript package that implements these in a general purpose way so that you can easily create a Deep Agent for your application
    - Break complex tasks into manageable steps
    - Sub-Agent Architecture - Delegate specialized work to focused agents
    - File System Integration - Persistent memory and state management
    - Streaming Support - Real-time updates, token streaming, and progress tracking
    - Built on the robust LangGraph framework

- https://github.com/zhu1090093659/CodeConductor /apache2/202601/python/ts
  - Open-source enhanced fork of AionUI / Anthropic Cowork
  - Modern Electron-based desktop application providing a polished chat interface for CLI AI agents (Claude Code, OpenAI Codex). Supports both desktop and web modes.
  - [【开源】开源版本的Cowork，但不仅是Cowork ](https://linux.do/t/topic/1481692)
    - 用瓦砾酱aionui二开的，在原版的基础上做了一些新特性和优化
    - ui还是太简陋了 交互也不太行

- https://github.com/lukilabs/craft-agents-oss /2.4kStar/apache2/202602/ts
  - https://agents.craft.do/
  - https://x.com/balintorosz/status/2013302678105796764  _202601
  - TL; DR - We've released Craft Agents as an open source product - it showcases our take on how to effectively work with agents (Especially Claude Code). 
  - It enables intuitive multitasking, no-fluff connection to any API or Service, sharing sessions, and a more document (vs code) centric workflow - in a beautiful and fluid UI.
  - It leans on Claude Code through the Claude Agent SDK - follow what we found great, and improves areas where we've desired improvements.
  - We ourselves are building Craft Agents with Craft Agents only - no code editors - so really, any customisation is just a prompt away.
  - We built Craft Agents because we wanted a better, more opinionated (and preferably non-CLI way) of working with the most powerful agents in the world. 
  - 只支持anthropic格式的api
    - 可尝试 快手、cliproxyapi
  - 🛝
    - 读 .docx 文件时，thinking的内容多是 read word document content using python-docx, 实际执行 python3 -c "code"
    - 读 .pdf/.md 文件很顺利
    - web fetch 非常慢, 待确定搜索源?
  - https://x.com/dotey/status/2013516064361943148
    - 告别命令行的 Claude Code 体验——保留 Claude Code 的全部能力，但用精心设计的 UI/UX 包装。
    - 解决实际痛点——针对 Claude Code 使用中常见的困扰：难以审查计划、不易理解代码变更的原因、多任务切换困难等问题，提供了更清晰的工作流。
    - 基于 Web 技术栈开发，底层调用 Claude Agent SDK。作者是有 20+ 年经验的 iOS/UIKit 工程师，整个项目 100% 代码由 Claude 编写
    - https://x.com/op7418/status/2018892524937695533
      - 聊天窗口中的文档浏览很舒服

- https://github.com/Liquid4All/cookbook/tree/main/examples/localcowork /MIT/202603/ts
  - LocalCowork is a desktop AI agent that runs entirely on-device. No cloud APIs, no data leaving your machine. The model calls pre-built tools via the Model Context Protocol (MCP), and every tool execution is logged to a local audit trail.
  - LocalCowork ships with 75 tools across 14 MCP servers covering filesystem operations, document processing, OCR, security scanning, email drafting, task management, and more (full tool registry).
  - The agent core communicates with the inference layer via the OpenAI chat completions API. Changing the model is a config change, not a code change. MCP servers are auto-discovered at startup by scanning mcp-servers/.
  - Limitations: 1-2 step workflows are reliable. 4+ step chains degrade as conversation history grows
  - https://x.com/liquidai/status/2029586519389086198
    - LocalCowork is an AI agent that runs on a MacBook. Open source. 
    - Everything runs locally

- https://github.com/eigent-ai/eigent /3.6kStar/apache2/202601/python/ts
  - https://www.eigent.ai/
  - The Open Source Cowork Desktop to Unlock Your Exceptional Productivity.
  - open source cowork desktop application, empowering you to build, manage, and deploy a custom AI workforce that can turn your most complex workflows into automated tasks.
  - Built on CAMEL-AI, our system introduces a Multi-Agent Workforce that boosts productivity through parallel execution, customization, and privacy protection.
  - 100% Open Source - 🥇 Local Deployment - 🏆 MCP Integration
  - Zero Setup - No technical configuration required
  - Enterprise Feature - SSO/Access control
  - Local backend server with full API
  - Local model integration (vLLM, Ollama, LM Studio, etc.)
  - Zero external dependencies
  - For teams who prefer managed infrastructure, we also offer a cloud platform. 
  - Human-in-the-Loop: If a task gets stuck or encounters uncertainty, Eigent will automatically request human input
  - [Local LLMs + Desktop Agents: An open source Claude Cowork : r/LocalLLaMA _202601](https://www.reddit.com/r/LocalLLaMA/comments/1qi3d4c/local_llms_desktop_agents_an_open_source_claude/)
    - At the core is CAMEL’s Workforce system, which is inspired by distributing systems: a root node for task planning and coordination, worker nodes for execution, and an asynchronous task channel. It also supports failure tolerance and recursive workers for long-horizon tasks. All of this is open source.
    - the hardest problems we face today is the local desktop runtime. Supporting multiple operating systems, versions, and package mirrors has been extremely painful. Our desktop agent installs Python and TypeScript dependencies on first launch, and supporting this reliably across macOS and Windows has been more complex than we initially expected.
    - After looking into a VM-based approach that uses Apple’s Virtualization framework to run Ubuntu on macOS, we started wondering whether a similar setup could help.
    - I had to resolve the same issue, to run agent code cross platforms as is, I shipped a runtime which is basically eval inside restricted sandbox https://github.com/netdur/hugind
    - Nice work on the agent! The VM approach might help with the cross-platform headaches but could introduce its own complexity around hardware access and performance overhead
    - Have you considered containerizing just the Python/TS runtime while keeping native OS hooks for system calls?
  - https://github.com/camel-ai/camel /15.4kStar/apache2/202601/python/ts
    - https://www.camel-ai.org/
    - The first and the best multi-agent framework. Finding the Scaling Law of Agents.
    - 看org的仓库，感觉是比langchain更复杂的全家桶
    - Agents maintain stateful memory, enabling them to perform multi-step interactions with environments and efficiently tackle sophisticated tasks.
    - Every line of code and comment serves as a prompt for agents. Code should be written clearly and readably, ensuring both humans and agents can interpret it effectively.

- https://github.com/openkursar/hello-halo /665Star/MIT/202603/ts
  - https://hello-halo.cc/
  - Open-source Claude Code GUI — like Claude Cowork
  - open-source desktop client that makes Claude Code's power accessible to everyone. No terminal, ever.
  - Multi-provider Support — Anthropic, OpenAI, DeepSeek, and any OpenAI-compatible API
  - https://x.com/FlynnWayne_Wang/status/2011079825956749365
    - Remote access from phone/tablet/any browser
    - Built-in AI Browser for web automation
    - 100% of the code after v1 was written by Halo itself

- https://github.com/Kalyankr/localCowork /202601/python
  - AI-powered assistant (Inspired by Cluade Cowork) that lives on your computer.

- https://github.com/ComposioHQ/open-claude-cowork /3.1kStar/MIT/202603/js
  - Open Source version of Claude Cowork built with Claude Code and Composio Tool Router
  - open-source desktop chat application powered by `Claude Agent SDK` and Composio Tool Router.
  - Multi-Provider Support - Choose between Claude Agent SDK and Opencode for different model options
  - Tool Call Visualization - See tool inputs and outputs in real-time in the sidebar
  - https://x.com/KaranVaidya6/status/2011845965234536540
    - I found Claude Cowork to be too expensive. So i asked Claude Code to build me a better version with @composio tool router
    - access local files and your terminal via claude code
    - chain actions across local files and cloud apps in one flow

- https://github.com/DevAgentForge/Open-Claude-Cowork /3kStar/MIT/202602/ts/inactive
  - open-source alternative to Claude Cowork — a desktop AI assistant that helps with programming, file management, and any task you can describe.
  - Reuses your existing ~/.claude/settings.json

- https://github.com/Lucifer1H/open-cowork /MIT/202601/shell
  - brings Claude Cowork's autonomous agent capabilities to OpenCode.
  - Zero Dependencies - Just one markdown file
  - Model Agnostic - Works with any model configured in OpenCode
  - Safe by Default - Uses OpenCode's built-in permission system

- https://github.com/OpenCoworkAI/open-cowork /233Star/MIT/202602/python/ts
  - open-source implementation of Claude Cowork
  - It provides a sandboxed workspace where AI can manage files, generate professional outputs (PPTX, DOCX, XLSX, etc.) through our built-in Skills system, and connect to desktop apps via MCP (browser, Notion, etc.) for better collaboration.
  - Remote Control: Connect to collaboration platforms like Feishu (Lark) and other remote services
  - GUI Operation: Control and interact with various desktop GUI applications on your computer
  - VM-Level Isolation: WSL2 (Windows) and Lima (macOS) VM isolation—all commands execute in an isolated VM to protect your host system.
  - Supports Claude, OpenAI-compatible APIs, and Chinese models like GLM...
  - Skills System: Built-in workflows for PPTX, DOCX, PDF, XLSX generation and processing. Supports custom skill creation and deletion.
  - Real-time Trace: Watch AI reasoning and tool execution in the Trace Panel.

- https://github.com/agi-hub/AGIAgent /python
  - An open-source Vibe platform similar to Claude Cowork / Manus / Openclaw, with professional rich image document generation.

- https://github.com/Safphere/opencowork /apache2/202601/python/ts
  - 你的数字同事
  - 支持多家模型、能执行命令，可以使用MCP和SKILL，也支持多平台使用

- https://github.com/poco-ai/poco-agent /MIT/202601/python/ts
  - https://poco-ai.com/
  - An intelligent agent harnessing cloud-based Claude Code to realize a Manus-like autonomous experience.
  - Poco is a cloud-based AI agent execution platform inspired by Anthropic's Cowork. It orchestrates Claude AI agents to perform autonomous tasks beyond coding—organizing files, writing documents, analyzing data, and more—in a distributed cloud environment.
  - Works in parallel — Queue multiple tasks without waiting for completion
  - [【开源】Poco：把 Claude Code 装进口袋，把 CoWork 搬上云 _202602](https://linux.do/t/topic/1605866)
    - Poco 意思是 Your Pocket Coworker，希望把 Claude Code 的能力拓展到云端
    - 支持接入 MCP、Skills
    - 对话界面进行了很多优化，可以看到不同格式的产物（代码、markdown、ppt、word、xlsx 等等），我们还学习 Manus，添加了沙盒执行过程的重放，能够看到 agent 每一步查看浏览器和执行命令的完整过程

- https://github.com/kuse-ai/kuse_cowork /MIT/202601/rust/ts
  - https://www.kuse.ai/
  - Open-source Alternative to Claude Cowork Desktop App By Kuse
  - Use your own API keys or even bring your own local models 
  - Agent fully written in Rust with zero external dependencies
  - Containerized: Docker isolation for enhanced security
  - [Rust + Local LLMs: An Open-Source Claude Cowork with Skills : r/LocalLLaMA _202601](https://www.reddit.com/r/LocalLLaMA/comments/1qhutc3/rust_local_llms_an_opensource_claude_cowork_with/)

- https://github.com/Prof-Harita/terminaI /387Star/apache2/202601/ts/tauri/inactive
  - Open-source, local-first alternative to Cowork-style computer assistants: real PTY terminal ops, explicit approvals, JSONL audit logs. Windows + Linux + macOS. Model agnostic.
  - CLI (canonical): for developers, power users, and headless environments.
  - Desktop (preview): a Tauri wrapper around the same engine (GUI + voice surface). Linux/Windows are early; macOS is in progress. 

- https://github.com/workany-ai/workany /apache+LOGO/202601/ts
  - https://workany.ai/
  - a desktop AI agent application that executes tasks through natural language. 
  - It provides real-time code generation, tool execution, and workspace management
  - Agent Runtime - Powered by Claude Code
  - Agent SDK - Built on Claude Agent SDK
  - Sandbox - Isolated execution via Codex CLI
  - Multi-provider - OpenRouter, Anthropic, OpenAI, custom providers
  - https://x.com/idoubicc/status/2014630939104776411
    - 沙箱 - 通过 Codex CLI 进行隔离执行？为啥引入 codex
    - 因为用户电脑不一定有代码执行环境，比如 node、python，引入沙箱可以跑脚本处理一些简单的任务。
    - 现在没有内置浏览器，在考虑用沙盒跑 browser-use，还是直接用本地的浏览器。

- https://github.com/fastaistack/OpenChat /MIT/202508/python/inactive
  - https://fastaistack.github.io/OpenChat/
  - 跨平台本地客户端，集成多模型聊天、网络检索、知识库与文档对话，开箱即用、稳定高效。
  - 兼容主流云端大模型：如 OpenAI、Deepseek、硅基流动等
  - 支持本地化模型部署：适配 Ollama，服务器部署等本地运行方案
  - 智能助手应用：集成Kimi，秘塔AI搜索，文心一言，豆包等应用，让你一站式访问国内多个大模型平台
  - 敏感词检测：精准识别敏感内容，确保文本合规
  - 跨平台支持：适配 Windows、Mac
  - 202510: 在v1.0.4的基础上添加了深度求索最新推出的 DeepSeek—OCR 

- https://github.com/GeoRetina/Arion /GPL/202512/python/ts
  - https://www.georetina.com/
  - the first agentic AI desktop app for geospatial analysis, developed by GeoRetina Inc.
  - Built with Electron, React (TypeScript), and Vite, Arion runs natively on Windows, macOS, and Linux, empowering users to leverage local and cloud-based Large Language Models (LLMs), integrate custom Model Context Protocol (MCP) servers, and utilize a plugin system for extended capabilities.

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

- https://github.com/eren726290/opencode-cowork-plugins
  - Standalone OpenCode CLI plugins for Windows. Ported from Anthropic's knowledge-work-plugins.
  - [Coworke Plugins wiped out 100 billion from SaaS. I made for opencode. : r/opencodeCLI _202603](https://www.reddit.com/r/opencodeCLI/comments/1rhrbgg/coworke_plugins_wiped_out_100_billion_from_saas_i/)

## manus/openclaw/computer-use

- https://github.com/openclaw/openclaw /273kStar/MIT/202603/ts
  - https://openclaw.ai/
  - https://docs.openclaw.ai/start/getting-started
  - OpenClaw is a personal AI assistant you run on your own devices. It answers you on the channels you already use (WhatsApp, Telegram, Slack, Discord, Google Chat, Signal, iMessage...)
  - It can speak and listen on macOS/iOS/Android, and can render a live Canvas you control. The Gateway is just the control plane — the product is the assistant.
- https://github.com/Neirth/OpenLobster /GPL/202603/go/ts
  - [OpenLobster – for those frustrated with OpenClaw's architecture : r/openclaw _202603](https://www.reddit.com/r/openclaw/comments/1rum56j/openlobster_for_those_frustrated_with_openclaws/)
  - Neo4j graph database (proper memory system, not .md files)
  - Real multi-user support (RBAC per user per channel)
  - Encrypted secrets backend
  - Task scheduler with cron + ISO 8601
  - [Migrating from OpenClaw to OpenLobster _202603](https://github.com/Neirth/OpenLobster/discussions/44)

- https://github.com/remorses/kimaki /577Star/MIT/202603/ts
  - https://kimaki.xyz/
  - Kimaki is a Discord bot that lets you control OpenCode coding sessions from Discord. Send a message in a Discord channel → an AI agent edits code on your machine.

- https://github.com/Bigchx/NestOS /MIT/202602/js
  - NestOS 运行在具备完整 Linux 图形桌面（GUI）的服务器中，既能像人一样操作浏览器（点击、输入、过验证），也能像运维一样调度底层环境完成部署与交付。
  - 基础设施：Linux (Ubuntu) + 1Panel + Docker/Compose
  - OS: Ubuntu 22.04 x64 (目前仅适配此版本)
  - 浏览器执行层：OpenClaw Browser (Chrome)
  - 图形交互层：XRDP + XFCE4
  - 控制端：Web / Discord / Telegram / 飞书 / ...（支持所有可接入 OpenClaw 的软件，如 WhatsApp 等）
  - AI 记忆能力：qmd 索引 + 语义检索 + 本地日志
  - [【开源自荐】我们把 VPS 变成了带桌面的“数字员工”，基于 OpenClaw 和 1Panel 搓了一套 GUI 自动化环境，理论上 100% 解决网页交互难题 _202602](https://linux.do/t/topic/1632379)
    - 配置: 建议 4 核 8G 内存 (4H8G)，带宽别太小（毕竟要传桌面画面）。
    - 验证码墙：通过 “AI 执行 + 人工协助” 解决自动化登录死角。

- https://github.com/0xranx/golembot /MIT/202603/ts
  - https://0xranx.github.io/golembot/
  - Any Agent × Any Provider × Anywhere
  - Compatible with 13, 000+ OpenClaw community skills
  - [【开源推广】让 Claude Code、Codex、Cursor、OpenCode 也支持接入微信/飞书/（甚至自己的产品） _202603](https://linux.do/t/topic/1802351)
    - Claude Code 前两天出了 Channels，可以把 Agent 挂到 Telegram 和 Discord 上，论坛里讨论也不少。
    - 我之前做了个开源项目 GolemBot，做的事情差不多，但覆盖面更广一些——不只是 Claude Code，Cursor、Codex、OpenCode 也都能接；通道这边除了 Telegram 和 Discord，还支持微信、飞书、钉钉、企业微信、Slack。 最近刚把个人微信也接上了

## office

- https://github.com/zhu1090093659/minister /apache2/202603/ts
  - 把 Claude Code 塞进飞书，给你的团队加一个全能同事。
  - 丞相是一个基于 Claude Code 的飞书 AI 助手框架，为企业团队打造。它不是又一个聊天机器人——它是一个住在飞书里的同事，能直接帮你发消息、建任务、写文档、排日程、操作多维表格，说完就办，不用你再动手。
  - 为每位同事维护专属记忆。你说过"我的周报喜欢分三段写"，它就记住了，下次直接照做。张三的习惯是张三的，李四的偏好是李四的，互不干扰。会话断了、服务重启了，记忆都还在。
  - 底层，丞相通过 MCP 协议将飞书 API 暴露给 Claude Code，让 AI 拥有真正的执行力而不只是生成文本。整个项目用 TypeScript 写成，Bun 驱动，Docker 一键部署。
  - [【开源】“丞相“——企业版OpenClaw _202603](https://linux.do/t/topic/1703072)

- https://github.com/googleworkspace/cli /MIT/202603/rust
  - This is a very well implemented CLI. It's so thorough. It dynamically registers commands, it's designed for a browser-wielding agent to automate the setup steps, it can start a MCP daemon…
  - https://x.com/addyosmani/status/2029372736267805081
    - Google Drive, Gmail, Calendar, and every Workspace API. 40+ agent skills included.

- https://github.com/jaredpalmer/mogcli /MIT/202603/go
  - Unofficial agent-friendly Microsoft 365 CLI
  - mogcli is a Microsoft Graph CLI for personal Microsoft accounts (MSA) and enterprise Microsoft Entra ID accounts. It provides scriptable commands for Mail, Calendar, Contacts, Groups, Tasks, and OneDrive.
  - https://x.com/jaredpalmer/status/2029643407606563140
    - (h/t to @steipete ’s for gogcli)

- https://github.com/griches/apple-mcp /MIT/202603/ts
  - A collection of Model Context Protocol (MCP) servers that provide AI assistants with access to native Apple applications on macOS.
  - [Apple Services MCP : r/mcp](https://www.reddit.com/r/mcp/comments/1rk4gys/apple_services_mcp/)
    - I’ve made a telegram bridge to this now so I can just message it requests and it will do my admin stuff like finding how details and adding stuff to my calendar.
    - I thought it had already an iMessage MCP by Anthropic. 

- https://github.com/ItMeDiaTech/Documentation_Hub /MIT/202602/ts/Electron
  - A modern desktop application for managing document processing workflows with advanced hyperlink management, table of contents generation, and comprehensive document styling capabilities.
  - Session-Based Workflow: Organize your document processing tasks into sessions, each maintaining its own configuration, documents, and processing history.
  - Add multiple Word documents (.docx) to each session
  - 类似headless的实现模式, 不需要打开编辑器，直接修改选择任务，然后一键执行
  - app未使用大模型
  - Hyperlink Management: Append custom content IDs to hyperlink URLs
  - Table of Contents Generation: Right-align page numbers option
  - Table Uniformity
  - Tracked Changes Visualization
  - Document Processing: DocXMLater 10.1 (type-safe OOXML processing)
  - State Management: React Context with Zustand
  - Data Persistence: IndexedDB for sessions, LocalStorage for settings
  - https://github.com/ItMeDiaTech/Documentation_Hub/releases/tag/v2.0.0
    - dmg

- https://github.com/iiinnovation/Solidify /MIT/202603/ts
  - 一款专为非研发背景实施人员打造的轻量级 AI 工具，专注文档生成、演示准备和知识管理。
  - 9 个内置技能 - 需求分析、方案设计、演示文稿、测试方案等
  - 多格式导出 - PPTX、PDF、DOCX、Markdown、HTML
  - 云端同步 - 可选的 Supabase 云端存储，多设备同步
  - Tauri 打包，体积小（~50MB），启动快（<1s）
  - [【开源分享】为实施人员打造的轻量级 AI 工具，专注文档生成、演示准备和知识管理 _202603](https://linux.do/t/topic/1681661)

- https://github.com/hewliyang/office-agents /MIT/202603/ts
  - Office Agents is a monorepo of Microsoft Office Add-ins with integrated AI chat panels. Each add-in connects to major LLM providers using your own credentials (BYOK) and can read/write documents through built-in tools, a sandboxed shell, and a virtual filesystem.
  - https://x.com/hewliyang/status/2033176726663249959
    - OpenWord v0.0.1 is out. it is competent at most text editing operations, can insert images into your doc, has vision, can add & reply to comments, and even works with Track Changes (redlining)
  - https://x.com/hewliyang/status/2030648851603087392
    - i've also renamed the open-excel repo into office-agents.
    - the SDK, which contains the agent loop, IndexedDB storage logic, etc is published to NPM. so you can build your own plugins.
    - fwiw, powerpoint is only ~2.5k LoC excluding the system prompt and the officejs .d.ts file
- https://github.com/tdimino/dabarat /MIT/202603/python/js
  - AI-native markdown previewer with annotations, bookmarks, and live reload. Zero dependencies.
  - 5 annotation types — Comment, Question, Suggestion, Important, Bookmark
  - Threaded replies — reply to any annotation inline
  - Resolve/archive workflow — resolved annotations move to a separate archive file

- https://github.com/chenhuawang-04/DocuFlow /apache2/202603/python
  - AI Powered Document Toolbox. Designed for codex/claude code
  - It exposes 149 tools across Word, Excel, PowerPoint, PDF, format conversion, OCR, HTML-to-PPTX, and AI image generation workflows.
  - The project is designed to provide one consistent MCP surface for common document tasks, so Claude Code, Codex, and other MCP-compatible clients can operate on documents directly.
  - [【DocuFlow】一个命令行Cli的文档处理MCP/SKILL工具集 - LINUX DO _202603](https://linux.do/t/topic/1760765)

- https://github.com/Prismer-AI/Prismer /BSL/202601/python/ts
  - https://paper.prismer.ai/
  - Open Source OpenAI Prism Alternative
  - [OpenAI just announced “Prism.” Our project is Prismer, so we’re open-sourcing everything now : r/Python](https://www.reddit.com/r/Python/comments/1qq1u91/openai_just_announced_prism_our_project_is/)
  - [Prismer: A self-hosted, open-source alternative to OpenAI Prism for academic research : r/selfhosted _202601](https://www.reddit.com/r/selfhosted/comments/1qq10su/prismer_a_selfhosted_opensource_alternative_to/)

- https://github.com/hehecat/gongwen /202602/ts
  - https://hehecat.github.io/gongwen/
  - 基于 GB/T 9704 国标的党政机关公文在线排版工具，支持实时预览、智能分页和 DOCX 导出。
  - 先解析为文本，再渲染为dom
  - [AI糊一个在线公文格式化工具 ](https://linux.do/t/topic/1641274)
    - 纯 vibe code，没看一点代码，没考虑有表格等情况，不过大致格式是确定的
    - 提几点小建议：
      - 不建议用行距来实现每页 22 行。应该通过调整页边距参数和限制每页 22 行来实现，原因有二：一是国标规定撑满版心的要求，直接 28/29 磅是撑不满的，二是插图片也会直接只剩一下一行图片。如果一定要磅数。建议是 29.6 磅，上 34.6 mm，下 32.6 mm，左 28 mm，右 26 mm。
    - 不建议默认是 GB2312，这个问题老生常谈了
      - 一是首先 GB2312 不是国标强制要求使用的仿宋，它只是当年的一种编码格式，包含的字体实在太少了，很多文件里会出现字体缺失的情况，尤其是一些名单的公布，姓名的生僻字格外多。像现在的 GB18130 则能很好地囊括这一点。
      - 二是现在绝大部分人的电脑都没有 GB2312 的字体，如果是一些附件报名表之类的以 word 形式下发，则显示效果完全不对。
      - 三，其实还是，国标根本没有要求用 GB2312，而是仿宋（正文），技术上进步了，但是仍被某些权威所禁锢。
      - GB2312 的字体确实更粗一些更适合看，但我个人觉得方正仿宋也挺好看的，你会发现越是更上层的机关就越少用 GB2312，你看沪府的文件，我感觉就很像方正仿宋，大部分的看着也直接是电脑自带的仿宋。当然，绝大部分正式的公文，或者说 GB/T 9704 是给印刷公文使用的，用专业排版软件才能完美符合，普通人用办公软件制作符合格式的公文不能简单套用参数。
      - 顺带一提其实也没要求英文和数字要求新罗马，甚至要求页码的 - 1 -，用的是宋体，当然了这些都是习惯了，而且新罗马电脑都有，且不会出现缺失这种情况。
    - 我们现在还是沿用 GB2312，数字新罗马。 另外提个 BUG， 引号 “ 现在是新罗马，要改成中文字体

- https://github.com/amluckydave/shiyu /MIT/202603/ts/vue/tauri
  - https://amluckydave.github.io/shiyu/
  - 拾语 — 外刊精读 · 原版书阅读利器 | AI 划词标注、长难句拆解、FSRS 间隔复习 (Tauri 2 + Vue 3 + Rust)
  - AI 思维导图	一键分析文章结构，中英双语切换，缓存秒开
  - AI 翻译 & 解析	流式翻译，句子成分彩色标注，兼容 DeepSeek/OpenAI
  - 生词本 & 句子库	搜索、批量操作、来源跳转、TTS 朗读
  - 在线编辑	md-editor-v3 全功能编辑器，实时预览
  - OCR 导入	PP-StructureV3 识别 + AI 校正，一键导入
  - 数据管理	JSON 导入/导出，支持合并或覆盖
  - 前端	Vue 3 + TypeScript + Vite + Vue Router + Pinia
  - 后端	Rust + rusqlite (SQLite) + reqwest + tokio
  - 解析渲染	epub + html2md + scraper + marked + md-editor-v3
  - 思维导图	markmap-lib + markmap-view
  - 语音	edge-tts-universal（三级缓存）
  - [【开源自荐】拾语：外刊、外文原版书精读利器  - LINUX DO _202603](https://linux.do/t/topic/1786244)

### office-skills

- https://github.com/MiniMax-AI/skills /MIT/202603/csharp
  - Development skills for AI coding agents. Plug into your favorite AI coding tool and get structured, production-quality guidance for frontend, fullstack, Android, iOS, and shader development.
  - [白领福音？MiniMax 开源 Office Skills：生产级办公文档引擎，覆盖 Word/Excel/PDF/PPT - LINUX DO _202603](https://linux.do/t/topic/1810907)
    - 3月25日，MiniMax 正式开源一整套 Office Skills，覆盖 Word（docx）、Excel（xlsx）、PDF、PPT（pptx）四种格式的文档生成与编辑能力
    - MiniMax-docx：选择 .NET OpenXML SDK（微软官方库）而非 python-docx，牺牲部署便利性换取对 Word 文档结构更完整的控制力。覆盖从零生成、在已有文档上编辑、模板套用三种场景
    - MiniMax-xlsx：绕开所有 Python Excel 库，直接在 XML 层面操作（解压→修改目标 XML 节点→重新打包），确保样式、图表、宏原封不动保留。开发了 13 个独立 Python 工具脚本 + 34,000 字金融格式化标准文档
    - MiniMax-pdf：封面用 HTML+CSS 通过 Playwright 渲染，正文用 ReportLab 排版，最后合并。为 15 种文档类型设计了独立视觉语言
    - PPTX-generator：基于 PptxGenJS，定义 5 种标准页面类型（封面/目录/章节分割/内容/总结）和 4 套视觉配方（Sharp/Soft/Rounded/Pill）
    - 前些天刷到佬友发的适用于wps的一套skill

## reader

- https://github.com/codedogQBY/ReadAny /GPL/2026t03/ts
  - https://codedogqby.github.io/ReadAny/
  - An AI-powered e-book reader with semantic search, intelligent chat, and knowledge management
  - [【开源自荐】ReadAny：一款与AI 深度结合的开源跨端电子书阅读器  - LINUX DO _202603](https://linux.do/t/topic/1809537)

## research

- https://github.com/Agents2AgentsAI/ata /apache2/202602/rust/ts
  - AI agents for solving engineering and research problems end to end
  - [We forked Codex CLI and turned it into a full research agent — it searches papers, reads PDFs, traverses citation graphs, and synthesizes everything into navigable documents : r/codex _202602](https://www.reddit.com/r/codex/comments/1rem9ai/we_forked_codex_cli_and_turned_it_into_a_full/)
    - We saw that with the current Codex, we have to spend a lot of manual efforts to handle pdfs, and adjust the prompts to get the results we want.
    - I have been using both Claude Code and Codex in parallel due to Claude Code’s ability to handle pdfs natively and it feels pretty “handicapped” now to switch to Claude.
  - why fork codex?
    - Codex gave us the best foundation for this. Paper reading is just step one — the roadmap is letting researchers pull methods from papers, combine them, and actually build from it. Code, experiments, prototypes, all from the terminal. The sandbox and agentic architecture gave us a huge head start.
    - Also it's all Rust, so it's fast and smooth.
  - What are you using to parse PDFs?
    - For pdf files, we encode as base64 and send to the LLM providers. For urls, we send the them directly to the providers, except Gemini doesn't accept pdf urls so we still send base64 data. It's much better than parsing them first and then sending a combination of text and figures to the providers, especially for scientific papers. I believe Claude Code also handles this similarly.
  - wouldn't the base model, e.g., chatgpt 5.2 (thinking) be more suitable to do this tyle of work than codex, which is specialized in coding?
    - Yes, that’s my experience too. I usually use gpt-5.2 high for reading papers and switch to gpt-5.3-codex xhigh for updating our codes.
  - A very nicely working tool. It’s just a pity that when changing the model, it doesn’t respect the option to specify a host for an OpenAI-compatible API. For example, I use Codex Loadbalancer, and when I change something like the model’s reasoning level, the provider automatically switches back to OpenAI. 

## fact-checking

- https://github.com/EmmaStoneX/NetPulse /MIT/202601/ts
  - https://netpulse.zxvmax.com/
  - [【开源自荐】事件视界，从“获取信息”升级到“获取洞察” ](https://linux.do/t/topic/1421261)
  - 最初的想法是：能有个快速扫描全球科技热点动态，然后还能跟历史上的类似事件对比的一个玩具，在AI Studio用build创建了最初的原型。
  - 做了前后端分离

- https://github.com/KeaBase/kea-research /BSL/202601/python/ts/astro
  - https://keabase.com/
  - Multi-AI collaboration platform that combines responses from multiple AI models, cross-validates information, and delivers verified, consensus-backed answers.
  - [[Open Sourse] I built a tool that forces 5 AIs to debate and cross-check facts before answering you : r/LocalLLM](https://www.reddit.com/r/LocalLLM/comments/1qj3l75/open_sourse_i_built_a_tool_that_forces_5_ais_to/)
    - So you copied pewdiepies council concept. 
  - https://github.com/karpathy/llm-council

## fintech/stock

- https://github.com/ZhuLinsen/daily_stock_analysis /MIT/202601/python
  - [[开源自荐] 基于AI的股票分析系统 _202601](https://linux.do/t/topic/1427263)
  - 起初只是自己做一个帮忙分析自选股和大盘的工具，减少盯盘、盯股票分析的精力，后面本着开源精神开源出来了，能够每天定时推送到企业微信上。
  - 用的都是免费的方案，github action + Gemini的API + Serpapi和TAVILY的检索功能，免费额度足够日常使用
  - 每日自动生成大盘复盘

- https://github.com/brokermr810/QuantDinger /apache2/202601/python/js/vue
  - https://ai.quantdinger.com/
  - a local-first, privacy-first, self-hosted quantitative trading infrastructure. 
  - It runs on your own machine/server, providing multi-user accounts backed by PostgreSQL while keeping full control of your strategies, trading data, and API keys.
  - runs locally. Your strategies, trading logs, API keys, and analysis results stay on your machine. No vendor lock-in
  - [【开源自荐】目前全网最全市场的AI量化工具【QuantDinger】，全面开源 ](https://linux.do/t/topic/1507020)

## ecommerce

- https://github.com/liangdabiao/amazon-sorftime-research-MCP-skill /MIT/202603/python
  - 亚马逊选品 之 Listing全维度穿透分析报告 加上 全品类分析 ，关键词分析，差评分析 等等。claude code agent skill, amazon sorftime research MCP 智能体skill. 
  - 基于 Sorftime MCP 服务和 Claude Skills 的亚马逊竞品分析工具集。
  - [【公益推广】周末加班-完成了跨境电商amazon选品分析之差评分析-6维痛点分析框架  _202603](https://linux.do/t/topic/1759097)

## social

- https://github.com/dreammis/social-auto-upload /MIT/202603/python/js/vue
  - https://sap-doc.nasdaddy.com/
  - 自动化上传视频到社交媒体：抖音、小红书、视频号、tiktok、youtube、bilibili
  - [[开源自荐]  [social-auto-upload] 社交媒体自动化发布 - LINUX DO _202603](https://linux.do/t/topic/1809328)

## openclaw

- https://github.com/suitedaces/dorabot /MIT/202602/ts
  - https://dora.so/
  - [How to turn Claude Code into a personal agent with memory and goals : r/ClaudeCode](https://www.reddit.com/r/ClaudeCode/comments/1rb2i61/how_to_turn_claude_code_into_a_personal_agent/)
    - I built an open-source agent that wraps the Claude Agent SDK into a persistent daemon on your Mac. 
    - It has memory, goals, scheduled tasks, messaging channels, browser automation, and more
    - Gateway server on localhost wraps the Claude Agent SDK, which spawns Claude Code as a subprocess. 
    - You get all the standard tools (Read, Write, Bash, Grep, etc.) plus custom MCP tools (browser via CDP, screenshots, messaging, scheduling, goals) with persistent state on top. Everything local, no cloud relay.
    - Memory: No RAG, no vector store. Just a curated MEMORY.md (preferences, decisions, context) loaded every session, plus daily journals at memories/YYYY-MM-DD/MEMORY.md the agent writes to as it works. 

- https://github.com/netease-youdao/lobsterai /MIT/202602/python/ts
  - https://lobsterai.youdao.com/
  - all-in-one personal assistant Agent developed by NetEase Youdao. It works around the clock to handle your everyday tasks — data analysis, making presentations, generating videos, writing documents, searching the web, sending emails, scheduling tasks, and more.
  - At its core is Cowork mode — it executes tools, manipulates files, and runs commands in a local or sandboxed environment, all under your supervision. 
    - Cowork is the core feature of LobsterAI — an AI working session system built on the Claude Agent SDK.
  - You can also chat with agent via Telegram, Discord, DingTalk or Feishu (Lark) and get work done from your phone anytime, anywhere.
  - Local + Sandbox Execution — Run tasks directly on your machine or in an isolated Alpine Linux sandbox
  - Built-in Skills — Office document generation, web search, Playwright automation, Remotion video generation, and more
  - Scheduled Tasks — Create recurring tasks via conversation or the GUI
  - Persistent Memory — Automatically extracts user preferences and personal facts from conversations
  - Mobile via IM — Control your Agent remotely from your phone through Telegram, Discord, DingTalk, or Feishu
  - Permission Gating — All tool invocations require explicit user approval before execution
  - Cross-Platform — macOS (Intel + Apple Silicon), Windows, Linux desktop, plus mobile coverage via IM
  - Local Data — SQLite storage keeps your chat history and configuration on your device
  - LobsterAI uses Electron's strict process isolation. All cross-process communication goes through IPC.
  - Uses electron-builder to produce platform-specific installers. 
  - https://x.com/fengzhou/status/2024332482322329905
    - What’s the difference between OpenClaw and LobsterAI
    - LobsterAI has GUI for mac and windows. So no terminal skills are needed for the user.
  - https://x.com/dotey/status/2024337839916286380
    - LobsterAI has GUI for mac and windows. So no terminal skills are needed for the user.技术上基于 Electron + React + TypeScript 构建，采⽤严格的进程隔离架构，任务⽀持本地执⾏和沙箱 VM（QEMU + Alpine Linux）两种模式。数据层使⽤ SQLite 实现全本地化存储，IM ⽹关层通过钉钉 Stream、⻜书 SDK 等对接各平台。
# cv
- https://github.com/IDEA-Research/Rex-Omni /1kStar/IDAE/202512/python/华人作者
  - https://rex-omni.github.io/
  - Detect Anything via Next Point Prediction (Based on Qwen2.5-VL-3B)
  - 视觉效果是检测物体，不确定文本检测效果
  - Rex-Omni is a 3B-parameter Multimodal Large Language Model (MLLM) that redefines object detection and a wide range of other visual perception tasks as a simple next-token prediction problem.
  - Unified architecture for multiple vision tasks
  - Rex-Omni reformulates visual perception as a next point prediction problem, unifying diverse vision tasks within a single generative framework. It predicts spatial outputs (e.g., boxes, points, polygons) auto-regressively and is optimized through a two-stage training pipeline—large-scale Supervised Fine-Tuning (SFT) for grounding, followed by GRPO-based reinforcement learning to refine geometry awareness and behavioral consistency.
  - https://github.com/Mountchicken/Resophy /202512/python/js
    - Resophy is an HTML-based AI paper reader with: AI Translation & Analysis — instantly understand structure
    - modern paper reader that helps you quickly understand the core content of papers through a simple tech stack (HTML + JavaScript + Python Flask) and AI features
    - Main Service (Resophy Core): HTML + JavaScript + Python Flask backend service, providing core features such as paper management, classification, and search
    - LLM Server: LLM inference service for AI translation, interpretation, and arXiv paper analysis (optional, supports local deployment or remote API)
    - MinerU Server: Document parsing service for PDF to Markdown parsing (optional, for AI features)

- https://github.com/roboflow/supervision /MIT/202502/python
  - https://supervision.roboflow.com/
  - We write your reusable computer vision tools. Whether you need to load your dataset from your hard drive, draw detections on an image or video, or count how many detections are in a zone.
  - Supervision was designed to be model agnostic. Just plug in any classification, detection, or segmentation model.
    - we have created connectors for the most popular libraries like Ultralytics, Transformers, or MMDetection.
# video
- https://github.com/zapdos-labs/unblink /182Star/AGPL/202512/ts
  - Unblink is a camera monitoring application that runs AI vision models on your camera streams in real-time
  - Object detection
  - Intelligent search across your video feeds.

- https://github.com/chatfire-AI/huobao-drama /202601/go/ts/vue
  - 基于 Go + Vue3 的全栈AI短剧自动化生产平台
  - 基于AI的短剧自动化生产平台，实现从剧本生成、角色设计、分镜制作到视频合成的全流程自动化。
  - 使用大语言模型自动生成剧本、角色设定和分镜脚本
  - AI绘图生成角色形象和场景背景
  - 基于文生视频模型自动生成分镜视频
  - 支持批量生成和异步任务处理
  - [【开源短剧】AI短剧创作工具 _202601](https://linux.do/t/topic/1431841)
  - [开源短剧产品三周时间的总结和思考 _202601](https://linux.do/t/topic/1547232)
  - https://github.com/chatfire-AI/huobao-canvas
    - 火宝无限画布；支持文生图，图生图，图生视频，多模型切换。兼容 openai标准格式
    - [【开源自荐】花两天时间做了一个无限画布，开源了一个 乞丐版 lovart _202601](https://linux.do/t/topic/1438600)
# more
