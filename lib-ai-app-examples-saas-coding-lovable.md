---
title: lib-ai-app-examples-saas-coding-lovable
tags: [ai, ai-coding, examples, saas]
created: 2026-04-07T11:47:47.315Z
modified: 2026-04-07T11:51:51.225Z
---

# lib-ai-app-examples-saas-coding-lovable

# guide

# popular
- https://github.com/WyRainBow/Resume-Agent /MIT/202604/python/ts
  - 一句话输入、生成可编辑、可导出的专业简历。
  - 可视化编辑：左侧编辑、右侧实时预览、支持模块化调整
  - AI 辅助优化：支持分模块导入、改写、润色和内容增强
  - 高质量导出：基于 LaTeX 生成专业 PDF、支持中英文渲染
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

- https://github.com/ZSeven-W/openpencil /1.9kStar/MIT/202603/ts
  - https://op.zseven.tech/
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
    - 兼容 .pen，支持 .fig 导入，还原度相当高， .fig 由于结构化过于混乱，还没有完美适配
    - 一键导出React/Vue等8种原生代码，还原度接近100%

- https://github.com/open-pencil/open-pencil /3.8kStar/MIT/202603/ts/vue/tauri
  - https://openpencil.dev/
  - AI-native design editor. Open-source Figma alternative.
  - Open-source design editor. Opens .fig and .pen design files, includes built-in AI, and ships as a programmable toolkit with a headless Vue SDK for building custom editors.
  - core依赖 canvaskit-wasm、diff、svgpath、yoga-layout、sucrase、fflate、fontoxpath
  - Note: There is another open-source project with the same name — OpenPencil by ZSeven-W, focused on AI-native design-to-code workflows. This project focuses on Figma-compatible visual design with real-time collaboration.
  - Opens .fig and .pen files — read and write native Figma files, open Pencil documents, copy & paste nodes between apps
  - Fully programmable — headless CLI, Figma Plugin API via eval, MCP server for AI agents
  - Real-time collaboration — P2P via WebRTC, no server, no account. Cursors, presence, follow mode
  - Auto layout & CSS Grid — flex and grid layout via `Yoga` WASM, with gap, padding, alignment, track sizing
  - Tailwind CSS export — export any selection as HTML with Tailwind v4 utility classes
  - ~7 MB desktop app — Tauri v2 for macOS, Windows, Linux. Also runs in the browser as a PWA

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

- https://github.com/donghaxkim/react-rewrite /MIT/202603/ts
  - react-rewrite lets you edit a React app visually while it is running locally, then automatically writes those changes back to the source files in your project.
  - It is built for local development and works by opening a proxy in front of your dev server and injecting an overlay into the page.
  - Select an element and inspect its component name, file path, and line number
    - Edit supported Tailwind-based layout, spacing, size, typography, and color properties
    - Undo in-progress canvas changes and review applied changes in the changelog
  - https://x.com/imdonghakim/status/2038230475894899119
    - how it works
      - reads your fiber react tree to find the element
      - parses your source file's AST
      - finds the JSX node and rewrites the className
      - deterministic AST transforms
      - no AI
# webapp-agent
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
# UI-gen
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

## ai-card-ui

- https://github.com/Rpeng666/Ant-Card /apache2/202510/ts
  - 现代化的在线卡片编辑器 - 支持多种精美模板，实时预览，PDF导出，AI 智能生成
  - 15+ 精美模板 - 从简约到创意，满足各种场景需求
  - 实时编辑 - 所见即所得的卡片编辑体验
  - AI 集成 - 智能内容生成和优化
  - 多格式导出 - PNG、JPEG、PDF 等多种格式
  - 支持 Model Context Protocol，可在 Claude Desktop 等工具中使用
  - 本地存储 - 支持保存和加载卡片项目
# designing/builder

# 3d
- https://github.com/TangSY/aedifex /MIT/202604/ts
  - https://aedifex.app/
  - Open-source 3D architectural editor with AI design assistant
  - [【开源】用自然语言驱动的开源 3D 建筑设计 AI 编辑器-Aedifex - LINUX DO _202604](https://linux.do/t/topic/1932519)
    - 运行在浏览器中的 3D 建筑编辑器，集成了基于大语言模型的 AI 设计助手。你可以通过自然语言描述设计意图，AI 直接在三维场景中执行建墙、开窗、摆放家具等操作——不需要学习任何专业建模工具。
    - 项目基于上游开源 3D 编辑器内核深度改造，重新设计了场景数据架构和渲染管线，并在此基础上构建了完整的 AI 辅助设计能力。
    - 在 GitHub 上看到一个开源的 3D 建筑编辑器项目，基础能力不错——墙体、门窗、家具摆放都有了，Three.js 渲染，浏览器里就能跑。但交互方式还是传统的那一套：左边工具栏选工具，右边属性面板调参数，中间画布上点来点去。能用，但对非专业用户来说门槛不低。
    - 看到这个编辑器的时候觉得方向对了：3D 建筑设计天然适合自然语言交互——人描述空间的时候用的就是"客厅放一组沙发，对面摆电视柜"这样的语言，而编辑器的每一个操作（建墙、开窗、放家具）都可以被抽象成结构化的工具调用。把 AI Agent 接入编辑器的操作接口，用户就不需要学习任何工具，直接用自然语言描述就行。
    - 真正动手之后才发现，"接入 AI"远不是加个对话框那么简单。原项目的数据结构、渲染方案、交互逻辑都是为手动编辑设计的，要让 AI 成为核心交互方式，几乎每一层都需要重新设计。
    - 原项目的节点结构不太适合 AI 操作——AI 需要快速定位和操作任意节点。重新设计成了扁平字典 + parentId 引用的架构：所有节点（墙体、门窗、家具、楼板、屋顶等）平铺存储在一个 `Record<NodeId, Node>` 字典中，通过 parentId 表达层级关系，任何节点都可以通过 ID 直接索引。
    - 兼容任何 OpenAI 格式的 API 端点——官方 OpenAI、Azure OpenAI、本地 Ollama、DeepSeek 等均可。
  - https://github.com/pascalorg/editor /9.8kStar/MIT/202604/ts
    - A 3D building editor built with React Three Fiber and WebGPU.
# docs/wiki

# examples

# more
