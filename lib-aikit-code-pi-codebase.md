---
title: lib-aikit-code-pi-codebase
tags: [codebase, pi]
created: 2026-08-14T21:43:18.872Z
modified: 2026-08-14T21:43:32.903Z
---

# lib-aikit-code-pi-codebase

# guide

# overview

# architecture

# sandboxing/isolation
- Pi approaches sandboxing in three distinct tiers, depending on the desired isolation depth 
  - OS Process Sandbox uses @anthropic-ai/sandbox-runtime
  - Container isolation uses Docker / Docker Sandboxes / OpenShell
  - Micro-VM/Gondolin: Minimal Linux VM (QEMU/libkrun)
- The primary reason Pi can switch between host execution, OS sandboxing, and micro-VM isolation without rewriting core agent logic is two architectural patterns:
  - Pattern A: Pluggable "Operations" Interfaces for Tools: Pi's tool logic (formatting line numbers, calculating diffs, truncation, token counting, error rendering) is decoupled from where the command or file operation actually happens.
  - Pattern B: Lifecycle & Tool-Overriding Extension API: built-in tools can be replaced with with sandboxed versions.

- Gondolin is a local micro-VM sandbox tailored specifically for AI agents. Rather than running the whole agent inside a VM or container, the agent runs on the host, while tools run inside a Linux micro-VM.
  - the host remains the sole authority for network and persistence. 

- Host-Side VFS Providers
  - Instead of giving the VM raw direct disk access to your host disk

- 
- 
- 
- 
- 
- 
- 

# more
