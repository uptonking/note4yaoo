---
title: lib-aikit-ollama-dev
tags: [large-language-model, ollama]
created: 2026-01-14T18:56:51.610Z
modified: 2026-01-14T18:57:01.673Z
---

# lib-aikit-ollama-dev

# guide

- tips-ai-tools
  - lm studio底层用的也是llama.cpp, 不必寻找替代，深入底层更容易替代和扩展

- mlx
  - mlx的优点之一是方便支持在iphone上运行

- ollama-pros
  - stable and rich models
  - 对 embedding 模型额支持更好

- ollama-cons
  - 很多模型推理速度比 llama.cpp 慢
  - 对 mlx 模型的支持落后

- lmstudio-pros
  - ui操作体验友好

- lmstudio-cons
  - 不提供api来支持remote control
  - 对mlx格式的 embedding 模型额支持有问题, 但gguf格式模型支持好
# draft
- 🤔 一种思路: tool-call时使用擅长tool-call的模型，分析时使用公益站的聊天优质但无法tool-call的模型
  - 支持类似 roocode 的 model profile 切换

- tool应该支持在ui上配置参数
  - tool级别的prompt
  - stable-diffusion文生图的工具应该支持配置steps/选择不同效果的模型

- 自动清理
  - 此类工具的runtime/模型文件会占用大量磁盘空间, 需要提供方便管理空间的工具

- 支持通过ui快速在提示词末尾添加`/non_think`的开关
# ui/server
- llm-ui/wrapper
  - janai(llama.cpp)
  - klee(ollama)

- llm-ui/client
  - 可参考 ollama/lmstudio/janai 封装 llama.cpp/mlx-lm/vlm 的逻辑
  - 还可参考LocalAi封装ollama/comfyui的逻辑
  - 类似lmstudio的模型市场, 但支持modelscope, 同时自动扫描本地已有的ollama/lmstudio模型
  - 用户自己上传的pdf，就类似词典软件的词库
  - llama.cpp ui + mlx/vllm
  - huggingface-cli, 下载模型优先搜索modelscope
- 🏘️ 参考主流厂商 coding-agent-cli 的实现, 有第三方在cli上实现web/electron/tauri, 如aionui
  - 采用aionui封装cc/gemini-cli的思路来封装llama.cpp/mlx
  - 同时需要支持 openai-compatible api, 这样方便低性能的电脑/客户端使用

- 针对mlx优化的版本，主要是后端多模型及切换模型的优化
  - 主要开发前端，是否有必要做后端?
  - 可参考 jan.ai

- model-api作为产品的非主要特性时, 没必要对标lm-studio/ollama将api暴露出去
  - 参考cline/roocode/librechat支持配置与切换agent即可
# ollama-xp

```sh
# ollama原始的版本是并不兼容 OpenAI 格式的请求
curl http://localhost:11434/api/chat -d '{
  "model": "gemma3:4b",
  "messages": [
    { "role": "user", "content": "why is the sky blue?" }
  ]
}'
# 模型响应输出如下 
{"model":"gemma3:4b","created_at":"2025-07-31T16:54:00.804772Z","message":{"role":"assistant","content":"That"},"done":false}

```

# llama.cpp/ollama/lmstudio 🔧🤔
- 用不同lm工具链(llama.cpp/mlx-lm/mlx-vlm)处理不同模型文件(gguf/mlx)的逻辑
  - 可参考vscode用不同编辑器打开不同文件的逻辑
  - 还可参考LocalAi封装多种cli
  - 还可参考文件管理器的逻辑

- 工具链功能
  - model management: Ollama(支持api), 直接import文件
  - frontend: openwebui, librechat
  - backend/api: Koboldcpp(包括fe)
  - all-in-one: lmstudio, janai

- ollama-pros
  - ollama实现的api对openai api的兼容性更好，如支持parse

- ollama-cons
  - mac上模型运行时占用内存很大，4b模型都会占满32gb内存
  - 不支持mlx

- lmstudio-pros
  - 模型运行时占用内存比ollama小很多
  - 对mlx的支持比较完善，而ollama还不支持
  - 使用本地小模型时，tool call成功率lmstudio比ollama感觉更高

- lmstudio-cons
  - 可以单独更新mlx-engine, 但不可以单独更新llama.cpp
  - prompt-processing的速度比ollama慢很多, 其实ollama速度也不快

- 自定义模型工具链的优点
  - 后台运行llm、自动切换llm、加入task queue及异常恢复 都需要自定义工具链的支持
  - 针对硬件自动选择合适参数
  - 支持针对模型添加自定义启动参数
  - 定制切换模型、模型保留缓存的逻辑，避免每次都重新加载模型
  - 自定义模型路由，类似openrouter, 根据体积/cost自动选择模型
  - 能优化软件占用的内存, lmstudio的内存占用很少, janai价值qwen3-4b模型gguf占用内存上10GB
  - 针对多gpu进行优化
  - 针对apple设备进行优化
  - 支持用户替换最新的llamacpp来测试最新模型

- ollama/lmstudio封装了llama.cpp, janai fork了llama.cpp

- 支持使用已有model文件.safetensors的工具包括
  - janai, 通过llama.cpp方式的provider
  - Oobabooga

- ai-chat的客户端封装可参考
  - janai, ollama-ui
  - gradio: Oobabooga, sd-webui

- llama.cpp的封装可参考
  - janai, Oobabooga

- gui封装后端逻辑的参考
  - comfyui, invokeai, aionui

- local-model-features

- lmstudio for image generation

- 
- 
- 
- 

# gpustack
- features
  - OpenAI-Compatible APIs: Fully compatible with OpenAI’s API specifications for seamless integration.
  - Broad GPU Compatibility: Seamlessly supports GPUs from various vendors across Apple Macs, Windows PCs, and Linux servers.
  - Supports a wide range of models including LLMs, VLMs, image models, audio models, embedding models, and rerank models.
  - Flexible Inference Backends: Flexibly integrates with multiple inference backends including vLLM, Ascend MindIE, llama-box (llama.cpp & stable-diffusion.cpp) and vox-box.
  - Multi-Version Backend Support: Run multiple versions of inference backends concurrently to meet the diverse runtime requirements of different models.
  - Distributed Inference: Supports single-node and multi-node multi-GPU inference
  - Scalable GPU Architecture: Easily scale up by adding more GPUs or nodes to your infrastructure.
  - Robust Model Stability: Ensures high availability with automatic failure recovery, multi-instance redundancy
  - Intelligent Deployment Evaluation: Automatically assess model resource requirements, backend and architecture compatibility, OS compatibility, and other deployment-related factors.
  - Automated Scheduling: Dynamically allocate models based on available resources.
  - Lightweight Python Package: Minimal dependencies and low operational overhead.
  - User & API Key Management: Simplified management of users and API keys.
  - Real-Time GPU Monitoring: Track GPU performance and utilization in real time.
  - Token and Rate Metrics: Monitor token usage and API request rates.
  - Supported Platforms: Linux macOS Windows
  - Supported Accelerators: nvidia cuda, apple metal, AMD ROCm, Ascend CANN, Moore Threads MUSA
  - GPUStack uses vLLM, Ascend MindIE, llama-box (bundled llama.cpp and stable-diffusion.cpp server) and vox-box as the backends and supports a wide range of models.

- 
- 
- 
- 
- 
- 
- 
- 
- 
- 

## docs-gpustack

- [Architecture](https://docs.gpustack.ai/0.7/architecture/)
- GPUStack server
  - API Server: Provides a RESTful interface for clients to interact with the system. It handles authentication and authorization.
  - Scheduler: Responsible for assigning model instances to workers.
  - Model Controller: Manages the rollout and scaling of model instances to match the desired model replicas.
  - HTTP Proxy: Routes inference API requests to workers.
  - 🛢️ uses `SQLite` by default, but you can configure it to use an external PostgreSQL or MySQL as well.
- GPUStack worker
  - Running inference servers for model instances assigned to the worker.
  - Reporting status to the server.
  - Routes inference API requests to backend inference servers.
- Inference Server
  - the backends that performs the inference tasks. GPUStack supports vLLM, Ascend MindIE, llama-box and vox-box as the inference server.
- RPC Server
  - enables running llama-box backend on a remote host. The Inference Server communicates with one or several instances of RPC server, offloading computations to these remote hosts. This setup allows for distributed LLM inference across multiple workers, enabling the system to load larger models even when individual resources are limited.
- Ray Head/Worker
  - Ray is a distributed computing framework that GPUStack utilizes to run distributed vLLM. Users can enable a Ray cluster in GPUStack to run vLLM across multiple workers. 
  - By default, it is disabled.

- 
- 
- 
- 
- 

# more
