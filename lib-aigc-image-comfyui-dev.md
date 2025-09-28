---
title: lib-aigc-image-comfyui-dev
tags: [comfyui, stable-diffusion]
created: 2025-09-25T16:23:55.593Z
modified: 2025-09-25T16:24:05.355Z
---

# lib-aigc-image-comfyui-dev

# guide
- pros-comfyui
  - easy ui to start image-gen
  - 可扩展: custom-node support
  - 对最新模型的支持很快
  - 对各种硬件的支持较好，包括nvidia/amd/cpu
  - 支持 sub-graph
  - 支持 flow control，如conditional
  - 提供了ui和api
  - 架构上支持extension: 内置了manager，支持custom_nodes
  - 提供扩展，支持批量出图，如XYPlot
  - 社区活跃，支持gguf

- cons-comfyui
  - license: GPLv3
  - 一些复杂的workflow难以理解和维护
  - 对于嵌入式文生图/改图的场景，comfyui的工作流图不如invokeAI的canvas易用

- who is using #comfyui
  - jaaz, comflowy
  - SwarmUI: 支持comfyui/sd-webui
  - ClaraVerse

- pros-InvokeAI 📌
  - license: apache2
  - canvas ux like photoshop
  - inpaint by layers
  - 能观察到图像从噪音点到目标图的绘制过程
  - 支持使用已有的models/lora, 但很多无法导入
  - 架构上支持extension: 支持custom_nodes
  - 支持desktop和web模式，但api未对外部使用做优化

- cons-InvokeAI
  - features slow
  - 对部分model/lora/vae/controlNet的支持很差, 对新模型支持很慢
  - RAM内存(非VRAM)占用很大，比comfyui大得多
  - workflow和教程示例太少
  - ~~models/safetensors auto converted to diffusers > duplicated~~
    - v4.2.6开始支持 Checkpoint models work without conversion to diffusers

- pros-diffusers 📌
  - flexible internals: pytorch, flax
  - comfyui loader 部分支持
  - 支持flux/qwen/wan
  - Hybrid Inference: VAE Encode/Decode, TextEncoders

- cons-diffusers
  - diffusers在未调优的条件下结果不如comfyui，因为comfyui内置了很多参数/prompt
  - comfyui-custom_nodes 移植到 diffusers 需要手动设置参数和转换

- who is using #diffusers
  - SDNext
  - InvokeAI

- comfyui
  - ⛓️ workflow的业务场景可参考n8n
  - comfyui的工作流ux对用户不友好，InvokeAI的canvas更易用、易嵌入
  - 👷: ComfyUI was never based on diffusers. It's a horrible library but I can't hate it that much because it's so bad that it's responsible for prematurely killing a lot of comfyui competition by catfishing poor devs into using it.

- stable-diffusion
  - 相对于传统PS软件的优点: upscale还原度高，速度快

- openrouter for image
  - 图像模型的配置比文本llm更复杂，不同场景所需的模型和配置都不同
  - 难点是sd系列模型相关的clip/encoder/vae种类繁多，不如直接用comfyui-api
  - image-gen的逻辑还需要考虑 VLM 生成图片描述prompt所采用的模型，过于灵活

- tips
  - 随着文本大模型能力的增强，prompt自动生成、memory管理基于coding实现更灵活，comfyui支持的能力有限
  - 在线图片生成或编辑的架构, 涉及到model/lora/vae/encoder的下载与组合，目前没有类似ollama的统一方案, 还涉及到GPU/CPU硬件支持，只有成熟方案才处理过相关问题
  - 下载模型文件后不要rename，方便与第三方包管理共享，方便与云端服务商的模型共享名称
# draft
- roadmap
  - docs-editor  + image-gen
  - image-editor + image-gen

- google-photos-like + google-drive + preview workflow

- 需要一个类似openrouter/groq的api能支持多个服务生成image, 需要同时支持 sd-webui和comfyui
  - 可参考aisdk来实现

- lmstudio-mlx for stable-diffusion

- booklet 画册
  - 红楼梦

- mobile-comfy
# dev-xp
- roadmap
  - workflow as app: 实现思路包括独立fullstack, custom_node-api, custom_node-ui, gradio
  - vscode-comfy
  - ⛓️ workflow的业务场景可参考n8n
  - 针对ppt优化的图片生成, 如自动添加目录编号/水印/调整大小
  - models: 学习图标库/logo库的模型
- usecase
  - upscale, anime, faceswap, bg-remove, ocr, ...
- extension-manager: batch enable/disable

## comfyui-devops

- build comfyui from source
  - [Adding UV installation instructionsUI](https://github.com/comfyanonymous/ComfyUI/pull/6349)

```sh
uv add --requirements requirements.txt

cp extra_model_paths.yaml.example extra_model_paths.yaml

uv run python main.py
```

# InvokeAI
- 🛢️ Invoke uses a SQLite database to store image, workflow, model, and execution data.
  - 软件元数据在 invokeRoot/databases/invokeai.db
  - 生成的图片在 invokeRoot/outputs/images
- [Inpainting: How do I remove an element from an existing image? : Invoke Support Portal](https://support.invoke.ai/support/solutions/articles/151000201404)
  - 尝试根据教程移除草地上的鸟，当 Denoising Strength 设为0.5时没效果，设为0.9时才移除
# more
