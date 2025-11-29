---
title: lib-ai-app-examples
tags: [ai, examples]
created: 2023-02-08T07:20:33.048Z
modified: 2023-02-08T07:20:48.475Z
---

# lib-ai-app-examples

# guide
- not-yet ❓
  - model routing
# popular
- https://github.com/mudler/LocalAI /36.2kStar/MIT/202511/go
  - https://localai.io/
  - free, Open Source OpenAI alternative. 
  - Self-hosted, community-driven and local-first. 
  - LocalAI act as a drop-in replacement REST API that’s compatible with OpenAI API specifications for local inferencing. 
  - It allows you to run LLMs, generate images, audio (and not only) locally or on-prem with consumer grade hardware, supporting multiple model families. 
  - Does not require GPU.
  - text-backend: llama.cpp, vLLM, MLX
  - audio-backend: whisper.cpp, kokoro
  - image-backend: stablediffusion.cpp, diffusers
  - [Add Local ComfyUI/SD base diffusers step with "json API" PLZ _202502](https://github.com/mudler/LocalAI/issues/4818)
    - 不支持

- https://github.com/janhq/jan /AGPLv3/202403/ts
  - https://jan.ai/
  - an open source alternative to ChatGPT that runs 100% offline on your computer
  - Nitro is a high-efficiency C++ inference engine for edge computing. It is lightweight and embeddable

- https://github.com/Doriandarko/maestro /202406/python
  - ⛓️ A framework for Claude Opus to intelligently orchestrate subagents.
  - This Python script demonstrates an AI-assisted task breakdown and execution workflow using the Anthropic API. 
  - It utilizes two AI models, Opus and Haiku, to break down an objective into sub-tasks, execute each sub-task, and refine the results into a cohesive final output.
  - Run locally with LMStudio or Ollama
  - Breaks down an objective into manageable sub-tasks using the Opus model
  - Executes each sub-task using the Haiku model
  - Refines the sub-task results into a final output using the Opus model
  - Generates a detailed exchange log capturing the entire task breakdown and execution process
  - Required Python packages: anthropic and rich
  - https://x.com/tuturetom/status/1805823266671775875
    - 基于 Claude 3.5 Sonnet 实现的「多 Agent 调度」框架
    - 同时提供了 Python flask 应用支持 UI Demo 完成多 Agent 演示
    - orchestrator 拆解任务，全局视野调度 sub_agent 

- https://github.com/run-llama/llama-agents /MIT/202407/python
  - llama-agents is an async-first framework for building, iterating, and productionizing multi-agent systems, including multi-agent communication, distributed tool execution, human-in-the-loop, and more!
  - each agent is seen as a service, endlessly processing incoming tasks. Each agent pulls and publishes messages from a message queue.
  - At the top of a llama-agents system is the control plane. The control plane keeps track of ongoing tasks, which services are in the network, and also decides which service should handle the next step of a task using an orchestrator.
  - https://x.com/tuturetom/status/1809445355832111312
    - 多 Agent 框架，使用 Docker/K8S 部署

- https://github.com/dstackai/dstack /MPL/202407/python
  - https://dstack.ai/
  - open-source container orchestration engine designed for running AI workloads across any cloud or data center. 
  - It simplifies dev environments, running tasks on clusters, and deployment.

- https://github.com/DataformerAI/dataformer /apache2/202410/python
  - https://dataformer.ai/
  - Dataformer empowers engineers with a robust framework for creating high-quality synthetic datasets for AI, offering speed, reliability, and scalability
  - We integrate with multiple LLM providers using one unified API and allow you to make parallel async API calls while respecting rate-limits.

- https://github.com/badboysm890/ClaraVerse /3kStar/MIT/202508/ts
  - https://claraverse.space/
  - Privacy-first, fully local AI workspace with Ollama LLM chat, tool calling, agent builder, Stable Diffusion, and embedded n8n-style automation. 
  - No backend. No API keys. Just your stack, your machine.
  - The Story Behind ClaraVerse: Why can't everything be in a single app?
  - The Solution: One App. Six Tools. Zero Compromises.
  - Built on the shoulders of giants: llama.cpp • llama-swap • faster-whisper • ComfyUI • N8N
  - 🍴 forks
  - https://github.com/vanvuongngo/ClaraN /MIT/202508/ts
    - This is a hardfork of ClaraVerse
    - Tauri for building Desktop- and Mobile apps 
    - Qwik web framework for building performant Web UIs
    - DaisyUI for faster, cleaner and simple tailwind CSS UI development
# LLM
- https://github.com/songquanpeng/one-api /MIT/202404/go/js
  - https://openai.justsong.cn/
  - OpenAI 接口管理 & 分发系统，支持 Azure、Anthropic Claude、Google PaLM 2 & Gemini、智谱 ChatGLM、百度文心一言、讯飞星火认知、阿里通义千问
  - 可用于二次分发管理 key，仅单可执行文件，已打包好 Docker 镜像，一键部署，开箱即用

- https://github.com/xenova/transformers.js
  - Run Transformers in your browser! We currently support BERT, ALBERT, DistilBERT, MobileBERT, SqueezeBERT, T5, T5v1.1, FLAN-T5, mT5, BART
  - [宝玉 on Twitter: "这有必要吗？"](https://twitter.com/dotey/status/1643801825580122115)
    - 毕竟浏览器有沙盒，相对在本地运行一个没审计过的程序放心一点，但现在浏览器对gpu硬件支持还是拉胯。
    - 这是分布式算力啊，这不就是挖矿嘛

- https://github.com/outlines-dev/outlines /apache2/202408/python
  - https://outlines-dev.github.io/outlines/
  - Robust (structured) text generation.
  - The first step towards reliability of systems that include large language models is to ensure that there is a well-defined interface between their output and user-defined code. Outlines provides ways to control the generation of language models to make their output more predictable.
  - Multiple model integrations: OpenAI, transformers, llama.cpp, exllama2, mamba
  - Simple and powerful prompting primitives based on the Jinja templating engine
  - Fast JSON generation following a JSON schema or a Pydantic model
  - Interleave completions with loops, conditionals, and custom Python functions

## benchmarks-llm

- https://github.com/bigcode-project/bigcodebench /apache2/202408/python
  - https://bigcode-bench.github.io/
  - BigCodeBench is an easy-to-use benchmark for code generation with practical and challenging programming tasks
  - It aims to evaluate the true programming capabilities of large language models (LLMs) in a more realistic setting.
  - The package is built on top of the EvalPlus framework, which is a flexible and extensible evaluation framework for code generation tasks.
  - [2024-06-18] We release BigCodeBench, a new benchmark for code generation with 1140 software-engineering-oriented programming tasks. Preprint is available here
# chatgpt
- app-site
  - https://github.com/LiLittleCat/awesome-free-chatgpt
  - [免费 chatgpt](https://twitter.com/search?q=%E5%85%8D%E8%B4%B9%20chatgpt&src=typed_query&f=live)

- api-free
  - [一口气送了350个免费的key](http://freeopenai.xyz/)

- https://freechatgpt.chat/
  - 类似官网，需要key
  - 可选内置不稳定key

- [ChatGPT API Demo](https://ai.ls/)
  - https://ai.ls/
  - Powered by gpt-3.5-turbo

- [free ChatGPT](https://freegpt.one/)
  - using gpt-3.5-turbo

- [OpenGPT](https://open-gpt.app/)
  - 立即使用海量的 ChatGPT 应用，或在几秒钟内创建属于自己的应用

- https://github.com/lencx/ChatGPT /rust
  - ChatGPT Desktop Application (Mac, Windows and Linux)
  - 国内ip无法访问

## gpt-apps

- https://github.com/enricoros/big-AGI /6.6kStar/MIT/202508/ts
  - https://big-agi.com/
  - AI suite powered by state-of-the-art models and providing advanced AI/AGI functions
  - New AIX framework lets us scale features we couldn't before

- https://github.com/n4ze3m/dialoqbase /MIT/202401/ts
  - https://dialoqbase.n4ze3m.com/
  - open-source application designed to facilitate the creation of custom chatbots using a personalized knowledge base

- https://github.com/KolosalAI/Kolosal /297Star/apache2/202505/cpp/inactive
  - https://kolosal.ai/
  - OpenSource and Lightweight alternative to LM Studio to run LLMs 100% offline on your device
  - On Linux/macOS, ensure .so/.dylib are in the library search path or same folder.
  - Is this windows only? Unfortunately currently yes. But, we're using framework that mostly is crossplatform
  - https://github.com/KolosalAI/kolosal-server /apache2/202509/cpp
    - inference server for large language models with OpenAI-compatible API endpoints. Now available for both Windows and Linux systems

- https://github.com/iBz-04/offeline /MIT/202510/ts
  - https://offeline.site/
  - Offeline is a privacy-first desktop & web app for running LLMs locally on your hardware using multiple backend options
  - All AI models run locally on your hardware. No data is sent
  - Multi-Platform: Use via browser (web app) or native desktop application with Electron
  - Offline-Capable: Download models once, use them offline indefinitely (WebGPU mode)
  - Multiple AI Backends: Choose your preferred inference engine:
    - Ollama - Manage and run models with Ollama backend
    - llama.cpp - CPU/GPU optimized inference on desktop
    - WebGPU - Run models directly in your browser using GPU acceleration
  - File Embeddings: Load and ask questions about documents (PDF, MD, DOCX, TXT, CSV, RTF) - fully locally
  - Voice Support: Interact with the AI using voice messages
  - Export Conversations: Save your chats as JSON or Markdown

- https://github.com/binary-husky/gpt_academic /GPLv3/202405/python/js
  - https://github.com/binary-husky/gpt_academic/wiki/online
  - 为GPT/GLM等LLM大语言模型提供实用化交互接口，特别优化论文阅读/润色/写作体验，模块化设计，支持自定义快捷按钮&函数插件，支持Python和C++等项目剖析&自译解功能，PDF/LaTex论文翻译&总结功能，支持并行问询多种LLM模型，支持chatglm3等本地模型。
  - 接入通义千问, deepseekcoder, 讯飞星火, 文心一言, llama2, rwkv, claude2, moss等。

- https://github.com/imyuanx/ai-lawyer
  - 写了个基于 ChatGPT 的 AI 维权律师，根据事实和诉求帮当事人生成起诉书。
  - https://twitter.com/imyuanx/status/1641715695762436098

- https://github.com/nicepkg/gpt-runner
  - Conversations with your files! Manage and run your AI presets!

- https://github.com/AprilNEA/ChatGPT-Admin-Web /MIT/202312/ts/inactive
  - CAW 是一个自托管网络应用程序，提供开箱即用的用户管理，包括后台界面以及可配置的支付计划和相关支付界面
  - Nest.js + Next.js
  - 开箱即用的用户管理
  - 付费方案配置，一键对接支付接口
  - 关键词过滤、替换保证文本安全

- https://github.com/amd/gaia /MIT/202510/python
  - Run LLM Agents on Ryzen AI PCs in Minutes
  - GAIA is specifically designed for AMD Ryzen AI systems and uses Lemonade Server for optimal hardware utilization
  - GAIA UI is an optional, modern web-based interface for GAIA, built on the RAUX (Open-WebUI fork) platform.

- [Reproducing Karpathy’s NanoChat on a Single GPU — Step by Step with AI Tools : r/LocalLLaMA _202510](https://www.reddit.com/r/LocalLLaMA/comments/1o76ev6/reproducing_karpathys_nanochat_on_a_single_gpu/)

- https://github.com/LostRuins/koboldcpp /AGPL/cpp
  - KoboldCpp is an easy-to-use AI text-generation software for GGML and GGUF models, inspired by the original KoboldAI. 
  - It's a single self-contained distributable that builds off llama.cpp and adds many additional powerful features.
  - Single file executable, with no installation required and no external dependencies
  - Runs on CPU or GPU, supports full or partial offloaded
  - Image Generation (Stable Diffusion 1.5, SDXL, SD3, Flux)
  - Speech-To-Text (Voice Recognition) via Whisper
- https://github.com/lone-cloud/gerbil /AGPL/202511/ts
  - A desktop app for running Large Language Models locally.
  - [Gerbil: An open source desktop app for running LLMs locally : r/LocalLLaMA](https://www.reddit.com/r/LocalLLaMA/comments/1ol9cai/gerbil_an_open_source_desktop_app_for_running/)
    - Under the hood it runs llama.cpp (via koboldcpp) backends and allows easy integration with the popular modern frontends like Open WebUI, SillyTavern, ComfyUI, StableUI (built-in) and KoboldAI Lite (built-in).

## api

- [https://www.steamship.com](https://www.steamship.com/)
  - SteamShip 开放了 GPT-4 的模型接口，只需要注册SteamShip 账号，无需付费，几行代码直接就能调用 GPT-4

## prompts

- [Open Prompt](https://openprompt.co/)

- https://github.com/verazuo/jailbreak_llms
  - A dataset consists of 15, 140 ChatGPT prompts from Reddit, Discord, websites, and open-source datasets (including 1, 405 jailbreak prompts).
  - 开源了论文中使用的 15, 140 个 ChatGPT 提示，其中包括 1, 405 个越狱提示，收集于 Reddit、Discord、网站和开源数据集。
# llm-impl
- https://github.com/ideaweaver-ai/qwen3-from-scratch /apache2/202509/python
  - A complete implementation of a Qwen3-based language model trained on the TinyStories dataset. 
  - This project demonstrates modern transformer architecture with Grouped Query Attention, SwiGLU activation, and Rotary Position Embeddings.
  - Efficient Training: Mixed precision training with gradient accumulation
  - Memory Optimized: Uses memory mapping for large dataset handling
  - Text Generation: Built-in generation capabilities with temperature and top-k sampling
  - Progress Monitoring: Real-time training progress and loss visualization
  - Model Size: 283M parameters
  - [Building Qwen3 from Scratch: This Is your chance : r/LocalLLaMA _202509](https://www.reddit.com/r/LocalLLaMA/comments/1ndxjsu/building_qwen3_from_scratch_this_is_your_chance/)
  - https://github.com/Emericen/tiny-qwen

- https://github.com/newhouseb/potatogpt
  - Pure Typescript, dependency free, ridiculously slow implementation of GPT2 for educational purposes

- https://github.com/openai/gpt-2 /MIT/201908/python
  - https://openai.com/blog/better-language-models/
  - Code for the paper "Language Models are Unsupervised Multitask Learners"
- https://github.com/openai/gpt-3 /202009/仅数据
  - GPT-3: Language Models are Few-Shot Learners
# coding-copilot
- products
  - https://copilot.microsoft.com/

- https://github.com/Codium-ai/pr-agent /apache2/202407/python
  - CodiumAI PR-Agent: An AI-Powered Tool for Automated Pull Request Analysis, Feedback, Suggestions
  - aims to help efficiently review and handle pull requests, by providing AI feedbacks and suggestions
  - Our JSON prompting strategy enables to have modular, customizable tools. 
  - We support multiple git providers (GitHub, Gitlab, Bitbucket), multiple ways to use the tool (CLI, GitHub Action, GitHub App, Docker, ...), and multiple models (GPT-4, GPT-3.5, Anthropic, Cohere, Llama2).
  - PR-Agent Pro is a hosted version of PR-Agent, provided by CodiumAI
    - Extra features - emphasize more customization, and the usage of static code analysis, in addition to LLM logic, to improve results. See here for a list of features available in PR-Agent Pro.
  - https://x.com/tuturetom/status/1809053337825989009
    - 自动基于你提交的代码进行分析，给于评论反馈与意见，生成 PR 描述
    - 支持私有化部署和开源模型
    - 针对大的 PR 设计了 PR Compression 策略，可以极大的处理几百个文件的场景

- https://github.com/TabbyML/tabby /apache2/202408/rust
  - https://tabbyml.github.io/tabby
  - Self-hosted AI coding assistant. 
  - An opensource / on-prem alternative to GitHub Copilot.
  - Self-contained, with no need for a DBMS or cloud service
  - OpenAPI interface, easy to integrate with existing infrastructure (e.g Cloud IDE).
  - Tabby 是一个自我托管的 #GitHub #Copliot 开源替代品，自带可视化界面与 #OpenAPI 接口，还支持消费者级别的 #GPU，具有 FP-16 重量加载和各种优化功能，提供了 #Docker 镜像

- https://github.com/rjmacarthy/twinny /995Star/MIT/202403/ts
  - The most no-nonsense locally hosted (or API hosted) AI code completion plugin for Visual Studio Code, like GitHub Copilot but 100% free and 100% private.
  - designed to work seamlessly with: Ollama
# agents-multi
- https://github.com/microsoft/autogen /31.4kStar/MIT/202410/python/jupyter
  - https://microsoft.github.io/autogen/
  - AutoGen is an open-source programming framework for building AI agents and facilitating cooperation among multiple agents to solve tasks.
  - It offers features such as agents capable of interacting with each other, facilitates the use of various large language models (LLMs) and tool use support, autonomous and human-in-the-loop workflows, and multi-agent conversation patterns.

- https://github.com/om-ai-lab/OmAgent /apache2/202407/python
  - OmAgent是一个多模态智能体系统，专注于利用多模态大语言模型能力以及其他多模态算法来做一些有趣的事
  - 包含一个专为解决多模态任务而设计的轻量级智能体框架omagent_core。我们利用这个框架搭建了超长复杂视频理解系统——OmAgent，当然你可以利用它实现你的任何想法。
  - DnCLoop: 受到经典算法思想Divide and Conquer启发，我们设计了一个递归的通用任务处理逻辑，它将复杂的问题不断细化形成任务树，并最终使复杂任务变成一组可解得简单任务。
# agent-open
- https://github.com/AIDC-AI/Pixelle-MCP /271Star/MIT/202508/python
  - https://pixelle.ai/
  - Open-Source Multimodal AIGC Solution based on ComfyUI + MCP + LLM
  - An AIGC solution based on the MCP protocol, seamlessly converting ComfyUI workflows into MCP tools
  - Server-side is built on ComfyUI, inheriting all capabilities from the open ComfyUI ecosystem

- https://github.com/modelcontextprotocol/servers /MIT/202411/python
  - https://modelcontextprotocol.io/
  - A collection of reference implementations and community-contributed servers for the Model Context Protocol (MCP). This repository showcases the versatility and extensibility of MCP, demonstrating how it can be used to give Large Language Models (LLMs) secure, controlled access to tools and data sources.
  - Each MCP server is implemented with either the Typescript MCP SDK or Python MCP SDK.
  - https://x.com/alexalbert__/status/1861464485011300839
    - The future of MCP is truly going to be community-led and not controlled by any single entity.
    - Here are some of the highlights I'm seeing from across the industry:
    - Replit is looking into adding MCP support to Agents
    - Sourcegraph has already added MCP to Cody and you can go try it out right now!
    - Zed has added MCP support in their editor, also available to try out!
    - Github Copilot is working with MCP
    - Codeium is using MCP to improve Windsurf's capabilities
  - https://x.com/alexalbert__/status/1861453744216453309
    - we do have a few clients beside Claude desktop that have already integrated MCP in production (Zed, Sourcegraph, etc).

- https://github.com/QwenLM/Qwen-Agent /tongyi/202411/python
  - https://pypi.org/project/qwen-agent/
  - Agent framework and applications built upon Qwen>=2.0, featuring Function Calling, Code Interpreter, RAG, and Chrome extension
  - 基于Qwen2.0的agent框架：Qwen-Agent，它有指令遵循、工具使用、做规划和记忆能力
  - 基于Qwen-Agent的一个Chrome浏览器扩展，一个智能浏览器助手：BrowserQwen, 它可以基于当前页面或文档跟你对话、能记住你浏览过的内容进行总结、可以解决数学问题、数据图表可视化
# llama.cpp
- https://github.com/yazon/flexllama /BSD/202510/python
  - Lightweight self-hosted tool for running multiple llama.cpp server instances with OpenAI v1 API compatibility and multi-GPU support

- https://github.com/xorbitsai/xllamacpp /MIT/202511/python/fork
  - a Python wrapper of llama.cpp
  - This project forks from cyllama and provides a Python wrapper for @ggerganov's llama.cpp which is likely the most active open-source compiled LLM inference engine.
  - https://github.com/xorbitsai/inference /apache2/202511/python
    - Xinference gives you the freedom to use any LLM you need.
    - Xllamacpp: New llama.cpp Python binding, maintained by Xinference team, supports continuous batching and is more production-ready
    - Support MLX backend for Apple Silicon chips

- https://github.com/airnsk/proxycache /202511/python
  - Smart OpenAI‑compatible proxy for llama.cpp: manages slots, saves/restores KV cache to disk, routes requests by prefix similarity
  - [Faster Prompt Processing in llama.cpp: Smart Proxy + Slots + Restore : r/LocalLLaMA _202511](https://www.reddit.com/r/LocalLLaMA/comments/1ostdcn/faster_prompt_processing_in_llamacpp_smart_proxy/)
    - This service is a smart proxy in front of llama.cpp that makes long‑context chat and IDE workflows much faster by managing llama.cpp slots, reusing cached context, and restoring saved caches from disk when needed.
    - llama.cpp provides “slots,” each holding a conversation’s KV cache so repeated requests with the same or very similar prefix can skip recomputing the whole prompt and continue from the first mismatching token, which dramatically cuts latency for large prompts. In real teams the number of users can easily exceed the number of available slots (e.g., 20 developers but only 4 slots), so naive routing causes random slot reuse and cache overwrites that waste time and GPU/CPU cycles. This proxy solves that by steering requests to the right slot, saving evicted caches to disk, and restoring them on demand, so long prompts don’t need to be recomputed from scratch each time.

- https://github.com/GeeeekExplorer/nano-vllm /MIT/202511/python
  - A lightweight vLLM implementation built from scratch.
  - Clean implementation in ~ 1, 200 lines of Python code
  - Fast offline inference - Comparable inference speeds to vLLM
  - Optimization Suite - Prefix caching, Tensor Parallelism, Torch compilation, CUDA graph, etc.

- https://github.com/lemonade-sdk/lemonade /1.6kStar/apache2/202511/python/cpp
  - https://lemonade-server.ai/
  - Lemonade helps users run local LLMs with the highest performance by configuring state-of-the-art inference engines for their NPUs and GPUs.
  - Lemonade supports both GGUF and ONNX models. You can also import custom GGUF and ONNX models from Hugging Face by using our Model Manager (requires server to be running).

## llama-rewrite

- https://github.com/projektjoe/gpt-oss /MIT/202511/python/cpp
  - From-scratch implementation of OpenAI's GPT-OSS model in Python. No Torch, No GPUs.
  - [GPTOSS: From-Scratch Implementation _202511](https://www.projektjoe.com/blog/gptoss)
    - We will rely completely on the CPU, so no need for special hardware here.
  - [I implemented GPT-OSS from scratch in pure Python, without PyTorch or a GPU : r/LLMDevs _202511](https://www.reddit.com/r/LLMDevs/comments/1ookn7f/i_implemented_gptoss_from_scratch_in_pure_python/)
  - [I implemented GPT-OSS from scratch in pure Python, without PyTorch or a GPU : r/LocalLLaMA](https://www.reddit.com/r/LocalLLaMA/comments/1oogvcw/i_implemented_gptoss_from_scratch_in_pure_python/)

- https://github.com/naklecha/llama3-from-scratch /MIT/202405/jupyter/inactive
  - llama3 implementation one matrix multiplication at a time

- https://github.com/karpathy/minGPT /MIT/202207/python/inactive
  - A minimal PyTorch re-implementation of the OpenAI GPT (Generative Pretrained Transformer) training
# ollama/lmstudio-like
- https://github.com/menloresearch/jan /37.5kStar/agpl > apache2/202508/ts/rust/tauri
  - https://jan.ai/
  - an AI assistant that can run 100% offline on your device
  - Local AI Models: Download and run LLMs (Llama, Gemma, Qwen, etc.) from HuggingFace
  - Cloud Integration: Connect to OpenAI, Anthropic, Mistral, Groq, and others
  - MCP integration for enhanced capabilities
  - 提供了类似lm studio的模型下载简化版
  - [chore: Jan's code is now under the Apache license _202505](https://github.com/menloresearch/jan/pull/5042)
    - release/v0.5.18

- https://github.com/oobabooga/text-generation-webui /45.1kStar/AGPLv3/202509/python/js
  - https://oobabooga.gumroad.com/l/deep_reason
  - A Gradio web UI for Large Language Models.
  - The definitive Web UI for local AI, with powerful features and easy setup.
  - Supports multiple local text generation backends, including llama.cpp, Transformers, ExLlamaV3, ExLlamaV2, and TensorRT-LLM (the latter via its own Dockerfile).
  - Easy setup: Choose between portable builds (zero setup, just unzip and run) for GGUF models on Windows/Linux/macOS, or the one-click installer that creates a self-contained installer_files directory.
  - 100% offline and private, with zero telemetry, external resources, or remote update requests.
  - File attachments: Upload text files, PDF documents, and .docx documents to talk about their contents.
  - Vision (multimodal models): Attach images to messages for visual understanding
  - Web search: Optionally search the internet with LLM-generated queries to add context to the conversation.
  - https://github.com/oobabooga/text-generation-webui-extensions
    - ad_discordbot (altoiddealer's discordbot)
    - Diffusion_TTS

- https://github.com/withcatai/catai /477Star/MIT/202406/ts/svelte/api+webapp/inactive
  - https://withcatai.github.io/catai/
  - Run AI assistant locally! with simple API for Node.js
  - Run GGUF models on your computer with a chat ui.
  - Inspired by Node-Llama-Cpp, Llama.cpp
  - Real time text streaming 
  - Fast model downloads
  - There is also a simple API that you can use to ask the model questions.

- https://github.com/EmreMutlu99/Ollama-Agent-Kit /202510/ts
  - https://emc-ltd.co/software-consultancy/
  - open-source Node.js toolkit for building memory-enabled AI agents powered by Ollama. 
  - It supports conversation threads, lightweight JSONL memory, and tool calls (e.g., weather, time, reservations), making it easy to integrate LLM agents into your own projects.

- https://github.com/cztomsik/ava /458Star/MIT/202508/zig/ts
  - https://avapls.com/
  - Ava is an open-source desktop application for running language models locally on your computer. 
  - It's batteries-included GUI for llama.cpp
  - Zig, C++ (llama.cpp), SQLite, Preact, Preact Signals, Twind

- https://github.com/felladrin/MiniSearch /480Star/apache2/202510/ts
  - https://felladrin-minisearch.hf.space/
  - A minimalist web-searching app with an AI assistant that runs directly from your browser.
  - Cross-platform: Models run inside the browser, both on desktop and mobile
  - Efficient: Models are loaded and cached only when needed
  - Customizable: Tweakable settings for search results and text generation
  - Can I use custom models via OpenAI-Compatible API?
    - Yes! For this, open the Menu and change the "AI Processing Location" to Remote server (API). Then configure the Base URL, and optionally set an API Key and a Model to use.
  - It's a docker-based web app built upon SearXNG.
  - https://github.com/searxng/searxng /AGPL/202510/python
    - https://docs.searxng.org/
    - SearXNG is a free internet metasearch engine which aggregates results from various search services and databases. Users are neither tracked nor profiled.

- https://github.com/pamelafox/ollama-python-playground /jupyter
  - A dev container with ollama and ollama examples with the Python OpenAI SDK
  - This project is designed to be opened in GitHub Codespaces as an easy way for anyone to try out SLMs (small language models) entirely in the browser.
  - https://x.com/pamelafox/status/1801678164969853034
    - To make it super easy for anyone to try out Ollama (esp teachers/students)
    - I've included an example notebook that walks through completions, prompt eng, few-shots, and RAG
# webgpu-ai
- https://huggingface.co/spaces/ibm-granite/Granite-4.0-Nano-WebGPU/tree/main /202510/ts
  - the demo uses Transformers.js to run the models 100% locally in your browser with WebGPU acceleration.
  - [Granite 4.0 Nano: Just how small can you go? _202510](https://huggingface.co/blog/ibm-granite/granite-4-nano)
  - [IBM releases Granite-4.0 Nano (300M & 1B), along with a local browser demo showing how the models can programmatically interact with websites and call tools/browser APIs on your behalf. : r/LocalLLaMA](https://www.reddit.com/r/LocalLLaMA/comments/1oifmg6/ibm_releases_granite40_nano_300m_1b_along_with_a/)
    - What will be interesting is how they handle permissioning, if the model can open URLS or trigger browser calls, sandboxing becomes key. 
    - `llama.cpp` has webasm support so they probably compiled it to webasm binary and run it via javascript.
# ml-neural-network
- https://github.com/AlloyTeam/netural
  - JavaScript的前向神经网络和反向传播的实现。

- https://github.com/TrevorBlythe/MentisJS
  - A javascript neural network library. 
  - It can train with backpropagation or neural evolution! 
  - [A better alternative to convnetjs](https://github.com/karpathy/convnetjs/issues/122)
    - This library has Deconv layers and other new features that not even convnetjs has.
    - It also doesn't require you to put your data in a custom data type.

- https://github.com/mlc-ai/web-llm
  - Introducing WebLLM, an open-source chatbot that brings language models (LLMs) directly onto web browsers. 
  - We can now run instruction fine-tuned LLaMA (Vicuna) models natively on your browser tab via @WebGPU with no server support.

- https://github.com/photopea/UNN.js
  - Deep Learning in Javascript. Alternative to ConvNetJS, that is 4x faster.
  - [A 4x faster alternative to ConvNetJS](https://github.com/karpathy/convnetjs/issues/115)
    - It has capabilities similar to ConvNetJS, but both training and testing are 4x faster (while still running in a single JS thread on the CPU).

- https://github.com/mil-tokyo/webdnn
  - The Fastest DNN Running Framework on Web Browser

- https://github.com/karpathy/convnetjs
  - Deep Learning in Javascript. Train Convolutional Neural Networks (or ordinary ones) in your browser.
  - [[Question] Why use javascript ?](https://github.com/karpathy/convnetjs/issues/72)
    - Performance-wise there is no reason to believe that JavaScript would perform significantly slower than Python. The reason why Python is used over C++ is not performance, it is the ecosystem.
    - For fast execution Python or C++ might not even be the best for neural networks as GPGPU computing could be the ultimate solution for fast parallel computing of lots of artificial neurons. In that case JavaScript would yield roughly the same performances as Python of C++.

- https://github.com/BrainJS/brain.js
  - robot GPU accelerated Neural networks in JavaScript for Browsers and Node.js
# ml-dl
- https://github.com/visheratin/web-ai /MIT/ts
  - run modern deep learning models directly in the web browser or in Node.js
  - Powered by ONNX runtime. Web AI runs the models using ONNX Runtime, which has rich support for of all kinds of operators.
  - Web worker support. All heavy operations - model creation and inference - are offloaded to a separate thread so the UI does not freeze.

- https://github.com/xenova/transformers.js /js
  - https://huggingface.co/docs/transformers.js
  - State-of-the-art Machine Learning for the web. 
  - Run Transformers directly in your browser, with no need for a server!
  - Transformers.js is designed to be functionally equivalent to Hugging Face's transformers python library
  - Transformers.js uses ONNX Runtime to run models in the browser. The best part about it, is that you can easily convert your pretrained PyTorch, TensorFlow, or JAX models to ONNX using Optimum.

- https://github.com/ml5js/ml5-library /js
  - provides access to machine learning algorithms and models in the browser, building on top of TensorFlow.js

- https://github.com/alibaba/pipcook /ts
  - https://alibaba.github.io/pipcook/
  - provides subprojects including machine learning pipeline framework, management tools, a JavaScript runtime for machine learning, and these can be also used as building blocks in conjunction with other projects.
  - provides access to Python packages by bridging the interface of `CPython` using N-API. so pytorch/tensorflow/scikit is available

- https://github.com/mljs/ml /js
  - Machine learning tools in JavaScript
# audio
- https://github.com/myshell-ai/OpenVoice /MIT/202407/python
  - https://research.myshell.ai/open-voice
  - Instant voice cloning by MyShell
  - Free Commercial Use. Starting from April 2024, both V2 and V1 are released under MIT License. 
  - OpenVoice has been powering the instant voice cloning capability of myshell.ai since May 2023. 
  - 即时语音克隆工具，只需从参考资料中截取一段简短的音频即可实现克隆。可详细控制语音风格，包括情感、口音、节奏、停顿和语调。生成多种语言的语音。
# rag-examples
- https://github.com/datawhalechina/all-in-rag /202511/python
  - https://datawhalechina.github.io/all-in-rag/
  - 大模型应用开发实战一：RAG 技术全栈指南，在线阅读
  - https://github.com/yksanjo/all-in-rag
# rag-utils
- https://github.com/rag-web-ui/rag-web-ui /apache2/202502/python/ts
  - RAG Web UI is an intelligent dialogue system based on RAG
# rag-fwk
- https://github.com/infiniflow/ragflow /68.2kStar/apache2/202511/python/ts/华人团队
  - https://ragflow.io/
  - https://demo.ragflow.io/
  - open-source RAG (Retrieval-Augmented Generation) engine based on deep document understanding
  - Template-based chunking: Plenty of template options to choose from
  - Grounded citations with reduced hallucinations
  - Supports Word, slides, excel, txt, images, scanned copies, structured data, web pages, and more.
  - Multiple recall paired with fused re-ranking.
  - 依赖 Crawl4AI、elasticsearch、flask-login、minio、pandas、voyageai、pyobvector
  - 未使用langchain/aisdk, 多model-provider的集成完全自定义实现
  - Prerequisites: RAM >= 16 GB
    - gVisor: Required only if you intend to use the code executor (sandbox) feature of RAGFlow.
  - ✨ 实测, rag后的chunk文本可查看chunk与原文对应的细节
    - 聊天的回答中, hover图标能显示引文，并可点击引文后可在页面遮罩侧面弹窗中查看pdf原文位置
  - 🐛 整个 知识库/聊天/查询 的创建及使用交互过于复杂， 不够简洁和自然
  - DeepDoc (Default) - RAGFlowPdfParser
    - Full OCR, Most comprehensive but slower
    - Stream Reading Capability: ✅ YES
    - Page-by-page processing with configurable page_from/page_to
    - Uses `pdfplumber.open()` with `page_from` and `page_to` parameters
    - 使用pdfplumber.open()和pypdf.PdfReader(), 一次性加载整个PDF文件到内存
  - Plain Text Parser - PlainParser
    - Uses `pypdf` for text extraction only
    - Only for text-based PDFs
    - Stream Reading Capability: ✅ YES
    - Uses `pypdf.PdfReader` with page ranges
    - Memory Usage: Very low - only text content loaded
    - 可以逐页处理，但仍需要加载完整PDF
  - Docling Parser - DoclingParser
    -  Uses `docling.DocumentConverter` with full file
  - MinerU Parser - MinerUParser
    - External tool, entire file processing
  - TCADP Parser - TCADPParser
    - Tencent Cloud API integration
    - Cloud-based, file upload to Tencent Cloud
    - Reading Method: Converts entire file to `base64` and uploads, entire file loaded into memory for Base64 conversion
  - Vision Parser - VisionParser
    - Visual model processing, full file
    - Higher memory requirements
    - Uses `pdfplumber` with full file access
  - [HARD -- Efficient way to use enterprise dataset without uploading all files? _202509](https://github.com/orgs/infiniflow/discussions/10388)
    - You have to upload the data from Azure to RAGFlow. And currently you can do that through API. From 0.22 which is going to be launched in this Nov, we will provide some data sources and you can ingest data by just click several buttons. And more data sources could be easily added.
  - [[Question]: Why can't knowledge graphs be used? _202509](https://github.com/infiniflow/ragflow/issues/10017)
    - Knowledge graphs can’t currently be used with the Table chunking method in RAGFlow. The reason is that table chunking treats each row as a separate chunk and stores field mappings for retrieval, but it does not run those chunks through the knowledge graph extraction pipeline. As a result, entity–relationship extraction is skipped for tables.
    - If you need a knowledge graph from table data, you’d have to implement a custom post-processing step (e.g., parsing the rows yourself and generating triples).
  - [Select PDF parser | RAGFlow](https://ragflow.io/docs/dev/select_pdf_parser)
  - [Deploy local models | RAGFlow](https://ragflow.io/docs/dev/deploy_local_llm)
    - RAGFlow supports deploying models locally using Ollama, Xinference, IPEX-LLM, or jina.
  - 🐛 [[Bug]: Fail to access model(text-embedding-bge-reranker-v2-m3). The LmStudioRerank has not been implement _202502](https://github.com/infiniflow/ragflow/issues/5354)
    - Unable to add reranker model for LM STUDIO，Fail to access model(text-embedding-bge-reranker-v2-m3).The LmStudioRerank has not been implement
  - 🐛 [[Question]: Support for calling the OLLAMA Reranker models ？ _202509](https://github.com/infiniflow/ragflow/issues/8988)
    - Ollama supports very few rerank models and is not recommended.
  - [FAQs | RAGFlow](https://ragflow.io/docs/dev/faq)
    - RAGFlow supports MinerU (>= 2.6.3) as an optional PDF parser with multiple backends. RAGFlow acts only as a client for MinerU, calling it to parse documents, reading the output files, and ingesting the parsed content.

- https://github.com/chunkhound/chunkhound /118Star/MIT/202509/python
  - https://chunkhound.github.io/
  - Deep Research for Code & Files
  - Transform your codebase into a searchable knowledge base for AI assistants using semantic search via cAST algorithm and regex search. 
  - Integrates with AI assistants via the Model Context Protocol (MCP).
  - cAST Algorithm - Research-backed semantic code chunking
  - Multi-Hop Semantic Search - Discovers interconnected code relationships beyond direct matches
  - Semantic search - Natural language queries like "find authentication code"
  - Regex search - Pattern matching without API keys
  - Local-first - Your code stays on your machine
  - 22 languages with structured parsing, via Tree-sitter

- https://github.com/HKUDS/LightRAG /20.1kStar/MIT/202508/python
  - Simple and Fast Retrieval-Augmented Generation
  - [2025.06.16]🎯 Our team has released RAG-Anything an All-in-One Multimodal RAG System for seamless text, image, table, and equation processing.
  - https://github.com/HKUDS/RAG-Anything /MIT/202508/python
    - All-in-One Multimodal Document Processing RAG system built on LightRAG.

- https://github.com/memfreeme/memfree /MIT/202409/ts
  - https://www.memfree.me/
  - MemFree is a Hybrid AI Search Engine.
  - Search and ask questions with text, images, files, and web pages.
  - Multi AI Models: ChatGPT, Claude, Gemini
  - 支持多模态（图片、文字、文件），多来源（Twitter、学术、本地知识库），多种表现形式（思维导图、图片音视频）等混合搜索形态

- https://github.com/KruxAI/ragbuilder /apache2/202410/python
  - https://docs.ragbuilder.io/
  - A toolkit to create optimal Production-readyRetrieval Augmented Generation(RAG) setup for your data
  - By performing hyperparameter tuning on various RAG parameters (Eg: chunking strategy: semantic, character etc., chunk size: 1000, 2000 etc.), RagBuilder evaluates these configurations against a test dataset to identify the best-performing setup for your data.

- https://github.com/llmware-ai/llmware /14.5kStar/apache2/202507/python/inactive
  - https://llmware-ai.github.io/llmware/
  - a unified framework for building LLM-based applications (e.g., RAG, Agents), using small, specialized models that can be deployed privately
  - llmware has two main components:
    - RAG Pipeline - integrated components for the full lifecycle of connecting knowledge sources to ai models
    - 50+ small, specialized models fine-tuned for key tasks in enterprise process automation, including fact-based question-answering, classification, summarization, and extraction
  - RAG-Optimized Models - 1-7B parameter models designed for RAG workflow integration and running locally.
# rag-memory
- https://github.com/mem0ai/mem0 /apache2/202409/python
  - https://mem0.ai/
  - Mem0 (pronounced as "mem-zero") enhances AI assistants and agents with an intelligent memory layer, enabling personalized AI interactions. 
  - Mem0 remembers user preferences, adapts to individual needs, and continuously improves over time, making it ideal for customer support chatbots, AI assistants, and autonomous systems.
  - Multi-Level Memory: User, Session, and AI Agent memory retention
  - Mem0 leverages a hybrid database approach to manage and retrieve long-term memories for AI agents and assistants. 
    - Each memory is associated with a unique identifier, such as a user ID or agent ID, allowing Mem0 to organize and access memories specific to an individual or context.
    - 🛢️ When a message is added to the Mem0 using add() method, the system extracts relevant facts and preferences and stores it across data stores: a vector database, a key-value database, and a graph database. 
    - This hybrid approach ensures that different types of information are stored in the most efficient manner, making subsequent searches quick and effective.
    - Mem0 performs search across these data stores, retrieving relevant information from each source

- https://github.com/getzep/zep /apache2/202409/go
  - https://docs.getzep.com/
  - a long-term memory service for AI Assistant apps. 
  - With Zep, you can provide AI assistants with the ability to recall past conversations, no matter how distant, while also reducing hallucinations, latency, and cost.
  - Zep persists and recalls chat histories, and automatically generates summaries and other artifacts from these chat histories. 
  - Zep also provides a simple, easy to use abstraction for document vector search called Document Collections. This is designed to complement Zep's core memory features, but is not designed to be a general purpose vector database.
# ai-examples
- https://github.com/Zeyi-Lin/HivisionIDPhotos /apache2/202409/python
  - https://swanhub.co/ZeYiLin/HivisionIDPhotos/demo
  - 一个轻量级的AI证件照制作算法
  - 旨在开发一种实用、系统性的证件照智能制作算法, 利用一套完善的AI模型工作流程，实现对多种用户拍照场景的识别、抠图与证件照生成
  - SwanLab：训练人像抠图模型全程用它来分析和监控，以及和实验室同学协作交流，大幅提升了训练效率。
  - 支持 纯离线 或 端云 推理
# ai-devops/tooling
- https://github.com/Tencent/AI-Infra-Guard /MIT/202503/go
  - 腾讯开源了一个AI基础设施安全评估工具：AI-Infra-Guard，一键检测AI系统的潜在安全风险
  - 支持包括langchain、ollama、gradio、open-webui以及ComfyUI等在内的30种AI组件
  - 可以帮助识别，比如像Ollama在其docker中默认以root权限运行且开放到公网上，由于缺乏鉴权，可能会导致模型被删除/窃取/投毒或算力被窃取的风险
  - 这个工具的特点是轻量级，二进制文件8MB，内存占用低，支持跨平台运行，开箱即用

- https://github.com/exo-explore/exo /GPL
  - exo: Run your own AI cluster at home with everyday devices
  - exo supports different models including LLaMA (MLX and tinygrad), Mistral, LlaVA, Qwen, and Deepseek.
  - 该项目支持将现有设备统一到一个功能强大的GPU中，支持 iPhone，iPad，Android，Mac，Nvidia，树莓派等等几乎所有设备

- https://github.com/GhennadiiMir/ollama_server_manager /202510/ruby
  - A streamlined web interface for managing Ollama models across multiple servers. 
  - Perfect for teams running distributed Ollama instances or managing models on different machines.
  - Since I only use this on my private, trusted network, I kept it intentionally simple with no authentication required.
# more
