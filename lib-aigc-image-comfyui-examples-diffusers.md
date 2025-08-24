---
title: lib-aigc-image-comfyui-examples-diffusers
tags: [comfyui, diffusers, examples, image]
created: 2025-08-23T11:43:02.194Z
modified: 2025-08-23T11:43:35.904Z
---

# lib-aigc-image-comfyui-examples-diffusers

# guide

# popular
- https://github.com/invoke-ai/InvokeAI /25.8kStar/apache2/202508/python/ts
  - https://invoke-ai.github.io/InvokeAI/
  - Invoke is a leading creative engine for Stable Diffusion models 
  - Invoke has a Community Edition that is freely available under a commercially-friendly license (Apache 2) and a Professional Edition available
  - Invoke is a powerful, secure, and easy-to-deploy generative AI platform for professional studios that provides a flexible workflow builder with multi-user sharing and permissions, a step-by-step custom AI model trainer
  - Invoke ensures that all integrated open-source technologies are commercially friendly, making it viable to use for commercial projects.
  - 🆚 [Why Invoke AI is the Best ComfyUI Alternative](https://www.invoke.com/comparisons/comfyui-vs-invokeai)
  - 🎯 [Invoke AI 3.0 Release : r/StableDiffusion _202307](https://www.reddit.com/r/StableDiffusion/comments/155sm30/invoke_ai_30_release/)
    - As of 3.0, all of the developments we’ve been working on are now available to install and use - And, to demonstrate our commitment to open-source, we’ve updated our license to the most explicitly permissive license available - Apache 2.0.

- https://github.com/comfyanonymous/ComfyUI /85.4kStar/GPLv3/202508/python
  - https://www.comfy.org/
  - The most powerful and modular diffusion model GUI, api and backend with a graph/nodes interface.
  - ComfyUI lets you design and execute advanced stable diffusion pipelines using a graph/nodes/flowchart based interface. 
  - Available on Windows, Linux, and macOS.
  - Image Models: SD1.x, SD2.x, SDXL, Flux, Qwen Image, HiDream
  - Image Editing Models: Flux Kontext, HiDream, Omnigen 2
  - Video Models: Stable Video Diffusion, Mochi, Hunyuan, Wan
  - Audio Models: Stable Audio, ACE Step
  - 3D Models: Hunyuan3D 2.0
  - Asynchronous Queue system
  - Many optimizations: Only re-executes the parts of the workflow that changes between executions.
  - Smart memory management: can automatically run large models on GPUs with as low as 1GB vram with smart offloading.
  - Works even if you don't have a GPU with: --cpu (slow)
  - Loras (regular, locon and loha)
  - Loading full workflows (with seeds) from generated PNG, WebP and FLAC files.
  - Works fully offline: core will never download anything unless you want to.
  - ⚙️ 配置GPU运行模式的文件在 `~/Library/Application Support/ComfyUI/config.json`, 同时配置启动参数文件在 `~/Documents/ComfyUI/user/default/comfy.settings.json` ; 
  - https://github.com/Comfy-Org/ComfyUI_frontend /GPL/202508/ts/vue
    - Official front-end implementation of ComfyUI
    - Backend: Dev server expects ComfyUI backend at http://localhost:8188 by default
    - 依赖vue-router、pinia、vuefire、tiptap-markdown、marked、three、jsondiffpatch
  - [Server Config - ComfyUI](https://docs.comfy.org/interface/settings/server-config)
    - host: Sets the IP address the server binds to. Default `127.0.0.1` means only local access is allowed. If you need LAN access, you can set it to `0.0.0.0`.
    - port: Desktop version defaults to port `8000`, Web version typically uses port `8188`.

- https://github.com/mcmonkeyprojects/SwarmUI /3kStar/MIT/202508/csharp/js
  - SwarmUI (formerly StableSwarmUI), A Modular Stable Diffusion Web-User-Interface, with an emphasis on making powertools easily accessible, high performance, and extensibility
  - Beginner users will love Swarm's primary Generate tab interface with a variety of powerful features. 
  - Advanced users may favor the Comfy Workflow tab to get the unrestricted raw graph, but will still have reason to come back to the Generate tab for convenience features (image editor, auto-workflow-generation, etc) and powertools (eg Grid Generator).
  - 💡 has the option to use as a backend AUTOMATIC1111/stable-diffusion-webui (AGPL).
    - A1111 stopped. So why would you support it?
  - [Same workflow significantly faster with SwarmUI vs. ComfyUI? : r/StableDiffusion _202502](https://www.reddit.com/r/StableDiffusion/comments/1if36so/same_workflow_significantly_faster_with_swarmui/)
    - SwarmUI is prolly using the native fp8 boost of RTX 40 cards by default, you have to set ComfyUI to fast for that. That gives you roughly a 30% boost.
    - Just to be clear: in ComfyUI in the Load Diffusion Model node set weight_dtype to fp8_e4m3fn_fast instead of fp8_e4m3fn
  - [Best way to use Qwen Image on Linux? : r/LocalLLaMA _202508](https://www.reddit.com/r/LocalLLaMA/comments/1mmx3cg/best_way_to_use_qwen_image_on_linux/)
    - It's a fairly standard UI that sits on top of it's own comfy instance. 
    - It supports nearly everything that comfyui does, and makes the full comfyUI available as a built-in tab for when you need custom workflows not doable with the main UIs parameters.
  - https://github.com/Stability-AI/StableSwarmUI /MIT/202406/csharp/inactive
    - A Modular Stable Diffusion Web-User-Interface, with an emphasis on making powertools easily accessible, high performance, and extensibility.
    - As of 2024/06/21 StableSwarmUI will no longer be maintained under Stability AI.

- https://github.com/vladmandic/sdnext /6.5kStar/AGPL > apache2/202508/python
  - https://vladmandic.github.io/sdnext-docs/
  - All-in-one WebUI for AI generative image and video creation
  - Built-in Control for Text, Image, Batch and Video processing
  - Interrogate/Captioning with 150+ OpenCLiP models and 20+ built-in VLMs
  - Built in installer with automatic updates and dependency management
  - [Backend](https://github.com/vladmandic/sdnext/wiki/Backend)
    - SD.Next supports two main backends: Diffusers and Original
    - Diffusers: Based on new Huggingface Diffusers implementation. This backend is set as default for new installations
    - Original: Based on LDM reference implementation and significantly expanded on by A1111. Supports SD 1.x and SD 2.x models
    - All other model types such as SD-XL/SD3, LCM, Stable Cascade, PixArt, Playground, Segmind, Kandinsky, etc. require backend Diffusers
  - [Changelog](https://vladmandic.github.io/sdnext-docs/CHANGELOG/?h=comfyui#details-for-2025-07-29)
    - 2025-07-29: switched from aGPL-v3.0 to Apache-v2.0
    - 2024-05-28: SD.Next is no longer marked as a fork of A1111 and github project has been fully detached
    - 但原版A1111一开始就是AGPL license且未改变过

- https://github.com/AUTOMATIC1111/stable-diffusion-webui /156kStar/AGPL/202407/python/inactive
  - A web interface for Stable Diffusion, implemented using Gradio library.
  - Custom scripts with many extensions from community
  - 4GB video card support (also reports of 2GB working)
  - https://github.com/AUTOMATIC1111/stable-diffusion-webui-extensions
    - Stable Diffusion web UI accesses index.json from this repo to show user the list of available extensions.
  - [What automatic1111 forks are still being worked on? Which is now recommended? : r/StableDiffusion _202505](https://www.reddit.com/r/StableDiffusion/comments/1khrqcc/what_automatic1111_forks_are_still_being_worked/)
  - https://github.com/AbdBarho/stable-diffusion-webui-docker
  - https://github.com/gradio-app/gradio /39.6kStar/apache2/202508/python/ts/svelte
    - http://www.gradio.app/
    - Gradio is an open-source Python package that allows you to quickly build a demo or web application for your machine learning model, API, or any arbitrary Python function.
    - You can then share a link to your demo or web application in just a few seconds using Gradio's built-in sharing features.

- https://github.com/modelscope/DiffSynth-Studio /9.7kStar/apache2/202508/python
  - DiffSynth-Studio 是由魔搭社区团队开发和维护的开源 Diffusion 模型引擎。
  - 似乎是image/video-gen的平台，能提供最新的阿里模型，类似在线IDE能配置运行环境GPU、模型参数、lora/controlnet
  - DiffSynth-Studio is an open-source Diffusion model engine developed and maintained by ModelScope team. 
  - DiffSynth currently includes two open-source projects
  - DiffSynth-Studio: Focused on aggressive technical exploration, for academia, providing support for more cutting-edge model capabilities.
  - DiffSynth-Engine: Focused on stable model deployment, for industry, offering higher computing performance and more stable features.
  - DiffSynth-Studio and DiffSynth-Engine are the core projects behind ModelScope AIGC zone https://modelscope.cn/aigc/home
  - [阿里魔搭社区开源了一款强力引擎：DiffSynth Studio，带你轻松生成图像和视频 - 知乎 _202410](https://zhuanlan.zhihu.com/p/1035820317)
    - 一款开源图像和视频生成整合引擎
    - 提供了两种非常友好的 WebUI 版本——Gradio 和 Streamlit
  - DiffSynth-Studio redesigns the inference and training pipelines for mainstream Diffusion models (including FLUX, Wan, etc.), enabling efficient memory management and flexible model training.
  - changelog
    - March 25, 2025 Our new open-source project, DiffSynth-Engine, is now open-sourced! Focused on stable model deployment. 
    - Dec 8, 2023. We decide to develop a new Project, aiming to release the potential of diffusion models, especially in video synthesis. The development of this project is started.
    - 🚀 Aug 29, 2023. We propose DiffSynth, a video synthesis framework.
  - https://github.com/modelscope/DiffSynth-Engine /apache2/202508/python
    - a high-performance engine geared towards building efficient inference pipelines for diffusion models.
    - Thoughtfully-Designed Implementation: We carefully re-implemented key components in Diffusion pipelines, such as sampler and scheduler, without introducing external dependencies on libraries like k-diffusion, ldm, or sgm.
    - Extensive Model Support: Compatible with popular formats (e.g., CivitAI) of base models and LoRA models
    - Comprehensive support for varous model quantization (e.g., FP8, INT8) and offloading strategies
    - Cross-Platform Support: Runnable on Windows, macOS (Apple Silicon), and Linux
  - https://github.com/AIFSH/ComfyUI-DiffSynth-Studio /apache2/202408/python
    - make DiffSynth-Studio availabe in ComfyUI

- https://github.com/easydiffusion/easydiffusion /10.1kStar/MIT-like/202508/python/js
  - https://easydiffusion.github.io/
  - An easy 1-click way to create beautiful artwork on your PC using AI
  - Provides a browser UI for generating images from text prompts and images.
  - Supports: "Text to Image", "Image to Image" and "InPainting"
  - Live Preview: See the image as the AI is drawing it. 比如upscale前就显示预览
  - [what happened? Why is the performance so poor? Before run much faster _202406](https://github.com/easydiffusion/easydiffusion/issues/1807)
    - I can think of two possibilities: maybe the version of torch has switched to CPU-only, or you're using the newer NVIDIA drivers.

- https://github.com/comfy-addons/comfyui-sdk /MIT/202508/ts
  - TypeScript SDK for seamless interaction with the ComfyUI API. 
  - This SDK significantly simplifies the complexities of building, executing, and managing ComfyUI workflows, all while providing real-time updates and supporting multiple instances
  - Construct and manipulate intricate ComfyUI workflows effortlessly using a fluent, intuitive builder pattern
  - Multi-Instance Management: Handle a pool of ComfyUI instances with ease, employing flexible queueing strategies for optimal resource utilization.
  - Subscribe to WebSocket events for live progress tracking, image previews, and error notifications.
  - Custom WebSocket Support: Supply your own WebSocket implementation for greater flexibility
  - Supports Basic Auth, Bearer Token, and Custom Authentication Headers
  - Extension Support: Seamlessly integrate with ComfyUI Manager and leverage system monitoring
  - Examples: Includes practical examples for Text-to-Image (T2I), Image-to-Image (I2I), and complex multi-node workflows

- https://github.com/SaladTechnologies/comfyui-api /218Star/MIT/202508/ts
  - A simple API server to make ComfyUI easy to scale horizontally. 
  - Get outputs directly in the response, or receive them via webhook or s3.
  - A simple wrapper that facilitates using ComfyUI as a stateless API, either by receiving images in the response, or by sending completed images to a webhook
  - The server supports the full ComfyUI /prompt API, and can be used to execute any ComfyUI workflow.
  - Stateless API: The server is stateless, and can be scaled horizontally to handle more requests.

- https://github.com/BennyKok/comfyui-deploy /1.4kStar/AGPL/202508/python/ts
  - https://www.comfydeploy.com/
  - open source `vercel` like deployment platform for Comfy UI
  - Open source comfyui deployment platform, a vercel for generative workflow infra. (serverless hosted gpu with vertical intergation with comfyui)
  - Stack: Clerk (Auth), NextJS, Drizzle (ORM), Neon / Vercel Postgres, R2 / S3 (Object Storage)

- https://github.com/Good-Dream-Studio/ComfyUI-Connect /MIT/202507/python
  - Expose your workflows into HTTP endpoints directly from ComfyUI itself.
  - Auto Documentation - Show all your workflows in OpenAPI format using `/api/connect` internal endpoint
  - Install by cloning this project into your `custom_nodes` folder.
  - [Made a custom node to turn ComfyUI into a REST API : r/comfyui _202505](https://www.reddit.com/r/comfyui/comments/1kef4xo/made_a_custom_node_to_turn_comfyui_into_a_rest_api/)

- https://github.com/heshengtao/comfyui_LLM_party /1.9kStar/AGPL/202508/python
  - aims to develop a complete set of nodes for LLM workflow construction based on comfyui as the front end. 
  - It allows users to quickly and conveniently build their own LLM workflows and easily integrate them into their existing image workflows.

- https://github.com/pollinations/pollinations /2.7kStar/MIT/202508/python
  - https://pollinations.ai/
  - https://text.pollinations.ai/
  - an open-source gen AI startup based in Berlin, providing the most easy-to-use, free text and image generation API available
  - 100% Open Source
  - 🖼️ Free AI image and text generation APIs
  - privacy: No logins, no keys, no data stored
  - ❓ 是否方便定制agentic的提示词和流程
  - 🎵 Audio generation: Text-to-speech and speech-to-text capabilities
  - Easy-to-use React hooks (React Hooks Examples)
  - Autonomous Development: Features implemented by our MentatBot coding assistant through GitHub issues
  - Our MCP server enables AI assistants like Claude to generate images and audio directly.
  - https://github.com/pollinations/pollinations/blob/master/APIDOCS.md
    - 可在线测试图片生成的api https://image.pollinations.ai/prompt/excel_logo /在url直接修改提示词
    - https://pollinations.ai/p/excel_logo 会重定向到上面的地址
  - 🏘️ `image.pollinations.ai/`: Backend service for image generation and caching with Cloudflare Workers and R2 storage.
  - `text.pollinations.ai/`: Backend service for text generation.
  - Future Developments
    - Digital Twins: Creating interactive AI-driven avatars
    - Music Video Generation
    - Real-time AI-driven Visual Experiences
  - [Add Dreamshaper and Turbo server as fallbacks for image generation _202504](https://github.com/pollinations/pollinations/issues/1837)
    - Currently, the image generation pipeline only falls back to ComfyUI when Cloudflare Flux fails. This enhancement adds two additional fallback options

- https://github.com/guoyww/AnimateDiff /11.7kStar/apache2/202407/python/inactive
  - https://animatediff.github.io/
  - the official implementation of AnimateDiff [ICLR2024 Spotlight]. 
  - It is a plug-and-play module turning most community text-to-image models into animation generators, without the need of additional training.
  - Note: The `main` branch is for Stable Diffusion V1.5; for Stable Diffusion XL, please refer `sdxl-beta` branch.
  - AnimateDiff is also officially supported by Diffusers. 
  - We created a Gradio demo to make AnimateDiff easier to use. 
  - https://github.com/Kosinkadink/ComfyUI-AnimateDiff-Evolved /3.3kStar/apache2/202508/python
    - Improved AnimateDiff for ComfyUI and Advanced Sampling Support
# ai-image-generator
- tips
  - midjourney alternative

- https://github.com/ammaarreshi/openjourney /135Star/MIT/202507/ts
  - https://openjourney.replit.app/
  - Open-source clone of the MidJourney web interface featuring real AI image and video generation powered by Google's Gemini SDK. 
  - Use Imagen 4 to generate images and Veo 2 and 3 for image and text to video with audio.
  - 4-image grid layout matching MidJourney's design
  - 依赖nextjs、framer-motion、shadcn-ui

- https://github.com/Nutlope/logocreator /5.5kStar/NALic/202501/ts/inactive
  - https://www.logo-creator.io/
  - A free + OSS logo generator powered by Flux on Together AI
  - Flux Pro 1.1 on Together AI for logo generation
  - nextjs + shadcn + redis + clerk + plausible
  - Create a .env file and add your Together AI API key 
  - [license · Issue · Nutlope/logocreator](https://github.com/Nutlope/logocreator/issues/16)

- https://github.com/Nutlope/blinkshot /NALic/202505/ts
  - https://www.blinkshot.io/
  - An open source real-time AI image generator. 
  - Powered by Flux through Together.ai.
  - Flux Schnell from BFL for the image model
  - Together AI for inference

- https://github.com/premieroctet/photoshot /3.8kStar/MIT/202412/ts
  - open-source AI avatar generator web app
  - 依赖nextjs、chakra-ui、prisma
  - Replicate, a platform for running machine learning models in the cloud

- https://github.com/rogeriochaves/pictureit-editor /38Star/MIT/202304/ts/inactive
  - an open-source design editor, currently in beta version, designed to be a studio to help you create and iterate on digital art using a variety of AI models available as tools in the editor
  - Picture it Editor was not built to run the model locally on your machine, this is because running models is not the focus of this project, the focus really is on the user experience
  - 🏠 Instead, Picture it uses Replicate as the API to run the models, the advantage of that is that the editor is able to use many models at the same time with no setup or the need of a powerful GPU
  - Replicate as a Backend: need a Replicate API key
  - [Picture it Editor: Open-source AI editor for Stable Diffusion : r/StableDiffusion _202301](https://www.reddit.com/r/StableDiffusion/comments/10dwamp/picture_it_editor_opensource_ai_editor_for_stable/)

- https://github.com/AIDC-AI/ComfyUI-Copilot /2.5kStar/MIT/202508/python/ts
  - ComfyUI-Copilot is an AIGC intelligent assistant built on ComfyUI that provides comprehensive support for tedious workflow building, ComfyUI-related questions, parameter optimization and iteration processes
  - 🎯v2-20250814: v2.0 evolves from a "helper tool" into a "development partner"—not just assisting with workflow development, but capable of autonomously completing development tasks.
  - We now cover the entire workflow lifecycle, including generation, debugging, rewriting, and parameter tuning, aiming to deliver a significantly enhanced creative experience.
  - Debug:：Automatically detects errors in your workflow, precisely identifies issues, and provides repair suggestions.
  - Workflow Rewriting：Optimizes the current workflow based on your description, such as adjusting parameters, adding nodes, and improving logic.
  - Enhanced Workflow Generation：Understands your requirements more accurately and generates tailored workflows
  - Upgraded Agent Architecture：Now aware of your local ComfyUI environment, Copilot delivers optimized, personalized solutions.
  - [Please add local Ai model support (no internet connection required) _202504](https://github.com/AIDC-AI/ComfyUI-Copilot/issues/57)
    - The adoption of the locally deployed model you mentioned is indeed a good idea, and we have considered related optimizations.
    - However, because there are many external data warehouses behind our project, and the entire project uses the Agent tool calling framework, the use of a smaller LLM model will cause the accuracy of the response to drop significantly, so we have abandoned this iterative solution in the short term.
    - In the future, from the perspective of upgrading the entire framework, we will also consider using a small large language model to drive the entire project, and then make relevant updates.
    - I think that adding integration with litellm should be reasonable, there are many MLLMs and LLMs that are supported in vllm that can be called through it. If someone is going to run comfyui in a solid computing environment, it is quite reasonable to self-host LMs
  - [Local AI model _202502](https://github.com/AIDC-AI/ComfyUI-Copilot/issues/12)
# comfyui-like
- https://github.com/oobabooga/text-generation-webui /44.8kStar/AGPLv3/202508/python
  - https://oobabooga.gumroad.com/l/deep_reason
  - A Gradio web UI for Large Language Models.
  - Supports multiple local text generation backends, including llama.cpp, Transformers, ExLlamaV3, ExLlamaV2, and TensorRT-LLM (the latter via its own Dockerfile).
  - 100% offline and private, with zero telemetry, external resources, or remote update requests.
  - Vision (multimodal models): Attach images to messages for visual understanding
  - Web search: Optionally search the internet with LLM-generated queries to add context to the conversation.
  - Extension support, with numerous built-in and user-contributed extensions available

- https://github.com/PySpur-Dev/PySpur /5.4kStar/apache2/202507/python/ts
  - https://pyspur.dev/
  - A visual playground for agentic workflows: use it to build agents, execute them step-by-step and inspect past runs.
  - Build the agent in Python code or via UI
  - Human in the Loop: Persistent workflows that wait for human approval.
  - Structured Outputs: UI editor for JSON Schemas.
  - RAG: Parse, Chunk, Embed, and Upsert Data into a Vector DB.
  - Multimodal: Support for Video, Images, Audio, Texts, Code.
  - Python-Based: Add new nodes by creating a single Python file.
  - By default, this will start PySpur app at http://localhost:6080 using a sqlite database.
  - Using Local Models with Ollama: PySpur only works with models that support structured-output and json mode. Most newer models should be good
  - [ComfyUI for LLMs : r/comfyui _202412](https://www.reddit.com/r/comfyui/comments/1hgfy3g/comfyui_for_llms/)
# examples

# extensions/custom-node

- https://github.com/Taremin/webui-monaco-prompt /MIT/202502/ts
  - Editors such as `CLIPTextEncode` and note are replaced with the Monaco Editor used in VSCode.
  - This extension introduces an autocomplete feature and provides the option to switch to a vim-style keymap.
  - https://x.com/Teslanaut/status/1896379544724295978
    - Is there a @ComfyUI extension for VSCode? I'm surprised there isn't. 
    - To be able to generate or have your AI co-pilot agent generate icon images, logos, or any other images or maybe even video you need for your website or book would be quite an interesting thing to add to your workflow. 

- https://github.com/talesofai/comfyui-browser /NALic/202411/python/svelte/inactive
  - This is an image/video/workflow browser and manager for ComfyUI. 
  - You can sync your workflows to a remote Git repository and use them everywhere.
  - Browse and manage your images/videos/workflows in the output folder.
  - Some useful custom nodes like xyz_plot, inputs_select.
  - Install ComfyUI Manager, search comfyui-browser in Install Custom Node and install it.

- https://github.com/neverbiasu/ComfyUI-ChatTTS /MIT/202505/python
  - A ComfyUI integration for ChatTTS, enabling high-quality, controllable text-to-speech generation directly in your ComfyUI workflows.
  - Load the ChatTTS model, Sample a random speaker voice, Convert text to speech
  - Batch Processing - Support for batch text processing through split_batch option
  - https://github.com/2noise/ChatTTS /AGPL/202505
    - https://2noise.com/
    - This repo contains the algorithm infrastructure and some simple examples.
    - ChatTTS is a text-to-speech model designed specifically for dialogue scenarios such as LLM assistant.
    - The main model is trained with Chinese and English audio data of 100,000+ hours.
    - The open-source version on HuggingFace is a 40,000 hours pre-trained model without SFT.
    - The released model is for academic purposes only.
    - The model is published under CC BY-NC 4.0 license. It is intended for educational and research use, and should not be used for any commercial or illegal purposes

- https://github.com/stavsap/comfyui-ollama /622Star/apache2/202508/python
  - Custom ComfyUI Nodes for interacting with Ollama using the ollama python client.
  - Integrate the power of LLMs into ComfyUI workflows easily or just experiment with LLM inference.

- https://github.com/kijai/ComfyUI-moondream /202403/python/inactive
  - ComfyUI node to use the moondream tiny vision language model

- https://github.com/gokayfem/ComfyUI_VLM_nodes /apache2/202502/python/inactive
  - Custom ComfyUI nodes for Vision Language Models, Large Language Models, Image to Music, Text to Music, Consistent and Random Creative Prompt Generation
  - Utilizes `llama-cpp-python` for integration of LLaVa models. You can load and use any VLM with LLaVa models in GGUF format with this nodes.

- https://github.com/if-ai/ComfyUI-IF_AI_PromptImaGen /MIT/202504/python
  - Lighter version of ComfyUI-IF_AI_tools is a set of custom nodes to Run Local and API LLMs and LMMs, supports Ollama, LlamaCPP LMstudio, Koboldcpp, TextGen, Transformers or via APIs Anthropic, Groq, OpenAI
  - https://github.com/if-ai/ComfyUI-IF_AI_tools /MIT/202412/python/inactive
    - https://ko-fi.com/impactframes
    - a set of custom nodes for ComfyUI that allows you to generate prompts using a local Large Language Model (LLM) via Ollama.
    - I am Moving the prompt generation to this new node PromptImaGen 
# utils
- https://github.com/AIDC-AI/Pixelle-MCP /271Star/MIT/202508/python
  - https://pixelle.ai/
  - Open-Source Multimodal AIGC Solution based on ComfyUI + MCP + LLM
  - An AIGC solution based on the MCP protocol, seamlessly converting ComfyUI workflows into MCP tools
  - Server-side is built on ComfyUI, inheriting all capabilities from the open ComfyUI ecosystem

- https://github.com/joenorton/comfyui-mcp-server /97Star/apache2/202503/python/inactive
  - lightweight Python-based MCP server that interfaces with a local ComfyUI instance to generate images programmatically via AI agent requests.
  - This project enables AI agents to send image generation requests to ComfyUI using the MCP protocol over WebSocket. 
  - Returns image URLs served by ComfyUI.
  - Dependencies: requests, websockets, mcp
  - https://github.com/Overseer66/comfyui-mcp-server

- https://github.com/lalanikarim/comfy-mcp-server /MIT/202503/python/inactive
  - A server using FastMCP framework to generate images based on prompts via a remote Comfy server.
  - https://github.com/lalanikarim/langgraph-mcp-pipeline /MIT/202503/python
    - This project demonstrates the use of the Model Context Protocol (MCP) with LangGraph to create workflows that generate prompts and AI-generated images based on a given topic. 
    - These scripts utilize the Comfy MCP Server to generate AI image prompts and AI images.
  - https://github.com/lalanikarim/comfy-mcp-pipeline
    - a pipeline wrapper for comfy-mcp-server for Open WebUI.

- https://github.com/daxcay/ComfyUI-Nexus /MIT/202503/python/inactive
  - A ComfyUI node designed to enable seamless multi-user workflow collaboration.
  - This node should only be installed on the server machine.
  - Other users don’t need to install this node.
  - Editor Permissions: Editors can only edit the graph

- https://github.com/Limitex/ComfyUI-Diffusers /MIT/202502/python/inactive
  - a custom node in ComfyUI. This is a program that allows you to use Huggingface Diffusers module with ComfyUI. 
  - Additionally, Stream Diffusion is also available.

- https://github.com/apppps/comfyui-agent /53Star/GPLv3/202504/python/inactive
  - It reflects the BASE flow nodes in real time and can be directly supervised by the AI.
  - The agent can judge the settings and recommend prompts, connection status, and various numbers.
  - system default ai chatgpt-4o-mini. and you needs chatgpt api.
  - [Comfyui Agent on Github : r/comfyui _202504](https://www.reddit.com/r/comfyui/comments/1jztequ/comfyui_agent_on_github/)
    - judging by the things you can define in ai_agent_api.py, you can at least also use lm-studio instead, maybe ollama too
    - You're describing full blown vibe coding. We're not there yet unfortunately.
    - I've spent the whole day yesterday trying to set up a workflow with several agents supervising eachother. I was running the local ollama codellama and gemma3. 
    - Turns out those local models aren't very bright. And the llm nodes from klm_party somehow dont support json format templates. So that was a complete mess.
    - https://github.com/AIDC-AI/ComfyUI-Copilot Vibe coding is now reality. I wonder if local possible though, because it is true some local llm are too dumb for these tasks.

- https://github.com/ComfyWorkflows/ComfyUI-Launcher /AGPLv3/202403/python/inactive
  - Run any ComfyUI workflow w/ ZERO setup.
  - Each workflow runs in its own isolated environment
  - [I made an open source tool for running any ComfyUI workflow w/ ZERO setup : r/comfyui _202403](https://www.reddit.com/r/comfyui/comments/1b8okxb/i_made_an_open_source_tool_for_running_any/)
    - each project created in comfyui launcher has its own virtualenv (so this will let you create a new isolated project for running workflows that require different dependencies than your other workflows), but the models folder is shared across all projects.
    - the reasoning behind this is that this setup allows you to run different workflows w/ different requirements, while not having to duplicate any models across them.

- https://github.com/cumulo-autumn/StreamDiffusion /10.4kStar/apache2/202412/python/inactive
  - StreamDiffusion is an innovative diffusion pipeline designed for real-time interactive generation.
  - Streamlined data processing through efficient batch operations.
  - Improved guidance mechanism that minimizes computational redundancy.
  - Improves GPU utilization efficiency through advanced Stochastic Similarity Filter.

- https://github.com/RishiDesai/CharForge /MIT/202506/python
  - https://www.charforge.dev/
  - Generate character consistent images with a single reference
  - 48GB is preferred, but you can get by with 24GB
  - [Generate character consistent images with a single reference (Open Source & Free) : r/StableDiffusion _202506](https://www.reddit.com/r/StableDiffusion/comments/1lkezo2/generate_character_consistent_images_with_a/)
    - I built a tool for training Flux character LoRAs from a single reference image, end-to-end.
# workflows
- https://github.com/dicksondickson/dickson-sci-fi-enhance-upscale /202505
  - These are ComfyUI workflows to upscale images to 2K, 4K, or 8K.
  - These workflows upscales images in multiple stages using a combination of upscaling models, CCSR, SUPIR and Ulitmate SD Upscale, upscaling models, SDXL and Flux.
  - Each workflow is tuned to a specific resolution with different speed variants. These workflows are continuing evolving.
# ai-image-provider
- https://github.com/Stability-AI/stablediffusion /Stable Diffusion Version 2
  - https://github.com/CompVis/stable-diffusion
  - A latent text-to-image diffusion model

- https://github.com/camenduru/stable-diffusion-webui-portable
  - This Project Aims for 100% Offline Stable Diffusion (People without internet or with slow internet can get it via USB or HD-DVD)

- https://github.com/cmdr2/stable-diffusion-ui
  - The easiest way to install and use Stable Diffusion on your computer.

- https://github.com/joanrod/star-vector /apache2/202503/python
  - https://starvector.github.io/
  - StarVector is a foundation model for SVG generation that transforms vectorization into a code generation task. 
  - Using a vision-language modeling architecture, StarVector processes both visual and textual inputs to produce high-quality SVG code with remarkable precision.
  - It can be used to perform image2SVG and text2SVG generation. We pose image generation as a code generation task, using the power of multimodal VLMs
  - March 2025: StarVector Accepted at CVPR 2025
  - SVGBench and SVG-Stack datasets are now available on HuggingFace Datasets
    - https://huggingface.co/datasets/starvector/svg-bench
    - https://huggingface.co/datasets/starvector/svg-stack
# sd-api/server
- https://github.com/Netwrck/stable-diffusion-server /53Star/MIT/202507/python
  - Image Generation API Server - Similar to https://text-generator.io but for images
  - Simple interface for generating images in Gradio locally and easy to use FastAPI docs/server for advanced users.
  - Running the Gradio UI: python gradio_ui.py
  - Local Deployment: Run locally for style transfer, art generation and inpainting.
# sd-ui/webapp
- https://github.com/Stability-AI/StableStudio /9kStar/MIT/202306/ts/inactive
  - StableStudio is Stability AI's official open-source variant of DreamStudio, our user interface for generative AI.
  - It is a web-based application that allows users to create and edit generated images. 
  - What's the difference between StableStudio and DreamStudio?
    - All "over-the-wire" API calls have been replaced by a plugin system which allows you to easily swap out the back-end.
    - you can create your own plugin and use StableStudio with any back-end you want
  - [`ComfyUI` plugin _202306](https://github.com/Stability-AI/StableStudio/pull/36)
  - [StableStudio.app downloaded the wrong compyui _202307](https://github.com/Stability-AI/StableStudio/issues/96)
    - macos m1, After running StableStudio.app, will download the Windows version of the ComfyUI installation package.
  - [StableStudio vs StableSwarmUI _202308](https://github.com/Stability-AI/StableStudio/discussions/106)
    - As StableSwarmUI and StableStudio are both projects with StabilityAI, I'm curious if one will be abandoned in favor of the other

- https://github.com/badboysm890/ClaraVerse /3kStar/MIT/202508/ts
  - https://claraverse.space/
  - Privacy-first, fully local AI workspace with Ollama LLM chat, tool calling, agent builder, Stable Diffusion, and embedded n8n-style automation. 
  - No backend. No API keys. Just your stack, your machine.
  - The Story Behind ClaraVerse: Why can't everything be in a single app?
  - The Solution: One App. Six Tools. Zero Compromises.
  - Built on the shoulders of giants: llama.cpp • llama-swap • faster-whisper • ComfyUI • N8N

- https://github.com/lllyasviel/stable-diffusion-webui-forge /11.4kStar/AGPL/202506/python
  - a platform on top of Stable Diffusion WebUI (based on Gradio)
  - Forge is currently based on SD-WebUI 1.10.1 at this commit. (Because original SD-WebUI is almost static now, Forge will sync with original WebUI every 90 days, or when important fixes.)
  - https://github.com/Panchovix/stable-diffusion-webui-reForge /202508/archived
# diffusers
- https://github.com/huggingface/diffusers /30.4kStar/apache2/202508/python
  - https://huggingface.co/docs/diffusers
  - Diffusers is a library of state-of-the-art pretrained diffusion models for generating videos, images, and audio in PyTorch and FLAX
  - Our library is designed with a focus on usability over performance, simple over easy, and customizability over abstractions.
  - Diffusers offers three core components: 
    - diffusion pipelines that can be run in inference with just a few lines of code
    - Interchangeable noise schedulers for different diffusion speeds and output quality
    - Pretrained models that can be used as building blocks
  - [Diffusers current/future _202504](https://github.com/huggingface/diffusers/discussions/11403)
    - ideas for longer-term priorities for diffusers
    - Better LoRA support: CivitAI is de-facto standard for LoRA distribution so asking for LoRA to be uploaded to HF hub just so it can be tested is a no-no
    - Support single-file everywhere: majority of users prefer single-file safetensors
    - Focus on consumer GPUs: Almost all new models are large 
    - Create differentiators: Remote VAE is another very positive initiative
  - [The different quality between ComfyUI and Diffusers ? _202408](https://github.com/huggingface/diffusers/discussions/9265)
  - [Why do Diffusers schedulers produce lower quality outputs compared to ComfyUI? _202406](https://github.com/huggingface/diffusers/discussions/8682)

- https://github.com/leejet/stable-diffusion.cpp /4.3kStar/MIT/202508/cpp/NoDeps
  - Inference of Stable Diffusion and Flux in pure C/C++
  - Plain C/C++ implementation based on ggml, working in the same way as llama.cpp
  - Super lightweight and without external dependencies
  - SD1.x, SD2.x, SDXL and SD3/SD3.5 support
  - https://github.com/piallai/stable-diffusion.cpp
    - a fork of stable-diffusion.cpp. It adds a GUI interface to the executable generating examples.
  - https://github.com/daniandtheweb/sd.cpp-webui /AGPL/python
    - A simple Gradio-based interface for stable-diffusion.cpp.
  - https://github.com/fszontagh/sd.cpp.gui.wx /MIT/cpp
    - A cross-platform GUI for Stable Diffusion C++, built using wxWidgets.
# more
