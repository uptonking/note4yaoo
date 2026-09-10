---
title: lib-aikit-paseo-codebase
tags: [codebase, paseo]
created: 2026-09-05T00:28:07.776Z
modified: 2026-09-05T00:28:18.805Z
---

# lib-aikit-paseo-codebase

# guide

# architecture
- 各 provider 会话格式互不兼容（Claude 的 JSONL ≠ Codex 的 rollout），Paseo 选择不转换格式，用文本作为通用格式
  - 显式文本交接优于隐式迁移。
- update_agent 只能改 model/thinking/mode，不能换 provider —— 换 provider 必然是新会话
# server

# agent
- Native（原生内置）Provider 绝大部分不是通过 ACP Adapter 实现的，而是各自针对该 CLI 的私有协议、官方 SDK 或专有 IPC 单独实现的；唯一的例外是 GitHub Copilot。
  - native providers are not supported through ACP adapters. With the single exception of GitHub Copilot, native providers are implemented separately and differently, using bespoke transports, proprietary SDKs, and custom IPC channels.

- The shared contract: where "native" and "external" meet
  - `AgentClient` — create/resume sessions, fetch catalog (models + modes), availability checks, list commands/features, import sessions
  - `AgentSession` — startTurn, subscribe (stream events), setMode, setModel, respondToPermission, interrupt, revertConversation/revertFiles/revertBoth (rewind), etc.
  - `AgentManager` and the WebSocket layer only ever talk to this contract, so from the daemon's perspective a native Claude session and an ACP Gemini session are indistinguishable. There's even a shared turn runner (`providers/provider-runner.ts`) all providers use to collect timeline/usage/final-text from a turn

- Provider 的接入被明确划分为两种截然不同的范式：
1. **Direct（直接实现模式）** ：
    - 包含： **Claude Code**、**Codex**、**OpenCode**、**Pi**、**OMP** 。
    - 它们各自通过专有的方式与对应的底层 CLI 进程通信（官方 TypeScript SDK、专有 JSON-RPC 2.0、HTTP/SSE 守护进程、JSONL 等），完全不走 ACP。
2. **ACP（Agent Client Protocol 适配器模式）** ：
    - one ACP base class, configuration-as-subclass
    - 包含： **GitHub Copilot**（虽然它是内置的，但官方 CLI 原生支持 ACP），以及**外部 Agent 目录（Cursor、Gemini CLI、Hermes、Kimi、Cline、Qwen Code 等 25+ 款）** 与用户通过 `config.json` 添加的任何自定义 ACP Agent。
    - 它们统一复用 Paseo 封装的 ACP 通信层（`ACPAgentClient` / `GenericACPAgentClient`）。
    - note: a custom provider with `extends: "claude"` (Z.AI, Alibaba Qwen) doesn't go through ACP at all — it *reuses the native Claude client* with a different `ANTHROPIC_BASE_URL` and env, which is why it inherits Claude's full native feature set.

- Paseo 的核心设计目标是： **在底层用各自不同的技术对接不同 Agent，但在顶层将它们抹平为统一的 `AgentClient` 和 `AgentSession` 抽象接口** ，从而让前端（移动端/网页/桌面）拥有统一的聊天交互、权限审批和流式输出体验。

- 各个 Native Provider 的实现原理截然不同
- Claude: ClaudeAgentSDK, claude CLI
  - in-process `query()`, not a spawned CLI
  - Managed via the SDK's `query()` factory (`query.ts`). Paseo spawns the `claude` subprocess through the SDK wrapper.
  - **Native Features** : Directly controls Claude's native `allowedTools`,                        `disallowedTools`, extended thinking tokens, UltraCode mode, and token compaction.
- Codex: stdio JSON-RPC, codex app-server 
  - proprietary __app-server JSON-RPC over stdio__, via a custom transport
  - Spawns `codex app-server` as a long-running subprocess.
  - Directly bridges Codex's OS sandbox modes (`sandbox_workspace_write`, writable roots, network proxy settings) and approval policies (`auto-review`,                      `full`).
  - **Native Features** : Supports conversation branch rollbacks, thread forks, and Codex Goals.
- OpenCode: HTTP/SSE Client, opencode server
  - HTTP __server API__ + a Paseo-authored __bridge plugin__ injected into OpenCode 
  - HTTP REST + Server-Sent Events (SSE) via `@opencode-ai/sdk/v2/client`.
  - Managed by `OpenCodeServerManager`, which starts and maintains an `opencode server` background daemon.
  - Maps OpenCode's granular per-tool permission rules (`bash, edit, websearch`, etc.) into Paseo permission cards.
- Pi: stdio JSONL, pi --mode rpc
  - PI: Custom __JSONL-RPC over stdio__
  - OMP: Its own __RPC / RPC-UI protocol__ , omp --mode rpc-ui
  - Spawns `pi --mode rpc` or `omp --mode rpc-ui` using `JsonlRpcProcess`.
  - Intercepts Pi RPC interactive extension dialogs (`select`,            `input`,            `editor`,            `confirm`) and translates them into Paseo question permission cards, sending the answer back via `extension_ui_response`.
- This is why native providers get deep features ACP can't express: subagent sidechain tracking and workflow output folding (Claude), file+conversation rewind via provider-native persistence (Claude/Codex/OpenCode), provider-native `providerOptions` schemas (only claude/codex/opencode have a `ProviderContract` with a real options schema in `provider-registry.ts:158-162`), and exact MCP preapproval for Hub unattended runs.

- External providers communicate over the Agent Client Protocol (ACP), an open standard (similar to Language Server Protocol, but for AI coding agents) using JSON-RPC 2.0 over stdio.
  - GitHub Copilot is listed under native/built-in providers in Paseo's UI manifest, but its backend is `CopilotACPAgentClient` (`copilot-acp-agent.ts`), which inherits directly from `ACPAgentClient`. Copilot CLI natively implemented ACP, allowing Paseo to reuse the ACP stack while treating Copilot as a first-class built-in choice.

- Paseo does not force native providers through ACP adapters. Native providers exist because tools like Claude Code, Codex, OpenCode, and Pi do not speak ACP; Paseo interfaces directly with their native SDKs and proprietary IPC protocols to unlock their full capabilities.

- 
- 
- 
- 
- 
- 

## pi

- Because Pi wrote the changes directly to disk in the workspace `cwd`
  - Paseo's background `file-observer` detects the disk modification
  - `WorkspaceGitService` runs an incremental `git status` and `git diff`.
  - The daemon emits a workspace checkout update.
  - In your workspace UI: The **Changes** tab / Git panel automatically highlights under Modified files.
# client-web/electron

## mac

- [Paseo macOS 桌面版运维手册](https://github.com/myysophia/paseo-best-practices/blob/main/docs/ops/macos-desktop.md)
- 桌面版没有独立 daemon，它就是 App 内部的一个 worker。App 退了，daemon 就没了（除非有僵尸 worker，见 坑 #2）
  - 密码	一般不需要（loopback）

- 
- 
- 
- 

# more
