---
title: lib-ide-app-examples-coding-popular
tags: [coding, examples, ide, large-language-model, vscode-ext]
created: 2025-12-11T18:09:43.379Z
modified: 2025-12-11T18:10:23.710Z
---

# lib-ide-app-examples-coding-popular

# guide
- tips
  - 对于模型厂商推出的cli-coding，会尽可能多的使用token来实现更好的效果
    - 对于类似cursor应用层推出的coding产品，会偏向减少token用量来降低成本
  - cli的实现经常与模型厂商自己的sdk紧密结合，但只要兼容openai的协议就可通用，目前不通用的是gemini-cli, 可考虑开发patch
  - ui类型的工具逐渐开始支持cli, 如cline-cli
  - cli类型的工具逐渐开始支持web, 如codex/claude
# popular
- https://github.com/oraios/serena /19.6kStar/MIT/202602/python
  - https://oraios.github.io/serena
  - A powerful coding agent toolkit providing semantic retrieval and editing capabilities (MCP server & other integrations)
  - Serena is a powerful coding agent toolkit capable of turning an LLM into a fully-featured agent that works directly on your codebase.
  - Unlike most other tools, it is not tied to an LLM, framework or an interface
  - Serena provides essential semantic code retrieval and editing tools that are akin to an IDE's capabilities
  - You can think of Serena as providing IDE-like tools to your LLM/coding agent. With it, the agent no longer needs to read entire files, perform grep-like searches or string replacements to find and edit the right code. Instead, it can use code centered tools like find_symbol, find_referencing_symbols and insert_after_symbol.
  - Memory & Knowledge System - **Markdown-based storage** in `.serena/memories/` directories
  - Serena can be integrated with an LLM in several ways: 
    - by MCP. Serena provides an MCP server for integration
    - by incorporating Serena's tools into an agent framework of your choice. Serena's tool implementation is decoupled from the framework-specific code and can thus easily be adapted to any agent framework.
  - Serena incorporates a powerful abstraction layer for the integration of language servers that implement LSP
    - With Serena's LSP library, we provide support for over 30 programming languages
    - All the language servers that we use through Solid-LSP.
  - [RAG Search for Memories _202506](https://github.com/oraios/serena/issues/205)
    - Would love to be able to use memory feature to the maximum. Can we save our memories with specialized RAG technique to be able to automatically load relevant memories?
    - Using embeddings will significantly increase the complexity and I don't see any benefit to it. Claude already loads the right memory from its name, and for an embedding based approach one can simply combine Serena with a dedicated embedding MCP and disable Serena's memory tools.
    - Sorry, that's not a feature for this project.
  - [[Feature] Ability to launch serena as ACP server _202509](https://github.com/oraios/serena/issues/644)
    - We already have `SerenaAgent` as dedicated abstraction which exposes all capabilities of serena. It should be fairly straightforward to use it in any connection layer, including ACP.
  - 📡 [Better integration with major agentic CLIs and IDEs _202511](https://github.com/oraios/serena/issues/757)
    - 已支持 claude-code, codex, vscode

- https://github.com/cline/cline /50kStar/apache2/202509/ts/cli使用go实现
  - https://docs.cline.bot/
  - Meet Cline, an AI assistant that can use your CLI aNd Editor.
  - Autonomous coding agent right in your IDE, capable of creating/editing files, executing commands, using the browser, and more with your permission every step of the way.
  - Unlike autocomplete tools, Cline is a true coding agent that can understand entire codebases, plan complex changes, and execute multi-step tasks.
  - 100% Open Source - Every line of code on GitHub. 
  - features
    - Use any API and Model
    - Create and Edit Files with diff view
    - Run Commands in Terminal for VSCode v1.93+
    - Add Context: @file, @url, @problems
    - Checkpoints: Compare and Restore, a snapshot of your workspace at each step
    - Use the Browser with Claude Sonnet's new Computer Use capability
    - mapSelection
    - Auto Approve menu lets you set fine-grained permissions on
    - 🏠 Plan & Act modes represent Cline’s approach to structured AI development, emphasizing thoughtful planning before implementation. 
    - Workflows: a series of steps to guide Cline through a repetitive set of tasks
    - Automatic Context Summarization: When your conversation approaches the model’s context window limit, Cline automatically summarizes it to free up space and keep working
  - https://github.com/cline/cline/tree/main/cli /apache2/go
    - https://docs.cline.bot/cline-cli/overview
    - coding agent CLI - capable of creating/editing files, running commands, using the browser, and more
    - Multi-Model Support: Works with Anthropic Claude, OpenAI GPT, and other AI models
    - 依赖grpc、better-sqlite3

- https://github.com/RooCodeInc/Roo-Code /19.2kStar/apache2/202509/ts
  - https://roocode.com/
  - https://docs.roocode.com/
  - an AI-powered autonomous coding agent that lives in your editor.
  - features
    - 🏠 Multiple Modes: Code, Architect/plan, ask, Debug, Custom Modes
    - Read and write files in your project
    - Execute commands in your VS Code terminal
    - Control a web browser
    - MCP with Roo Code Marketplace
    - Message Queueing: Keep your workflow uninterrupted with message queueing, send multiple messages while Roo is working, and they'll be processed sequentially 
    - API Configuration Profiles allow you to create and switch between different sets of AI settings
    - Boomerang Tasks (also known as subtasks or task orchestration) allow you to break down complex projects into smaller, manageable pieces
    - Code Actions provide instant access to Roo Code's AI assistance directly within your code editor through VSCode's lightbulb (quick fix) system
    - Codebase Indexing transforms how Roo Code understands your project by creating a semantic search index using AI embeddings.
    - The diagnostics feature seamlessly integrates with VSCode's diagnostic system to provide context-aware assistance for code issues.
    - Fast Edits (using the "Enable editing through diffs" setting) is enabled by default in Roo Code.
    - Model Temperature is a setting (usually between 0.0 and 2.0) that controls how random or predictable the AI's output is. lower values make the output more focused and consistent, while higher values encourage more creativity and variation.
    - Concurrent File Edits(AKA Multi-File Edits) allows Roo to modify multiple files in your workspace within a single request
    - "Background Editing" disables automatic diff view displays when Roo Code edits files.
    - Image Generation: Roo sends your prompt (and optionally an existing image) to an image-capable model through OpenRouter.

- https://github.com/Kilo-Org/kilocode /9.7kStar/apache2/202509/ts
  - Open Source AI coding assistant for planning, building, and fixing code. 
  - We frequently merge features from open-source projects like Roo Code and Cline, while building our own vision. 
  - Automate the browser

- https://github.com/kodu-ai/claude-coder /5.3kStar/AGPL/202504/ts/inactive
  - https://www.kodu.ai/
  - Kodu is an autonomous coding agent that lives in your IDE
  - It's a VS Code extension that adapts to your skill level, helping you bring ideas to life faster than ever before. 

- https://github.com/nutlope/llamacoder /6.8kStar/MIT/202512/ts
  - https://www.llamacoder.io/
  - open source Claude Artifacts – generate small apps with one prompt. 
  - Powered by Llama 3 405B & Together.ai.
  - Llama 3.1 405B from Meta for the LLM
  - Together AI for LLM inference
  - Sandpack for the code sandbox
  - Next.js app router with Tailwind
  - Helicone for observability
  - [Generate an entire app from a prompt using Together AI’s LlamaCoder _20240918](https://ai.meta.com/blog/together-ai-llamacoder/)

- https://github.com/artmoskvin/hide /MIT/202408/go
  - https://hide.sh/
  - Headless IDE for Coding Agents
  - Hide provides containerized development environments for codebases and exposes APIs for agents to interact with them. When given a code repo, Hide spins up a devcontainer, installs the dependencies and provides APIs for codebase interaction. Developers can craft custom toolkits using Hide APIs or use Hide's pre-built toolkits for popular frameworks like Langchain.

- https://github.com/TabbyML/tabby /apache2/202408/rust
  - https://tabbyml.github.io/tabby
  - Self-hosted AI coding assistant. 
  - An opensource / on-prem alternative to GitHub Copilot.
  - Self-contained, with no need for a DBMS or cloud service
  - OpenAPI interface, easy to integrate with existing infrastructure (e.g Cloud IDE).
  - Tabby 是一个自我托管的 #GitHub #Copliot 开源替代品，自带可视化界面与 #OpenAPI 接口，还支持消费者级别的 #GPU，具有 FP-16 重量加载和各种优化功能，提供了 #Docker 镜像

- https://github.com/meltylabs/melty /MIT/202409/ts
  - https://docs.google.com/forms/d/e/1FAIpQLSc6uBe0ea26q7Iq0Co_q5fjW2nypUl8G_Is5M_6t8n7wZHuPA/viewform
  - Melty, an open source AI code editor for 10x engineers
  - Melty is the first AI code editor that's aware of what you're doing from the terminal to GitHub, and collaborates with you to write production-ready code
  - 两位来自 Replicate 和 Netflix 的工程师开发了 Melty，第一个能够在多个文件中进行大规模修改并与整个工作流程集成的 AI 代码编辑器。

- https://github.com/SilasMarvin/lsp-ai /MIT/202408/rust
  - LSP-AI is an open-source language server that serves as a backend for AI-powered functionality, designed to assist and empower software engineers, not replace them.
  - It offers features like in-editor chatting with LLMs and code completions. Because it is a language server, it works with any editor that has LSP support.
  - In-Editor Chatting
  - Note that speed for completions is entirely dependent on the backend being used. For the fastest completions we recommend using either a small local model or Groq

- https://github.com/morph-labs/rift /apache2/202310/python/inactive
  - https://morph.so/
  - Rift: an AI-native language server for your personal AI software engineer
  - The Rift Code Engine implements an AI-native extension of the language server protocol. The Rift VSCode extension implements a client and end-user interface which is the first step into that future.

- https://github.com/block/goose /apache2/202503/rust/ts
  - https://block.github.io/goose/
  - a local, extensible, open source AI agent that automates engineering tasks
  - 提供了cli/desktop-gui
  - an open source, extensible AI agent that goes beyond code suggestions - install, execute, edit, and test with any LLM
  - goose is your on-machine AI agent, capable of automating complex development tasks from start to finish. More than just code suggestions, goose can build entire projects from scratch, write and execute code, debug failures, orchestrate workflows, and interact with external APIs - autonomously.
  - Designed for maximum flexibility, goose works with any LLM and seamlessly integrates with MCP-enabled APIs, making it the ultimate AI-powered assistant

- https://github.com/covibes/zeroshot /939Star/MIT/202601/js
  - https://covibes.ai/
  - Your autonomous engineering team in a CLI. Point Zeroshot at an issue, walk away, and return to production-grade code. Supports Claude Code, OpenAI Codex, OpenCode, and Gemini CLI.
# terminal-ai

## claude-cli

- https://github.com/anthropics/claude-code /202506/NonOpen
  - https://docs.anthropic.com/s/claude-code
  - 📌 an agentic coding tool that lives in your terminal, understands your codebase, and helps you code faster
  - [open source? _202502](https://github.com/anthropics/claude-code/issues/59)
    - We currently don't have plans to open source it.
  - [[DOCS] Open Source Licensing ](https://github.com/anthropics/claude-code/issues/8517)
    - The Claude Code binaries distributed by Anthropic contain Open Source software.
    - Some of that software is made available to Anthropic under the terms of the Apache-2.0 license, however there does not appear to be a notice of this in the distributed files, nor on the Claude Code documentation website

- https://github.com/iOfficeAI/AionUi /3kStar/apache2/202512/ts
  - https://www.aionui.com/
  - https://github.com/iOfficeAI/AionUi/wiki
  - open-source GUI app for Gemini CLI — Better Chat UI, multi-agent support, multi-LLMs & apikey polling, Workspace Management, AI image editing & more
  - While the official Gemini CLI is powerful, its command-line interface has limitations for daily use. 
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
  - [feat: Implement ACP integration with improved Gemini authentication _20250903](https://github.com/iOfficeAI/AionUi/commit/23b3c4fae1af1c763f7ca41957ec141df47ad3a2)
    - Add comprehensive ACP (Agent Client Protocol) support for Claude and Gemini backends
  - 📡 roadmap
    - 可结合下面async-code和其他ui的优点, 优化 background-agents 后台任务/并发任务
  - [AionUi V1.7.4 更新：兼容了Newapi（Cowork开源版可以用公益站/中转站了 _202601](https://linux.do/t/topic/1508016)
    - 测了一下部分中转站已经通了，基于newapi的公益站也通了。配置在“自定义模型平台”上即可。
    - 之前aionui直接配置中转站时会被中转站拦截请求。需要带上user-agent才能通信。他们要在标准的OpanAI协议基础上带上defaultHeader才可以识别请求，之前AionUi没做这个。
    - 支持多key轮询, 同一个url下的多key轮询
- https://github.com/RAIT-09/obsidian-agent-client /127Star/apache2/202512/ts
  - Bring AI agents into Obsidian via Agent Client Protocol (ACP), such as Claude Code, Codex and Gemini CLI.
  - This plugin lets you chat with Claude Code, Codex, Gemini CLI, and other AI agents right from your vault.
  - Multi-Agent Support: Switch between Claude Code, Codex, Gemini CLI, and custom agents
  - Note Mention Support: @notename to reference specific notes
  - Use / commands to browse and trigger actions provided by your current agent
  - Permission Management: Fine-grained control over agent actions

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

- https://github.com/J3n5en/EnsoAI /MIT/202512/ts
  - https://enso.j3.do/
  - 无缝切换 Claude、Codex、Gemini 或本地 LLM。每个 Worktree 都有独立的持久化 AI 会话。 你也可以通过指定 CLI 命令来添加自定义 Agent。
  - 专注于 Git Worktree + AI Agent 的协作场景。它不是要替代 VS Code 或 Cursor，而是作为一个轻量级的工作空间管理器
  - 内置 可视化 Git 面板
  - 基于 Monaco 构建的轻量级编辑器
  - 内置专业的三栏合并编辑器。
  - 毫秒级创建与切换 Git Worktree
  - 框架: Electron + React 19 
  - 终端: xterm.js + node-pty
  - Git: simple-git
  - 数据库: better-sqlite3
  - 为什么使用官方 CLI 而不使用 ACP？
    - 虽然 ACP 能够统一不同 Agent 的核心能力，但是也仅限于核心能力缺失了很多功能。切换不同 Agent 的场景其实并不多而且不同 Agent 的 CLI 核心功能都相似。所以我们认为对于有经验的开发者各 CLI 更具有生产力。

- https://github.com/21st-dev/1code /4.7kStar/apache2/202601/ts
  - https://1code.dev/
  - Better UI app for running code agents in parallel (ClaudeCode, OpenCode, Codex)
  - Best UI for Claude Code with local and remote agent execution.
  - 1Code is an open-source app that provides a calm, visual interface for Claude Code. It lets you run multiple coding sessions in parallel, track progress visually, and manage your AI-assisted development workflow more effectively.
  - fully open source. 
  - Note: Currently tested on macOS and Linux. Windows support is experimental and may have issues.
  - built for coding. It has a full terminal, GitHub integration, visual diff previews, and worktree management. 
  - Git Worktree Isolation - Each chat session runs in its own isolated worktree
  - [[Question] Does this usage violate Anthropic’s ToS? _202601](https://github.com/21st-dev/1code/issues/8)
    - 1Code uses the official Claude Code SDK which wraps the Claude Code binary. This is the official way to build on top of Claude Code.
    - Some other tools (like OpenCode) made direct API calls while impersonating Claude Code - that approach got banned. We're not doing that.

- https://github.com/pedramamini/Maestro /AGPL/202601/ts
  - https://runmaestro.ai/
  - a cross-platform desktop app for orchestrating your fleet of AI agents and projects.
  - It's a high-velocity solution for hackers who are juggling multiple projects in parallel.
  - Run multiple agents in parallel with a Linear/Superhuman-level responsive interface. 
  - Currently supporting Claude Code, OpenAI Codex, and OpenCode with plans for additional agentic coding tools (Aider, Gemini CLI, Qwen3 Coder) based on user demand.
  - Git Worktrees - Run AI agents in parallel on isolated branches
  - File-system-based task runner that batch-processes markdown checklists through AI agents. Create playbooks for repeatable workflows
  - Mobile Remote Control - Built-in web server with QR code access.
  - Full CLI (maestro-cli) for headless operation.
  - Multi-Agent Management - Run unlimited agents and terminal sessions in parallel. 
  - Message Queueing - Queue messages while AI is busy; they're sent automatically when the agent becomes ready. Never lose a thought.

- https://github.com/coder/mux /774Star/AGPL/202512/ts
  - https://mux.coder.com/
  - A desktop app for isolated, parallel agentic development
  - Isolated workspaces: local directory, worktree, ssh
  - models: openrouter, Ollama
  - mux has a custom agent loop but much of the core UX is inspired by Claude Code.

- https://github.com/openkursar/hello-halo /MIT/202601/ts
  - The Missing UI for Claude Code
  - open-source desktop client that makes Claude Code's power accessible to everyone. No terminal, ever.
  - https://x.com/FlynnWayne_Wang/status/2011079825956749365
    - Remote access from phone/tablet/any browser
    - Built-in AI Browser for web automation
    - 100% of the code after v1 was written by Halo itself

- https://github.com/lukilabs/craft-agents-oss /apache2/202601/ts
  - https://x.com/balintorosz/status/2013302678105796764
  - TL; DR - We've released Craft Agents as an open source product - it  showcases our take on how to effectively work with agents (Especially Claude Code). 
  - It enables intuitive multitasking, no-fluff connection to any API or Service, sharing sessions, and a more document (vs code) centric workflow - in a beautiful and fluid UI.
  - It leans on Claude Code through the Claude Agent SDK - follow what we found great, and improves areas where we've desired improvements.
  - We ourselves are building Craft Agents with Craft Agents only - no code editors - so really, any customisation is just a prompt away.
  - We built Craft Agents because we wanted a better, more opinionated (and preferably non-CLI way) of working with the most powerful agents in the world. 

- https://github.com/fengshao1227/ccg-workflow /MIT/202601/js
  - CCG v3.0: Claude Code 编排三 CLI 协作
  - v3.0.0 重大更新：从 Python 脚本进化为 npm 包，三 CLI 协作时代正式开启！
  - 从 Python 脚本重构为 TypeScript + unbuild 构建系统
  - Claude Code 是主对话，负责编排整个工作流、做最终决策、实施代码
    - Codex/Gemini/Claude 子进程 通过 codeagent-wrapper 调用，生成原型代码
    - 零写入权限：子进程只能返回 Unified Diff Patch，不能直接修改文件
    - 子进程输出视为"脏原型"，需经 Claude Code 重构为生产级代码
  - Claude Code CLI 作为主导编排者
    - Codex CLI 负责后端原型生成
    - Gemini CLI 负责前端原型生成
    - Claude CLI 子进程负责全栈整合
  - 支持 smart/parallel/sequential 三种协作模式
  - [【开源】CCG v3.0: Claude Code 编排三 CLI 协作 | Codex + Gemini + Claude ](https://linux.do/t/topic/1405588)
    - 之前一直在用 孙佬 @DaiSun 的 Skills 仓库，用着用着就想搞点定制化的东西。比如给 Codex 和 Gemini 配上专家角色提示词，让它们不再是无头苍蝇；再比如把 zcf 佬的 Git 工具也缝进来，一站式解决开发需求。于是就有了这个 CCG（Claude Code + Codex + Gemini）项目 

- https://github.com/ObservedObserver/async-code /apache2/202508/python/ts/inactive
  - Use Claude Code / CodeX CLI to perform multiple tasks in parallel with a Codex-style UI.
  - A code agent task management system that provides parallel execution of AI-powered coding tasks. 
  - Users can run multiple Claude Code agents simultaneously through a Codex-style web interface, with support for different agents for comparison and evaluation.
  - Multi-Agent Support: Run Claude Code and other AI agents in parallel
  - Parallel Task Management: Execute multiple coding tasks simultaneously
  - Git Integration: Automatic repository cloning, commits, and PR creation
  - Backend: Python Flask API with Docker orchestration

- https://github.com/slopus/happy /5kStar/MIT/202512/ts/tauri
  - https://happy.engineering/
  - Mobile and Web client for Codex and Claude Code, with realtime voice, encryption and fully featured
  - On your computer, run happy instead of claude or happy codex instead of codex to start your AI through our wrapper. When you want to control your coding agent from your phone, it restarts the session in remote mode.
  - Switch devices instantly - Take control from phone or desktop with one keypress
  - Open source - Audit the code yourself. No telemetry, no tracking
  - https://github.com/slopus/happy-server /MIT/202512/ts
    - Minimal backend for open-source end-to-end encrypted Claude Code clients.
    - Only essential features for secure sync, nothing more
    - The server stores encrypted data but has no ability to decrypt it
    - WebSocket-based synchronization across all your devices
    - Built to scale horizontally when needed
    - 待确定, 是否支持区分不同用户的不同客户端
    - How It Works: Your Claude Code clients generate encryption keys locally and use Happy Server as a secure relay. Messages are end-to-end encrypted before leaving your device. The server's job is simple: store encrypted blobs and sync them between your devices in real-time.

- https://github.com/siteboon/claudecodeui /5kStar/GPL/202512/js
  - https://cloudcli.ai/
  - A desktop and mobile UI for Claude Code, and Cursor CLI
  - Use Claude Code or Cursor CLI on mobile and web with Claude Code UI. 
  - Claude Code UI free open source webui/GUI that helps you manage your Claude Code session and projects remotely
  - You can use it locally or remotely to view your active projects and sessions in Claude Code or Cursor and make changes to them
  - Supports models including Claude Sonnet 4, Opus 4.1, and GPT-5
  - Direct access to Claude Code or Cursor CLI through built-in shell functionality
  - Session Management - Resume conversations, manage multiple sessions, and track history
  - File Explorer - Interactive file tree with syntax highlighting and live editing
  - Git Explorer - View, stage and commit your changes. You can also switch branches
  - 🐛 [Feature Request: Support for Claude Code Proxy Tools (CCR Integration) _202511](https://github.com/siteboon/claudecodeui/issues/234)
    - I'm using claude-code-router (CCR), a proxy tool that routes Claude Code requests to different AI models and providers (Gemini, DeepSeek, Ollama, etc.). However, claudecodeui currently doesn't support integration with CCR due to its architecture.
    - Since the main chat functionality uses the SDK, it bypasses the claude CLI and connects directly to Anthropic's API, making it impossible to use proxy tools like CCR that work by intercepting CLI calls.
  - [How feasible is it to add support for other CLI agents like Gemini? _202507](https://github.com/siteboon/claudecodeui/discussions/13)
    - Gemini CLI is there yet. It's important to be able to work in non interactive mode for the Chat function to work.

- https://github.com/milisp/codexia /335Star/MIT > AGPL/202601/ts/tauri
  - https://github.com/codexia-team/codexia /renamed
  - ~~A powerful GUI and Toolkit for Codex CLI~~
  - A powerfull GUI/IDE and Toolkit for Codex CLI + Claude Code. FileTree + prompt notepad + git worktree and more
  - fork chat, file-tree integration, notepad, git diff, build-in pdf csv/xlsx viewer, and more.
  - [We built Codexia - A free and open-source powerful GUI app and Toolkit for Codex CLI : r/ChatGPTCoding _202511](https://www.reddit.com/r/ChatGPTCoding/comments/1op0yr6/we_built_codexia_a_free_and_opensource_powerful/)
  - Is there git worktree integration?
    - No, but in my plan
  - https://github.com/milisp/codexia-zen
    - GUI for OpenAI Codex CLI, minimalist design

- https://github.com/winfunc/opcode /19.1kStar/AGPL/202510/ts/rust/tauri/inactive
  - https://opcode.sh/
  - A powerful GUI app and Toolkit for Claude Code
  - Create custom agents, manage interactive Claude Code sessions, run secure background agents, and more.
  - Session History: View and resume past coding sessions with full context
  - Background Execution: Run agents in separate processes for non-blocking operations

- https://github.com/stravu/crystal /2.9kStar/MIT/202512/ts/inactive
  - a new graphical interface to manage Claude Code sessions. 
  - Run multiple Codex and Claude Code AI sessions in parallel git worktrees
  - We built this internally to help speed up the development of Stravu, and it was so helpful we decided we had to share it
  - Create sessions from prompts, each in an isolated git worktree: Each session operates in its own git worktree
  - Monitor all your Claude Code sessions from a unified interface
  - [Crystal: Supercharge Your Development with Multi-Session Claude Code Management](https://nimbalyst.com/blog/crystal-supercharge-your-development-with-multi-session-claude-code-management)

- https://github.com/opactorai/Claudable /3.4kStar/MIT/202512/ts/electron/inactive
  - an open-source web builder that leverages local CLI agents, such as Claude Code, Codex, Gemini CLI, Qwen Code, and Cursor Agent, to build and deploy products effortlessly.
  - Instant Preview: See your changes immediately with hot-reload as AI builds your app
  - Zero Setup, Instant Launch: No complex sandboxes, no API key, no database headaches - just start building immediately
  - Deploy to Vercel: Push your app live with a single click
  - Supabase Database: Connect production PostgreSQL with authentication ready to use
  - Desktop App: Available as Electron desktop application for Mac, Windows, and Linux

- https://github.com/d-kimuson/claude-code-viewer /MIT/202512/ts
  - A full-featured web-based Claude Code client that provides complete interactive functionality for managing Claude Code projects
  - View Claude Code session logs in real-time through the web UI. Supports historical logs as it uses standard Claude Code logs (~/.claude/projects/...) as the data source
  - Built-in Git Diff Viewer lets you review all changes directly within Claude Code Viewer
  - What Makes Claude Code Viewer Different: specifically designed as a session log viewer

- https://github.com/sugyan/claude-code-webui /MIT/202509/ts/inactive
  - A modern web interface for Claude Code CLI - Transform your command-line coding experience into an intuitive web-based chat interface
  - Secure tool access with granular permission controls and clear approval workflow
  - Browse and restore previous chat sessions

- https://github.com/wbopan/cui /1kStar/apache2/202510/ts
  - A web UI for Claude Code agents
  - Start the server and access your agents anywhere in your browser. 
  - Common Agent UI is powered by Claude Code SDK and supports all kind of LLMs with the most powerful agentic tools.
  - Parallel Background Agents: Stream multiple sessions simultaneously

- https://github.com/opslane/opslane /MIT/202511/rust/ts/tauri/docker
  - Desktop app for managing multiple Claude Code sessions in parallel.
  - Work on multiple projects simultaneously with isolated sessions
  - Docker Isolation - Each session runs in its own container with resource limits
    - claude reads files, edits code, runs commands in isolated container
    - Sync to Local - Apply container changes to your local repository when ready
  - Live Diff Viewer - Review all file changes with syntax highlighting before applying
  - Optional bidirectional file synchronization between container and local repo

- https://github.com/JessyTsui/Claude-Code-Remote /MIT/202512/js
  - Control Claude Code remotely via multiple messaging platforms.
- https://github.com/preset-io/agor /BSL/202512/ts  
  - Agor is a multiplayer spatial canvas where you coordinate multiple AI coding assistants on parallel tasks, with GitHub-linked worktrees, automated workflow zones, and isolated test environments—all running simultaneously.

- https://github.com/RVCA212/claude-code-ui /GPL/202508/js/inactive
  - an Electron-based desktop application for interacting with Claude Code in a 'Cursor' style view with features such as checkpointing.
  - Native desktop application for macOS, Windows, and Linux
  - Checkpoint system to undo changes
  - Parrlel runs support
  - Multi-process architecture with secure IPC (parralel claude code runs)

- https://github.com/DevAgentForge/claude-code-webui /202601/ts
  - https://x.com/austinit/status/2009824160680169511
  - Claude Agent WebUI 才比较准确。因为它是基于Claude Agent SDK 构建的
  - 使用 regex 搜索文件内容
  - WebFetch - 获取和解析网页

- https://github.com/shareAI-lab/Kode /2.2kStar/apache2/202509/ts
  - Like Claude Code, but Koding with DeepSeek V3.1, Kimi2, GLM4.5, Qwen Coder etc.
  - Kode proudly supports the `AGENTS.md` standard protocol initiated by OpenAI - a simple, open format for guiding programming agents that's used by 20k+ open source projects.
  - Subagent System - Advanced agent delegation and task orchestration
  - Security Notice: Kode runs in YOLO mode by default (equivalent to Claude's `--dangerously-skip-permissions` flag), bypassing all permission checks for maximum productivity.
  - https://github.com/shareAI-lab/analysis_claude_code
    - 本仓库包含对 Claude Code v1.0.33 进行逆向工程的完整研究和分析资料。包括对混淆源代码的深度技术分析、系统架构，以及重构 Claude Code agent 系统的实现蓝图。
    - 源复现版会在这里发布 Kode
    - 项目包含超过 50,000 行混淆代码 的分析结果，覆盖了从UI交互到Agent核心引擎的完整技术栈

- https://github.com/dzhng/claude-agent-server /202511/ts/e2b
  - A WebSocket server that wraps the Claude Agent SDK, allowing real-time bidirectional communication with Claude through WebSockets. 
  - Deploy it as an E2B sandbox and connect via the TypeScript client library.

- https://github.com/musistudio/claude-code-router /23.3kStar/MIT/202512/ts
  - Use Claude Code as the foundation for coding infrastructure, allowing you to decide how to interact with the model
  - Model Routing: Route requests to different models based on your needs (e.g., background tasks, thinking, long context).
  - Supports various model providers like OpenRouter, DeepSeek, Ollama, Gemini, Volcengine, and SiliconFlow.
  - Switch models on-the-fly within Claude Code using the /model command.
  - The `activate` command allows you to set up environment variables globally in your shell, enabling you to use the claude command directly or integrate Claude Code Router with applications built using the Agent SDK.
    - `eval "$(ccr activate)"`
- https://github.com/Fast-Editor/Lynkr /MIT/202512/js
  - https://fast-editor.github.io/Lynkr/
  - Lynkr is a self-hosted Claude Code proxy that lets the CLI route requests through your own infrastructure. 
  - It is a Cli tool which acts like a HTTP proxy that lets Claude Code CLI talk to non-Anthropic backends, manage local tools, and compose Model Context Protocol (MCP) servers with prompt caching, repo intelligence, and Git-aware automation

- https://github.com/UfoMiao/zcf /4.7kStar/MIT/202512/ts
  - http://zcf.ufomiao.com/
  - Zero-Config Code Flow for Claude code & Codex
  - supports Claude Code and Codex, with both environments sharing one CLI
  - API and proxy management: Supports official login, API Key, and CCR proxy three modes, with built-in presets for 302. AI, GLM, MiniMax, Kimi, etc.

- https://github.com/ding113/claude-code-hub /756Star/MIT/202512/ts
  - https://claude-code-hub.app/
  - 现代化的 Claude Code & Codex API 代理服务，提供智能负载均衡、用户管理和使用统计功能。
  - 通过 Next.js 15 + Hono + PostgreSQL + Redis 组合，实现 Claude/OpenAI 兼容 API 代理、智能负载均衡、实时监控、价格管理
  - 智能负载均衡：权重 + 优先级 + 分组调度，内置熔断保护与最多 3 次故障转移。当某个供应商出现问题时，系统自动切换到备用供应商，用户完全无感知
  - 多供应商管理：同时接入 Claude、Codex、Gemini CLI、OpenAI Compatible，自定义模型重定向与 HTTP/HTTPS/SOCKS 代理
  - 限流与并发控制：RPM、金额（5 小时/周/月）、并发 Session 多维限制，Redis Lua 脚本确保原子性与 Fail-Open 降级
  - OpenAI 兼容层：支持 /v1/chat/completions，自动格式转换、工具调用、reasoning 字段与 Codex CLI 指令注入

- https://github.com/qinsehm1128/cloud_claude_code /202601/go/ts
  - [云cc项目部署教程(第一次写教程向, 比较der) ](https://linux.do/t/topic/1408766)

- https://github.com/enulus/OpenPackage /apache2/202601/ts
  - A better, universal, open source version of Claude Code Plugins

- https://github.com/QuivrHQ/247-claude-code-remote
  - Access Claude Code from anywhere - Mobile / Desktop secure connection via Tailscale. Provision VMs with Fly.io. 
  - Compatible with Gemini / Codex / OpenCode

- https://github.com/poco-ai/poco-agent /MIT/202601/python/ts
  - https://poco-ai.com/
  - An intelligent agent harnessing cloud-based Claude Code to realize a Manus-like autonomous experience.
  - Poco is a cloud-based AI agent execution platform inspired by Anthropic's Cowork. It orchestrates Claude AI agents to perform autonomous tasks beyond coding—organizing files, writing documents, analyzing data, and more—in a distributed cloud environment.
  - Works in parallel — Queue multiple tasks without waiting for completion

- https://github.com/AndyMik90/Auto-Claude /11.2kStar/AGPL/202602/python/ts/Electron
  - Autonomous multi-agent coding framework that plans, builds, and validates software for you.
  - Autonomous Tasks	Describe your goal; agents handle planning, implementation, and validation
  - Parallel Execution	Run multiple builds simultaneously with up to 12 agent terminals
  - Isolated Workspaces	All changes happen in git worktrees
  - Memory Layer	Agents retain insights across sessions for smarter builds

### clude-plugins

- https://github.com/treylom/knowledge-manager /202601/ts
  - Knowledge Manager Agent for Claude Code - Extract and organize content from web, PDF, social media to Obsidian/Notion

## codex-cli

- https://github.com/openai/codex /29.7kStar/apache2/202506/rust/ts
  - 📌 Lightweight coding agent that runs in your terminal
  - [Introducing Codex | OpenAI _202505](https://openai.com/index/introducing-codex/)
  - 📴 [Support for local / other LLMs _202504](https://github.com/openai/codex/issues/26)
    - This project is currently using the `/responses` endpoint from OpenAI's API. Ollama has compatibility with some OpenAI API endpoints, but the /responses endpoint is not included yet.
    - [Codex - Ollama](https://docs.ollama.com/integrations/codex)
  - [Codex CLI is Going Native · openai/codex · Discussion _202505](https://github.com/openai/codex/discussions/1174)
    - We're planning to continue merging bugfixes in the TypeScript implementation, while we get the Rust implementation to experience and feature parity in the coming weeks.
  - 🍴 forks
  - https://github.com/just-every/code /apache2/202510/rust
    - a community-driven fork of `openai/codex` focused on real developer ergonomics: Browser integration, multi-agents, theming, and reasoning control — all while staying compatible with upstream.
    - Auto Drive runs the whole play – hand `/auto` a task and it now plans, coordinates agents, reruns checks, and recovers from hiccups without babysitting.
    - [I got tired of GPT-5 being limited by codex, so I forked it : r/OpenAI _202508](https://www.reddit.com/r/OpenAI/comments/1mtqww5/i_got_tired_of_gpt5_being_limited_by_codex_so_i/)
  - https://github.com/a5c-incubator/codex /202508/rust/inactive
    - Add a5c agent workflow template
  - https://github.com/epuerta9/codex-go /apache2/202504/go/inactive
    - codex port in Go

- https://github.com/lulu-sk/CodexFlow /apache2/202512/ts
  - an enhanced GUI tool designed for Codex CLI, focused on improving conversation management and interaction. 
  - Platform recommendation: Windows 11 + WSL (default distro Ubuntu‑24.04). The best experience appears when Codex runs inside WSL. PowerShell mode is experimental 
  - Project architecture: UI host with a minimal terminal bridge (Electron + React + Vite + node‑pty + xterm).
  - Parallel projects: Display active sessions per project to keep multi-tasking organized.

- https://github.com/acrognale/pasture /202512/ts/rust
  - a GUI client built on top of OpenAI's codex agent harness.
  - Message Editing & Conversation Branching
  - Queued messages: Start a new prompt while a turn is running—it queues automatically. Review or cancel queued messages in the status indicator.
  - Limitations - Here's what's not built yet:
    - Custom models/APIs: Codex supports various models and providers, but I haven't exposed that in the UI yet.
    - MCP servers: If you have them configured via codex-cli, they might work? I don't use MCPs myself, so I haven't tested this.

## gemini/qwen-code-cli

- https://github.com/Piebald-AI/gemini-cli-desktop /109Star/MIT/202512/rust/ts/tauri
  - powerful desktop and web interface for Gemini CLI and Qwen Code with visual tool confirmation, real-time thought processes, code diff viewing, chat history management & search, a file tree browser, and file @-mentions. 
  - Built with Rust and React for performance and reliability.
  - Multi-model support - Gemini 2.5 Pro/Flash, Qwen Code, custom OpenAI providers
  - Backend: Rust with Tauri for desktop, Rocket for web server
  - Frontend: React + TypeScript with Tailwind CSS
  - Protocols: Agent Communication Protocol (ACP), WebSocket events
  - Roadmap
    - Token/cost tracking
    - Multi-modal support (images, audio)
    - Extension system
    - LLxprt integration

- https://github.com/cruzyjapan/Gemini-CLI-UI /GPL/202508/js/inactive
  - A desktop and mobile UI for Gemini CLI, Google's official CLI for AI-assisted coding. 
  - You can use it locally or remotely to view your active projects and sessions in Gemini CLI and make changes to them the same way you would do it in Gemini CLI.
  - File Explorer - Interactive file tree with syntax highlighting and live editing
  - YOLO Mode - Skip confirmation prompts for faster operations (use with caution)

- https://github.com/QwenLM/qwen-code /11.9kStar/apache2/202509/ts
  - https://qwenlm.github.io/qwen-code-docs/zh/
  - 📌 Qwen Code 将先进的代码模型能力带入你的终端，提供交互式的 Read-Eval-Print Loop (REPL) 环境
  - a powerful command-line AI workflow tool adapted from Gemini CLI
  - 由一个客户端应用 (packages/cli) 和一个本地 server (packages/core) 组成。
  - 还包含多种工具，用于执行文件系统操作、运行 shell 命令和网络请求等任务，这些工具由 packages/core 管理。
  - Mainland China: ModelScope offers 2, 000 free API calls per day
    - Qwen Code may issue multiple API calls per cycle, resulting in higher token usage (similar to Claude Code). We're actively optimizing API efficiency.
  - [Clicking `esc` will not escape ](https://github.com/QwenLM/qwen-code/issues/496)
    - New line? That’s Ctrl+J. (esc to cancel, 6s)
  - 📴 [有人尝试过本地部署吗？ _202507](https://github.com/QwenLM/qwen-code/discussions/828)
    - 可以连接，我现在连了本地部署的 Ollama，用 qwen3:14b 是可以正常工作的，就是 14b 能力太弱，等于请了个弱智来干活。
    - 能正常调用OLLAMA模型，试过很多模型，大都不能调用工具，只有今天新出的QWEN3:30B,配合的非常好，正常调用工具，但所有模型没有对话历史。 
  - [qwen-code/CHANGELOG.md](https://github.com/QwenLM/qwen-code/blob/main/CHANGELOG.md)
    - Synced upstream `gemini-cli` to v0.x.x
    - [sync upstream gemini-cli Pull request search results](https://github.com/search?q=repo%3AQwenLM%2Fqwen-code+gemini-cli&type=pullrequests&s=updated&o=desc)
  - [Standardize Tool Output Format for Better LLM Communication _202510](https://github.com/QwenLM/qwen-code/pull/881)
    - This PR refactors the tool output format across the codebase to use plain text with system reminders instead of JSON structures. This change improves LLM comprehension and makes tool responses more natural and actionable.
    - Previously, tools returned structured JSON responses (e.g., `{"success": true, "output": "..."}`) 
    - Verbose and unnatural: JSON structures add cognitive overhead for LLMs
    - Inconsistent parsing: The LLM had to parse and interpret JSON semantics
    - Less human-like: Plain text is more aligned with how LLMs naturally process information

- https://github.com/google-gemini/gemini-cli /15.2kStar/apache2/202506/ts
  - 📌 a command-line AI workflow tool that connects to your tools, understands your code and accelerates your workflows.
  - Query and edit large codebases in and beyond Gemini's 1M token context window.
  - Generate new apps from PDFs or sketches, using Gemini's multimodal capabilities.
  - Automate operational tasks, like querying pull requests or handling complex rebases.
  - Use tools and MCP servers to connect new capabilities, including media generation with Imagen, Veo or Lyria
  - Ground your queries with the Google Search tool, built in to Gemini.
  - [Google announces Gemini CLI: your open-source AI agent _202506](https://blog.google/technology/developers/introducing-gemini-cli-open-source-ai-agent/)
  - [Gemini CLI: your open-source AI agent | Hacker News _202506](https://news.ycombinator.com/item?id=44373754)
  - [Whats is the quota limit? 1000 of gemini 2.5 pro? You have reached your daily gemini-2.5-pro quota limit. ](https://github.com/google-gemini/gemini-cli/issues/4300)
    - The limit for Gemini 2.5 Pro for free is 100 requests per day, with the reset time approximately at 5:00 AM UTC
  - 📴 [pr已关闭 Add OpenRouter support for Gemini models _202506](https://github.com/google-gemini/gemini-cli/pull/2319)
    - 👷202508: I appreciate the desire to support models through open router, but we are fully focused on gemini models and endpoints right now, and do not plan to support the differences between the model access on open router vs our own endpoints.
  - [Add support for local/offline language models (Ollola, LM Studio, etc.) ](https://github.com/google-gemini/gemini-cli/issues/5938)
    - I made a patch script to make it work with LM Studio OpenAI compatible API
  - [Open AI API compatible ?  ](https://github.com/google-gemini/gemini-cli/discussions/1974)
    - At this time, we're optimizing Gemini CLI for Gemini models, and not building direct support for other LLM providers.
    - The latest release of `LiteLLM` supports gemini cli. So you can configure a local proxy, configure any model providers you want, and then use them in Gemini CLI. Works great

- https://github.com/iOfficeAI/aioncli /apache2/202512/ts
  - open-source AI agent that brings the power of Gemini directly into your terminal

- https://github.com/vybestack/llxprt-code /202510/ts
  - open-source multi-provider (including local) fork of gemini-cli. 
  - a powerful fork of Google's Gemini CLI, enhanced with multi-provider support and improved theming.
- https://github.com/PardusAI/Pardus-CLI /202510/ts
  - [Pardus CLI: Ollama Support Gemini CLI. : r/ollama _202510](https://www.reddit.com/r/ollama/comments/1of0vcq/pardus_cli_ollama_support_gemini_cli/)
    - the same as Gemini CLI, except you don’t have to log in and can use a local host model.
  - https://github.com/ConardLi/easy-llm-cli /202507/ts/inactive
- https://github.com/gen-cli/gen-cli /202509/ts/inactive
  - custom ContentGenerator for SiliconFlow

- https://github.com/tcsenpai/ollama-code /apache2/202508/ts/inactive
  - forked from Qwen Code, designed to work with locally-hosted Ollama models for enhanced privacy and data sovereignty.
- https://github.com/tinfoilsh/qwen-code /202509/ts/inactive
  - all AI inference to the Qwen3 Coder model is performed using Tinfoil's private AI infrastructure

## opencode-cli

- https://github.com/anomalyco/opencode /75kStar/MIT/202601/ts
   - https://github.com/sst/opencode
  - https://opencode.ai/
  - 📌 The open source AI coding agent.
  - It's very similar to Claude Code in terms of capability. Here are the key differences:
    - 100% open source
    - Not coupled to any provider. can be used with Claude, OpenAI, Google or even local models. 
    - Out of the box LSP support
    - A client/server architecture. support remote control. the TUI frontend is just one of the possible clients.
  - 🎯 [Release v1.0.0 _20251101](https://github.com/sst/opencode/releases/tag/v1.0.0)
    - 1.0 is a complete rewrite of the TUI.
    - We moved from the go+bubbletea based TUI which had performance and capability issues to an in-house framework (OpenTUI) written in zig+solidjs.
    - https://github.com/sst/opentui /MIT/zig/ts
    - The new TUI works like the old one since it connects to the same opencode server.
  - 🍴 forks
  - https://github.com/nanogpt-community/nanocode /MIT/202601
    - a fork of OpenCode configured to use NanoGPT as the default provider.
    - AI-powered coding agent using NanoGPT.
    - Why Use This over Opencode with Nano-GPT as a provider?
    - Models that support reasoning will use the v1thinking endpoint with interleaved thinking enabled by default
    - All models are automatically updated from the nano-gpt api, no need to hardcode them
    - Nano-GPT MCP built in
  - https://github.com/AllAboutAI-YT/pi-terminal /MIT/202508/go/ts/inactive
    - Prompt Injection Terminal
  - https://github.com/IgorWarzocha/opencode-chat
    - [OpenCode Chat - a slimmer version of OC. From 20k tokens init to 5k. : r/LocalLLaMA _202510](https://www.reddit.com/r/LocalLLaMA/comments/1oclqet/opencode_chat_a_slimmer_version_of_oc_from_20k/)
    - The entire prompt stack and tool descriptions have been rewritten around chatting instead of coding. 
  - https://github.com/bon5co/opencode-webui-workspace /docker
    - A containerized development environment running OpenCode WebUI with comprehensive tooling support. 
  - https://github.com/awesome-opencode/awesome-opencode

- https://github.com/NeuralNomadsAI/CodeNomad /203Star/NALic/202512/ts
  - built for people who live inside OpenCode
  - Multi-Instance: Juggle several OpenCode sessions side-by-side with tabs.
  - Monitor background tasks and child sessions without losing flow
  - A native application (Electron-based) with global shortcuts, deeper system integration, and a dedicated window.
  - The SolidJS-based frontend
  - We are also working on a lightweight, high-performance version built with Tauri. 
  - [CodeNomad - multi-instance opencode desktop client : r/opencodeCLI _202511](https://www.reddit.com/r/opencodeCLI/comments/1ox9a4u/codenomad_multiinstance_opencode_desktop_client/)
    - The TUI wasn't cutting it for my workflow and other UIs are either slow or have a different perspective.
    - Primary feature - Fast long session handling. Quick scrolling the session.,
    - Multiple Opencode instances in same window, different tabs.,

- https://github.com/different-ai/openwork /7.6kStar/MIT/202601/rust/ts/tauri
  - https://openwork.software/
  - open-source alternative to Claude Cowork, powered by OpenCode
  - [I built an open-source alternative to Claude Cowork (on top of opencode!) : r/ClaudeAI _202601](https://www.reddit.com/r/ClaudeAI/comments/1qcf8mu/i_built_an_opensource_alternative_to_claude/)
    - it’s basically an alternative gui for opencode, which (at least until now) has been more focused on technical folks.
    - the goal with openwork is to bring the kind of workflows i’m used to running in the cli into a gui, while keeping a very deep extensibility mindset. ideally this grows into something closer to an obsidian-style ecosystem, but for agentic work.
    - open by design: no black boxes, no hosted lock-in.
    - extensible: skills are installable modules via a skill/package manager, using the native opencode plugin ecosystem.
    - non-technical by default: plans, progress, permissions, and artifacts are surfaced in the ui, not buried in logs.
  - [We just hit 7k stars in 10 days, so we're releasing owpen bot a WhatsApp interface for opencode : r/opencodeCLI](https://www.reddit.com/r/opencodeCLI/comments/1qlgi47/we_just_hit_7k_stars_in_10_days_so_were_releasing/)
  - [Show HN: OpenWork – An open-source alternative to Claude Cowork | Hacker News](https://news.ycombinator.com/item?id=46612494)
    - I don't understand the point when opencode desktop already exists.
    - it's fully integrated with Claude Skills.
    - What's the security boundary here - there's no mention of a VM or anything to isolate the agent from the file system?

- https://github.com/joelhooks/opencode-vibe /MIT/202601/ts
  - Next.js 16 rebuild of the OpenCode web application. Real-time chat UI with streaming message display, SSE sync, and React Server Components.
  - Prerequisites: Bun v1.3+ and OpenCode CLI running locally.
  - The web UI auto-discovers all running OpenCode processes. No configuration needed.
  - The web UI auto-discovers all running OpenCode processes. No configuration needed.
  - Cross-process messaging - Send from web UI, appears in your TUI
  - SSE sync - All updates pushed via Server-Sent Events

- https://github.com/0xSero/open-orchestra /MIT/202512/ts
  - Open Orchestra is a multi-agent orchestration plugin for OpenCode that enables you to spawn, manage, and coordinate specialized AI workers. 
  - It implements a hub-and-spoke architecture where a central orchestrator coordinates multiple specialized workers, each optimized for specific tasks.
  - Hub-and-Spoke Architecture - Central orchestrator with specialized workers
  - 6 Built-in Worker Profiles - Vision, Docs, Coder, Architect, Explorer, Memory
  - Optional Neo4j Memory - Persistent knowledge graph (advanced feature)
  - Open Orchestra follows a hub-and-spoke pattern inspired by successful multi-agent systems like AutoGen and LangGraph, but optimized for OpenCode's plugin architecture.

- https://github.com/milisp/opencode-gui /MIT/202510/ts/tauri/inactive
  - A lightweight Tauri GUI for Opencode CLI
- https://github.com/chriswritescode-dev/opencode-manager /70Star/MIT/202601/ts
  - Mobile-first web interface for OpenCode AI agents. 
  - Manage, control, and code with OpenCode from any device - your phone, tablet, or desktop.
  - Features Git integration, file management, and real-time chat in a responsive PWA.
  - Worktree Support - Create and manage Git worktrees for working on multiple branches
  - Multi-Repository Support - Clone and manage multiple git repos/worktrees in local workspaces
  - Git Diff Viewer - View file changes with unified diff, line numbers, and addition/deletion counts
  - Browse files and folders with tree view
  - Large File Support - Virtualization for large files

- https://github.com/code-yeongyu/oh-my-opencode /18.5kStar/NC/202601/ts
  - Run background agents, call specialized agents like oracle, librarian, and frontend engineer. Use crafted LSP/AST tools, curated MCPs, and a full Claude Code compatibility layer.
  - We're building a fully productized version of Sisyphus to define the future of frontier agents.
  - https://github.com/alvinunreal/oh-my-opencode-slim
    - Slimmed and cleaned oh-my-opencode, consumes much less tokens
  - https://github.com/Yeachan-Heo/oh-my-claude-sisyphus
    - Sisyphus from OmO (Oh My Opencode), ported to the Claude Code SDK.

- https://github.com/Microck/opencode-studio /112Star/MIT/202601/ts
  - a local gui for managing opencode configurations. 
  - toggle mcp servers, edit skills, manage plugins, handle auth - no json editing required.

- https://github.com/btriapitsyn/openchamber /322Star/MIT/202601/rust/ts
  - Web and desktop interface for the OpenCode AI coding agent. Works alongside the OpenCode TUI.
  - The OpenCode team is actively working on their own desktop app. I still decided to release this project as a fan-made alternative.

- https://github.com/chriswritescode-dev/opencode-web /MIT/202512/ts
  - A full-stack web application for running OpenCode in local processes, controllable via a modern web interface. 
  - Designed to allow users to run and control OpenCode from their phone or any device with a web browser.
- https://github.com/chris-tse/opencode-web /AGPL/202507/ts/inactive
  - A web-based UI for interacting with the opencode API
  - Live streaming responses via Server-Sent Events
  - Tool execution display with enhanced diff viewing for code changes
- https://github.com/marmotz-dev/opencode-ui /202511/ts/inactive
  - a simple yet powerful desktop client for Opencode
- https://github.com/hosenur/portal /202601/ts
  - Mobile first batteries included web ui for sst/opencode
  - provides a browser interface to interact with OpenCode sessions, view messages, and chat with the AI assistant.
  - This portal is designed for remote access to your OpenCode instance. Deploy the portal on a VPS alongside OpenCode, then use Tailscale (or similar VPN) to securely connect from your mobile device or any other machine.
  - https://github.com/Shahfarzane/opencode-mobile

- https://github.com/Tommertom/opencode-plugin-marketplace /MIT/202601/ts
  - https://opencode-plugin-market.web.app/
  - A community-driven marketplace for discovering and sharing OpenCode plugins.
  - Community-Driven: Anyone can contribute via Pull Requests
  - Fast & Static: Built with SolidJS and hosted on Firebase

- https://github.com/easychen/openMode /MIT/202511/dart
  - a mobile client for OpenCode (and more, maybe). Built with Flutter, it provides a seamless and intuitive interface for interacting with AI assistants, managing code projects, and enhancing your development workflow on the go.

- https://github.com/Th0rgal/opencode-ralph-wiggum /MIT/202601/ts
  - Type `ralph "prompt"` to start open code in a ralph loop. Also supports a prompt file
  - Ralph is a development methodology where an AI agent receives the same prompt repeatedly until it completes a task. Each iteration, the AI sees its previous work in files and git history, enabling self-correction and incremental progress.
  - This package provides a CLI-only implementation (no OpenCode plugin).
  - The AI doesn't talk to itself. It sees the same prompt each time, but the files have changed from previous iterations. This creates a feedback loop where the AI iteratively improves its work until success.
  - https://github.com/Hona/opencode-ralph
    - Ralph Driven Development using OpenCode SDK and OpenTUI

- https://github.com/crottolo/opencode-agent-browser /MIT/202601/ts
  - OpenCode plugin for agent-browser - headless browser automation for AI agents
  - Full Dev Tools - Console logs, network requests, cookies, localStorage, sessionStorage
  - Cookie Banner Handling - Automatically dismisses cookie consent popups
  - Persistent Sessions - Cookies saved across navigations, login once and stay authenticated
  - JavaScript Execution - Run arbitrary JS in page context
  - Video Streaming - Real-time WebSocket streaming for visual monitoring
  - Zero Config - Works out of the box
# cli-coding-agent
- https://github.com/1rgs/nanocode /1.7kStar/MIT/202601/python/单文件
  - Minimal Claude Code alternative. Single Python file, zero dependencies, ~250 lines.
  - Full agentic loop with tool use
  - Tools: read, write, edit, glob, grep, bash
  - Conversation history
  - https://x.com/rahulgs/status/2010179011033608227  __202601
    - launching nanocode! minimal claude code implementation.
    - model >>> agent loop implementation?
  - https://x.com/shao__meng/status/2011791885124206702
    - 核心是一个 Agentic Loop，是能够通过“工具”操作本地文件系统的编程助手
  - https://github.com/kaushal07wick/nanocodex /MIT/python
    - Minimal Codex-CLI implementation.
    - https://x.com/ofcboogeyman/status/2012467798816198889
    - full agentic loop with tools (read, write, glob, grep, bash).

- https://github.com/Aider-AI/aider /37.1kStar/apache2/202508/python
  - https://aider.chat/
  - aider is AI pair programming in your terminal
  - [Aider does not work with lm studio on mac, linux, or windows _202508](https://github.com/Aider-AI/aider/issues/4396)
  - You need an underscore `lm_studio/...` in the prefix
  - `aider --model lm_studio/<your-model-name>`

- https://github.com/hotovo/aider-desk /973Star/apache2/202512/ts/electron
  - https://aiderdesk.hotovo.com/
  - desktop application bringing all the power of aider into a user-friendly graphical interface. 
  - Isolated development environments using Git worktrees 
  - Parallel Development: Work on multiple features simultaneously in isolated worktrees
  - Built-in conflict detection, merge revert, and state preservation
  - Diff Viewer: Review AI-generated code changes with a clear side-by-side comparison.
  - Cost Tracking: Monitor token usage and associated costs per project session for both Aider and the Agent.
  - Usage Dashboard: Visualize token usage, costs, and model distribution with interactive charts and tables.
  - Utilize an autonomous AI agent (powered by Vercel AI SDK) capable of complex task planning and execution 
  - Multi-Project Management: Seamlessly organize, switch between, and manage multiple codebases.
  - [Using Codex-CLI insted of Aider as "engine"? _202504](https://github.com/hotovo/aider-desk/discussions/40)
    - AiderDesk is currently tightly integrated with Aider and relies on some of its specific features. However, the communication within AiderDesk is structured around Connectors (think of them as a plugin system), so in theory, replacing Aider with something like Codex-CLI could be possible
    - One possible approach that came to mind was to build an MCP server for Codex (or Claude Code) and connect it to AiderDesk as a set of tools—similar to how the current Agent mode in Aider works through tools.
  - ⚖️ [Use api of Claude Desktop/Code _202511](https://github.com/hotovo/aider-desk/discussions/488)
    - While technical feasibility seems likely, my primary concern revolves around the legal implications due to a gray area concerning its permissibility under Anthropic's policy.
    - I have done some research. Unfortunately, as I suspected, this would violate Anthropic's terms of service.
  - 📱 [Mobile port _202506](https://github.com/hotovo/aider-desk/issues/242)
    - 👷 202511: Server solution has been added some time ago, so it's possible to use running AiderDesk instance from mobile.

- https://github.com/MoonshotAI/kimi-cli /1.9kStar/apache2/202510/python
  - a new CLI agent that can help you with your software development tasks and terminal operations.
  - https://x.com/yihong0618/status/1982032672559096232
    - 代码写的真挺好
    - RisingWave Labs的实力
    - pyright没有一个warning
    - python 代码不都这样？
  - https://x.com/istdrc/status/2017981457692770737
    - Try install Kimi Code CLI and then run `kimi web`. It's the best Claude Cowork alternative you can get I suppose.
    - Kimi Web still runs the agent loop locally on your terminal, just with a web-based interface
  - https://x.com/tualatrix/status/2018145633635541164
    - Kimi Code 自带的 Web 界面还不错，虽然各家 Coding Agent 都从 CLI 开始搞，但我觉得最终依然会回归 GUI 的。
    - 就像好多视频编辑工具是 ffmpeg 的 CLI 套壳一样

- https://github.com/mistralai/mistral-vibe /839Star/apache2/202512/python
  - Mistral's open-source CLI coding assistant.
  - use natural language to explore, modify, and interact with your projects
  - Autocompletion for slash commands (/) and file paths (@).
  - [ollama/lmstudio support _202512](https://github.com/mistralai/mistral-vibe/issues/9)
    - I think we're missing ability to override model identifier 
    - For those looking to play around with this, was able to get vibe working with ollama with the following diff, I imagine something similar would work for for llmstudio
  - [Local usage? ](https://github.com/mistralai/mistral-vibe/issues/4)
    - for now we support llama-server/llama.cpp for local deployment, currently devstral 2 models don't work well with GGUF format 
  - https://github.com/nicksenger/revibe /apache2/202512/rust
    - a Rust port of Mistral Vibe
    - [Revibe is a Rust-rewrite of Mistral Vibe written by Devstral 2 : r/LocalLLaMA _202512](https://www.reddit.com/r/LocalLLaMA/comments/1pslzv6/revibe_is_a_rustrewrite_of_mistral_vibe_written/)

- https://github.com/gptme/gptme /4.1kStar/MIT/202602/python
  - https://gptme.org/docs/
  - Your agent in your terminal, equipped with local tools: writes code, uses the terminal, browses the web, vision
  - An unconstrained local free and open-source alternative to Claude Code, Codex, Cursor Agents, etc.
  - https://github.com/gptme/gptme-tauri /NALic/202507/rust/ts/inactive
    - Desktop app for gptme built with Tauri

- https://github.com/neovateai/neovate-code /MIT/202601/ts
  - https://neovateai.dev/
  - a coding agent to enhance your development workflow. You can use it to generate code, fix bugs, review code, add tests, and more

- https://github.com/iflow-ai/iflow-cli /NonOpen
  - https://cli.iflow.cn/
  - AI assistant that runs directly in your terminal.
  - [代码是否有开源，没有找到源代码？ ](https://github.com/iflow-ai/iflow-cli/issues/77)
    - 当前cli代码并没有开源。不过cli有几个关联项目已经开源了

- https://github.com/vinhnx/vtcode /MIT/202510/rust
  - a Rust-based terminal coding agent with semantic code intelligence via `Tree-sitter` (parsers for Rust, Python, JavaScript/TypeScript, Go, Java) and `ast-grep` (structural pattern matching and refactoring).
  - Multi-Provider AI: Support for OpenAI, Anthropic, Gemini, xAI, DeepSeek, Z. AI, Moonshot AI, OpenRouter, and Ollama (local)
  - [VT Code — Rust terminal coding agent doing AST-aware edits + local model workflows : r/LocalLLaMA](https://www.reddit.com/r/LocalLLaMA/comments/1oe6y1a/vt_code_rust_terminal_coding_agent_doing_astaware/)
    - Most of the features I planned to build are completed. For local models, I had planned to do ollama integration firsthand. I also do plan to integrate with llama.cpp and lmstudio next

- https://github.com/synthetic-lab/octofriend /202510/ts
  - Octo is a small, helpful, cephalopod-flavored coding assistant that works with any OpenAI-compatible or Anthropic-compatible LLM API, and allows you to switch models at will mid-conversation
  - Octo has helped write some of its own source code, but the codebase is human-first
  - Octo has built-in Docker support, and can attach to any Docker container without needing special configuration or editing the image or container. 

- https://github.com/wonderwhy-er/DesktopCommanderMCP /MIT/202512/ts
  - https://desktopcommander.app/
  - MCP server for Claude that gives it terminal control, file system search and diff file editing capabilities
  - Built on top of MCP Filesystem Server to provide additional search and replace file editing capabilities.

- https://github.com/manaflow-ai/cmux /MIT/202512/ts/rust
  - Open source Claude Code manager that supports Codex/Gemini/Cursor/OpenCode/Amp CLI
  - cmux lets you spawn Claude Code, Codex CLI, Cursor CLI, Gemini CLI, Amp, Opencode, and other coding agent CLIs in parallel across multiple tasks.
  - Every run spins up an isolated VS Code workspace either in the cloud or in a local Docker container with the git diff view, terminal, and dev server preview ready so parallel agent work stays verifiable, fast, and ready to ship.
  - cmux supports macOS. Linux and Windows support coming soon.
  - 未使用tauri

- https://github.com/QuantaAlpha/RepoMaster /202511/python/web
  - https://quantaalpha.github.io/
  - RepoMaster transforms how you solve coding tasks by automatically finding the right GitHub tools and making them work together seamlessly.

- https://github.com/AIPowerGrid/grid-code /202508/ts/inactive
  - a coding agent powered by the grid, a decentralized network of AI workers

- https://github.com/superset-sh/superset /apache2/202512/ts
  - https://superset.sh/
  - A Terminal Built for Coding Agents
  - Run 10+ CLI coding agents like Claude Code, Codex, etc. in parallel on your machine. Spin up new coding tasks while waiting for your current agent to finish. Quickly switch between tasks as they need your attention.
  - For each parallel tasks, Superset uses git worktrees to clone a new branch on your machine.

- https://github.com/erans/lunaroute /apache2/202511/rust
  - LunaRoute is a high-performance local proxy for AI coding assistants like Claude Code, OpenAI Codex CLI, and OpenCode. 
  - Get complete visibility into every LLM interaction with zero-overhead passthrough, comprehensive session recording, and powerful debugging capabilities.
  - Accepts both OpenAI and Anthropic formats simultaneously
  - See Everything Your AI Does

- https://github.com/saadnvd1/agent-os /MIT/202601/ts
  - https://runagentos.com/
  - Mobile-first web UI for managing AI coding sessions (Claude Code, Codex, Aider, Gemini CLI). 
  - Self-hosted with multi-pane terminals, git integration, and session orchestration.

- https://github.com/hlhr202/Conductor-for-all /apache2/202601/ts
  - Conductor for All is a standalone command-line tool designed to bring the Conductor spec-driven development methodology to any coding environment.
  - Originally tied to the Gemini CLI extension, this project aims to decouple the methodology, allowing developers to install and initialize Conductor workflows in their projects so they can be leveraged by any AI Coding Agent (e.g., Claude Code, Cursor, VS Code Copilot, Codex) or IDE.

- https://github.com/specstoryai/getspecstory /961Star/apache2/202601/go
  - https://specstory.com/
  - Turn your AI development conversations into searchable, shareable knowledge.
  - Install our local first extensions for your favorite AI IDE or Terminal Agent. Sync your conversations to the cloud
  - https://x.com/doesdatmaksense/status/2012209297380544940
    - we’ve spent a lot of time normalizing agent sessions, and defining a stable contract for ai conversations across tools.
    - Normalizing agent sessions into a stable contract is underrated. Once the “conversation shape” is consistent, you can do boring but important stuff—diffs, audits, replay, evals—without rewriting integrations every time a new tool pops up.
# cli-utils
- https://github.com/BloopAI/vibe-kanban /20.4kStar/apache2/202602/rust/ts
  - https://www.vibekanban.com/
  - Get 10X more out of Claude Code, Gemini CLI, Codex, Amp and other coding agents...
  - AI coding agents are increasingly writing the world's code and human engineers now spend the majority of their time planning, reviewing, and orchestrating tasks. Vibe Kanban streamlines this process 
  - Easily switch between different coding agents
  - Orchestrate the execution of multiple coding agents in parallel or in sequence
  - Quickly review work and start dev servers
  - Track the status of tasks that your coding agents are working on
  - Centralise configuration of coding agent MCP configs

- https://github.com/doobidoo/mcp-memory-service /1.3kStar/apache2/202602/python/未实现rag
  - Stop re-explaining your project to AI every session. Automatic context memory for Claude, VS Code, Cursor, and 13+ AI tools.
  - ⚖️ fully compatible with the SHODH Unified Memory API Specification v1.0.0, enabling seamless interoperability across the SHODH ecosystem.
  - ❓ 是否支持incremental-indexing
  - Persistent Memory – Context survives across sessions with semantic search
    - Hybrid Backend - Fast 5ms local SQLite + background Cloudflare sync (RECOMMENDED default)
  - Web Dashboard – Visualize and manage memories
  - Knowledge Graph – Interactive D3.js visualization of memory relationships 
  - Compatibility
    - Claude Desktop - Native MCP integration
    - Claude Code - HTTP transport + Memory-aware development with SessionStart hooks
    - VS Code, Cursor, Continue - IDE extensions
    - 15+ AI applications - REST API compatibility
  - [Claude Code Integration: Commands vs MCP Server](https://github.com/doobidoo/mcp-memory-service/blob/main/docs/guides/commands-vs-mcp-server.md)
    - Choose Commands if you want: Simple usage, No configuration (zero MCP server setup)
    - Choose MCP Server if you want: Deep integration with Claude Code's MCP system, Multi-server workflows (alongside other MCP servers)
  - [setting up MCP Memory Service for multiple clients, enabling shared memory access across different applications and devices](https://github.com/doobidoo/mcp-memory-service/blob/main/docs/integration/multi-client.md)
  - 📡 [Enhancement: Hybrid BM25 + Vector Search for Better Exact Match Scoring _202510](https://github.com/doobidoo/mcp-memory-service/issues/175)
  - https://github.com/varun29ankuS/shodh-memory /apache2/202601/rust
    - Persistent memory for AI agents. Single binary. Local-first. Runs offline.
    - We built this because AI agents forget everything between sessions. 

- https://github.com/0xranx/OpenContext /368Star/MIT/202601/rust/js/未实现rag
  - https://0xranx.github.io/OpenContext/
  - 给你的 AI 助手一个持久记忆。 不再重复解释，专注高效构建。
  - OpenContext 直接接入你现有的 CLI（Codex/Claude/OpenCode），并提供 GUI + 内置 Skills/工具
  - OpenContext 是一个面向 AI 助手（Agent）与 Cursor / Claude Code / Codex 等编码工具用户的「个人上下文/知识库」。它直接复用你已有的 coding agent CLI（Codex/Claude/OpenCode），并提供 GUI 与内置 Skills/工具，让 AI 助手能「先读历史再动手、做完再沉淀」。
  - oc CLI — 管理全局 contexts/ 文档库（目录/文档、清单、检索）
  - MCP Server — 让 Cursor/Claude Code/Codex/Agent 通过工具调用 OpenContext
  - Web UI — 本地浏览/编辑文档（无需安装桌面版）

- https://github.com/zilliztech/claude-context /5.2kStar/MIT/202509/python/ts/inactive
  - MCP plugin that adds semantic code search to Claude Code and other AI coding agents(codex/gemini-cli)
  - Hybrid Code Search: BM25 + dense vector
    - uses semantic search to find all relevant code from millions of lines. No multi-round discovery needed. It brings results straight into the Claude's context.
  - efficiently stores your codebase in a vector database and only uses related code in context to keep your costs manageable.
  - 🔄 Incremental Indexing: Efficiently re-index only changed files using Merkle trees.
  - Analyze code in Abstract Syntax Trees (AST) for chunking.
  - Customizable: Configure file extensions, ignore patterns, and embedding models.
  - Embedding Providers: OpenAI, VoyageAI, Ollama, Gemini
  - Vector Databases: Milvus or Zilliz Cloud(fully managed vector database as a service)
  - Code Splitters: AST-based splitter (with automatic fallback), LangChain character-based splitter
  - While MCP is the recommended way to use Claude Context with AI assistants, you can also use it directly or through the VSCode extension.
  - 🧑‍🏫 [Update Docs: Fully offline install guide _202508](https://github.com/zilliztech/claude-context/issues/162)
  - [Question: is index autosync available _202511](https://github.com/zilliztech/claude-context/issues/238)
    - After I run initial indexing, does Claude context continue to auto-sync and update the changes in multiple code granularity, meaning only the changes gets updated and vectors created only for the changed code?
    - Currently having to manually update indexes after every change
  - [Is it required and must use openai key? _202507](https://github.com/zilliztech/claude-context/issues/81)
    - This project currently doesn't use LLM, so what you need to do is to select an embedding model
    - openrouter does not have embedding models. you can use Mistral Code Embedding that supports the same API
    - It looks like Mistral Code Embedding is a good one, but it seems to have it's own api
    - 202601: OpenRouter only recently added support for embeddings. 

- https://github.com/Wildcard-Official/deepcontext-mcp /258Star/apache2/202509/ts/inactive
  - https://wild-card.ai/deepcontext
  - DeepContext is an MCP server that adds symbol-aware semantic search to Claude Code, Codex CLI, and other agents for faster, smarter context on large codebases.
  - Currently supports Typescript and Python.
  - Visit the Wildcard DeepContext page, Click "Generate API Key"
  - Most coding agents use grep based search that match exact text, these searches miss semantically related code and fill context windows with irrelevant results.
  - 🚧 Self-hosting requires code modifications to integrate directly with vector storage and embedding providers, as the current implementation uses the Wildcard API backend.
    - Turbopuffer API key for vector storage and hybrid search operations
    - Jina AI API key for text embeddings and reranking services
  - MCP Integration Flow
    - Coding Agent communicates with DeepContext through the Model Context Protocol
    - MCP server receives requests, validates parameters, and routes to appropriate core components
    - For long-running operations like indexing, spawns detached background processes to prevent timeouts

- https://github.com/marcoaapfortes/Mantic.sh /532Star/AGPL/202601/ts/rag
  - A structural code search engine for Al agents.
  - After testing across 5 repositories (cal.com, next.js, tensorflow, supabase, chromium), it demonstrates superior result quality compared to grep/ripgrep 
  - Semantic Reranking (Hybrid Intelligence): Combines heuristic speed with neural understanding. Uses local embeddings (transformers.js) to find "conceptually relevant" code even without exact keyword match
  - Deep understanding of your codebase structure using Tree-sitter.
  - CLI Installation: npx mantic.sh@latest "your search query"
  - MCP Server Installation: Mantic works as an MCP server for Claude Desktop, Cursor, VS Code, and other MCP-compatible tools.

- https://github.com/campfirein/cipher /3.5kStar/elastic/202512/ts/rag/inactive
  - https://docs.byterover.dev/cipher/overview
  - opensource memory layer specifically designed for coding agents. 
  - Compatible with Cursor, Codex, Claude Code, Windsurf, Cline, Claude Desktop, Gemini CLI, AWS's Kiro, VS Code, Roo Code, Trae, Amp Code and Warp through MCP.
  - MCP integration with any IDE you want.
    - Cipher can run as an MCP (Model Context Protocol) server, allowing integration with MCP-compatible clients like Codex, Claude Desktop, Cursor, Windsurf, and other AI coding assistants.
  - Auto-generate AI coding memories that scale with your codebase.
  - Switch seamlessly between IDEs without losing memory and context.
  - Dual Memory Layer that captures System 1 (Programming Concepts & Business Logic & Past Interaction) and System 2 (reasoning steps of the model when generating code).
  - llm支持local, 包括lmstudio
  - vector db支持 Qdrant, Milvus, ChromaDB, or In-Memory
  - The Cipher Web UI provides an intuitive interface for interacting with memory-powered AI agents, featuring session management, tool integration, and real-time chat capabilities.
  - [Hybrid RAG _202602](https://github.com/campfirein/cipher/discussions/293)
    - as i got some exp in RAG design i was wondering, what effect hybrid rag could have here, i mean using also Keywordsearch internally.
  - [[FEATURE] Implement Cross-Project Knowledge Transfer System _202509](https://github.com/campfirein/cipher/issues/249)
    - This repository has been archived. No further work will be done. For production use, please visit byterover.dev
  - https://github.com/RyanNg1403/agentic-search-vs-rag /MIT/202601/python/同作者
    - A reproducible experiment comparing traditional vector-based RAG with Agentic Search (context trees) for code retrieval tasks.
    - This experiment validates that context trees with agentic search dramatically outperform traditional RAG for code understanding tasks.
      - 2× better retrieval accuracy (IoU score)
      - 99% fewer tokens used per query

- https://github.com/johnhuang316/code-index-mcp /731Star/MIT/202601/python
  - MCP server that helps large language models index, search, and analyze code repositories with minimal setup
  - get started with any MCP-compatible application: cc, codex, ...

- https://github.com/BeehiveInnovations/pal-mcp-server /11kStar/apache2/202512/python/inactive
  - Why rely on one AI model when you can orchestrate them all?
  - A Model Context Protocol server that supercharges tools like Claude Code, Codex CLI, and IDE clients such as Cursor or the Claude Dev VS Code extension. 
  - PAL MCP connects your favorite AI tool to multiple AI models for enhanced code analysis, problem-solving, and collaborative development.
  - PAL supports conversation threading so your CLI can discuss ideas with multiple AI models

- https://github.com/pchalasani/claude-code-tools /1.4kStar/MIT/202601/python/rust
  - productivity tools for Claude Code, Codex-CLI, and similar CLI coding agents.
  - aichat is your unified CLI command-group for managing Claude Code and Codex sessions: Resume with lineage, Full-text search with Tantivy
  - tmux-cli works with any CLI coding agent, Think Playwright for terminals - Terminal automation for AI agents.
  - lmsh: Natural language shell - type what you want in plain English, get an editable command.
# background-ai
- https://github.com/ColeMurray/background-agents /MIT/202601/python/ts
  - https://backgroundagents.dev/
  - open-source background coding agent system inspired by Ramp's Inspect.
  - https://x.com/_colemurray/status/2016210023366717818
    - OpenInspect is an open source implementation of Ramp's background agent blog post.
  - [Why We Built Our Own Background Agent: Inspect — Ramp Builders Blog _202601](https://builders.ramp.com/post/why-we-built-our-background-agent)
    - Inspect writes the code like any other coding agent, but closes the loop on verifying its work by having all the context and tools needed to prove it
    - Each session runs in a sandboxed VM on Modal with everything an engineer would have locally: Vite, Postgres, Temporal, the works.

- https://github.com/ishaan1013/shadow /MIT/202508/ts
  - https://shadowrealm.ai/
  - Background coding agent and real-time web interface
  - Sets up isolated execution environments for AI agents to work on GitHub repositories with tools to understand code, edit files, and much more.
  - Automatic workspace setup and cleanup on Micro-VMs
  - Kata QEMU containers for hardware-level isolation
  - Multi-provider LLM support (Anthropic, OpenAI, OpenRouter)
  - Tool execution with file operations, terminal commands, and code search
  - Memory system for repository-specific knowledge retention
  - Lightweight Shadow Wiki generation for comprehensive codebase documentation
  - Shadow supports two execution modes through an abstraction layer:
    - Local Mode: Direct filesystem execution on the host machine
    - Remote Mode (For Deployment): Hardware-isolated execution in Kata QEMU containers, True VM isolation via QEMU hypervisor
  - https://x.com/_rajanagarwal/status/1955075526621794716
    - meet Shadow, a powerful open-source background coding agent
    - 1.7K commits later, we think this is a great open source framework to build off of to make background coding agents. 
    - shadow has contributed 1k+ lines to itself
    - https://x.com/ElijahKurien/status/1955075209720967457
# vscode-ai
- https://github.com/continuedev/continue /21.3kStar/apache2/202508/ts
  - https://docs.continue.dev/
  - Continue is the leading open-source AI code assistant. You can connect any models and any context to build custom autocomplete and chat experiences inside VS Code and JetBrains
  - Tab to autocomplete code suggestions
  - [Continue 实现原理 · Pines-Cheng/blog _202505](https://github.com/Pines-Cheng/blog/issues/108)
  - [docs: added the fastapply model to the recommendations by Olyray · Pull Request · continuedev/continue](https://github.com/continuedev/continue/pull/8249)
    - [Feature Request: Support FastApply model format parsing _202411](https://github.com/continuedev/continue/issues/2801)

- https://github.com/robertpiosik/CodeWebChat /GPL/202601/ts
  - open-source AI coding toolkit. You can use CWC in VS Code family of editors (Cursor, Antigravity, VSCodium etc.) for a much faster and cost efficient* development experience.
  - Apply responses—interactive edits integration with checkpoints for state restoration
  - Fully-featured—code completions, commit messages, checkpoints, skills, and more
  - zero-overhead prompts optimized for prompt caching
  - 100% local operation
  - [I created a coding tool that produce prompts simple enough for smaller, local models : r/LocalLLaMA _202511](https://www.reddit.com/r/LocalLLaMA/comments/1p3qxj4/i_created_a_coding_tool_that_produce_prompts/)

- https://github.com/twinnydotdev/twinny /MIT/202408/ts
  - https://twinny.dev/
  - The most no-nonsense, locally or API-hosted AI code completion plugin for Visual Studio Code - like GitHub Copilot but completely free and 100% private
  - Operates online or offline
  - Conforms to the OpenAI API standard
  - Chat conversations are preserved
  - Compatible with Ollama, llama.cpp, oobabooga, and LM Studio APIs

- https://github.com/julesmons/recline /MPLv2/202501/ts
  - The AI assistant that seamlessly integrates with VSCode to autonomously create, edit, and run terminal commands; redefining how you code.

- https://github.com/Joouis/agent-maestro /MIT/202510/ts
  - Turn VS Code into your compliant AI playground
  - With Agent Maestro, spin up Cline or Roo on demand and plug Claude Code or Codex straight in through an OpenAI/Anthropic-compatible API.
  - Universal API Compatibility: Anthropic (/messages) and OpenAI (/chat/completions) compatible endpoints - use Claude Code, Codex or any LLM client seamlessly
  - Headless AI Agent Control: Create and manage tasks through REST APIs for Roo Code and Cline extensions
  - Parallel Execution: Run up to 20 concurrent RooCode (and its variants like Kilo Code) tasks with built-in MCP server integration
# more
