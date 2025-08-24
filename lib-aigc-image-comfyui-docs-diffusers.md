---
title: lib-aigc-image-comfyui-docs-diffusers
tags: [comfyui, diffusers, docs, image]
created: 2025-08-23T06:42:00.128Z
modified: 2025-08-23T11:42:50.170Z
---

# lib-aigc-image-comfyui-docs-diffusers

# guide

- pros-comfyui
  - easy ui to start image-gen
  - 可扩展: custom-node support
  - 对最新模型的支持很快
  - 支持 sub-graph
  - 支持flow control，如conditional
  - 提供了ui和api

- cons-comfyui
  - license: GPLv3
  - 一些复杂的workflow难以理解和维护

- comfyui-wrapper
  - SwarmUI
  - ClaraVerse

- pros-diffusers
  - flexible internals: pytorch, flax
  - comfyui loader 部分支持
  - 支持flux/qwen/wan
  - Hybrid Inference: VAE Encode/Decode, TextEncoders

- cons-diffusers
  - diffusers在未调优的条件下结果不如comfyui，因为comfyui内置了很多参数/prompt
  - comfyui-custom-node 移植到 diffusers 需要手动设置参数和转换

- who is using #diffusers
  - SDNext
  - InvokeAI

- tips
  - 随着文本大模型能力的增强，prompt自动生成、memory管理基于coding实现更灵活，comfyui支持的能力有限
  - 在线图片生成或编辑的架构, 涉及到模型下载与扩展下载，目前没有类似ollama的统一方案, 还涉及到GPU/CPU硬件支持，只有成熟方案才处理过相关问题
  - 👷: ComfyUI was never based on diffusers. It's a horrible library but I can't hate it that much because it's so bad that it's responsible for prematurely killing a lot of comfyui competition by catfishing poor devs into using it.
# overview
- A diffusion model combines multiple components to generate outputs in any modality based on an input, such as a text description, image or both.

- For a standard text-to-image model:
  - A text encoder turns a prompt into embeddings that guide the denoising process. Some models have more than one text encoder.
  - A scheduler contains the algorithmic specifics for gradually denoising initial random noise into clean outputs. Different schedulers affect generation speed and quality.
  - A UNet or diffusion transformer (DiT) is the workhorse of a diffusion model. At each step, it performs the denoising predictions, such as how much noise to remove or the general direction in which to steer the noise to generate better quality outputs. The UNet or DiT repeats this loop for a set amount of steps to generate the final output.
  - A variational autoencoder (VAE) encodes and decodes pixels to a spatially compressed latent-space. Latents are compressed representations of an image and are more efficient to work with. The UNet or DiT operates on latents, and the clean latents at the end are decoded back into images.

- The `DiffusionPipeline` packages all these components into a single class for inference.

- Adapters insert a small number of trainable parameters to the original base model. 
  - Only the inserted parameters are fine-tuned while the rest of the model weights remain frozen. This makes it fast and cheap to fine-tune a model on a new style. 
  - Among adapters, LoRA’s are the most popular.

- Quantization stores data in fewer bits to reduce memory usage. It may also speed up inference because it takes less time to perform calculations with fewer bits.

- 
- 
- 
- 
- 
- 

# docs

- 
- 
- 
- 

# more
