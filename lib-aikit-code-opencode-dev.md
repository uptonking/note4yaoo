---
title: lib-aikit-code-opencode-dev
tags: [ai-coding, opencode]
created: 2026-01-17T22:39:30.432Z
modified: 2026-01-17T22:40:27.013Z
---

# lib-aikit-code-opencode-dev

# guide

# draft

# dev-xp

## devops

- resources
  - [Developing OpenCode](https://github.com/anomalyco/opencode/blob/dev/CONTRIBUTING.md)
  - [docs(desktop): enhance README with environment setup ](https://github.com/anomalyco/opencode/pull/8487/files)

```sh
# start tui
bun install
bun dev

# Building a "localcode"
export RUST_TARGET=aarch64-apple-darwin
# export RUST_TARGET=x86_64-pc-windows-msvc
# export RUST_TARGET=x86_64-unknown-linux-gnu
./packages/opencode/script/build.ts --single
# start server
# ./packages/opencode/dist/opencode-<platform>/bin/opencode
./packages/opencode/dist/opencode-darwin-arm64/bin/opencode serve --port 4096

# Running the Web App  http://localhost:3000
bun run --cwd packages/app dev

# To run the native desktop app:
bun run --cwd packages/desktop tauri dev

```

# more
