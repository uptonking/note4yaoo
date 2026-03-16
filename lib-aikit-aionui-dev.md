---
title: lib-aikit-aionui-dev
tags: [aionui, claude-code, electron, gemini-cli, large-language-model]
created: 2025-12-13T18:37:56.593Z
modified: 2025-12-13T18:38:27.763Z
---

# lib-aikit-aionui-dev

# guide

- pros
  - supports multiple parallel sessions, each session with independent context
  - WebUI Mode: Supports LAN, cross-network, server deployment 
  - Automatically recognizes local CLI tools, provides a unified graphical interface
  - 基于electron, 方便打包python/js运行时, 这样可以方便用户直接使用python skills
  - support for macOS, Windows, Linux (Claude Cowork currently only macOS)
  - switch between different models: Gemini, OpenAI, Claude, Qwen, as well as local models like Ollama, LM Studio.
    - 本地model、多个model的配置UI简单易用, 而很多产品没有实现如openclaw/cowork
    - 支持多 key 轮询
  - All conversations and files saved locally: local sqlite

- cons
  - 不支持rag
  - 缺少类似编辑器的 undo/diff 体验
  - chat体验待优化
    - 流式输出
    - thinkingcontent

- features
  - Smart File Management: Batch renaming, automatic organization, smart classification
  - After AI generates files, view preview immediately without switching apps
  - Automatically tracks file changes, editor and preview sync intelligently
  - Intelligent image generation, editing, and recognition, powered by Gemini
# aionui-office
- pm
  - 将cline/roo/kilo的工作UX引入 aionui: tools, tasks, approval
  - skills for existing apps like msoffice/libreoffice
  - 父子文件夹的rag如何去重
  - ai执行的进度和反馈不够透明和丰富

- 对本地文件的rag采用client/server更合适, 而不是在每个文件夹都创建index.sqlite数据库
  - 方便支持多个terminal/agent/app同时操作文件，能减少冲突
  - 减少重复索引

- ? migrate sidebar to chromium-split-view
- local ai by @electron/llm

## draft-office

- models
  - 根据不同任务，使用不同模型，类似claude-sonnet/opus/haiku, 能优化成本，也能改善toolcall

- 提供完全使用外部 gemini-cli/opencode-cli 的方式, 
  - 增加抽象层，通用的能力支持其他cli, 定制/复杂的能力使用内置cli, 内置cli的设计是否要去掉?

- llamaindex open source version
  - https://x.com/jerryjliu0/status/2026032764131451334
    - We built an AI agent that lets you vibe-code document extraction

- 集成 docling-mcp

### issues

- 使用内置的cli，会导致使用外部同名cli出现配置冲突、端口冲突、编辑冲突吗
  - dev-start前，若3000端口被占用， 会启动失败且没有日志, 问题会出现在 `npm run webui` 时无法正常停止而没有自动关闭端口

### sandbox

- git-worktree to agentfs

- web-clipper to import chatgpt/gemini/deepseek-chat-message

- 
- 
- 
- 

### chat体验待优化

- 流式输出
- thinking-content

### image

- ai找不到文件路径， 一直回复 don't have access to any image
- 大图片在编码为base64文本后, 会提示超过模型上下文

### file-manager

- 文件重命名后, 旧文件在列表中未消失

### opencode-cli

- 参考 opencode-desktop 的官方实现 来优化aionui的数据流

- tool-call fix

- chat内容中的文件路径不可点击打开

- 4096 auto close
  - 是否需要自动关闭, 后台任务/远程访问 如何是否依赖

- I notice another issue from your log: The first chat's server is being stopped before the second chat starts.

- 🐛 Copying the config file to the workspace triggers OpenCode CLI's file watcher, which auto-spawns a new server.
  - The OpenCode CLI has a file watcher that monitors for new opencode.json files being created, and automatically spawns a server when it detects one
# 📌 AionUi
- pros
  - ⚖️ 通过ACP协议支持多种cli

- cons
  - 默认使用gemini-cli, 使用ollama时偶尔会碰到问题
    - 虽然qwen-code支持ollama，但不支持使用配置的apikey

- features
  - ?

- All conversations are saved locally:
  - macOS: ~/Library/Application Support/AionUi/
  - Windows: %APPDATA%/AionUi/
  - Linux: ~/.config/AionUi/

- tips
  - 采用aionui封装cc/gemini-cli的思路来封装llama.cpp/mlx

## draft-aionui

- pdf-view-edit
  - 支持docling/nanotes等模型解析pdf，并还原布局
  - 不与pdf软件厂商绑定

- office
  - word/excel不与软件厂商绑定的方案

- 和gemini-cli的 api 集成的event type没有标准

- cli-本地rag
  - 可参考 https://github.com/run-llama/semtools /MIT/rust/ts
  - Semantic search and document parsing tools for the command line
  - We made a simple cli command `ask` which lets you ask questions over any arbitrary folder in your filesystem. 
  - 迁移 主流rag-cli 或 claude-code-rag 的方案到aionui

- chat input 不是富文本, 但支持undo快捷键
  - read-file 的tool-call 默认折叠或只显示部分文字

- 模型列表不支持手动排序

- 未显示thinking内容，给人感觉很慢
  - thinking类型的模型不展示thinking内容和状态时，容易误导用户系统故障了

- default response for gemini is very slow

- chat
  - chat界面无法切换provider/model

- Supported Formats: Text files, images, code files, etc.
  - 可增加: markdown优化, docx, xlsx, pdf

- 选择文件夹后，不支持取消/删除选择

- switch projects/workspaces

- 设置快捷键

- search in page

- 支持更多cli, 如 mistral-vibe, kimi-cli

- 集成github上分享的claude-code workflow

- 
- 
- 

- 集成cluade-code相关的plugins/workflows
  - memory
  - rag
  - 参考 Roo Code built a new Claude Code integration with Caching and Interleaved thinking

- 重命名文件或文件夹后, workspace信息会丢失? vscode也存在类似问题, 顶层文件夹重命名后，聊天记录会丢失

- 
- 
- 
- 

- toolchain-migrate
  - webpack > rspack
  - UnoCSS > tailwindcss
  - react-router-v7 > tanstack-router/start

- qwen-code支持ollama，但不支持使用配置的apikey
# dev-xp-aionui
- electron启动时，会自动读取`.env`文件, 注意里面设置的值可能不符合预期

- 💡 本地模型经常读取文件失败, 原因是提示词没写好, 可用的提示词示例: 
  - show current working directory
  - summarize file   lib-db-postgresql-docs.md   in current working directory
  - 比如可根据ai针对第一个问题的回答翔略程度来扩容或缩容第二个问题的提问方式

- 使用本地ollama/lmstudio时，需要更详细更明确的提示词才能让8b模型执行, 4b模型很难成功执行
  - 特别是4b模型的tool call经常失败，在读文件失败时经常导致agent loop失败

- 基于coding-cli封装/二次开发app的缺点, coding场景内置大量system prompt, 本地小模型效果很差
  - 而使用自定义提示词的RAG app, 使用小模型的效果较好, 所以要根据场景选择性使用coding-cli agent

- gemini-cli is imported as @office-ai/aioncli-core as an npm package dependency, and i can use the default gemini-cli without installing gemini-cli.

- Each conversation gets its own SEPARATE CLI/server instance
  - ForkTask (from @/worker/fork/ForkTask) spawns a separate Node.js child process for each agent instance
  - gemini-cli uses In-process (aioncli-core)
  - opencode-cli-mini uses Separate HTTP server (opencode serve) , Random port per conversation 
  - Concurrency: Multiple conversations can run simultaneously without blocking
  - Each process can be killed independently when conversation is closed

- 
- 
- 

## devops

```sh
# start electron app in dev
npm run start

BUNDLED_CLI_PROVIDER

```

- 
- 
- 
- 

## custom-models-xp

- Unhandled event type: { type: 'model_info', value: 'ep-b35yem-1765485729171085834' }
# docs-aionui

# alternatives-claude-cowork/codex-app

- claude-cowork
- pros
- cons

- codex-app
- pros
- cons
  - 启动时必须选择文件夹
  - 选择文件夹后，通过 add files 添加指定文件，ai似乎未获取到文件路径而回应 Which PDF file should I summarize?
  - cmd+q推出后所有任务会中断 Any local threads running on this machine will be interrupted and scheduled automations won't run
# more
- [【教程】用 AionUI & Chrome MCP Tools控制自己的 Chrome浏览器（带浏览器原始数据，非新开），完全免费 ](https://linux.do/t/topic/1510601)

- [想玩的试试：用Telegram远程控制AionUi在本地干活  ](https://linux.do/t/topic/1537271)
