---
title: lib-aikit-code-pi-examples
tags: [examples, pi]
created: 2026-08-14T21:43:45.337Z
modified: 2026-08-14T21:43:52.168Z
---

# lib-aikit-code-pi-examples

# guide
- resources
  - [[pi] 对Pi Code Agent生态的整理 - LINUX DO _202607](https://linux.do/t/topic/2504439)
# popular
- https://github.com/earendil-works/pi /55.5kStar/MIT/202605/ts
  - https://pi.dev/
  - https://pi.dev/docs/latest
  - Pi Agent Harness Mono Repo
    - @earendil-works/pi-ai	Unified multi-provider LLM API (OpenAI, Anthropic, Google, etc.)
    - @earendil-works/pi-agent-core	Agent runtime with tool calling and state management
    - @earendil-works/pi-coding-agent	Interactive coding agent CLI
    - @earendil-works/pi-tui	Terminal UI library with differential rendering
  - 核心开发仅2人
  - [Pi: The Minimal Agent Within OpenClaw  _202601](https://lucumr.pocoo.org/2026/1/31/pi/)
  - [Learn Agents by Building One: The Minimal Agent pi _202602](https://www.vandee.art/blog/2026-02-11-learn-agents-by-building-one-the-minimal-agent-pi.html)
  - [Pi – A minimal terminal coding harness | Hacker News _202602](https://news.ycombinator.com/item?id=47143754)
  - [Add a Python SDK for `pi-agent-core` and `pi-ai` _202605](https://github.com/earendil-works/pi/issues/4174)
    - sorry, this is entirely out of scope for pi itself. but nothing stops you from building this as your own project.
  - [大模型应用开发：学习和整理Pi的LLM模块设计 - LINUX DO _202606](https://linux.do/t/topic/2293027)
  - https://github.com/earendil-works/pi-chat
    - A pi extension that bridges Discord and Telegram channels to a sandboxed pi session. Each connected channel gets its own Gondolin micro-VM with persistent workspace, shared storage, memory, and skills.
    - Requirements
    - QEMU installed (brew install qemu on macOS)
    - Gondolin guest image (downloaded automatically on first connect)
  - https://github.com/Xplo8E/piai /MIT/202603/python
    - Python port of pi-ai 
  - https://github.com/vamsi/pi /MIT/202602/python
    - A modular AI agent toolkit written in Python
  - https://github.com/solvit-team/py-pimono
    - a local coding agent and a Python reimplementation of pi-mono.
  - https://github.com/atveit/mojopi /MIT/202604/python
    - A Mojo/MAX port of pi-mono 
    - Port maintained against Mojo 26.2 and the MAX nightly channel.
  - https://github.com/Dicklesworthstone/pi_agent_rust /MIT/202606/rust
    - a from-scratch Rust port of Pi Agent 
    - Single binary, instant startup, stable streaming, and 8 built-in tools.
- https://github.com/can1357/oh-my-pi /12.6kStar/MIT/202606/rust/ts
  - https://omp.sh/
  - AI Coding agent for the terminal — hash-anchored edits, optimized tool harness, LSP, Python, browser, subagents, and more
  - Fork of Pi. Originally built on Mario Zechner's wonderful Pi, omp adds everything you're missing.
  - 40+ providers · 32 built-in tools · 14 lsp ops · 28 dap ops · ~55k lines of Rust core.
  - https://x.com/geekbb/status/2065979536471417341
    - 从 Tau 分出来的一个分支，专门给 Pi 编码代理做了个 Codex 风格的客户端。把 Pi 运行时直接打包进应用里，装完就能用，不用额外装命令行工具。

- https://github.com/ayuayue/PiDeck /571Star/MIT/202608/ts
  - https://github.com/ayuayue/pi-desktop /renamed
  - https://ayuayue.github.io/PiDeck/
  - 在本地项目目录中统一管理 pi Agent 会话，并支持导入 Codex、Claude 本地会话以便统一浏览和恢复。
  - 支持多项目工作区、会话历史、Git 集成、内置终端、模型配置和插件管理，基于 Electron 构建。
  - PiDeck 不是 pi 的分支。它是一个轻量 Electron 外壳，通过启动多个 pi --mode rpc 进程，将项目管理、会话管理、对话界面、配置管理和工具编排整合到一个原生桌面应用中——所有 Agent 能力由 pi 原生提供。

- https://github.com/omaclaren/pi-studio /202608/ts
  - Extension for pi that opens a local two-pane browser workspace for working with prompts, responses, live working details, Markdown and LaTeX documents, interactive HTML previews, code files
- https://github.com/shixin-guo/picot /MIT/202608/ts
  - A local desktop GUI for the Pi coding agent. No cloud, no account — runs entirely on your machine.
  - [Pi Studio — a local desktop UI for Pi coding agent : r/PiCodingAgent _202606](https://www.reddit.com/r/PiCodingAgent/comments/1tti7d8/pi_studio_a_local_desktop_ui_for_pi_coding_agent/)
    - interaction with Pi agent like Codex desktop app, but free, open and extendable 

- https://github.com/deflating/tau  /202606/ts
  - A web UI that mirrors your Pi terminal session in the browser. 
  - No separate server — it runs as a Pi extension inside your existing process.
  - Tau connects to your running Pi TUI and gives you a second view in the browser. Same session, same messages, same tools — just a different screen. 
  - Type in the terminal or the browser, both stay in sync.
- https://github.com/goncalossilva/tau /MIT/202608/ts
  - a batteries-included distribution for Pi
  - It takes Pi's minimal core and turns it into an opinionated, complete, polished experience, adding a websearch tool to complement the four default built-in tools, plus several useful skills and tasteful extensions, split into purpose-driven packages

- https://github.com/huggingface/tau /1.8kStar/MIT/202607/python
  - http://twotimespi.dev/
  - A Python port of Pi’s minimalist coding agent.
  - Tau can read files, edit code, run commands, and keep a durable session history while streaming what it is doing.
  - tau_coding  →  tau_agent  →  tau_ai
    - tau_ai translates model providers into Tau's provider-neutral stream.
    - tau_agent owns the portable brain: messages, tools, events, loop, harness, and session primitives.
    - tau_coding wraps the brain as a real coding app: CLI, TUI, file/shell tools, provider config, project instructions, skills, and on-disk sessions.

- https://github.com/itayinbarr/little-coder /1.5kStar/apache2/202606/ts
  - https://itayinbarr.github.io/little-coder/
  - A coding agent tuned for small local models, built on top of `pi`.
  - pi is the minimal substrate — agent loop, multi-provider API, TUI, session tree, compaction, extension model. Four built-in tools (read / write / edit / bash) and a ~1000-token system prompt.
  - little-coder is pi + 20 extensions + 30 skill markdown files + a Python benchmark harness. 
    - It doesn't fork pi or shadow its CLI — pi is a plain dependency in package.json, and everything little-coder-specific lives under .pi/extensions/, skills/, and benchmarks/. 

- https://github.com/0xku/kon /323Star/MIT/202606/python
  - Kon is a minimal coding agent focused on a tiny core prompt, a small built-in toolset, and project-specific context layered on top only when you want it. 
  - The default system prompt stays under 270 tokens, and even including the built-in tool descriptions and parameter schemas
  - ❓ 是否不支持extension
  - Kon takes significant inspiration from `pi` coding-agent, especially around philosophy and UI direction.
    - Kon also borrows ideas from Amp, Claude Code, and other terminal coding agents.

- https://github.com/smallnest/pigo /MIT/202607/go
  - https://colobu.com/pigo/
  - 使用 Go 复刻的 pi AI Agent —— 一个面向命令行的编码智能体，同时支持无头（headless）脚本模式与交互式 REPL。
  - pigo 可以读写文件、执行命令、检索代码、抓取网页，并借助大模型完成从"读懂需求"到"改好代码"的闭环。它兼容 OpenAI / Anthropic 等多种协议网关，支持会话续跑、项目信任、技能（Skills）、插件与包管理。
  - https://x.com/smallnest/status/2080103406837129633
    - 使用Go又重写pi agent, 以前重写是为了复制openclaw,这次纯粹是为了它的小巧灵。

- https://github.com/justhil/pi-app /202606/ts
  - 面向个人开发者的 pi 桌面 GUI：在 Electron 里跑 pi SDK，复用 ~/.pi/agent 的认证、配置与会话 JSONL，用时间线、工具卡片、改动审查和扩展兼容层替代终端里那套 TUI 交互。
  - [【π】pi-app，兼容pi插件生态，优雅的 pi 桌面 GUI 开源实现 - LINUX DO _202606](https://linux.do/t/topic/2452715)
    - 抄的codex app
    - 内置 SDK 或复用已有 pi 环境; 自动检测已有会话, GUI 与 TUI 会话双向非实时同步(同一份 JSONL)。
    - 兼容 pi 现有插件生态——通过单文件 JSON 适配器把 TUI 界面适配到 GUI, AI 可一键生成; 应用内置主流插件适配, 且支持外置覆盖。
    - pi配置模型不是直接让ai来就好了吗 
    - 公式渲染支持的如何? 我有个朋友(真)总是和我抱怨TUI不好看公式.
    - jerryan/pi-hashline-edit 这个插件 然后就是pi-tool-display 这个插件会提供原版的编辑工具的差异更改 反正都挺好看的

- https://github.com/heyhuynhgiabuu/openpi /MIT/202606/ts/electron
  - [OpenPi - a desktop workbench for the Pi coding agent : r/PiCodingAgent _202605](https://www.reddit.com/r/PiCodingAgent/comments/1tcrb2v/openpi_a_desktop_workbench_for_the_pi_coding_agent/)
  - a desktop workbench for the Pi coding agent. It’s meant to make Pi feel more at home as a desktop app: session sidebar, conversation view, command palette, source control panel, file search, diff viewer, and terminal/output in one place.
  - It uses pi-coding-agent under the hood 

- https://github.com/agegr/pi-web /MIT/202606/ts
  - pi 编程智能体 的网页界面。在浏览器中浏览会话、与智能体对话、分叉对话、切换消息分支。
  - 会话内分支 — 回退到任意节点继续对话，在同一文件内创建分支
  - https://github.com/Chasen-Liao/pi-agent-desktop
    - 基于 Electron 的 Pi 编程智能体桌面客户端 (衍生自 pi-web)

- https://github.com/jmfederico/pi-web /MIT/202606/ts
  - https://pi-web.dev/
  - Web UI for Pi Coding Agent that keeps sessions alive in real workspaces.

- https://github.com/pithings/pi-vscode /MIT/202604/ts
  - 🍴 forks
  - [在VSCode中深度集成Pi Agent经验分享 - LINUX DO _202606](https://linux.do/t/topic/2432358/7)
  - 终端即本体 — pi 跑在 VS Code 内置终端里，不是 GUI 包装器，没有 shell 转义地狱
  - 侧边栏管理 — Sessions、Models、Settings 三合一，Providers / OAuth / API Keys 一站式配置
  - 极简，省token。系统提示词就5k，4个tools，配置简单但是可扩展能力强，也是openclaw核心sdk。
  - 其实是vscode的终端打开pi，还的原生tui，插件只是简化操作。vscode终端和编辑器是两套快捷键，不冲突。

- https://github.com/ayuayue/PiDeck /MIT/202606/ts
  - https://ayuayue.github.io/PiDeck/
  - Desktop workbench for managing multiple pi coding-agent sessions across project folders.

- https://github.com/1jehuang/jcode /7.6kStar/MIT/202606/rust
  - The next generation coding agent harness to raise the skill ceiling.
  - Built for multi-session workflows, infinite customizability, and performance.
  - [I made my own coding agent harness : r/PiCodingAgent _202606](https://www.reddit.com/r/PiCodingAgent/comments/1ud9vrh/i_made_my_own_coding_agent_harness/)
    - It has somewhat of a similar spirit of PI, but much more performance/efficiency focused.

- https://github.com/zosmaai/pi-llm-wiki /MIT/202606/ts
  - Self-maintaining, Obsidian-compatible knowledge base for pi. Follows Andrej Karpathy's LLM Wiki pattern.
  - Turn raw sources (URLs, PDFs, markdown, JSON, XML) into a durable, interlinked, LLM-maintained wiki that compounds over time.
  - Turn raw sources (URLs, PDFs, markdown, JSON, XML) into a durable, interlinked, LLM-maintained wiki that compounds over time.

- https://github.com/rcarmo/piclaw /MIT/202607/ts
  - https://rcarmo.github.io/projects/piclaw/
  - PiClaw packages the Pi Coding Agent into a self-hosted workspace with a trilingual streaming web UI, persistent state, multi-provider LLM support, and a practical built-in toolset that includes many add-ons.

- https://github.com/ThilinaTLM/nerve /apache2/202607/ts/svelte
  - https://nerve.tlmtech.dev/
  - A transparent, local-first desktop coding harness with the focus of a small agent and the workflow of a complete workbench.
  - [Nerve — an open-source, local-first desktop coding harness inspired by the simplicity of Pi : r/PiCodingAgent _202607](https://www.reddit.com/r/PiCodingAgent/comments/1v976ro/nerve_an_opensource_localfirst_desktop_coding/)

- https://github.com/daugasauron/piodide /MIT/202607/ts/c
  - https://daugasauron.github.io/piodide/
  - pi coding-agent terminal running entirely in the browser with Ghostty Web and Pyodide
  - A coding agent, Python runtime, shell, editor, and local LLM host that run in one browser tab.

- https://github.com/hahhforest/pi-textbook /MIT/202607/ts
  - https://build-your-own-pi-cn.enochzhang.chatgpt.site/
  - 《动手学 Pi》：沿 15 个真实 checkpoint 从零构建 Pi-style Agent
# ui

# examples

# utils
- https://github.com/awoaCrim/pi-openai-toolkit /MIT/202608/ts
  - [【开源自荐】pi-openai-toolkit：把 GPT 的原生能力带进 Pi - LINUX DO _202608](https://linux.do/t/topic/2774555)
  - 共有两个工具：
  - v2 远程 compaction： 允许你在使用 openai-responses 端点时，走 gpt 官方的远程压缩路线，至于好处大概就是不需要维护 compact 提示词，比传统 compact 在保留长时间 Agent 任务中的任务状态与推理连续性更优秀。 另外本次更新支持 compact 时用指定的模型，比如平时用 sol，compact 时候用 luna，进一步减少消耗。
  - 原生 websearch 工具： 直接将检索放进模型 reasoning loop 里，省略了中间层。

## pi-web-search

- https://github.com/demigodmode/pi-web-agent /AGPL/202608/ts
  - Reliable web tools for Pi: search for sources, fetch over HTTP, and use headless browsing only when explicitly requested.
  - [pi-web-agent is essentially feature-complete now, Tavily and Exa are the last backends that were added : r/PiCodingAgent _202608](https://www.reddit.com/r/PiCodingAgent/comments/1vmkzzp/piwebagent_is_essentially_featurecomplete_now/)
    - What's the marginal improvement for adding more API keys or you only get to pick one to search in at a time?
    - multi-provider search isn't a bad idea at all. I could see value in optionally fanning a query out to 2-3 providers, deduping the results, then reranking them before the research loop continues. main downside would be extra latency/API usage, so I'd probably make it opt-in rather than the default. 
  - how does it compare to pi-web-access? https://pi.dev/packages/pi-web-access
    - the reason I ended up building this was that "pi-web-access" felt a bit too interactive for how I wanted web research to work. the curator/review flow can open a browser/window and ask you to approve results, which is useful if you want that level of control but I found it disruptive for normal agent use. you can disable that now (right?) but that workflow was a big part of what pushed me toward building something more hands-off.
    - "pi-web-agent" is intentionally more hands-off. the model gets one research tool, "web_explore", and search/fetch/headless/ranking/evidence checks all happen behind that boundary without popping you out of the session.
    - "pi-web-access" has a bigger feature surface. mine is more opinionated around keeping research bounded, quiet, and agent-native.
# more
