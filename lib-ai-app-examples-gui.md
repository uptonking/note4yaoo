---
title: lib-ai-app-examples-gui
tags: [ai, app, examples, large-language-model, ollama]
created: 2026-04-06T22:41:46.252Z
modified: 2026-04-06T22:42:11.263Z
---

# lib-ai-app-examples-gui

# guide

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

- https://github.com/menloresearch/jan /39.7kStar/agpl > apache2/202512/ts/rust/tauri
  - https://github.com/janhq/jan
  - https://jan.ai/
  - an AI assistant that can run 100% offline on your device
  - Local AI Models: Download and run LLMs (Llama, Gemma, Qwen, etc.) from HuggingFace
  - Cloud Integration: Connect to OpenAI, Anthropic, Mistral, Groq, and others
  - MCP integration for enhanced capabilities
  - 提供了类似lm studio的模型下载简化版
  - [chore: Jan's code is now under the Apache license _202505](https://github.com/menloresearch/jan/pull/5042)
    - release/v0.5.18
  - this project is a llm chat app built with tauri. it supports using external llm api like openai/mistral api, as well as running local .gguf models and mlx models to provide api. 
  - please analyze the project architecture and related code. explain the core architecture and data flow for the extensible architecture to support local models in different formats. write your result to dev-arch-gguf-mlx.md. 
  - there are different approaches to run local models. is it possible to write a extensible module to make the logic of running swift mlx server swappable. i want to use python mlx-server implementation to replace the swift implementation.

- https://github.com/AtomicBot-ai/Atomic-Chat /apache2/202603/ts/rust/tauri
  - https://atomic.chat/
  - Open-source ChatGPT alternative. Run local LLMs or connect cloud models — with full control and privacy.
  - Llama.cpp
  - ❓ a fork of janai
  - [Google TurboQuant running Qwen Locally on MacAir : r/LocalLLaMA _202603](https://www.reddit.com/r/LocalLLaMA/comments/1s5kdu0/google_turboquant_running_qwen_locally_on_macair/)
    - We patched llama.cpp with Google’s new TurboQuant compression method and then ran Qwen 3.5–9B on a regular MacBook Air (M4, 16 GB) with 20000 tokens context.
  - Compression is only for context or also the model?
    - context only
  - Model compression already exists, it's called quantization (the q4, q8, etc that we generally run on our local systems).
  - TurboQuant essentially takes that idea and applies it to context (data that constantly changes, unlike the model weights that are all already there, also known as the kv cache).
  - The KV context quantization also already existed before TurboQuant. You can set up llamacpp using -ctk or -ctv q8_0, q5_0, q4_0, etc. 
  - TurboQuant is an optimization of what llama.cpp KV cache quantization does. Llama.cpp KV cache uses a block based quantization, meaning each block of values requires storing a full-precision scale constant to restore the approximate original value. This scale constant was an overhead because of which the compression was not as efficient. TurboQuant uses a polar quant method which stores data in angles instead of coordinates (which is a technique already used in model weights quantization by, for example, GGUF format), essentially removing the need of those scale constants to be stored. It also implements some kind of 1-bit error correction step
  - [Google TurboQuant running Qwen Locally on MacAir : r/LocalLLM _202603](https://www.reddit.com/r/LocalLLM/comments/1s5k9n7/google_turboquant_running_qwen_locally_on_macair/)

- https://github.com/badboysm890/ClaraVerse /3.8kStar/MIT > AGPL/202603/go/ts
  - https://claraverse.space/
  - Privacy-first, fully local AI workspace with Ollama LLM chat, tool calling, agent builder, Stable Diffusion, and embedded n8n-style automation. 
  - No backend. No API keys. Just your stack, your machine.
  - The Story Behind ClaraVerse: Why can't everything be in a single app?
  - The Solution: One App. Six Tools. Zero Compromises.
  - Built on the shoulders of giants: llama.cpp • llama-swap • faster-whisper • ComfyUI • N8N
  - 🍴 forks
  - https://github.com/vanvuongngo/ClaraN /MIT/202508/ts/inactive
    - This is a hardfork of ClaraVerse
    - Tauri for building Desktop- and Mobile apps 
    - Qwik web framework for building performant Web UIs
    - DaisyUI for faster, cleaner and simple tailwind CSS UI development
# ollama/lmstudio-like
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

- https://github.com/nicklansley/OllamaImageGenerator
  - web-based image generator using Ollama
  - a simple proxy server for the Ollama Image Generator, which serves an HTML interface and forwards API requests to the Ollama API. 
  - The purpose of this is to overcome the CORS policy of many browsers which prevents direct access to the Ollama API from a local HTML file
  - The server listens on port 8080 and forwards requests to the Ollama API located at http://localhost:11434/api/generate.
  - The server acts as a proxy, forwarding requests from the HTML interface to the Ollama API and returning the generated images to the HTML interface in 'stream' format so that the progress of the image generation is displayed as it is being generated.
  - [Ollama Image Generator : r/ollama _202601](https://www.reddit.com/r/ollama/comments/1qkokhv/ollama_image_generator/)

- https://github.com/Kieirra/murmure /AGPL/202602/rust/ts
  - Fully local, private and cross platform Speech-to-Text with LLM Post-processing
  - [Murmure 1.7.0 - A local voice interface for Ollama : r/ollama](https://www.reddit.com/r/ollama/comments/1r3abol/murmure_170_a_local_voice_interface_for_ollama/)

- https://github.com/Laszlobeer/Ollama-Vision-Memory-Desktop /MIT/202602/python
  - Local AI Desktop Assistant with a focus on long-term memory, computer vision, and customizable behavior.
  - [Ollama-Vision-Memory-Desktop — Local AI Desktop Assistant with Vision + Memory! : r/ollama](https://www.reddit.com/r/ollama/comments/1rfffru/ollamavisionmemorydesktop_local_ai_desktop/)

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
# examples
- https://github.com/Peuqui/AIfred-Intelligence /NC/202604/python
  - https://peuqui.github.io/AIfred-Intelligence/
  - Multi-Agent AI Assistant with TTS, RAG, Web Research & Voice capabilities. 
  - Supports Ollama, vLLM, TabbyAPI.
  - Features AIfred/Sokrates/Salomo debate system.
  - fully-featured AI assistant running locally on your own hardware. It autonomously manages emails, appointments, documents and databases — with function calling, persistent memory and multi-agent debates. No cloud dependency, full data sovereignty.
# more
