---
title: lib-aikit-paseo-dev
tags: [agent, paseo]
created: 2026-09-05T00:27:22.306Z
modified: 2026-09-05T00:27:42.212Z
---

# lib-aikit-paseo-dev

# guide
- pros
  - license: apache2
  - remote control: local server, remote server
    - webapp添加本地paseo app作为host后，可以直接从web控制本地电脑
    - 移动端登录时会自动同步workspace/session
    - 👀 如果要通过webapp控制本地的paseo app, 需要手动修改配置 daemon.cors.allowedOrigins
    - zcode的webapp不支持添加 remote connection
  - existing coding agents, use it  on your own device
  - providers: Bring your own
  - plugins: add server-side functionality, modify the client with custom components
  - parallel work with optional git worktree: Per-worktree services. Each worktree gets allocated ports for dev servers and databases, 
  - automation: cli, mcp
  - browser tools
  - hub integrations: github, slack, discord
    - 类似openclaw, 但能让agent操作云端资源
    - 采用类似github workflow .yaml的设计，对普通用户不友好, 但对agent友好
  - Can I get banned for using Paseo? Paseo is designed to use each provider's officially supported integration and does not attempt to bypass its terms of service
  - 支持使用其他agentt的功能: 
    - 其他agent的skills
    - codex的computer-use
  - connection
    - Connect to remote daemons over SSH 

- cons
  - sync的功能不够强: 如何让云端设备与本地设备同步
  - Paseo manages other agents, it doesn't ship one.
  - 依赖用户本地的环境， 如果用paseo之前的agent没配置好， 那也需要先配好再用paseo
  - 适合个人用户私有化部署, 但不适合作为saas对外提供， 因为自定义host需要支持存储/计算/git操作/开发环境...
    - 一个host似乎只能一个用户使用， scale成本太高
    - By delegating to `gh` and `git`, Paseo automatically inherits your existing developer setup
    - 🤔 可尝试将用户本地的secrets复制到云端， 这种方案好吗
  - 不方便使用多账号, 这是设计目标的取舍
  - local隔离模式下, 不支持历史记录
  - 在paseo的web-terminal(xtermjs)中执行 `git pull` 会出现异常，但ssh到vps的repo目录执行pull可以成功
  - ux
    - webapp不支持很多桌面端的快捷键

- [features](https://paseo.sh/docs/why)
  - clients: The native mobile app has full feature parity with desktop.
  - integrations: GitHub, Slack, Discord
  - Voice runs locally on your device by default
  - You can use the hosted relay (end-to-end encrypted, Paseo can't read your traffic), set up your own tunnel (Tailscale, Cloudflare Tunnel, etc.), or expose the daemon port directly. 

- tips
  - paseo放在docker容器运行时注意设置最大cpu/ram, 会影响多agent和subagent并发运行, 有些agent可能占用较多ram如claude-code
# issues
- 不同vps上的同一git仓库，似乎会覆盖/合并为一个， 不能同时使用

- 在paseo的web-terminal(xtermjs)中执行 `git pull` 会出现异常，但ssh到vps的repo目录执行pull可以成功

- 
- 
- 
- 

- 是否支持daemon主机上的port forwarding, 比如运行webapp然后直接暴露
  - https://github.com/itsjustanks/paseo-plugin-daemon  /cf-tunnel/relay/ssh-forward
  - Open a remote project's dev server from Paseo in one press.
# aichor
- aichor as paseo bundle
  - paseo + custom-agent + ocr-skills + ui

- architecture
  - 能否通过 skills + ui plugins 的方式提升复用性
  - 也可考虑使用paseo sdk开发自定义前端， 类似amble

- non-goals
  - less multiple-agent collab
# draft
- usecases
  - work/doc, code, design
  - mobile远程控制pc
  - 远程控制时使用pc上的computer-use

- agent-base
  - built-in agent: 这样移动端可以直接执行agent，而不依赖桌面端或外部agent
  - external: deepseek-harness, cursor-cli, commandcode

- 与im平台的集成，类似openclaw
  - telegram
  - qq

- cowork/workbuddy-like
  - implement integrations for google-docs/msoffice/lark like github/gitea

- rag
  - qmd

- local folder as project/workspace

- sandbox

- browser-use
  - 参考开源的zcode

- computer-use
  - 参考开源的zcode
  - 参考 pi computer use

- paseo-relay server
  - ts, go

- cloud的易用性改进
  - chat history
  - project快速跳转到github repo, workspace快速跳转到branch
  - chat-turn-mark + content-toc

- transparency
  - show thinking/tools

- github-integrations
  - 支持现有github cli的设计， 同时支持github oauth登录来选择repo

- version-history for non-git folder
  - like git panel

- 
- 
- 
- 
- 

- sync
  - ?

- integrations
  - qq
  - telegram
  - 支付系统接入ldc

- paseo-hub
  - 用 n8n/activepieces 替代

- voice
  - toggle speech models

- 
- 
- 

## remote-control

- 远程控制的交互不够自然
  - 可参考 zcode, uu远程

## mobile-agent

- mobile agent xp
  - 桌面版的agent过于复杂

## browser-use

- headless browser-use
  - 可以在不打开文件的情况下编辑修改(vibe coding就是这样不看代码)

- 🤔 editor + browser-use, 大部分数据都在editor的数据结构中， 是否有必要实现browser-use
  - 缺乏统一标准的ui, 如office/wps的排版不同, 此场景也可用computer-use来解决
  - 缺乏统一标准的ux, 难量化的场景， 比如统一调整元素样式、主题
  - adhoc类型的场景如 表格数据计算、公式计算 
  - 多个tab时，能获取用户当前的位置
  - 也许不需要browser-use
    - 能让用户选择元素
    - highlight/cite web page content
    - link preview, 类似wikipedia的预览链接内容

- Paseo has NO headless CLI browser
- Paseo uses Electron WebContents directly (via Electron's built-in `contents.debugger` CDP and native input events). It does NOT use Playwright in its runtime.
  - directly employing CDP and native input events within its desktop application
  - Native Input Simulation: mouse moves, clicks, and drags are sent via CDP, while keyboard inputs use Electron's contents.sendInputEvent
- Turn-by-turn LLM Loop
  - Every navigation, snapshot, click, and wait requires an individual LLM inference round-trip.
  - The agent only has discrete MCP tools (browser_snapshot, browser_click, browser_scroll).
  - This consumes massive token budgets, incurs huge latency (several minutes), and increases the chance of the LLM losing context
- Ephemeral element refs (@e1, @e2) from the latest snapshot; mutates goes stale on DOM change.

- Paseo's interaction model operates through granular tools and a turn-by-turn LLM loop, each step demanding LLM inference. 
  - Conversely, ZCode employs a single code execution engine, allowing LLMs to script browser interactions programmatically. This highlights ZCode's potential for more efficient and complex web scraping tasks due to its programmatic flexibility.
  - ZCode's single-turn script execution capability provides a key advantage for complex browser interactions, encompassing loops and error handling in a single operation. 
  - Paseo's reliance on turn-by-turn LLM inference for each tool interaction results in increased overhead.

- Paseo's desktop-dependent architecture and use of a tethered host limits its environment compatibility, unlike ZCode's dual-mode headless operation. This difference fundamentally impacts deployment options.

- Paseo's `browser_snapshot` is engineered for UI accessibility testing. It transforms the page into an ARIA tree. Unlabelled `<div>` tags, custom table layouts, metadata, JSON-LD, and CSS attributes are intentionally flattened or dropped to keep tokens low for human UI interactions (buttons, textboxes).
  - ZCode's Playwright integration allows full query selector power

- While ZCode and Paseo both automate an Electron browser using WebContents and the Chrome DevTools Protocol (CDP), their implementations are completely separate codebases
- Both teams had the exact same technical constraint: Electron cannot natively use Playwright out-of-the-box without launching an external Chromium browser or exposing unsafe remote debugging ports
  - To solve this, both projects used Electron's built-in contents.debugger (CDP 1.3) and borrowed ideas from Microsoft's Playwright (Apache-2.0) to make WebContents automation robust and stable.
- PASEO DESKTOP 
  - Agent calls MCP: browser_snapshot ──▶ returns ARIA accessibility tree with @ref
  - Agent calls MCP: browser_click("@e3")
  - Handcrafted ARIA script injected into page (adapted from Playwright concepts).
  - Dispatches mouse click via CDP `Input.dispatchMouseEvent`.
  - Paseo wrote a ~300-line custom script adapted from Playwright's ARIA tree concept
  - The agent never writes CSS or XPath selectors. The agent must pass @e3 to browser_click. If the DOM mutates between turns, the ref invalidates
  - Text is entered either via CDP Input.insertText or Electron's native sendInputEvent
- ZCODE DESKTOP 
  - Agent writes JS: await tab.playwright.locator("button.save").click()
  - Dynamically extracts real Playwright's compiled `injectedScriptSource.js`.
  - Creates CDP isolated world (`zcode-playwright-locator`).
  - Evaluates full CSS / XPath / Role selectors using Playwright's strict mode engine.
  - Dispatches input via CDP or Virtual Clipboard (for fast text paste). 
  - Direct bytecode/source extraction from playwright-core
  - ZCode locates `injectedScriptSource.js` on disk, parses the string literal using Node vm.runInNewContext, caches it, and injects it directly into Electron
  - Uses Playwright's real internal selector parser
  - Elements are resolved dynamically at runtime with Playwright's strict mode
  - In addition to standard typing, ZCode implements a Virtual Clipboard
  - LRU Tab Eviction & Residency: Automatically parks background tabs to conserve memory when too many tabs are open
  - Built-in Video Recording: Directly records tab interactions into .webm video streams

- 
- 
- 
- 
- 

### [zcode browser-use](https://zcode.z.ai/cn/docs/browser-use)

- 浏览器面板 仅桌面端可用。
- Agent 默认只操作自己打开的标签。你手动打开的那些它不会动，要接管其中某一个，需要先显式认领。
  - 在后台运行的会话不会抢占你正在看的界面——只有当前这个工作区在前台时，它的浏览器操作才会显示出来。
- 另外，Agent 操作网页和它改文件、执行命令一样受 执行模式 约束。涉及会真正提交数据的页面时，用「变更前确认」会更稳妥。
  - 暂时不能上传文件。 需要选择本地文件的表单环节它做不了，这一步得你自己来。

- ZCode can run completely headless in the background on remote Linux servers, Docker containers, or terminal sessions via `zcode --browser-use=headless`.
  - ZCode utilizes Electron WebContents for its desktop app and Playwright with CDP for its CLI
  - Built-in standalone headless CDP runner for CLI, servers, and CI
  - Full DOM & Playwright Locators: css selectors, XPath, aria
  - controls Electron WebContents / WebContentsView instances embedded directly in the desktop workspace UI.
  - cli launched via `--browser-use=headless`. It spawns a headless Chromium process driven by playwright-core using direct Chrome DevTools Protocol (CDP) sessions
  - Agent Entry Point: The agent does not get separate single-step MCP tools for clicking or navigating; instead, it uses the @zcode/node-repl-host (js tool) to run JavaScript scripts that call await agent.browsers.get("iab") or await agent.browsers.get("cdp"), giving the agent a comprehensive Playwright-style API facade.
- relations/differences of desktop/cli
  - follow a "Shared Contract & Client Facade, Divergent Execution Backends" architecture
  - control-browser/SKILL.md is shared across both environments
  - Commands sent from the agent are serialized into the exact same JSON format: BrowserCommand
- CLI Backend (cdp): Native Playwright 
  - The CLI uses real playwright-core. it launches a headless Chromium instance. 
  - When the agent calls tab.playwright.locator("button").click(), CLI simply forwards the call directly to Playwright's native methods
- Desktop Backend (iab): Emulated Playwright on Electron
  - Electron WebContents cannot be directly wrapped by Playwright without opening external debugging ports and spawning remote sessions.
  - ZCode reverse-engineered and re-implemented Playwright's core selector and snapshot logic inside Electron
  - Desktop creates an isolated JavaScript world via CDP, injects Playwright's script into it, and compiles selectors
  - It then simulates clicks and keypresses using Electron's native input pipeline
- Duplicated Code & Logic  
  - DOM Snapshotting (snapshot.ts vs browserCommandScripts.ts) 
  - Element Inspection (elementInfo)
  - Visual Highlighting Overlays (elementScreenshot) 

- "Browser Automation / Use" (浏览器自动化) Works in BOTH Desktop and CLI: 
  - The actual automation engine—navigating pages, clicking, typing, taking DOM snapshots, and running Playwright scripts—is fully implemented in the CLI as a headless CDP runtime
  - ZCode even bundles the runtime assets for playwright-core and the browser-use plugin so that the single-executable binary (npm run sea) can extract and run headless Chromium on Linux servers
  - In the CLI, browser automation is disabled by default. Chromium is heavy (~300MB RAM, CPU overhead). headless browser requires external OS binaries (chromium-browser or google-chrome) and Linux system libraries (libnss3, libgbm1, etc.) that are rarely present on a bare Linux server.
  - ZCode is commercially marketed by Zhipu as a Desktop AI IDE, less cli features

- ZCode's CLI adapter checks for an installed Chromium binary at /usr/bin/chromium or chrome
  - It boots a headless Chromium instance via playwright-core. 
  - The AI agent executes JavaScript in node_repl calling agent.browsers.get("cdp").
  - The agent writes and runs real Playwright scripts in memory to navigate, scroll, click, evaluate DOM, and save extracted JSON/CSV directly to your VPS disk.
- Run in tmux: Always launch inside tmux new -s zcode so long scraping tasks keep running after you disconnect your SSH session.

- 
- 
- 

## computer-use

- 暂无内置实现， 可用外部agent提供的 computer use

- 
- 
- 
- 
- 

## relay

- desktop app 不支持添加多个relay
  - ~/.paseo/config.json 的 `relay` 属性值不是array
  - 当前的实现, 修改relay server url后, 因为server id不变, 旧的relay配置直接被新的relay配置覆盖了

- 
- 
- 
- 
- 

## ux

- paseo daemon pair 让移动端扫码的ui

- thinking content height
  - thinking内容的markdown未渲染为富文本元素

- 更明显的relay引导和提示

- 
- 
- 

## terminal-hiding

- git operations
  - commit/push/pull 性能很差, 有时必须ssh到vps执行命令才成功

- 
- 
- 
- 
- 

## windows

- powershell

- 
- 
- 

# dev-xp
- use webapp to control native app
  - 如果要通过webapp控制本地的paseo app, 需要手动修改配置 daemon.cors.allowedOrigins
  - ws://localhost:6767/ws means the browser is talking to the daemon on your Mac directly.  JavaScript running in Chrome opened a WebSocket directly to the Paseo daemon listening on your Mac.
  - Chromium implements the W3C _Secure Contexts_ specification, which explicitly designates `127.0.0.1` and `localhost` as **"potentially trustworthy origins"** (loopback exception).
  - Apple's WebKit takes a strict security stance and **does not grant a mixed-content exemption to `localhost` ** . An HTTPS origin is **strictly forbidden** from loading any unencrypted subresources ( `http://` or `ws://` ).
  - If you want to use Safari instead of Chrome/Edge, you cannot use an unencrypted `ws://localhost` connection from an HTTPS site.
  - Use Paseo's Encrypted Relay (Recommended for Safari)
  - paseo daemon pair --relay

- Daemon Spawns the Pi Subprocess
  - pi --mode rpc --model gemini-3.8-flash --thinking high --extension /tmp/paseo-ext-...
  - It spawns the `pi` binary as a child process with its working directory set to your workspace
  - Communication is handled through `JsonlRpcProcess` using newline-delimited JSON over `stdin` and `stdout`.
  - Coding agents like Pi execute tools locally in their working directory. As Gemini instructs Pi to perform actions, Pi outputs JSON-RPC events on `stdout`

- https://github.com/myysophia/paseo-best-practices
  - Linux 服务器部署：ARCHITECTURE → USAGE → OPS → ADR
  - macOS 桌面 App：MACOS_DESKTOP → USAGE → ARCHITECTURE
  - 把历史 Codex / Claude 会话迁到 Paseo：SESSION_MIGRATION → USAGE

- Project: The top-level logical repository or root codebase.
  - Does not execute code directly.
  - It is simply the parent anchor that groups checkouts and workspaces together.
- Workspace: A concrete working directory (`cwd`) + Git branch/worktree + terminals + dev servers. A concrete filesystem directory (`cwd`) on a specific machine, with its own Git state and dev environment.
  - `local_checkout`: The main repository directory on disk.
  - `worktree`: A dedicated, isolated Git worktree automatically created by Paseo (under `~/.paseo/worktrees/<name>`) on an isolated branch.
  - `directory`: A plain directory (for non-Git codebases).
  - **Workspace scripts / background services** (e.g., dev servers defined in `paseo.json`).
  - **File explorer & changes tree** .
  - Tabs: Contains one or more agent sessions, terminal tabs, diff viewers, and browsers.
- Session / Agent Session: One active AI agent conversation (Claude, Codex, Pi) running in that directory.
  - equivalent of the "chat/conversation" in Claude Code or Codex.
  - In Paseo's code, "Session" also sometimes refers to the low-level WebSocket connection in `session.ts`, which is why the UI and docs standardize on **Agent Session** or **Agent** for the user-facing chat.

- why workspace
  - 🌹 By introducing Workspaces (especially Git worktrees): Paseo lets you spin up a new workspace in one click. Agent 1 works in Worktree A, Agent 2 works in Worktree B. Both belong to the same **Project** , but their files and Git branches are isolated.
  - Multi-Agent Collaboration in the Same Workspace: Tab 1 Claude Code , Tab 2 codex. Because **Workspace** is the environment container, you can switch providers or have multiple agents and terminals cooperate on the same working tree.

- paseo relies on the host system's **GitHub CLI (`gh`)** and local **Git configuration** (SSH keys, Git credential helper, or PAT).
  - Local-First & Zero Credential Relaying: Paseo never stores, relays, or refreshes GitHub OAuth tokens or client secrets on its servers or across remote devices.
  - Environment Inheritance: By delegating to `gh` and `git`, Paseo automatically inherits your existing developer setup: 适合个人用户，不适合服务端
  - No Centralized Cloud Proxy: your machine communicates directly with GitHub.
- Paseo abstracts Git hosting platforms under a **Git Forge** layer (which supports GitHub, GitLab, Gitea, Forgejo, and Codeberg). GitHub is implemented as an adapter in this forge registry.
- clone from github
  - gh auth status
  - **Repository search:** Runs `gh repo list --json ...` for user repos or `gh search repos <query>` for public repos.
  - daemon executes `git clone <url> .paseo-clone-<temp>`
  - gh pr view <number> --json ...

- There is one place where a **GitHub App is used**: **Paseo Hub** 
  - Hub uses environment variables to receive GitHub webhooks and mint scoped installation access tokens.

- you can add your local Mac as a host to the web app running at `https://aichor.aichorage.de`, but it requires using Paseo's **Encrypted Relay** (or an HTTPS tunnel) rather than a direct `localhost` connection, due to web browser security policies.
  - because you already installed the Paseo Mac App, you can also do the reverse (and often much better) setup: add your VPS to your Mac App.

- Paseo is designed to run concurrent workspaces and worktrees in parallel without port conflicts.
  - Dynamic Port Allocation: When "port" is omitted from paseo.json, Paseo allocates an available ephemeral TCP port per workspace.
  - Environment Variable Injection: Paseo injects PASEO_PORT (and HOST=127.0.0.1) into the script's environment.
  - Unique Proxy URLs: Each workspace (on separate branches) gets a unique hostname (e.g. http://dev--feature-a--react-starter-rspack.localhost:6767), proxying requests to that workspace's assigned PASEO_PORT.
- Paseo gives each service an isolated proxy hostname based on its branch name

- Git itself enforces a fundamental safety rule: a local branch can only be checked out in one working tree at a time.

- 
- 
- 
- 
- 
- 
- 
- 
- 

# more

# docs
- Paseo follows a client-server architecture, similar to Docker. 
  - The daemon runs on your machine and manages your coding agents. 
  - Clients (the mobile app, CLI, or web interface) connect to the daemon to monitor and control those agents.
- The Paseo daemon can run anywhere you want to execute agents: your laptop, a Mac Mini, a VPS, or a Docker container. 
- Clients connect to the daemon over WebSocket. There are two ways to establish this connection:
  - Relay connection (recommended), The daemon connects outbound to our relay server, and clients meet it there. No open ports required.
  - Direct connection, The daemon listens on a network address and clients connect directly.

- The Paseo CLI lets you manage agents from your terminal. It's the same interface exposed by the daemon's API, so anything you can do in the app you can do from the command line.
  - You can tell coding agents to use the Paseo CLI to spawn and manage other agents. 
  - CLI-created workers get the same workspace and parent defaults as MCP-created workers.
- The CLI is designed to be used by agents themselves. You can instruct an agent to spawn sub-agents for parallel work

- You'll also want the GitHub CLI (gh) installed and authenticated, Paseo uses it for PR-aware worktrees and a few orchestration features.

- A project can be a git repository, a GitHub project, or any directory on a machine running the Paseo daemon.
  - Inside each project are workspaces. 
- Paseo is organized around workspaces, not chats.
  - A workspace is the place where a task happens. It has a working directory and can contain multiple sessions running at the same time. In the app, each session opens as a tab.
  - Each workspace is a separate place to work. You can keep one for your main checkout, create another for a feature, or open a GitHub PR as another workspace.

- Agents run inside a workspace as sessions. A workspace can have one agent session, several agent sessions, terminals, browsers, and diffs open at the same time.

- The workspace is the product concept; a git worktree is one way to isolate its files. More than one workspace can refer to the same managed worktree, and Paseo removes that worktree after its last workspace is archived.

- Every workspace in Paseo is backed by a working directory. When that directory is a git worktree, you get a separate branch and isolated environment for each task.
- When a workspace is backed by a git worktree, Paseo creates a separate directory on a separate branch so parallel agents never step on each other.

- A provider is the contract between Paseo and one external agent CLI: how to launch it, how to stream its output, how to send input back, what modes it supports. The actual binary lives on your machine and runs as a normal subprocess.

- Paseo ships a bundled adapter for the major agents (Claude Code, Codex, OpenCode, pi). Auto-discovered when the underlying CLI is installed, with mode metadata and voice support where applicable.
- any agent speaking the Agent Client Protocol is supported through a generic adapter. Paseo ships a curated catalog of one-click installs 

- A schedule starts a new agent for you on a cron cadence: at this time, run this prompt, in this repo, with these agent settings.
  - Schedules create a new agent each run. You can inspect, pause, resume, run once, update, or delete them.
  - Heartbeats target one existing agent. They are intentionally lightweight: create or delete them over MCP; from the CLI you can also update only their cron period. A heartbeat sends a recurring prompt back into one existing agent so it can reassess and continue the same conversation.

- The most important difference from native subagents is that Paseo subagents can cross provider boundaries.
  - Native subagents belong to one provider. Claude Code launches Claude Code subagents; Codex launches Codex subagents. 
  - Paseo subagents are full agents managed by the Paseo daemon. The orchestrator can choose any configured provider and model, keep the worker in the current workspace, or place it in another workspace created for the task. Use them when you want one model to plan, another to implement, and another to review.

- Agents in Paseo can drive real browser tabs — the same tabs you see in the Paseo desktop app. 
  - An agent can open your dev server, read the page, click through a flow, fill a form, and take a screenshot, all without leaving your machine.
  - Browser tools let agents access and control Paseo browser tabs, including logged-in browser state. Only enable this for agents you trust.
- Desktop only, for now: Browser tabs are hosted by the Paseo desktop app. The daemon itself doesn't run a browser — it routes tool calls to a connected desktop app, and returns an error when none is connected. The wire contract is host-neutral, so other hosts can carry the same tools later.
  - Reach for Playwright or agent-browser when the browser work stands on its own — headless CI runs, an existing test suite, or automation that isn't tied to an agent session in Paseo.
- How an agent sees a page
  - The primary tool is `browser_snapshot`, which returns the page as an accessibility tree — headings, text, form state, and hierarchy — instead of raw HTML
  - For anything the tree can't capture, agents fall back to `browser_screenshot`, and browser_logs exposes console messages and network timing.
  - agent ──MCP──▶ daemon (broker) ──▶ browser host (desktop app) ──▶ webview
  - Navigation is restricted to http(s) URLs.

- A daemon runs agents on one machine, for you. Paseo Hub is the layer above your daemons. 
  - Your daemons keep running agents where they always did. Hub decides when to ask them to.
- A daemon is one of your machines running the Paseo daemon. Enroll it once with your Hub organization, then any project can reference it.
- For agents it dispatched, Hub owns creation, reconnect recovery, output observation, and completion. Agents you start yourself are untouched.
- A workflow file contains one trigger and the ordered steps it starts. Files are discovered from .paseo/workflows/*.yml.
- A trigger says which provider event can start a workflow. The Hub workflows page covers the steps, inputs, routing, prompts, and deadlines that run after a match.
- Every event Hub accepts is recorded, whether or not it ran anything. That record is how you debug a trigger.

- Hosted Hub uses the same projects, workflows, daemons, and activity model.

- Do I need Hub to use Paseo?
  - No. Paseo runs agents on your machines without it. 
  - Hub adds what a single daemon cannot do on its own: starting agents from external activity, versioned configuration, a shared record of what ran, and team access.

- 
- 

- Connectivity
  - SSH: SSH transport connects to an existing daemon through your local OpenSSH client.
  - Paseo relay: works without Tailscale, port forwarding, or network configuration
  - Tailscale: Install Tailscale on the daemon machine and your phone. Sign in to the same tailnet on both devices.

- Relay connections
  - The relay is the simplest way to connect from your phone. It requires no VPN setup, no port forwarding, and no firewall configuration. 
  - The daemon can stay bound to localhost or a socket file, it connects outbound to the relay, and your phone meets it there. 
  - The official relay server is the open-source Elixir service at getpaseo/paseo-relay.
  - The relay is designed to be untrusted. All traffic between your phone and daemon is end-to-end encrypted. The relay server cannot read your messages, see your code, or modify traffic without detection. Even if the relay is compromised, your data remains protected.
- Relay is off on new installations. 
  - Choosing not to enable relay leaves the daemon available for direct TCP, Tailscale, or other VPN connections and does not create a pairing QR code. 

- Direct connections
  - By default, the daemon listens on 127.0.0.1:6767 (localhost only). 
  - For maximum isolation, you can configure the daemon to listen on a Unix socket file instead of a TCP port. This prevents any network access entirely, only processes on the same machine can connect. The CLI supports this mode, but the mobile app and web interface require a network connection.

- The official Paseo Docker image runs the daemon and serves the bundled browser UI from the same HTTP origin. 
- The official Docker image runs the daemon and bundled web UI in one container. 
  - It binds to 0.0.0.0:6767 inside the container so Docker port publishing and reverse proxies work normally.

- 
- 
- 
- 
- 
- 
- 
- 
- 
