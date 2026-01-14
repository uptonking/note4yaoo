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
# popular
- https://github.com/ml-explore/mlx-lm /2.7kStar/MIT/202511/python
  - a Python package for generating text and fine-tuning large language models on Apple silicon with MLX.
  - Integration with the Hugging Face Hub to easily use thousands of LLMs with a single command.
  - Low-rank and full model fine-tuning with support for quantized models.
  - Distributed inference and fine-tuning with mx.distributed
  - [MLX Community Projects · ml-explore/mlx _202402](https://github.com/ml-explore/mlx/discussions/654)

- https://github.com/Blaizzy/mlx-vlm /1.8kStar/MIT/202511/python
  - a package for inference and fine-tuning of Vision Language Models (VLMs) and Omni Models (VLMs with audio and video support) on your Mac using MLX

- https://github.com/RamboRogers/mlx-gui /GPL/202601/python/tkinter
  - https://mlxgui.com/
  - A lightweight Inference Server for Apple's MLX engine with a GUI.
  - TLDR - OpenRouter-style v1 API interface for MLX with Ollama-like model management, featuring auto-queuing, on-demand model loading, and multi-user serving capabilities via single mac app.

- https://github.com/cubist38/mlx-openai-server /MIT/202601/python
  - A high-performance API server that provides OpenAI-compatible endpoints for MLX models. 
  - Developed using Python and powered by the FastAPI framework, it provides an efficient, scalable, and user-friendly solution for running MLX-based vision and language models locally with an OpenAI-compatible interface.
  - Multimodal model support with vision, audio, and text
  - Easy Python and CLI usage
  - LoRA adapter support for fine-tuned image generation and editing
  - https://github.com/arcee-ai/fastmlx /apache2/202503/python/inactive
    - production ready API to host MLX models.
# mlx/llama.cpp-server/wrapper
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

- https://github.com/xusenlinzy/api-for-open-llm /2.5kStar/apache2/202409/python/inactive
  - 此项目为开源大模型的推理实现统一的后端接口，与 OpenAI 的响应保持一致
  - 支持流式响应，实现打印机效果
  - 实现文本嵌入模型
  - 支持加载经过自行训练过的 lora 模型
  - 启动方式详见 vLLM启动方式、transformers启动方式
    - Uses native HuggingFace transformers library with PyTorch
    - Uses vLLM library optimized for LLM serving
  - [changelog](https://github.com/xusenlinzy/api-for-open-llm/blob/master/docs/NEWS.md)
    - 【2023.11.24】 支持 llama-cpp-python 推理, 实测已删除
  - 🍴 forks
    - https://github.com/wood-charcoal/api-for-open-llm
    - https://github.com/gordonchanfz/api-for-open-llm
  - [大佬，这个项目还更新吗？或者有啥平替的项目吗 ](https://github.com/xusenlinzy/api-for-open-llm/issues/318)
    - 应该不更新了，推荐使用gpustack来部署和管理模型
    - 模型和vllm版本更新太快了，两者不适配的问题频发，用爱发电确实难以为继哈哈哈

- https://github.com/gpustack/gpustack /4.4kStar/apache2/202601/python
  - https://gpustack.ai/
  - 开源的 GPU 集群管理器，专为高效的 AI 模型部署而设计。它允许您在自己的 GPU 硬件上高效运行模型，通过选择最佳推理引擎、调度 GPU 资源、分析模型架构以及自动配置部署参数来实现。
  - GPUStack 采用插件式架构，可以轻松添加新的 AI 模型、推理引擎和 GPU 硬件。
  - 经过测试的推理引擎：vLLM, SGLang, TensorRT-LLM, MindIE
  - 多集群 GPU 管理。 跨多个环境管理 GPU 集群。这包括本地服务器、Kubernetes 集群和云提供商。
  - 可插拔推理引擎。 自动配置高性能推理引擎，如 vLLM、SGLang 和 TensorRT-LLM。您也可以根据需要添加自定义推理引擎。
  - GPUStack worker 节点仅支持 Linux。如果你使用 Windows，可考虑使用 WSL2 并避免使用 Docker Desktop。macOS 不支持作为 GPUStack worker 节点。
  - [Using Custom Inference Backend - GPUStack](https://docs.gpustack.ai/latest/tutorials/using-custom-backends/)
    - 

- https://github.com/lm-sys/FastChat /apache2/202506/python/inactive
  - an open platform for training, serving, and evaluating large language model based chatbots.
  - It has a modular architecture with a "Controller", "Model Workers", and an "API Server".
  - Look at their Model Worker implementation. They have different workers for different backends. This is a great example of a Python-based distributed architecture.

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
  - makes use of node-llama-cpp

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
# llm-apps
- https://github.com/eclaire-labs/eclaire /MIT/202510/ts
  - Local-first, open-source AI assistant for your data. Unify tasks, notes, docs, photos, and bookmarks. Private, self-hosted, and extensible via APIs.
  - works with llama.cpp, vLLM, mlx-lm/mlx-vlm, LM Studio, Ollama, and more via the standard OpenAI-compatible API.
    - Eclaire is designed to work with various LLM backends and models. By default we picked llama.cpp
    - eclaire-backend expects a text model with decent tool calling / agentic capabilities
    - eclaire-workers expects a multi-modal model with support for text + images
    - Both eclaire-backend and eclaire-workers can point to same or different endpoints as long as the model meets the requirements mentioned above.

- https://github.com/nodetool-ai/nodetool /AGPL/202511/ts
  - https://nodetool.ai/
  - Nodetool lets you design agents that work with your data. Use any model to analyze data, generate visuals, or automate workdlows.
  - Local models (Llama.cpp, MLX, vLLM, HuggingFace) + optional cloud (OpenAI/Anthropic/Replicate/FAL)
  - What NodeTool Is Not (today)
    - Managed SaaS, SLAs, multi‑tenant
# examples

# utils

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
  - [Electron app feedback _202411](https://github.com/lemonade-sdk/lemonade/issues/594)

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
# more
