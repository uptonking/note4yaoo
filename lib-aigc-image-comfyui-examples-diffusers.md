---
title: lib-aigc-image-comfyui-examples-diffusers
tags: [comfyui, diffusers, examples, image]
created: 2025-08-23T11:43:02.194Z
modified: 2025-08-23T11:43:35.904Z
---

# lib-aigc-image-comfyui-examples-diffusers

# guide

- tips
  - 一些流行的custom_nodes/extension仓库也提供了comfyui的workflow示例

- fans-comfyui
  - https://github.com/cubiq/ComfyUI_essentials
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
  - [ComfyUI to InvokeAI - Invoke](https://invoke-ai.github.io/InvokeAI/nodes/comfyToInvoke/)
    - InvokeAI's backend and ComfyUI's backend are very different which means Comfy workflows are not able to be imported into InvokeAI.
  - https://github.com/invoke-ai/ui-library
    - UI Components for Invoke's applications.
    - Customized Chakra-UI components.
  - https://github.com/Millu/invoke-workflows

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
- https://github.com/Comfy-Org/desktop /1.7kStar/GPLv3/202508/ts
  - The desktop app for ComfyUI (Windows & macOS)
  - bundled with a few things: ComfyUI_frontend, ComfyUI-Manager, uv
  - https://github.com/Comfy-Org/ComfyUI_frontend /1.3kStar/GPLv3/202508/ts/vue
    - Official front-end implementation of ComfyUI.
    - On startup, it will install all the necessary python dependencies with uv and start the ComfyUI server.
    - We use the NSIS installer for Windows: https://www.electron.build/nsis.html
  - https://github.com/Comfy-Org/ComfyUI-Manager /GPL/python
    - It offers management functions to install, remove, disable, and enable various custom nodes
    - provides a hub feature
  - https://github.com/YanWenKun/ComfyUI-Docker
    - 容器镜像与启动脚本
  - https://github.com/ashleykleynhans/comfyui-docker /28Star/GPLv3/202508/hcl
    - Docker image for ComfyUI: The most powerful and modular stable diffusion GUI, api and backend with a graph/nodes interface.
    - This image is designed to work on RunPod.
    - Running Locally: linux/windows
  - https://github.com/ai-dock/comfyui
    - ComfyUI docker images for use in GPU cloud and local environments.
  - https://github.com/Comfy-Org/comfy-cli
  - https://github.com/Comfy-Org/rfcs
    - RFCs for substantial changes to ComfyUI core, APIs, and standards.
  - https://github.com/patientx/ComfyUI-Zluda /GPLv3/202508
    - ZLUDA enhanced for better AMD GPU performance.
    - Windows-only version of ComfyUI which uses ZLUDA to get better performance with AMD GPUs.

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
  - 侧重于训练与调优, 似乎对标diffusers
  - 似乎是image/video-gen的平台，能提供最新的阿里模型，类似在线IDE能配置运行环境GPU、模型参数、lora/controlnet
  - DiffSynth-Studio is an open-source Diffusion model engine developed and maintained by ModelScope team. 
  - DiffSynth currently includes two open-source projects
  - DiffSynth-Studio: Focused on aggressive technical exploration, for academia, providing support for more cutting-edge model capabilities.
  - DiffSynth-Engine: Focused on stable model deployment, for industry, offering higher computing performance and more stable features.
  - DiffSynth-Studio and DiffSynth-Engine are the core projects behind ModelScope AIGC zone https://modelscope.cn/aigc/home
  - [Compararison with diffusers _202503](https://github.com/modelscope/DiffSynth-Studio/issues/475)
    - I would like to know why the inference speed is much faster than diffusers implementation and there's quality gap as well.
    - diffusers is much better but much slower
  - [阿里魔搭社区开源了一款强力引擎：DiffSynth Studio，带你轻松生成图像和视频 - 知乎 _202410](https://zhuanlan.zhihu.com/p/1035820317)
    - 一款开源图像和视频生成整合引擎
    - 提供了两种非常友好的 WebUI 版本——Gradio 和 Streamlit
  - [训练的lora文件支持导出为diffusers可用的safetensor格式吗？ _202409](https://github.com/modelscope/DiffSynth-Studio/issues/203)
    - 我们已经在努力避免分化开源生态，flux 的 lora 训练脚本中已经支持通过参数 --align_to_opensource_format 来将 lora 文件的格式转换为其他开源项目中通用的格式，您可以提供您所需的格式，我们会晚点适配
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

- https://github.com/StableCanvas/comfyui-client /121Star/MIT/202506/ts/NoDeps
  - https://stablecanvas.github.io/comfyui-client/
  - Javascript api Client for ComfyUI that supports both NodeJS and Browser environments.
  - This client provides comprehensive support for all available RESTful and WebSocket APIs, with built-in TypeScript typings for enhanced development experience. 
  - Introduces a human-readable and highly customizable workflow interface inspired by this issue and https://github.com/Chaoses-Ib/ComfyScript
  - https://stablecanvas.github.io/tool-w2c/
    - Online convert workflow to code
  - https://github.com/devniel/nextjs-comfyui-example /202408/ts/inactive
    - 🌰 An example of a project calling ComfyUI via websockets
  - https://github.com/itsKaynine/comfy-ui-client /MIT/202309/ts/inactive
    - Node.js WebSockets API client for ComfyUI

- https://github.com/comfy-addons/comfyui-sdk /196Star/MIT/202508/ts
  - TypeScript SDK for seamless interaction with the ComfyUI API. 
  - This SDK significantly simplifies the complexities of building, executing, and managing ComfyUI workflows, all while providing real-time updates and supporting multiple instances
  - Construct and manipulate intricate ComfyUI workflows effortlessly using a fluent, intuitive builder pattern
  - Multi-Instance Management: Handle a pool of ComfyUI instances with ease, employing flexible queueing strategies for optimal resource utilization.
  - Subscribe to WebSocket events for live progress tracking, image previews, and error notifications.
  - Custom WebSocket Support: Supply your own WebSocket implementation for greater flexibility
  - Supports Basic Auth, Bearer Token, and Custom Authentication Headers
  - Extension Support: Seamlessly integrate with ComfyUI Manager and leverage system monitoring
  - Examples: Includes practical examples for Text-to-Image (T2I), Image-to-Image (I2I), and complex multi-node workflows

- https://github.com/BennyKok/comfyui-deploy /1.4kStar/AGPL/202508/python/ts
  - https://www.comfydeploy.com/
  - open source `vercel` like deployment platform for Comfy UI
  - Open source comfyui deployment platform, a vercel for generative workflow infra. (serverless hosted gpu with vertical intergation with comfyui)
  - Stack: Clerk (Auth), NextJS, Drizzle (ORM), Neon / Vercel Postgres, R2 / S3 (Object Storage)
  - https://github.com/BennyKok/comfyui-deploy-next-example /202404/ts/inactive
    - https://demo.comfydeploy.com/
    - This project is designed to demonstrate the integration and utilization of the ComfyDeploy SDK within a Next.js application.
    - showcase how developers can get started creating applications running ComfyUI workflows using Comfy Deploy.

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

- https://github.com/16131zzzzzzzz/EveryoneNobel /1.4kStar/apache2/202411/python/inactive
  - A flexible framework powered by ComfyUI for generating personalized Nobel Prize images.
  - We utilizes ComfyUI for image generation and HTML templates to display text on the images. 
  - This project serves not only as a process for generating nobel images but also as a potential universal framework. This framework transforms the ComfyUI-generated visuals into final products, offering a structured approach for further applications and customization.
# ai-image-generator
- tips
  - midjourney alternative

- https://github.com/11cafe/jaaz /2.3kStar/NonComm/202508/python/ts
  - https://jaaz.app/
  - AI design agent, local alternative for Lovart. Canva + Cursor. 
  - Infinite Canvas & Visual Storyboarding Plan scenes with an unlimited canvas
  - 社区许可证： 面向个人及组织有限使用的免费许可证。
  - 商业许可证： 任何内部团队部署，或对代码的任何二次开发或修改，都必须获取商业许可证。
  - [Jaaz's "completely" self-hosted? _202508](https://github.com/11cafe/jaaz/issues/252)
    - if you use ollama and add comfyui workflows for image generations, it will be fully self hosted. Or add your own replicate api key, you can also self host
  - [Self-hosted image generation and LLM API _202506](https://github.com/11cafe/jaaz/issues/21)
    - you want to local host your stable diffusion models or Flus models? Yea we will support that through local comfyui image generations
  - [WIP: support ComfyUI  _202506](https://github.com/11cafe/jaaz/pull/7)
    - add ComfyUI installation & install dialog, add adm-zip
    - Get the latest ComfyUI release information from GitHub
    - refactor: Standalone comfyUI installation logic

- https://github.com/6174/comflowyspace /2.3kStar/NonComm/202408/ts/inactive
  - an open-source AI image and video generation tool committed to providing a better, interactive experience than the standard SDWebUI and ComfyUI
  - a typical Client-Server app, for long term design, it can work as a cloud web app and a electron app.
  - /apps/node: A node application to connect comfyUI and front-end
  - ComflowySpace 可以直接加载 ComfyUI 里的模型，也支持直接加载 Stable Diffusion WebUI 内的模型
  - 可以继续在 ComflowySpace 上使用所有 ComfyUI 的插件
  - 云端版本和开源离线版本提供相同的功能。主要区别在于：云端版本运行在高性能 GPU 上，性能更强，但需要付费。离线开源版本使用你电脑的 GPU，所以免费
  - 由于 Comflowy 采用纯无服务器设计以及自定义节点带来的独特挑战，我们不支持用户安装自定义节点。但你可以通过客服聊天联系我们，我们的团队可以手动安装它们。
  - [Comflowy 和 ComfyUI 有什么区别？ – Comflowy](https://www.comflowy.com/zh-CN/blog/comflowy-vs-comfyui)
    - ComflowySpace 是基于 ComfyUI 进行二次开发的产品，其内核依然是 ComfyUI。并且我们也按照 ComfyUI 的协议要求，对代码进行了开源。
    - ComfyUI 安装教程。 看完你就会发现，安装起来非常困难，为了解决这个问题，ComflowySpace 提供一键安装功能
    - 增加了 Workflow 管理功能，这个功能可以让你更方便地管理你的 Workflow，且你的每次更改都会自动保存
    - 支持模板功能，可以利用各种模板来搭建 workflow
  - https://github.com/6174/comflowy
    - ComfyUI 相比于 Stable Diffusion WebUI 等其他开源产品具备非常强的差异化能力，它具备高度的扩展性和应用可能性
    - ComfyUI 却缺乏系统成熟的教程和经验文档，工具也缺乏良好的体验设计，以至上手门槛过高被很多 Stable Diffusion 用户拒之门外
    - 我们决定先做一个 ComfyUI 社区 - Comflowy
    - 提供一个开源版的 Better ComfyUI - Comflowyspace

- https://github.com/xingren23/ComfyFlowApp /584Star/GPL/202403/python/archived
  - ComfyFlowApp is a tool to help you develop AI webapp from ComfyUI workflow and share to others.
  - offers an in-built test account(username: demo) with the credentials(password: comfyflowapp)
  - [API是否支持自建？ _202403](https://github.com/xingren23/ComfyFlowApp/issues/65)
    - 如果只是想自己用，不提供登录服务的话,也可以直接改下代码返回。 本地用用是可以的
    - API for user login only

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
- https://github.com/Visionatrix/Visionatrix /149Star/AGPL/202507/ts/vue
  - https://visionatrix.github.io/VixFlowsDocs/
  - Simplify your AI media generation workflows with Visionatrix—an intuitive interface built on top of ComfyUI
  - ⏳ Versioned and upgradable workflows.
  - Scalability: Run multiple instances with simultaneous task workers for increased productivity.
  - Multi-User Support: Configure for multiple users with ease and integrate different user backends.
  - LLM Integration: Effortlessly incorporate Ollama/Gemini as your LLM for ComfyUI workflows
  - Run as a service with backend endpoints for smooth project integration.
  - Easy integrate LoRAs from CivitAI into your flows.
  - Official Docker images and a pre-configured Docker Compose file.

- https://github.com/sdfxai/sdfx /440Star/AGPL/202505/ts/vue
  - https://sdfx.ai/
  - no-code platform to build and share AI apps with beautiful UI.
  - What SDFX allows, for example, is the creation of complex graphs (as one would do on ComfyUI), but with an overlay of a simpler, high-level UI (such as a form-based interface, with an incredible UI). 
  - This is an initial draft, there is still much to do 
  - We tried to do things right, focusing solely on what we do best: UIs and product design with a modern frontend stack. 
  - Therefore, we rely 100% on Comfy's backend, making SDFX fully compatible with ComfyUI. 
  - However, installing ComfyUI is not necessary, as everything is abstracted. We also made an effort to simplify the installation process; 
  - 100% compatible with ComfyUI and all its features
  - Can work with your existing Comfy installation (with our SDFXBridgeForComfy custom node)
  - LiteGraph almost refactored from scratch in typescript
  - Node bookmarks and advanced graph search

- https://github.com/huanyingtianhe/EasyComfyUI /MIT/202411/js/inactive
  - https://easy-comfyui.vercel.app/
  - An UI to integrate with ComfyUI backend for easy use
  - we only support "Text to image" and "Video to video": Text to Image, Text to Video, Image to Image, Image to video, Video to video

- https://github.com/rvion/CushyStudio /781Star/AGPL/202412/ts/inactive
  - https://docs.cushystudio.com/
  - The AI and Generative Art platform for everyone
  - Cushy orchestrate various tools like ComfyUI or FFMpeg. Some apps require you to have those tools installed.
  - Most CushyStudio Apps build on top of ComfyUI as a backend

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
- https://github.com/MoJIeAIGC/Comfyui-MojieUI /10Star/BSD/202506/python/ts/vue
  - https://www.qihuaimage.com/
  - MoJie-UI 是一个以comfyui为后端的图像生成UI和server框架，通过redis进行队列服务管理、前端使用vue框架，集成了GPT4O, FLUX-Kkontext，即梦API。
  - 能够进行多任务处理，用户支付，积分充值等。
  - 本项目依赖于 ComfyUI、Redis 和 MySQL 等服务。
  - 后端服务 python-django
  - 使用redis作为任务缓存，将任务请求依次发送至comfyui
  - 支持多任务多GPU负载均衡。
  - 采用对话式交互+常用功能，支持拖拽，交互体验极佳。

- https://github.com/ShivanshKandwal/Kairo---image-generation-and-editing-frontend-application-based-on-comfyui-backend /202508/js
  - Kairo is a user-friendly desktop application that acts as a powerful, network-accessible host for your ComfyUI backend.
  - Kairo allows you to host a ComfyUI backend on one machine and connect to it from any other device on your network via a simple web browser.
  - All models are managed on the host machine, so clients don't need to download or install anything.
# extensions/custom-node
- https://github.com/VrchStudio/comfyui-web-viewer /248Star/MIT/202508/python/js
  - http://vrch.ai/
  - custom nodes and web utilities for real-time AI generation and interaction
  - This utility integrates realtime streaming into ComfyUI workflows, supporting keyboard control nodes, OSC control nodes, sound input nodes, and more
  - Real-Time AI Generation & Interaction: Immediate response for interactive creativity.
  - Multi-Input Support: Easily integrates keyboard, OSC, and audio input for versatile interactivity.
  - Universal Web Accessibility: Compatible with any device equipped with a web browser.

- https://github.com/Taremin/webui-monaco-prompt /MIT/202502/ts
  - Editors such as `CLIPTextEncode` and note are replaced with the Monaco Editor used in VSCode.
  - This extension introduces an autocomplete feature and provides the option to switch to a vim-style keymap.
  - https://x.com/Teslanaut/status/1896379544724295978
    - Is there a @ComfyUI extension for VSCode? I'm surprised there isn't. 
    - To be able to generate or have your AI co-pilot agent generate icon images, logos, or any other images or maybe even video you need for your website or book would be quite an interesting thing to add to your workflow. 

- https://github.com/chflame163/ComfyUI_LayerStyle /2.5kStar/MIT/202508/python
  - A set of nodes for ComfyUI that can composite layer and mask to achieve Photoshop like functionality.
  - https://github.com/chflame163/ComfyUI_LayerStyle_Advance /MIT
    - The nodes detached from ComfyUI Layer Style are mainly those with complex requirements for dependency packages.

- https://github.com/rgthree/rgthree-comfy /2.2kStar/MIT/202508/ts
  - A collection of nodes and improvements created while messing around with ComfyUI.
  - Reroute, Bookmark, Image Comparer
  - A lot of the power of these nodes comes from Muting. Muting is the basis of correctly implementing multiple paths for a workflow utlizing the Context Switch node.
- https://github.com/lum3on/ComfyUI_logic-bypasser /202506/python/js
  - An advanced logic bypasser node for ComfyUI with automation support, inspired by the rgthree group bypasser architecture but enhanced for backend execution and programmatic control.
  - Works in ComfyUI's execution engine, not just frontend
  - Conditional Logic: Advanced condition evaluation

- https://github.com/taabata/ComfyCanvas /2024011/python/js/inactive
  - Canvas to use with ComfyUI
  - select a part of the image to be third output in OutputCanvasNode. https://github.com/taabata/LCM_Inpaint_Outpaint_Comfy.git

- https://github.com/Lerc/canvas_tab /BSD/202401/python/js/inactive
  - ComfyUI canvas editor page
  - provides two nodes to provide a full page editor that runs in another tab.

- https://github.com/zanllp/sd-webui-infinite-image-browsing /1.2kStar/MIT/202508/python/ts/vue
  - A fast and powerful image/video browser for Stable Diffusion webui / ComfyUI / Fooocus / NovelAI / StableSwarmUI, featuring infinite scrolling and advanced search capabilities using image parameters.
  - Once caching is generated, images can be displayed in just a few milliseconds.
  - Images are displayed with thumbnails by default, with a default size of 512 pixels. You can adjust
  - The prompt, model, Lora, and other information will be converted into tags and sorted by frequency of use for precise searching.

- https://github.com/receyuki/comfyui-prompt-reader-node /MIT/385Star/202502/python/js
  - solution for managing image metadata and multi-tool compatibility. 
  - ComfyUI node version of the SD Prompt Reader
  - https://github.com/receyuki/stable-diffusion-prompt-reader /202405/python/inactive
    - A simple standalone viewer for reading prompts from Stable Diffusion generated image outside the webui.

- https://github.com/talesofai/comfyui-browser /NALic/202411/python/svelte/inactive
  - This is an image/video/workflow browser and manager for ComfyUI. 
  - You can sync your workflows to a remote Git repository and use them everywhere.
  - Browse and manage your images/videos/workflows in the output folder.
  - Some useful custom nodes like xyz_plot, inputs_select.
  - Install ComfyUI Manager, search comfyui-browser in Install Custom Node and install it.

- https://github.com/giriss/comfy-image-saver /MIT/202308/python/inactive
  - All the tools you need to save images with their generation metadata on ComfyUI. 
  - Compatible with Civitai & Prompthero geninfo auto-detection. 
  - Works with png, jpeg and webp.
  - 支持保存prompt

- https://github.com/thedyze/save-image-extended-comfyui /202409/python/inactive
  - Customize the information saved in file- and folder names.
  - Save data about the generated job (sampler, prompts, models) as entries in a json (text) file, in each folder.

- https://github.com/LEv145/images-grid-comfy-plugin /202405/python
  - https://civitai.com/models/31126
  - A simple comfyUI plugin for images grid (X/Y Plot)
  - XYZPlot, like in auto1111, but with more settings

- https://github.com/aiaiaikkk/super-prompt-canvas /202506/python/js
  - 为 ComfyUI 设计的图像编辑提示词生成插件，通过可视化画布标注和AI辅助，快速生成精准的编辑提示词。
  - 可视化标注和AI辅助提示词生成

- https://github.com/Yanick112/ComfyUI-ToSVG /225Star/MIT/202506/python
  - Converts raster images into SVG in ComfyUI.
  - thanks to visioncortex and potracer

- https://github.com/AARG-FAN/Image-Vector-for-ComfyUI /202406/python/inactive
  - 一个打包了vtracer的comfyui节点，用于把像素转矢量

- https://github.com/Gourieff/ComfyUI-ReActor /749Star/GPL/202508/python
  - Fast and Simple Face Swap Extension Nodes for ComfyUI, based on blocked ReActor

- https://github.com/THtianhao/ComfyUI-FaceChain /138Star/apache2/202504/python
  - This repository is the ComfyUI version of FaceChain
  - This project is adapted from facechain and involves the breakdown and improvement of the processes of facechain.
  - https://github.com/modelscope/facechain

- https://github.com/banodoco/Steerable-Motion /925Star/OSNL/202506/python
  - A ComfyUI node for driving videos using batches of images.
  - The Wan approach uses VACE to create anchor images and continuations from previous images, which are chained together at the end:
  - The Animatediff approach uses a combination of IP-Adapter and SparseCtrl to travel between images

- https://github.com/melMass/comfy_mtb /MIT/202507/python/js
  - Animation oriented nodes pack for ComfyUI

- https://github.com/djbielejeski/a-person-mask-generator /MIT/202507/python
  - Extension for Automatic1111 and ComfyUI to automatically create masks for Background/Hair/Body/Face/Clothes in Img2Img
  - Uses the Multi-class selfie segmentation model model by Google.

- https://github.com/EllangoK/ComfyUI-post-processing-nodes /230Star/GPL/202501/python
  - A collection of post processing nodes for ComfyUI, which enable a variety of visually striking image effects

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

- https://github.com/burnsbert/ComfyUI-EBU-LMStudio /MIT/202507/python
  - provides custom nodes for integrating with LMStudio, allowing for loading, managing, and making requests of LLM models through the LMStudio local server and command-line interface.
  - Load and manage LLM models directly from ComfyUI
  - Optional image model unloading to free up VRAM

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

- https://github.com/11cafe/comfyui-workspace-manager /1.3kStar/MIT/202408/python/ts/inactive
  - A ComfyUI workflows and models management extension to organize and manage all your workflows, models in one place.
  - [2025-4-16] since ComfyUI frontend has built-in workspace management feature now, this plugin becomes obsolte and will not be maintained anymore. 
# utils
- https://github.com/Tavris1/ComfyUI-Easy-Install /170Star/MIT/202508/bat
  - Portable ComfyUI for Windows, macOS and Linux 
  - Pixaroma Community Edition 

- https://github.com/bytedance/comfyui-lumi-batcher /401Star/GPLv3/202508/python/ts
  - 专为 ComfyUI 设计的批量处理扩展插件，旨在提升 AIGC 创作效率，是一个调参抽卡、批量出素材的利器
  - 不局限在 xyz 三维参数的交叉调试，而是 workflow 内的所有参数均可交叉，一次完成所有调试
  - 批量调试可以是多个参数的组合体，如「商品图 + 对应 prompt」 X 不同基模
  - 多维表格，自由抽卡预览或批量导出：不同参数的聚合浏览方式

- https://github.com/Chaoses-Ib/ComfyScript /571Star/MIT/202506/python
  - A Python frontend and library for ComfyUI
  - Serving as a human-readable format for ComfyUI's workflows.
  - Directly running the script to generate images. The main advantage of doing this than using the web UI is being able to mix Python code with ComfyUI's nodes
  - With ComfyScript, ComfyUI's nodes can be used as functions to do ML research
  - Generating ComfyUI's workflows with scripts.
  - Converting workflows from ComfyUI's web UI format to API format without the web UI.

- https://github.com/pydn/ComfyUI-to-Python-Extension /2kStar/MIT/202507/python/js
  - a powerful tool that translates ComfyUI workflows into executable Python code.
  - Designed to bridge the gap between ComfyUI's visual interface and Python's programming environment
  - this tool streamlines the process of implementing ComfyUI workflows in Python.

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

- https://github.com/ericwanghp/ComfyUI_MCP /MIT/202505/python
  - 为 ComfyUI 设计的松耦合、可扩展、配置驱动的模型上下文协议（ModelContextProtocol）服务端。
  - 支持依据客户定制工作流可扩展MCP服务(tool) 如: txt2img、img2img，每个MCP服务(tool)的参数和行为均可通过 JSON初始化和MCP工具装饰器模块灵活扩展，适合 AI 绘图、推理等场景的自动化与集成。

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
  - https://github.com/jesenzhang/ComfyUI_StreamDiffusion
    - a simple implemention StreamDiffusion for ComfyUI

- https://github.com/RishiDesai/CharForge /MIT/202506/python
  - https://www.charforge.dev/
  - Generate character consistent images with a single reference
  - 48GB is preferred, but you can get by with 24GB
  - [Generate character consistent images with a single reference (Open Source & Free) : r/StableDiffusion _202506](https://www.reddit.com/r/StableDiffusion/comments/1lkezo2/generate_character_consistent_images_with_a/)
    - I built a tool for training Flux character LoRAs from a single reference image, end-to-end.

- https://github.com/ty0x2333/ComfyUI-Dev-Utils /146Star/MIT/202507/python/js
  - Execution Time Analysis, Reroute Enhancement, Remote Python Logs, For ComfyUI developers.

- https://github.com/tzwm/comfyui-profiler /202408/python/js/inactive
  - Calculate the execution time of all nodes.

- https://github.com/jordenyt/stable_diffusion_sketch /122Star/GPLv3/202506/java
  - an Android client app that connect to your own ComfyUI or A1111-sd-webui
  - This app integrates with ComfyUI via a RESTful API, enabling powerful AI image generation capabilities right from your mobile device.

- https://github.com/CLOUDWERX-DEV/DiffuGen /MIT/202504/python
  - DiffuGen is a powerful yet user-friendly interface for local\edge image generation.
  - DiffuGen is a powerful MCP-based image generation system that brings cutting-edge AI models directly into your development workflow.
  - Built on top of the highly optimized `stable-diffusion.cpp` implementation
  - Now includes OpenAPI server support and OpenWebUI OpenAPI Tools (OWUI Version 0.60.0 Required) integration for seamless image generation and display in chat interfaces

- https://github.com/CrazyBoyM/ComfyUI2API /apache2/202408/python/inactive
  - 一个把ComfyUI工作流转换为API服务的服务
  - 基于本地websocket通信实现数据转发，用于让ComfyUI变成一个通用的API服务

- https://github.com/ParisNeo/comfyui_proxy_server /apache2/202403/python/inactive
  - a lightweight reverse proxy server designed for load balancing and rate limiting. 

- https://github.com/l3lackcurtains/Comfy_UI_Backend /202506/python
  - A Python-powered API backend featuring a custom Comfy UI, seamlessly integrated with Docker and Kubernetes for modern containerization and orchestration. 
  - Scalable, reliable, and built for efficient deployment

- https://github.com/d3x-at/sd-parsers /MIT/202504/python
  - A Python library to read metadata from images created by Stable Diffusion.
  - Prompts as well as some well-known generation parameters are provided as easily accessible properties (see Output).
  - support: sd-webui, ComfyUI
# workflows
- https://github.com/pwillia7/Basic_ComfyUI_Workflows /202508
  - Basic Stable Diffusion Workflows for ComyUI using minimal custom nodes
  - This is meant to be a good foundation to start using ComfyUI in a basic way.
  - You can import the JSON files or the PNGs into Comfy to use the workflows. Most workflows are built for SDXL by default but can be changed easily to work with other SD versions.
  - simply clone this repo into your ComfyUI custom_nodes directory. ComfyUI will automatically detect 

- https://github.com/dicksondickson/dickson-sci-fi-enhance-upscale /202505
  - These are ComfyUI workflows to upscale images to 2K, 4K, or 8K.
  - These workflows upscales images in multiple stages using a combination of upscaling models, CCSR, SUPIR and Ulitmate SD Upscale, upscaling models, SDXL and Flux.
  - Each workflow is tuned to a specific resolution with different speed variants. These workflows are continuing evolving.

- https://github.com/comfyanonymous/ComfyUI_examples
  - https://comfyanonymous.github.io/ComfyUI_examples/
  - All the images in this repo contain metadata which means they can be loaded into ComfyUI
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
- https://github.com/yushan777/comfyui-api-part1-basic-workflow /202312/python/inactive
  - [ComfyUI : Using the API : Part 1. Controlling ComfyUI via Script _202309](https://medium.com/@yushantripleseven/comfyui-using-the-api-261293aa055a)
  - https://github.com/ZYJ-3721/ComfyUI-API-Client /202411/python/inactive
    - 调用ComfyUI的API实现文生图和图生视频

- https://github.com/SaladTechnologies/comfyui-api /218Star/MIT/202508/ts
  - A simple API server to make ComfyUI easy to scale horizontally. 
  - A simple wrapper that facilitates using ComfyUI as a stateless API, either by receiving images in the response, or by sending completed images to a webhook
  - ComfyUI API sits in front of ComfyUI, and uses the ComfyUI `/prompt` API to execute workflows, so any API-formatted prompt can be executed by the server.
  - The server is built with Fastify. It sits in front of ComfyUI, and provides a RESTful API for interacting with ComfyUI.
  - 🏠 Stateless API: The server is stateless, and can be scaled horizontally to handle more requests. 
    - server is designed to be stateless, meaning that it does not store any state between requests. 
    - This allows the server to be scaled horizontally behind a load balancer, and to handle more requests by adding more instances of the server. 
    - The server uses a configurable warmup workflow to ensure that ComfyUI is ready to accept requests, and to load any required models. 
  - The server supports the full ComfyUI /prompt API, and can be used to execute any ComfyUI workflow.
  - "Synchronous" Support: The server will return base64-encoded images directly in the response, if no webhook is provided.
    - The default behavior of the API is to return an array of base64-encoded outputs in the response body. 
    - All that is needed to do this is to omit the `.webhook` and `.s3` field in the request body.
  - Webhook Support: The server can send completed images to a webhook, which can be used to store images
  - The server can return images in PNG, JPEG, or WebP format, via a parameter in the API request. Most options supported by `sharp` are supported.
  - Dynamic Workflow Endpoints: Automatically mount new workflow endpoints by adding conforming .js or .ts files to the /workflows directory in your docker image.
  - Bring Your Own Models And Extensions: Use any model or extension you want by adding them to the normal ComfyUI directories `/opt/ComfyUI/`.
  - Single Binary: The server is distributed as a single binary, and can be run with no dependencies.
  - The server can forward ComfyUI websocket events to a configured webhook, which can be used to monitor the progress of a workflow.
  - The server is designed to work well with SaladCloud. It is likely to work well with other platforms as well.

- https://github.com/nexmoe/serverless-comfyui /MIT/202502/ts/inactive
  - 一个基于 Docker 的 ComfyUI 弹性 Serverless 应用，提供完整的前后端分离架构和用户友好的界面。
  - 基于nextjs的前端
  - 项目的图片上传功能需要配置 S3 存储服务。你可以使用 AWS S3 或其他兼容 S3 协议的对象存储服务（如 MinIO）

- https://github.com/Netwrck/stable-diffusion-server /53Star/MIT/202507/python
  - 🖼️ Image Generation API Server - Similar to https://text-generator.io but for images
  - Simple interface for generating images in Gradio locally and easy to use FastAPI docs/server for advanced users.
  - Running the Gradio UI: python gradio_ui.py
  - Local Deployment: Run locally for style transfer, art generation and inpainting.

- https://github.com/piyushK52/comfy_runner /235Star/202411/python/inactive
  - Automatically install ComfyUI nodes and models and use it as a backend
  - This tool automatically downloads all the necessary nodes and models and executes the provided workflow. 
  - This repo can make it easier for people to use ComfyUI as a backend.
  - Executes the workflow without starting the UI server
  - Auto installs missing nodes
  - Link to custom nodes and models can be provided for installation/Setup

- https://github.com/Distillery-Dev/Discomfort /248Star/MIT/202508/python
  - https://www.discomfort.ai/
  - Control ComfyUI with Python
  - Discomfort is a ComfyUI extension that lets you control your workflows with the power of Python, enabling loops, conditionals, and stateful execution.
  - you can write simple scripts to automate complex image generation tasks, turning your workflows into reusable, programmable components.
  - 🏠 Discomfort introduces a layer of programmatic control on top of ComfyUI's existing graph-based execution model.
  - ComfyUI's native execution model follows a Directed Acyclic Graph (DAG) pattern, executing nodes once in topological order. 
    - While powerful for single-pass workflows, this model doesn't natively support things like iterations, backpropagation of data, or conditional execution paths.
    - Discomfort addresses these limitations by introducing an execution layer on top of ComfyUI's DAG model, using pre-execution graph manipulation and a self-managed ComfyUI server for isolated runs, as well as a simple data store that handles context throughout the run.
  - Self-Managed ComfyUI Server: Discomfort starts and manages its own ComfyUI instance in the background. This ensures that it doesn't interfere with your regular ComfyUI sessions.
  - Pre-Execution Graph Manipulation: Before a workflow is executed, Discomfort modifies the graph to inject and extract data through the DiscomfortPort nodes.
  - Intelligent Data Handling: Discomfort can handle different types of data, passing large objects like models by reference to avoid unnecessary memory overhead.

- https://github.com/luckkyzhou/ComfyUI-API-Integration /MIT/202411/python/inactive
  - This project provides a comprehensive suite for developers to integrate ComfyUI APIs and automate image generation workflows. 
  - By encapsulating API input and output, this suite enables developers to input any workflow json file and receive the processed output image directly. 
  - Allows users to input images and receive the processed result based on selected workflows.

- https://github.com/SharCodin/comfy-gradio-api /202401/python/inactive
  - building a Python API to connect Gradio and Comfy UI for AI image generation with Stable Diffusion models.
  - connect a Gradio front-end interface to a Comfy UI backend

- https://github.com/bobvinch/comfy-server /525Star/202405/ts/nestjs/inactive
  - comfyui server to use comfyui API as easy as send a message
  - 核心功能1：ComfyUI的绘画API服务和websocket转发，客户端必须使用socketIO链接，WS无法连接
  - 核心功能2：方便将任意comfyui工作转换为在线API，向外提供AI能力
  - 修复Redis相关问题，增加容器一键部署方式
  - 天然支持利用nginx直接实现负载均衡, ComfyUI server之间可以共享AI绘画能力

- https://github.com/sugarkwork/Comfyui_api_client /MIT/202506/python
  - A Python client library for interacting with ComfyUI via its API. 
  - Supports both synchronous and asynchronous operations with automatic workflow format conversion.
  - Both sync (ComfyUIClient) and async (ComfyUIClientAsync) implementations
  - Automatically converts workflow.json to API format
  - Direct image upload to ComfyUI server

- https://github.com/Acly/comfyui-tooling-nodes /540Star/GPL/202508/python/js
  - Provides nodes and API geared towards using ComfyUI as a backend for external tools.
  - Send and receive images directly without filesystem upload/download.
  - ComfyUI exchanges images via the filesystem. This requires a multi-step process (upload images, prompt, download images), which invites a whole class of potential issues you might not want to deal with.

- https://github.com/9elements/comfyui-api /202402/python/inactive
  - You need to a comfyUI server running and be able to access the "/ws" path for this server. If you have the server running localy it usually runs under "127.0.0.1:8188".

- https://github.com/deimos-deimos/comfy_api_simplified /MIT/202411/python/inactive
  - This is a small python wrapper over the ComfyUI API. 
  - It allows you to edit API-format ComfyUI workflows and queue them programmatically to the already running ComfyUI.
  - Only Basic auth and no auth (for local server) are supported.

- https://github.com/comfy-addons/comfy-station /28Star/MIT/202508/ts
  - open-source application designed to streamline the management of multiple ComfyUI instances.
  - nextjs 15, React Query for data fetching
  - Elysia for API server
  - LangChain for AI integrations
  - tRPC for type-safe API communication
  - MikroORM with LibSQL for database
  - Next-Auth for authentication

- https://github.com/richinsley/comfy2go /MIT/202506/go/inactive
  - a Go-based API that acts as a bridge to ComfyUI
  - Comfy2go is comprised of two main parts:
    - The GraphAPI approximates the functionality of ComfyUI's front-end graph-based pipeline. While it does not allow for creating or editing existing workflows, it does allow for quickly finding, and setting the various inputs of each node in a workflow.
    - The ClientAPI interoperates with the ComfyUI backend, offering: Concurrent access to multiple instances of ComfyUI, Creating and queuing prompts from GraphAPI workflows
    - https://github.com/qxdo/comfyui-go

- https://github.com/kiri-art/docker-diffusers-api /MIT/202309/python/inactive
  - Diffusers / Stable Diffusion in docker with a REST API, supporting various models, pipelines & schedulers.
  - Used by kiri.art, perfect for local, server & serverless.

- https://github.com/bananaml/serverless-template-stable-diffusion /MIT/202305/python/inactive
  - This repo gives a basic framework for serving Stable Diffusion in production using simple HTTP servers.

- https://github.com/cantrell/stable-diffusion-api-server /apache2/202211/python/inactive
  - A local inference REST API server for the Stable Diffusion Photoshop plugin. (Also a generic Stable Diffusion REST API for whatever you want.)
  - Stable Diffusion weights automatically downloaded from Hugging Face.
  - Custom fine-tuned models in the Hugging Face `diffusers` file format like those created with DreamBooth.

- https://github.com/viral-medialab/stable_diffusion_server /202210/python/js/inactive
  - Runs your own Stable Diffusion v1.4 API with Flask & Docker

- https://github.com/bentoml/stable-diffusion-server /apache2/202209/python/inactive
  - Deploy Your Own Stable Diffusion Service
  - Download Pre-built Stable Diffusion Bentos 似乎是定制sd发型版
  - https://github.com/bentoml/BentoDiffusion
# sd-ui/webapp
- https://github.com/ViewComfy/ViewComfy /461Star/AGPL/202508/ts
  - https://www.viewcomfy.com/
  - open source tool to help you create beautiful web apps from ComfyUI workflows.
  - The Playground is a simplified UI where you can run your workflows.
  - [How to turn a ComfyUI workflow into a web app in minutes _202410](https://www.viewcomfy.com/blog/turn-a-comfyui-workflow-into-an-app)

- https://github.com/jac3km4/comfyweb /72Star/MIT/202506/ts/svelte
  - a simple interface for ComfyUI that replaces graphs with beautiful forms.
  - A unified gallery view that allows you to easily preview, edit and manage both generated images as well as anything that's pending in the queue.
  - This project builds into a single HTML file. 

- https://github.com/ImDarkTom/ComfyUIMini /288Star/AGPL/202501/ts
  - A mobile-friendly WebUI to run ComfyUI workflows.
  - Ensure ComfyUI is installed and functional (minimum v0.2.2-50-7183fd1 / Sep. 18th release).

- https://github.com/diStyApps/ComfyUI-disty-Flow /556Star/202501/python/js/inactive
  - a custom node designed to provide user-friendly interface for ComfyUI by acting as an alternative user interface for running workflows. It is not a replacement for workflow creation.

- https://github.com/canisminor1990/kitchen-comfyui /228Star/MIT/202304/python/ts/inactive
  - A reactflow base stable diffusion GUI as ComfyUI alternative interface

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

- https://github.com/space-nuko/ComfyBox /669Star/GPL/202308/jupyter/ts/svelte
  - Customizable Stable Diffusion frontend for ComfyUI
  - It uses ComfyUI under the hood for maximum power and extensibility.
  - An installation of vanilla ComfyUI for the backend

- https://github.com/lllyasviel/stable-diffusion-webui-forge /11.4kStar/AGPL/202506/python
  - a platform on top of Stable Diffusion WebUI (based on Gradio)
  - Forge is currently based on SD-WebUI 1.10.1 at this commit. (Because original SD-WebUI is almost static now, Forge will sync with original WebUI every 90 days, or when important fixes.)
  - [Forge Is Not Using ComfyUI as A Backend _202402](https://github.com/lllyasviel/stable-diffusion-webui-forge/discussions/169)
    - The backend is WebUI backend with Forge optimizations. (We call it Forge backend.)
    - Forge is not using Comfy as backend. But adopt lot of techniques and code used in comfy.  some of addon modules are just copied from comfy with some modification.
    - i agree, comfyui is NOT the backend 1:1; but most/a lot of the code used in the backend is comfy's code (with a1111 compat fixes which have been known to comfy users for a while now)
  - https://github.com/Panchovix/stable-diffusion-webui-reForge /202508/archived

- https://github.com/licyk/term-sd /GPL/202508/sh
  - 多平台 Stable Diffusion 部署，管理脚本
  - Term-SD 是一款基于 Dialog 实现前端界面显示的 AI 管理器，支持安装，管理以下软件：sd-webui, comfyui, InvokeAI, fooocus
  - Term-SD 支持在 Linux，Windows，MacOS 上
  - https://github.com/licyk/sd-webui-all-in-one /80Star/GPLv3/202508/jupyter
    - 支持部署多种 WebUI 的 Jupyter Notebook，支持部署以下 WebUI：sd-webui, comfyui, InvokeAI,fooocus
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

- https://github.com/cozy-creator/gen-server /202501/python/go
  - A rebuild of ComfyUI, using Diffusers for inference and Golang for efficiency.
  - This repo is not yet useable or functional, and contains a lot of dead code.
  - This repo is the backend used to power cozy.art using Runpod GPUs currently.
  - The graph editor front-end is here: https://github.com/cozy-creator/graph-editor
  - The graph editor is currently not yet functional

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
# InvokeAI
- https://github.com/CodeGandee/invokeai-py-client /MIT/202508/python
  - A Python client library to operate InvokeAI system through its web API
  - This client does not re‑implement the UI; instead it leverages the exported workflow artifact and selected REST endpoints to let GUI users automate large, repeatable runs in Python.
  - https://github.com/VeyDlin/invokeai-python

- https://github.com/Echsecutor/gen_ai_container /MIT/202508/python/js
  - This is a minimalist container running invoke web UI. 
  - I have just turned the installation manual at https://invoke-ai.github.io/InvokeAI/installation/manual/ into a Dockerfile.
  - See the Comfy UI Docs for how to use Comfy UI

- https://github.com/kraussian/invoke-civitai /apache2/202504/python
  - Convert metadata from InvokeAI for automatic recognition when uploading to CivitAI
# more
- https://github.com/Comfy-Org/registry-backend /GPL/202502/go
  - https://registry.comfy.org/
  - The server that backs ComfyUI Registry, a public collection of custom node packs used in ComfyUI.
  - The backend API server for Comfy Registry and Comfy CI/CD.

- https://github.com/runpod-workers/worker-comfyui /AGPL/202508/python
  - This project allows you to run ComfyUI workflows as a serverless API endpoint on the RunPod platform.
  - Submit workflows via API calls and receive generated images as base64 strings or S3 URLs.
  - The worker exposes standard RunPod serverless endpoints (/run, /runsync, /health). 
    - By default, images are returned as base64 strings. 
    - You can configure the worker to upload images to an S3 bucket instead by setting specific environment variables 
  - https://github.com/Dekita/runpod-serverless-comfyui-worker /202311/inactive
    - serverless ComfyUI worker for Runpod.io

- https://github.com/replicate/cog-comfyui /MIT/202507/python
  - https://replicate.com/fofr/any-comfyui-workflow
  - Run ComfyUI with an API
  - You’ll need the API version of your ComfyUI workflow. This is different to the commonly shared JSON version, it does not included visual information about nodes
  - You can use LoRAs directly from CivitAI, HuggingFace, or any other URL in two ways
  - To get the best performance from the model you should run a dedicated instance.
