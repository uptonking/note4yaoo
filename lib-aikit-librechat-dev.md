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

- pm
  - 聊天类应用是否该采用多tab设计，这样可以在其他tab打开链接/附件/生成的ppt
  - 左右分栏视图比多tab体验更好
# draft
- roadmap
  - 支持直接在界面上配置大模型url, 可参考openwebui/janai
  - 支持多backends的架构可参考 
  - 有一类给website添加search的产品，可参考实现添加chat的产品，特别是支持主流ssg工具的 search/chat
  - 快捷常用语

- 🖼️ 对话时如何无缝插入图片(mistral网页版支持)
  - 方案1: 预置unsplash图片，或外部图片搜索工具/MCP
  - 方案2: svg形式的图片，多模型并行执行，然后实时组装

- 针对 vlm 优化的 agent/工作流

- 利用chrome最新的侧边栏，实现类似cline/roocode的页面ai助理/office编辑
  - 基于cline-cli的client/server架构，支持多种工具如 wps/飞书/腾讯文档/notion
  - 甚至结合文生图

- 🤔 一种思路: tool-call时使用擅长tool-call的模型，分析时使用公益站的聊天优质但无法tool-call的模型
  - 支持类似 roocode 的 model profile 切换

- ❓ chat-queue: 对于很慢的本地模型，一次只能处理一个task，需要支持添加多个task到queue, 不同task可能需要切换不同模型
  - message queue, image queue
  - queue的必要性: ollama能设置并发数, 其他provider能吗
  - 通过queue自动收集不同模型对同一prompt的输出，最终汇总结果并自动分析
  - queue中的message支持删除

- librechat-custom-agent
  - custom comfyui workflow as custom agent
  - ai-table
  - ai-chart

- docs/knowledgebase
  - granite-docling
  - model for data like statistics/papers

- comfyui-local: ollama与comfyui结合的产品形态应该是怎样的
  - support tool config: steps, sampler, scheduleer, style-preset
  - ✨ 测试需求: 将comfyui中多模型测试输出的能力迁移到文本模型

- mermaid
  - 文生图难度高，但基于文本的流程图难度低很多，如集成 mermaid

- chart
  - markdown-chart + llm

- chat-sources
  - wikipedia(kiwix)
  - dictionaries(mdx/kiwix)
  - ebooks

- code interpreter 如何实现
  - open source alternative
- [【提示词工程】Canvas助手（推荐 AI Studio），让模型用HTML回复，支持Graphviz逻辑流程图、Echarts图表 ](https://linux.do/t/topic/590614/21)
  - 可参考html将其转换为低代码形式的交互

- tool应该支持在ui上配置参数
  - tool级别的prompt
  - stable-diffusion文生图的工具应该支持配置steps/选择不同效果的模型

- 默认图片输出目录`imageOutput`为 `client/public/images/{userId}/imageName.png`, 需要提供环境变量支持配置到外部系统

- oauth登录及退出登录的交互及ui需要针对框架定制
  - authentik切换到keycloak后, social login button的文字及图标未改变，但登录逻辑已顺利改变

- 聊天类软件都可考虑自动添加标签/分组

- 优化artifacts/coding的交互为类似aionui/discord-channel的收窄侧边栏效果，侧边栏并不是收窄为仅图标，而是图标+几个文字
- 采用类似vscode文件图标的方案在chat前显示图标

- 
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

- 图文混排编辑的方案
  - 基于coding的方案，参考lovable/lovart/mj-studio
  - 文档元数据需要包含文档prompt、图片prompt、图片编辑prompt，以timeline的形式，尽量朝着reproducible内容的方向去探索

- [[Bug]: error: [getAvailableTools] MCPManager has not been initialized. _202509](https://github.com/danny-avila/LibreChat/issues/9437)
  - 导致添加stable-diffusion工具失败，更新到最新代码就可以了
# more
