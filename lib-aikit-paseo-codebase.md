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
  - **Native Features** : Directly controls Claude's native `allowedTools`, disallowedTools, extended thinking tokens, UltraCode mode, and token compaction.
- Codex: stdio JSON-RPC, codex app-server 
  - proprietary __app-server JSON-RPC over stdio__, via a custom transport
  - Spawns `codex app-server` as a long-running subprocess.
  - Directly bridges Codex's OS sandbox modes (`sandbox_workspace_write`, writable roots, network proxy settings) and approval policies (`auto-review`, full).
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
  - Intercepts Pi RPC interactive extension dialogs (`select input editor confirm`) and translates them into Paseo question permission cards, sending the answer back via `extension_ui_response`.
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
# plugins
- Paseo recently introduced a comprehensive **full-stack plugin system** (in v0.8).
- Unlike simple UI plugins or basic terminal hooks, Paseo plugins are **dual-runtime extensions**: they can execute code in a **Node.js daemon child process** on your development machine, while simultaneously delivering **rich React Native UI** to every connected mobile, desktop, or web client.

- In `plugin-examples/`, Paseo maintains canonical examples demonstrating key plugin patterns:
  - Example 1: External Context Integration (`plugin-examples/linear`), Allows developers to search Linear issues directly from Paseo's message composer and attach them as rich context cards to any agent prompt.
  - Example 2: Lifecycle Actions & Policy Governance (`plugin-examples/lifecycle-actions`), Demonstrates how plugins can enforce security policies, automate git workflows, and handle agent errors.
  - Example 3: Adding Custom Coding Agents (`plugin-examples/provider-direct` & `provider-acp-transformer`)
  - Example 4: Transcript Customization (`plugin-examples/timeline-items` & `inline-thinking`), Transforms raw agent tool invocations into beautiful native UI components.
  - Example 5: Themes (`plugin-examples/catppuccin`), Adds custom visual themes across the entire Paseo app.

- 
- 
- 
- 
- 
- 
- 
- 
- 
- 

## https://github.com/itsjustanks/paseo-plugin-daemon

- paseo-plugin-daemon provides three distinct forwarding modes

- Mode 1: "Browser Link" (One-Click Temporary Public HTTPS URL)
  - This is the primary flow when you click "Open" or "Browser Link" next to a server card. 
  - The plugin spawns an in-memory Node.js HTTP/WebSocket reverse proxy on an ephemeral loopback port.
  - The plugin spawns a background cloudflared process: 
  - `cloudflared tunnel --no-autoupdate --protocol http2 --url http://127.0.0.1:<gatePort> ` 
  - Every 2 seconds, the Gate probes the local dev server. If the dev server stops, the tunnel immediately shuts down.

- Mode 2: "Private Localhost" (Zero-Knowledge E2EE Relay Forwarding) 
  - Used when you pair two Paseo hosts (e.g., your laptop and your desktop/VPS) via Connect → Private localhost.
  - Host B pairs with Host A.  
  - Host B starts a local TCP server on an arbitrary port (e.g. 127.0.0.1:45678). 
  - When your local browser connects to http://localhost:45678, Host B opens an end-to-end encrypted WebSocket channel to Host A through the Paseo Relay (@getpaseo/relay/e2ee).

- Mode 3: "SSH Forward" (server/ssh.ts) 
  - If you already have SSH access, the plugin can manage persistent `ssh -L 127.0.0.1:<localPort>:127.0.0.1:<remotePort>` connections, monitoring their health and auto-restarting them if dropped.
  - Low-latency private tunnel if you have SSH keys configured

- On Linux, the plugin doesn't use macOS lsof or ps. Instead, it reads the Linux /proc virtual filesystem directly: Ports: It parses /proc/net/tcp and /proc/net/tcp6 to find all listening sockets.
  - When you click "Set up browser links" on your VPS, you do not need to install cloudflared manually via apt or yum
  - It downloads the official pinned binary (cloudflared-linux-amd64 / arm64) from GitHub directly to ~/.paseo/daemon-link/bin/cloudflared.

- With Browser Link (Cloudflare Quick Tunnel): cloudflared makes an outbound connection to Cloudflare Edge servers (outbound HTTPS/port 7844). You do not need to open any inbound ports on your VPS firewall. You can access the dev server on your phone through the trycloudflare.com URL immediately.

- With Private Localhost (Paseo Relay): Both the VPS and your client connect outbound to your relay server (relay.yourdomain.com:443). No inbound VPS ports are required.

- 
- 
- 
- 
- 

# client-web/electron
- What the web/desktop UI is built from (packages/app)
  - One React Native codebase — the web UI and Electron desktop UI are the same Expo app rendered via react-native-web; mobile is native RN.
  - react-native-unistyles (v3) for styling and theming — this is the closest thing to a "UI library" in the stack.
  - Plain RN primitives (View/Text/Pressable) plus supporting libs: @gorhom/bottom-sheet, @floating-ui/react-native, @dnd-kit, lucide-react-native icons, @tanstack/react-query, zustand, reanimated.

- if the web-ui/desktop-ui is all built with react-native, how can it be bundled to a desktop app?
  - the trick is that the desktop app doesn't run React Native at all. It loads the web build of the React Native app inside a Chromium window.
  - React Native is compiled to a web SPA by Metro/react-native-web, and Electron is a Node-capable Chromium wrapper that hosts that SPA — dev against Metro, packaged against a static paseo:// protocol.
  - packages/app includes react-native-web (~0.21) and react-dom, and app.config.js declares a web: { output: "single" }
  - react-native-web implements RN primitives (View, Text, Pressable, …) as DOM elements, so the same component tree that renders natively on iOS/Android renders to HTML in a browser. 
  - Metro (Expo's bundler) exports a static web bundle. 
  - Electron is just a Chromium shell around that bundle. In packages/desktop/electron-builder.yml, the web export is shipped as `extraResources`
- How platform-specific code still works
  - Since one codebase serves iOS, Android, browser, and desktop, the desktop-specific pieces are split out mechanically rather than with if statements
  - Build time: PASEO_WEB_PLATFORM=electron, When bundling for web, Metro first tries to resolve local imports as foo.electron.ts(x) before falling back to foo.web.ts(x) and plain files. That's how desktop-only modules (e.g. the Electron `<webview>` browser pane) get into the desktop bundle while the plain browser build gets index.web.tsx and native gets index.tsx — the other variants are never bundled.
  - Runtime: a sandboxed preload script exposes window.paseoDesktop via contextBridge — an IPC bridge for window controls, file dialogs, notifications, deep links, and the auto-updater. App code checks getIsElectron() before touching it
  - Main process side: the Electron main owns everything the web page can't do — window management/chrome, native menus, notifications, spawning and supervising the local daemon

- You cannot render ProseMirror/Tiptap inside a plugin surface today — plugin UI is deliberately locked to host-provided React Native components with no DOM access. 
  - A plugin's index.client.tsx is compiled by the daemon's esbuild compiler and runs inside the Paseo app's React Native tree — react-native-web on browser/Electron desktop, real RN (Hermes) on iOS/Android.
  - The SDK gives you exactly this render surface. No WebView, no iframe, no HTML elements. 
  - compiler rejects Node builtins and server-only modules in client bundles and enforces the SDK boundary.
- One important nuance: the compiler does allow bundling arbitrary npm libraries into the client bundle (only host modules and boundary rules are special-cased), so shipping tiptap/prosemirror-* code is fine. 
  - The blocker is purely that there's no DOM surface to mount them on.
- Paseo's plugin client bundle may only import host modules — I confirmed the exact external list in the Paseo compiler. 
  - So no pdf.js, no canvas, no viewer library, no gesture library on the client. 
- When Paseo compiles a plugin via packages/server/src/server/plugins/compiler.ts, esbuild bundles all npm dependencies into the client bundle except those marked external like react/react-native/tanstack
  - When the bundle executes inside Paseo, the host provides only those external modules via runtimeRequire. Notice that react-dom is NOT in that list.
  - If you use @tiptap/react, it imports react-dom. Because react-dom is not provided by the plugin runtime, it will throw: Module "react-dom" is not available 
  - The Solution: Use vanilla ProseMirror or @tiptap/core. Because they are pure DOM/JS libraries with no React dependencies, esbuild will bundle them completely into your plugin bundle. You then wrap it in a lightweight React component with `useRef<HTMLDivElement>` and useEffect, exactly like Paseo does for CodeMirror.
- By default, Paseo plugin scaffolds omit "DOM" from tsconfig.json to encourage mobile compatibility.
  - For desktop/web-specific code, you can enable "DOM" in your plugin's tsconfig.json lib, gate with layout.platform === "web" from PluginHostProps, and render a standard `<div ref={hostRef} style={{ flex: 1 }} />`.

- The perception that react-native-web prevents using rich web React components or DOM editors is a common misconception. Nothing prevents mounting DOM-based editors. In fact, Paseo already does this across several core features
  - Paseo mounts CodeMirror 6 (with Vim emulation, search/replace, and syntax highlighting) directly into a `<div ref={hostRef} />`.
  - Terminal: Runs xterm.js inside a DOM container on web.
  - Embedded Browser: Uses Electron `<webview>` elements.
  - HTML Preview: Uses an `<iframe>`.
- 
- 
- 
- 
- The app's own answer to "react-native-web can't do X"
  - The repo itself hits this wall constantly and its pattern is: prebuild a web bundle and mount it in a WebView (native) / iframe (web), bridged with postMessage
  - The xterm terminal
  - Mermaid diagrams
  - HTML file preview
  - This machinery exists in the app but is not exposed to plugins.
- Option A — workspace browser tab.
  - The plugin server side (index.server.ts) runs unsandboxed Node on the daemon host: it can bind a localhost HTTP port, serve a Tiptap page, and expose read/write endpoints for the markdown file 
- Option B — contribute the renderer to the app (upstream PR, best UX). 
  - Add a file-pane renderer following the mermaid/terminal pattern: filePreviewRenderKind
  - a prebuilt Tiptap webview bundle would fit the existing architecture exactly. 
  - but the plugin system could eventually grow a registerFileRenderer contribution, which would be the feature to propose.
- Option C — imperative DOM mount (hacky, web-only). 
  - On web, react-native-web Views are real DOM elements, so a plugin could grab a View ref (a div), gate it with Platform. OS === "web", and mount ProseMirror into it imperatively.
  - It would work on desktop Electron/browser and be a no-op on iOS/Android, but it fights React Native's reconciler (node replacement, keyboard/IME/selection conflicts), violates the documented cross-platform contract, and will break unpredictably across RN-web versions. 

- https://github.com/dbhq-uk/paseo-file-viewer
  - it doesn't fight react-native-web's constraints at all. It pushes all heavy lifting into the daemon and ships the client only PNG images or plain JSON, which stock RN components can render.
  - The plugin's answer: the daemon does all parsing and rasterising, the client renders React Native primitives. 
  - rasterise (PDF, images): ship a PNG
  - parse (docx, xlsx): ship structured JSON, 
    - This was a deliberate, benchmarked decision (DESIGN.md): converting a 33-sheet workbook to PDF takes LibreOffice 8.7s and produces 169 anonymous A4 pages, while exceljs parses it in 0.4s into 33 named sheets.
    - .docx: mammoth converts to HTML, and node-html-parser (on the daemon) flattens it into a small block union 
    - .xlsx: exceljs returns sheet metadata (doc.open), then doc.rows streams row windows; SheetReader has a horizontal sheet-picker bar and a paged FlatList. Any sheet over 500 rows breaks. PAGE_SIZE limit
  - This plugin confirms the constraint is real and shows the "work with it" strategy: anything expressible as images or JSON can be rendered beautifully from a plugin on all four platforms. 
    - But it also shows the boundary — this is a read-only viewer. 
- A hybrid is also plausible: this plugin's panel pattern for browsing/listing, plus openBrowser for the editing surface.

- 
- 
- 
- 
- 
- 
- 

## mac

- [Paseo macOS 桌面版运维手册](https://github.com/myysophia/paseo-best-practices/blob/main/docs/ops/macos-desktop.md)
- 桌面版没有独立 daemon，它就是 App 内部的一个 worker。App 退了，daemon 就没了（除非有僵尸 worker，见 坑 #2）
  - 密码	一般不需要（loopback）

- 
- 
- 
- 

# isolation/worktree
- for Non-Git Folder, worktree is not supported.

- local: Your actual filesystem folder (e.g. `/Users/you/project`).
  - No file isolation. Edits happen immediately in your working folder and editor. 
  - If two agent sessions run concurrently in the same directory and edit the same file, **they will overwrite each other's edits** . Paseo does not lock filesystem files.
    - **Provider-level protection:** Most agent providers (Claude Code, Pi, Codex) perform check-before-write in their `edit` tool. If Agent 1 edits lines in `index.ts` while Agent 2 is also modifying it, Agent 2’s tool invocation fails with an `oldText did not match` error.
  - Shares the main repository's `.git/index` and checked-out branch.
  - for **Workspace Archive / Deletion** , Only archives workspace metadata/chat history. **Files are never touched or deleted.** 
    - For `local_checkout` and non-git `directory` workspaces, archiving removes the workspace record from Paseo's UI and daemon registry, but **never deletes the directory on your disk** .
  - Dev server port collisions must be handled manually.
- worktree: A dedicated directory under `~/.paseo/worktrees/{slug}`.
  - **Full physical isolation.** Changes are completely secluded in the worktree folder. each worktree has its own physical copy of files on disk.
  - Completely isolated `.git/worktrees/{name}/index` and dedicated branch.
  - Each worktree maintains its own independent index file under `.git/worktrees/<name>/index`, so worktree Git mutations do not lock the main repo.
  - If Paseo owns the worktree, archiving the workspace deletes the worktree folder via `git worktree remove`.
  - Runs setup scripts defined in `paseo.json` (e.g. `npm ci`, build steps).
  - Injected with `PASEO_WORKTREE_PORT` and ephemeral port allocation.

- for Simple Non-Git Folder (`kind: "directory"`), The daemon creates a workspace record with `isGit: false` `currentBranch: null`, and `cwd: /path/to/folder`.
  - When you run an agent session (Claude, Codex, Pi, etc.) or open a terminal, the daemon spawns the process with `process.cwd` set to that directory.
  - Git-specific panels (Git diff, branch switcher, forge PR/MR integration) are automatically disabled. 
  - The file explorer, composer, agent transcripts, and terminals operate directly on the folder.

- for Local Git Repo with `local` Isolation (`kind: "local_checkout"`), The daemon inspects your repo via `workspaceGitService.getCheckout()`, detecting your Git root and current branch.
  - Agents run directly in your main repo. Any file edited by Claude, Codex, or Pi is instantly visible in your IDE (VS Code, Cursor, etc.) and in `git status`.
  - Paseo allows you to open multiple workspaces pointing to the exact same local folder.
  - Directory-backed state (Shared across same-directory workspaces): Includes Git status, Git diff, forge PR/MR status, and file contents. Both workspaces see the identical on-disk reality.
  - Workspace-owned state (Strictly isolated per workspace): Includes agent sessions, chat transcripts, terminals, draft messages, review draft comments, and file explorer expanded trees. 
  - Agent running status (`running` vs `idle`) is isolated to the owning workspace

- for Local Git Repo with `worktree` Isolation (`kind: "worktree"`), Executes `git worktree add <worktreePath> -b <newBranch> <baseRef>`.
  - Writes `.paseo/worktree.json` with metadata (`baseRef`  `changeRequestLookupTarget`), and seeds `paseo.json` from the source repository.
  - Writes `.paseo/worktree.json` with metadata (`baseRef`  `changeRequestLookupTarget`), and seeds `paseo.json` from the source repository.
  - If the worktree directory is accidentally deleted,  `workspace-recovery-service.ts` can reconstruct the worktree from `mainRepoRoot` + `baseBranch`.

- When multiple agents or background polling tasks run `git status` or `git diff` simultaneously, standard Git repos can crash due to index locking.
  - All read-only Git operations (polling, diffing, status checks, rev-parse) inject `GIT_OPTIONAL_LOCKS: "0"`, This tells Git not to acquire index locks during read operations.
  - A centralized concurrency scheduler git-process-scheduler.ts limits concurrent Git processes and prioritizes user operations over background polling.
  - 
- 
- 
- 
- 
- 
- 

# more
