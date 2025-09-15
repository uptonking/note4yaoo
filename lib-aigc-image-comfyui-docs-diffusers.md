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
# dev-xp

## draft

- 需要一个类似openrouter/groq的api能支持多个服务生成image, 需要同时支持 sd-webui和comfyui
  - 可参考aisdk来实现

## comfyui

- build comfyui from source
  - [Adding UV installation instructionsUI](https://github.com/comfyanonymous/ComfyUI/pull/6349)

```sh
uv add --requirements requirements.txt

cp extra_model_paths.yaml.example extra_model_paths.yaml

uv run python main.py
```

### draft-comfy

- roadmap
  - workflow as app: 实现思路包括独立fullstack, custom_node-api, custom_node-ui, gradio
  - vscode-comfy
  - ⛓️ workflow的业务场景可参考n8n
  - 针对ppt优化的图片生成, 如自动添加目录编号/水印/调整大小
  - models: 学习图标库/logo库的模型
- usecase
  - upscale, anime, faceswap, bg-remove, ocr, ...
- extension-manager: batch enable/disable

## InvokeAI

- 🛢️ Invoke uses a SQLite database to store image, workflow, model, and execution data.
  - 软件元数据在 invokeRoot/databases/invokeai.db
  - 生成的图片在 invokeRoot/outputs/images
- [Inpainting: How do I remove an element from an existing image? : Invoke Support Portal](https://support.invoke.ai/support/solutions/articles/151000201404)
  - 尝试根据教程移除草地上的鸟，当 Denoising Strength 设为0.5时没效果，设为0.9时才移除
# docs-sd-webui

- 
- 
- 
- 

## api-webui

- [API · AUTOMATIC1111/stable-diffusion-webui Wiki](https://github.com/AUTOMATIC1111/stable-diffusion-webui/wiki/API)
  - [Stable Diffusion web UI txt2img img2img api example python script](https://gist.github.com/w-e-w/0f37c04c18e14e4ee1482df5c4eb9f53)
- /sdapi/v1/txt2img
  - 

- request POST
  - `override_settings`: The purpose of this parameter is to override the webui settings such as model or CLIP skip for a single request.
  - `sdapi/v1/options`: different from override_settings because this change will persist

```JSON
{
  "prompt": "",
  "negative_prompt": "",
  "styles": [
    "string"
  ],
  "seed": -1,
  "subseed": -1,
  "subseed_strength": 0,
  "seed_resize_from_h": -1,
  "seed_resize_from_w": -1,
  "sampler_name": "string",
  "scheduler": "string",
  "batch_size": 1,
  "n_iter": 1,
  "steps": 50,
  "cfg_scale": 7,
  "width": 512,
  "height": 512,
  "restore_faces": true,
  "tiling": true,
  "do_not_save_samples": false,
  "do_not_save_grid": false,
  "eta": 0,
  "denoising_strength": 0,
  "s_min_uncond": 0,
  "s_churn": 0,
  "s_tmax": 0,
  "s_tmin": 0,
  "s_noise": 0,
  "override_settings": {},
  "override_settings_restore_afterwards": true,
  "refiner_checkpoint": "string",
  "refiner_switch_at": 0,
  "disable_extra_networks": false,
  "firstpass_image": "string",
  "comments": {},
  "enable_hr": false,
  "firstphase_width": 0,
  "firstphase_height": 0,
  "hr_scale": 2,
  "hr_upscaler": "string",
  "hr_second_pass_steps": 0,
  "hr_resize_x": 0,
  "hr_resize_y": 0,
  "hr_checkpoint_name": "string",
  "hr_sampler_name": "string",
  "hr_scheduler": "string",
  "hr_prompt": "",
  "hr_negative_prompt": "",
  "hr_cfg": 1,
  "force_task_id": "string",
  "sampler_index": "Euler",
  "script_name": "string",
  "script_args": [],
  "send_images": true,
  "save_images": false,
  "alwayson_scripts": {},
  "infotext": "string"
}
```

- response-200-Successful
  - `images` is a list of base64-encoded generated images.

```JSON
{
  "images": [
    "string"
  ],
  "parameters": {},
  "info": "string"
}
```

- response-422-Validation Error

```JSON
{
  "detail": [
    {
      "loc": [
        "string",
        0
      ],
      "msg": "string",
      "type": "string"
    }
  ]
}
```

- 
- 
- 
- 

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

# docs-concepts
- [IPAdapter · vladmandic/sdnext Wiki](https://github.com/vladmandic/sdnext/wiki/IPAdapter)
  - IP-Adapter is a tool designed for style transfer with minimal resource usage. It provides an efficient way to clone faces or apply image transformations.
  - Low Resource Usage: The IP-Adapter is lightweight, with memory requirements under 100MB for SD 1.5 and 700MB for SD-XL, making it an efficient choice for style transfer tasks.
  - Style Transfer: It offers powerful style transfer capabilities, allowing you to clone faces or apply various image styles.
  - Integration with ControlNet: IP-Adapter can be combined with ControlNet for more stable results, especially useful for batch processing or video tasks.
- 
- 
- 
- 
- 
- 
- 
- 

# more
- [Hosting a ComfyUI Workflow via API - 9elements _202402](https://9elements.com/blog/hosting-a-comfyui-workflow-via-api/)
