---
title: lib-aikit-paseo-dev-log
tags: [dev-log, paseo]
created: 2026-09-08T04:45:08.195Z
modified: 2026-09-08T04:45:17.635Z
---

# lib-aikit-paseo-dev-log

# guide

# devops
- locations
  - /opt/apps/llm-hub-lite/shared/data/prod/aichor/workspace

- Browser connection succeeds using host aichor.aichorage.de, port 443, SSL enabled.
# dev-xp
- 初版 autumn-studio 采用custom build的方式embed pi
# discuss-stars
- ## 

- ## 

- ## 

- ## 
# discuss
- ## 

- ## 

- ## 

- ## 

- ## Why does "build" script not exist in package.json? how to build this plugin and install to paseo mac app. source code for paseo is at folder ../paseo
- plugins are authored directly in source TypeScript and do not produce an ahead-of-time dist/ bundle on disk
- Paseo is the Compiler Host: When Paseo installs or runs a plugin, Paseo’s daemon discovers index.server.ts and index.client.tsx, and compiles them in-memory using its internal esbuild compiler
  - Preparation is defined in paseo-plugin.json

- ## does web-app/desktop-app use tailwindcss? can i use tailwindcss to build custom plugin?
- Neither the web app nor the desktop app uses Tailwind CSS. They are built on React Native / Expo and use react-native-unistyles (v3) for styling.
- Electron shell: It does not maintain an independent frontend or styling system; it launches the exported Expo web build from packages/app inside an Electron BrowserWindow
- Cross-Platform UI Contract (No HTML, No className)
- The Plugin Compilation Pipeline Has No CSS Extraction
  - Plugins are built by the daemon using esbuild
  - There is no PostCSS, Tailwind CLI, or CSS bundler in this pipeline, nor is there any mechanism to emit, transport, or inject .css files into the host app.
- Paseo supports multiple host themes (adaptive light/dark, user custom themes, Catppuccin, etc.). Hardcoded CSS utility classes (such as bg-slate-900 text-white) do not adapt to Paseo's theme tokens, resulting in unreadable text or broken contrast when the user switches themes.

- The Plugin Compiler Discards Separate CSS Files
  - Paseo explicitly supports a "build" step in paseo-plugin.json. Before Paseo compiles your code, it executes declared commands. This gives you the exact lifecycle hook needed to extract and compile Tailwind CSS before installation.
- The Big Trap: Tailwind Preflight Breaks Paseo's Host UI: Paseo's UI is built on React Native Web and Unistyles. 
  - If you inject standard Tailwind CSS into document.head, Tailwind's Preflight reset (* { box-sizing: border-box; margin: 0; padding: 0 }, button resets, border resets) will pollute the entire app: buttons will lose backgrounds, SVG icons will shift, and form inputs will break. 
  - You must isolate Tailwind from the host.
- Workaround 1: Scoped Tailwind with Preflight Disabled (Recommended)
  - disable Preflight and scope all Tailwind utility classes strictly to your editor's root container.
  - Because the styles are scoped to #markdown-editor-root and preflight is disabled, you can inject it cleanly into markdown-editor-root
- Workaround 2: Shadow DOM (100% Complete Style Isolation)
  - If you want Tailwind Preflight and the official @tailwindcss/typography plugin (prose classes like .prose h1, .prose ul, etc.) for rich text rendering, use Shadow DOM.
  - ProseMirror and TipTap natively support Shadow Roots.

- ## what's the relationship/differences between autumn-studio-plugin's pi embedding and paseo's built-in pi provider? 
- Both are pi-embedding clients speaking the same wire protocol — autumn-studio's RPC layer is a scaled-down sibling of Paseo's built-in pi client — but they sit at different boundaries of the system, source their pi binary differently, and make opposite trade-offs on fidelity vs. isolation.
- Both spawn `pi --mode rpc` as a child process and speak newline-delimited JSON over stdio
- Autumn-studio's server/rpc-process.ts is structurally a mini JsonlRpcProcess (same framing, stderr tail in errors, SIGTERM→SIGKILL teardown). the built-in's mapper was the reference implementation for Autumn-studio.

- differences
- Contract and process location. The built-in pi provider is a daemon-internal `AgentClient` factory, implementing Paseo's older in-process agent boundary directly inside the daemon. 
  - Autumn-studio implements the newer plugin provider contract (`ProviderRegistration/ProviderConnection`) and runs inside a forked plugin child — everything it emits crosses an IPC bridge, gets zod-revalidated, and is capability-negotiated before the daemon sees it.
- The built-in spawns PI_COMMAND ?? "pi" from the user's PATH , with the user's real ~/.pi/agent config. 
  - Autumn-studio spawns pi from its own `node_modules` via `server/pi-runner.mjs` — version-pinned by the plugin's dependency, zero user setup. 
- The built-in passes user-owned config through: real auth.json/models.json, real settings.json, real extensions and skills, MCP via a --mcp-config tmpfile
  - Autumn-studio generates a per-session agent dir, and runs with --no-approve so project-local .pi leakage can't happen.
  - The user's external dir is never pointed at directly — OAuth rotations come back through a guarded write-back instead. Built-in = full fidelity to the user's environment; autumn-studio = isolated config the plugin owns and regenerates.
- The built-in is ~4, 000 lines because it exposes everything pi can do: session listing/import, conversation rewind via the extension bridge, compaction triggering, usage polling, model cycling, fork/tree navigation, extension-UI dialogs mapped to Paseo permission prompts, --mcp-config injection. 
  - 🐛 Autumn-studio is ~1, 200 lines covering a deliberate subset: prompts, steers, tool/compaction/retry timeline items, usage, session resume via --session + get_entries replay, and native skills as session.commands. 
  - It auto-cancels extension dialogs rather than mapping them to permissions, and doesn't do listing, rewind, or compaction control. 
  - It has things the built-in doesn't by design: bundled pi (no install), /v1/models discovery with a persisted known-good cache, self-healing root discovery
- here's an agent that works out of the box, " with its own keys, its own config, and its own crash domain (a pi bug kills the session's child process, not the daemon). 

- ## paseo daemon is bundled in the desktop app so that the desktop app can be used out of the box. can the daemon also be bundled in a mobile app so that mobile app can be used out of the box without server?
- Node.js runtime vs. Mobile React Native engine
  - The daemon (packages/server) is a Node.js server relying on Node core modules (child_process, fs, net, http, native C++ bindings for PTY and file watching).
  - The mobile app (packages/app) runs on React Native / Expo using the Hermes JavaScript engine. Hermes is designed for UI rendering and cannot run Node.js server architectures or native Node C++ addons.

- iOS: Apple’s sandbox strictly disables POSIX process spawning (fork/exec). An iOS app cannot spawn arbitrary CLI processes.
  - Coding agents are external processes: The daemon orchestrates external binaries and runtimes—such as claude (Anthropic Agent SDK), codex-app-server, copilot (ACP), opencode, and pi. A mobile app cannot launch these tools as child processes.
  - Terminal PTYs: The daemon relies on native pseudo-terminal emulation (node-pty) to handle interactive terminal sessions, bash/zsh shells, and keystroke streaming.
- The local dev environment does not exist on mobile

- Background execution limits
  - Coding agents frequently run multi-minute (or longer) agentic turns, running tests or refactoring files.
  - Mobile operating systems aggressively freeze or terminate background apps (iOS limits background execution to roughly 30 seconds; Android kills background processes under battery/memory pressure). Running the daemon on mobile would cause agent tasks to be terminated whenever the app is backgrounded or the screen locks.

- ## is server/pi-sdk.cjs copied from source code? can this file be imported from npm package?  use minified js file in source code is bad smell. can it be added to .gitignore? 
  - can we import directly from @earendil-works/pi-coding-agent instead of the vendor bundle, or do we still need the bundle?
- No, we can't import directly from @earendil-works/pi-coding-agent — the vendor bundle is genuinely necessary.
  - The "." export drags in the TUI. Pi's main entry (dist/index.js) re-exports InteractiveMode, 25+ TUI components, terminal themes, and main — which transitively pulls in @earendil-works/pi-tui (terminal rendering engine), chalk, highlight.js, @silvia-odwyer/photon-node (WASM), quickjs-wasi (WASM), etc. There are no subpath exports like ./sdk or ./core/model-runtime
  - import.meta.url breaks in the eval sandbox. Pi uses import.meta.url at module scope in many files. The Paseo plugin compiler produces CJS bundles evaluated via globalThis.eval inside (function(require){...}) — there's no real import.meta. esbuild's CJS output turns it into an empty object, so import.meta.url.includes(...) checks crash. The vendor build script has a custom esbuild plugin (importMetaPlugin) that rewrites every import.meta.* reference to safe constants.
  - WASM deps can't exist inside an eval'd bundle. @silvia-odwyer/photon-node and quickjs-wasi use fs.readFileSync at module scope to load adjacent .wasm files — those files can't exist inside an eval'd CJS bundle. The vendor build marks them external so their lazy loaders fail inside pi's existing try/catch wrappers.
- What could eliminate the bundle long-term
  - An upstream PR to @earendil-works/pi-coding-agent adding subpath exports for the headless SDK surface
  - Plus decoupling the core/tools/renderers/* from @earendil-works/pi-tui imports. That would let consumers import just the embedding surface without the TUI graph. But that's upstream work

- from pi's docs, pi is designed for embedded use case.  why does a custom build is used in autumn studio?
  - @earendil-works/pi-coding-agent is designed for embedded use cases, there is a fundamental difference between embedding Pi in a standard Node.js application versus embedding Pi inside a Paseo Plugin.
- When Pi’s authors designed the embedding SDK (createAgentSession), they designed it for a standard Node.js or Bun process (e.g. running node server.js or bun run index.ts). T
  - he filesystem is directly accessible at node_modules/. import.meta.url points to an actual file on disk. 
  - Node can resolve native addons (.node), load adjacent WebAssembly (.wasm) files, and use the runtime module loader.
- In contrast, Paseo plugins run in a compiled in-memory sandbox:
  - Paseo’s plugin compiler bundles index.server.ts and all its non-host dependencies with esbuild into a single CommonJS text string.
  - The Paseo daemon then evaluates that string in memory using: javascript (0, globalThis.eval)(bundleString)(runtimeRequire); 
- Why the Custom Build (build-vendor.mjs) is Necessary
  - import.meta.url Crashes Inside eval()
  - Native WASM Modules Crash Without Files on Disk
  - Missing __dirname and __filename Globals
  - Pi's Package exports Map Drags the Entire TUI into the Bundle. Although createAgentSession is exported from dist/index.js, that same file re-exports InteractiveMode and 25+ interactive TUI components from @earendil-works/pi-tui. in esm, top-level static imports are eagerly evaluated. Importing Pi from "." pulls in the entire interactive terminal rendering engine, terminal widget trees, diff formatters, and syntax highlighters.

- ## is current architecture for embedding pi agent good ?  is there any better solution? if there is, how will it be better than current custom build solution?
- The vendored pre-bundle isn't a preference; it's the only way to run pi inside a plugin today, because three walls stand between a plugin and pi's npm package:
  - The daemon's eval-based loader. Plugin server bundles are evaluated via globalThis.eval inside a factory that supplies only require — no real module identity.
  - pi's package shape. The . entry re-exports the interactive TUI, so a naive import pulls the terminal UI into the bundle; the WASM packages
  - pi's published type graph. The Paseo compiler walks type declarations of every import, and pi's types don't resolve outside their own tree — even type-only imports fail.
- The vendor bundle neutralizes all three in one place (~250 lines of build machinery), built from npm-pinned packages, generated at install time, with the smoke test pinning the eval-context behavior. Within those constraints, this is the right call over the alternatives available today — spawning pi's CLI from the plugin's node_modules hits the same type-graph wall on the client side, and there's no supported SDK subpath to import.
- 
- 
- 
- 

- ## The pairing URL normally begins with https://app.paseo.sh/#offer=...; 
  - that is expected even when the embedded relay is your own Relaichor instance.

- ## when i open https://app.paseo.sh in chrome or microsoft edge browser, the localhost:6767 is auto detected and added as host. but when i open it in safari browser, why is localhost:6767  not auto detected and added as host?
- This happens because of a major architectural difference between browser engines: **Chromium (Chrome & Edge) vs. WebKit (Safari)** regarding **Mixed Content Security Policies** .
  - https://app.paseo.sh  is served over HTTPS. When a web page loaded over HTTPS tries to open an unencrypted WebSocket (ws:// instead of wss://), browsers have to decide whether to permit it under their Mixed Content rules.
  - Chromium implements the W3C _Secure Contexts_ specification, which explicitly designates `127.0.0.1` and `localhost` as **"potentially trustworthy origins"** (loopback exception).
  - Apple's WebKit takes a strict security stance and **does not grant a mixed-content exemption to `localhost` ** . An HTTPS origin is **strictly forbidden** from loading any unencrypted subresources ( `http://` or `ws://` ).

- ## where is location for "Search for directory" ?
- /workspace is the intended persistent project area. It survives Aichor/container/VPS restarts and is separate from Paseo’s internal state.
  - /opt/apps/llm-hub-lite/shared/data/prod/aichor → /home/paseo
  - /opt/apps/llm-hub-lite/shared/data/prod/aichor/workspace → /workspace
- Choose Add project → Search for directory
  - Enter the full container path: /workspace/my-project

- ## the hostname shows as 04226b5abf73 . is there any way to edit the connection info and change the host name to a semantic host name?
  - Do not enter wss:// or /ws in the Host field. The UI constructs the WebSocket URL itself. Entering a complete WebSocket URL there is what causes the Invalid URL error.

- ## When you select "Direct connection", you should NOT enter any host, port, or URL.
  - "Direct connection" means the UI will automatically connect to the same daemon that served the web page.
  - The form fields should be empty or grayed out.
  - "Direct connection" means "connect to the daemon that served this page" - it should be automatic.
  - The auto-detection is failing - it's falling back to ws://localhost:6767/ws instead of detecting wss://aichor.aichorage.de
- The problem is that your reverse proxy (Caddy) isn't forwarding the necessary headers.
