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
  - an open-source AI-native creation engine powered by 13+ leading AI models. 
  - Its intuitive free-form canvas interface integrates multi-threaded conversations, multimodal inputs (text/images/files), RAG 
# workflow-ai
- https://github.com/FlowiseAI/Flowise /42.5kStar/apache2+EE/202508/ts
  - https://flowiseai.com/
  - https://docs.flowiseai.com/
  - Drag & drop UI to build your customized LLM flow
  - Open source low-code tool for developers to build customized LLM orchestration flow & AI agents
  - 大量使用 LangchainJS, 支持langchain的各种组件

- https://github.com/browser-use/workflow-use /AGPL/python
  - Create and run workflows (RPA 2.0)
  - https://x.com/gregpr07/status/1923595378286268812
    - we started Workflow Use (Playwright on steroids):
    - Show browser once, run forever
    - 10x faster, ~90% cheaper than pure LLM agents
    - Self-healing via LLM fallback 

- https://github.com/langflow-ai/langflow /109kStar/MIT/202508/python/ts
  - http://www.langflow.org/
  - a powerful tool for building and deploying AI-powered agents and workflows.
  - It provides developers with both a visual authoring experience and a built-in API server that turns every agent into an API endpoint that can be integrated into applications built on any framework 
  - 大量使用langchain

- https://github.com/1Panel-dev/MaxKB /15.5kStar/GPL/202504/python/ts/vue
  - https://maxkb.pro/
  - 基于大模型和 RAG 的开源知识库问答系统
  - it is a ready-to-use RAG chatbot that features robust workflow and MCP tool-use capabilities. 
  - 依赖django、langchain、pgvector、Vue
  - Flexible Orchestration: Equipped with a powerful workflow engine, function library and MCP tool-use, enabling the orchestration of AI processes to meet the needs of complex business scenarios.

- https://github.com/PySpur-Dev/PySpur /5.4kStar/apache2/202507/python/ts
  - https://pyspur.dev/
  - A visual playground for agentic workflows: use it to build agents, execute them step-by-step and inspect past runs.
  - Build the agent in Python code or via UI
  - Human in the Loop: Persistent workflows that wait for human approval.
  - Structured Outputs: UI editor for JSON Schemas.
  - RAG: Parse, Chunk, Embed, and Upsert Data into a Vector DB.
  - Multimodal: Support for Video, Images, Audio, Texts, Code.
  - Python-Based: Add new nodes by creating a single Python file.
  - By default, this will start PySpur app at http://localhost:6080 using a sqlite database.
  - Using Local Models with Ollama: PySpur only works with models that support structured-output and json mode. Most newer models should be good
  - [ComfyUI for LLMs : r/comfyui _202412](https://www.reddit.com/r/comfyui/comments/1hgfy3g/comfyui_for_llms/)

- https://github.com/nocode-js/sequential-workflow-designer /1.2kStar/MIT/202502/ts/NoDeps
  - https://nocode-js.com/
  - Customizable no-code component for building flow-based programming applications or workflow automation
  - written in pure TypeScript and uses `SVG` for rendering
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
# ai-designer/lovable
- https://github.com/mendableai/open-lovable /8.3kStar/MIT/202508/ts
  - Clone and recreate any website as a modern React app in seconds
  - Chat with AI to build React apps instantly. Made by the Firecrawl team.
  - 基于e2b sandbox实现

- https://github.com/dyad-sh/dyad /14.2kStar/apache2/202508/ts
  - https://dyad.sh/
  - Free, local, open-source AI app builder 
  - v0 / lovable / Bolt alternative 
  - Easy to run on Mac or Windows.
  - https://github.com/dyad-sh/sandpack-bundler /apache2
    - The new bundler/runtime powering client-side sandpack sandboxes

- https://github.com/11cafe/jaaz /2.3kStar/NonComm/202508/python/ts
  - https://jaaz.app/
  - AI design agent, local alternative for Lovart. Canva + Cursor. 
  - Infinite Canvas & Visual Storyboarding Plan scenes with an unlimited canvas
  - 社区许可证： 面向个人及组织有限使用的免费许可证。
  - 商业许可证： 任何内部团队部署，或对代码的任何二次开发或修改，都必须获取商业许可证。
  - [Jaaz's "completely" self-hosted? _202508](https://github.com/11cafe/jaaz/issues/252)
    - if you use ollama and add comfyui workflows for image generations, it will be fully self hosted. Or add your own replicate api key, you can also self host
  - [Self-hosted image generation and LLM API _202506](https://github.com/11cafe/jaaz/issues/21)
    - you want to local host your stable diffusion models or Flus models? Yea we will support that through local comfyui image generations
  - [WIP: support ComfyUI  _202506](https://github.com/11cafe/jaaz/pull/7)
    - add ComfyUI installation & install dialog, add adm-zip
    - Get the latest ComfyUI release information from GitHub
    - refactor: Standalone comfyUI installation logic

- https://github.com/onlook-dev/onlook /apache2/202502/ts
  - https://onlook.com/
  - The open source Cursor for Designers. 
  - Design directly in your live React app and publish your changes to code.

## ai-webapp

- https://github.com/admineral/Reactor /202405/ts/inactive
  - https://reactor-dev.vercel.app/
  - Chat with React Code-Editor and Live-preview using Sandpack by Codesandbox
  - An experimental preview of AI SDK 3.0 with Generative UI support

- https://github.com/asj9469/Reactonaut /13Star/NALic/202308/js/inactive
  - an online React code editor with an AI assistant. 
  - Live code editing with Ace Editor
  - React-Live for real-time rendering of React components
  - OpenAI's ChatGPT API integration for code suggestions
  - Reactonaut is the general/public version of his original project Reactor with a new UI and enhanced features. It was developed during our collaboration in an AI Startup Hackathon.

- https://github.com/Nutlope/llamacoder /6.5kStar/MIT/202508/ts
  - https://www.llamacoder.io/
  - open source Claude Artifacts – generate small apps with one prompt. 
  - Powered by Llama 3 on Together.ai.
  - Sandpack for the code sandbox
  - Next.js app router with Tailwind
  - 🍴 forks
  - https://github.com/Hassanrkbiz/llamacoder-any-llm /202412/inactive
    - Multiple LLMs & Providers Added
    - Local LLMs (Ollama & LM Studio) Added
    - Image Support

- https://github.com/etrobot/nextArtifacts /MIT/202409/ts/inactive
  - https://github.com/etrobot/nextArtifacts
  - A Next.js version of Claude Aritfacts , inspired by llamacoder
  - generate small applications using any Large Language Model (LLM) API compatible with the OpenAI format. 
  - This project is inspired by and modified from llamacoder, which uses Llama 3 405B & Together.ai.
- https://github.com/xKevIsDev/GenUAI /202408/ts/inactive
  - AI to UI generation app that uses Shadcn, Aceternity, MagicUI, SyntaxUI built in components to generate websites.
  - forked and adapted from llamacoders

- https://github.com/iotserver24/pollin-coder /MIT/202508/ts
  - https://pollin-coder.megavault.in/
  - open-source AI code generator that lets you create small apps with a single prompt
  - Powered by advanced AI models and the Pollinations.ai platform
  - Generate full-stack apps or code snippets from a single prompt
  - Uses state-of-the-art models for code and text generation
  - Live code sandbox powered by Sandpack
  - Built with Next.js, Tailwind CSS, and modern web tech
  - Pollinations AI for LLM inference

- https://github.com/TesslateAI/Builder-Lite /202504/ts/inactive
  - A web application that allows you to generate React components using an AI chat interface and view/edit them live in a Sandpack sandbox environment.
  - Describe the component you need, and the AI will attempt to generate the code, which is then rendered instantly for preview.
  - Live Sandbox Environment: Uses @codesandbox/sandpack-react to provide an instant preview
  - Integrated Code Editor: View and modify the generated Component.tsx code directly in the 'Editor' tab.
  - Dependencies Included: The sandbox automatically includes react, react-dom, framer-motion, and @heroicons/react for richer component possibilities.
  - Optional Proxy: Built-in logic to route API requests through a local proxy (/llm-proxy) if the target API is not on localhost (requires separate proxy setup).
# ai-apps

# more
