---
title: lib-aikit-zcode-codebase
tags: [codebase, zcode]
favorited: true
created: 2026-09-24T16:00:54.650Z
modified: 2026-09-24T16:01:06.061Z
---

# lib-aikit-zcode-codebase

# guide

# architecture

- 
- 
- 
- 
- 

- 
- 
- 
- 

# dataflow

# providers

# sandboxing/isolation
- Application-Layer Permission Gating 
  - Assumes commands are legitimate unless the user rejects the approval prompt
  - Raw `child_process.spawn`(macos) , execFile/spawn(linux), POSIX `exec` (no OS sandbox wrapping).
  - ZCode originally attempted an OS sandbox ("protected-resource sandbox"), but abandoned it because capability probing, cross-platform inconsistencies, and hung processes created too much friction.
  - No Seatbelt / sandbox-exec. The command executes with full user permissions on macOS. running `rm -rf ~` or reads `~/.ssh/id_rsa` are allowed.
  - on linux, Isolation is limited to environment variable stripping (sanitizeZCodeRuntimeEnv) and process tree termination (process-tree.ts).
  - on windows, Uses koffi to bind child processes to a Win32 Job Object. This is NOT a security sandbox. It is strictly a process lifecycle cleanup mechanism to ensure grandchild processes are terminated when the CLI exits. File, registry, and network access remain completely unrestricted.

- Ephemeral Node Workers + node:vm (forJS REPL only), Electron `<webview>`. 
  - When the agent runs arbitrary JavaScript via the `js` tool (e.g. for scraping, data manipulation, or browser control), ZCode implements isolation in apps/zcode-cli/packages/node-repl-host
  - each js tool call runs inside an ephemeral Node.js worker_threads. Worker
  - Spawning a fresh worker ensures that when the call finishes or times out, the worker is terminated
- Because standard node:vm contexts can be bypassed if the script accesses process.exit() or writes to stdout, packages/core/src/repl/node-repl-session.ts and node-repl-runtime-helpers.ts install a frozen proxy

- ZCode provides a specialized, deterministic sandbox for dynamic workflow snippets
  - Subprocess Isolation: Runs in a separate Node.js child process communicating solely via NDJSON over stdin/stdout.
  - Host Interaction via Stubs: The script can only invoke external operations via __host calls that serialize messages across the pipe to the parent engine.

- Child Process Tree Containment 
  - On Windows, ZCode uses koffi to bind spawned processes to native Win32 Job Objects. When ZCode or the MCP host exits, Windows automatically kills all subprocesses and grandchild processes in the kernel. 
  - On Linux and macOS, ZCode discovers the full PID process tree, issues SIGTERM, verifies termination with kill(pid, 0), and forces SIGKILL if processes hang.

- 
- 
- 
- 
- 
- 

# more
