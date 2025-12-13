---
title: lib-aikit-aionui-codebase
tags: [aionui, codebase]
created: 2025-12-13T18:38:34.795Z
modified: 2025-12-13T18:38:44.267Z
---

# lib-aikit-aionui-codebase

# guide

# overview
- Tech Stack: TypeScript, React, Electron, Webpack, UnoCSS, Arco Design, SQLite
  - Worker Processes (src/worker/): Separate Node.js processes for AI agent execution (Gemini, ACP, Codex).

- frontend-renderer
  - React Context: 全局状态 (认证、主题、布局)
  - Local State: 组件内部状态
  - SWR: 服务端状态缓存
  - localStorage: 持久化 UI 配置
# modules

# more
