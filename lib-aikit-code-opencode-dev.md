---
title: lib-aikit-code-opencode-dev
tags: [ai-coding, opencode]
created: 2026-01-17T22:39:30.432Z
modified: 2026-01-17T22:40:27.013Z
---

# lib-aikit-code-opencode-dev

# guide

- tips
  - Coding agent clients (sometimes referred to as harnesses)
# draft

# dev-xp
- 基于coding-cli封装/二次开发app的缺点, coding场景内置大量system prompt, 本地小模型效果很差
  - 而使用自定义提示词的RAG app, 使用小模型的效果较好, 所以要根据场景选择性使用coding-cli agent

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
