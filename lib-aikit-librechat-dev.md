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
- ❓ chat-queue: 对于很慢的本地模型，一次只能处理一个task，需要支持添加多个task到queue, 不同task可能需要切换不同模型
  - message queue, image queue

- librechat-custom-agent
  - custom comfyui workflow as custom agent
  - ai-table
  - ai-chart

- docs/knowledgebase
  - granite-docling

- comfyui-local: ollama与comfyui结合的产品形态应该是怎样的
  - support tool config: steps, sampler, scheduleer, style-preset
  - ✨ 测试需求: 将comfyui中多模型测试输出的能力迁移到文本模型

- mermaid
  - 文生图难度高，但基于文本的流程图难度低很多，如集成 mermaid

- chart
  - markdown-chart + llm

- code interpreter 如何实现
  - open source alternative

- tool应该支持在ui上配置参数
  - tool级别的prompt
  - stable-diffusion文生图的工具应该支持配置steps/选择不同效果的模型

- 默认图片输出目录`imageOutput`为 `client/public/images/{userId}/imageName.png`, 需要提供环境变量支持配置到外部系统

- 针对mlx优化的版本，主要是后端多模型及切换模型的优化
  - 主要开发前端，是否有必要做后端?

- oauth登录的交互及ui需要针对框架定制

- 
- 
- 
- 

# dev-xp
- code artifacts对于某些模型很难触发，实测devstral难触发，gemma3-12b较容易触发

- 本地已有用户迁移到openid的方式，手动将mongodb的`users`表中对应用户的数据修改为 `provider: ""`, 然后用本地用户原邮箱登陆到openid

- 不同浏览器在退出登录后，再次选择openid登录时能快速登录到各自的上个帐号

## comfyui-integration

- o1: 最简单的方式是，直接去comfyui的output文件夹读取生成的图片为 base64，不推荐此方法因为模型/输出文件夹可能变化那读取路径也会跟着变，已有工作流配置好的output可能各不相同
- o2: 不需要comfyui server保存图片，使用自定义server封装请求comfyui的api，获取图片输出并转换为base64再转发给librechat服务端
- o3: 使用主流comfyui-mcp-server或自定义mcp-server，按o2的方式定制逻辑

## image

- image-sd-webui
  - chat生成的图片不会出现在sd-webui源码的 `outputs` 文件夹, 而在 默认的imageOutput 文件夹
  - 有时文生图失败，可尝试新建一个agent或换模型，也许就能work
  - 本地模型最好选择同时支持 tool-use + vision, 否则生成图片后会提升异常
    - Error in iterating prediction stream: ValueError: Vision add-on is not loaded, but images were provided for processing
  - 在SDAPI(extends Tool)的`_call`方法生成图片base64后没有立刻保存图片到磁盘，而是在 api/server/controllers/agents/callbacks.js 的 `createToolEndCallback` 方法中检查 `output.artifact.content` 是否存在，若存在才将 content 中的 `image_url`保存到磁盘

- 文生图相关请求
  - GET http://localhost:3090/api/agents/tools/calls?conversationId=10198a1b-2fc3-47d0-966f-17d03dc8f3e1

- [[Bug]: error: [getAvailableTools] MCPManager has not been initialized. _202509](https://github.com/danny-avila/LibreChat/issues/9437)
  - 导致添加stable-diffusion工具失败，更新到最新代码就可以了
# more
