---
title: lib-ai-app-examples-utils-mlx
tags: [ai, large-language-model, machine-learning, macos, mlx]
created: 2025-11-01T10:54:01.772Z
modified: 2025-11-01T10:54:26.044Z
---

# lib-ai-app-examples-utils-mlx

# guide

# popular
- https://github.com/ml-explore/mlx-lm /2.7kStar/MIT/202511/python
  - a Python package for generating text and fine-tuning large language models on Apple silicon with MLX.
  - Integration with the Hugging Face Hub to easily use thousands of LLMs with a single command.
  - Low-rank and full model fine-tuning with support for quantized models.
  - Distributed inference and fine-tuning with mx.distributed
  - [MLX Community Projects · ml-explore/mlx _202402](https://github.com/ml-explore/mlx/discussions/654)

- https://github.com/lordmathis/llamactl /MIT/202509/go/ts
  - http://llamactl.org/
  - Unified management and routing for llama.cpp, MLX and vLLM models with web dashboard.
  - llamactl sits on top of popular LLM backends (llama.cpp, MLX, and vLLM) and provides a unified interface to manage model instances through a web dashboard or REST API.
  - [I built llamactl - Unified management and routing for llama.cpp, MLX and vLLM models with web dashboard. : r/LocalLLaMA _202509](https://www.reddit.com/r/LocalLLaMA/comments/1nr06en/i_built_llamactl_unified_management_and_routing/)
    - I got tired of SSH-ing into servers to manually start/stop different LLM instances, so I built a web-based management layer for self-hosted language models.
    - Great for running multiple models at once or switching models on demand.
  - What differentiates this project from `llama-swap`?
    - The main thing is that you can create instances via web dashboard. With llama-swap you need to edit the config file. There's also API key auth which llama-swap doesn't have at all as far as I know.
# mlx/llama.cpp
- https://github.com/Michael-A-Kuykendall/shimmy /3.3kStar/MIT/202510/rust
  - Python-free Rust inference server — OpenAI-API compatible
  - Available Backends
    - MLX native acceleration for Apple Silicon
    - CUDA	NVIDIA GPUs
    - Vulkan	Cross-platform GPUs
    - MOE Hybrid	Any GPU + CPU

- https://github.com/EricLBuehler/mistral.rs /MIT/202510/rust
  - a cross-platform, highly-multimodal inference engine
  - All-in-one multimodal workflow: text↔text, text+vision↔text, text+vision+audio↔text, text→speech, text→image
  - APIs: Rust, Python, OpenAI HTTP server (with Chat Completions, Responses API), MCP server
  - Support prequantized models from MLX 

- https://github.com/NexaAI/nexa-sdk /apache2/202511/go
  - https://docs.nexa.ai/
  - NexaSDK is an easy-to-use developer toolkit for running any AI model locally — across NPUs, GPUs, and CPUs — powered by our NexaML engine, built entirely from scratch for peak performance on every hardware stack.
  - Unlike wrappers that depend on existing runtimes, NexaML is a unified inference engine built at the kernel level.
  - NexaML supports 3 model formats: GGUF, MLX, and Nexa AI's own .nexa format.

- https://github.com/DAMO-NLP-SG/Multipurpose-Chatbot /apache2/202404/python/inactive
  - A chatbot UI for RAG, multimodal, text completion. (support Transformers, llama.cpp, MLX, vLLM)
  - Designed support both locally, remote and huggingface spaces.
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

# more
