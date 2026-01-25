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

- https://github.com/onlook-dev/onlook /apache2/202502/ts
  - https://onlook.com/
  - The open source Cursor for Designers. 
  - Design directly in your live React app and publish your changes to code.

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

## ai-card

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
# ai-apps
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
  - https://github.com/camel-ai/camel /15.4kStar/apache2/202601/python/ts
    - https://www.camel-ai.org/
    - The first and the best multi-agent framework. Finding the Scaling Law of Agents.
    - 看org的仓库，感觉是比langchain更复杂的全家桶
    - Agents maintain stateful memory, enabling them to perform multi-step interactions with environments and efficiently tackle sophisticated tasks.
    - Every line of code and comment serves as a prompt for agents. Code should be written clearly and readably, ensuring both humans and agents can interpret it effectively.

- https://github.com/openkursar/hello-halo /MIT/202601/ts
  - The Missing UI for Claude Code
  - open-source desktop client that makes Claude Code's power accessible to everyone. No terminal, ever.
  - https://x.com/FlynnWayne_Wang/status/2011079825956749365
    - Remote access from phone/tablet/any browser
    - Built-in AI Browser for web automation
    - 100% of the code after v1 was written by Halo itself

- https://github.com/Kalyankr/localCowork /202601/python
  - AI-powered assistant (Inspired by Cluade Cowork) that lives on your computer.

- https://github.com/ComposioHQ/open-claude-cowork /MIT/202601/js
  - Open Source version of Claude Cowork built with Claude Code and Composio Tool Router
  - open-source desktop chat application powered by Claude Agent SDK and Composio Tool Router.
  - Multi-Provider Support - Choose between Claude Agent SDK and Opencode for different model options
  - Tool Call Visualization - See tool inputs and outputs in real-time in the sidebar
  - https://x.com/KaranVaidya6/status/2011845965234536540
    - I found Claude Cowork to be too expensive. So i asked Claude Code to build me a better version with @composio tool router
    - access local files and your terminal via claude code
    - chain actions across local files and cloud apps in one flow

- https://github.com/Safphere/opencowork /apache2/202601/python/ts
  - 你的数字同事
  - 支持多家模型、能执行命令，可以使用MCP和SKILL，也支持多平台使用

- https://github.com/Lucifer1H/open-cowork /MIT/202601/shell
  - brings Claude Cowork's autonomous agent capabilities to OpenCode.
  - Zero Dependencies - Just one markdown file
  - Model Agnostic - Works with any model configured in OpenCode
  - Safe by Default - Uses OpenCode's built-in permission system

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
# more
