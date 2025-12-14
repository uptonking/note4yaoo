---
title: lib-aikit-aionui-community
tags: [aionui, claude-code, community, electron, large-language-model]
created: 2025-12-13T18:38:47.137Z
modified: 2025-12-13T18:38:59.837Z
---

# lib-aikit-aionui-community

# guide

# discuss-stars
- ## 

- ## 

- ## 

- ## 
# discuss-roadmap
- ## 

- ## 

- ## 

- ## [Two functional requirements _202508](https://github.com/iOfficeAI/AionUi/issues/89)
  - Can you add a place to configure the GMEINI.md file, similar to the configuration rules in augment?
  - Can you develop a code index similar to the RAG feature in augment?

- better yet just follow agents.md . instead of multi gemini claude md

- 👷 202511: 
  - Request 1: Already on our roadmap! We'll support custom configurations, but tailored for office workflows rather than pure coding scenarios.
  - Request 2: We're taking a different approach. AionUI focuses on terminal agents with ReAct patterns, not IDE-style code indexing. We may revisit RAG if needed for office productivity use cases in the future.
# discuss-issues
- ## 

- ## 

- ## 

- ## 
# discuss
- ## 

- ## 

- ## 

- ## 

## dev-log-aionui

- ## webpack > rspack
- npm run webui 会启动express server后端服务器 http://localhost:25808

- 前端使用不同端口时, chat history不会显示，因为存储在 localStorage ?
- 
- 

- ## params must have required property 'file_path'
  - 部分本地模型经常执行tool call失败，就出现此问题

- ## 使用claude-code-router全局激活的claude，~~会提示 Authentication required~~
- 无法复现, 几乎都能正常运行claude
