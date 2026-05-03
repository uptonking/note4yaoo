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

- https://github.com/ZJU-LLMs/OpenStory /apache2/202604/python
  - http://xhslink.com/o/9aBzc2kULyF
  - a multi-agent deduction and simulation framework developed based on Large Language Models (LLMs) and Agent-Kernel.
  - https://github.com/ZJU-LLMs/Agent-Kernel
    - multi-agent system development framework, which is designed to powerfully enable large-scale social simulation.
  - [OpenStory：拒绝线性结局，你的故事从此拥有 1000 种活法 - LINUX DO _202604](https://linux.do/t/topic/1940123)
    - 还原了红楼梦的世界，可以任意添加智能体，指派任务，有点像一个游戏版的斯坦福小镇。 你可以实现孙悟空棒打王熙凤，柯南调查大观园等任何你想要的剧情
    - 我制作了一个 1：1 还原的红楼梦前端，宁国府，荣国府，大观园完全合理的空间安排。 地图上会显示所以角色的模型，以及它们的动作，对话，记忆，像上帝一样观察红楼梦的故事。
    - 后端纯 python 架构，前端为 web 架构，非常轻量 
    - 我感觉我们最大的特点是可以自由添加角色，还可以指定行动
    - 可以自动推演剧情，会比较有意思，但是这种项目的痛点都是token消耗比较高，我们用各种方法，降低到了1个tick用flash模型只要3毛左右
# ai-apps
- https://github.com/NPC-Worldwide/incognide /AGPL/202604/ts/类似全家桶
  - https://enpisi.com/incognide
  - Incognide unifies chat, code, documents, web browsing, and media into a tileable workspace with intelligent context and composable automations.
  - https://github.com/npc-worldwide/npcsh /MIT/python
    - The agentic shell for building and running AI teams from the command line.
  - https://github.com/npc-worldwide/npcpy /MIT/python
    - flexible agent framework for building AI applications

- https://github.com/NitroRCr/nyaai /apache2/202603/ts/vue
  - https://nyaai.cc/
  - [[开源] Nya AI: 在一个地方进行 AI 对话 / 网络搜索 / 笔记 / 协作 / 频道 / 网盘  - LINUX DO _202603](https://linux.do/t/topic/1787694)
    - Nya AI 结合了 AI 对话客户端和协作平台，让你能够在一个平台进行 AI 对话、网络搜索、记笔记、编写文档、与团队沟通/协作、管理文件等操作。
    - Nya AI 是可协作的平台，因此所有内容都储存在云端，你可以随时通过任意设备访问所有内容。得益于同步引擎 ZeroSync
    - 类似于传统搜索引擎和 AI 搜索的结合，左侧是搜索结果，右侧会生成 AI 总结回答，也可进行后续对话。

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

## cowork

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

- https://github.com/different-ai/openwork /1.1kStar/MIT+EE/202601/rust/ts/tauri
  - https://openwork.software/
  - https://openworklabs.com/
  - open-source alternative to Claude Cowork, powered by OpenCode
  - Built on OpenCode and utilizes OpenPackage for plugins installation.
  - [Future licensing: is OpenWork going closed source? _202604](https://github.com/different-ai/openwork/issues/1412)
  - [OpenWork, an opensource Claude Cowork alternative, is silently relicensing under a commercial license : r/LocalLLaMA _202604](https://www.reddit.com/r/LocalLLaMA/comments/1sgnppg/openwork_an_opensource_claude_cowork_alternative/)
    - Openwork will remain a true open-source solution. We're just re-licensing parts of the stack that are for enterprise.
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
  - https://github.com/different-ai/the-factory
    - OpenWork Enterprise is the OpenWork Factory superproject: one workspace for product repos, operational automation, and reusable OpenCode behaviors.
    - Build automation-first workflows, skills, and runbooks that scale beyond ad-hoc scripts.

- https://github.com/CoWork-OS/CoWork-OS /MIT/202603/ts
  - Operating System for your personal AI Agents with Security-first approach. 
  - Multi-channel (WhatsApp, Telegram, Discord, Slack, iMessage), multi-provider (Claude, GPT, Gemini, Ollama), fully self-hosted.

- https://github.com/agi-hub/AGIAgent /apache2/202604/python
  - https://agiagentonline.com/
  - 支持 Vibe Doc、Vibe Coding 和自然语言通用任务执行的智能体平台，也是一个图文文档交互式创作平台
  - 通过直观的 GUI，AGI Agent 能够与您携手完成内容的深度加工——更换图片、编辑文字、实时修改 SVG 矢量图与 Mermaid 流程图，乃至边写边运行 HTML 小程序，让每一次创作都所见即所得
  - 平台内置 40+ 工具，提供 GUI、CLI 及嵌入式运行等多种模式，
  - 全面支持 Anthropic/OpenAI 大模型接口及开源/私有化部署。
  - AGI Agent 主要用于生产力任务，如写专业文档、编写程序、整理数据等，并提供了强大的文档/图像编辑能力，包括图文文档的 Word/PDF 无损直接导出、网页小程序直接执行等；
  - 强化中文处理：对 Mermaid、SVG 图像等环节的中文进行了优化，生成的图像中文显示效果出众，界面支持中/英文切换；
  - 适配了多数国产大模型，支持各类大模型接口（streaming/non-streaming、tool-call/message、OpenAI/Claude）
  - 完全可本地化：无需依赖云服务
  - 100% 开源：提供完整的源代码，实现透明度、可定制性
  - 无需 Claude Code 作为底层：从零开始构建的独立架构
  - AGIAgent 采用 Manager + 多子 Agent 的协作架构：Manager（老板）负责发起并管理多个子 Agent（如码工、具身机器人、艺术工作者等），每个子 Agent 在独立线程中运行，可独立完成任务，也可相互协作或竞争。
  - 遵循 Plan → Act → Observe → Reflect 循环，大模型在每轮中调用工具并接收反馈，支持多轮迭代优化（默认 50 轮）。内置渐进式历史压缩机制，突破上下文长度限制，实现真正的长程任务执行。
  - 双层记忆架构: 短期、长期
  - 支持外部的 skill 文件

- https://github.com/cortask/cortask /MIT/202603/ts
  - https://www.cortask.com/
  - a self-hosted AI orchestration platform
  - It connects to multiple LLM providers, extends functionality through a skill system, and runs as a web app, desktop app, CLI, or Docker container. All data stays on your machine.
  - Channels — Connect to Telegram, Discord, and WhatsApp as a bot
  - [I built Cortask - an open source desktop app to orchestrate AI agents locally, with native Ollama support [MIT] : r/ollama _202603](https://www.reddit.com/r/ollama/comments/1s397v1/i_built_cortask_an_open_source_desktop_app_to/)
  - How did you route the LLM to different activities based on user inputs? when I say "create a blogpost on my website about birds" how the LLM knows what to do next? (for example what tools to use, what credentials, ...?)
    - The system prompt of the agent contains a list of all tools/skills available (but not like an mcp where the whole context of the tool/skill is pumped into the system prompt). Just the Name and Short description of the tool/skill is inside the system prompt. The agent then decides what skill fits the prompt of the user. Then looking up the skill in detail and work with this context. This saves a lot of tokens and is equally good from the output. 
  - So there is only 1 persistent agent? All others are ephemeral "task" agents?
    - Correct. However, I am currently testing a multi agent solution where you can create dedicated agents with their own personalities, similar to building a team within a company.

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

- https://github.com/holaboss-ai/holaboss-ai /MIT/202604/ts
  - https://holaboss.ai/
  - OSS core runtime and desktop workspace stack for Holaboss
  - Holaboss enables you to build AI workspaces that go beyond one-off task execution. Each workspace packages instructions, tools, apps, memory, and runtime state for sustained long-horizon operation. 
  - You can manage multiple workspaces in parallel, and because workspaces and workspace templates are portable, they can be packaged, shared, resumed, and reused across the Holaboss ecosystem.
  - At its core, Holaboss is built to support long-horizon agent operation. The design target is not isolated task execution, but role-holding work that has to persist across many runs inside the same workspace.
  - [I wanted Ollama to hold a job, not just answer prompts, so I built this : r/ollama _202604](https://www.reddit.com/r/ollama/comments/1sdzjy9/i_wanted_ollama_to_hold_a_job_not_just_answer/)

- https://github.com/eren726290/opencode-cowork-plugins
  - Standalone OpenCode CLI plugins for Windows. Ported from Anthropic's knowledge-work-plugins.
  - [Coworke Plugins wiped out 100 billion from SaaS. I made for opencode. : r/opencodeCLI _202603](https://www.reddit.com/r/opencodeCLI/comments/1rhrbgg/coworke_plugins_wiped_out_100_billion_from_saas_i/)

- https://github.com/rowboatlabs/rowboat /9.4kStar/apache2/202604/ts
  - https://www.rowboatlabs.com/
  - Open-source AI coworker that turns work into a knowledge graph and acts on it
  - for Mac/Windows/Linux
  - Local-first. Voice-powered.
  - https://x.com/segmenta/status/2041563979299139975
    - Memory is markdown files on specific topics: things about the user and their preferences on tasks like email drafting, presentations, etc. The assistant can save things to memory when needed and there is also a background agent that looks at chats and creates memory notes if the assistant missed anything.

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

- https://github.com/iOfficeAI/OfficeAI /NonOpen
  - https://office-ai.net/
  - Make Office/WPS more powerful and easier to use with AI, similar to Office Copilot and WordGPT
  - System Requirements: Windows 7/10/11 or later + Office 2013/2016/2019/Office 365

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
- https://github.com/google/skills /apache2
  - Agent Skills for Google products and technologies

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

- https://github.com/zai-org/GLM-skills /apache2/202604/python
  - Official skills for the GLM family of models, designed for agent architectures including Claude Code, OpenCode, OpenClaw, AutoClaw, and other AI coding agents.

- https://github.com/hewliyang/office-agents /MIT/202603/ts
  - Office Agents is a monorepo of Microsoft Office Add-ins with integrated AI chat panels. Each add-in connects to major LLM providers using your own credentials (BYOK) and can read/write documents through built-in tools, a sandboxed shell, and a virtual filesystem.
  - https://x.com/hewliyang/status/2033176726663249959
    - OpenWord v0.0.1 is out. it is competent at most text editing operations, can insert images into your doc, has vision, can add & reply to comments, and even works with Track Changes (redlining)
  - https://x.com/hewliyang/status/2030648851603087392
    - i've also renamed the open-excel repo into office-agents.
    - the SDK, which contains the agent loop, IndexedDB storage logic, etc is published to NPM. so you can build your own plugins.
    - fwiw, powerpoint is only ~2.5k LoC excluding the system prompt and the officejs .d.ts file
  - https://github.com/hewliyang/headless-word /MIT/202604/cpp
    - Word document automation via LibreOffice for headless environments.
  - https://github.com/hewliyang/headless-spreadjs /MIT/202604/ts
    - Headless Excel engine for Node.js using SpreadJS. Runs without a browser or Excel.
    - require SpreadJS license key

- https://github.com/GongRzhe/Office-Word-MCP-Server /1.8kStar/MIT/202512/python/archived
  - MCP server for creating, reading, and manipulating Microsoft Word documents. 
  - expose Word document operations as tools and resources. It serves as a bridge between AI assistants and Microsoft Word documents, allowing for document creation, content addition, formatting, and analysis.
  - [vibe coding 很爽，那么 vibe WORD 最好实践是什么？  - LINUX DO _202604](https://linux.do/t/topic/1903403)
    - 用 AionUi 也能渲染出 word 来，可惜似乎 word 的缺陷，编辑带锁，少一点即时预览的安全感

- https://github.com/sunbigfly/ppt-agent-skills /MIT/202604/python
  - PPT Agent 以严格的状态机驱动多 Agent 协作，将一句话需求输出为专业级 PPTX 文件，从根源解决传统大模型生成的幻觉、重叠与布局混乱问题。
  - 双引擎 PPTX 导出：PNG 光栅流保证跨平台 100% 视觉还原；SVG 矢量流保留字体可独立编辑。
  - Subagent 阶段隔离：Research / Outline / Style / Planning 四大阶段各自运行独立的子代理，Context 不互染。
    - 优先使用带有subagent 功能的CLI：Codex / Claude code
  - 数据层与渲染层隔离：每页先生成并由 planning_validator.py 通过校验的 JSON 合同，再驱动 HTML 渲染。写入前校验拦截所有结构错误，不进入渲染流程。
  - Visual QA 闭环：每页 HTML 构建后自动截图，由大模型进行视觉审计。检测到布局溢出后，子代理以 DOM + CSS 结构重写的方式消除冲突，而非依赖间距微调。
  - 无状态断点恢复：全流程不依赖任何进度状态文件。中断后通过扫描磁盘上已存在的产物文件（outline.txt / style.json / slide-N.png 等）自动推断恢复点。
  - [pptx agent skills 完全重构版（harness agent），佬友们所期待的 SKILL 终于完成了 - LINUX DO _202604](https://linux.do/t/topic/1882610)

- https://github.com/qWaitCrypto/AuraWork /MIT/202604/python/ts
  - A local-first multi-agent framework for office workflows — clarify requirements, plan as a DAG, execute with parallel subagents and human-in-the-loop approvals.
  - Structured before execution — every task starts with a clarified WorkSpec, not a raw prompt
  - DAG-based parallel dispatch — dependency-aware scheduling with concurrent subagents
  - Human-in-the-loop approvals — high-risk actions pause for review; low-risk actions proceed automatically
  - Office-native skills — built-in Word, Excel, PowerPoint, PDF, and browser research capabilities
    - Office/PDF files are converted to a structured intermediate representation (Markdown/JSON preserving heading levels, table boundaries, image positions), edited there, then written back to the target format for delivery.
  - CLI is the recommended and most stable entry point.
  - Web Workspace is under active development — the frontend UX and flows are not finalized; expect rough edges.

- https://github.com/yeap531/word-format-skill /apache2/202604/python
  - skill：把一份参考 Word (.docx) 的排版样式（字体 / 字号 / 缩进 / 行距 / 对齐 / 页面设置 / 样式表 / 主题 / 页眉页脚）视觉一致地复刻到新内容上。
  - 仅在 macOS 工作（依赖 Microsoft Word + 浏览器 + System Events 的 UI 自动化）。
  - [100%复刻word模版的skill - LINUX DO _202604](https://linux.do/t/topic/2068329)

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

- https://github.com/IUnlimit/opennews /MIT/202604/python/vue
  - https://opennews.top/
  - Real-time financial news knowledge graph and impact scoring system.
  - a LangGraph-based pipeline for financial news analysis. It ingests multi-source news, runs NLP and impact scoring, then persists results to PostgreSQL and Neo4j, with a built-in web dashboard for real-time filtering and inspection.
  - Multi-source ingestion (NewsNow API + JSONL seeds)
  - FinBERT embedding + online topic clustering
  - DeBERTa zero-shot classification
  - DK-CoT impact score (0-100)
  - Redis temporal memory (rolling window)
  - [[开源]实时金融新闻影响评分网站（带一键分享api）  - LINUX DO _202604](https://linux.do/t/topic/1890565)

- https://github.com/wbh604/UZI-Skill /MIT/202604/python
  - 游资（UZI）Skills — 51位投资大佬帮你看盘 · 22维数据 × 180条量化规则 × 17种机构分析方法 · A股/港股/美股
  - [今年A股收益率42.83%我只靠他？游资Skill！让格雷厄姆、陈小群同台竞技，帮你分析个股 - LINUX DO _202604](https://linux.do/t/topic/1981105)

- https://github.com/TraderAlice/OpenAlice /AGPL/202604/python/ts
  - https://openalice.ai/
  - Your one-person Wall Street. An AI trading agent covering equities, crypto, commodities, forex, and macro — from research through position entry, ongoing management, to exit.

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

## data

- https://github.com/Rohithgilla12/data-peek /1.6kStar/MIT/202604/ts
  - https://www.datapeek.dev/
  - A minimal, fast, database client desktop application. 
  - minimal, fast SQL client desktop application with AI-powered querying.
  - Supports PostgreSQL, MySQL, Microsoft SQL Server, and SQLite.
  - SSH Tunnels - Connect securely through bastion hosts with password or key auth

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

- https://github.com/Lianues/Iris /GPL/202603/ts/vue
  - 一个面向多平台的智能代理程序。支持 Console、Web、Discord、Telegram、微信、企业微信、飞书、QQ 等平台，支持工具调用、会话存储、图片输入、OCR 回退、Computer Use、MCP 和记忆能力。
  - [IrisAgent，将coding，claw，web，mcp，skill，多agent，computer use等全部集成的agent项目，支持飞书，vx，终端，网页等多个平台同时使用，支持一键安装，替代openclaw  - LINUX DO _202603](https://linux.do/t/topic/1839669)
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
# image 
- https://github.com/dwzhu-pku/PaperBanana /6.2kStar/apache2/202604/python/js
  - https://dwzhu-pku.github.io/PaperBanana/
  - PaperBanana: Automating Academic Illustration For AI Scientists
  - PaperBanana is a reference-driven multi-agent framework for automated academic illustration generation.
  - Acting like a creative team of specialized agents: Retriever, Planner, Stylist, Visualizer, and Critic agents
  - https://github.com/917940234/PaperBanana-CN
    - 持各类中转站的科研生图工具（中文友好，包含最新gpt-image-2）
    - [[开源自荐] PaperBanana-CN：支持各类中转站的科研生图工具（中文友好，包含最新gpt-image-2） - LINUX DO _202605](https://linux.do/t/topic/2098853)
# video/mtv
- https://github.com/zapdos-labs/unblink /182Star/AGPL/202512/ts
  - Unblink is a camera monitoring application that runs AI vision models on your camera streams in real-time
  - Object detection
  - Intelligent search across your video feeds.

- https://github.com/waoowaooAI/waoowaoo /MIT/202602/ts
  - 首家工业级全流程可控协作式专业AIagent影视生产平台，从短片到漫剧到真人级影视剧一站搞定，采用好莱坞专业制作团队思路，让你拥有虚拟制片场
  - [免费开源！已经盈利的AI影视/短剧agent制作系统 waoowaoo _202602](https://linux.do/t/topic/1666777)

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

- https://github.com/Stonewuu/ai-fusion-video /MIT/202604/java/ts
  - [基于 Agent 的AI短剧漫剧创作平台：融光 - LINUX DO _202604](https://linux.do/t/topic/1986023)
  - 搓了一个Java 技术栈基于 Agent 的AI短剧漫剧创作平台
  - 整个AI创作过程都是基于agent运行的，为此写了30多个 tools（数量确实太多了，后续考虑怎么合并一下）
  - 分镜编辑则参考了影视飓风的 闪电分镜（低配版哈哈哈，未来争取融入协作功能）

- https://github.com/liangdabiao/Seedance2-Storyboard-Generator /202603
  - [为什么 -怎样做 -经验分享Seedance2-Storyboard-Generator ](https://linux.do/t/topic/1985955)
  - seedance效果很好，而且功能已经非常强大，但是我看了市面上的大部分开源项目，都是用传统那种分镜和首尾帧方式，还有就是大量强调一致性，其实seedance根本不需要这些，seedance需要的其实是文学，所以我就做了这个开源项目。

- [PDF to Brainrot | MemenomeLM](https://www.memenome.gg/)
  - 把 PDF 转化为易上瘾的视频
  - 通过 AI 技术将传统的 PDF 学习材料转换为更生动有趣的视频形式, 既保留了学习内容的专业性, 又强调提高效率、改善学习体验和趣味性, 网站显示已经有超过 10w 学生使用
  - 用 AI 改造成交互式学习的过程, 交互视频、AI 和真人交互都可以
  - https://x.com/0xPaulius/status/1852697757124845684
    - Been using this to post automated tiktoks on the latest research papers, its actually getting pretty good traction

- https://github.com/actionow-ai/actionow /apache2+LOGO/202604/java/ts
  - 从剧本到分镜，从角色到成片，Actionow 把"开拍 · 此刻"变成创意团队。
  - 触手可及的工程化工作台——智能体驱动，开箱即接最新模型，可代码级控制、可私有化部署
  - [【开源·Actionow】【演示站上线】包含Agent辅助·团队协作·多租户·积分系统的 AI 影视创作SaaS平台 - LINUX DO _202604](https://linux.do/t/topic/2034482)

- https://github.com/hjxwz123/flowmusegallery
  - [[开源]FlowMuse 本地的AI 图片与视频创作工作台 - LINUX DO _202604](https://linux.do/t/topic/2083254)
  - 使用codex+Gemini vibe coding了一个本地的ai创作平台，接入API（官方或者公益）即可使用，支持Gemini，GPT生图格式以及seedance2.0、最新的HappyHorse 1.0视频模型，接入火山/阿里百炼的key即可使用。
  - 本地的 AI 图片与视频创作工作台，适合把日常的提示词、生成任务、项目素材、对话式创作流程和桌面应用集中管理起来。它支持浏览器服务模式，也支持 Electron 桌面端打包，数据默认使用 SQLite 保存，生成结果和上传资源默认落在本地，比较适合个人创作者、独立开发者或需要沉淀项目素材的人使用。
  - 目前内置了 NanoBanana、Midjourney、GPT Image、火山豆包、通义千问、通义万相等媒体渠道配置入口
  - 另外对于视频生成方面，由于我不是专业的工作者，只是按照我的理解+ai的理解进行编写的，所以对于视频生来说可能略微不足，还请各位佬提提意见。

## vid2txt

- https://github.com/maskgo68/YPBrief
  - [【开源】YPBrief，自托管 YouTube 播客与长视频简报工具，支持docker、GitHub Action部署 - LINUX DO _202604](https://linux.do/t/topic/2086869)

## subtitle

- https://github.com/Nutlope/ai-subtitles /MIT/202604/ts
  - https://www.usesubstudio.com/
  - Upload a video or paste a direct media link to instantly create accurate, timed subtitles.
  - https://x.com/nutlope/status/2041199444855492790
    - Powered by Whisper on @togethercompute and @FFmpeg via fluent-ffmpeg.

- https://github.com/timminator/VideOCR /MIT/202604/python
  - Extract hardcoded subtitles from videos via a simple GUI using machine learning. Supports 200+ languages.
  - VideOCR supports both 100% local processing utilizing the PaddleOCR engine, as well as a hybrid cloud-based approach using Google Lens for highly accurate text recognition. Everything can be easily configured via a few clicks.
  - This repository also provides a version of VideOCR that can be used from the command line in combination with the supported OCR engines.
  - https://github.com/devmaxxing/videocr-PaddleOCR /legacy
# audio
- https://github.com/Deep-unlearning/smol-audio /apache2/202604/jupyter
  - Practical, Colab-friendly notebooks for fine-tuning and running audio AI models
  - Practical notebooks for shrinking, optimizing, and customizing audio AI models with the Hugging Face ecosystem.
  - https://x.com/Tu7uruu/status/2048768154818801956
    - A collection of notebooks & scripts to build on cutting-edge local audio models
    - Fine-tune Whisper / Parakeet / Voxtral / Granite Speech
# more
