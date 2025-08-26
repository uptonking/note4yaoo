---
title: lib-aigc-image-comfyui-docs-diffusers
tags: [comfyui, diffusers, docs, image]
created: 2025-08-23T06:42:00.128Z
modified: 2025-08-23T11:42:50.170Z
---

# lib-aigc-image-comfyui-docs-diffusers

# guide

- pros-comfyui 📌
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
  - comfyui-custom-node 移植到 diffusers 需要手动设置参数和转换

- who is using #diffusers
  - SDNext
  - InvokeAI

- stable-diffusion
  - 相对于传统PS软件的优点: upscale还原度高，速度快

- openrouter for image
  - 图像模型的配置比文本llm更复杂，场景更多样
  - 难点是sd系列模型相关的clip/encoder/vae种类繁多，不如直接用comfyui-api

- tips
  - 随着文本大模型能力的增强，prompt自动生成、memory管理基于coding实现更灵活，comfyui支持的能力有限
  - 在线图片生成或编辑的架构, 涉及到模型下载与扩展下载，目前没有类似ollama的统一方案, 还涉及到GPU/CPU硬件支持，只有成熟方案才处理过相关问题
  - 👷: ComfyUI was never based on diffusers. It's a horrible library but I can't hate it that much because it's so bad that it's responsible for prematurely killing a lot of comfyui competition by catfishing poor devs into using it.
# dev-xp

## comfyui

## InvokeAI

- 🛢️ Invoke uses a SQLite database to store image, workflow, model, and execution data.
  - 软件元数据在 invokeRoot/databases/invokeai.db
  - 生成的图片在 invokeRoot/outputs/images

- [Inpainting: How do I remove an element from an existing image? : Invoke Support Portal](https://support.invoke.ai/support/solutions/articles/151000201404)
  - 尝试根据教程移除草地上的鸟，当 Denoising Strength 设为0.5时没效果，设为0.9时才移除
# docs-diffusers
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

# docs-InvokeAI
- When you start working on a blank Canvas, your first image generation will be added as a Raster Layer

- Layers are a powerful set of tools enabling you to control and guide the image generation process to produce a desired outcome.

- Regional Reference Image layers use Image Prompt (IP) Adapters to inspire a new image with the content of an input image. You can use add Regional Reference Images as layers on the ‘Layers’ tab.

- Inpaint Mask layer allows you to specify a region that will be modified for generation, while preserving the rest of your raster layer data.
  - The Denoising Strength that you select will dictate how much change you want the AI model to generate in the selected region. At very high denoising strengths, the newly generated content will be very different from your original image, and at low denoising strengths, it will only make minor changes.

- Regional Guidance layers allow you more fine-tuned control over the prompt information used to guide the generation process. 

- Control Layers can provide structural control over the output of your image generations, with a number of different ways to instruct the system using visual representations like sketches, edge maps, and depth renderings.

- A Raster Layer is the image content of your canvas, similar to other Image Editing solutions. 
  - When included in your bounding box, these images serve as the base image content to start your creative process
  - This layer allows you to inspire the generation process with an initial drawing or image, which preserves the original image's rough structure, colors, and layout, while using AI to reimagine new content with your input prompt based on your denoising strength.

- Inpainting, in the context of image generation, is a process where we try to fill in parts of an image with new or modified content.
  - inpainting methods use the available information in an image (such as edges, textures, colors) to predict what the incomplete areas should look like, and then uses the selected model to regenerate that portion of the image

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

# more
