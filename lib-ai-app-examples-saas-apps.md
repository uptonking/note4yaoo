---
title: lib-ai-app-examples-saas-apps
tags: [ai, examples, large-language-model, saas]
created: 2025-02-21T17:16:46.331Z
modified: 2025-02-21T17:17:42.225Z
---

# lib-ai-app-examples-saas-apps

# guide

- tips
  - bpmn + ai
# popular
- https://github.com/OpenHealthForAll/open-health /AGPL/202502/ts
  - https://www.open-health.me/
  - AI Health Assistant | Powered by Your Data
  - Smart Parsing: Automatically parses your health data and generates structured data files.
  - Contextual Conversations: Use the structured data as context for personalized interactions with GPT-powered AI.
# open-canvas
- https://github.com/refly-ai/refly /apache2/202503/ts
  - https://refly.ai/
  - Refly is an open-source AI-native creation engine powered by 13+ leading AI models. 
  - Its intuitive free-form canvas interface integrates multi-threaded conversations, multimodal inputs (text/images/files), RAG 
# workflow-ai
- https://github.com/browser-use/workflow-use /AGPL/python
  - Create and run workflows (RPA 2.0)
  - https://x.com/gregpr07/status/1923595378286268812
    - we started Workflow Use (Playwright on steroids):
    - Show browser once, run forever
    - 10x faster, ~90% cheaper than pure LLM agents
    - Self-healing via LLM fallback 

- https://github.com/langflow-ai/langflow /52.9kStar/MIT/202503/python/ts
  - http://www.langflow.org/
  - a powerful tool for building and deploying AI-powered agents and workflows.
  - It provides developers with both a visual authoring experience and a built-in API server that turns every agent into an API endpoint that can be integrated into applications built on any framework 

- https://github.com/1Panel-dev/MaxKB /15.5kStar/GPL/202504/python/ts/vue
  - https://maxkb.pro/
  - 基于大模型和 RAG 的开源知识库问答系统
  - it is a ready-to-use RAG chatbot that features robust workflow and MCP tool-use capabilities. 
  - 依赖django、langchain、pgvector、Vue
  - Flexible Orchestration: Equipped with a powerful workflow engine, function library and MCP tool-use, enabling the orchestration of AI processes to meet the needs of complex business scenarios.

- https://github.com/nocode-js/sequential-workflow-designer /1.2kStar/MIT/202502/ts/NoDeps/svg
  - https://nocode-js.com/
  - Customizable no-code component for building flow-based programming applications or workflow automation
  - written in pure TypeScript and uses SVG for rendering
  - This designer is not associated with any workflow engine. 
  - the definition is stored as JSON
  - https://github.com/nocode-js/sequential-workflow-editor /MIT/vanillajs
    - Mainly designed to work with the Sequential Workflow Designer
  - https://github.com/nocode-js/sequential-workflow-machine /MIT/202408/ts
    - Powerful sequential workflow machine for front-end and back-end applications.
    -  It provides a simple API for creating its own step execution handlers (activities). It supports multiple types of activities. 
    - Internally it uses the `xstate` library.
    - This machine uses the same data model as the Sequential Workflow Designer.
  - [Pricing of Sequential Workflow Designer Pro](https://nocode-js.com/sequential-workflow-designer-pro-pricing)
    - Pro Step Components
    - Custom Theme

- https://github.com/FlowiseAI/Flowise /apache2/202406/ts
  - https://flowiseai.com/
  - https://docs.flowiseai.com/
  - Drag & drop UI to build your customized LLM flow
  - Open source low-code tool for developers to build customized LLM orchestration flow & AI agents
  - 支持langchain的各种组件

- https://github.com/samdenty/react-ai-flow /202503/ts
  - https://react-ai-flow.com/
  - smooth React AI chatbot primitives
  - 支持多种打字动画效果 per character/word/line, 支持react/vanillajs
  - This library uses a single canvas-rendered mask-image, so we can do pixel-level fade-in effects.
  - Other libraries can accomplish at most a per-character opacity animation with a HTML soup
  - This library also features a super customizable text splitter API. Pick a built-in splitter (character, word, line, sentence) or provide you own function that splits the visually rendered text on screen.
  - https://x.com/samddenty/status/1905843003471581337
    - I just created a demo website for https://react-ai-flow.com a super advanced cross-framework library for smooth LLM text streaming effects & also text-staggers.

- https://github.com/gensx-inc/gensx /apache2/202502/ts
  - https://gensx.com/
  - The TypeScript framework for agents & workflows with react-like components.
  - GenSX takes a lot of inspiration from React, but the programming model is very different - it’s a Node.js framework designed for data flow.
  - Pure Functions: Components are pure TypeScript functions that are easily testable, reusable, and sharable
  - Parallel by Default: Components execute in parallel when possible while maintaining dependencies
  - Full TypeScript support with no DSLs or special syntax - just standard language features
  - Streaming Built-in: Stream responses with a single prop change, no refactoring needed
  - https://x.com/_Evan_Boyle/status/1892590845485895730
    - GenSX components are reusable by default and are easy to consume and share. 

- https://github.com/Onelevenvy/flock /apache2/202502/python/ts
  - 一个基于工作流 workflow 的低代码平台：Flock。
  - 基于 LangChain 和 LangGraph 构建，提供灵活的低代码编排协作代理解决方案，可用于快速构建聊天机器人、RAG 应用和协调多代理团队。
  - 支持聊天机器人、RAG 应用、代理和多代理系统，并具备离线运行能力。
# ai-figure/数字人
- https://github.com/taoofagi/easegen-front
  - 开源的数字人课程制作项目：easegen，它提供从课程制作、视频管理、智能课件生成到智能出题全套方案
  - 支持ppt课件批量自动生成、数字人克隆、声音克隆、数字人课程设计、数字人视频渲染等
  - https://x.com/aigclink/status/1847102226088841648
# cv
- https://github.com/roboflow/supervision /MIT/202502/python
  - https://supervision.roboflow.com/
  - We write your reusable computer vision tools. Whether you need to load your dataset from your hard drive, draw detections on an image or video, or count how many detections are in a zone.
  - Supervision was designed to be model agnostic. Just plug in any classification, detection, or segmentation model.
    - we have created connectors for the most popular libraries like Ultralytics, Transformers, or MMDetection.
# image
- https://github.com/Nutlope/logocreator /202411/ts
  - https://www.logo-creator.io/
  - A free + OSS logo generator powered by Flux on Together AI
  - Flux Pro 1.1 on Together AI for logo generation
  - nextjs + shadcn + redis + clerk + plausible
  - Create a .env file and add your Together AI API key: TOGETHER_API_KEY=
  - [license · Issue · Nutlope/logocreator](https://github.com/Nutlope/logocreator/issues/16)
# ai-apps

# more
