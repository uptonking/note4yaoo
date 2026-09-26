---
title: lib-aikit-paseo-examples
tags: [examples, paseo]
created: 2026-09-17T14:19:21.975Z
modified: 2026-09-17T14:19:32.208Z
---

# lib-aikit-paseo-examples

# guide

# popular
- https://github.com/paseo-cafe/paseo-cafe /apache2/202609/ts
  - https://paseo.cafe/
  - community driven directory of paseo.sh plugins

- https://github.com/getpaseo/paseo /13.4kStar/MIT > AGPL > apache2/202608/ts
  - https://paseo.sh/
  - Manage coding agents from your phone and desktop.
  - a self-hosted daemon for Claude Code, Codex, and OpenCode.
  - Agents run on your machine with your full dev environment. 
  - Connect from phone, desktop, or web.
  - [I built a fully self-hosted and open-source Claude Code UI for desktop and mobile : r/ClaudeCode _202602](https://www.reddit.com/r/ClaudeCode/comments/1r8rqnv/i_built_a_fully_selfhosted_and_opensource_claude/)
    - Git worktree management for running agents in parallel, Git operations so you don't have to leave the app, integrated terminal, it also comes with fully local voice mode and dictation
  - [I built an open source mobile and desktop app for OpenCode : r/opencodeCLI _202604](https://www.reddit.com/r/opencodeCLI/comments/1s9d7u6/i_built_an_open_source_mobile_and_desktop_app_for/)
  - [Relicensing Paseo from AGPL-3.0-or-later to Apache-2.0  _202608](https://github.com/getpaseo/paseo/issues/2982)
    - The goal is to make Paseo easier for individuals and organizations to adopt, integrate, redistribute, and build upon. 
  - [v0.7.0  _20260901](https://github.com/getpaseo/paseo/releases/tag/v0.7.0)
    - Changed the project license to Apache-2.0
  - https://github.com/blockfeed/paseo-selfhosted
    - A Docker build that runs the Paseo web UI and connects it to a self-hosted local daemon — no relay, no cloud, no app install required.
    - This is an unofficial showcase. It patches two files in the Paseo source at Docker build time and adds an nginx WebSocket proxy that makes the browser→daemon connection work. 
    - The Paseo web app is built as a static SPA (Expo web export). In its normal release form it only supports connecting to the official Paseo relay or a local desktop daemon via a Unix socket — it has no path for connecting a browser to a self-hosted TCP daemon. This repo makes it work with two changes
    - This repository contains only build tooling and documentation. The Paseo source code is fetched from getpaseo/paseo at build time 

- https://github.com/mcowger/amble /202609/ts
  - modern, high-performance web workbench for the Paseo autonomous coding agent daemon. 
  - Amble features Summary Mode—a dual-card visualization that aggregates tool executions into clear tallies on the left while streaming a formatted Markdown Thought Log on the right.
  - [Amble is an alternative client for the Paseo daemon : r/PaseoAI _202609](https://www.reddit.com/r/PaseoAI/comments/1w71k4j/amble_is_an_alternative_client_for_the_paseo/)
    - built using the Paseo SDK
    - alternative client with a more opinionated UI in certain aspects like how it shows the tool calls and context usage, just another flavor to chose from if that's your thing
- https://github.com/wangfh5/paseo-web-client /202609/js
  - zero-dependency web client for Paseo daemons — the official Paseo UI (same code as the desktop/mobile app) exported for the browser, plus KaTeX math rendering, served by a single ~120-line Node.js script. No Electron, no bundled daemon

- https://github.com/frogg-app/frogg /apache2/202609/ts
  - Frogg Development Environment: Tauri desktop client for remote AI coding agents (fork of Paseo)
  - Every client, one state. Desktop (Windows, macOS, Linux), web, Android and CLI see the same projects, timelines and permission requests, live.
  - Isolated workspaces. Git worktrees per task, with setup scripts and per-worktree services from frogg.json.
# paseo-alternatives
- https://github.com/vastsa/pi-desktop /4kStar/LGPL/202609/ts/rust
  - https://pi-docs.aiuo.net/
  - Local-first AI coding agent desktop: Electron + Rust host core + pi Agent Harness + user-installable plugins
  - [【PI-Desktop】两个月，300 亿 Token，终于把自己想要的 Agent 桌面端搓出来了 - LINUX DO _202609](https://linux.do/t/topic/2869113)
  - 插件系统
  - 模型配置
  - 会话导入
  - 内置 Agent / Plan / Goal 三种工作方式
  - Subagent 真正可见，而且可以用不同模型

- 
- 
- 
- 
- 
- 
- 
- 

# agent-provider
- https://github.com/Pheobe-Southwood/dsh-acp-paseo /MIT/202608/ts
  - 把 DeepSeek Harness（dsh）编码代理通过 ACP（Agent Client Protocol）接入 Paseo。
  - 用户把 dsh 添加为 Paseo provider 后，模型目录、凭据、模式、思考强度与斜杠命令全部从 dsh 侧自动发现，Paseo 端零配置。
# plugins
- https://github.com/omercnet/paseo-plugins /MIT/202609/ts
  - agent-monitor
  - agent-crew
  - paseo-omp
  - paseo-shared-browser: plugin that runs one real Chromium browser per workspace on the daemon host and shares that exact live session with every connected Paseo client. Version 1.0 replaces the previous browser runtime in place with a plugin-owned, pinned `agent-browser` runtime; 

- https://github.com/mcowger/paseo-plugins /MIT/202609/ts
  - Pi tasks timeline
  - Subagent activity
  - Reasoning display
  - Colorful agent activity

- https://github.com/panrafal/paseo-plugins /MIT/202609/ts
  - agents-dash-list — a sidebar list of workspaces grouped by what needs you: waiting, unread, in progress, failing
  - agents-history — every workspace and agent the daemon has ever had, including archived ones
  - schedule-runs — one feed of every schedule run: status, workspace, agent, archived state, and the agent's final response
  - session-usage — token, cache, cost, and activity stats for Claude, Codex, OpenCode, Kilo, and Devin CLI from local transcripts and session stores

- https://github.com/gpambrozio/paseo-plugins /MIT/202609/ts
  - github-board	A sidebar board of open issues, draft PRs, open PRs, and discussions
  - launchd-jobs	Schedules shell commands through launchd on the daemon's Mac 
  - herald	A sidebar panel of every agent waiting on you 

- https://github.com/lalaze/paseo-plugins /202609/ts
  - AI 协作（Director） 由你选择设计、执行和审核 AI，完成设计、实现、审核与验收协作。
  - 工作区文件传输面板：浏览目录树，上传下载当前 daemon 主机上的文件。

- https://github.com/koinzhang/paseo-plugins /202609/ts
  - activity	Local usage analytics and workspace agent ops (Explorer fleet list, live attention, terminals)

- https://github.com/geoqiao/paseo-stuff /202609/ts
  - Independent community plugins for Paseo: readable activity, DeepSeek Harness, math and pets

- https://github.com/sleeyax/paseo-plugins /apache2/202609/ts
  - Discord Rich Presence: Show your current Paseo activity on Discord.
  - Claude TTY: Offer the Claude TTY ACP adapter as a Paseo provider, and manage it on the daemon host.

- https://github.com/tomgrin10/paseo-defer /MIT/202609/ts
  - plugin for queuing a message to an agent and delivering it later.
  - 和paseo内置的 schedule 有什么区别

- https://github.com/Laokashouji/paseo-turn-changes /apache2/202609/ts
  - Paseo 插件，按一轮 Agent 执行汇总文件改动。在回答后显示文件数量、增删行数和文件列表，点击文件或“审核”查看当轮差异；“撤销”恢复这一轮之前的文件内容。
  - 纯插件模式依赖结构化文件编辑记录，无法完整追踪 Shell 直接写文件。
  - 记录不完整、工作目录外文件或文件已有后续修改时，不提供自动撤销；能获取的编辑内容仍可审核。

- https://github.com/itsjustanks/paseo-plugin-sync /MIT/202609/ts
  - plugin that syncs selected projects - git history, chat transcripts and workspaces - between two Paseo daemons.
  - Scope is per-project and opt-in. A project you have not selected is never read, never compared, and never touched.

- https://github.com/hsiangron/paseo-auto-sync /202609/ts
  - plugin that imports local Codex and Pi sessions whenever the Paseo client loads. It follows Gaseo's link-not-copy model: original JSONL transcripts remain in their provider directories, while Paseo stores the provider session handle needed to resume them.

- https://github.com/Vokturz/paseo-in-app-browser /202609/ts
  - A Chromium-powered browser surface for Paseo. Chromium runs on the Paseo daemon host and is controlled through the Chrome DevTools Protocol; Paseo clients display the remote viewport and forward navigation, clicks, swipes, typing, and common key presses.

- https://github.com/ThePlenkov/paseo-browser-plugin /MIT/202609/ts
  - plugin that adds a Browser workspace tab — a full Chromium browser running on the daemon host, streamed to the client via VNC/noVNC.

- https://github.com/ZackYJz/paseo-workspace-agent-count /202609/ts
  - 插件：随时看到每个 workspace 下有几个会话 —— Agent 总览页（只读）+ 可选标题前缀 (3) 原标题

- https://github.com/supermomonga/paseo-plugin-canvas /202609/ts
  - Open a workspace, then choose Open Canvas from the Command Center
  - Keep plans, notes, and review discussions in one place. Ask an agent to write a document, edit it yourself, and send comments back for another pass. Other agents in the same workspace can read and update the same canvas, even in separate sessions.

- https://github.com/lalaze/paseo-plugins /202609/ts
  - Selection Translate: Select text in a user message or AI reply and translate it in place. On iOS/Android a native "Translate" pill next to the composer translates a draft for sending or copying, or translates the latest AI reply
  - Pi Qwen thinking levels

- https://github.com/theTd/paseo-translate /202609/ts
  - Converse in your language while the agent works in another. Prompts are translated into the agent language before they reach the inner agent; replies stream back in the agent's own words and are translated in the app after each stream completes.

- https://github.com/Julesseg/paseo-deck /MIT/202609/ts
  - A multi-session terminal client for managing Paseo agents and workspaces
  - keyboard-first terminal client for managing several Paseo sessions at once. 
  - It presents projects, workspaces, and sessions as a navigable tree beside the active session's live timeline, with prompt composition, permissions, session creation, and lifecycle controls in one terminal screen.

- https://github.com/ZackYJz/paseo-workspace-cleaner /202609/ts
  - 硬删除 Agent、归档并清理 Workspace、统一停机删除已归档 Workspace 及其 Pi session（优先进废纸篓、引用感知）

## git

- https://github.com/ZFhuang/paseo-git-tree /MIT/202609/ts
  - plugin that draws the current workspace's branch history as a lane-based commit graph.
  - 💡 可参考迁移 git graph 相关功能

- https://github.com/huangcb01/paseo-git-graph /202609/ts
  - 在 Paseo 右侧 Explorer 中浏览 Git 提交拓扑、分支、标签和文件差异。插件跟随当前工作区，支持仓库子目录和 Git worktree。

- https://github.com/mentalfl0w/review-deck /202609/ts
  - Human-in-the-loop code review workspace for Paseo with inline file comments, project-level AI processing, and safe Git diff review.

- https://github.com/ImAnOwl/Paseo-Worktree-Status /MIT/202609/ts
  - Shows in a Paseo Worktee the current GIT status of the branch and worktree

## dev-pattern

- https://github.com/obetomuniz/auto-mode-for-paseo /MIT/202609/ts
  - plugin that routes each message to a persona on Codex, Claude, OpenCode, or any other installed provider.

- https://github.com/hypermemetic-ai/qq-workflows /202609
  - plugin for planning software changes with you, then researching, implementing, reviewing, and merging them.
  - Ticket-driven planning, in-session teaching, and deliberate delegation. One Architect, one worker runtime.

- https://github.com/denny64/paseo-github-kanban /MIT/202609/ts
  - Kanban board for Paseo backed by GitHub issues, with one-click agents per card.

- https://github.com/frailbongat/paseo-ship-check /202609/ts
  - Ship readiness for Paseo: the daemon checks the tree when a turn ends and drops a verdict card in the agent timeline, with a one-tap ship

## ui-plugin

- https://github.com/dbhq-uk/paseo-file-viewer /MIT/202609/ts
  - Read PDFs, images, Word documents and spreadsheets inside Paseo
  - Needs poppler-utils, imagemagick and librsvg2-bin on the daemon machine
  - Plugin client bundles may only import react, react-native, @tanstack/react-query, zod and @getpaseo/plugin. No pdf.js, no canvas, no gesture library. So the daemon does the work and the client renders the result.
  - PDFs and images are rasterised. pdftoppm renders one page at a time at a requested DPI
  - Word documents and spreadsheets are parsed, not rasterised. This is the design decision the plugin turns on
  - 在主编辑区上方的标签栏右侧，点击 + 号按钮，找到并点击 Viewer
  - 🐛 issues
    - 文本类pdf中的文字无法选中， 渲染效果是图片， 很模糊
    - docx不显示 分页、多栏布局 
    - 扁平化显示所有文件， 不显示文件夹结构

- https://github.com/ABorakati/beautiful-chat /MIT/202609/ts
  - plugin that redraws the Oh My Pi (OMP) chat stream: tool calls, reasoning, prompts, approvals, and checklists. It replaces the host rendering of OMP timeline items with typed, syntax-aware cards that follow the active Paseo theme.

- https://github.com/q5m-ai/beautiful-pi /202609/ts
  - A compact, polished timeline renderer for Pi agents in Paseo.

- https://github.com/AStox/paseo-chat-links /202609/ts
  - Paseo plugin that shows Linear tickets and GitHub PRs mentioned in a chat

- https://github.com/opsb/paseo-markdown-viewer /MIT/202609/ts
  - plugin that adds a read-only Markdown panel to every workspace. Open any markdown file in a tab, watch it update the moment it changes on disk, and let the panel follow the files your agents write.

- https://github.com/dutchakdev/paseo-plugin-mermaid /MIT/202609/ts
  - Render Mermaid diagrams inside the Paseo chat timeline

- https://github.com/tonyredondo/paseo-inline-review /202609/ts
  - plugin for commenting on agent responses inline and sending the comments back as a review.
  - Replaces each assistant response in the timeline with a paragraph view: tap a paragraph to attach a comment anchored below it. 
  - Adds a "Review (n)" composer pill for every agent that opens the plugin panel.
  - Comments persist in the daemon store and carry a status: pending comments are included in the next "Send to agent"; sent comments stay visible as muted conversation context (and can be re-opened).
  - The agent panel offers: Send to agent:

- https://github.com/infectiousstupidity/paseo-reasoning-display /202609/ts
  - plugin that replaces built-in reasoning rows with expandable Markdown cards and lets you control how reasoning blocks open by default.

- https://github.com/samgbafa/paseo-thread-board /MIT/202609/ts
  - A live Kanban and filterable list view of every coding-agent thread on a Paseo host.
  - Thread Board was informed by the Paseo community's Agent Monitor, GitHub Board, and Agents Dash. Agent Monitor's host-wide triage semantics and GitHub Board's responsive lanes were especially useful references. No existing plugin found during development combined live thread state with this focused Kanban workflow.
  - https://github.com/HankLeo/paseo-kanban /MIT
    - 以 session（agent 会话）为卡片粒度，聚合本机与远程 daemon 上的活跃会话，提供泳道 / 列表 / 甘特图三种可切换视图。主题自动跟随 Paseo app
  - https://github.com/breathi3552/paseo-kanban
    - plugin for Paseo with custom lanes, subtasks, project filtering, and drag-and-drop.

- https://github.com/xpufx/paseo /MIT/202609/ts
  - plugins/top/ — Live host system resource monitor, timeline telemetry
  - plugins/mcp-tools/ — MCP server fleet management and diagnostic plugin.
  - packages/paseo-plugin-helper/ — Shared runtime library for Paseo plugins (UI components, server utilities, RPC contracts, settings schema, and testing harness).

- https://github.com/custyhs/paseo-advanced-markdown /apache2/202609/ts
  - Renders math formulas and Mermaid diagrams inside assistant messages in Paseo 0.8.0
  - Chinese bold text and boxed equation borders are preserved.
  - mermaid fences rendered on the host with the pinned Mermaid CLI and a plugin-managed Chrome headless shell.
  - Copy TeX and original source, formula/diagram inspection, light and dark themes, and per-host size/module settings.

- https://github.com/q5m-ai/paseo-math /apache2/202609/ts/仅公式
  - Markdown and LaTeX rendering for math-bearing assistant responses in Paseo, with inline formulas, display equations, and a Copy source action that preserves the original Markdown and TeX.
  - Requires Paseo 0.8+ on both the host daemon and the client app; Paseo 0.7 is not supported. 

- https://github.com/kschniedergers/paseo-plugins /MIT/202609/ts
  - Renders !`[clip](/path.mp4)` in assistant messages as an inline video player — mp4, webm, mov, with audio. Mobile shows a placeholder card.

- https://github.com/Laokashouji/paseo-feishu-ui /MIT/202609/ts
  - Feishu-inspired light and dark themes for Paseo, with a desktop workspace layout, continuous assistant bubbles, compact tool cards, and first-line thinking previews.

- https://github.com/feixqemn/paseo-smooth-ui /202609/ts
  - A focused Paseo UI fork: inline reasoning, compact tool activity, Markdown messages and configurable file opening
  - It keeps the official Paseo 0.8.0 foundation and focuses on small, direct UI changes: predictable file opening, a compact reasoning and tool timeline, and Markdown that reads like Markdown.

- https://github.com/thisjrodriguez/paseo-plugin-clusters /202609/ts
  - plugin that groups your projects into clusters and puts them as circles above the workspace list, Discord-style.
  - Circles in the sidebar. A row above "New workspace". 

- https://github.com/frailbongat/paseo-composer-pills /202609/ts
  - Status pills in the Paseo agent composer track bar.

- https://github.com/midodimori/paseo-tool-ui-plugin /202609/js
  - Automatically expands Paseo's native Edit and Write tool cards on desktop and web, so their existing file details and diffs are visible.
  - Paseo provides all tool rendering, diffs, paths, and actions. This plugin only clicks the existing expansion controls; it does not create diffs or read or write your files. Reads, searches, shell commands, and other tools keep their usual behavior.

## prompt

- https://github.com/hungcuong9125/paseo-prompt-kit /MIT/202609/ts
  - PromptKit is a Paseo plugin that rewrites the prompt in your Composer before you send it. It adds a PromptKit pill to the Composer and a `/rewrite <prompt>` slash command. The rewrite replaces the Composer text in your own voice — first person, speaking to the agent — and keeps your language and every protected literal (URLs, absolute paths, shell commands, code blocks, model and tool names).
  - The rewrite runs one of three ways, chosen in Settings: the agent's own provider CLI with the model the Composer shows (the default), a provider CLI with a model you pick, or a direct request to an API you configure 

- https://github.com/yannelli/paseo-prompt-manager /MIT/202609/ts
  - Markdown prompt library for Paseo. Create, edit, search, and reuse prompts across agents, with local version history and optional Git sync.
- https://github.com/custyhs/paseo-drafts
  - Durable prompt drafts for Paseo, delivered as a plugin: write, plan, send, and search drafts that outlive every session
- https://github.com/AmaneRX01/paseo-plugin-prompt-studio
  - plaintext-first Paseo plugin for drafting, organizing, versioning, and safely dispatching prompts to agents.

## more-plugins

- https://github.com/AStox/paseo-model-bench /202609/ts
  - Paseo plugin. It turns the model picker into a score vs cost chart, so you can see what you're actually paying for before you switch models.
# examples

# providers

- https://github.com/itsjustanks/paseo-plugin-ai-router /MIT/202609/ts
  - route your agents through one AI router (OmniRoute) — providers, accounts, usage, settings, one provider with every model.
  - Routes the agents a Paseo daemon launches through one OmniRoute endpoint. It keeps an "AI Router" provider in Paseo with every model of your connected accounts

- https://github.com/xuruiye/paseo-cliproxyapi-providers /202609/ts
  - a Paseo direct Provider Plugin. It discovers Claude-compatible models from CLIProxyAPI and launches the local Claude Code CLI with the selected cloaked model ID.

- https://github.com/RUIIIOVO/paseo-usage-sidebar /202609/ts
  - provider plan usage as a sidebar surface, read from Paseo's own usage data
# utils
- https://github.com/lyhu/paseo-plugin-tunnel /202609/ts
  - Connect an HTTP or HTTPS service you manage to another trusted Paseo host through the Paseo Relay and end-to-end encryption. 
  - Manage each connection from the HTTP Tunnel entry in Paseo's sidebar.

- https://github.com/itsjustanks/paseo-plugin-daemon /MIT/202609/ts
  - Open a remote project's dev server from Paseo in one press.
  - See every dev server running on a host, press Open, and it appears in your browser.

- https://github.com/vercel-labs/paseo-vercel-sandbox /202609/ts
  - Run a Paseo daemon and a coding agent inside a persistent Vercel Sandbox, then connect from your existing Paseo client over Paseo's end-to-end encrypted relay.
  - The sandbox filesystem is preserved across stop and resume, so you can pick up where you left off. The daemon inside the sandbox never listens on a public port: clients reach it through the Paseo relay only.

- https://github.com/itsjustanks/paseo-fleet /apache2/202609/ts
  - Authenticated dashboard and declarative CLI for multi-space Paseo servers
  - The installer discovers existing Paseo services, shows the plan, optionally converges configuration and installs Team Presence, then offers the authenticated dashboard. 

- https://github.com/dutchakdev/paseo-plugin-machine-status /MIT/202609/ts
  - Machine dashboard, open ports and Docker control inside Paseo

- https://github.com/cleiter/desvio /apache2/202608/sh
  - Keep a personal build of someone else's project.
  - You have branches that upstream has not merged — open pull requests, changes that were rejected, things only you want. desvio merges them onto a fresh upstream in a worktree of your own checkout, resolves the conflicts, and runs your gate. What comes out is a build you can install and use every day, rebuilt in a minute when upstream moves.
  - 🍴 使用了paseo
  - 感觉很复杂， 学习成本太高， 慎用
  - Every run does the same thing: fetch upstream, recreate the integration branch from the base commit, merge each manifest branch in order, install, build, verify, and print what you got.
  - Why merge, not cherry-pick: A merge resolves once against a whole topic. Cherry-pick replays a branch commit by commit, so a branch that builds on itself conflicts with itself 
  - The first time a conflict appears, something has to resolve it. After that, git's `rerere` replays the same resolution on every rebuild, and most rebuilds spend no thought at all.
# devops
- https://github.com/Costben/paseo-statusbar-builds /202609/js
  - Automated CI that rebuilds getpaseo/paseo Android Universal (4-ABI: armeabi-v7a, arm64-v8a, x86, x86_64) APK from the latest non-draft upstream release with the edge-to-edge status bar fix applied, and publishes them to this repo's Releases.
  - This is a standalone build repo, not a fork. It stores only the workflow and the patch script. At build time it checks out an upstream tag, injects the patch, and compiles — it never stores or merges upstream source, so there are no merge conflicts to maintain.

- https://github.com/khoawatt/paseo-workflow-starter-guide /js
  - Small static website that teaches a new developer how to start using paseo-workflow.

- https://github.com/manziman/paseo-gateway /202609/ts
  - Independent Paseo-compatible Kubernetes gateway: isolated agent workspaces, schedules and headless automation.
  - Run isolated Paseo workspaces on Kubernetes and expose them as one host to an unchanged Paseo client. One TypeScript service contains the gateway and workspace controller. Workspace pods run the version-pinned upstream Paseo daemon.
# integrations
- https://github.com/wangfh5/paseo-feishu-seance /MIT/202609/ts
  - The bot is a remote prompt channel into your machine. Anyone whose messages reach the bot can drive the channeled agent with the agent's own permissions.
# relay
- https://github.com/itsjustanks/paseo-canvas-relay /MIT/202608/ts
  - Renderer-neutral canvases for Paseo: React apps, Mermaid diagrams, data notebooks, tldraw and Excalidraw, with agent-scoped tabs and a hosted or self-hosted sharing Relay.
  - Hosted setup and pairing instructions live at https://canvas.dev.yournet.space/setup.
  - https://github.com/itsjustanks/paseo-canvas /MIT/202608/ts
    - Live-render, share and send-to-chat everything your AI agents build — a Paseo plugin
    - Apps, notebooks, diagrams and boards built by agents — live inside Paseo, linked to the conversation, and shareable through a hosted or self-hosted Relay.

- https://github.com/getpaseo/paseo-relay /apache2/202608/elixir
  - distributed, protocol-compatible relay for Paseo

- https://github.com/keepmind9/paseo-relay /MIT/202605/go
  - A standalone Go relay server for Paseo, fully compatible with the original Paseo relay protocol (v1 and v2).

- https://github.com/zenghongtu/paseo-relay /AGPL/202608/go
  - A lightweight self-hosted relay server for Paseo.
  - The relay bridges your Paseo daemon and the mobile app when they can't connect directly. It forwards encrypted bytes without being able to read them — the relay is completely untrusted by design.
  - All traffic between daemon and app is E2E encrypted with XSalsa20-Poly1305 (NaCl box). The relay sees only IP addresses, timing, message sizes, and session IDs — never the content.

- https://github.com/chenmijiang/paseo-relay-selfhost /MIT/202606/ts
  - Self-hosted Node.js relay compatible with paseo's zero-knowledge relay wire protocol. 
  - A low-latency, self-hostable alternative to relay.paseo.sh.
# more
