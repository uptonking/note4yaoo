---
title: lib-aikit-librechat-dev
tags: [large-language-model, librechat]
created: 2025-09-01T05:52:12.154Z
modified: 2025-09-01T05:52:34.241Z
---

# lib-aikit-librechat-dev

# guide

- pros
  - license: apache2
  - Customizable Agents: No-Code Custom Assistants, tools
  - 👥🔀 multi-conversation: 选择模型1，点add multi-conversation, 再选择模型2, 输入并发送需求
    - 🐛 实测选一个ollama一个LMStuio模型时能同时输出，但选2个LMStudio模型时会有一个异常或一个输出不全
  - Artifacts/Generative UI: React, HTML, Mermaid diagrams
  - Code Interpreter API: provides a secure and hassle-free way to execute code and manage files through a simple API
  - 🖼️ Image Generation & Editing: GPT-Image-1, Flux, Stable Diffusion(local), MCP Servers

- cons
  - Code Interpreter 未开源

- features
  - Web Search: Combines search providers, content scrapers, result rerankers 
  - Memory: Users can toggle memory on/off for individual chats
  - MCP: Support for scalable HTTP-based servers
  - AI Models
  - 🔌 Plugins: deprecated. It is recommend to use MCP for integrating custom tools
  - 💾 chat export/import
  - Create, Save, & Share Custom Presets
  - Conversation Branching: Branch conversations to explore different discussion paths without losing context
  - Fork Messages & Conversations: Split messages to create multiple conversation threads
  - Temporary Chat: private conversations that won’t clutter your history
  - Multimodal Chat: Image Analysis, File Interaction
  - Hands-Free Chat: stt, tts
  - Comprehensive Configuration Options
  - Flexible Auth: OAuth2-OIDC, email, LDAP

- who is using #librechat
  - ?
# draft
- code interpreter 如何实现
  - open source alternative

- tool应该支持在ui上配置
  - tool级别的prompt
  - stable-diffusion文生图的工具应该支持配置steps/选择不同效果的模型

- 默认图片输出目录`imageOutput`为 `client/public/images/{userId}/imageName.png`, 需要提供环境变量支持配置到外部系统

- 
- 
- 
- 
- 

# dev-xp
- image-sd-webui
  - chat生成的图片不会出现在sd-webui源码的 `outputs` 文件夹
  - 本地模型最好选择同时支持 tool-use + vision, 否则生成图片后会提升异常
    - Error in iterating prediction stream: ValueError: Vision add-on is not loaded, but images were provided for processing

- [[Bug]: error: [getAvailableTools] MCPManager has not been initialized. _202509](https://github.com/danny-avila/LibreChat/issues/9437)
  - 导致添加stable-diffusion工具失败，更新到最新代码就可以了
# more
