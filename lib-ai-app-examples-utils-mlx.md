---
title: lib-ai-app-examples-utils-mlx
tags: [ai, large-language-model, machine-learning, macos, mlx]
created: 2025-11-01T10:54:01.772Z
modified: 2025-11-01T10:54:26.044Z
---

# lib-ai-app-examples-utils-mlx

# guide

- tips
  - 不必执着于lmstudio的替代, 采用client/server架构后, 普通后端都可以支持定制前端
# dev-xp
- mlx-4bit 模型通常比 gguf-Q4_K_XL 速度快，但质量更差
- mlx模型的fixes/updates通常无人维护, 连lmstudio社区的模型都很少维护， 远不如gguf

- 
- 
- 
- 
- 

# popular
- https://github.com/ml-explore/mlx-lm /2.7kStar/MIT/202511/python
  - a Python package for generating text and fine-tuning large language models on Apple silicon with MLX.
  - Integration with the Hugging Face Hub to easily use thousands of LLMs with a single command.
  - Low-rank and full model fine-tuning with support for quantized models.
  - Distributed inference and fine-tuning with mx.distributed
  - [MLX Community Projects · ml-explore/mlx _202402](https://github.com/ml-explore/mlx/discussions/654)
  - https://github.com/ml-explore/mlx-lm/blob/main/mlx_lm/SERVER.md
    - use mlx-lm to make an HTTP API for generating text with any supported model. 
    - The HTTP API is intended to be similar to the OpenAI chat API.
    - not recommended for production as it only implements basic security checks.
    - SSE
    - LoRA Adapters
    - LRU prompt cache with trie-based prefix matching
    - 🐛 
      - 只支持text, 不支持vlm
      - Python's built-in ThreadingHTTPServer (threading-based)
      - single model per server
      - single queue

- https://github.com/Blaizzy/mlx-vlm /1.8kStar/MIT/202511/python
  - a package for inference and fine-tuning of Vision Language Models (VLMs) and Omni Models (VLMs with audio and video support) on your Mac using MLX
  - https://github.com/avbiswas/mlx-vlm-batch-outlines /MIT/202604/python
    - Minimalist repo to do mlx vlm constrained decoding in batch mode
    - a small Qwen-focused MLX vision-language package for: multimodal chat with images; batched multimodal chat; structured outputs from Pydantic, regex, CFG, or JSON Schema
    - It is intentionally narrow. It is built for local MLX/Qwen workflows and does not try to support every mlx-vlm backend or the full Outlines API surface.
    - This project heavily reuses and adapts ideas and code paths from: mlx-vlm, outlines
    - https://x.com/neural_avb/status/2042908404390437000
      - I have been using local VLMs for annotating videos and images locally and producing synthetic datasets on my mac.
      - You can point to a folder full of images and get structured outputs 2-3x faster. Fully local.

- https://github.com/jundot/omlx /6.4kStar/apache2/202603/python
  - https://omlx.ai/
  - https://omlx.ai/benchmarks
  - LLM inference server with continuous batching & SSD caching for Apple Silicon — managed from the macOS menu bar
  - Continuous batching and tiered KV caching, managed directly from your menu bar.
  - The server discovers LLMs, VLMs, embedding models, and rerankers from subdirectories automatically.
    - Point `--model-dir` at a directory containing MLX-format model subdirectories.
    - Models are auto-detected by type: llm/vlm/ocr
  - Supports text LLMs, vision-language models (VLM), OCR models, embeddings, and rerankers on Apple Silicon.
  - oMLX provides both OpenAI-compatible (/v1/chat/completions) and Anthropic-compatible (/v1/messages) API endpoints.
  - Web UI at /admin for real-time monitoring, model management, chat, benchmark, and per-model settings.
    - Search and download MLX models from HuggingFace directly in the admin dashboard.
  - Multi-Model Serving: Load LLMs, VLMs, embedding models, and rerankers within the same server
  - macOS Menubar App: Native PyObjC menubar app (not Electron). 
  - FastAPI Server (OpenAI / Anthropic API): CLI Server
  - 🆚 How is oMLX different from Ollama or LM Studio?
    - Ollama and LM Studio cache the KV state in memory, but when the context shifts mid-session — which happens constantly with coding agents — the entire cache gets invalidated and recomputed from scratch. oMLX persists every KV cache block to SSD, so previously cached portions are always recoverable. TTFT drops from 30–90 seconds to under 5 seconds on long contexts.
  - 📡 
    - [Is there a way to use the huggingface cache? _202603](https://github.com/jundot/omlx/discussions/211)
  - [Unable to find the gguf model  _202603](https://github.com/jundot/omlx/issues/180)
    - oMLX uses mlx-lm as its backend, so GGUF models are not supported. 
  - [I input LM Studio's downloaded models dir doesn't work _202603](https://github.com/jundot/omlx/issues/149)
    - you need to set the parent directory instead of the model directory itself, and it will discover all models inside. @TipKnuckle has also submitted a PR to make it work when pointing directly to a model directory, so i'll review and merge that soon!
  - [Built oMLX.ai/benchmarks - One place to compare Apple Silicon inference across chips and models : r/LocalLLM _202603](https://www.reddit.com/r/LocalLLM/comments/1ro646t/built_omlxaibenchmarks_one_place_to_compare_apple/)

- https://github.com/RamboRogers/mlx-gui /GPL/202601/python/tkinter
  - https://mlxgui.com/
  - A lightweight Inference Server for Apple's MLX engine with a GUI.
  - TLDR - OpenRouter-style v1 API interface for MLX with Ollama-like model management, featuring auto-queuing, on-demand model loading, and multi-user serving capabilities via single mac app.

- https://github.com/cubist38/mlx-openai-server /MIT/202601/python
  - A high-performance API server that provides OpenAI-compatible endpoints for MLX models. 
  - Developed using Python and powered by the FastAPI framework, it provides an efficient, scalable, and user-friendly solution for running MLX-based vision and language models locally with an OpenAI-compatible interface.
  - Multimodal model support with vision, audio, and text
    - Text, Multimodal, Image Gen/Edit, Embeddings, Whisper
  - Easy Python and CLI usage
  - LoRA adapter support for fine-tuned image generation and editing
  - 支持multiple models, 通过yaml config
    - Multi-process (spawn) per model
    - Process isolation via HandlerProcessProxy 
    - InferenceWorker pattern (dedicated thread per handler)
  - 支持Structured Outputs: JSON schema via outlines
  - Queue: 3-level, per-model config
  - SSE
  - LoRA Adapters
  - Extensive parser/converter system
  - use `mlx-lm` as its core text generation engine
  - mlx-vlm for vlm
  - mflux for image gen
  - mlx-embeddings for embedding
  - mlx-whisper for audio
  - mlx-openai-server can be used as a library
    - You can import and use the async functions directly: from app.main import start, start_multi
    - You can also use the handlers directly without the web server: from app.schemas.openai import ChatCompletionRequest
    - Or use the model wrappers directly (lowest level): model = MLX_LM(model_path="mlx-community/Mistral-7B-Instruct-v0.3-4bit")
  - 需要手动配置模型的 model_type, 之后 The server uses `model_type` parameter to determine which handler (and underlying library) to use
    - routing is explicit and configuration-driven
    - a simple factory pattern based on the model_type string
  - https://github.com/arcee-ai/fastmlx /apache2/202503/python/inactive
    - production ready API to host MLX models.

- https://github.com/madroidmaq/mlx-omni-server /638Star/MIT/202512/python
  - MLX Omni Server provides dual API compatibility with both OpenAI and Anthropic APIs, enabling seamless local inference on Apple Silicon using the MLX framework.
  - [Best setup for running a production-grade LLM server on Mac Studio (M3 Ultra, 512GB RAM)? : r/LocalLLM](https://www.reddit.com/r/LocalLLM/comments/1p7ei31/best_setup_for_running_a_productiongrade_llm/)
    - MLX Omni server is far from production ready. It’s heavily vibe coded and PRs never get merged. Tools parsing is unusable.
    - I don’t think llama.cpp supports MLX quants. It has metal acceleration, though. MLX-LM is what you need for that, and is what MLX-Omni-server uses. This is also what LM Studio uses.
    - Mac studios are great for single user research and applications, but not for low latency, high speed, or concurrency.
  - https://github.com/lucasventurasc/mlx-studio /MIT/202512/python/js
    - High-performance local LLM server for Apple Silicon with intelligent caching and multi-backend support
    - MLX Studio using MLX Omni Server as Backend with many cache improvements and tool calling for Claude Code CLI e Qwen-CLI with Qwen3 models
    - wraps `mlx-omni-server` with production-ready features: smart prompt caching (99%+ cache hit rates), on-demand model loading, Claude Code integration, and a web UI.
    - MLX Studio auto-downloads models on first use, or you can pre-download

- https://github.com/unslothai/unsloth /54.3kStar/apache2+AGPL/202603/python/ts
  - https://unsloth.ai/docs
  - Unified web UI for training and running open models like Qwen, DeepSeek, and Gemma locally.
  - Unsloth Studio lets you run and train models for text, audio, embedding, vision and more. 
  - Available on Windows, Linux and macOS.
  - Unsloth provides several key features for both inference and training
  - The `llama.cpp` library that lets users run and save models with Unsloth
  - Search + download + run models including GGUF, LoRA adapters, safetensors
  - Export models: Save or export models to GGUF, 16-bit safetensors and other formats.
  - Tool calling: Support for self-healing tool calling and web search
  - Code execution: lets LLMs run code, data and verify results so answers are more accurate.
    - Unsloth Studio allows LLMs to run code and programs in a sandbox so it can calculate, analyze data, test code, generate files, or verify an answer with actual computation.
  - Auto-tune inference parameters and customize chat templates.
  - Upload images, audio, PDFs, code, DOCX and more file types to chat with.
  - Supports full fine-tuning, pretraining, 4-bit, 16-bit and, FP8 training.
  - Observability: Monitor training live, track loss and GPU usage and customize graphs.
  - Multi-GPU training is supported, with major improvements coming soon.
  - 🐛
    - studio的backend和ui都是AGPL
    - mac is chat-only, When chat_only=true, model selector shows only Hub picker (no local/fine-tuned picker)
    - “Downloaded GGUF” list is from HF cache repos (/api/models/cached-gguf)
  - 🛝
    - In the current script, every unsloth studio setup on local machine does a full reset of the Studio env
    - rm -rf "$VENV_DIR" and rm -rf "$VENV_T5_DIR" at studio/setup.sh
    - it also deletes/rebuilds ~/.unsloth/llama.cpp each run at studio/setup.sh
    - rerunning setup is expensive. Practical workflow: run unsloth studio setup only when first installing, after major updates, or when deps break
    - Local .gguf (or directory containing .gguf) is auto-detected in studio/backend/utils/ models/model_config.py
  - [[Feature] MLX Support  _202602](https://github.com/unslothai/unsloth/issues/4061)
    - We're working on it as we speak. Will be released within 2 months I'd say
  - [Introducing Unsloth Studio  _202603](https://unsloth.ai/docs/new/studio)
    - open-source, no-code web UI for training, running and exporting open models in one unified local interface.
    - Powered by llama.cpp + Hugging Face, we support multi-GPU inference and most models.
    - Unsloth Studio runs 100% offline and locally.
    - Studio supports a range of supported transformers compatible model families, including text, multimodal models, text-to-speech, audio, embeddings, and BERT-style models.
    - https://x.com/UnslothAI/status/2033926272481718523
    - This is the right direction. The next bottleneck for most teams isn’t model speed anymore — it’s dataset + eval quality. We saw local fine-tuning cut iteration cost by ~60% in one workflow, but bad eval sets still gave misleading “wins.” Are you planning built-in eval templates/versioning so people can benchmark model changes more reliably?
  - ⚖️ Is Unsloth now licensed under AGPL-3.0?
    - No. The main Unsloth package is still licensed under Apache 2.0. Only certain optional components, such as the Unsloth Studio UI, are under the AGPL-3.0 open-source license.
    - Unsloth now has dual-licensing where some parts of the codebase are licensed Apache 2.0, while others are licensed AGPL-3.0. This structure helps support ongoing Unsloth development
  - [Unsloth Studio vs Llama.cpp vs LlamaFactory : r/unsloth _202603](https://www.reddit.com/r/unsloth/comments/1rx8tzi/unsloth_studio_vs_llamacpp_vs_llamafactory/)
    - I think everyone is misunderstanding the purpose of Unsloth Studio. It’s a UI for Unsloth. Unsloth is a popular framework for training, finetuning and RL for almost all model architectures. It isn’t designed to be your primary tool for inference. It’s meant to provide a UI and eventual API for model training and dataset creation.
    - Actually our chat feature is now highly sophiscated with toolcalling, code execution in python and bash. We intend to also support APIs very soon
  - [I'd be nice if Unsloth Studio was stand alone : r/unsloth _202603](https://www.reddit.com/r/unsloth/comments/1s5v6g9/id_be_nice_if_unsloth_studio_was_stand_alone/)
    - It's coming. It's already nearly finished. Will be out next month 

- https://github.com/llama-farm/llamafarm /760Star/apache2/202601/python/go/ts/electron
  - https://llamafarm.dev/
  - https://docs.llamafarm.dev/docs/intro
  - Deploy any AI model, agent, database, RAG, and pipeline locally or remotely in minutes
  - LlamaFarm brings enterprise AI capabilities to everyone. Run powerful language models, document processing, and intelligent retrieval—all locally on your hardware. No cloud required
  - Hardware Optimized — Automatic GPU/NPU acceleration on Apple Silicon, NVIDIA, and AMD
  - LlamaFarm focuses on inference rather than fine-tuning.
  - [Multi-Model Runtime Support with API and CLI Integration _202510](https://github.com/llama-farm/llamafarm/pull/263)
    - [Multi-Model architecture and implementation ](https://github.com/llama-farm/llamafarm/issues/202)
  - Choosing a Provider
    - Local models (Ollama)
    - Local models (Lemonade): Currently, Lemonade must be manually started. In the future, Lemonade will run as a container and be auto-started by the LlamaFarm server.
    - Self-hosted vLLM / OpenAI-compatible
    - Hosted APIs (OpenAI, Anthropic via proxy, Together, LM Studio)
  - The Universal Runtime is LlamaFarm's most versatile runtime provider, supporting any HuggingFace model through PyTorch Transformers and Diffusers.
  - 🛝
    - pc-app启动时会下载默认runtime
    - 支持下载huggingface的模型
  - 🍎 pr未合并且已关闭 [feat(runtime): initial mlx support _202512](https://github.com/llama-farm/llamafarm/pull/557)
  - [Support native docker models for local models _202510](https://github.com/llama-farm/llamafarm/issues/295)
    - Docker engine and compose comes with built in support for running local models similar to Ollama across osx, windows and linux, so it brings down the number of dependencies developers have to install.
    - 202601: For now, we're moving away from this direction given the way the LlamaFarm Universal Runtime works at present.
  - [We just launched the LlamaFarm Designer - build full AI systems visually, locally, and open-source : r/LlamaFarm _202511](https://www.reddit.com/r/LlamaFarm/comments/1onjyo6/we_just_launched_the_llamafarm_designer_build/)

- https://github.com/transformerlab/transformerlab-app /4.7kStar/AGPL/202601/python/ts/electron
  - https://lab.cloud/
  - 100% Open Source Toolkit for Large Language Models: Train, Tune, Chat on your own Machine
  - Use Different Inference Engines: mlx, vllm, llama.cpp, sglang, FastChat
    - 🌹 支持选择 local-engine, remote-engine
  - Support for Image Diffusion Models
  - Finetune / Train Across Different Hardware
  - win, linux, macos
  - Download any LLM, VLM, or Diffusion model from Huggingface
  - Chat with Models
  - RAG (Retreival Augmented Generation)
  - Convert Models Across Platforms: Convert from/to Huggingface, MLX, GGUF
  - 🔌 Plugin Support: loader, trainer, generator, eval, exporter
  - NVIDIA or AMD GPU on Linux (or Windows via WSL2)
  - 🛝
    - 插件功能强大，体验类似lmstudio
    - import model时选择的路径在windows的wsl环境下逻辑有问题, 在mac下只支持.workspace目录下的文件，导致需要拷贝
    - 模型RUN很慢，STOP停止困难
    - 需要chat template的模型(如qwen3-0.6b)无法配置template, 可以先用不需要template的模型如lfm测试
    - new chat有问题，只能聊一次，之后必须restart model才能再聊一次
    - 安装时，使用 miniforge3/conda 安装环境， 本地环境+workspace+1GB小模型总体占用空间为8GB左右
  - macOS with Apple Silicon is supported (training functionality varies by hardware)
  - CPU-only installs run inference but not GPU-heavy workflows
  - Transformer Lab consists of a React application "Frontend" that communicates with a Python API "Backend" (found in the api directory). Application data is stored in a file system workspace that is accessed by the API and third-party scripts using the SDK (which can be found in the lab-sdk directory).
  - 🐛 [Importing models from folder doesn't work on Windows _202408](https://github.com/transformerlab/transformerlab-app/issues/142)
    - The challenge is that Transformer Lab is architected as a frontend app running in your browser/Electron talking to an API running in WSL, and when you pop open the file explorer dialog it is passing a windows path to WSL.
    - There are a number of ways we might be able to fix this but we were hoping to solve in a way that allows the API to run on a remote machine. 
    - Perhaps the easiest short term fix is to just add the ability to copy and paste a path that the server can access into the modal.
    - Or if you are comfortable generating paths to your models relative to you WSL install, you can try directly importing your models via the API by calling a path like `http://localhost:8338/model/import_from_local_path/?model_path=<wsl_path>`.

- https://github.com/lm-sys/FastChat /39.4kstar/apache2/202506/python/inactive
  - FastChat is an open platform for training, serving, and evaluating large language model based chatbots.
  - FastChat powers Chatbot Arena (lmarena.ai), serving over 10 million chat requests for 70+ LLMs.
  - FastChat's core features include:
    - The training and evaluation code for state-of-the-art models (e.g., Vicuna, MT-Bench).
    - A distributed multi-model serving system with web UI and OpenAI-compatible RESTful APIs.
  - FastChat provides OpenAI-compatible APIs for its supported models, so you can use FastChat as a local drop-in replacement for OpenAI APIs. 
  - Multiple GPUs: You can use model parallelism to aggregate GPU memory from multiple GPUs on the same machine.
  - Metal Backend (Mac Computers with Apple Silicon or AMD GPUs)
  - Launch Chatbot Arena (side-by-side battle UI)
  - 🏘️ worker架构与gpustack类似
  - [Apple MLX Integration](https://github.com/lm-sys/FastChat/blob/main/docs/mlx_integration.md)

- https://github.com/gpustack/gpustack /4.4kStar/apache2/202601/python
  - https://gpustack.ai/
  - 开源的 GPU 集群管理器，专为高效的 AI 模型部署而设计。它允许您在自己的 GPU 硬件上高效运行模型，通过选择最佳推理引擎、调度 GPU 资源、分析模型架构以及自动配置部署参数来实现。
  - GPUStack 采用插件式架构，可以轻松添加新的 AI 模型、推理引擎和 GPU 硬件。
  - 经过测试的推理引擎：vLLM, SGLang, TensorRT-LLM, MindIE
  - 多集群 GPU 管理。 跨多个环境管理 GPU 集群。这包括本地服务器、Kubernetes 集群和云提供商。
  - 可插拔推理引擎。 自动配置高性能推理引擎，如 vLLM、SGLang 和 TensorRT-LLM。您也可以根据需要添加自定义推理引擎。
  - GPUStack worker 节点仅支持 Linux。如果你使用 Windows，可考虑使用 WSL2 并避免使用 Docker Desktop。macOS 不支持作为 GPUStack worker 节点。
  - 🍴 forks
  - https://github.com/xuan-wei/gpustack /202508
    - Implemented automatic instance start when requests arrive; adjust the number of replicas based on the demand/supply relationship in the past two mins.
  - https://github.com/shengjian-tech/gpustack /202508
    - 增加声音克隆的接口服务
  - https://github.com/szlhl1040/gpustack /202503
    - fix: making VRAM configurable from UMA for macOS
  - [Using Custom Inference Backend](https://docs.gpustack.ai/latest/tutorials/using-custom-backends/)
    - 支持 llama.cpp
  - v0.7.1_20250822 是最后一个非容器版
  - 🎯 [v2.0.0 _20251124](https://github.com/gpustack/gpustack/releases/tag/v2.0.0)
    - 🏘️ Container-based Architecture: Redesigned deployment framework to container-based architecture
    - Pluggable Inference Backends: multiple built-in inference backends (vLLM, SGLang, MindIE, vox-box).
    - Supports any custom inference backends like TensorRT-LLM, llama-server, kokoro-fastapi via container images
    - Inference Backend Multi-Versioning
    - GPU device management moved to separate GPUStack Runtime project.
    - Integrated Higress, an open-source AI gateway, to eliminate previous server proxy bottlenecks.
    - Built-in SGLang Support
  - [Dropped MacOS Support _202512](https://github.com/gpustack/gpustack/discussions/3704)
    - About macOS: starting with v2 we run all models inside containers, and macOS doesn’t allow GPU access in containers yet. 
    - As we don't have enough resources to maintain two separate runtimes, we had to drop macOS and native Windows support.
    - Two things could change this in the future:
    - If we have the bandwidth to keep a separate native desktop edition based on 0.7, or
    - If Apple adds GPU support to their container runtime (a lot of people are asking for it).

- https://github.com/containers/ramalama /2.5kStar/MIT/202601/python
  - https://ramalama.ai/
  - open-source tool that simplifies the local use and serving of AI models for inference from any source through the familiar approach of containers
  - RamaLama eliminates the need to configure the host system by instead pulling a container image specific to the GPUs discovered on the host system, and allowing you to work with various models and platforms.
  - Run AI models securely in rootless containers, isolating the model from the underlying host.
  - Models are treated similarly to how Podman and Docker treat container images.

- https://github.com/lemonade-sdk/lemonade /1.8kStar/apache2/202512/python/cpp
  - https://lemonade-server.ai/
  - Lemonade helps users run local LLMs with the highest performance by configuring state-of-the-art inference engines for their NPUs and GPUs.
  - Lemonade supports both GGUF and ONNX models. You can also import custom GGUF and ONNX models from Hugging Face by using our Model Manager (requires server to be running).
  - [How to run Lemonade server-router on an Apple Silicon mac _202510](https://github.com/lemonade-sdk/lemonade/issues/448)
    - Lemonade is an open source server-router (like OpenRouter, but local) that auto-configures LLM backends for your computer. 
    - The same Lemonade tool works across engines (llamacpp/ONNX/FLM), backends (vulkan/rocm/metal), and OSs (Windows/Ubuntu/macOS).
    - One of our most popular requests was for macOS support, so we shipped it last week
  - [The C++ rewrite of Lemonade is released and ready! : r/LocalLLaMA _202511](https://www.reddit.com/r/LocalLLaMA/comments/1p1h9fz/the_c_rewrite_of_lemonade_is_released_and_ready/)
    - Lemonade is an open-source alternative to local LLM tools like Ollama
  - [Electron app feedback _202511](https://github.com/lemonade-sdk/lemonade/issues/594)
  - pr已合并 [Geramy/macosx support stg1 _202602](https://github.com/lemonade-sdk/lemonade/pull/868)
    - This PR introduces comprehensive macOS support for Lemonade, focusing on native packaging, system integration, and performance optimizations. 
    - It establishes the foundation for seamless macOS integration, replacing the previous cross-platform approach with macOS-native implementations.
    - Switched to `.pkg` installer: Replaced `.dmg` with `.pkg` format for automatic installation of both the Electron app and system services
  - [Do we want the benefits of Ollama API without actually using Ollama? : r/LocalLLaMA _202602](https://www.reddit.com/r/LocalLLaMA/comments/1r8gb3p/do_we_want_the_benefits_of_ollama_api_without/)
    - lemonade is a local ai sever that does LLMs, image, and audio. Similar to Ollama or LM Studio but it’s open source and sponsored by AMD to make sure it’s optimized for their GPUs and NPUs.
    - Lemonade is 100% open source. It’s sponsored by AMD, which only makes money if you buy a computer. The idea is that if local AI gets increasingly awesome then more people will buy computers, so there’s no need for lemonade itself to have revenue/profits.
    - llama.cpp has had server routing for models for months now. You can literally mount and unmount models on the fly. lemonade literally copied and pasted the relevant snippets into their code base. They did do some other stuff in there, Ill give them that at the very least. But the only thing special about it is that its optimized for AMD hardware. Thats really it.

- https://github.com/kyuz0/amd-strix-halo-toolboxes /202604/python
  - https://strix-halo-toolboxes.com/
  - This project provides pre-built containers (“toolboxes”) for running LLMs on AMD Ryzen AI Max “Strix Halo” integrated GPUs. 
  - Toolbx is the standard developer container system in Fedora (and now works on Ubuntu, openSUSE, Arch, etc).
  - This repository is part of the Strix Halo AI Toolboxes project.
  - [Toolbox or Lemonade : r/StrixHalo _202604](https://www.reddit.com/r/StrixHalo/comments/1smyye9/toolbox_or_lemonade/)
    - Lemonade recently added NPU support under linux, which gets an extra 50 TOPS (vs the 76 TOPS from gpu/cpu)
    - Lemonade dev here. The main UI/UX idea is that installation should be a single click/command, and after that you can manage all your backends and models with the web app or CLI.
  - https://github.com/stampby/halo-ai-core

- https://github.com/jjang-ai/vmlx /apache2/202604/python/ts
  - https://vmlx.net/
  - vMLX - Home of JANG_Q - Cont Batch, Prefix, Paged, KV Cache Quant, VL - Powers MLX Studio. Image gen/edit, OpenAI/Anth
  - [MLX Studio — Chat, Code, Generate Images & More on Mac | Local AI with 20+ Tools](https://mlx.studio/)
    - https://github.com/jjang-ai/mlxstudio /未开源
    - MLX Studio is the app — the chat UI, agentic tools, model browser, and settings interface you interact with. 
    - vMLX Engine is the inference backend that powers it — the caching, batching, model loading, and API layer. Think of it like LM Studio and llama.cpp.
    - Any Mac with Apple Silicon (M1 or later) running macOS 26 (Tahoe). 8 GB RAM minimum, 16 GB+ recommended. Remote endpoints work on macOS 14+.
# mlx/llama.cpp-server/wrapper
- https://github.com/HazyResearch/minions /1.2kStar/MIT/202601/python
  - Big & Small LLMs working together
  - Minions is a communication protocol that enables small on-device models to collaborate with frontier models in the cloud. By only reading long contexts locally, we can reduce cloud costs with minimal or no quality degradation. This repository provides a demonstration of the protocol
  - We support three servers for running local models: lemonade, ollama, and tokasaurus. You need to install at least one of these.
    - You should use ollama if you do not have access to NVIDIA/AMD GPUs

- https://github.com/lordmathis/llamactl /69Star/MIT/202601/go/ts
  - http://llamactl.org/
  - Unified management and routing for llama.cpp, MLX and vLLM models with web dashboard.
  - llamactl sits on top of popular LLM backends (llama.cpp, MLX, and vLLM) and provides a unified interface to manage model instances through a web dashboard or REST API.
  - Run different models at the same time (7B for speed, 70B for quality)
  - llama.cpp router mode - serve multiple models from a single instance with on-demand loading
  - Multi-Backend Support: Native support for llama.cpp, MLX (Apple Silicon optimized), and vLLM
  - Modern React UI for managing instances, monitoring health, and viewing logs
  - 手动安装backend
    - brew install llama.cpp
    - pip install mlx-lm
    - pip install vllm
  - [I built llamactl - Unified management and routing for llama.cpp, MLX and vLLM models with web dashboard. : r/LocalLLaMA _202509](https://www.reddit.com/r/LocalLLaMA/comments/1nr06en/i_built_llamactl_unified_management_and_routing/)
    - I got tired of SSH-ing into servers to manually start/stop different LLM instances, so I built a web-based management layer for self-hosted language models.
    - Great for running multiple models at once or switching models on demand.
  - What differentiates this project from `llama-swap`?
    - The main thing is that you can create instances via web dashboard. With llama-swap you need to edit the config file. There's also API key auth which llama-swap doesn't have at all as far as I know.

- https://github.com/gitkaz/mlx_gguf_server /MIT/202512/python
  - a FastAPI based LLM server. 
  - Load multiple LLM models (MLX or llama.cpp) simultaneously using multiprocessing.
  - By leveraging multiprocessing, load, unload, and switch between multiple LLM models
  - This program is using MLX framework, so run only on Apple Silicon Macs.
  - Lora is only support for MLX model now
    - This branch adds basic LoRA (adapter) support for MLX models. Adapters are managed similarly to models and stored under the repository adapters/ directory. Frontend 

- https://github.com/malibrated/simple-llm-service /202507/python/代码少/inactive
  - lightweight, performant REST API service for Large Language Models with OpenAI-compatible endpoints. 
  - Supports both llama.cpp (GGUF) and Apple MLX models with configurable parameters and intelligent caching.

- https://github.com/xusenlinzy/api-for-open-llm /2.5kStar/apache2/202409/python/inactive
  - 此项目为开源大模型的推理实现统一的后端接口，与 OpenAI 的响应保持一致
  - 支持流式响应，实现打印机效果
  - 实现文本嵌入模型
  - 支持加载经过自行训练过的 lora 模型
  - 启动方式详见 vLLM启动方式、transformers启动方式
    - Uses native HuggingFace transformers library with PyTorch
    - Uses vLLM library optimized for LLM serving
  - langchain只有rag相关的逻辑用到了，用得很少
  - [changelog](https://github.com/xusenlinzy/api-for-open-llm/blob/master/docs/NEWS.md)
    - 【2023.11.24】 支持 llama-cpp-python 推理, 实测已删除
    - 20240612: reafactor project时不知为何删掉了llama.cpp的方式
  - 🍴 forks
    - https://github.com/wood-charcoal/api-for-open-llm
    - https://github.com/gordonchanfz/api-for-open-llm
  - [大佬，这个项目还更新吗？或者有啥平替的项目吗 ](https://github.com/xusenlinzy/api-for-open-llm/issues/318)
    - 应该不更新了，推荐使用gpustack来部署和管理模型
    - 模型和vllm版本更新太快了，两者不适配的问题频发，用爱发电确实难以为继哈哈哈

- https://github.com/katanaml/sparrow /5.1kStar/GPL/202601/python
  - https://sparrow.katanaml.io/
  - Structured data extraction and instruction calling with ML, LLM and Vision LLM
  - Pluggable Architecture: Mix and match different pipelines (Sparrow Parse, Instructor, Agents)
  - Multiple Backends: MLX (Apple Silicon), Ollama, vLLM, Docker, Hugging Face Cloud GPU
  - Multi-format Support: Images (PNG, JPG) and multi-page PDFs
  - API-First Design: RESTful APIs for easy integration
  - Built-in dashboard and agent workflow tracking
  - Local Vision LLMs: Mistral, QwenVL, DeepSeek OCR, etc.

- https://github.com/rmusser01/tldw_chatbook /AGPL/202508/python/inactive
  - A sophisticated Terminal User Interface (TUI) application built with the Textual framework for interacting with various Large Language Model APIs.
  - optional 可选安装mlx, mlx_whisper, rag

- https://github.com/abetlen/llama-cpp-python /9.9kStar/MIT/202508/python/inactive
  - Python bindings for llama.cpp

- https://github.com/withcatai/node-llama-cpp /1.8kStar/MIT/202601/ts/cpp
  - [Using in Electron](https://node-llama-cpp.withcat.ai/guide/electron)
  - Run AI models locally on your machine with node.js bindings for llama.cpp.
  - Metal, CUDA and Vulkan support
  - Embedding and reranking support
  - Up-to-date with the latest llama.cpp. Download and compile the latest release with a single CLI command
  - https://github.com/tib0/local-llama /CC-NC/202506/ts/inactive
    - an electron app that runs llama 3 models locally
    - Local Llama integrates Electron and llama-node-cpp. The app interacts with the llama-node-cpp library, which encapsulates the Llama 3 model within a node.js module, ensuring smooth compatibility with both Electron and native code.
    - Upon launching the application, a folder structure is created to store history, models, and logs under your current user folder
  - https://github.com/SurfaceData/local-llama-electron /apache2/202312/ts/inactive
    - a simple demo app that embeds node-llama-cpp into an Electron.js. 
    - Think of this as a basic skeleton for how you can create your own version of LM Studio, but without having to go through some javascript compiler pain.
    - built using Electron Forge
  - https://github.com/ItsPi3141/alpaca-electron /MIT/202312/python/js/inactive
    - run Alpaca (and other LLaMA-based local LLMs) on your own computer
    - uses llama.cpp as its backend 
- https://github.com/electron/llm /202505/ts/inactive
  - This module makes it easy for developers to prototype local-first applications interacting with local large language models (LLMs)
  - It aims for an API surface similar to Chromium's window. AI API, except that you can supply any GGUF model.
  - makes use of `node-llama-cpp`.

- https://github.com/ngxson/wllama /975Star/MIT/202512/cpp/ts
  - https://huggingface.co/spaces/ngxson/wllama
  - WebAssembly binding for llama.cpp - Enabling on-browser LLM inference
  - Can run inference directly on browser (using WebAssembly SIMD), no backend or GPU is needed
  - Inference is done inside a worker, does not block UI render
  - No runtime dependency
  - Auto switch between single-thread and multi-thread build based on browser support
  - No WebGPU support, but maybe possible in the future
  - Max file size is 2GB, due to size restriction of ArrayBuffer.

- https://github.com/antarasi/electron-ollama /MIT/202508/ts/inactive
  - Bundle Ollama with your Electron.js app for seamless user experience
  - No conflict: Works well with standalone Ollama server (skips installation if Ollama already runs)
  - Binaries Management: Automatically find and manage Ollama executables
  - Cross-Platform: Tested on Windows, macOS, and Linux

- https://github.com/signerlabs/klee /1.7kStar/MIT/202511/ts/inactive
  - https://github.com/signerlabs/klee-service /legacy
  - a modern desktop application that combines AI-powered chat, knowledge base management, and note-taking capabilities.
  - It offers both Cloud Mode for seamless synchronization and Private Mode for complete offline functionality.
  - Integrated with OpenAI and local Ollama models
  - Tiptap-based collaborative editor with Markdown support
  - At its core, Klee is built on:
    - `Ollama`: For running local LLMs quickly and efficiently.
    - `LlamaIndex`: As the data framework.
  - Privacy-First: Complete offline mode with local AI and data storage
  - Optional cloud synchronization via Supabase
  - Private Mode
    - Local AI: Powered by Ollama (embedded or system-installed)
    - Local Storage: SQLite for structured data
    - Vector Search: LanceDB for semantic search (planned)
  - Cloud Mode
    - File Storage: Supabase Storage for documents and attachments
    - Data Sync: PostgreSQL database with real-time updates
    - Authentication: Google OAuth and email/password via Supabase
  - 🍴 forks
  - https://github.com/EclipseFever/Klee /202504
    - electron-build-ci: https://github.com/EclipseFever/Klee/blob/main/.github/workflows/build.yml
  - https://github.com/olivestory-corp/Sasara /MIT/202505/ts
    - local AI on your desktop with a built-in RAG knowledge base and Markdown note support.
    -  built on: klee, ollama, llamaindex
  - [I built and open sourced a electron app to run LLMs locally with built-in RAG knowledge base and note-taking capabilities. : r/electronjs _202503](https://www.reddit.com/r/electronjs/comments/1j43om9/i_built_and_open_sourced_a_electron_app_to_run/)
    - Would the users need to download Ollama separately or is it somehow embedded?
      - It is embedded, but if you already have ollama running, we will use your ollama instance.
    - We start with SwiftUI but switch to Electron after 3 weeks
  - [I built and open sourced a desktop app to run LLMs locally with built-in RAG knowledge base and note-taking capabilities. : r/LocalLLM _202503](https://www.reddit.com/r/LocalLLM/comments/1j4wvsu)
  - [I open-sourced Klee today, a desktop app designed to run LLMs locally with ZERO data collection. It also includes built-in RAG knowledge base and note-taking capabilities. : r/LocalLLaMA _202503](https://www.reddit.com/r/LocalLLaMA/comments/1j2j7su/i_opensourced_klee_today_a_desktop_app_designed/)
    - I see you were inspired by Slack's UI
    - Can I just point it at the folder with my existing models?
      - If you use windows, look up junctions and symbolic links: mklink /J C:\LinkDirectory D:\TargetDirectory
    - When I've used Ollama I find it's not just the file location; it requires turning the GGUF models into some hashed 'model file', which is exactly why I quit using Ollama.
    - Does this force Ollama? Or can I use llama.cpp as a backend?
      - backend and front end are in different repo, you can use llamacpp as backend
    - What key features differentiate this from those options like lmstudio/koboldai?
      - Nothing. Just yet another wrapper over ollama.
    - What does Klee use for embeddings for the RAG? does it support directory/folder upload or just individual file upload?
      - individual file, multiple files and folder
    - Would also like to know if it allows users to connect to an existing ollama instance over LAN? Would it allow me to connect to my ollama API on my network? So I can use this on my laptop and connect to my AI server in the basement? Can you put a custom IP/port? 
      - this is the most requested feature 

- https://github.com/BruceMacD/chatd /MIT/202405/js/inactive
  - Chat with your documents using local AI. All your data stays on your computer 
  - What makes chatd different from other "chat with local documents" apps is that it comes with the local LLM runner packaged in. 
  - If you already have an Ollama instance running locally, chatd will automatically use it. Otherwise, chatd will start an Ollama server for you and manage its lifecycle.

- https://github.com/lmstudio-ai/mlx-engine /859Star/MIT/202601/python
  - Apple MLX LLM Engine for LM Studio
  - Built with
    - mlx-lm - Apple MLX inference engine (MIT)
    - mlx-vlm - Vision model inferencing for MLX (MIT)
    - Outlines - Structured output for LLMs (Apache 2.0)

- https://github.com/frost-beta/node-mlx /MIT/202504/cpp/ts
  - A machine learning framework for Node.js, based on MLX.
  - https://x.com/zcbenz/status/1787441190629208437 _202405
    - Motivations: I don't like writing python, which is the No.1 reason.
    - I ported ~15k lines of MLX's python code (10k are tests) to typescript, using GPT4. It cost me ~$70.
    - Still had to review every line and do heavy modifications for most code, but freed from repetitive boring labour work.
    - It took me a month from 0 to publishing the project, would probably take another month if without GPT4.
  - https://github.com/frost-beta/llama3.js /202407/js/inactive
    - A JavaScript implementation of Llama 3 using node-mlx.

- https://github.com/Michael-A-Kuykendall/shimmy /3.3kStar/MIT/202510/rust
  - Python-free Rust inference server — OpenAI-API compatible
  - Available Backends
    - MLX native acceleration for Apple Silicon
    - CUDA	NVIDIA GPUs
    - Vulkan	Cross-platform GPUs
    - MOE Hybrid	Any GPU + CPU

- https://github.com/ShelbyJenkins/llm_client/tree/master/lmcpp
  - llama.cpp's llama-server for Rust
  - I have the lmcpp crate that is just a llama-server wrapper, and even that was a lot of work

- https://github.com/EricLBuehler/mistral.rs /MIT/202510/rust
  - a cross-platform, highly-multimodal inference engine
  - All-in-one multimodal workflow: text↔text, text+vision↔text, text+vision+audio↔text, text→speech, text→image
  - APIs: Rust, Python, OpenAI HTTP server (with Chat Completions, Responses API), MCP server
  - Support prequantized models from MLX 

- https://github.com/intentee/paddler /1.4kStar/apache2/202601/rust/ts
  - https://paddler.intentee.com/
  - open-source LLM load balancer and serving platform. It allows you to run inference, deploy, and scale LLMs on your own infrastructure
  - Inference through a built-in `llama.cpp` engine
  - Dynamic model swapping
  - Works through agents that can be added dynamically, allowing integration with autoscaling tools
  - Request buffering, enabling scaling from zero hosts
  - Built-in web admin panel for management, monitoring, and testing
  - Paddler is self-contained in a single binary file with only two deployable components, the balancer and the agents.
    - The balancer exposes Inference service, Management service, Web admin panel
    - Agents are usually deployed on separate instances. They further distribute the incoming requests to slots, which are responsible for generating tokens and embeddings.
    - Paddler uses a built-in llama.cpp engine for inference, but has its own implementation of llama.cpp slots, which keep their own context and KV cache.
  - [I just rewrote llama.cpp server in Rust (most of it at least), and made it scalable : r/rust _202508](https://www.reddit.com/r/rust/comments/1ml5ogd/i_just_rewrote_llamacpp_server_in_rust_most_of_it/)
    - I rewrote most of the llama-server, made it scalable, and bundled that into Paddler.
    - Initially, the project started as a monitor for the llama.cpp servers, but ended up with being an entire platform for self-hosting LLMs written in Rust, with its own backend (still uses llama.cpp for inference, but the entire infra and server components are custom now).
    - Ollama is a wrapper for llama-server. They don't even do the bindings directly. So this is an improvement in that regard.

- https://github.com/mlx-chat/mlx-chat-app /MIT/202403/python/ts/inactive
  - Chat with MLX is a high-performance macOS application that connects your local documents to a personalized large language model (LLM).
  - First, setup huggingface access tokens to download models
  - we are working to release with correct packaging (pyinstaller & electron-builder) and authentication (Apple codesign). I

- https://github.com/NexaAI/nexa-sdk /apache2/202511/go
  - https://docs.nexa.ai/
  - NexaSDK is an easy-to-use developer toolkit for running any AI model locally — across NPUs, GPUs, and CPUs — powered by our NexaML engine, built entirely from scratch for peak performance on every hardware stack.
  - Unlike wrappers that depend on existing runtimes, NexaML is a unified inference engine built at the kernel level.
  - NexaML supports 3 model formats: GGUF, MLX, and Nexa AI's own .nexa format.
  - [Running the latest LLMs like Granite-4.0 and Qwen3 fully on ANE (Apple NPU) : r/LocalLLM](https://www.reddit.com/r/LocalLLM/comments/1p0tmew/running_the_latest_llms_like_granite40_and_qwen3/)
    - TL;DR Well-built wrapper around proprietary engine. "Apache 2.0" is marketing—the ML inference core is closed source. Great for NPU/mobile where there's no real option. Terrible for learning/auditing/contributing.
    - 🏠 how it works: Your CLI → Go wrapper → CGo → nexasdk-bridge (??) → Hardware
    - What you clone: Apache 2.0 Go/Python wrappers (~20k lines)
    - What the license covers: Just the wrapper
    - What you actually run: Closed-source `nexasdk-bridge` binary curled from their S3
    - What does the work: Mystery C library, unknown license
    - features: Clean Go structure, multiple NPU backends (Qualcomm, Apple, Intel, AMD)
    - Can't build tests without downloading proprietary binary first

- https://github.com/DAMO-NLP-SG/Multipurpose-Chatbot /apache2/202404/python/代码少/inactive
  - A chatbot UI for RAG, multimodal, text completion. (support Transformers, llama.cpp, MLX, vLLM)
  - Designed support both locally, remote and huggingface spaces.
  - 安装不同os的依赖，分别执行
    - pip install -r vllm_requirements.txt
    - pip install -r mlx_requirements.txt

- https://github.com/mzbac/kooka-server /MIT/202601/python
  - mlx-lm server wrapper for agentic harness
  - Local inference web server for MLX / mlx-lm.
  - uvx kooka-server serve --model mlx-community/MiniMax-M2.1-4bit --host 127.0.0.1 --port 8080

- https://github.com/LlamaEdge/LlamaEdge /apache2/202511/rust/inactive
  - https://llamaedge.com/
  - The easiest & fastest way to run customized and fine-tuned LLMs locally or on the edge
  - The Rust+Wasm stack provides a strong alternative to Python in AI inference.
  - The WASI-NN ggml plugin embedded llama.cpp as its backend.
  - https://github.com/LlamaEdge/scalable-server
    - Selection of backends. The server can switch between inference frameworks (e.g., llama.cpp or MLX, plain CUDA or TensorRT) through runtime configuration to optimize performance for the specific use case.

- https://github.com/devo8604/CICD_LLM_DATA_SCRAPER /MIT/202512/python 
  - Automated pipeline for generating high-quality Q&A training data from Git repositories. Processes source code with LLMs to create fine-tuning datasets. 
  - Features smart caching, resume support, MLX (Apple Silicon) & llama.cpp backends, multiple export formats (Alpaca, ChatML, etc).
  - This tool processes source code files and uses Large Language Models to create Q&A pairs suitable for fine-tuning code-focused LLMs.

- https://github.com/dillondesilva/tauri-local-lm /202505/rust/ts/inactive
  - [Building Local LM Desktop Applications with Tauri _202506](https://medium.com/@dillon.desilva/building-local-lm-desktop-applications-with-tauri-f54c628b13d9)
    - Sticking with our approach of using prebuilt llama.cpp binaries, we’re lucky that the Tauri ecosystem provides a well-defined method for embedding external binaries.
    - A sidecar is any binary bundled alongside your application that can be executed to add functionality. In our case, we’ll be adding the `llama-server` binary as a sidecar.
    - You’ll notice I’ve added the suffix aarch64-apple-darwin to all the llama.cpp binaries. This is because when Tauri builds your application, it needs to select the correct binaries based on the target architecture.
    - we’ll also want to be spawn our runtime from JS/TS code in the webview. 
    - Installing the Tauri shell plugin, enabling us to handle execute/spawn of external binaries. Expose this shell usage capability to the webview for our respective binaries

- https://github.com/av/harbor /2.3kStar/apache2/202601/python/ts
  - Harbor is a CLI and companion app that lets you spin up a complete local LLM stack—backends like Ollama, llama.cpp, or vLLM, frontends like Open WebUI, plus supporting services like SearXNG for web search, Speaches for voice chat, and ComfyUI for image generation—all pre-wired to work together with a single harbor up command. 
  - No manual setup: just pick the services you want and Harbor handles the Docker Compose orchestration, configuration, and cross-service connectivity so you can focus on actually using your models.

- https://github.com/dorukgezici/pydantic-ai-mlx /202503/python/inactive
  - Add MLX support to Pydantic AI through LM Studio or mlx-lm, run MLX compatible HF models on Apple silicon
  - LM Studio backend (OpenAI compatible server that can also utilize mlx-lm, model runs on a separate background process)
  - LM Studio backend (OpenAI compatible server that can also utilize mlx-lm, model runs on a separate background process)

- https://github.com/acon96/home-llm /202601/python
  - A Home Assistant integration & Model to control your smart home using a Local LLM
  - a complete solution for adding AI-powered voice and chat control to Home Assistant.
  - It consists of two parts:
    - Local LLM Integration – A Home Assistant custom component that connects local language models to your smart home
    - Home Models – Small, efficient AI models fine-tuned specifically for smart home control
  - Supported Backends
    - Llama.cpp (built-in)	Running models directly in Home Assistant

- https://github.com/pwilkin/llama-runner /MIT/202508/python/inactive
  - Llama.cpp runner/swapper and proxy that emulates LMStudio / Ollama backends (for IntelliJ AI Assistant / GitHub Copilot), now with headless mode.
  - support for different llama.cpp runtimes including ik_llama 
  - dynamically loads and unloads runtimes based on model string in request
  - double proxy: emulation for LM Studio-specific backend and OpenAI-compatible backends (running on port 1234) and for Ollama specific backends (running on port 11434)

- https://github.com/mostlygeek/llama-swap /2.6kStar/MIT/202603/go/swift
  - Reliable model swapping for any local OpenAI/Anthropic compatible server - llama.cpp, vllm, etc
  - Run multiple generative AI models on your machine and hot-swap between them on demand. 
  - llama-swap works with any OpenAI and Anthropic API compatible server 
  - Built in Go for performance and simplicity, llama-swap has zero dependencies and is incredibly easy to set up. 
  - [Add a Playground to the UI _202601](https://github.com/mostlygeek/llama-swap/issues/481)
  - 🍴 forks
  - https://github.com/kooshi/llama-swappo
    - A fork of llama-swap with a minimally implemented ollama compatible api grafted onto it
- https://github.com/bjodah/llm-multi-backend-container /BSD/202602/python
  - Docker/podman container for llama.cpp/vllm/exllamav{2, 3} orchestrated using llama-swap
  - This repo is my working config, it's mainly used on a 16 core Ryzen machine with 64 GiB RAM and a single RTX 3090.
- https://github.com/pkeffect/llama-swap-sync /MIT/202511/python/inactive
  - production-ready Python toolkit to automate the synchronization between a directory of .gguf model files and a llama-swap config.yaml file. 
  - This project provides utilities for downloading models from Hugging Face, verifying their integrity, and automatically maintaining your llama-swap configuration.

- https://github.com/yousefjan/rais /MIT/202603/cpp
  - A scheduling runtime for concurrent inference on Apple Metal
  - [I built a priority scheduler that cuts TTFT 3.4x when running concurrent mlx-lm requests : r/mlxAI _202604](https://www.reddit.com/r/mlxAI/comments/1s7kpn7/i_built_a_priority_scheduler_that_cuts_ttft_34x/)

- https://github.com/raketenkater/llm-server /MIT/202604/python
  - Smart launcher for ik_llama.cpp and llama.cpp. Auto-detects your hardware, figures out the optimal configuration, and launches the server — no manual flag tuning required.
  - Running llama.cpp on multi-GPU setups means juggling dozens of flags. llm-server figures it all out.
  - Supports Linux (NVIDIA CUDA), macOS (Apple Silicon Metal), and Windows (via WSL2).

- https://github.com/PurpleDirective/purple-directive-cli /MIT/202603/python
  - https://purpledirective.com/
  - A local AI agent with native inference + MCP tool calling. ~3800 lines of Python across 5 core files. 
  - No frameworks, no OpenAI shims, no abstractions between you and the model.
  - Dual inference backends: Ollama (/api/chat) for GGUF models, vllm-mlx (/v1/chat) for Apple Metal (auto-detected at startup)
  - Unified brain server -- Memory, knowledge, web search, and teaching in one MCP server (8 tools). Replaces separate memory + knowledge servers.
# llm-apps
- https://github.com/eclaire-labs/eclaire /MIT/202510/ts
  - Local-first, open-source AI assistant for your data. Unify tasks, notes, docs, photos, and bookmarks. Private, self-hosted, and extensible via APIs.
  - works with llama.cpp, vLLM, mlx-lm/mlx-vlm, LM Studio, Ollama, and more via the standard OpenAI-compatible API.
    - Eclaire is designed to work with various LLM backends and models. By default we picked llama.cpp
    - eclaire-backend expects a text model with decent tool calling / agentic capabilities
    - eclaire-workers expects a multi-modal model with support for text + images
    - Both eclaire-backend and eclaire-workers can point to same or different endpoints as long as the model meets the requirements mentioned above.

- https://github.com/nodetool-ai/nodetool /269Star/AGPL/202603/ts
  - https://nodetool.ai/
  - Nodetool lets you design agents that work with your data. Use any model to analyze data, generate visuals, or automate workdlows.
  - Local models (Llama.cpp, MLX, vLLM, HuggingFace) + optional cloud (OpenAI/Anthropic/Replicate/FAL)
  - What NodeTool Is Not (today)
    - Managed SaaS, SLAs, multi‑tenant

- https://github.com/darrylmorley/ollmlx /202603/swift
  - Run local LLMs on Apple Silicon via mlx-lm. 
  - Menubar app + CLI with OpenAI-compatible and Ollama-compatible APIs on localhost:11434.
  - [Show: ollmlx — run local LLMs on Apple Silicon with an Ollama-compatible API. : r/mlxAI _202604](https://www.reddit.com/r/mlxAI/comments/1s82jmf/show_ollmlx_run_local_llms_on_apple_silicon_with/)
# examples
- https://github.com/Lakr233/FlowDown /934Star/AGPL/202601/swift
  - a native AI chat client for Apple platforms, designed for speed, privacy, and power users. 
  - It provides a fluid, responsive interface to interact with a variety of AI models, right from your iPhone, iPad, and Mac.
  - 🧪 both the Mac app and iPhone app support testing model abilities including tool-calling, instruction-following, coding
# utils
- https://github.com/waybarrios/vllm-mlx /apache2/202601/python
  - vLLM-like inference for Apple Silicon - GPU-accelerated Text, Image, Video & Audio on Mac
  - vllm-mlx brings native Apple Silicon GPU acceleration to vLLM by integrating: mlx-lm, mlx-vlm, mlx-audio

- https://github.com/mzau/mlx-knife /112Star/apache2/202511/python
  - ollama like cli tool for MLX models on huggingface (pull, rm, list, show, serve etc.)
  - [[Update] mlx-knife 2.0 stable — MLX model manager for Apple Silicon : r/LocalLLaMA _202511](https://www.reddit.com/r/LocalLLaMA/comments/1otwdq0/update_mlxknife_20_stable_mlx_model_manager_for/)
    - Can you help me understand how this is better than simply using: mlx_lm.server
      - Yeah. Unless it supports vision, mlx_lm.server plus llama swap is much better.

- https://github.com/mlx-node/mlx-node /MIT/202512/rust/ts
  - MLX-Node brings Apple's MLX framework to JavaScript/TypeScript, enabling efficient on-device ML inference and training on Apple Silicon and CUDA devices. 
  - Built with a Rust compute layer and TypeScript orchestration, it delivers production-ready GRPO training with 100% feature parity with HuggingFace's TRL library.
  - Pure Rust/TypeScript implementation — no Python runtime required
  - TypedArray-First API: Zero-copy operations using native JavaScript typed arrays

- https://github.com/rohanelukurthy/rig-rank /MIT/202602/go
  - a CLI tool written in Go that benchmarks how well Large Language Models (LLMs) run on your specific hardware. 
  - It measures real-world performance metrics via Ollama and tells you whether your "rig" is ready for AI workloads.
  - [I built a small CLI tool to help beginners see if their hardware can actually handle local LLMs : r/ollama](https://www.reddit.com/r/ollama/comments/1r8rgg8/i_built_a_small_cli_tool_to_help_beginners_see_if/)
# llm-server
- https://github.com/danveloper/flash-moe /202603/oc
  - Running a big model on a small laptop
  - Pure C/Metal inference engine that runs Qwen3.5-397B-A17B (a 397 billion parameter Mixture-of-Experts model) on a MacBook Pro with 48GB RAM at 4.4+ tokens/second with production-quality output including tool calling.
  - The entire 209GB model streams from SSD through a custom Metal compute pipeline.
  -  No Python. No frameworks. Just C, Objective-C, and hand-tuned Metal shaders.
# llm-provider
- https://github.com/ArseniiBrazhnyk/Veritensor /apache2/202601/python
  - https://www.veritensor.com/
  - Veritensor is the Zero-Trust security platform for the AI Supply Chain. 
  - We replace naive model scanning with deep AST analysis and cryptographic signing.
  - [I need a feedback about an open-source CLI that scan AI models (Pickle, PyTorch, GGUF) for malware, verify HF hashes, and check licenses : r/LocalLLM _202601](https://www.reddit.com/r/LocalLLM/comments/1qcmc9v/i_need_a_feedback_about_an_opensource_cli_that/)
    - I've created a new CLI tool to secure AI pipelines. It scans models (Pickle, PyTorch, GGUF) for malware using stack emulation, verifies file integrity against the Hugging Face registry, and detects restrictive licenses (like CC-BY-NC). It also integrates with Sigstore for container signing.
# mlx-benchmark

# llm-cpu/ram
- https://github.com/e1n00r/tinyserve /MIT/202603/python
  - Run 20B-400B+ MoE models on 8GB consumer GPUs. 
  - 3-tier expert caching (SSD→RAM→GPU), native MXFP4/GGUF Q4_K compute, SDPA Flash attention, CPU KV cache for unlimited context. Pure Python.
  - [TinyServe - run large MoE models on consumer hardware : r/LocalLLaMA _202603](https://www.reddit.com/r/LocalLLaMA/comments/1s54zdo/tinyserve_run_large_moe_models_on_consumer/)
  - Not enough VRAM? We keep only hot experts and offload the rest to RAM.
  - Not enough RAM? We have a second tier of caching logic with prefetch from SSD and performance hacks.
  - This project is a PoC to push these features in vLLM and llama.cpp, but as i started I kept piling features into it and I intend to get to it to be at least as good as llama.cpp on all popular models.
# model-safetensors/gguf
- https://github.com/EvanZhouDev/umr /AGPL/202604/ts
  - The Unified Model Registry for all your local AI apps.
  - [Use the Same Model Across Ollama, LM Studio, Jan, and your Favorite Local AI Apps : r/ollama _202604](https://www.reddit.com/r/ollama/comments/1sgwjwy/use_the_same_model_across_ollama_lm_studio_jan/)
    - A problem I’ve had is that every local AI app, like Ollama, LM Studio, Jan, all download and store their own copy of any local model you use.
    - So, I created UMR, the Unified Model Registry for all your local AI Apps!
    - It lets you add one canonical copy of whatever model you’re using, then link it to tools like Ollama, LM Studio, or Jan. Linking uses the same model you already downloaded, doesn’t require extra storage, and is super fast.
    - Add any Hugging Face GGUF model that you want. Use that model ID to add it to any supported local AI app. 
    - UMR itself does not necessarily store your model. It simply knows where to find them after you register them.
      - You can also add a model manually with `umr add ./path/to/file.gguf`, which will clone it locally into UMR's own store
# more
- https://github.com/intel/ipex-llm /apache2/202510/python/inactive
  - an LLM acceleration library for Intel GPU (e.g., local PC with iGPU, discrete GPU such as Arc, Flex and Max), NPU and CPU
  - See demos of running local LLMs on Intel Core Ultra iGPU, Intel Core Ultra NPU, single-card Arc GPU, or multi-card Arc GPUs using ipex-llm below.
  - IPEX-LLM provides seamless integration with llama.cpp, Ollama, vLLM, HuggingFace transformers, LangChain, LlamaIndex
  - 70+ models have been optimized/verified on ipex-llm
  - [Run llama.cpp Portable Zip on Intel GPU with IPEX-LLM](https://github.com/intel/ipex-llm/blob/main/docs/mddocs/Quickstart/llamacpp_portable_zip_gpu_quickstart.md)
    - 需要下载并使用定制版llama.cpp
