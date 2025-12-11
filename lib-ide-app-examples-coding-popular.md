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
- https://github.com/oraios/serena /17.1kStar/MIT/202512/python
  - A powerful coding agent toolkit providing semantic retrieval and editing capabilities (MCP server & other integrations)
  - Serena is a powerful coding agent toolkit capable of turning an LLM into a fully-featured agent that works directly on your codebase.
  - Unlike most other tools, it is not tied to an LLM, framework or an interface
  - Serena provides essential semantic code retrieval and editing tools that are akin to an IDE's capabilities
  - You can think of Serena as providing IDE-like tools to your LLM/coding agent. With it, the agent no longer needs to read entire files, perform grep-like searches or string replacements to find and edit the right code. Instead, it can use code centered tools like find_symbol, find_referencing_symbols and insert_after_symbol.

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

- https://github.com/winfunc/opcode /19.1kStar/AGPL/202510/ts/rust/tauri/inactive
  - https://opcode.sh/
  - A powerful GUI app and Toolkit for Claude Code
  - Create custom agents, manage interactive Claude Code sessions, run secure background agents, and more.
  - Session History: View and resume past coding sessions with full context
  - Background Execution: Run agents in separate processes for non-blocking operations

- https://github.com/stravu/crystal /MIT/202511/ts
  - a new graphical interface to manage Claude Code sessions. 
  - Run multiple Codex and Claude Code AI sessions in parallel git worktrees
  - We built this internally to help speed up the development of Stravu, and it was so helpful we decided we had to share it
  - Create sessions from prompts, each in an isolated git worktree: Each session operates in its own git worktree
  - Monitor all your Claude Code sessions from a unified interface
  - [Crystal: Supercharge Your Development with Multi-Session Claude Code Management](https://nimbalyst.com/blog/crystal-supercharge-your-development-with-multi-session-claude-code-management)

- https://github.com/opactorai/Claudable /3.4kStar/MIT/202512/ts/electron
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

- https://github.com/milisp/codexia /300Star/MIT/202511/ts/tauri
  - https://github.com/codexia-team/codexia /renamed
  - A powerful GUI and Toolkit for Codex CLI
  - fork chat, file-tree integration, notepad, git diff, build-in pdf csv/xlsx viewer, and more.
  - [We built Codexia - A free and open-source powerful GUI app and Toolkit for Codex CLI : r/ChatGPTCoding _202511](https://www.reddit.com/r/ChatGPTCoding/comments/1op0yr6/we_built_codexia_a_free_and_opensource_powerful/)
  - Is there git worktree integration?
    - No, but in my plan
  - https://github.com/milisp/codexia-zen
    - GUI for OpenAI Codex CLI, minimalist design

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

## cli-coding-agent

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

- https://github.com/sst/opencode /28.7kStar/MIT/202510/go/ts
  - https://opencode.ai/
  - 📌 The AI coding agent built for the terminal
  - It's very similar to Claude Code in terms of capability. Here are the key differences:
    - 100% open source
    - Not coupled to any provider. Although Anthropic is recommended
    - Out of the box LSP support
    - A client/server architecture. support remote control
  - 🍴 forks
  - https://github.com/IgorWarzocha/opencode-chat
    - [OpenCode Chat - a slimmer version of OC. From 20k tokens init to 5k. : r/LocalLLaMA _202510](https://www.reddit.com/r/LocalLLaMA/comments/1oclqet/opencode_chat_a_slimmer_version_of_oc_from_20k/)
    - The entire prompt stack and tool descriptions have been rewritten around chatting instead of coding. 

- https://github.com/NeuralNomadsAI/CodeNomad /203Star/NALic/202512/ts
  - built for people who live inside OpenCode
  - Multi-Instance: Juggle several OpenCode sessions side-by-side with tabs.
  - Monitor background tasks and child sessions without losing flow
  - A native application (Electron-based) with global shortcuts, deeper system integration, and a dedicated window.
  - We are also working on a lightweight, high-performance version built with Tauri. 

- https://github.com/milisp/opencode-gui /MIT/202510/ts/inactive
  - A lightweight Tauri GUI for Opencode CLI

- https://github.com/chriswritescode-dev/opencode-web /MIT/202512/ts
  - A full-stack web application for running OpenCode in local processes, controllable via a modern web interface. 
  - Designed to allow users to run and control OpenCode from their phone or any device with a web browser.
- https://github.com/chris-tse/opencode-web /202507/ts/inactive
  - A web-based UI for interacting with the opencode API
  - Live streaming responses via Server-Sent Events
  - Tool execution display with enhanced diff viewing for code changes
- https://github.com/marmotz-dev/opencode-ui /202511/ts/inactive
  - a simple yet powerful desktop client for Opencode

- https://github.com/MoonshotAI/kimi-cli /1.9kStar/apache2/202510/python
  - a new CLI agent that can help you with your software development tasks and terminal operations.
  - https://x.com/yihong0618/status/1982032672559096232
    - 代码写的真挺好
    - RisingWave Labs的实力
    - pyright没有一个warning
    - python 代码不都这样？

- https://github.com/mistralai/mistral-vibe /839Star/apache2/202512/python
  - Mistral's open-source CLI coding assistant.
  - use natural language to explore, modify, and interact with your projects
  - Autocompletion for slash commands (/) and file paths (@).
  - [ollama/lmstudio support _202512](https://github.com/mistralai/mistral-vibe/issues/9)
    - I think we're missing ability to override model identifier 
    - For those looking to play around with this, was able to get vibe working with ollama with the following diff, I imagine something similar would work for for llmstudio
  - [Local usage? ](https://github.com/mistralai/mistral-vibe/issues/4)
    - for now we support llama-server/llama.cpp for local deployment, currently devstral 2 models don't work well with GGUF format 

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
# background-ai
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
