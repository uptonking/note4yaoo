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
    - 移动端登录时会自动同步workspace/session
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

- cons
  - Paseo manages other agents, it doesn't ship one.
  - 不方便使用多账号, 这是设计目标的取舍

- [features](https://paseo.sh/docs/why)
  - clients: The native mobile app has full feature parity with desktop.
  - integrations: GitHub, Slack, Discord
  - Voice runs locally on your device by default
  - You can use the hosted relay (end-to-end encrypted, Paseo can't read your traffic), set up your own tunnel (Tailscale, Cloudflare Tunnel, etc.), or expose the daemon port directly. 

- tips
  - paseo放在docker容器运行时注意设置最大cpu/ram, 会影响多agent和subagent并发运行, 有些agent可能占用较多ram如claude-code
# draft
- agent-base
  - built-in agent

- cowork/workbuddy-like
  - implement integrations for google-docs/msoffice like github/gitea

- sandbox

- paseo-relay server
  - ts, go

- cloud的易用性改进
  - chat history

- transparency
  - show thinking/tools

- 
- 
- 

- sync
  - ?

- integrations
  - qq
  - telegram

- 
- 
- 
- 

# dev-xp
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
  - The tools are part of the Paseo MCP toolset, so Enable Paseo tools on the same page must also be on for agents to receive them. 
  - Browser tools let agents access and control Paseo browser tabs, including logged-in browser state. Only enable this for agents you trust.
- Browser tabs are hosted by the Paseo desktop app. The daemon itself doesn't run a browser — it routes tool calls to a connected desktop app, and returns an error when none is connected. The wire contract is host-neutral, so other hosts can carry the same tools later.
- How an agent sees a page
  - The primary tool is `browser_snapshot`, which returns the page as an accessibility tree — headings, text, form state, and hierarchy — instead of raw HTML
  - For anything the tree can't capture, agents fall back to `browser_screenshot`, and browser_logs exposes console messages and network timing.
  - agent ──MCP──▶ daemon (broker) ──▶ browser host (desktop app) ──▶ webview

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
