---
title: lib-aikit-aionui-dev
tags: [aionui, claude-code, electron, gemini-cli, large-language-model]
created: 2025-12-13T18:37:56.593Z
modified: 2025-12-13T18:38:27.763Z
---

# lib-aikit-aionui-dev

# guide

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

- chat input 不是富文本, 但支持undo快捷键
  - read-file 的tool-call 默认折叠或只显示部分文字

- 模型列表不支持手动排序

- 未显示thinking内容，给人感觉很慢
  - thinking类型的模型不展示thinking内容和状态时，容易误导用户系统故障了

- default response for gemini is very slow

- 

- Supported Formats: Text files, images, code files, etc.
  - 可增加: markdown优化, docx, xlsx, pdf

- 选择文件夹后，不支持取消/删除选择

- switch projects/workspaces

- 设置快捷键

- search in page

- 支持更多cli, 如 mistral-vibe, kimi-cli

- cli-本地rag
  - 可参考 https://github.com/run-llama/semtools /MIT/rust/ts
  - Semantic search and document parsing tools for the command line
  - We made a simple cli command `ask` which lets you ask questions over any arbitrary folder in your filesystem. 

- 集成github上分享的claude-code workflow

- 集成rag-cli相关工具

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

## dev-xp-aionui

- 💡 本地模型经常读取文件失败, 原因是提示词没写好, 可用的提示词示例: 
  - show current working directory
  - summarize file   lib-db-postgresql-docs.md   in current working directory
  - 比如可根据ai针对第一个问题的回答翔略程度来扩容或缩容第二个问题的提问方式

- 使用本地ollama/lmstudio时，需要更详细更明确的提示词才能让8b模型执行, 4b模型很难成功执行
  - 特别是4b模型的tool call经常失败，在读文件失败时经常导致agent loop失败

- 
- 
- 
- 

## custom-models-xp

- Unhandled event type: { type: 'model_info', value: 'ep-b35yem-1765485729171085834' }

## docs-aionui

# 📌 claude-code/codex
- claude-code-cli 使用ollama本地模型时，可能提示 
  - "qwen3-vl:4b-instruct" does not support thinking
  - think value "high" is not supported for this model "qwen3-vl:4b"
  - 💡 使用gpt-oss-20b就无问题, 实测ollama/lmstudio的gpt-oss-20b都支持

- 
- 
- 
- 
- 

# more
