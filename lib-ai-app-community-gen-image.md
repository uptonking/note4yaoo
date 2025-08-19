---
title: lib-ai-app-community-gen-image
tags: [ai, community, image, large-language-model]
created: 2025-08-16T14:11:47.076Z
modified: 2025-08-16T14:12:24.416Z
---

# lib-ai-app-community-gen-image

# guide

- tips
  - sd的包管理器如StabilityMatrix会移动models/lora等文件， 导致已有的workflow不工作，可考虑只用来管理视频而不管理图片相关模型

- image-gen-xp
  - 模型参数: models/checkpoints, clip/text-encoder, vae, sampler, ...
  - sd 模型: sd-v1.5(+ hyper-lora), sdxl-lightning, segmind-ssb/vega, ...
  - hot模型: flux, qwen, ...
  - 模型尝试: lumina, omnigen, sonic-风格迁移(如对口型), ACE-audio, ...
  - 💡 直接搜索 comfyui + 模型名, 找资源更准; 还可用github搜索code找模型名如 `"SSD-1B.safetensors" language:JSON`

- fans-stable-diffusion
  - [深入浅出完整解析Stable Diffusion（SD）核心基础知识 - 知乎](https://zhuanlan.zhihu.com/p/632809634)

- resources
  - [【轻科普】StableDiffusion那些事儿，关于LoRA、DreamBooth、模型分层融合等](https://www.bilibili.com/video/BV1RT411D7h7/)
  - [【SD + ComfyUI】合集 - 知乎](https://zhuanlan.zhihu.com/c_1625633809227010048)

- ai-image-examples
  - https://openart.ai/workflows/home
  - https://civitai.com/
# models-benchmark
- time cost for image-gen on macbook air m4(32gRAM)
  - prompts: lawn, rabbit, cat

```markdown
- model,                       1st/s,  2nd/s, size/gb, license, year,  notes
- 🌹sdxs-512-dreamshaper/1step,6.1,    2.4,   1.26,     202403, sd15
- 🌹sdxl-segmind-vega/2step,   12,     3.6,   3.29,     202401, sdxl
- sdxl-lightning/1step,        18,     3.8,   6.94,     20240x, sdxl
- sdxl-hyper/1step,            20,     4.2,   6.94,     20240x, sdxl
- sd15/hyper-lora/1step,       12,     4.2,   2.13,     202404, sd15
- sd15/lcm/2step,              22,     5.3,   2.13,     202404, sd15
- sdxl-lightning/2step,        30,     6.2,   6.94,     20240x, sdxl/小于768过于卡通风
- 🌹sdxl-hyper/4step,          29,     9,     6.94,     20240x, sdxl/小于768过于卡通风
- sdxl-turbo/4step,            33,     9,     6.94,     20240x, sdxl/小于768输出正常
- sdxl-dmd2/4step,             27,     9,     6.94,     20240x, sdxl/过于卡通风,质量差
- sdxl-lightning/4step,        27,     11,    6.94,     20240x, sdxl/小于768过于卡通风
- qwen/4step,                  250,    219,   7.06+3,   202404, qwen2.5-vl-7b
- lumina/6step,                134,    127,   1.79+5,   202404, gemma2-2b
- omnigen2/4step,              147,    123,   5.98+3,   202404, qwen-2.5-vl-3b
- 🌹flux-miniQ3KS/8step,       90,     80,    5.21,     202404, 3.2b-MMDiT
- 🌹fluxQ4KM-hyper/8step,      260,    220,   5.21,     202404, hypersd
- fluxQ3KS-gguf/8step,         350,    320,   5.21,     202404, model
- flux-gguf-hyper/8step,       760,    770,   5.21+1,   202404, model
- flux-gguf-turbo/8step,       760,    760,   5.21+0.6, 202404, model

```

- 
- 
- 

# docs-image-gen
- 🧩 Text to Image is a fundamental process in AI art generation that creates images from text descriptions, with diffusion models at its core.
  - This text-to-image generation process can be simply understood as telling your requirements (positive and negative prompts) to an artist (the image model), who then creates what you want on the latent space(as canvas)

- 🧩 Image to Image is a workflow in ComfyUI that allows users to input an image and generate a new image based on it.
  - Image to Image process is very similar to Text to Image, just with an additional input reference image as a condition.
  - we let the artist create based on both our reference image and prompts.
  - Note that in ComfyUI txt2img and img2img are the same node. Txt2Img is achieved by passing an empty image to the sampler node with maximum denoise.

- 🧩 Inpaint/局部重绘
  - In AI image generation, we often encounter situations where we’re satisfied with the overall image but there are elements we don’t want or that contain errors. 
  - Simply regenerating might produce a completely different image, so using inpainting to fix specific parts becomes very useful.
  - We need to tell the artist which areas to adjust (mask), and then let them repaint (inpaint) according to our requirements.

- 🧩 Outpaint/图像扩展
  - In AI image generation, we often encounter situations where an existing image has good composition but the canvas area is too small, requiring us to extend the canvas to get a larger scene. This is where outpainting comes in.
  - it requires similar content to Inpainting, but we use different nodes to build the mask.

- 🧩 Upscale
  - Image Upscaling is the process of converting low-resolution images to high-resolution using algorithms. 
  - Unlike traditional interpolation methods, AI upscaling models (like ESRGAN) can intelligently reconstruct details while maintaining image quality.
  - SD1.5 model often struggles with large-size image generation. To achieve high-resolution results, we typically generate smaller images first and then use upscaling techniques.
  - 🧩 Hires(aka. high resolution) fix is just creating an image at a lower resolution, upscaling it and then sending it through img2img. Note that in ComfyUI txt2img and img2img are the same node. Txt2Img is achieved by passing an empty image to the sampler node with maximum denoise.

- 🧩 LoRA
  - LoRA (Low-Rank Adaptation) is an efficient technique for fine-tuning large generative models
  - It introduces trainable low-rank matrices to the pre-trained model, adjusting only a portion of parameters rather than retraining the entire model, thus achieving optimization for specific tasks at a lower computational cost. 
  - by using a LoRA model, we can generate images in different styles without adjusting the base model.

- 🧩 ControlNet
  - ControlNet is a conditional control generation model based on diffusion models, first proposed by Lvmin Zhang et al. in 2023 in the paper Adding Conditional Control to Text-to-Image Diffusion Models.
  - ControlNet models significantly enhance the controllability of image generation and the ability to reproduce details **by introducing multimodal input conditions, such as edge detection maps, depth maps, and pose keypoints**.
  - Before ControlNet, we could only rely on the model to generate images repeatedly until we were satisfied with the results, which involved a lot of randomness.
  - With the advent of ControlNet, we can control image generation by introducing additional conditions. For example, we can use a simple sketch to guide the image generation process, producing images that closely align with our sketch.

- 👾 Flux is one of the largest open-source text-to-image generation models, with 12B parameters and an original file size of approximately 23GB.
  - It was developed by Black Forest Labs, a team founded by former Stable Diffusion team members. 
  - Flux is known for its excellent image quality and flexibility, capable of generating high-quality, diverse images.
  - Hybrid Architecture: Combines the advantages of Transformer networks and diffusion models
  - Supports Multiple Styles

- 👾 Qwen-Image
  - It’s a 20B parameter MMDiT (Multimodal Diffusion Transformer) model open-sourced under the Apache 2.0
  - The model has made significant advances in complex text rendering and precise image editing, achieving high-fidelity output for multiple languages including English and Chinese.
  - Excellent Multilingual Text Rendering: Supports high-precision text generation in multiple languages including English, Chinese, Korean, Japanese, maintaining font details and layout consistency
  - Diverse Artistic Styles: From photorealistic scenes to impressionist paintings, from anime aesthetics to minimalist design, fluidly adapting to various creative prompts

- 👾 HiDream-I1 is a text-to-image model officially open-sourced by HiDream-ai on April 7, 2025. The model has 17B parameters and is released under MIT
  - Hybrid Architecture Design: A combination of Diffusion Transformer (DiT) and Mixture of Experts (MoE) architecture
  - Multimodal Text Encoder Integration

- 👾 OmniGen2 is a powerful and efficient unified multimodal generation model with approximately 7B total parameters (3B text model + 4B image generation model).
  - Unlike OmniGen v1, OmniGen2 adopts an innovative dual-path Transformer architecture with completely independent text autoregressive model and image diffusion model, achieving parameter decoupling and specialized optimization.
  - Dual-path Architecture: Based on Qwen 2.5 VL (3B) text encoder + independent diffusion Transformer (4B)
  - Parameter Decoupling Design: Avoids negative impact of text generation on image quality
  - Omni-RoPE Position Encoding: Supports multi-image spatial positioning and identity distinction
  - Visual Understanding: Inherits the powerful image content interpretation and analysis capabilities of the Qwen-VL-2.5 foundation model
  - Text-to-Image Generation
  - Image Editing: Performs complex, instruction-based image modifications, achieving state-of-the-art performance 
  - Contextual Generation: Versatile capabilities to process and flexibly combine diverse inputs (including people, reference objects, and scenes), producing novel and coherent visual outputs
  - Excellent detail preservation capabilities
  - Unified architecture supporting multiple image generation tasks

- 
- 
- 
- 
- 
- 
- 
- 
- 

# discuss-stars
- ## 

- ## 

- ## 

- ## 🆚 [Any alternatives to Automatic1111 or ComfyUI that DON'T Use Python : r/StableDiffusion _202502](https://www.reddit.com/r/StableDiffusion/comments/1ivpbno/any_alternatives_to_automatic1111_or_comfyui_that/)
  - Python is such a pain in a$$ with its dependency hell, requiring specific versions of everything. The slightest thing can break it.
  - Is there an alternative sort of like llamma.cpp but for images?

- The entire ML ecosystem is basically based on pytorch, so you're gonna need python. No real way around it.
- All of the ML people collectively decided to use package hell with Python so I think you are out of luck.

- A real hero would be some company building a PyTorch alternative in C so we can make bindings in any language.
  - Actually, PyTorch is built upon Torch, which was a machine learning library originally written in C and Lua. Currently, PyTorch's internal engine is C/C++, and the project itself provides its own C++ interface, which I believe is called LibTorch.

- I found at least a couple like Koboldcpp and stable-diffusion.cpp. Koboldcpp probably being the closest.
  - I use ComfyUI if I need to do something complicated but sometimes I just want to get up and running quickly without worrying about the latest python shenanigans.

- I just use a dedicated venv for each app. For comfy and automatic it's really not so bad.

- You might like Stability Matrix then. Oneclick installers for most popular tools
  - But it uses incomplete python and thats why triton will not work on it

- A1111 is really bad at memory management.. models get stuck in VRAM and using other features like upscale get way too slow until you restart.. on my 1080 8gb 
  - Forge is 5 times faster. ComfyUI is 30% slower than Forge.

- make sure your dependencies run inside a venv and most of those issues go away.

- ## [Stable Diffusion experts: Are you more focussed on getting good images in one step, or are you creating a base image and then inpainting? : r/StableDiffusion _202303](https://www.reddit.com/r/StableDiffusion/comments/11whzuf/stable_diffusion_experts_are_you_more_focussed_on/)
- It depends on what you’re trying to do. 
  - I need a fun quick image for a presentation? One step. 
  - I want a very specific recipe image at high resolution, with specific colors? Multiple steps with multiple programs.

- Never got a great image in one go. Always inpaint and rough color guides in photoshop.

- I 'ALWAYS' inpaint faces after upscaling.

- I usually want the best image possible on the initial text to image generation; then maybe inpaint pre-upscale if its something major; then upscale to inpaint small details for a final image

- As few steps as possible. Ideally it’s one generation plus an upscale. Things break when sd doesn’t have the full freedom to draw a completely new image on a blank canvas, even more so when you’re not using the base models preferred dimensions (512 etc)
# discuss-comfyui/sd ⛓️🖼️
- https://github.com/nerdyrodent/AVeryComfyNerd
  - A variety of ComfyUI related workflows
  - https://github.com/nerdyrodent/AVeryComfyNerd/blob/main/workflows/SDXL/SSD1B-SDXL-8GB.png
- https://github.com/replicate/cog-comfyui
  - Run ComfyUI workflows on Replicate, with an API
  - https://github.com/replicate/comfyui-replicate
    - Custom nodes for running Replicate models in ComfyUI.
- https://github.com/602387193c/ComfyUI-wiki
  - 分享最好用、最实用的ComfyUI工作流
- https://github.com/yjuddpl/Interesting-things
  - 空余时间给大家制作一些实用性的工作流
- workflows
  - https://github.com/602387193c/ComfyUI-wiki/tree/main/pysssss-workflows
  - https://github.com/aimpowerment/comfyui-workflows
  - https://github.com/Clinteastman/comfyui_workflows
  - https://github.com/Creepybits/ComfyUI-workflow
  - https://github.com/BennyKok/comfyui-deploy

- stable-diffusion
  - https://modelscope.cn/models/ByteDance/SDXL-Lightning/files
  - https://huggingface.co/ByteDance/SDXL-Lightning
  - [ComfyUI平台下应用字节SDXL-Lightning 模型 - 老E的博客 _202405](https://appscross.com/blog/using-sdxl-lightning-model-under-comfyui-platform.html)
  - [Hyper-SD · 模型库](https://modelscope.cn/models/ByteDance/Hyper-SD/summary)
  - [DMD2 Speed LoRA [SDXL, Pony, Illustrious] | Civitai](https://civitai.com/models/1608870/dmd2-speed-lora-sdxl-pony-illustrious)

- sd15
  - https://huggingface.co/segmind/tiny-sd /647mb/Realistic_Vision_V4.0
  - https://huggingface.co/segmind/small-sd /2.32gb/Realistic_Vision_V4.0/202304
  - https://huggingface.co/stablediffusionapi/realistic-vision-v51 /1.72gb

- sdxl
  - https://modelscope.cn/models/AI-ModelScope/stable-diffusion-xl-base-1.0/files /6.94gb
  - https://github.com/xingren23/ComfyUI-for-ComfyFlowApp /1step
  - https://huggingface.co/segmind/SSD-1B /4.47gb/202310
    - a distilled 50% smaller version of SDXL
  - https://huggingface.co/segmind/Segmind-Vega /3.29gb
    - a distilled version of SDXL,  70% reduction in size
  - https://huggingface.co/segmind/Segmind-VegaRT
    - adapter for Segmind-Vega that allows to reduce the number of inference steps to only between 2 - 8 steps.
  - [SDXL Turbo-LoRA-Stable Diffusion XL faster than light - v1-128dim | Stable Diffusion XL LoRA | Civitai](https://civitai.com/models/215485/sdxl-turbo-lora-stable-diffusion-xl-faster-than-light)
  - [SDXL DPO-Turbo-LoRA - v1.0 DPO XL TURBO | Stable Diffusion XL LoRA | Civitai](https://civitai.com/models/237775/sdxl-dpo-turbo-lora)

- sdxs
  - https://huggingface.co/IDKiro/sdxs-512-dreamshaper
  - https://huggingface.co/IDKiro/sdxs-512-0.9
  - [SDXS-1024 Release? · Issue · IDKiro/sdxs _202403](https://github.com/IDKiro/sdxs/issues/2)
    - 💰 The subsequent open source program has been terminated by the Company.
  - https://github.com/Zeqiang-Lai/OpenDMD
    - I just read this paper's figures, which has a one-step model training method that is closer to the idea of this paper
    - [SDXS-512-0.9 - New Base Model for April 2024 | Civitai](https://civitai.com/articles/4760)

- lumina 👾
  - https://modelscope.cn/models/calcuis/lumina-gguf/files

- omnigen 👾
  - https://huggingface.co/OmniGen2/OmniGen2/tree/main
  - https://huggingface.co/Shitao/OmniGen-v1/tree/main
  - https://modelscope.cn/models/calcuis/omnigen2-gguf/files
  - https://huggingface.co/calcuis/omnigen2-gguf
  - https://github.com/VectorSpaceLab/OmniGen2
  - 📌 [OmniGen2: Exploration to Advanced Multimodal Generation _202506](https://vectorspacelab.github.io/OmniGen2/)
    - a unified multimodal generation model that combines strong visual understanding, text-to-image synthesis, instruction-based image editing, and subject-driven in-context generation within a single framework.
  - 📌 [OmniGen: Unified Image Generation _202409](https://vectorspacelab.github.io/OmniGen/)
    - in the realm of image generation, a unified model capable of handling various tasks within a single framework remains largely unexplored.
    - Unlike popular diffusion models (e.g., Stable Diffusion), OmniGen no longer requires additional modules such as ControlNet or IP-Adapter to process diverse control conditions.
    - Unification. OmniGen not only demonstrates text-to-image generation capabilities but also inherently supports various downstream tasks, such as image editing, subject-driven generation, and visual-conditional generation. 
  - [Another Omnigen ComfyUI Workflow - v2.0 | Other Workflows | Civitai](https://civitai.com/models/916444/another-omnigen-comfyui-workflow)
  - [ComfyUI OmniGen2 Native Workflow Examples - ComfyUI](https://docs.comfy.org/tutorials/image/omnigen/omnigen2)
  - [ComfyUI OmniGen2 Native Workflow Examples - ComfyUI](https://docs.comfy.org/tutorials/image/omnigen/omnigen2)
    - OmniGen2 is a powerful and efficient unified multimodal generation model with approximately 7B total parameters (3B text model + 4B image generation model).
    - Unlike OmniGen v1, OmniGen2 adopts an innovative dual-path Transformer architecture with completely independent text autoregressive model and image diffusion model, achieving parameter decoupling and specialized optimization.
    - [Omnigen 2 | ComfyUI_examples](https://comfyanonymous.github.io/ComfyUI_examples/omnigen/)
  - 🌰
  - https://github.com/AIFSH/OmniGen-ComfyUI
  - https://github.com/1038lab/ComfyUI-OmniGen
  - [Basic Workflow for OmniGen : r/comfyui _202411](https://www.reddit.com/r/comfyui/comments/1ghogwb/basic_workflow_for_omnigen/)
  - [OmniGen nodes with progress, preview, better memory handling, faster load, etc. : r/comfyui _202411](https://www.reddit.com/r/comfyui/comments/1gy0ja2/omnigen_nodes_with_progress_preview_better_memory/)
    - I wanted to play with this model and found a lot of issues with other nodes. So I wrote my own nodes.

- ## 

- ## 

- ## 

- ## [ComfyUI standalone and Stability Matrix : r/StableDiffusion _202408](https://www.reddit.com/r/StableDiffusion/comments/1eidfbn/comfyui_standalone_and_stability_matrix/)
  - I wanted to ask if any of you have tested whether installing ComfyUI through Stability Matrix is slower than the standalone ComfyUI? 
- I have both. I go back and forth pretty much every day. Anecdotally I havn't noticed a performance difference. 
  - Custom Node packages are a different matter. They are not all created equally and can certainly cause major slowdowns. The one I was fighting with last week was the "Easy Nodes". Their Ksampler was adding at least 20 seconds to each generation for no good reason. You just gotta eyeball it and make the call.

- ## [Stability matrix. Impressions of a Novice. : r/StableDiffusion _202411](https://www.reddit.com/r/StableDiffusion/comments/1h1rxr3/stability_matrix_impressions_of_a_novice/)
- Most likely you couldnt get generation to work because you didnt install and connect comfyui. SM itself has no generation engine, its just a visual ui. You can also run packages installed via sm directly, like normal too

- I would never bother with it's built in "inference" that gives very little control

- ## [Do you know Stability matrix? : r/StableDiffusion _202502](https://www.reddit.com/r/StableDiffusion/comments/1im8wkj/do_you_know_stability_matrix/)
- I like it. It makes things simpler. But the downside is that it can limit what you can do. I've found a bunch of models that I could not use with it, but as a beginner, it is a godsend.
- I agree it can limit you on certain fronts, but what model couldn't you run because of stability matrix?
  - There's a few that I remember but the one that I never forget is PulId. My PC is a potato (3060-12gb), so I would never risk train a LORA. I've been scraping by using IPadapter (which I love) but I wold love to have something like it for flux.
  - I also tried to use F5-TTS which looks incredible and would have saved me quite some time a few weeks ago but no luck.
- Yeah I couldn't get F5-TTS to work on comfyui either, don't think it was a stability matrix issue-- Btw, you can change python versions and such through stability matrix's interface in your package section..

- ## 💡 [Stability Matrix : r/StableDiffusion _202506](https://www.reddit.com/r/StableDiffusion/comments/1l07xob/stability_matrix/)
  - My Models became quite large since I tried ComfyUI, Framepack in Pinokio, Swarm UI and others. Many of them want to get it's own Models etc.
- You can also use symlink, btw. I have one master model folder, and all of my different UIs refer to that folder for models.
- Yes, though you could've done it manually too. Stability Matrix uses symbolic links to share folders' contents with other UIs or the configs like yaml file in ComfyUI's case.
  - I manually moved the other Package Models using the Handy 'Folder reference' into the folder structure of Stability Matrix since they were in the same drive. Ran the 'Find Connected Metadata' on them. Nice that the models can be directly downloaded in it as well.

- It's great, I just wish they dropped the inference tab because every update that comes out 80% of the effort goes into that when most people uses the App for Package/Model management.

- ## [Stability Matrix for macOS Released! : r/StableDiffusion _202402](https://www.reddit.com/r/StableDiffusion/comments/1ajad6l/stability_matrix_for_macos_released/)
- Does this have up adapter and control net support?
  - Yes of course.  Or can install any model and any python package.

- ## 🚀📦 [Stability Matrix - One-click install and update for Stable Diffusion WebUIs (Automatic1111, ComfyUI, SD. Next), with shared checkpoint management and CivitAI import : r/StableDiffusion _202306](https://www.reddit.com/r/StableDiffusion/comments/14iuilo/stability_matrix_oneclick_install_and_update_for/)
  - We are introducing Stability Matrix - a free and open-source Desktop App to simplify installing and updating Stable Diffusion Web UIs.
  - The one-click install manages all package dependencies like Git and C redistributable frameworks and chooses optimal PyTorch / xformers packages based on your GPU and CUDA versions. 
  - There’s no need to install anything prior. If you already have Python installed, our embedded version won’t interact with that in any way.
  - Web UIs you install automatically share the same model directory, and you can find and download new model checkpoints with the in-app model browser, powered by CivitAI.
  - You can also import existing local model files by drag and drop. 

- I like the concept, unfortunately the inability to like, customize paths across multiple drives or move the project out of `C:\~\AppData\Roaming` is going to keep me from using it for now, for space reasons. 
  - You can choose a custom install location in the installer window currently, but the model directories are junctions stored in `AppData` under `StabilityMatrix/Models`. 
  - We're planning to make the model storage directory selectable 
  - Portable mode and custom data directory now in v1.1.2

- Will this make portable installs? 
  - At startup we unpack embedded Git and Python 3.10 to` AppData/Roaming/StabilityMatrix`, and the WebUI installs themselves will have a Python `venv` folder in the root directory.
  - It is self-contained in the sense that you just need your WebUI install folder + the StabilityMatrix app to run on any computer.

- Any plans to include extensions? In particular ControlNet is almost essential, but currently requires many additional steps, manual downloading GBs of models, putting them in the correct folder etc.
  - Definitely yeah, we have extensions management planned soon. Getting the ControlNet plugin working was pretty confusing to me at first as well, on top of not using the `models/ControlNet` directory as expected but instead the one in `extensions/sd-webui-controlnet/models`

- How to build this in Ubuntu?
  - Currently we're using WPF and other native windows frameworks, so it is only able to be built and run on Windows. 
  - But we have an alternate cross-platform version for Linux and MacOS on the roadmap.

- I have an existing master directory for models, and I cannot figure out the best way to install this. It won't let me use my master directory, which I want to keep, and if I manually import them to Stability, it makes copies of my giant repository.

- ## 🤔 [(ComfyUi) detail issues with DMD2 LoRa and Upscaling : r/StableDiffusion _202507](https://www.reddit.com/r/StableDiffusion/comments/1m2jxse/comfyui_detail_issues_with_dmd2_lora_and_upscaling/)
  - I'm stumbling over a problem I cannot fix by myself. Whenever I upscale an image with a DMD2 checkpoint I get decent-looking results, but as soon as I switch to a regular SDXL checkpoint with the DMD2-LoRa combined, all skin and image details are washed away. This happened with all my upscale testings.

- There was an article published recently by epinikion on Civitai explaining how to upscale images with the DMD2 LoRA. He suggests Euler Ancestral (aka Euler A) for more details and less plastic look. Have a look at this article. I think it might help you with this.
  - [Simple Upscale with DMD2 Lora (ForgeUI, A1111) | Civitai _202506](https://civitai.com/articles/15873/simple-upscale-with-dmd2-lora-forgeui-a1111)
  - This article was really helpful. And I was able to get good-looking results with epinikion's recommendations. Especially with Euler A + Karras. 
  - I think my basic problem was that I didn't link the KSampler - of the upscaling pass- to the LoRa-Loader-Model-Connector. It was linked with the Checkpoint-Loader-Model-Connector. So I guess, when using a SDXL-Model with the DMD2 LoRa, the DMD2 LoRa got ignored during upscaling.

- [detail issues with DMD2 LoRa and Upscaling : r/comfyui](https://www.reddit.com/r/comfyui/comments/1m1royd/detail_issues_with_dmd2_lora_and_upscaling/)
  - I would recommend you use a different scheduler, because exponential doesnt handle low steps that well. Or rather it doesnt provide any benefits and can be detrimental. Use it when you run it with 25-50 steps.
  - Additionally, low step LoRas generally work well with `sgm_uniform` as the scheduler.
  - If you want to use low step workflows I would recommend you look for 4-step Hyper models as there are far more of them. (Hyper-SD is available as a 4/8/12 step lora or model and even as a 1 step model)
- I also linked solid and fast sd1.5 and SDXL upscale workflows

- ## 🆚 [Sometimes I want to return to SDXL from FLUX : r/comfyui _202506](https://www.reddit.com/r/comfyui/comments/1l2ddep/sometimes_i_want_to_return_to_sdxl_from_flux/)
- Give the DMD2 4 step lora for XL(linked below) a try. I used the LCM sampler and the sgm_uniform scheduler with it. I set the steps to 4 and the CFG to 1.0. You can play with the CFG, 1 is my personal preference with this.
  - Now, since you have dropped the steps down to 4, you can chain another ksampler in the workflow(with the denoise set to 0.2) and this will add details to your render. You can play with the denoise, lower keeps more of the exact output from the 1st kamspler, higher allows the 2nd ksampler more freedom to add stuff and it uses the prompt more.

- SDXL is more creative that's why I've gone back. And of course controlnets work.
  - Flux controlnets are better than sdxl. Union pro 2 is amazing. The only CN is better is for ad 1.5
- Upon your tip, and in my very limited testing... Yes, Union Pro 2, does seem to work well.

- The key reason I still use SDXL and SD 1.5 is Artists/Art styles support natively. You don't get any of that in Flux out of the box, even with the numerous variants that are out now, although Chroma (based on Flux Schnell) shows some promise.
  - Flux is great at what it does, but its breadth and scope is narrow. That is a narrow subset of imagery that I produce.

- Personally I love XL still. I mostly use it for more creative stuff and Flux for more realistic stuff. Both have their use cases. It really comes down to what you’re specifically working on

- ## [Best generation speed ups : r/comfyui _202507](https://www.reddit.com/r/comfyui/comments/1lrajf7/best_generation_speed_ups/)
- Nunchaku is in my opinion the best option if you are looking for speed and quality.

- For SDXL, DMD2 is the best LCM low step lora.
  - You can combine with other speedups like compile torch + sage attention + fp16 accumulation + teacache.

- ## [VAE and "Realistic Vision" Checkpoint : r/StableDiffusion _202312](https://www.reddit.com/r/StableDiffusion/comments/189tyz7/vae_and_realistic_vision_checkpoint/)
- (VAE) means it has VAE baked-in so no need to use any. So V6.0 B1 is a full-fledged checkpoint.
- If a checkpoint has "vae" in the name that means it contains a vae, so you want to set your vae in settings to "none". Otherwise, you want to select the appropriate vae (usually the default vae 840000 mse for SD1.5 models).

- ## [Best way to generate TONS of small images? : r/StableDiffusion _202405](https://www.reddit.com/r/StableDiffusion/comments/1d0y9us/best_way_to_generate_tons_of_small_images/)
- No model is good for small images, because the smallest SD we have was trained on 512x512 images.

- ## 🤔 [Question: how can stable diffusion models be so small? : r/StableDiffusion](https://www.reddit.com/r/StableDiffusion/comments/14lczjp/question_how_can_stable_diffusion_models_be_so/)
- Visual information can be decomposed very efficiently into low-level and high-level features. In fact, the visual cortex in our brains works that way: Lower regions encode orientation, color, and the like, while higher regions can combine them into more complex shapes such as geometric forms or faces. An auto-encoder works in a similar way, splitting images up into low-level features that are efficient to store and from which you can reconstruct the original image (with some loss). This is why models like Stable Diffusion can draw many different things with so few parameters.
  - By comparison, language somewhat escapes the neat regularity and hierarchical structure of visual information. Words can have a wide range of meanings that depend on context, be it within a sentence, within a paragraph, within a conversation, or beyond. This necessitates a deep network structure that possesses some form of memory. Furthermore, the meaning of words and sentences is often inherently ambiguous, making only sense if you have relevant world knowledge. Now, language models do not store world knowledge directly, they have to completely infer it from the relation between words. That's a pretty monumental task, especially if we expect near human-level communication from the trained model.

- stable diffusion has fewer parameters... a picture is worth 1000 words, so you can use a lot less parameters apparantly.

- ## 🤔 [Smaller sized SD1.5 model? : r/StableDiffusion _202312](https://www.reddit.com/r/StableDiffusion/comments/189jzjy/smaller_sized_sd15_model/)
- Any checkpoint that is below the 2GB fp16 version of the SD 1.5 checkpoint file wouldn't be a valid checkpoint because you'd either have to throw some data out, or quantize it down to 4-bit/8-bit. As far as I know no one has released anything like that.
  - basically, SD 1.5 has 3 main parts: U-Net (where the 'data' actually lives), the Text Encoder, and the VAE (turns image into latent or latent into image).
  - > A 512X512 image is converted into a 64X64 latent for img2img, and a latent is turned into a 512X512 image as the last step of image generation.
  - SD 1.5 has 860 million parameters in the U-Net, Text Encoder is about 500MB in size, and the VAE is about 300MB. This is normally in 32-bit float so 4 bytes X 860 million + 500MB + 300MB = 4GB+
  - Convert the model into 16-bit float and you'd get 2 bytes X 860 million + 250MB + 150MB = 2GB+
  - Convert everything into 8-bit float and you'd get 1GB+, or 4-bit and you'd get 500MB+. No one has released files of 8-bit or 4-bit that I know of but you can do this yourself for your explorations.
  - The other way to reduce the file size is to reduce the number of parameters in the U-Net but which parameters to throw out?

- ## 🌰 [LCM Lora for SDXL is very slow (\~1 minute for 5 steps) : r/comfyui _202311](https://www.reddit.com/r/comfyui/comments/17t2a86/lcm_lora_for_sdxl_is_very_slow_1_minute_for_5/)
  - Tried new LCM Loras. The one for SD1.5 works great. Two others (lcm-lora-sdxl and lcm-lora-ssd-1b) generate images around 1 minute 5 steps.

- ## [Why is there no more hype for tech that speeds up image generation e.g. LCM, SSD-1B, Tensor-RT? : r/StableDiffusion _202311](https://www.reddit.com/r/StableDiffusion/comments/17o40gi/why_is_there_no_more_hype_for_tech_that_speeds_up/)
- I think mostly because they generally require retrained or converted models, don't work with tools like ControlNet or LoRAs, or aren't smoothly integrated into A1111.
  - This is it. The biggest advantage of stable diffusion over things like midjourney is the amount of control you can do to your images like controlnet and loras. If you can't use those features on top of having a crappy GPU then you might as well use cloud server and generate stuff from your iphone instead.

- Because the point for most of us are not clicking and make 30 images in 10 secs. The trade off about quality/colors is much more than visible.
  - The point is coherence, higher quality and precission trainings, etc.
- Exactly my opinion, it takes me 5 seconds to get an image, 2 or 3 seconds less wouldn’t change my experience but being able to render accurate hands and feet or simply the right color for every clothes would be so much nicer.

- SSD-1B is not as good , in comparison with base SDXL it generates 1.5 like images. (Tested in foocus) 
  - LCM: there is just one model and the output again is not as good as 30 step output and you need comfy. 
  - TensorRT : I tried it but most of the times it’s useless as no control net , no multiple Lora’s, needs even more vram, won’t work with most speed up techniques.

- I don't think that speed is that compelling, what people want is better results and more control over the result.
- 99% of the time I don't need more speed, I need more control. I can already generate several thousand images a day if I'm so inclined

- ## [Smallest Stable Diffusion model to use with Comfy UI? : r/comfyui _202408](https://www.reddit.com/r/comfyui/comments/1ejyuo8/smallest_stable_diffusion_model_to_use_with_comfy/)
- Most of the SD15 checkpoints are around 2-3gb. Like realisticVisionV51, analogmadness, epicrealism, epicphotogasm, its also the best model to run if you have very low hardware stuff. 
  - You could try SDXL, those models are round 6gb.

- ## [SSD-1B: a distilled SDXL model that is 50% smaller and 60% faster without much quality loss! : r/StableDiffusion _202312](https://www.reddit.com/r/StableDiffusion/comments/17fbta8/ssd1b_a_distilled_sdxl_model_that_is_50_smaller/)
- Is it compatible with sdxl based lora/Controlnets?
  - No the current Lora’s are not compatible. New ones should be trained. But it’s now 40% faster to train Lora’s

- ## [What is your preferred SDXL distillation method/lora? : r/StableDiffusion _202408](https://www.reddit.com/r/StableDiffusion/comments/1em0uae/what_is_your_preferred_sdxl_distillation/)
- Out of the ones, I've tried: dmd2_sdxl_4step_lora_fp16.safetensors
  - It has good compatibility, has worked on all the checkpoints I've tried it on. 
  - I use 1.0 CFG which disables the negative prompt and speeds up generation even more.
- this one is very interesting and tempermental with most samplers, what are you using, I'm getting amazing results for realism with LCM and weird results with others
  - Yes, LCM is the correct sampler, it says on the huggingface. It's not designed to work with anything else. They also say to use Simple for the scheduler, however, I didn't really notice a difference. That's in ComfyUI, I have no idea how you set that in any other UI.

- ## [Are there any smaller versions of Stable Diffusion ? : r/StableDiffusion _202312](https://www.reddit.com/r/StableDiffusion/comments/18hklt5/are_there_any_smaller_versions_of_stable_diffusion/)
- You can try running ComfyUI in fp8. It will convert models from fp16, reducing their size. For example, on my machine, SDXL uses only around 3gb VRAM instead of over 6gb. But 2gb VRAM really is not enough.

- ## [From the creators of SDXL Lightning introduce "Hyper SD." Works with SDXL SD1.5 and controlnet models : r/StableDiffusion _202404](https://www.reddit.com/r/StableDiffusion/comments/1caalgo/from_the_creators_of_sdxl_lightning_introduce/)
- whats the Sampling method for this?
  - I seem to get best results with LCM sampler, ddim_uniform or sgm_uniform scheduler - and 8-10 steps, CFG 1-1.2 (for SDXL 4 step version)
  -  I get best results with the TCD sampler I think, gamma set to ~0.75

- so far with sdxl , it doesn't seem faster or more accurate then lightning @ 4 steps , maybe we need special sampler. they talk about ddim but it doesn't produce the same output as they present

- ## [SDXS: Real-Time One-Step Latent Diffusion Models with Image Conditions : r/StableDiffusion _202403](https://www.reddit.com/r/StableDiffusion/comments/1bo2aj6/sdxs_realtime_onestep_latent_diffusion_models/)
- I just did a top post for sdsx. Given I can hit 294 images per second on my 4090 I certainly will be interested when version 1 is released. Previously with sd-turbo my best was 200 images per second.

- ## [Lumina 2.0 is a pretty solid base model, it's what we hoped SD3/3.5 would be, plus it's truly open source with Apache 2.0 license. : r/StableDiffusion _202502](https://www.reddit.com/r/StableDiffusion/comments/1ilipk3/lumina_20_is_a_pretty_solid_base_model_its_what/)
- Lumina 2 is superior to Flux in 2 aspects:
  - Better concept understanding. e.g. It is the only model that understands Left vs Right.
  - It is better at illustrations.

- How does it compare to SD1.5, SDXL, and Flux in terms of resolution and prompt inheritance.
  - I think it beats them all except Flux. And you can go pretty high res with it without requiring too much VRAM. I think about around 2048x2048 it starts to break. Still a very new model, no tools at all for it like LoRAs, IPAdapter, CN, etc.
  - It has pretty good image quality, I think it tends to be photorealistic but also very flexible with aesthetics. What I think sets it apart is using Gemma for text encoding. You can prompt it like an LLM, we're still figuring out what is possible to do with it.

- I hope it's easy to train and develop tools around it. It's a really impressive model with only 2.6B params. 

- I've noticed that generally Gemma 2 2b is known to be heavily censored which may limit the potential output of lumina image 2. has anyone had success using another llm? I tried but I know very little and got an error when simply trying to substitute uncensored Gemma model in is place.

- ## [Open-Source Generative AI model: Lumina-Next : r/StableDiffusion _202406](https://www.reddit.com/r/StableDiffusion/comments/1dc16vt/opensource_generative_ai_model_luminanext/)
- It’s another DiT model not just a regular Unet model

- ## 🚀 [Omnigen 2 is out : r/StableDiffusion _202506](https://www.reddit.com/r/StableDiffusion/comments/1li4fui/omnigen_2_is_out/)
- This is good stuff, closest thing to local ChatGPT that we have, at least until BFL releases Flux Kontext local (if ever)

- didn’t Bytedance publish Bagel? Not on ChatGPT’s level but same capabilities.
  - There's also dream0
- I think DeepSeek’s Janus began the trend
  - If I am being honest, I don’t actually think these unified approaches do much beyond what a VLM and diffusion model can accomplish separately. 
  - Bagel and Janus had a separate encoder for the autoregressive and diffusion capabilities. The autoregressive and the diffusion parts had no way to communicate with each other.

- 4 Minute per image 768x512 on a 4090 is pretty slow but hopefully someone will optimize this further

- ## 🚀 [OmniGen: A stunning new research paper and upcoming model! : r/StableDiffusion _202409](https://www.reddit.com/r/StableDiffusion/comments/1fl46sk/omnigen_a_stunning_new_research_paper_and/)
  - It's a multimodal model with a built in LLM and a vision model that gives you unbelievable control through prompting.

- It just is an LLM, Phi-3-mini (3.8B) apparently, with only some minor changes to enable it to handle images directly.
  - They don't add a vision model, they don't add any adapters, and there is no separate image generator model. 
  - 💡 All they do is bolt on the SDXL VAE and change the token masking strategy slightly to suit images better. 
  - No more cumbersome text encoders, it's just a single model that handles all the text and images together in a single context.
  - The quality of the images doesn't look that great, tbh, but the composability that you get from making it a single model instead of all the other split-brain text encoder + unet/dit models is HUGE. And there's a good chance that it will follow similar scaling laws as LLMs, which would give a very clear roadmap for improving performance.

- I don't see how they could adapt an existing LLM to do this? To my understanding, the transformers in existing LLMs are trained to predict the logits (i.e. probabilities) of each token it knows on how likely that token is next to appear.
  - here's what I can piece together from reading the paper and looking at the Phi-3 source code. Trying to read between the lines of the paper, the image tokens just get directly un-patched and decoded with the VAE. They might keep the old classifier layer for text, but idk if that is actually supported, since they don't show any examples of text generation.
  - And they say they start from the pre-trained Phi-3, not from random initialization.

- It sounds sort of like they just retrained the model to behave the same way as SD3 or Flux, with similar architecture, though I haven't read any details beyond your post.
  - Sort of? Except that SD3 and Flux both use text encoders which are separate from the diffusion model, and use special attention layers, like cross attention in older diffusion models, to condition the text into the images. This gets rid of all that complexity, and instead treats the text and the image as a single unified input sequence, with only a single type of basic self-attention layers, same as how LLMs do it.
- SD3 and Flux join the sequences in each attention block, and I think Flux has a mix of some layers where they're always joined and some where they're manually joined, so the end result is somewhat the same.
  - I've been an advocate for ditching text encoders for a while, they're unnecessary bloat especially in the next transformer models. This sounds like it just does what SD3 and Flux would do with trained input embeddings in place of the text model encodings, and likely achieves about the same thing.

- And if this is true (which is freaking nuts), then that means we can just bolt on an SDXL VAE onto any LLM. With some tweaking, of course...

- It should be fine for consumer GPUs. The paper says it’s a 3.8B parameter model, compared to SD3s 12.7B parameters, and SDXLs 2.6B parameters.
  - SD3 is only 2.3B parameters (the crap they released. 8B still to be seen), Flux is the one with 12B. SDXL is around 700M

- Source code does not mean model weights.

- ## [Crazy fast image generation with LCM LoRA for SDXL | myByways _202311](https://mybyways.com/blog/crazy-fast-image-generation-with-lcm-lora-for-sdxl)
- If you, like me, already have SDXL Base 1.0, then just download and apply the LCM LoRA for SDXL, which “can then be applied to any fine-tuned version of the model without having to distil them separately.”
  - Alternatively, the full LCM SDXL model can be used avoid the two steps of first loading SDXL and then loading the LoRA.
  - Similarly, you can download segmind/SSD-1B and the apply the LCM LoRA for SSD-1B, or you can just download the full LCM SSD-1B model.

- ## [SDXL Lightning 1 Step | 2 Step | 4 Step | 8 Step · comfyanonymous/ComfyUI · Discussion _202402](https://github.com/comfyanonymous/ComfyUI/discussions/2867)
  - I upgrade the original workflow to support multi lora and multi model merge and is really fast.
  - Here is my Workflow base on lora not the full checkpoint.
  - This is Lightning lora and LCM lora combined and looks the quality in 2 steps
  - I recommend using the lora for acceleration not the model, the lora give much better result combined with other model with the merge node.

- ## [I hope comfyui will support sdxs soon · Issue · comfyanonymous/ComfyUI _202403](https://github.com/comfyanonymous/ComfyUI/issues/3147)
  - This model can achieve a speed of 100FPS on a single GPU
  - https://github.com/IDKiro/sdxs

- I wrapped up all of this thread into something a bit easier to understand, with some other features just for fun:  https://openart.ai/workflows/-/-/fUxFDJrPkuSshjFyTl7F

- Just a quick word of feedback for others interested in this model:
  - It is fast, but it is also really baked-in. Even in a huge batch generation, different images are only minimally different. To be honest it feels more like a db of pre-generated images being retrieved than a full generative model.
  - Negative prompts as for most of these fast models do not work. This can very much limit the kind of generations
  - The direct generation of images which are not exactly 512x512 will just not work.

- ## 📡 [Current State of Text-To-Image models : r/StableDiffusion _202503](https://www.reddit.com/r/StableDiffusion/comments/1jnt4ch/current_state_of_texttoimage_models/)
- Flux is really good, pony is really good for *cough* nsfw stuff, SDXL shines in photrealism with the plethora of LORAs to give your stuff a unique feel.

- ## [Gguf speed question : r/comfyui _202409](https://www.reddit.com/r/comfyui/comments/1fguxif/gguf_speed_question/)
- Gguf is slower but smaller, use the Q4 gguf if you are trying to add a ton of overhead like stacked loras and controlnet.

- [Should GGUF will be faster than safetensors? : r/comfyui _202503](https://www.reddit.com/r/comfyui/comments/1j52vsy/should_gguf_will_be_faster_than_safetensors/)
- No, oftentimes GGUF is slower even. The main benefit of these quantized models (same as with LLMs) is it allows you to run a larger "better" model on lower end hardware at the cost of precision and time depending on which type of quantization you use
- GGUF is often slower unless the overhead of swapping stuff in and out of VRAM (for the non-GGUF model) outweighs the overhead of having to dequantize everything before actually performing calculations. If you can compile the GGUF model, that actually seems to make a huge difference. 
- Gguf save vram not speed, they’re technically slower as gguf is compression

- I've found GGUF is to save VRAM, not necessarily to speed up generations, though it can help to fit more operations on your cards at once. 

- It would actually use slightly more (but you're right about higher quality). GGUF quants are block-based, so they have a small header at the start of every chunk. FP8 is basically just casting to an 8-bit type and doesn't contain meta-information.

- 
- 
- 
- 

- ## [SD-Turbo is out : r/StableDiffusion _202312](https://www.reddit.com/r/StableDiffusion/comments/189zvcg/sdturbo_is_out/)
  - They actually seem to have released SD-turbo at the same time as SDXL-turbo.
  - It does not allow for commercial use. But DOES allow for non-commercial redistribution. 
  - Its like SDXL-turbo. But with 1/4 the memory, 1/4 the rendering time.... and 1/4 the variety of subject matter.

- ## [why is SD1.5 still so popular and so many new models come on civit? : r/StableDiffusion _202501](https://www.reddit.com/r/StableDiffusion/comments/1hzwkvl/why_is_sd15_still_so_popular_and_so_many_new/)
- Because of the lower cost of resources and training, works that pursue an artistic style rather than a "real photo" can and will be well represented by LORA.

- Fine-tuning with SD1.5 is efficient due to its lower parameter count and resolution, resulting in faster training and less burden for large-scale tasks. SD1.5 requires no compromise on accuracy. With advanced tools available today, fine-tuning is more efficient than ever. 

- ## [What is currently the fastest, low-resolution way to generate images on an M1 Mac? : r/StableDiffusion](https://www.reddit.com/r/StableDiffusion/comments/1heqec0/what_is_currently_the_fastest_lowresolution_way/)
- For 256x256, use miniSD , and I think you can use a sd1.5 LCM LoRA to make it very fast.
  - [justinpinkney/miniSD · Hugging Face](https://huggingface.co/justinpinkney/miniSD)

- ## [Current state of 1.5 vs SDXL? : r/StableDiffusion _202401](https://www.reddit.com/r/StableDiffusion/comments/19df545/current_state_of_15_vs_sdxl/)
- What's nice about SDXL:
  - prompt styling - you barely need to switch models or add loras, like you can, but usually the base models like juggernaut can just adapt to way more styles via prompts that they are already pretty solid.
  - larger images
- Whats nice about 1.5:
  - better NSFW support
  - better skin textures via custom models
  - easier to train
  - lower memory footprint
  - backlog of tools
  - contronet works better

- SD1.5 is better in the following ways:
  - Lower hardware requirement
  - Hardcore NSFW
  - "SD1.5 style" Anime (a kind of "hyperrealistic" look that is hard to describe). But some say AnimagineXL is very good. There is also Lykon's AAM XL (Anime Mix)
  - Asian Waifu
  - Simple portraiture of people (SD1.5 are overtrained for these type of images, hence better in terms of "realism")
  - Better ControlNet support?

- [SDXL vs. SD 1.5: A Deep Dive into Image Generation AI Performance _202308](https://sandner.art/sdxl-vs-sd-15-a-deep-dive-into-image-generation-ai-performance/)

- ## [comfyui知识点简记](https://oq6szavaxui.feishu.cn/wiki/JoDRwnWz6iOi3SkYMxwcDycInkh)
- 
- 
- 

- ## [字节又整活，新型框架 Hyper-SD，比 SDXL-Lightning 更优秀！ - 知乎 _202404](https://zhuanlan.zhihu.com/p/694590649)
- Hyper-SD 不仅支持对 SDXL 大模型的加速，这次还增加了对 SD1.5 大模型的加速支持。

- ## [What is the difference between lighting versions on checkpoints? : r/StableDiffusion _202412](https://www.reddit.com/r/StableDiffusion/comments/1hpevjb/what_is_the_difference_between_lighting_versions/)
- Lightning models take only about 5 steps to converge, so they are much faster. Make sure to set the CFG lower for Lightning models. It should be around 2, rather than the 7 or so for a regular model. From what I can tell, Lightning models don't seem to take much notice of negative prompts, which is a disadvantage.
  - UPDATE: Lightning models also work best with a different sampler schedule, such as SGM Uniform or Turbo. Some samplers work better than others.

- I recommend trying DMD2 checkpoints instead of lighting ones. Or just manually download the dmd2 lora and generate at 4-12 steps with CFG 1-1.5 using LCM scheduler.

- ## [Are there any fast, lightweight models? : r/StableDiffusion _202501](https://www.reddit.com/r/StableDiffusion/comments/1i6k86e/are_there_any_fast_lightweight_models/)
- Any SDXL model with DMD2 lora. It's newer and as fast as LCM, Turbo and Lighting but with better prompt adherence (according to DMD2 paper).

- [I work a lot with FLUX, but DMD2 keeps amazing me (12 examples) : r/StableDiffusion _202408](https://www.reddit.com/r/StableDiffusion/comments/1f0znay/i_work_a_lot_with_flux_but_dmd2_keeps_amazing_me/)
  - This is DMD2 for SDXL, something like 18 images/minute on a simple L4 Colab. I do 0.4 GS for 8 Steps (default is 0/4). It's NOT as coherent as FLUX of course, but it hits differently, right?
  - DMD2 is just an optimiser, like Lightning, Turbo or LCM. Your post does not specify what checkpoint you're using.
  - DMD2 is a LORA, but also a model based on PG2 or SDXL.

- ## [What are the currently known methods to speed up SDXL image generation in A1111/forge? (windows) : r/StableDiffusion _202502](https://www.reddit.com/r/StableDiffusion/comments/1ixuii6/what_are_the_currently_known_methods_to_speed_up/)
- For me the dmd2 lora is the best method right now
  - I personally use with 10 steps, 1 cfg and lcm karras
  - https://huggingface.co/tianweiy/DMD2
- The lora is to keep the image quality in lower steps. Low steps=faster generation There's dmd2, lcm and lightning loras for that purpose but I personally think dmd2 gives better results.

- Turbo loras etc

- A lcm LoRA will Bring SDXL down to 6 steps

- ## 🆚 [What's the Difference Between SDXL LCM, Hyper, Lightning, and Turbo? : r/StableDiffusion _202506](https://www.reddit.com/r/StableDiffusion/comments/1lk1anq/whats_the_difference_between_sdxl_lcm_hyper/)
- They are all distillation techniques that trade some quality and variability for increased generation speed.
- CFG: for some distill techniques, CFG needs to be very low, typically below 2, so negative prompting mostly doesn't work (unless you can raise CFG by other means, like APG). The main tradeoff is that CFG at exactly 1 typically doubles the generation speed, _and_ they usually work great at very low step counts. Some techniques like Hyper and PCM are available both as small CFG and normal CFG versions: the normal ones behave more like usual models, with CFG reduced a bit.
- Samplers: LCM, PCM "lcmlike" and DMD2 are "small CFG" distills that work specifically with the LCM sampler (although sometimes you can have successful gens with other samplers, like Euler). TCD is designed to work with the TCD distill, although it can work very well with other small CFG techniques; DDIM and Euler also tend to go well with those. Oh, and to make matters more confusing, note that "LCM" and "TCD" can mean the samplers, and/or the techniques/LoRAs.
- the original SDXL-Turbo generates at only 1-2 steps, but at a lower resolution (512x512), and AFAIK there are no official LoRAs available. There are some unofficial around, and many other models called "Turbo"
  - it'd fall into the "small CFG" variety.

- Small CFG: Lightning, Hyper, TCD, PCM, Turbo: low CFG with DDIM, TCD, Euler, or other samplers.
- Small CFG, LCM-like: LCM original, PCM-lcmlike, DMD2: low CFG with the LCM sampler.
- Normal CFG: Hyper, PCM; sampler likely depends on the model.

- ## [Lightning/DMD2/PCM equivalents for Flux? : r/StableDiffusion _202505](https://www.reddit.com/r/StableDiffusion/comments/1khkdvi/lightningdmd2pcm_equivalents_for_flux/)
- My favourite is Flux 1 Turbo Alpha, a LoRA that allows you to drop your steps to 8-12.
  - There's also the Hyper LoRA, which works similarly but it's double the size.

- That's what the Schnell version of the Flux model is.

- 🆚 [Compare 1 step real time generations between SDXL Turbo, Lightning and Hyper : r/StableDiffusion _202405](https://www.reddit.com/r/StableDiffusion/comments/1cbzwqh/compare_1_step_real_time_generations_between_sdxl/)
- Why is Lighting sd xl is really great. almost no quality loss and all superfast 1.5 model are garbage in comparison with full 1.5 or am I doing something wrong? is there a way to use Hyper in 1.5 with 1-6 steps and get good quality?
  - You need the 1.5 hyper lora models

- ## 🆚 [Lightning vs Turbo models?? : r/StableDiffusion _202404](https://www.reddit.com/r/StableDiffusion/comments/1bsg1cb/lightning_vs_turbo_models/)
- Turbo diffuses the image in one step, while Lightning diffuses the image in 2 - 8 steps usually (for comparison, standard SDXL models usually take 20 - 40 steps to diffuse the image completely).
  - I'm not fully sold on the idea of diffusing the image in just one step, since stable diffusion was originally intended to be a multi-step process.
- SDXL Turbo is optimized for 512×512 image resolution, while Lightning supports 1024×1024 full SDXL resolution (and also all the various resolutions SDXL was trained on). 
  - Also, SDXL Turbo doesn't support CFG scale or negative prompts

- Lightning works well with ControlNet.
  - Turbo, not so much since it generates in one step, and multiple steps are required for fine ControlNet influence control.
  - Turbo and all the derived models are limited by Stability AI's Non-Commercial license.
  - 💰 Lightning models have a proper free and open-source license, and commercial use is allowed, no question asked, no registration required.

- turbo model works with 1 step and gives goodish results, there are 4 lightning models, for 1, 2, 4 and 8 steps, fewer steps are faster but more steps gives better quality, the 2 steps one is the fastest giving a passable quality, in line with turbo I would say, so the turbo model is the fastest as it only needs one step. 
  - The 1 step lightning exists but it's experimental and don't work too well. Sdxl turbo is optimized for 512x512, so speed is even faster, in can do 1024x1024, but quality drops. Lightning is optimized for 1024x1024.

- LCM increases the inference speed of older stable diffusion models (SD 1.5, SD 2.0) by reducing the number of steps needed to diffuse the image (basically the same as Lightning but for older models). However, Lightning is made to work with SDXL models and it's faster than LCM. While there's an LCM for SDXL, using SDXL Lightning is recommended because it's faster than LCM SDXL.

- ## [SDXL Turbo, SDXL Lightning, Cascade and SD3 : r/StableDiffusion _202402](https://www.reddit.com/r/StableDiffusion/comments/1b23p3l/sdxl_turbo_sdxl_lightning_cascade_and_sd3/)
- Neither Turbo nor Lightning are “improved.” The whole point of using them is the speed, not quality. 

- Turbo needs as few as just 1 step, suitable for real-time applications. 
  - As for Lightning, it still retains a pretty good quality at 8 steps, as opposed to LCM which had noticeable quality loss. Lightning is good enough that I switch to using it for normal uses now.
- As for Cascade, I find SDXLs refined models to give better looking outputs but Stable Cascades ability to write all kind of random text pretty accurately is really impressive... 

- ## 🆚 [Hyper, Turbo, Lightning, Cascade, Pony, Pix Art and more - Whats the differences? : r/StableDiffusion _202405](https://www.reddit.com/r/StableDiffusion/comments/1cy9lcm/hyper_turbo_lightning_cascade_pony_pix_art_and/)
- Hyper, Lightning, Turbo = special checkpoints that only need 1 to 8 steps to make an image and work better with really low CFG of 1 to 2 (though Hyper can now work at 5-8 CFG). 

- Turbo: meant for 512x512 image size. Faster than lightning.
- Lightning: a fast model with good image quality. I prefer it over sdxl. Pretty popular in the community.
- Hyper: similar to lightning. Creator claims that it outperforms lightning in image aesthetics but so far I have been disappointed. 
- Cascade: almost as slow as sdxl on my poor old system. Usually creates pretty good images. A bit surprisingly not that popular in the community.
- Pony: I think it was trained with booru images and image tags so it is able to produce anime/hentai images with great prompt adherence.

- ## 🧩 [Difference between checkpoint , lora, model... : r/StableDiffusion _202308](https://www.reddit.com/r/StableDiffusion/comments/15jfsdt/difference_between_checkpoint_lora_model/)
- Technically they're all machine learning models, but checkpoints are usually referred to just as models. 
  - All models are static, meaning they only know what they were trained on. In order for them to learn something new, they have to be (re)trained again, also known as finetuning.
- Their differences in very rough terms:
  - Checkpoints are the big models that make images on their own.
  - Loras and all their variations like Lycoris are "mini models" that plug into a checkpoint and alter their outputs. They let checkpoints make styles, characters and concepts that the base checkpoint they're used on doesn't know or didn't know very well.
  - Hypernetworks are an older and not as good implementation of the same paper and same concept as Loras.
  - Textual Inversions are sort of bookmarks or compilations of what a model already knows, they don't necessarily teach something new but rearrange stuff that a model already knows in a way that it didn't know how to arrange by itself.
- SD 1.x, SD 2.x and SDXL are both different base checkpoints and also different model architectures
  -  SD 1.5 is say both the NES itself but also one game for it. All SD 1.x based models are compatible with SD 1.x Loras and models for extensions like ControlNet. 
  -  SD 2. X is the SNES, it's a different architecture so 1.x models won't be compatible with it, same for SDXL if you say that's like the N64.

- ControlNet models are also machine learning models that inject into the Stable Diffusion process and control the denoising process, they're used with an image made by preprocessor. That image is be used to guide and control that denoising process, also hence the name.

- ## [Super fast image generation with LCM Sampler : r/comfyui _202311](https://www.reddit.com/r/comfyui/comments/17s3s6u/super_fast_image_generation_with_lcm_sampler/)
- FYI LCM sampler is no longer required, ksampler supports lcm (coming from the original creator of that node)
- THis POST is now outdated ! LCM has been integrated in ComfyUI and can be used with normal samplers. Just update ComfyUI and you will be able to choose it.

- i do not understand how to use it. Any examples of workflow?
  - There you go: https://app.flowt.ai/c/ilKpVL
  - you just plug in a Lora that uses the LCM-weights thing, then set your LCM settings in K-Sampler and off you go.

- ## [How well does ComfyUI perform on macOS with the M4 Max and 64GB RAM? : r/comfyui _202503](https://www.reddit.com/r/comfyui/comments/1jhifyi/how_well_does_comfyui_perform_on_macos_with_the/)
- TLDR - if you want to work linear on one image, a Mac is a huge waste of time. Maybe 25% of the speed of a decent NVIDIA PC for AI generation. 
  - However, if you know how or want to multitask, it’s easily the best system you can purchase.

- for generative AI stuff, compared with my Linux PC with a RTX 4090 - mac m4 pales in comparison. 
  - We are talking minutes vs seconds here for a 1024x1024 Flux generation. Most of it is tuned for Nivida CUDA and that is the key. 
  - Apple Silicon offers great performance for everyday computing, but its support for machine learning frameworks like PyTorch sucks butt compared to CUDA.
  - i can drive Comfui remotely from the mac with the server running on the linux pc.

- AI image and video generation require cuda cores to function properly so Apple or even AMD gpus are not recommended.

- Not well. Most local AI is still tied to having CUDA. Honestly the biggest missing link is getting Pytorch to run accelerated on Apple silicon. That will speed up most of the tasks that do CPU fallback which is where you get your abysmal performance.

- Apple has been so far behind in AI. Best just go for PC with Nvidia gpu.

- M4 Max MBP with 128 GB memory here. Let’s just say I never, ever run image gen on that machine. Even for models/pipelines that ARE supported, it’s not worth the agonizing wait.

- my Mac M4 16gb is much more slower than my old PC with the good old Geforce 3060. An Apple a day keeps the Comfyui away.

- ## 把ComfyUI工作流无缝转为MCP Tool的一款工具：Pixelle-MCP
- https://x.com/aigclink/status/1955163038035914972
  - 也就是说用自然语言即可让LLM控制ComfyUI执行复杂的生成任务
  - 自动化和批量化，LLM可以自动化执行重复性的任务，比如批量生成不同风格的图像，或者根据预设的规则自动调整参数

- ## ComfyUI 现在是不是没人学了。时间线上的 ComfyUI 大佬好像都不发新教程了 _202508
- https://x.com/hylarucoder/status/1954857846987968542
- 现在很多通用生图模型的能力已经足够覆盖很多工作流了，而且comfyUI铺天盖地的配置，看的让人头疼，我现在做的 YOOART IMAGE 都是接入的通用模型，比如gpt-4o-image、即梦、midjourney、qwen-image、imagen4 这些，普通任务都可以完成，只需要输入提示词就好
- 是不是可以这么理解，只要不是很专精的或者需要批量生成的图片，基本就告别 comfyui 了？
  - comfyui 在一些比较垂直的领域比如电商的细分场景，需要自己部署的训练的模型，批量化作业才需要它，对于大众普通人来说，随着模型能力越来越强，那么提示词就会替代越来越多的工作流，典型的就是 Chatgpt 4o、flux-kontext、即梦、这来能生图，能改图的胜任大部分，未来应该还是生图 Agent 的天下吧。
  - 在一些需要固定工作流，固定结果的场景我觉得还是需要comfyui，类似传统的PS，AE 吧，现在普通大模型会占据的应该是类似美图秀秀，剪映这种简单化的生态位，但是这种生态位人数多，但是comfyui的商业价值，其实还是不小的，专业重活儿还是得靠它。

- 新的开源模型很大，运行门槛过高，而且效果没办法打过好的闭源模型

- 我一直认为工作流是过渡产物，注定被模型干掉

- 感觉comfyUI很麻烦，租个云电脑配置半天还不如直接花钱在平台生图 生视频

- https://x.com/hylarucoder/status/1955106887407653234
  - 汇总一下大家的观点, 早期 ComfyUI 火是因为生图必须「会搭工作流」
  - 现在 通用模型就能解决 80% 的场景。搭节点的边际价值下降，而 ComfyUI 生态商业化分叉进一步拉大了用户和开发者学习和维护成本
  - 而开源世界里面又有很多一键化套件，ComfyUI 进一步成为了牛夫人。。。。
# discuss-qwen
- qwen-image
  - https://huggingface.co/city96/Qwen-Image-gguf/tree/main
  - https://modelscope.cn/models/city96/Qwen-Image-gguf/files
  - [Qwen-Image ComfyUI Native Workflow Example - ComfyUI](https://docs.comfy.org/tutorials/image/qwen/qwen-image)

- https://github.com/ModelTC/Qwen-Image-Lightning /apache2/202508/python
  - Qwen-Image-Lightning: Speed up Qwen-Image model with distillation
  - Qwen-Image-Lightning-8steps-V1.1
  - Qwen-Image-Lightning-4steps-V1.0

- ## 

- ## 

- ## [The 4-Step lightening lora for Qwen Image is available now : r/StableDiffusion _202508](https://www.reddit.com/r/StableDiffusion/comments/1mngtnn/the_4step_lightening_lora_for_qwen_image_is/)
  - 提供了workflow示例

- Can anyone confirm the workflow is working? It's not for me, it's like the lora is ignored and i get a lot of `lora key not loaded:` errors.
  - I have tried unsucessfully with both the city96 qwen-image-gguf and the distilled version from DiffSynth-Studio.
- Did you update the comfyui to the nightly one?
  - I just updated to nightly and it is working fine now ! Thanks !

- The text encoder still takes a minute to load whenever i change the prompt
  - Try this https://huggingface.co/unsloth/Qwen2.5-VL-7B-Instruct-GGUF/tree/main
  - I'm on Q3 RTX-3060 12gb, 4 steps, 1328x1328, total render time even changing prompts: Prompt executed in 49.27 seconds
  - If I've posted it is because I'm using it. It's the one recommended by city96, the fp8 clip is also very slow on my computer.

- Can anyone explain how these lightning loras work?
  - Use it like a regular lora (add a lora node) set cfg to one, steps to four, and don't bother with a negative prompt. In exchange for a small quality decrease, that might not be noticeable, you get a massive speedup. 
  - As of now, this LORA is absolutely amazing, I'm generating 1920 x 1074 images on my laptop with 8GB VRAM in under a minute, and it's getting more prompt adherence than I've ever seen even from ChatGPT.

- ## [Comfyorg upload Qwen-Image models bf16 and fp 8 : r/comfyui _202508](https://www.reddit.com/r/comfyui/comments/1mhzi3b/comfyorg_upload_qwenimage_models_bf16_and_fp_8/)
- VRAM usage reference - Tested with RTX 4090D 24GB
- Model Version: Qwen-Image_fp8
  - VRAM: 86%
  - Generation time: 94s for the first time, 71s for the second time
- Model Version: Qwen-Image_bf16
  - VRAM: 96%
  - Generation time: 295s for the first time, 131s for the second time

- ## [Qwen image 20B is coming : r/LocalLLaMA _202508](https://www.reddit.com/r/LocalLLaMA/comments/1mhf0kl/qwen_image_20b_is_coming/)
- ComfyUI is just a simple visual programming language with custom node support. 
  - If you want a simpler approach use some UI for it like https://github.com/mcmonkeyprojects/SwarmUI and if you need more control no need to pack everything into a workflow just use Krita AI or sth...

# discuss-flux
- flux-guff
  - [Lists of FLUX.1 Series Models : r/StableDiffusion](https://www.reddit.com/r/StableDiffusion/comments/1h3fcs8/lists_of_flux1_series_models/)
  - https://huggingface.co/city96/FLUX.1-schnell-gguf/tree/main
  - https://huggingface.co/city96/FLUX.1-dev-gguf/tree/main
  - https://hf-mirror.com/city96/FLUX.1-schnell-gguf/tree/main
  - https://huggingface.co/city96/t5-v1_1-xxl-encoder-gguf/tree/main
  - https://huggingface.co/TencentARC/flux-mini
  - https://github.com/city96/ComfyUI-GGUF
  - https://huggingface.co/martintomov/Hyper-FLUX.1-dev-gguf
  - https://huggingface.co/Zuntan/flux1-dev-TurboA-8step/tree/main
    - a direct GGUF conversion of black-forest-labs/FLUX.1-dev by @city96 merged with ByteDance/Hyper-Flux.
  - 🌰 [How to Run Flux Dev GGUF Models in ComfyUI (Low VRAM Guide) - Next Diffusion _202506](https://www.nextdiffusion.ai/tutorials/how-to-run-flux-dev-gguf-in-comfyui-low-vram-guide)
  - 🌰 [How to Use Flux LoRA's in ComfyUI: A Complete Walkthrough - Next Diffusion _202506](https://www.nextdiffusion.ai/tutorials/how-to-use-flux-lora-in-comfyui)
  - 🌰 [Run Flux model (gguf) with LoRA in ComfyUI _202411](https://lyleaf.medium.com/run-flux-model-gguf-with-lora-in-comfyui-50877c2c703a)
  - 🌰 [Flux.1 ComfyUI 对应模型安装及教程指南 | ComfyUI Wiki](https://comfyui-wiki.com/zh/tutorial/advanced/image/flux/flux-1-dev-t2i)
  - [如何用ComfyUI运行FLUX GGUF文件模型_慕课手记](https://www.imooc.com/article/371309)
  - 版本比较及示例 [Flux Examples | ComfyUI_examples](https://comfyanonymous.github.io/ComfyUI_examples/flux/)
  - 🆚🌰 [Most Efficient Flux? GGUF + Hyper-SD Comparisons | ComfyUI Workflow](https://openart.ai/workflows/LO4EDSFcrS6gsPnhCIPF)
  - [Flux Dev 8-16 Steps LoRA [HyperSD] | ComfyUI Workflow](https://openart.ai/workflows/reverentelusarca/flux-dev-8-16-steps-lora-hypersd/iTFCDLtctlMO6sjmEzoQ)

- ## 

- ## 

- ## 

- ## [FLUX.1是目前最好的开源AI图像生成模型吗？ - 知乎 _202410](https://www.zhihu.com/question/1457540426/answer/1904675843768317216)
- 个人觉得Flux与SDXL各有胜负，至于其他模型只能靠边站。
- 文生图：Flux在写实摄影风格绝对的王者，但二次元方向目前不怎么行，还是看SDXL魔改训练的Illustrious分支，训练资源与生态太强，Flux没得比。
- 控图：ControlNet目前还是SDXL的好用，Flux虽然Union的模型出到了V2，但还是那么回事，最大的痛点除了控制能力一般之外，还是是占用显存太高。我用远程控制4090那台机器时，多用两个ControlNet串联工作流时，经常因为爆显存卡死不动...
- 一致性上SDXL的IPAdapter与Flux的Redux各有千秋吧。
- 改图：Flux因为有专门的Fill模型，而且可以做INT4量化，所以非常强，包括二次元修复画崩区域。你没看错，Flux对二次元生图弱，但改图强，可以把SDXL的图扔给Flux做局部修改。
- 而SDXL模型如果想Inpaint与Outpaint需要插件注入特殊层修改大模型，工作流复杂，效果没Flux好，但是胜在资源占用低，不过自从Flux有了INT4之后，这个优势没多大了。而且ILL类的模型没法做注入修改。
- 真正使用的时候，这两个模型经常混用，可以把有优势模型生成的图，当做一个控制底图扔给另一个模型，或者用Flux修图，SDXL快速添加高频细节，甚至用其中一个模型批量抽取生图结果，炼成Lora给另一个模型用。非常灵活，没有谁更好，适合的就是最好的。
- 当然了要是这样用的话，好多时候用GPT生成的草图，可以作为一个很好的创作参考起点。

- 瑟瑟还是sdxl更好

- 生图用flux真的质量碾压sdxl, 就算用nunhcaku+8步turbo, 质量也是远胜于sdxl, 烂手指, 烂脸的概率低太多了, 生图时间比sdxl还快. 最大的缺点就是用 controlnet拉跨了. 二次元我觉得也是比sdxl好, kontext好好研究还不错, 对工作流没啥要求, 主要就是要研究提示词

- 
- 

- ## [ComfyUI Flux Dev: 8-Step vs. 28-Step Workflow Comparison : r/comfyui _202410](https://www.reddit.com/r/comfyui/comments/1g3jwh5/comfyui_flux_dev_8step_vs_28step_workflow/)
- Half the size of hyper so we're moving on up

- ## 🆚 [GGUF Q8 much slower than fp16 on 8GB card : r/StableDiffusion _202409](https://www.reddit.com/r/StableDiffusion/comments/1ff42v4/gguf_q8_much_slower_than_fp16_on_8gb_card/)
  - I’m running forge, with GPU weights set to 7000 MB. I can run the original Flux dev fp16 at ~5s/it, and fp8 models at ~3s/it. But when I try the GGUF version it goes up to over a minute/it, which really confuses me because it’s about the same size with the fp8 model. 
  - I even tried changing the GPU weights slider but it’s always this slow. What am I doing wrong?

- All GGUFs were severely slower for me until I removed `--cuda-malloc`, if you never had it though then it might be something else.
  - One thing I noticed is--cuda-malloc use a bit more VRAM than without which cause first run using GGUF to offload into RAM especially when you have < 8 Gb VRAM. I have to interrupt first run but then the next run will have no problem.
  - Without --cuda-malloc I don't have huge slowdown in the first run, sure it's slower than the next run but it's manageable.

- GGUF isn't properly supported in comfyui or forge. It needs to be dequantized on the fly, which is costly, and then the operations are done in normal fp.

- As the other said maybe because it try to load as much as VRAM in the first run and the problem apparent in 8 Gb or below GPU VRAM. I tried to interrupt the first run and the second and next run went smooth.
  - Also, I didn't noticed any quality advantage using Q8 GGUF than NF4 or even Hyper NF4 (8 steps) which is far more faster.

- ## 🆚 [Comparing FLUX Models: Pro, Dev, and Schnell Explained _202409](https://stockimg.ai/blog/ai-and-technology/what-is-flux-and-models-comparison)
  - Quality, Speed, license
- FLUX is a cutting-edge AI image generator created by Black Forest Labs, the same team behind the popular Stable Diffusion.
- FLUX.1 Pro is the flagship model, offering exceptional image quality and intricate details, making it ideal for high-end commercial and artistic projects.
- FLUX.1 Dev is designed for research and development, providing similar quality but optimized for non-commercial use. 
- FLUX.1 Schnell, on the other hand, is built for speed and efficiency, perfect for personal projects and quick experiments.

- ## 🆚🌰👨‍🏫 [FluxTurbo vs. HyperFlux LoRAs: Generate FLUX.1-dev Image in 4-9 Steps _202410](https://sandner.art/fluxturbo-vs-hyperflux-loras-generate-flux1-dev-image-in-4-9-steps/)

- https://github.com/sandner-art/ai-research/tree/main/FLUX
  - Settings for AI Training
  - https://github.com/sandner-art/ai-research/tree/main/FLUX/FLUX-TURBO-ALPHA
  - https://github.com/sandner-art/ai-research/tree/main/HYPER-SD/COMFYUI

- FluxTurbo is another solution to reduce generation times when using the FLUX.1-dev 
  - The technique uses distilled LoRAs, similar to the Hyper-SD/HyperFlux method.
  - Considering that FLUX.1-dev typically requires 20-30 steps to produce a final image, this technique presents a promising solution
- You can achieve impressive results with just four steps (see examples). For even more precise anatomy and details (hands), consider increasing the steps to five or more. 
  - In general, the optimal range for generating high-quality images is 7-9 steps.
- FluxTurbo Alpha is used with standard weight 1.0, HyperSD needs weight 0.125 (1.3 in ComfyUI).

- Conclusion
  - FluxTurbo is slightly faster (approximately 10%) and tends to produce better details at lower step counts. 
  - However, their quality becomes comparable around 8 steps, where both solutions generate high-quality output.
  - Compared to Flux.1-schnell (which can produce good results in just 3-5 steps), FluxTurbo offers the advantage of allowing you to use Flux.1-dev-specific features like CFG and Distilled CFG. This technique also shows potential for inpainting applications.

- ## 🆚 [Advice needed. Anything between Flux schnell and Flux 1 dev quality wise? : r/StableDiffusion _202412](https://www.reddit.com/r/StableDiffusion/comments/1hbpyjx/advice_needed_anything_between_flux_schnell_and/)
  - 🧩 Flux.1 [schnell]： Uses the Apache2.0 license, requires only 4 steps to generate images, suitable for low-spec hardware.

- You can use turbo lora for flux 1 dev. It creates ~dev quality images in just 8 steps.
  - Exceptionally good at 6 steps, latent upscale and then 6 steps with another seed
- I have had good results with 8 steps and 4 step upscale, even at 3x.

- ## 🌰 [Simple ComfyUI Flux workflows v2.1 (for Q8, , Q4 models, T5xx Q8) : r/StableDiffusion _202408](https://www.reddit.com/r/StableDiffusion/comments/1f0t6ux/simple_comfyui_flux_workflows_v21_for_q8q4_models/?share_id=u0bxKt1YqGrrp_hLHlvKp&utm_content=1&utm_medium=android_app&utm_name=androidcss&utm_source=share&utm_term=1)
  - [Simple ComfyUI Flux workflows v2 (for Q8, Q5, Q4 models) : r/StableDiffusion _202408](https://www.reddit.com/r/StableDiffusion/comments/1ewdllh/simple_comfyui_flux_workflows_v2_for_q8q5q4_models/?share_id=bcuoxLoJm9Cu9N8Ik_Gxi&utm_content=1&utm_medium=android_app&utm_name=androidcss&utm_source=share&utm_term=1)

- ## 🆚🌰 [Most efficient way to run Flux? Testing GGUF + Hyper-SD: usable images at 8 steps (workflow included) : r/StableDiffusion _202409](https://www.reddit.com/r/StableDiffusion/comments/1f9i2al/most_efficient_way_to_run_flux_testing_gguf/)
  - Hardware: RTX 4090, Image Size: 832 x 1216
  - Seems like the hyper-sd lora is optimized for the original flux-dev. I was surprised that dev-1 at 8 steps ran so much faster than that of GGUF 8 steps. Even within GGUF, it seems like 20 steps with no hyper-sd lora actually ran faster than the 16 steps version.
  - Tbh quality and fidelity loss on hyper-sd 8 step versions were noticeable to me. So I'd rather go with the 16 step version. Dev-1 + 16 step lora for those with enough VRAM.
  - Looks to me like text adherence was off to most of the images anyway, but this can be alleviated by using the fine tuned clip model 

- I wish there was a quick way to get a low res preview before waiting 20s on a full render.

- Yes GGUF versions are a bit slower, but they are a savior for us people with not much VRAM. I think the reason is using Loras on GGUF. Each lora you add, the time to complete increases by quite a lot. And Hyper is a lora after all.

- ## [Slow generation times in Flux, using loras ( fixed by using GGUF models or XLabs loras ) · Issue · comfyanonymous/ComfyUI _202408](https://github.com/comfyanonymous/ComfyUI/issues/4674)
- In Summary:
  - Flux model + XLabs loras => FAST
  - GUFF model + loras => FAST
  - Flux FP8 + civitai loras => SLOW

- ## [What's the fastest flux model right now? : r/comfyui _202409](https://www.reddit.com/r/comfyui/comments/1fryi73/whats_the_fastest_flux_model_right_now/)
- On my 3090, fp8 e5m2 with the --fast command line switch is approx 50% faster than fp16, gguf, or fp8 e4m3.
  - I thought --fast was only useful for 40xx cards! Testigñng right away with my 3070

- Gguf models are the fastest after nf4

- ## [Fast Flux.1 Dev (in 8 steps!) - Turbo Alpha: First Impressions and Testing Results : r/StableDiffusion _202410](https://www.reddit.com/r/StableDiffusion/comments/1g26pim/fast_flux1_dev_in_8_steps_turbo_alpha_first/)
  - I spent my Saturday morning testing out the newly released Flux.1 Dev Turbo Alpha.
  - Quality vs. Speed Trade-off: It maintains most of the quality of Flux Dev, but there is an obvious decline in fine details (generations are done in 8 steps). You will notice details are off (e.g., a waterfall in an unexpected spot or a crooked pole).

- For those who don't know, these are model distillations.
  - A model is effectively retrained to do the same task in less steps and attempt to meet the same quality as the original. Distillations in general attempt to get 90%+ of the original quality in less steps.

- ## [Testing Flux. Dev vs HiDream. Fast – Image Comparison : r/StableDiffusion _202506](https://www.reddit.com/r/StableDiffusion/comments/1l1dn1e/testing_fluxdev_vs_hidreamfast_image_comparison/)
- i use FLUX.1-Turbo-Alpha by alimama-creative. It gives great images in just 8 steps with euler_ancestral, Sgm_Uniform & cfg at 1.

- ## [Why is Flux "schnell" so much slower than SDXL? : r/StableDiffusion _202502](https://www.reddit.com/r/StableDiffusion/comments/1itw0j4/why_is_flux_schnell_so_much_slower_than_sdxl/)
- Schnell isn't a small model - it's the same as Dev model, and it just uses fewer steps. Why would you compare it to SDXL? 

- Use fp8 versions of Flux Schnell based models and 4 steps only, CFG1, flux guidance 3.5

- SDXL is an LDM architecture and Flux is a DiT architecture, which requires more computing resources.

- ## [Is Flux GGUF supposed to be faster or its just memory savings? : r/StableDiffusion _202408](https://www.reddit.com/r/StableDiffusion/comments/1evktoz/is_flux_gguf_supposed_to_be_faster_or_its_just/)
- It is actually slower at the moment, because it once dequants and calculate. to make faster, we need more optimized calculation.

- The current implementation of GGUF doesn't yet fully utilize the advantages of GGUF's structure. It's partially borrowing techniques used in LLMs, but it still needs to evolve further.

- ## [m4 mac mini本地部署ComfyUI, 测试Flux-dev-GGUF的workflow模型10步出图, 测试AI绘图性能, 基于MPS(fp16), 优点是能耗小和静音 - 刘悦的技术博客 - 博客园 _202505](https://www.cnblogs.com/v3ucn/p/18593990)
- [How to Use FLUX GGUF Files in ComfyUI _202505](https://promptingpixels.com/tutorial/flux-gguf)

- 最后是10步迭代的出图效果，可以看到，精度没有下降太多，主要问题还是出图速度太慢

- ## [Flux.1 GGUF模型说明及使用](https://www.zhihu.com/tardis/zm/art/16474690938)

- GGUF 版本 是 Flux 模型的一种优化版本，专门为低显存设备设计
- GGUF 是 GPT-Generated Unified Format 的缩写，是一种高效的模型存储和交换格式。它通过量化技术（如 4 位、6 位、8 位等）压缩模型权重，从而减少显存占用，同时保持较高的生成质量。
  - 量化原理：量化通过减少模型权重的精度（如从 32 位浮点数压缩到 4 位），降低显存需求，但可能会略微影响生成质量。
  - 优势：GGUF 版本可以在低显存设备（如 6GB 显存）上运行，适合没有高端显卡的用户。
- 原始版本（如 Flux.1 Dev 和 Schnell）对显存要求较高，通常需要 16GB 或更多的显存才能流畅运行。
  - Q4 和 Q5：适合大多数用户，显存需求适中，生成质量较好。

```table
量化级别	      显存需求	 生成质量
Q2/Q3（2/3 位）	6GB	     较低
Q4（4 位）	    8GB	     中等
Q5（5 位）	    10GB	   较高
Q8（8 位）	    16GB+	   接近原始版本
```

- GGUF 版本的优势与局限​
- 优势​
  - 低显存需求：最低仅需 6GB 显存，适合老显卡或低端设备。
  - 快速生成：量化后的模型推理速度更快，适合需要快速出图的场景。
  - 高质量生成：尽管是量化版本，但 Flux GGUF 的生成质量仍然非常出色，尤其是在 8 步或更多步数的情况下。
- 局限​
  - 生成质量略低：与原始版本相比，GGUF 版本的生成质量略有下降，尤其是在低量化级别（如 Q2 或 Q4）时。
  - 不支持负提示：Flux GGUF 版本不支持负提示功能。

- ## 📌 [FLUX.1入门教程：模型资源汇总与详细说明 - 知乎 _202503](https://zhuanlan.zhihu.com/p/10106104364)
- 一般情况：完整版（fp16）需要 24G 显存才能正常驾驭，阉割版（fp8）16G 就足够，nf4 版本 8-12G 显存可正常驾驭，
  - 而 gguf 格式量化的如最小的 Q2 版本 6G 显存也能够正常驾驭，而且由于 gguf 近期展现出强劲的技术发展，充分体现降低内存需求而质量更好的特点，黑暗森林官方开始全面支持，所以 nf4 的版本将逐渐淘汰。

# discuss-upscale
- examples
  - [SD 1.5 LCM Upscale + 4x-UltraSharp | ComfyUI Workflow](https://openart.ai/workflows/gambz/sd-15-lcm-upscale/RO8RtrOWhbNvmbCqHcav)
  - [UpscaleV2 (Tiled KSampler) + 4x_NMKD-Superscale + xl_more_art-full_v1 | ComfyUI Workflow](https://openart.ai/workflows/gambz/upscalev2-tiled-ksampler/BMt5f1o7pbIPrzBb61uT)
    - 🆚 [Upscale comparison to 1.5 | ComfyUI Workflow](https://openart.ai/workflows/gambz/upscale/jQ8rhVNNtPTGEz0SKkJ0)
  - [Model-based Pixel Upscale Workflow by UpscalePth | ComfyUI Workflow](https://openart.ai/workflows/openart/model-based-pixel-upscale-workflow/V6horzh1YQN8Pz5rJXzP)
  - [Latent Upscale Workflow: Enhance Your Base Image | ComfyUI Workflow](https://openart.ai/workflows/elim_droflem/latent-upscale-workflow-enhance-your-base-image/tdumeZf39DyTUWNDDIK8)
  - 🆚 [ComfyUI - Sd1.5 & SDXL Upscale workflow (Simple , Basic) - v1.0 | Stable Diffusion XL Workflows | Civitai](https://civitai.com/models/982843/comfyui-sd15-and-sdxl-upscale-workflow-simple-basic)
  - [ComfyUi Latent Upscaling | Civitai](https://civitai.com/articles/2685/comfyui-latent-upscaling)
  - [Simple SDXL ControlNet Upscaler Workflow for ComfyUI - v1.0 | Stable Diffusion XL Workflows | Civitai](https://civitai.com/models/1484256/simple-sdxl-controlnet-upscaler-workflow-for-comfyui)

- ## 

- ## 

- ## [WorkFlow - Choose images from batch to upscale : r/comfyui _202308](https://www.reddit.com/r/comfyui/comments/15natwz/workflow_choose_images_from_batch_to_upscale/)
- one question - the choosing that you mention. how does that work? You dont seem to click an image to choose it so you run the process twice?
  - You dont click an image, like in MJ, but you have to decide which image(s) in the batch you want to upscale and put into the "LatentSelector" box.
  - I was trying to figure out how to do a switch with integers, but couldnt figure it out. I also was playing with "LatentFromBatch" but it wasnt scalable and I was getting regens, and not the exact image i wanted to upscale.
  - I believe he does, the seed is fixed so ComfyUI skips the processes that have already executed. Once ComfyUI gets to the choosing it continues the process with whatever new computations need to be done. In this case if you enter 4 in the Latent Selector, it continues computing the process with the 4th image in the batch.

- ## 🌰 [Help a beginner navigate the upscaling options : r/comfyui _202312](https://www.reddit.com/r/comfyui/comments/18dtfg3/help_a_beginner_navigate_the_upscaling_options/)
  - I find myself overwhelmed with the number of ways to do upscaling.
  - From the ComfyUI_examples, there are two different 2-pass (Hires fix) methods, one is latent scaling, one is non-latent scaling

- I just wrote a lengthy reply to someone regarding this very thing. In my experience, 'FreeU_V2' + `PatchModelAddDownscale` is basically god mode when it comes to generating detailed images at high resolution. No other method I have tried has even come close.
  - If you want to generate really high resolution images (4k and above) the best bet is to use PatchModelAddDownscale to generate at 2k, then run that image through ultimate SD upscaler - though it should be noted that I've been able to generate desktop wallpaper sized images (3440X1440) directly using PatchModelAddDownscale.

- ## [Comfyui SDXL upscaler / hires fix : r/comfyui _202405](https://www.reddit.com/r/comfyui/comments/1d42dim/comfyui_sdxl_upscaler_hires_fix/)
  -  I wanted to get an image with a resolution of 1080x2800, while the original image is generated as 832x1216.
- Why has no one mentioned this?? Your math doesn't work. You can't upscale a 832x1216 image to 1080x2800, without seriously stretching and distorting the image.
  - You should keep the aspect ratio while upscaling. You can crop it later.
  - And you should start with the recommended resolutions for SDXL.
  - If you wanna get from 832 to 1024 and don't wanna keep the aspect ratio, it's more like an out-painting.

- Either Ultimate SD Upscale Or Supir
  - Ultimate SD upscale is good and plays nice with lower-end GFX cards, Supir is great but very resource-intensive.

- 
- 
- 
- 
- 
- 

# discuss-model-tuning
- ## 

- ## 

- ## 

- ## [ComfyUI_修剪模型的方法 - 知乎 _202502](https://zhuanlan.zhihu.com/p/16255414246)
- 有一些模型的精度为 fp32 的，以 SD1.5 模型为例，一般修剪过的 fp16 模型大小为 2G，如果是 fp32 的，则可能会达到 4G。

- 在 ComfyUI 中修剪模型十分简单便捷，首先安装 mtb 插件，这是一个综合插件，功能颇多，是我最常用的插件之一
  - 在节点 mtb--prune 中找到 Model Pruner，并将想要修剪的模型与之连接。

- ## ⚡️ [ComfyUI_提升图片生成速度 - 知乎 _202408](https://zhuanlan.zhihu.com/p/695820264)
- LCM 的模型并不多见，原因之一是其质量不太理想，之二是它刚出来没几天就有更好的 Turbo 问世。为普通模型添加 LCM Lora 模型，可以明显提升出图速度。
  - 采样器需为 `LCM` ， Scheduler 建议 `sgm_uniform。`

  - SDXL 模型不建议使用 LCM，因为有更快更好的 Lightning、Hyper 可用。

- Turbo Lora 只能用于 SDXL 模型，它的效果其实并不好，我用在出角色图时，坏图率极高，会严重拉长主体或肢体混乱。
  - Turbo Lora 对采样器没有固定要求，Scheduler 推荐` sgm_uniform`，但我用其它的也没见明显负面影响。

- Lightning 的模型越来越多，其出图品质整体上要优于 Turbo 和 LCM，对于没有采用 Lightning 技术的 SDXL 模型来说，加个 Lightning Lora 也能降低步数产出不错的图。
  - 采样器建议 `euler`，Scheduler 需使用 `sgm_uniform`。示例中我使用的是 8 Steps Lora, 其整体效果已经足够好，很接近原模型直出图了，并且在角色图形中表现要远优于 Turbo。

- 目前 Hyper Lora 有 SD1.5、SDXL、SD3、Flux1 的，它有多种步数的 Lora 可选，步数越低效果相应的差一些，8 和 12 步的效果非常不错。
  - 采样器建议 `ddim、euler a、euler`，Scheduler 需使用 `sgm_uniform`。
  - 建议使用带有 CFG 的 Lora，此类 Lora 可以使用更高的 CFG 值而不像 Lightning 那样限制在 1-2，更高的 CFG 值可以让图像有更丰富的细节。

- DMD2_SDXL_4step_lora 仅用于 SDXL 模型，采样器推荐 `LCM Karras`，步数 4-8，CFG 1。
  - DMD2 有 fp32 和 fp16 两种模型，fp16 速度要比 fp32 快不少，两者生成的图片质量并无可见差异。

- SDXL 模型的几种 Lora 对比图:
  - LCM 的图片更显柔和，但细节不理想，Turbo 的我尝试了很多参数，凡是角色图，大多都有肢体异常，单就画面质量来看，还是要比 LCM 好上不少的。
  - Lightning 的图片细节不错，画面较柔和。Hyper 的图片细节更为丰富，但有种锐化过度的感觉，而 Hyper CFG Lora 则可以用更高的 CFG 值，细节丰富且不那么锐利，画面效果要好于 Hyper Lora。此两者虽是同出字节，但 Hyper 并非 Lightning 的替代，它们之间更像是一种互补。
  - Lightning 及 Hyper 出图速度要比 DMD2 慢一些，但质量明显更优，构图较原图更接近，细节优于原图。
- 以上是使用 Lora 的方法来提升出图速度，Lora 使用方法与常规的一样，权重设置为 1 就好。
  - 目前模型网上同类的 Lora 不止这些，我尝试了下，结果和他的大模型一样，属于效果极差浪费时间的一类。
  - 只用自己顺手的就好。
- TCD 一款用于提升出图速度的插件，需搭配相应的 Lora 模型使用，但与常规 Lora 的使用方法有所不同
  - 示例图中，Hyper 画质表现优异，TCD 速度提升明显，但画面细节缺失较为严重
- TGate提升出图速度的节点，无需额外模型，能明显减少出图用时，但也会有一定的质量损失。
  - 将 TGate Apply 节点连接在模型与采样器之间，start_at 设为 0.5，如果设为 1 的话，它将不起作用。
# discuss-image
- ## 

- ## 

- ## 

- ## 

- ## 有分析称，GPT-4o 图片生成效果这么好是因为采用了自回归模型（autoregressive model）而不再是扩散模型（diffusion model）。
- https://x.com/jason2be/status/1905834259547361645
  - 如果真是这样的话，那我将再次称 DeepSeek 为神，因他们一月份开源的 Janus-Pro 图像生成模型就是自回归框架，虽然目前效果还待提升，但技术路线选择上相当于又踩对了一次。
- 这跟deepseek 没啥关系，基于transformer的图像生成22年23年就开始有了，也是一个研究热点，因为大家都想要一个统一的端到端模型既能生成文字也能生成图像。别说图像，openai 的sora 也是基于transformers
  - 是的。DeepSeek 的 Janus-Pro 创新是将自回归（AR）和扩散模型结合，但这也是有其他团队在研究的。DeepSeek 选 AR 和 GPT 选 Transformer 一样，其实都是行业技术演进的一部分。虽然是独立事件，但也暗示一些必然。
- 早就是研究热点了，包括nips24的best paper就是给了自回归的视频生成

- 机器学习就那几种模型，论文都是公开的，什么叫踩对一次？

- ## 揭秘一下一键大胸技术原理，顺便请教一下有没有更好的解决方案:
- https://twitter.com/moeimiku/status/1769285829586022574
  1. 通过 SagmentAnyThing + Grounding-DINO识别乳沟和胸部，然后做叠加遮罩~  
  2. 利用StableDiffution对遮罩区域做基于原图的重绘
  - 现在遇到的问题是，灵敏度默认0.3的情况下不能覆盖所有图片：有的图片识别不出来，需要降低到0.25. 有的图片把全身都识别出来了，则需要增加灵敏度。
- 可以加个遮罩层区域抹涂编辑功能，既能解决准确性的问题，又会大大增加产品的趣味性和粘性。
  - 靠谱，还想做一键穿丝袜功能
- 这个通过拖拽构建系统的框架是什么？
  - comfyUI 关注我回头出教程

- ## [how to image generate locally? : r/ollama _202505](https://www.reddit.com/r/ollama/comments/1kjhul8/how_to_image_generate_locally/)
- r/StableDiffusion would be the place to ask. There are a couple different UIs like ComfyUI, Fooocus, Forge, and SwarmUI that can be used to do local generation.

- ## [How to generate text to image with ollama? · Issue · ollama/ollama-python _202409](https://github.com/ollama/ollama-python/issues/280)
- You need to know what's a LLM and how it work: llm stand for large language model, which basically mean it a model made to understand language, and can reply with similar language, understandable for human.
  - what you're trying to do is to have this llm generate an image, without being train on generating image but only generating text... So its impossible to have the model nativly provide you an image by its own.
  - If you're looking to have a chatbot capable of chatting and generating image, you must have two AI, one LLM and one made to generate image (like stable diffusion, etc), if you have a good computer, you can run both locally

- ## 这几天在研究Stable Diffusion。需求是把客户做的衣服穿到AI生成的模特身上。
- https://twitter.com/felixding/status/1768511354208739692
  - 如果用一张衣服的照片+ControlNet，结果的细节总是不够，因为本来就只用了一张照片。
  - 如果用多张衣服的照片训练个Lora，结果就变得不可控了，比如衣服的细节总是和真实情况不完全一样。
- 细节还原很难，看看这几个方案呢
  - 1、OOTDiffusion
  - 2、一张参考服装、一张参考动作
  - 3、OutfitAnyone，未开源，可以在线用
- 我试过了。唯一可行的技术方案是用身模实拍，用sd生成人头和背景然后组合起来。最大的BUG在于同样的输入条件，语言输入的扩散模型，结果一定会有至少15%的偏差。用图生图的话，流程复杂，边缘结合部还处理不好。技术上暂时无解。
- 你用ControlNet了吗？我用Inpaint Anything+Segment Anything，然后丢给ContrlNet，这样似乎还行，但是就会遇到我说的第一个问题。
  - ControlNet我玩得透透的，这是SD最有价值的插件，本意就是用来解决结果偏差问题的。透过骨骼、边界、边缘三层约束，可以最大化的解决结果偏差问题。但也只能缩小结果偏差。只要无法做到可复制、可控制，就没有产量，无法成为可规模生产的工具，这个我早就看穿了。

- ## DALLE3 ChatGPT 输出的风格似乎很稳定，太美了！
- https://twitter.com/lencx_/status/1721331238219506111

- ## 🆚️ 用 Midjourney、DALL-E 3、Adobe Firefly 2 还是 Stable Diffusion？
- https://twitter.com/FinanceYF5/status/1716288468186431811
  - 在过去的 6 个月里，作者在所有 4 个平台上生成了 50, 000 多张图像。

- ## 🧮 开个 thread 来做个人人都难懂的 AI 作画科普。
- https://twitter.com/haoel/status/1632211302356783104
- 目前主要流行的AI作画有，OpenAI的Dall-E2, Google 的 Imagen，Midjourney，有还Stability AI 公司开的 Stable Diffusion 等等。
  - 它们都是2022年才出来的，无一例外，全部都是基于 Diffusion 算法模型，这个算法的原理其实并不复杂

- 💡 最后说一下Stable Diffusion，他使用了一种图片压缩算法可以大规模的减少训练的内存和时间，在工程上可以用更少的GPU和时间来计算更大量的数据，于是让“大力出奇迹”成为了可能，
  - 因为开源，所以，它的社区是非常活跃的。开源和封闭的竞争永远都在，OpenAI 和Stability AI之间就像苹果和安卓

- Diffusion算法需要先找一堆高质量的图片，训练就是对每张图片一步一步的按一种公式（高斯噪声公式）来加噪点，直到整张图片变成一个完全噪点的图像（就像电视的雪花点），把所有的步骤都保存下来，然后用神经网络的方式来反向学习如何从一个完全是噪点的图像变成一张高清的图
  - 一旦这个模型产生，机器就可以通过“噪点”来预测图形，所以，整个绘画的过程就是用一组随机数（随机的噪点）来预测会是一个什么样的画。很令人惊讶吧，AI就是从一堆乱七八糟的随机数中来画画的。这种个算法很机器，就是以大力出奇迹，但牛逼的地方是，可以产生清晰度和细节度巨高无比的图片
- 这个过程需要依赖于几个事，一个是训练的图片，一个初始化的随机噪点，还有就是 Prompt 的预测路径，整个过程非常地机械，而且这个模型也不保证能生成让人觉得舒服的图片，所以需要各种人为的调参，并需要人通过在生成的图片中选择自己喜欢的图片后再度生成，类似于ChatGPT用上下文来调整内容
- 💡 所以，像Midjourney这种通过聊天机器人来让人选择最喜欢的图片，其实就是让人来告诉机器哪些随机数，哪些预测路径，哪些Prompt更靠谱可生成更好的图片，在用户生成图片的同时让用户来反哺了AI 模型，而生成出来的图片又可以成为下一轮的图片训练集，于是，AI以后就再也不需要使用人类的图片
- 再说一下 **Prompt**，这是一种Transformer语言模型，它接受文本提示并产生Token，
  - Stable Diffusion 以前使用的是 OpenAI的CLIP，但去年11月切到了OpenCLIP，使用了3.5亿的参数，而CLIP只有6千万的参数，
  - Prompt对高质量的图片的生成有非常大的影响因素，我认为这是一种未来的更接近自然语言的编程语言
