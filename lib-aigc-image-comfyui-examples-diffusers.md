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

- resources
  - https://github.com/search?type=repositories&q=stable-diffusion
# popular
- https://github.com/invoke-ai/InvokeAI /25.8kStar/apache2/202511/python/ts
  - https://invoke-ai.github.io/InvokeAI/
  - Invoke is a leading creative engine for Stable Diffusion models 
  - 交互逻辑很特别，支持canvas/workflow/form/queue-list-log
  - 后端依赖fastapi、pydantic、asyncio、torch、diffusers、typing、starlette
  - 前端依赖@reduxjs/toolkit、redux-undo、@nanostores/react、pragmatic-drag-and-drop、@xyflow/react、@dagrejs/dagre、@dagrejs/graphlib、konva、ag-psd、async-mutex、cmdk、dockview、framer-motion、i18next、idb-keyval、jsondiffpatch、linkifyjs、perfect-freehand、react-hook-form、react-virtuoso、zod、socket.io
  - 软件元数据在sqlite `invokeRoot/databases/invokeai.db`, 生成的图片在文件夹 invokeRoot/outputs/images
  - Invoke has a Community Edition that is freely available under a commercially-friendly license (Apache 2) and a Professional Edition available
  - Invoke is a powerful, secure, and easy-to-deploy generative AI platform for professional studios that provides a flexible workflow builder with multi-user sharing and permissions, a step-by-step custom AI model trainer
  - 💰 [InvokeAI was just acquired by Adobe : r/StableDiffusion _202510](https://www.reddit.com/r/StableDiffusion/comments/1obws1z/invokeai_was_just_acquired_by_adobe/)
  - 🆚 [Why Invoke AI is the Best ComfyUI Alternative](https://www.invoke.com/comparisons/comfyui-vs-invokeai)
  - 🎯 [Invoke AI 3.0 Release : r/StableDiffusion _202307](https://www.reddit.com/r/StableDiffusion/comments/155sm30/invoke_ai_30_release/)
    - As of 3.0, all of the developments we’ve been working on are now available to install and use - And, to demonstrate our commitment to open-source, we’ve updated our license to the most explicitly permissive license available - Apache 2.0.
  - [ComfyUI to InvokeAI - Invoke](https://invoke-ai.github.io/InvokeAI/nodes/comfyToInvoke/)
    - InvokeAI's backend and ComfyUI's backend are very different which means Comfy workflows are not able to be imported into InvokeAI.
  - https://github.com/invoke-ai/ui-library
    - UI Components for Invoke's applications.
    - Customized Chakra-UI components.
  - https://github.com/Millu/invoke-workflows
  - https://github.com/invoke-ai/launcher /apache2/202508/ts
    - 📌 The launcher is a desktop application for Windows, macOS (Apple Silicon) and Linux.
    - It can install, update, reinstall and run Invoke Community Edition. It is self-contained, so you don't need to worry about having the right python version installed.
    - 依赖@electron-toolkit/typed-ipc、electron-builder、node-pty、xterm、@emotion/react、vite
    - Using the launcher to update Invoke
    - Updating the launcher itself
    - If installation fails, retrying the install in Repair Mode may fix it. 
    - Like the install script, the launcher creates and manages a normal python virtual environment.
    - The launcher is an electron application with React UI. We bundle `uv` with the build and then call it to install python, create the app `venv`, and run the app.
  - The "old" scripts will be phased out over time. The goal is to support 3 ways to install and run Invoke:
    - Launcher
    - Docker
    - Manual (e.g. create a `venv` manually, install the `invokeai` package, run it as a script)

- https://github.com/comfyanonymous/ComfyUI /85.4kStar/GPLv3/202508/python
  - https://www.comfy.org/
  - The most powerful and modular diffusion model GUI, api and backend with a graph/nodes interface.
  - ComfyUI lets you design and execute advanced stable diffusion pipelines using a graph/nodes/flowchart based interface. 
  - 依赖torchvision、torchsde、torchaudio、transformers、scipy、safetensors、numpy、aiohttp(未使用框架如fastapi)、Pillow、pyyaml、tqdm、SQLAlchemy、pydantic
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
  - [Is there an API you can call? _202307](https://github.com/comfyanonymous/ComfyUI/issues/952)
    - yes, read the top of: `master/script_examples/basic_api_example.py` or `master/script_examples/websockets_api_example.py`;
    - comfyui caches the node outputs of the last workflow so you submit the same workflow twice it won't execute anything in it. Set a random seed instead of the fixed seed in the script.
  - [support flask api like webui ?  _202306](https://github.com/comfyanonymous/ComfyUI/issues/799)
    - The api is meant to be both stateless and asynchronous because some workflows can take minutes to complete.
  - [Proposal: Replacing aiohttp with FastAPI in ComfyUI Backend _202412](https://github.com/comfyanonymous/ComfyUI/discussions/5931)
    - our team at Nextcloud—where we were considering offering ComfyUI to the community—has currently put that plan on hold until the situation improves.
  - https://github.com/Comfy-Org/ComfyUI_frontend /GPL/202508/ts/vue
    - 📌 Official front-end implementation of ComfyUI
    - 依赖vue-router、pinia、vueuse、firebase、vuefire(Firebase bindings for Vue)、tiptap.v2、tiptap-markdown、marked、three、jsondiffpatch、pragmatic-drag-and-drop、@primevue/core(ui)、xterm、fuse.js、algoliasearch、es-toolkit、extendable-media-recorder
    - On startup, it will install all the necessary python dependencies with uv and start the ComfyUI server.
    - We use the NSIS installer for Windows: https://www.electron.build/nsis.html
    - Backend: Dev server expects ComfyUI backend at http://localhost:8188 by default
    - [Consolidate network calls to use consistent HTTP clients _202508](https://github.com/Comfy-Org/ComfyUI_frontend/issues/5017)
      - mixed usage of direct fetch() calls and axios clients: makes it difficult to implement cross-cutting concerns like request/response interceptors, consistent error handling, and header management.
  - [Server Config - ComfyUI](https://docs.comfy.org/interface/settings/server-config)
    - host: Sets the IP address the server binds to. Default `127.0.0.1` means only local access is allowed. If you need LAN access, you can set it to `0.0.0.0`.
    - port: Desktop version defaults to port `8000`, Web version typically uses port `8188`.
  - [Change default port · Issue · Comfy-Org/desktop _202506](https://github.com/Comfy-Org/desktop/issues/1193)
    - You can specify custom port with `COMFY_PORT` env variable
    - This is also available within the `Settings` menu under `Server-Config`.
    - Edit the comfy.settings.json file `"Comfy.Server.LaunchArgs": { "port": "9000" }`;
  - https://github.com/Comfy-Org/desktop /1.7kStar/GPLv3/202508/ts
    - 📌 The desktop app for ComfyUI (Windows & macOS)
    - bundled with a few things: ComfyUI_frontend, ComfyUI-Manager, uv
    - 依赖electron-store、node-pty、@electron/rebuild、@todesktop/runtime(未开源的云端打包)
    - [Open sourcing v1 Desktop - by Robin - ComfyUI Blog _202411](https://blog.comfy.org/p/open-sourcing-v1-desktop)
    - https://github.com/Comfy-Org/comfy-cli
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
  - https://github.com/Comfy-Org/rfcs
    - RFCs for substantial changes to ComfyUI core, APIs, and standards.
  - https://github.com/patientx/ComfyUI-Zluda /GPLv3/202508
    - ZLUDA enhanced for better AMD GPU performance.
    - Windows-only version of ComfyUI which uses ZLUDA to get better performance with AMD GPUs.

- https://github.com/liusida/top-100-comfyui /MIT/202508/python/jinja
  - This repository automatically updates a list of the top 100 repositories related to ComfyUI based on the number of stars on GitHub.

- https://github.com/mcmonkeyprojects/SwarmUI /3kStar/MIT/202508/csharp/js
  - SwarmUI (formerly StableSwarmUI), A Modular Stable Diffusion Web-User-Interface, with an emphasis on making powertools easily accessible, high performance, and extensibility
  - 未直接使用comfyui的代码库，通过请求交互; 前端js实现，有挂载对象到window上
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

- https://github.com/vladmandic/sdnext /6.5kStar/AGPL > apache2/202508/python/js
  - https://vladmandic.github.io/sdnext-docs/
  - All-in-one WebUI for AI generative image and video creation
  - Built-in Control for Text, Image, Batch and Video processing
  - 后端依赖torchsde、safetensors、tqdm、numpy、pandas、pydantic、httpx
  - 前端es5，将变量方法挂在`window`上
  - 代码似乎不优雅
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
  - 🍴 forks
  - https://github.com/anapnoe/stable-diffusion-webui-ux /AGPL/202508
    - Removed FormSubGroup Component
    - Split View Resizer Added
    - Support for Image Aspect Ratio Helper Extension Accordion
  - https://github.com/lshqqytiger/stable-diffusion-webui-amdgpu /AGPL/202508
    - ZLUDA support for AMDGPUs.
    - DirectML support for every GPUs that support DirectX 12 API.

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

- https://github.com/comfy-addons/comfyui-sdk /196Star/MIT/202508/ts
  - TypeScript SDK for seamless interaction with the ComfyUI API. 
  - This SDK significantly simplifies the complexities of building, executing, and managing ComfyUI workflows, all while providing real-time updates and supporting multiple instances
  - 可使用js builder模式创建workflow， 也可以导入api-format格式的json(workflow)
  - Construct and manipulate intricate ComfyUI workflows effortlessly using a fluent, intuitive builder pattern
  - Multi-Instance Management: Handle a pool of ComfyUI instances with ease, employing flexible queueing strategies for optimal resource utilization.
  - Subscribe to WebSocket events for live progress tracking, image previews, and error notifications.
  - Custom WebSocket Support: Supply your own WebSocket implementation for greater flexibility
  - Extension Support: Seamlessly integrate with ComfyUI Manager and leverage system monitoring
  - 🌰 Examples: Includes practical examples for Text-to-Image (T2I), Image-to-Image (I2I), and complex multi-node workflows
  - Auth: Supports Basic Auth, Bearer Token, and Custom Authentication Headers
  - Flexible Node Bypassing: Strategically bypass specific nodes in your workflows during generation, enabling advanced customization
  - [Loading an existing ComfyUI workflow? _202501](https://github.com/comfy-addons/comfyui-sdk/issues/23)
    - The workflow should be exported as API format, you can export it from the ComfyUI web interface

- https://github.com/StableCanvas/comfyui-client /121Star/MIT/202509/ts/NoDeps
  - https://stablecanvas.github.io/comfyui-client/
  - Javascript api Client for ComfyUI that supports both NodeJS and Browser environments.
  - 可将workflow json转换为js代码, 而comfyui-sdk只处理export-as-api-format格式的json
  - 作者似乎转向了 comfyui-sdk 
  - This client provides comprehensive support for all available RESTful and WebSocket APIs, with built-in TypeScript typings for enhanced development experience. 
  - Introduces a human-readable and highly customizable workflow interface inspired by this issue and https://github.com/Chaoses-Ib/ComfyScript
  - https://github.com/StableCanvas/tool-w2c
    - https://stablecanvas.github.io/tool-w2c/
    - Online convert workflow to `comfyui-client` js code
    - Upload or drag & drop a ComfyUI .json (API format) or .png workflow file.
  - https://github.com/devniel/nextjs-comfyui-example /202408/ts/inactive
    - 🌰 An example of a project calling ComfyUI via websockets
  - https://github.com/itsKaynine/comfy-ui-client /MIT/202309/ts/inactive
    - Node.js WebSockets API client for ComfyUI
  - https://github.com/StableCanvas/sd-webui-a1111-client
    - API client for AUTOMATIC111/stable-diffusion-webui for nodejs/browser
  - https://github.com/zandko/comfyui-sdk /MIT
    - TypeScript-first client for interacting with ComfyUI

- https://github.com/sugarkwork/Comfyui_api_client /17Star/MIT/202506/python
  - A Python client library for interacting with ComfyUI via its API. 
  - Supports both synchronous and asynchronous operations with automatic workflow format conversion.
  - Both sync (ComfyUIClient) and async (ComfyUIClientAsync) implementations
  - Automatically converts workflow.json to API format
  - Direct image upload to ComfyUI server

- https://github.com/zinigor/comfy-es-wrapper /GPL/202508/ts
  - a frontend wrapper for ComfyUI, designed to provide ESM imports and utilities for building, editing, and interacting with ComfyUI workflows
  - It offers a modular API for workflow and node manipulation, as well as integrations for Vue and React.
  - 依赖@comfyorg/litegraph、打包了源码`github: Comfy-Org/ComfyUI_frontend`; 
  - API utilities: Fetch node types, execute workflows, monitor queue status, retrieve workflow history, and manage real-time WebSocket connections.
  - Editor Component: Provides a `ComfyEditor` class for embedding and manipulating workflow graphs with ease.
  - Vue & React adapters: Includes example wrappers for integration with popular frameworks.

- https://github.com/Chaoses-Ib/ComfyScript /571Star/MIT/202506/python
  - A Python frontend and library for ComfyUI
  - Serving as a human-readable format for ComfyUI's workflows.
  - Converting workflows from ComfyUI's web UI format to API format without the web UI.
  - Directly running the script to generate images. The main advantage of doing this than using the web UI is being able to mix Python code with ComfyUI's nodes
  - Scripts can also be used to generate ComfyUI's workflows and then used in the web UI or elsewhere. 
  - Scripts can be automatically translated from ComfyUI's workflows. See transpiler for details.
  - With ComfyScript, ComfyUI's nodes can be used as functions to do ML research

- https://github.com/pydn/ComfyUI-to-Python-Extension /2kStar/MIT/202507/python/js
  - a powerful tool that translates ComfyUI workflows into executable Python code.
  - Designed to bridge the gap between ComfyUI's visual interface and Python's programming environment
  - this tool streamlines the process of implementing ComfyUI workflows in Python.

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

- https://github.com/DaWe35/image-router /202508/js
  - https://imagerouter.io/
  - https://docs.imagerouter.io/
  - A simple API router for image generation models. 
  - This service acts as a proxy between your application and other image generation APIs, simplifying the process of using different models.
  - OpenAI compatible API endpoint
  - Rate limiting
  - Integrate ImageRouter into Open WebUI with the ready-made ImageRouter Plugin.
  - 依赖prisma
  - [I built Image Router - A Unified Interface for AI Image Models (Like OpenRouter, but for Images) : r/SideProject _202504](https://www.reddit.com/r/SideProject/comments/1k3tcsa/i_built_image_router_a_unified_interface_for_ai/)
    - It also has a unified API, so you can switch between models in your own code without any changes.
    - Image Router does not store any images you generate. This means you need to download anything you want to keep

- https://github.com/AIDC-AI/ComfyUI-Copilot /2.5kStar/MIT/202508/python/ts
  - 👾 An AI-powered custom node for ComfyUI designed to enhance workflow automation and provide intelligent assistance
  - ComfyUI-Copilot is an AIGC intelligent assistant built on ComfyUI that provides comprehensive support for tedious workflow building, ComfyUI-related questions, parameter optimization and iteration processes
  - 🎯v2-20250814: v2.0 evolves from a "helper tool" into a "development partner"—not just assisting with workflow development, but capable of autonomously completing development tasks.
  - We now cover the entire workflow lifecycle, including generation, debugging, rewriting, and parameter tuning, aiming to deliver a significantly enhanced creative experience.
  - Debug:：Automatically detects errors in your workflow, precisely identifies issues, and provides repair suggestions.
  - Workflow Rewriting：Optimizes the current workflow based on your description, such as adjusting parameters, adding nodes, and improving logic.
  - Enhanced Workflow Generation：Understands your requirements more accurately and generates tailored workflows
  - Upgraded Agent Architecture：Now aware of your local ComfyUI environment, Copilot delivers optimized, personalized solutions.
  - [ComfyUI-Copilot 实现原理 · Pines-Cheng/blog _202507](https://github.com/Pines-Cheng/blog/issues/127)
    - ❓ 只开源了前端
  - [Local AI model _202502](https://github.com/AIDC-AI/ComfyUI-Copilot/issues/12)
    - 👷20250827: Now you can use your local LLAMA, and any fuction, like workflow generation, node suggestion, model suggestion are supported with local LLM now. 
  - [Please add local Ai model support (no internet connection required) _202504](https://github.com/AIDC-AI/ComfyUI-Copilot/issues/57)
    - The adoption of the locally deployed model you mentioned is indeed a good idea, and we have considered related optimizations.
    - However, because there are many external data warehouses behind our project, and the entire project uses the Agent tool calling framework, the use of a smaller LLM model will cause the accuracy of the response to drop significantly, so we have abandoned this iterative solution in the short term.
    - In the future, from the perspective of upgrading the entire framework, we will also consider using a small large language model to drive the entire project, and then make relevant updates.
    - I think that adding integration with `litellm` should be reasonable, there are many MLLMs and LLMs that are supported in vllm that can be called through it. If someone is going to run comfyui in a solid computing environment, it is quite reasonable to self-host LMs

- https://github.com/16131zzzzzzzz/EveryoneNobel /1.4kStar/apache2/202411/python/inactive
  - A flexible framework powered by ComfyUI for generating personalized Nobel Prize images.
  - We utilizes ComfyUI for image generation and HTML templates to display text on the images. 
  - This project serves not only as a process for generating nobel images but also as a potential universal framework. This framework transforms the ComfyUI-generated visuals into final products, offering a structured approach for further applications and customization.
  - 🚀 [不到30个小时，我们做了一款AI产品 _202410](https://mp.weixin.qq.com/s/t3v-h1MzpFKuh0RCMRmjEg)
    - 10月9日夜里我们开启了内测，我们采用的发送注册码的方式让群里的用户添加。各种各样的生成失败，排队过长用户反馈。但彼时群内已经有接近2000名用户，并且还在不断增加，大量的用户在群里质疑什么时候可以体验。
    - 大家都认可引入直接付费的机制。我们在网站的入口处直接放了本人的微信二维码，希望用户能够来我这边购买注册码。
    - 但实际的结果是，大火的一个小半天里只有不到100人添加微信，有意向购买的不到十个人，最终仅有1人愿意付款，甚至认为19.9 10张图太贵
    - 10.10号的下午我们才正式接入了支付，令人意外的是，当天就有不少流水，和私域的大失败形成鲜明对比。

- https://github.com/PastLifeDreamer/Pocket-Comfy /MIT/202509/python
  - Lightweight mobile first web app combining ComfyUi, ComfyUi Mini and Smart ComfyUI Gallery with convenient local control functions hosted on your PC under one python script.
  - [Pocket Comfy. Free open source Mobile Web App released on GitHub. : r/StableDiffusion _202509](https://www.reddit.com/r/StableDiffusion/comments/1npylj2/pocket_comfy_free_open_source_mobile_web_app/)
    - Pocket Comfy wraps the best comfy mobile apps out there and runs them in one python console
    - Pocket Comfy unifies the best web apps currently available for mobile first content creation including: ComfyUI, ComfyUI Mini (Created by ImDarkTom), and smart-comfyui-gallery (Created by biagiomaf) into one web app that runs from a single Python window. 
    - Launch, monitor, and manage everything from one place at home or on the go.
# ai-image-generator
- tips
  - midjourney alternative

- https://github.com/LastLighter/Dreamifly /MIT/202511/ts
  - https://dreamifly.com/
  - 基于 Next.js 与 ComfyUI API 的开源 AI 图像生成平台，支持文生图（Text-to-Image）和图生图（Image-to-Image），无需注册，专为开发者与创意者打造
  - 集成多种先进 AI 模型（如 HiDream-I1、Flux.1-Dev、Stable Diffusion 3.5、Qwen-Image 等），通过调用 ComfyUI 后端 API 实现快速入门的图像生成
  - 生图时默认进入排队状态
  - [我开源了月浏览量 70K+ 的AI绘画网站 _202510](https://linux.do/t/topic/1022006)
    - 我们的网站近期一个月内发访问数据如下，浏览量 70k+, 访问次数 40K+，访客量 23K+

- https://github.com/google-gemini/gemini-image-editing-nextjs-quickstart /484Star/apache2/202505/ts/inactive
  - https://ai.google.dev/gemini-api/docs/image-generation
  - Nextjs quickstart for to generating and editing images with Google Gemini 2.0 Flash
  - It allows users to generate images from text prompts or edit existing images through natural language instructions, maintaining conversation context for iterative refinements. 

- https://github.com/ammaarreshi/openjourney /135Star/MIT/202507/ts/提交少
  - https://openjourney.replit.app/
  - Open-source clone of the MidJourney web interface featuring real AI image and video generation powered by Google's Gemini SDK. 
  - 👾 Use Imagen 4 to generate images and Veo 2 and 3 for image and text to video with audio.
  - 4-image grid layout matching MidJourney's design
  - 依赖nextjs、framer-motion、shadcn-ui

- https://github.com/Nutlope/blinkshot /955Star/NALic/202508/ts
  - https://www.blinkshot.io/
  - An open source real-time AI image generator. 
  - Powered by Flux through Together.ai 👾 .
  - Flux Schnell from BFL for the image model
  - Together AI for inference

- https://github.com/Nutlope/logocreator /5.5kStar/NALic/202501/ts/inactive
  - https://www.logo-creator.io/
  - A free + OSS logo generator powered by Flux on Together AI 👾 
  - Flux Pro 1.1 on Together AI for logo generation
  - nextjs + shadcn + redis + clerk + plausible
  - [license · Issue · Nutlope/logocreator](https://github.com/Nutlope/logocreator/issues/16)

- https://github.com/premieroctet/photoshot /3.8kStar/MIT/202412/ts/inactive
  - open-source AI avatar generator web app
  - 依赖nextjs、chakra-ui、prisma
  - 👾 Replicate, a platform for running machine learning models in the cloud

- https://github.com/jaaronkot/picprose /719Star/MIT/202508/ts
  - https://picprose.pixpark.net/
  - a powerful cover image generator designed for bloggers, content creators, developers, and designers
  - 🖼️ Access high-quality images directly through the Unsplash API
  - Flexible Editing - Customize titles, author info, fonts, colors, and transparency
  - Real-time Preview - See all changes instantly with a WYSIWYG interface
  - 依赖 dom-to-image、react-photo-album、nextjs、nextui、react-infinite-scroll-component
  - Developer Icons - Built-in tech-related icons perfect for technical article covers
  - Multiple Export Formats - Support for JPG, PNG, and SVG exports

- https://github.com/virgoone/next-money /374Star/MIT/202504/ts/inactive
  - https://fluxaipro.art/
  - Flux AI Image generator
  - 比 ComfyUI 更易于使用
  - Empower your next project with the stack of Next.js 14, Prisma, Supabase, Clerk Auth, Resend, React Email, Shadcn/ui, and Stripe.

- https://github.com/Nutlope/loras-dev /344Star/202501/ts/inactive
  - https://loras.dev/
  - An open source real-time AI image generator. 
  - Powered by Flux through Together.ai.

- https://github.com/Stability-AI/StableStudio /9kStar/MIT/202306/ts/inactive
  - StableStudio is Stability AI's official open-source variant of DreamStudio, our user interface for generative AI.
  - 被同公司的SwarmUI所替代
  - It is a web-based application that allows users to create and edit generated images. 
  - What's the difference between StableStudio and DreamStudio?
    - All "over-the-wire" API calls have been replaced by a plugin system which allows you to easily swap out the back-end.
    - you can create your own plugin and use StableStudio with any back-end you want
  - [`ComfyUI` plugin _202306](https://github.com/Stability-AI/StableStudio/pull/36)
  - [StableStudio.app downloaded the wrong compyui _202307](https://github.com/Stability-AI/StableStudio/issues/96)
    - macos m1, After running StableStudio.app, will download the Windows version of the ComfyUI installation package.
  - [StableStudio vs StableSwarmUI _202308](https://github.com/Stability-AI/StableStudio/discussions/106)
    - As StableSwarmUI and StableStudio are both projects with StabilityAI, I'm curious if one will be abandoned in favor of the other
  - https://github.com/jtydhr88/ComfyUI-StableStudio
    - a ComfyUI plugin that provides a user interface of StableStudio
  - 🍴 forks
  - https://github.com/altx-labs/StableStudio /202507/ts
  - https://github.com/gryphus-lab/StableStudio /bot
  - https://github.com/crazydevlegend/StableStudio /202310/ts
  - https://github.com/AndyKong207/DrawStudio /202308
  - https://github.com/codeoria/StableStudio

- https://github.com/rogeriochaves/pictureit-editor /38Star/MIT/202304/ts/inactive
  - an open-source design editor, currently in beta version, designed to be a studio to help you create and iterate on digital art using a variety of AI models available as tools in the editor
  - Picture it Editor was not built to run the model locally on your machine, this is because running models is not the focus of this project, the focus really is on the user experience
  - 👾 Instead, Picture it uses Replicate as the API to run the models, the advantage of that is that the editor is able to use many models at the same time with no setup or the need of a powerful GPU
  - Replicate as a Backend: need a Replicate API key
  - [Picture it Editor: Open-source AI editor for Stable Diffusion : r/StableDiffusion _202301](https://www.reddit.com/r/StableDiffusion/comments/10dwamp/picture_it_editor_opensource_ai_editor_for_stable/)

- https://github.com/yardimli/ImageGeneratorForComfyUI /MIT/202508/php/blade
  - Client/Server for generating images with comfyUI and Flux, use OpenRouter for creating prompts, run ComfyUI locally. 
  - Run generator on the web. Use S3 to transfer generation from local to the web. Use Replicate to upscale.

- https://github.com/replicate/inpainter /425Star/MIT/202508/js
  - https://inpainter.app/
  - A web GUI built with Next.js for inpainting with AI models using Replicate's API
  - A web GUI for inpainting with Ideogram v2 and Ideogram v2 Turbo using the Replicate API.
  - Next.js server-side API routes for talking to the Replicate API

- https://github.com/dabasajay/Image-Caption-Generator /183Star/MIT/202307/js/inactive
  - A very simple placeholder image generator with zero dependencies. 
  - Returns a data URI (or raw SVG source) as a string for use in templates.

- https://github.com/huarzone/Text2img-Cloudflare-Workers /202505/js/inactive
  - https://text2img.huarzone.com/
  - 基于 CloudFlare AI & Workers 的免费在线文生图服务
  - 该项目为通过简单调用 Cloudflare 官方提供的 文生图 - Text-to-Image 模型，可以快速实现随时随地无需登录的图像生成需求。
  - https://github.com/zhumengkang/cf-ai-image /202508/js/inactive
    - 进行二次开发和功能增强
  - [基于cloudflare搭建的免费在线文生图服务 ](https://linux.do/t/topic/886265)
# examples
- https://github.com/d4N-87/ComfyUI-Workflow-Inspector /7Star/MIT/202508/ts
  - https://d4n-87.github.io/ComfyUI-Workflow-Inspector/
  - A React application to inspect ComfyUI workflow metadata embedded in PNG, WebP, MP4, FLAC, and JSON files.
  - Supports workflows from PNG, WebP, MP4, FLAC, and JSON files.
  - Workflow graph rendered using `LiteGraph.js`, with link colors and node names as faithful as possible to ComfyUI (based on object_info.json).
  - ComfyUI Look & Feel: Polished user interface inspired by ComfyUI.

- https://github.com/Nutlope/description-generator /311Star/NALic/202501/ts/inactive
  - https://product-descriptions.vercel.app/
  - Generate descriptions from product images in multiple languages with AI
  - Powered by Together AI and Llama 3.2 Vision.
  - S3 for image storage

- https://github.com/Tiefflieger06/comfyui-simple-frontend /GPL/202506/python/inactive
  - A basic web frontend for ComfyUI with the goal of being as simple to use as possible
  - Prompt-Based Image Generation: Users can input text prompts to generate images.
  - Generated images can be easily downloaded directly from the web 
  - The backend processes the prompt using ComfyUI and generates an image.
  - Flask, websocket-client, PyYAML

- https://github.com/MoJIeAIGC/Comfyui-MojieUI /10Star/BSD/202506/python/ts/vue
  - https://www.qihuaimage.com/
  - MoJie-UI 是一个以comfyui为后端的图像生成UI和server框架，通过redis进行队列服务管理、前端使用vue框架，集成了GPT4O, FLUX-Kkontext，即梦API。
  - 能够进行多任务处理，用户支付，积分充值等。
  - 本项目依赖于 ComfyUI、Redis 和 MySQL 等服务。
  - 后端服务 python-django
  - 使用redis作为任务缓存，将任务请求依次发送至comfyui
  - 支持多任务多GPU负载均衡。
  - 采用对话式交互+常用功能，支持拖拽，交互体验极佳。
  - https://github.com/MoJIeAIGC/comfyui-MJAPI-party /13Star/apache2/202508/python
    - 为了让comfyui更加普及，让本地低配置电脑也同样能顺利的运行comfyui，同时避免在comfyui中调用外部API时密钥和地址难以统一管理，以及许多更优秀模型本地算力难以支撑，本地部署耗时耗力，
    - 因此mjapi-party将许多优秀常用的API节点做整合，只需要一个API-key即可以调用全网的API接口能力，也能够通过comfyui节点式操作，保留极大的灵活性
    - 更多API节点正逐步添加中,后续也会逐步增加对扣子和n8n的支持

- https://github.com/Visionatrix/Visionatrix /149Star/AGPL/202507/ts/vue/参考架构
  - https://visionatrix.github.io/VixFlowsDocs/
  - Simplify your AI media generation workflows with Visionatrix—an intuitive interface built on top of ComfyUI
  - 可安装新comfyui，也可管理现有的comfyui
  - ⏳ Versioned and upgradable workflows.
  - Scalability: Run multiple instances with simultaneous task workers for increased productivity.
  - Multi-User Support: Configure for multiple users with ease and integrate different user backends.
  - LLM Integration: Effortlessly incorporate Ollama/Gemini as your LLM for ComfyUI workflows
  - Run as a service with backend endpoints for smooth project integration.
  - Easy integrate LoRAs from CivitAI into your flows.
  - Official Docker images and a pre-configured Docker Compose file.
  - 🏠 [Working modes - Visionatrix Documentation](https://visionatrix.github.io/VixFlowsDocs/AdminManual/WorkingModes/working_modes/)
    - By default, Vix launches with all components integrated (Server + Worker + UI) for quick and easy use on a single computer.
    - A simple and understandable User Interface
    - A server component, namely, the backend
    - A component responsible for processing tasks (in short - Worker)
    - TaskQueue - a database (SQLite (default), PgSQL)
    - it is allowed and recommended to run the server part and the AI processing part of the task separately.
    - Each worker can have a different set of tasks (Flows) installed, which is useful to avoid installing a task on a worker instance that cannot handle it. A worker will only request the tasks installed for it.
    - Worker to Server mode: workers do not have direct access to the database or the server file system. All communication occurs through the network, with workers accessing the server backend directly.
  - 🤔 Can I use my own already installed ComfyUI with Visionatrix?
    - You can tell Visionatrix to use ComfyUI installed in a different path
  - Can I use ComfyUI which is included in Visionatrix?
    - Yes, you can install your Nodes there and run ComfyUI separately without running Visionatrix.
  - Can I run it on multiple GPU?
    - You can run one worker on one GPU and process tasks in parallel, take a look at Server and Worker modes.
  - [ComfyUI to Visionatrix migration ](https://visionatrix.github.io/VixFlowsDocs/FlowsDeveloping/comfyui_vix_migration/)
    - it is recommended to install our custom ComfyUI-Visionatrix nodes. Otherwise, you will have to use custom nodes titles which will be parsed by Visionatrix.

- https://github.com/rvion/CushyStudio /781Star/AGPL/202412/ts/inactive
  - https://docs.cushystudio.com/
  - The AI and Generative Art platform for everyone
  - Cushy orchestrate various tools like ComfyUI or FFMpeg. Some apps require you to have those tools installed.
  - Most CushyStudio Apps build on top of ComfyUI as a backend

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
  - 已合并 [WIP: support ComfyUI  _202506](https://github.com/11cafe/jaaz/pull/7)
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
  - [Comflowy 和 ComfyUI 有什么区别？](https://www.comflowy.com/zh-CN/blog/comflowy-vs-comfyui)
    - ComflowySpace 是基于 ComfyUI 进行二次开发的产品，其内核依然是 ComfyUI。并且我们也按照 ComfyUI 的协议要求，对代码进行了开源。
    - ComfyUI 安装教程。 看完你就会发现，安装起来非常困难，为了解决这个问题，ComflowySpace 提供一键安装功能
    - 增加了 Workflow 管理功能，这个功能可以让你更方便地管理你的 Workflow，且你的每次更改都会自动保存
    - 支持模板功能，可以利用各种模板来搭建 workflow
  - https://github.com/6174/comflowy /仅社区
    - ComfyUI 相比于 Stable Diffusion WebUI 等其他开源产品具备非常强的差异化能力，它具备高度的扩展性和应用可能性
    - ComfyUI 却缺乏系统成熟的教程和经验文档，工具也缺乏良好的体验设计，以至上手门槛过高被很多 Stable Diffusion 用户拒之门外
    - 我们决定先做一个 ComfyUI 社区 - Comflowy
    - 提供一个开源版的 Better ComfyUI - Comflowyspace

- https://github.com/huanyingtianhe/EasyComfyUI /MIT/202411/js/inactive
  - https://easy-comfyui.vercel.app/
  - An UI to integrate with ComfyUI backend for easy use
  - we only support "Text to image" and "Video to video": Text to Image, Text to Video, Image to Image, Image to video, Video to video
  - 依赖prisma、Mysql、nextjs

- https://github.com/ShivanshKandwal/Kairo---image-generation-and-editing-frontend-application-based-on-comfyui-backend /202508/js
  - Kairo is a user-friendly desktop application that acts as a powerful, network-accessible host for your ComfyUI backend.
  - Kairo allows you to host a ComfyUI backend on one machine and connect to it from any other device on your network via a simple web browser.
  - All models are managed on the host machine, so clients don't need to download or install anything.

- https://github.com/ainewsto/Comfyui_Comfly /290Star/apache2/202508/python
  - https://comfly.chat/
  - 我喜欢comfyui，它就像风一样的自由，所以我取名为：comfly 
  - Ai Chat and Midjourney
  - Comfyui version: comfyui本体版本的管理和切换
  - https://github.com/ainewsto/Comfyui_Comfly_v2 /apache2/python
    - 此版本为无悬浮按钮版本，只有节点

- https://github.com/Praecordi/comfy-character-app /202507/python 
  - A ComfyUI and ComfyScript Gradio-based app for generating characters using a multi-step process.
  - provides a Gradio-based interface for generating consistent character images using ComfyUI. It features a multi-step generation process with specialized controls for character attributes, style transfer, and detail enhancement.

- https://github.com/comfy-deploy/comfyui-deploy-gradio-demo /202408/python/inactive
  - This project provides a Gradio interface for interacting with ComfyDeploy, allowing users to dynamically generate UI components based on deployment input definitions and submit jobs to ComfyDeploy.
  - Dynamic UI generation based on ComfyDeploy input definitions
  - Asynchronous job submission to ComfyDeploy

- https://github.com/zyddnys/manga-image-translator /8.4kStar/GPL/202508/python
  - https://cotrans.touhou.ai/
  - 一键翻译各类图片内文字
  - This project aims to translate images that are unlikely to be professionally translated, such as comics/images on various group chats and image boards, making it possible for Japanese novices like me to understand the content
  - It mainly supports Japanese, but also supports Simplified and Traditional Chinese, English and 20 other minor languages.
# comfyui/sd-llm
- https://github.com/AIDC-AI/Pixelle-MCP /271Star/MIT/202508/python
  - https://pixelle.ai/
  - Open-Source Multimodal AIGC Solution based on ComfyUI + MCP + LLM
  - An AIGC solution based on the MCP protocol, seamlessly converting ComfyUI workflows into MCP tools with zero code
  - Server-side is built on ComfyUI, inheriting all capabilities from the open ComfyUI ecosystem
  - MCP Server provides functionality based on the MCP protocol, supporting integration with any MCP client (including but not limited to Cursor, Claude Desktop, etc.)
    - 服务端不依赖langchain
  - MCP Client is developed based on the `Chainlit` framework, inheriting Chainlit's UI controls
  - Integrated the LiteLLM framework, adding multi-model support for Gemini, DeepSeek, Claude, Qwen, and more
  - Flexible Deployment: Supports standalone deployment of Server-side only as MCP Server, or standalone deployment of Client-side only as MCP Client, or combined deployment
  - Unified Configuration: Uses YAML configuration scheme, one config file manages all services
  - https://github.com/Chainlit/chainlit /10.5kStar/apache2/202508/python/ts
    - https://docs.chainlit.io/
    - Build python production-ready conversational AI applications in minutes
    - As of May 1st 2025, the original Chainlit team has stepped back from active development.
    - 依赖langchain、LlamaIndex、ChromaDB

- https://github.com/oobabooga/text-generation-webui /44.8kStar/AGPLv3/202508/python
  - https://oobabooga.gumroad.com/l/deep_reason
  - A Gradio web UI for Large Language Models.
  - Supports multiple local text generation backends, including llama.cpp, Transformers, ExLlamaV3, ExLlamaV2, and TensorRT-LLM (the latter via its own Dockerfile).
  - 100% offline and private, with zero telemetry, external resources, or remote update requests.
  - Vision (multimodal models): Attach images to messages for visual understanding
  - Web search: Optionally search the internet with LLM-generated queries to add context to the conversation.
  - Extension support, with numerous built-in and user-contributed extensions available
  - [Ollama. Please?  _202408](https://github.com/oobabooga/text-generation-webui/issues/6346)
    - Ollama is llama.cpp. To be precise, the server side of ollama runs on llama.cpp, 
    - and the server side of text-generation-webui also runs on llama.cpp.
    - i couppled textgenwui with my open webui and it works perfect
    - I had the same problem. Because ollama also uses gguf files I simply created a script which links them into the models folder.
  - [Ollama Integration _202402](https://github.com/oobabooga/text-generation-webui/issues/5532)
  - https://github.com/SkinnyDevi/skdv_comfyui
    - ComfyUI image generation integration for oobabooga's Text Generation WebUI
  - https://github.com/Atinoda/text-generation-webui-docker
    - Docker variants of oobabooga's text-generation-webui, including pre-built images.

- https://github.com/badboysm890/ClaraVerse /3kStar/MIT/202508/ts
  - https://claraverse.space/
  - Privacy-first, fully local AI workspace with Ollama LLM chat, tool calling, agent builder, Stable Diffusion, and embedded n8n-style automation. 
  - No backend. No API keys. Just your stack, your machine.
  - The Story Behind ClaraVerse: Why can't everything be in a single app?
  - The Solution: One App. Six Tools. Zero Compromises.
  - Built on the shoulders of giants: llama.cpp • llama-swap • faster-whisper • ComfyUI • N8N

- https://github.com/apocas/restai /431Star/apache2/202508/python
  - https://apocas.github.io/restai/
  - an AIaaS (AI as a Service) open-source platform. 
  - Built on top of LlamaIndex & Langchain. langchain仅用于dalle_image_generator, LlamaIndex用得多
  - Supports any public LLM supported by LlamaIndex and any local LLM supported by Ollama/vLLM/etc
  - Built-in image generation (Dall-E, SD, Flux) and dynamic loading generators.
  - Image Generation: Supports local and remote image generators. 
    - Local image generators are run in a separate process. 
    - New generators are easily added and loaded dynamically.
    - 本地的图片生成基于diffusers实现， 如 `from diffusers import DiffusionPipeline`;
  - Proxy: Allows management of an OpenAI compatible proxy. LiteLLM is supported out of the box.
  - Projects: There are multiple project types, each with its own features. (rag, ragsql, inference, vision, router, agent)
  - The API is a first-class citizen of RestAI. All endpoints are documented using Swagger.
  - There are two vectorstores supported: ChromaDB and RedisVL
  - https://github.com/apocas/restai-frontend /202505/js/inactive
    - 依赖mui.v5、@reduxjs/toolkit、echarts、mui-datatables、react-d3-tree、recharts

- https://github.com/CLOUDWERX-DEV/DiffuGen /MIT/202504/python
  - a powerful yet user-friendly interface for local\edge image generation.
  - DiffuGen is a powerful MCP-based image generation system that brings cutting-edge AI models directly into your development workflow.
  - Built on top of the highly optimized `stable-diffusion.cpp` implementation
  - Now includes OpenAPI server support and OpenWebUI OpenAPI Tools (OWUI Version 0.60.0 Required) integration for seamless image generation and display in chat interfaces

- https://github.com/sanyabeast/imginarium /202504/python
  - A powerful tool for generating high-quality images using AI. 
  - This project combines LM Studio for prompt generation with ComfyUI for image creation, with embedded metadata for easy searching.
  - Tag-Based Generation: Create images based on customizable tags like subject, mood, setting, and style
  - LM Studio Integration: Generate detailed, creative prompts using advanced language models
  - ComfyUI Integration: Create high-quality images using the powerful ComfyUI backend
  - Metadata-Based Search: Search for images using embedded PNG metadata
  - Flexible Configuration: Customize all aspects of the generation process
  - Placeholder System: Use placeholders in workflows for dynamic content

- https://github.com/stavsap/comfyui-ollama /622Star/apache2/202508/python
  - Custom ComfyUI Nodes for interacting with Ollama using the ollama python client.
  - Integrate the power of LLMs into ComfyUI workflows easily or just experiment with LLM inference.

- https://github.com/mattjohnpowell/comfyui-lmstudio-image-to-text-node /MIT/202508/python
  - custom nodes for ComfyUI that deeply integrate LM Studio's capabilities using the official lmstudio Python SDK. 
  - It allows you to leverage locally run models for various generative tasks directly within your ComfyUI workflows.

- https://github.com/burnsbert/ComfyUI-EBU-LMStudio /MIT/202507/python
  - provides custom nodes for integrating with LMStudio, allowing for loading, managing, and making requests of LLM models through the LMStudio local server and command-line interface.
  - Load and manage LLM models directly from ComfyUI
  - Optional image model unloading to free up VRAM

- https://github.com/kijai/ComfyUI-moondream /202403/python/inactive
  - ComfyUI node to use the moondream tiny vision language model

- https://github.com/DadoIrie/ComfyUI_Dados_Nodes /MIT/202508/python/js
  - A collection of custom nodes for ComfyUI featuring AI vision models, advanced text processing tools, and wildcard prompt utilities.

- https://github.com/comfy-deploy/comfyui-llm-toolkit /33Star/NALic/202508/python
  - A custom node collection for integrating various LLM (Large Language Model) providers with ComfyUI.
  - Streaming Output directly on the node UI stream
  - Runs openai latest image model GPT-image-1 and we include various templates
  - Text generation using various LLM providers (OpenAI and local models, etc.)
  - Provider selection and configuration with dynamic model fetching
  - Seamless integration with ComfyUI workflows
  - Supported Providers: OpenAI (Default: gpt-4o-mini), Ollama (local)
  - When you change the LLM provider, the model dropdown updates dynamically with available models
  - Unified ONE-INPUT / ONE-OUTPUT Architecture
    - Toolkit uses a single "context" input/output approach for maximum flexibility
    - Cascading Data Flow: As data flows through nodes, it accumulates in the "context" structure. Preserve and accumulate data throughout the workflow
    - Chain multiple LLM operations with a single connection

- https://github.com/gokayfem/ComfyUI_VLM_nodes /apache2/202502/python/inactive
  - Custom ComfyUI nodes for Vision Language Models, Large Language Models, Image to Music, Text to Music, Consistent and Random Creative Prompt Generation
  - Utilizes `llama-cpp-python` for integration of LLaVa models. You can load and use any VLM with LLaVa models in GGUF format with this nodes.

- https://github.com/fblissjr/shrug-prompter /MIT/202508/python
  - ComfyUI nodes using uses local vision LLMs / VLMs (and other providers) optimized for wan2.2, wan2.1, and flux kontext.
  - memory-efficient VLM nodes for ComfyUI, with state management, looping, keyframe extraction, batching, and built-in templates for Wan2.1, VACE, and beyond.
  - Built for Wan2.1, WAN VACE, and FLUX Kontext, but obviously can be extended beyond that. The nodes are generic enough to work with any workflow that needs vision-to-text capabilities
  - Initially built and tested with my local (OpenAI API compatible and sorta ollama compatible) vision LLM server, https://github.com/fblissjr/heylookitsanllm, which works with any GGUF or MLX model. 
    - Most features will work with any OpenAI-compatible API endpoint

- https://github.com/if-ai/ComfyUI-IF_AI_PromptImaGen /MIT/202504/python
  - Lighter version of ComfyUI-IF_AI_tools is a set of custom nodes to Run Local and API LLMs and LMMs, supports Ollama, LlamaCPP LMstudio, Koboldcpp, TextGen, Transformers or via APIs Anthropic, Groq, OpenAI
  - https://github.com/if-ai/ComfyUI-IF_AI_tools /MIT/202412/python/inactive
    - https://ko-fi.com/impactframes
    - a set of custom nodes for ComfyUI that allows you to generate prompts using a local Large Language Model (LLM) via Ollama.
    - I am Moving the prompt generation to this new node PromptImaGen 
  - https://github.com/if-ai/ComfyUI-IF_LLM /MIT/202504/python
    - Run Local and API LLMs, Features Gemini2 image generation, DEEPSEEK R1, QwenVL2.5, QWQ32B, Ollama, LMStudio

- https://github.com/pupba/Rabbit-Hole /GPL/202507/python
  - Modular image generation pipeline for enterprise, research, and MLOps—custom flows, batch-ready, inspired by ComfyUI.
  - rabbit_hole was created to bring powerful, customizable image generation pipelines into enterprise and research environments.
  - While ComfyUI is highly visual and flexible, it has limitations for production use:
    - Node development is complex and not easily extensible.
    - Workflow customization requires internal code changes.
    - Integration with external Python libraries is difficult.
    - Maintaining reproducibility, batch operations, and versioned config is not straightforward.
  - rabbit_hole was built to solve these, enabling rapid, modular, and automated workflows—fully in Python and easy to extend.
    - Build custom flows as Python classes by connecting modular tunnel steps.
    - Use static, version-controlled YAML files for models, runtime, and batch settings.
# extensions/custom_nodes
- https://github.com/CheNing233/ComfyUI_Image_Pin /202507/python/js
  - 可以将图片固定到工作流的JSON中，随JSON迁移，也可以嵌入图像metadata
  - 钉住图片并转换为Base64字符串嵌入到工作流中
  - 支持压缩为WebP格式的Base64字符串
  - 嵌入图片到工作流，生成的图片的metadata也具有该图片, 方便分享
  - 节点部分代码来自 ComfyUI-Inspire-Pack

- https://github.com/Comfy-Org/ComfyUI-React-Extension-Template /GPL/202506/ts/vue
  - A minimal template for creating React/TypeScript frontend extensions for ComfyUI, with complete boilerplate setup.
  - ComfyUI API Integration: Properly typed access to ComfyUI's internal API
  - Auto-Reload Development: Watch mode for seamless development experience
  - Graph Manipulation: Programmatically manipulate the workflow graph
  - [Import app directly rather than waitForInit _202508](https://github.com/Comfy-Org/ComfyUI-React-Extension-Template/issues/14)
    - The template's `waitForInit` function (main.tsx:20-52) waits for `window.app` to exist to avoid trying to mount things before the vue app is setup (if I recall correctly)
    - The current ComfyUI Extension Lifecycle is: 1. init → 2. addCustomNodeDefs → 3. getCustomWidgets → 4. beforeRegisterNodeDef → 5. registerCustomNodes → 6. beforeConfigureGraph → 7. nodeCreated → 8. loadedGraphNode → 9. afterConfigureGraph → 10. setup
    - The template currently registers at step 10, missing critical steps 3 and 7.
    - Both approaches can be used together in the same extension 

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

- https://github.com/a63976659/ComfyUI-prompt-formula /MIT/202508/python
  - comfyui使用的提示词便捷输入节点，能够保存提示词预设文本
  - 提示词预设文本可以直接在`提示词预设文件夹`中进行添加、编辑、删除json文件

- https://github.com/aiaiaikkk/super-prompt-canvas /202506/python/js
  - 为 ComfyUI 设计的图像编辑提示词生成插件，通过可视化画布标注和AI辅助，快速生成精准的编辑提示词。
  - 可视化标注和AI辅助提示词生成

- https://github.com/yawiii/comfyui_prompt_assistant /675Star/GPL/202508/python/js
  - https://space.bilibili.com/520680644
  - 这是一个无需添加任何节点，即可实现提示词翻译、扩写、图片反推提示词、预设Tag插入、历史记录功能等功能的comfyUI插件。

- https://github.com/ComfyAssets/ComfyUI_PromptManager /MIT/202508/python
  - custom node that extends the standard text encoder with persistent prompt storage, advanced search capabilities, automatic image gallery system, and powerful ComfyUI workflow metadata analysis using SQLite.
  - Persistent Storage: Automatically saves all prompts to a local SQLite database
  - Advanced Web Interface: Comprehensive admin dashboard with metadata analysis
  - Automatically links generated images to their prompts
  - Uses SHA256 hashing to detect and prevent duplicate storage

- https://github.com/SanicsP/ComfyUI-CsvUtils /apache2/202508/python/js
  - A comfyui extension to manage prompts in a simple way using mainly csv files.
  - Nodes have no external dependencies, no need for the manager, the built-in python csv library is simply used

- https://github.com/flybirdxx/ComfyUI_Prompt_Helper
  - 专为 ComfyUI 设计的综合性自定义节点插件套件，提供强大的AI提示词生成功能。
  - 该插件套件包含视频提示词生成器和图片提示词生成器，支持中英文双语界面
- https://github.com/lihaoyun6/ComfyUI-QwenPromptRewriter
  - 使用千问大模型对提示词进行重写
- https://github.com/chenpipi0807/Comfyui-Qwen-image-edit-CharacterConsistency
  - ComfyUI 官方的 `TextEncodeQwenImageEdit` 节点简化了提示词工程，这个节点支持自定义系统提示词以增强灵活性

- https://github.com/pythongosssss/ComfyUI-Custom-Scripts /MIT/202508/python/js
  - Enhancements & experiments for ComfyUI, mostly focusing on UI features

- https://github.com/chflame163/ComfyUI_LayerStyle /2.5kStar/MIT/202508/python
  - A set of nodes for ComfyUI that can composite layer and mask to achieve Photoshop like functionality.
  - https://github.com/chflame163/ComfyUI_LayerStyle_Advance /MIT
    - The nodes detached from ComfyUI Layer Style are mainly those with complex requirements for dependency packages.

- https://github.com/Azornes/Comfyui-LayerForge /170Star/MIT/202508/python/ts
  - an advanced canvas node for ComfyUI, providing a Photoshop-like layer-based editing experience directly within your workflow.
  - It extends the concept of a simple canvas with multi-layer support, masking, blend modes, precise transformations, and seamless integration with other nodes.
  - Intuitive UI: Familiar controls like drag-and-drop, keyboard shortcuts, and a pannable/zoomable viewport make editing fast and easy.
  - Freeform Inpainting Area: Draw any custom (like a polygonal lasso tool) area directly inside the image for inpainting.
  - Persistent & Stateful: Your work is automatically saved to the browser's IndexedDB, preserving your full canvas state (layers, positions, etc.) even after a page reload.
  - Multi-Layer Editing: Add, arrange, and manage multiple image layers with z-ordering.
  - Comprehensive Undo/Redo: Full history support for both layer manipulations and mask drawing.

- https://github.com/alessandrozonta/ComfyUI-Layers /55Star/GPL/202407/python/inactive
  - custom node for ComfyUI allows you to create layers of an image based on input masks and save them into a PSD file.

- https://github.com/jtydhr88/ComfyUI-LayerDivider /202405/python/inactive
  - custom nodes that generating layered psd files inside ComfyUI, original implement is mattyamonaca/layerdivider
  - 依赖psd_tools、pytoshop
  - https://github.com/mattyamonaca/layerdivider /MIT/202308/python/inactive
    - A tool to divide a single illustration into a layered structure

- https://github.com/grinlau18/ComfyUI_XISER_Nodes /GPL/202508/python/js
  - 旨在提供交互式画布功能，方便用户在工作流中进行图像编辑与管理。
  - 节点支持加载多张图像，显示在画布上，用户可通过拖动、缩放、旋转等操作调整图像位置与大小，同时支持图层管理，选择和切换不同图层以进行精细编辑
  - 节点提供撤销、重做功能，方便操作回溯
  - Dependencies: Requires torch, PIL, numpy, opencv-python

- https://github.com/o-l-l-i/ComfyUI-Olm-ImageAdjust /NonComm/202508/python/js
  - An interactive image adjustment node for ComfyUI, with an easy-to-use graphical interface and realtime preview.
  - Built using only Pillow, Torch, and NumPy.
  - https://github.com/o-l-l-i/ComfyUI-Olm-ColorBalance /NonComm/202508/python/js
    - An interactive, color balance adjustment node for ComfyUI, featuring a clean interface and realtime preview.
  - https://github.com/o-l-l-i/ComfyUI-Olm-CurveEditor
    - A single-purpose, multi-channel curve editor for ComfyUI, providing precise color control over R, G, B, and Luma channels directly within the node graph.

- https://github.com/aiaiaikkk/ComfyUI-Curve /135Star/MIT/202508/python/js
  - Simple implementation of Photoshop Curves, HSL Mixer, Levels Adjustment, and Color Grading in ComfyUI.
  - ComfyUI专业色彩调整扩展，提供类似Photoshop的曲线、HSL、色阶调整功能，支持70+种预设风格、高级遮罩和Lightroom风格的色彩分级功能。
  - 类似Photoshop的专业曲线调整，支持多种插值方式
  - 双击节点打开Photoshop风格色阶调整界面：专业三点控制（黑场、灰场、白场）
  - 专业的图像直方图分析: 平均值、中位数、标准差等图像统计数据
  - 零延迟反馈：在弹出窗口中调整参数时图像实时更新，像使用专业图像编辑软件一样流畅

- https://github.com/rgthree/rgthree-comfy /2.2kStar/MIT/202508/ts
  - A collection of nodes and improvements created while messing around with ComfyUI.
  - Reroute, Bookmark, Image Comparer
  - A lot of the power of these nodes comes from Muting. Muting is the basis of correctly implementing multiple paths for a workflow utlizing the Context Switch node.
- https://github.com/lum3on/ComfyUI_logic-bypasser /202506/python/js
  - An advanced logic bypasser node for ComfyUI with automation support, inspired by the rgthree group bypasser architecture but enhanced for backend execution and programmatic control.
  - Works in ComfyUI's execution engine, not just frontend
  - Conditional Logic: Advanced condition evaluation

- https://github.com/quasiblob/ComfyUI-EsesImageCompare /NonModify/202508/python
  - a ComfyUI custom node designed for interactively viewing and comparing two images.

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

- https://github.com/Firetheft/ComfyUI_Local_Image_Gallery /70Star/202508/python/js
  - 一个为 ComfyUI 打造的终极本地图片、视频、音频媒体管理器
  - The Ultimate Local File Manager for Images, Videos, and Audio in ComfyUI
  - It eliminates the need to constantly switch to your OS file explorer
  - The gallery features a fluid waterfall (masonry) layout, smooth transitions, and an advanced lightbox viewer
  - Full Metadata Management: Tagging System, Star Rating
- https://github.com/Firetheft/ComfyUI_Civitai_Gallery /202508/python
  - custom node for ComfyUI that integrates a seamless image browser for the Civitai website directly into your workflow.
  - allows you to browse, search, and select images from Civitai and instantly import their prompts, negative prompts, and full-resolution images into your workflow.
  - speed up your creative process by eliminating the need to switch between your browser and ComfyUI.
  - The gallery features a fluid, responsive waterfall (masonry) layout that intelligently fills the available space, ensuring a beautiful and efficient browsing experience.

- https://github.com/zeitmaschinen/GalleryFlow /MIT/202507/python/ts
  - A modern web application for browsing and managing ComfyUI-generated images with advanced metadata support.
  - Workflow visualization for each image and copy JSON to clipboard
  - Recursively reads all folders, so you never miss an image
  - WebSocket support for real-time updates
  - Direct integration with ComfyUI workflows

- https://github.com/talesofai/comfyui-browser /605Star/NALic/202411/python/svelte/inactive
  - This is an image/video/workflow browser and manager for ComfyUI. 
  - You can sync your workflows to a remote Git repository and use them everywhere.
  - Browse and manage your images/videos/workflows in the output folder.
  - Some useful custom nodes like xyz_plot, inputs_select.
  - Install ComfyUI Manager, search comfyui-browser in Install Custom Node and install it.

- https://github.com/hayden-fr/ComfyUI-Image-Browsing /GPL/202508/ts/vue
  - Browsing Output Images in ComfyUI
  - Folder management

- https://github.com/giriss/comfy-image-saver /MIT/202308/python/inactive
  - All the tools you need to save images with their generation metadata on ComfyUI. 
  - Compatible with Civitai & Prompthero geninfo auto-detection. 
  - Works with png, jpeg and webp.
  - 支持保存prompt
- https://github.com/nkchocoai/ComfyUI-SaveImageWithMetaData /GPL/202503/python
  - Custom node for ComfyUI. Add a node to save images with metadata (PNGInfo) extracted from the input values of each node.
  - https://github.com/edelvarden/comfyui_image_metadata_extension /57Star/GPL/202508/python
    - a fork of nkchocoai/ComfyUI-SaveImageWithMetaData.
    - Included metadata for LoRa weights.

- https://github.com/audioscavenger/save-image-extended-comfyui /110Star/GPL/202406/inactive
  - Save as JXL, AVIF, WebP, JPEG, JPEG2k, customize the folder, sub-folders, and filenames of your images
  - Supports those extensions: JXL AVIF WebP jpg jpeg j2k jp2 png gif tiff bmp
- https://github.com/thedyze/save-image-extended-comfyui /202409/python/inactive
  - Customize the information saved in file- and folder names.
  - Save data about the generated job (sampler, prompts, models) as entries in a json (text) file, in each folder.

- https://github.com/lihaoyun6/ComfyUI-BlindWatermark /GPL/202506/python
  - 在生成的图片中嵌入不可见的隐形水印

- https://github.com/BigStationW/ComfyUi-Load-Image-And-Display-Prompt-Metadata /202508/python/js
  - This node displays the positive and negative prompts of a ComfyUi image.

- https://github.com/LEv145/images-grid-comfy-plugin /202405/python
  - https://civitai.com/models/31126
  - A simple comfyUI plugin for images grid (X/Y Plot)
  - XYZPlot, like in auto1111, but with more settings

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

- https://github.com/11cafe/comfyui-workspace-manager /1.3kStar/MIT/202408/python/ts/inactive
  - A ComfyUI workflows and models management extension to organize and manage all your workflows, models in one place.
  - [2025-4-16] since ComfyUI frontend has built-in workspace management feature now, this plugin becomes obsolete and will not be maintained anymore. 

- https://github.com/yichengup/ComfyUI-WorkflowManager /MIT/202508/python/js
  - 专为 ComfyUI 设计的高效工作流文件管理器插件。
  - 它提供了完整的文件系统操作功能
  - 双视图模式：列表视图（紧凑布局）+ 网格视图（预览模式）

- https://github.com/Nuked88/ComfyUI-N-Sidebar /560Star/MIT/202507/python
  - A simple sidebar for ComfyUI
  - In WORKFLOW PATHS, set the folder path to where your workflows are located
  - Search within your nodes
  - This new panel allows you to download CIVITAI models (Checkpoint, lora)

- https://github.com/chrisgoringe/cg-controller /75Star/MIT/202504/js
  - The Controller is a new way to interact with a Comfy workflow, in which just the nodes that you select are mirrored in the Controller, without you needing to make any changes to the workflow itself.
  - The controller gets saved with the workflow, so once you've set it up, it's always there for you. And if you share the workflow with someone else, they get your controller as well...

- https://github.com/yolain/ComfyUI-Easy-Use /1.9kStar/GPLv3/202508/python/js
  - custom nodes integration package, which is extended on the basis of TinyTerraNodes.
  - optimized for many popular awesome custom nodes to achieve the purpose of faster and more convenient use of ComfyUI
  - https://github.com/yolain/ComfyUI-Easy-Use-Frontend /202508/js/vue
    - New Front-end of ComfyUI-Easy-Use custom nodes. This repo will replace the original web_extension in future releases.
  - https://github.com/TinyTerra/ComfyUI_tinyterraNodes /GPL/202508/python/js
    - custom nodes for ComfyUI.
    - Fullscreen Image Viewer
    - Advanced XY(Z)Plot
    - Dynamic Widgets

- https://github.com/manifestations/comfyui-outfit /MIT/202508/python
  - A comprehensive outfit generation system for ComfyUI with AI-powered prompt enhancement and dynamic outfit composition.
  - generates AI-friendly outfit descriptions from configurable JSON data.
  - 20+ outfit categories (torso, legs, feet, accessories, etc.)
  - JSON-Based Data: Easily customizable outfit options via JSON files

- https://github.com/phyblas/paint-by-example_comfyui /202508/python
  - 这个包是提供用来在comfyui执行paint by example的节点。
  - 这个方法是inpaint类似的。可以把作为范例的图片插入到原本图片中所要的地方。不必须要写任何提示词。但结果也可能不太像范例的图。虽然如此有时候会导出很有意思的结果。
  - 首次执行节点的时候会自动从huggingface下载paint-by-example模型，所以要等一段时间并且会占用大于5GB的硬盘。
  - https://github.com/Fantasy-Studio/Paint-by-Example
    - Exemplar-based Image Editing with Diffusion Models

- https://github.com/whmc76/ComfyUI-UniversalToolkit /42Star/MIT/202508/python
  - 提供丰富的图像处理、音频处理、掩码操作和实用工具节点，支持批量处理、智能分析、色彩迁移等多种高级功能。
  - 图像处理：色彩迁移、图像拼接、尺寸调整、深度图模糊等
  - 音频处理：音频加载、裁剪、重采样、增益调节等
  - 智能预设：32种Kontext VLM系统预设，支持动态场景描述

- https://github.com/yondonfu/comfystream /105Star/MIT/202508/python/js
  - a package for running img2img Comfy workflows on video streams.
  - This repo also includes a WebRTC server and UI that uses comfystream to support streaming from a webcam and processing the stream with a workflow JSON file (API format) created in ComfyUI. 
  - https://github.com/livepeer/comfystream
    - A custom ComfyUI node for running real-time media workflows directly within ComfyUI
    - a package for running img2img Comfy workflows on video streams.
  - 🍴 forks
  - https://github.com/creativeplatform/comfystream_inside
  - https://github.com/ryanontheinside/comfystream_inside

- https://github.com/crystian/ComfyUI-Crystools /1.4kStar/MIT/202508/python/ts
  - A powerful set of tools for ComfyUI
  - you can see the resources monitor, progress bar & time elapsed, metadata and compare between two images, compare between two JSONs
# utils
- https://github.com/Comfy-Org/ComfyUI_devtools /21Star/202505/python/inactive
  - ComfyUI developer tools (Custom Node)

- https://github.com/xingren23/ComfyFlowApp /584Star/GPL/202403/python/archived
  - https://comfyflow.app/
  - ComfyFlowApp is a tool to help you develop AI webapp from ComfyUI workflow and share to others.
  - offers an in-built test account(username: demo) with the credentials(password: comfyflowapp)
  - [API是否支持自建？ _202403](https://github.com/xingren23/ComfyFlowApp/issues/65)
    - 如果只是想自己用，不提供登录服务的话,也可以直接改下代码返回。 本地用用是可以的
    - API for user login only

- https://github.com/MixLabPro/comfyui-mixlab-nodes /1.7kStar/MIT/202507/python/js
  - 新增 AppInfo 节点，可以通过简单的配置，把 workflow 转变为一个 Web APP。
  - 支持多个 web app 切换
  - 发布为 app 的 workflow，可以在右键里再次编辑了

- https://github.com/yuyou-dev/ComfyUI_workflow2app /MIT/202412/python/js
  - 教学项目：ComfyUI的工作流如何开发成app
  - 1. 在ComfyUI中搭建并运行成功任意工作流。
  - 2. 在ComfyUI中，配置开发模式，允许通过Save(API Format)的形式下载可用于API搭建的工作流版本。
  - 3. 将编辑完成的workflow工作流下载到本地。
  - 4. 部署workflow的后端模块，开发对应的API接口。
  - 5. 开发「app / 小程序」的前端业务逻辑。
  - 6. 调试 / 部署 / 上线
- https://github.com/shadowcz007/comfyui-plugins /MIT/202311/ts/inactive
  - Plugins：把任意comfyUI的工作流变成一个应用
  - Comfyui提供了编辑器、后端服务，缺少了一个使用端。 当创作者创建了属于自己的工作流之后，下一次使用还需要同样的界面打开，其他不需要的功能（或者节点）无法隐藏。 类似于游戏引擎，在编辑器里制作好游戏之后，需要打包成一个用户友好的交互界面使用。

- https://github.com/ronaldzgithub/ComfyUI_Appstore /apache2/202412/python/js
  - a framework to turn comfyui workflows to web apps
  - 增加运行过程显示

- https://github.com/queiul/MeldUI /202412/NonOpen
  -  A ComfyUI client app that will help Manage and Generate Images with Ease

- https://github.com/Comfy-Org/ComfyUI-embedded-workflow-editor /12Star/NALic/202505/ts
  - https://comfyui-embedded-workflow-editor.vercel.app/
  - In-place embedded workflow-exif editing experience for ComfyUI generated media files. 
  - Edit workflow data embedded in PNG, WEBP, FLAC, MP3, and MP4 files directly in your browser.
  - Requirements: - Bun — A fast all-in-one JavaScript runtime
  - https://github.com/comfyui-wiki/ComfyUI-Workflow-JSON-Editor /202508/js
    - https://comfyui-wiki.github.io/ComfyUI-Workflow-JSON-Editor/
    - A tool for helping edit ComfyUI workflow's model link.

- https://github.com/hayden-fr/ComfyUI-Model-Manager /146Star/GPL/202508/python/ts/vue
  - Download, browse and delete models in ComfyUI.

- https://github.com/willmiao/ComfyUI-Lora-Manager /579Star/GPLv3/202508/python/js
  - A comprehensive toolset that streamlines organizing, downloading, and applying LoRA models 
  - powerful features like recipe management, checkpoint organization, and one-click workflow integration
  - Installation
    - Option 1: ComfyUI Manager (Recommended for ComfyUI users)
    - Option 2: Portable Standalone Edition (No ComfyUI required), You can now run LoRA Manager independently from ComfyUI

- https://github.com/Firetheft/ComfyUI_Local_Lora_Gallery /202508/python/js
  - 一个为 ComfyUI 打造的，用于管理和应用多个 LoRA 模型的可视化图库节点
  - 用一个直观的、基于卡片的视觉界面取代了标准的下拉式LoRA加载器
  - 本插件还集成了对 comfyui-nunchaku 的可选支持，可在兼容模型（如FLUX）上实现显著的性能加速。

- https://github.com/sn0w12/ComfyUI-Sn0w-Scripts /MIT/202508/python
  - a collection of nodes and improvements created for lora management
  - A major focus for me was making loras more manageable by letting users create their own lora loaders with specific folder paths and automatically loading loras based on tags. 
  - Allows creation of new LoRa loaders by specifying their name and path.

- https://github.com/bytedance/comfyui-lumi-batcher /401Star/GPLv3/202508/python/ts
  - 专为 ComfyUI 设计的批量处理扩展插件，旨在提升 AIGC 创作效率，是一个调参抽卡、批量出素材的利器
  - 不局限在 xyz 三维参数的交叉调试，而是 workflow 内的所有参数均可交叉，一次完成所有调试
  - 批量调试可以是多个参数的组合体，如「商品图 + 对应 prompt」 X 不同基模
  - 多维表格，自由抽卡预览或批量导出：不同参数的聚合浏览方式

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

- https://github.com/zjf2671/hh-mcp-comfyui /15Star/MIT/202507/python
  - 这是一个基于Model Context Protocol (MCP)的ComfyUI图像生成服务，通过API调用本地ComfyUI实例生成图片
  - 支持动态替换工作流中的提示词和尺寸等参数
  - 必须确保本地ComfyUI实例正在运行(默认地址: http://127.0.0.1:8188)
  - 图片尺寸默认为1024x1024
  - 自动加载workflows目录下的工作流文件作为资源
  - 服务启动时会自动加载workflows目录下的所有JSON工作流文件
  - 如果使用你本地的comfyui工作流的话，先要保证你的工作流能在comfyui正常运行，然后需要导出(API)的JSON格式，并放入到你本地的`/path/hh_mcp_comfyui/workflows`目录中

- https://github.com/ericwanghp/ComfyUI_MCP /MIT/202505/python
  - 为 ComfyUI 设计的松耦合、可扩展、配置驱动的模型上下文协议（ModelContextProtocol）服务端。
  - 支持依据客户定制工作流可扩展MCP服务(tool) 如: txt2img、img2img，每个MCP服务(tool)的参数和行为均可通过 JSON初始化和MCP工具装饰器模块灵活扩展，适合 AI 绘图、推理等场景的自动化与集成。

- https://github.com/MarcusYuan/mcp-comfyui-anything /202507/python
  - 针对 ComfyUI 工作流管理难题的智能执行引擎
  - 两个主要挑战：
    - 工作流碎片化：用户常为不同任务创建多个变体工作流（如文生图/图生图/视频生成）
    - 参数管理复杂：每个工作流可能有数十个可调参数（提示词、采样步数、ControlNet 权重等）
  - 即插即用：用户只需将 ComfyUI 工作流保存为 .json 文件并添加轻量级模板（_tp.json）
  - 自动识别工作流中的可配置节点（如 CLIP 文本编码器、KSampler 等）
  - 模板系统：通过 `{参数}` 占位符将技术参数转化为用户友好配置项
  - 工具1 (list_workflows)：工作流枚举器，提供可用工作流清单
  - 工具2 (analyze_and_execute)：智能分析器，分析用户需求并生成工作流补丁
  - 工具3 (execute_workflow)：纯执行引擎，执行两级融合和ComfyUI调用
  - 工具2不直接调用工具3，而是通过返回引导信息让Client LLM自动调用工具3, 符合FastMCP最佳实践
  - 提供实时执行反馈和进度跟踪
  - 依赖FastMCP、Pydantic、HTTPX、aiofiles、deepmerge、watchdog

- https://github.com/felixszeto/ComfyUI-RequestNodes /91Star/MIT/202508/python
  - a custom node plugin for ComfyUI that provides functionality for sending HTTP requests and related utilities. 
  - Rest Api Node: A versatile node for sending various HTTP methods (GET, POST, PUT, DELETE, PATCH, HEAD, OPTIONS) with retry settings.
  - Key/Value Node: Creates key/value pairs for building request parameters, headers, or other dictionary-like structures.
  - Retry Settings Node: Creates retry setting configurations for the Rest Api Node.
  - https://github.com/jtydhr88/comfyui-http-api /MIT/202507
    - custom nodes for interacting with ComfyUI's internal HTTP APIs, such as fetching files from workflows.

- https://github.com/Starnodes2024/ComfyUI_StarBetaNodes /202508/python/js
  - This is a playground and test playground for coming nodes
  - a staging ground for experimental custom nodes for ComfyUI. Most beta nodes have now been released to the main ComfyUI_StarNodes repository. 

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

- https://github.com/ty0x2333/ComfyUI-Dev-Utils /146Star/MIT/202507/python/js
  - Execution Time Analysis, Reroute Enhancement, Remote Python Logs, For ComfyUI developers.

- https://github.com/tzwm/comfyui-profiler /202408/python/js/inactive
  - Calculate the execution time of all nodes.

- https://github.com/jordenyt/stable_diffusion_sketch /122Star/GPLv3/202506/java
  - an Android client app that connect to your own ComfyUI or A1111-sd-webui
  - This app integrates with ComfyUI via a RESTful API, enabling powerful AI image generation capabilities right from your mobile device.
  - https://github.com/jordenyt/ComfyuiGW /202508/python
    - https://github.com/jordenyt/stable_diffusion_sketch/tree/comfyui
    - a RESTful API Gateway designed specifically for running ComfyUI version of Stable Diffusion Sketch. 
    - It provides a robust interface for executing complex workflows through both API endpoints and a user-friendly web interface.
    - Real-time Progress Tracking - Monitor workflow execution with live updates

- https://github.com/eltonkola/ComfyFlux /apache2/202408/kotlin/inactive
  - simple android client for ComfyUi and Flux workflows

- https://github.com/d3x-at/sd-parsers /MIT/202504/python
  - A Python library to read metadata from images created by Stable Diffusion.
  - Prompts as well as some well-known generation parameters are provided as easily accessible properties (see Output).
  - support: sd-webui, ComfyUI

- https://github.com/StableLlama/ComfyUI-basic_data_handling /GPL/202507/python 
  - Basic Python functions for manipulating data that every programmer is used to. 
  - These nodes are very lightweight and require no additional dependencies.

- https://github.com/bentoml/comfy-pack /174Star/apache2/202508/python/js
  - a comprehensive toolkit for reliably packing and unpacking environments for ComfyUI workflows.
  - Pack workflow environments as artifacts: Saves the workflow environment in a `.cpack.zip` artifact with Python package versions, ComfyUI and custom node revisions, and model hashes.
  - Deploy workflows as APIs: Deploys the workflow as a RESTful API with customizable input and output parameters.
  - [comfy-pack: Serving ComfyUI Workflows as APIs _202412](https://www.bentoml.com/blog/comfy-pack-serving-comfyui-workflows-as-apis)
    - once you’ve built a workflow and want to run it in production, new challenges arise.
    - Limited portability: Workflows can't be easily packaged and deployed elsewhere while maintaining consistent behavior. Users must manually manage Python dependencies, download custom nodes, and source specific model versions.
    - No scaling capabilities: ComfyUI doesn’t support dynamic scaling, such as scaling down to zero when idle or scaling up to handle high traffic
    - `comfy-pack` ensures consistency by locking the versions of every component in the workflow, such as custom nodes (pinned to its exact Git commit hash), Python packages, and ComfyUI version
    - you can deploy your ComfyUI workflow to BentoCloud, our AI inference platform 

- https://github.com/martijnat/comfyui-previewlatent /GPL/202508/python
  - ComfyUI plugin for previewing latents without vae decoding

- https://github.com/LarryJane491/Lora-Training-in-Comfy /505Star/NALic/202401/python/inactive
  - This custom node lets you train LoRA directly in ComfyUI
  - By default, it saves directly in your ComfyUI lora folder. That means you just have to refresh after training

- https://github.com/Tessera-C/Comfy_augment /GPL/202508/python/jupyter
  - Comfy Augment is a powerful data augmentation pipeline designed to generate synthetic data using generative models, based on the ComfyUI framework. 
  - It provides a comprehensive workflow for data preprocessing, image generation, and quality assessment, enabling users to expand their datasets with high-quality synthetic images.
  - This project is particularly useful for computer vision tasks where large amounts of varied data are required for training robust models.
  - Automated Generation: A script (run_pipeline.py) to automate the image generation process using configurable workflows.
  - Quality Assessment: Tools to measure the quality of generated images (e.g., using LPIPS, DreamSim, FID).

- https://github.com/calcuis/gguf-pack /GPL/202508/python/js
  - gguf portable pack for picture/audio/video generation
  - major difference between gguf-pack and comfy
    - gguf is a core node in gguf-pack
    - gguf is a custom node in comfy
  - ui-codebase: comfy
  - base: llama.cpp

- https://github.com/christian-byrne/python-interpreter-node /202504/python/inactive
  - Embed scripts into workflows. Alter the node's input/outputs with python.
  - Write Python code that executes when the workflow is queued
  - The stdout/err (e.g., prints, error tracebacks) are displayed in the node.
# integrations
- https://github.com/nomcycle/comfyui-dev /MIT/202506
  - A secure, remote, and persistent development environment for ComfyUI that works with cloud GPU services. 
  - This container combines Tailscale's secure VPN service with VSCode's remote development capabilities, making it perfect for developing on services like RunPod.

- https://github.com/nchenevey1/gimp-comfy-tools /91Star/GPL/202507/python
  - GIMP plugins that communicate with ComfyUI. 
  - Currently uses Power Lora Loader (rgthree)

- https://github.com/MoonHugo/ComfyUI-FFmpeg /100Star/apache2/202508/python
  - 把FFmpeg常用功能封装成ComfyUI节点，方便用户可以在ComfyUI上也可以进行各种视频处理。
  - Video2Frames节点: 作用是将视频转为一张一张的图片，并保存到指定目录中
  - Frames2Video节点: 作用是将图片转为视频，并保存到指定目录中

- https://github.com/jtydhr88/ComfyUI-OpenCut /202508/ts/vue
  - a ComfyUI plugin that integrated OpenCut into ComfyUI, originally developed by OpenCut

- https://github.com/itsPreto/tangent /277Star/apache2/202502/python/js/inactive
  - Tangent is a canvas for exploring AI conversations, treating each chat branch as an experiment you can merge, compare, and discard.
  - Branch & Explore: Effortlessly create conversation forks at any point to test multiple approaches or ideas.
  - Offline-First: Fully powered by local models, leveraging Ollama with plans to expand support.
  - compatibility with Claude and ChatGPT data exports

- https://github.com/Lingyuzhou111/Comfyui_Free_Jimeng
  - 将即梦AI的强大图片生成功能集成到ComfyUI中的官方插件
  - https://github.com/Yunwuxin-666/Comfyui-Jimeng-api
    - 为 ComfyUI 提供了火山引擎即梦AI的四个核心功能：t2i, i2i, t2v, vlm
# workflows
- https://github.com/pwillia7/Basic_ComfyUI_Workflows /202508
  - Basic Stable Diffusion Workflows for ComfyUI using minimal custom nodes
  - This is meant to be a good foundation to start using ComfyUI in a basic way.
  - You can import the JSON files or the PNGs into Comfy to use the workflows. Most workflows are built for SDXL by default but can be changed easily to work with other SD versions.
  - simply clone this repo into your ComfyUI custom_nodes directory. ComfyUI will automatically detect 

- https://github.com/comfyanonymous/ComfyUI_examples /202508
  - https://comfyanonymous.github.io/ComfyUI_examples/
  - Examples of ComfyUI workflows
  - All the images in this repo contain metadata which means they can be loaded into ComfyUI
  - https://github.com/Comfy-Org/workflow_templates

- https://github.com/heshengtao/comfyui_LLM_party /1.9kStar/AGPL/202508/python
  - aims to develop a complete set of nodes for LLM workflow construction based on comfyui as the front end. 
  - It allows users to quickly and conveniently build their own LLM workflows and easily integrate them into their existing image workflows.
  - [‌‍⁤⁢‍‌⁢‌‌关于LLM-party的一切 - 飞书云文档](https://dcnsxxvm4zeq.feishu.cn/wiki/IyUowXNj9iH0vzk68cpcLnZXnYf)
  - https://github.com/heshengtao/Let-LLM-party
    - 学会LLM Party

- https://github.com/ZHO-ZHO-ZHO/ComfyUI-Workflows-ZHO /GPL/202412/inactive
  - 我的 ComfyUI 工作流合集 

- https://github.com/dicksondickson/dickson-sci-fi-enhance-upscale /202505
  - These are ComfyUI workflows to upscale images to 2K, 4K, or 8K.
  - These workflows upscales images in multiple stages using a combination of upscaling models, CCSR, SUPIR and Ulitmate SD Upscale, upscaling models, SDXL and Flux.
  - Each workflow is tuned to a specific resolution with different speed variants. These workflows are continuing evolving.

- https://github.com/yaiol/ComfyUI-Workflows /202508
  - Each workflow is named using following convention: [Category]-[Workflow]-[Model]-[Method]

- https://github.com/edenartlab/workflows /202507
  - the official repository of all production-ready ComfyUI workflows for Eden.art.

- more-flows
  - https://github.com/dci05049/Comfyui-workflows
  - https://github.com/cubiq/ComfyUI_Workflows
# sd-api/server
- https://github.com/comfyanonymous/ComfyUI/blob/master/script_examples/basic_api_example.py
  - [How to Use ComfyUI API with Python: A Complete Guide _202503](https://medium.com/@next.trail.tech/how-to-use-comfyui-api-with-python-a-complete-guide-f786da157d37)
    - export workflow-api.json
    - customize prompt text
    - init websocket
    - exec `/prompt` as queue
    - Monitor Execution Status with websocket
    - get result image and info, close websocket

- https://github.com/yushan777/comfyui-api-part1-basic-workflow /202312/python/inactive
  - [ComfyUI : Using the API : Part 1. Controlling ComfyUI via Script _202309](https://medium.com/@yushantripleseven/comfyui-using-the-api-261293aa055a)
  - [ComfyUI : Using the API : Part 2. Digging a Bit Deeper _202309](https://medium.com/@yushantripleseven/comfyui-using-the-api-part-2-daac17fd2727)
  - [ComfyUI : Using the API : Part 3. Controlling An img2img Workflow _202312](https://medium.com/@yushantripleseven/comfyui-using-the-api-part-3-5042da5fc75c)
- https://github.com/ZYJ-3721/ComfyUI-API-Client /202411/python/inactive
  - 调用ComfyUI的API实现文生图和图生视频

- https://github.com/Phando/ComfyUIImageServer /GPL/202405/js
  - A server to run workflows against a ComfyUI server

- https://github.com/nexmoe/serverless-comfyui /91Star/MIT/202502/ts/inactive
  - 一个基于 Docker 的 ComfyUI 弹性 Serverless 应用，提供完整的前后端分离架构和用户友好的界面。
  - 基于nextjs的前端
  - 项目的图片上传功能需要配置 S3 存储服务。你可以使用 AWS S3 或其他兼容 S3 协议的对象存储服务（如 MinIO）

- https://github.com/CrazyBoyM/ComfyUI2API /apache2/202408/python/inactive
  - 一个把ComfyUI工作流转换为API服务的服务
  - 基于本地websocket通信实现数据转发，用于让ComfyUI变成一个通用的API服务

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

- https://github.com/realazthat/comfy-catapult /26Star/MIT/202407/python/inactive
  - Python library to programmatically schedule ComfyUI workflows via the ComfyUI API
  - a library for scheduling and running ComfyUI workflows from a Python program, via the existing API endpoint. 
  - ComfyUI API Pydantic Schema
  - Download the example workflow, and export it in the API format
  - https://github.com/realazthat/comfy-catapult-fastapi /MIT/202402/python
    - This is a demo of how to use the ComfyUI to serve workflows to public facing users using the ComfyUI API, Comfy Catapult, your workflows, and FastAPI.

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

- https://github.com/Netwrck/stable-diffusion-server /53Star/MIT/202507/python
  - 🖼️ Image Generation API Server - Similar to https://text-generator.io but for images
  - Simple interface for generating images in Gradio locally and easy to use FastAPI docs/server for advanced users.
  - Running the Gradio UI: python gradio_ui.py
  - Local Deployment: Run locally for style transfer, art generation and inpainting.

- https://github.com/piyushK52/comfy_runner /235Star/NALic/202411/python/inactive
  - Automatically install ComfyUI nodes and models and use it as a backend
  - This tool automatically downloads all the necessary nodes and models and executes the provided workflow. 
  - This repo can make it easier for people to use ComfyUI as a backend.
  - Executes the workflow without starting the UI server
  - Auto installs missing nodes
  - Link to custom nodes and models can be provided for installation/Setup

- https://github.com/bobvinch/comfy-server /525Star/NALic/202405/ts/nestjs/inactive
  - comfyui server to use comfyui API as easy as send a message
  - 核心功能1：ComfyUI的绘画API服务和websocket转发，客户端必须使用socketIO链接，WS无法连接
  - 核心功能2：方便将任意comfyui工作转换为在线API，向外提供AI能力
  - 修复Redis相关问题，增加容器一键部署方式
  - 天然支持利用nginx直接实现负载均衡, ComfyUI server之间可以共享AI绘画能力

- https://github.com/Acly/comfyui-tooling-nodes /540Star/GPL/202508/python/js
  - Provides nodes and API geared towards using ComfyUI as a backend for external tools.
  - Send and receive images directly without filesystem upload/download.
  - ComfyUI exchanges images via the filesystem. This requires a multi-step process (upload images, prompt, download images), which invites a whole class of potential issues you might not want to deal with.

- https://github.com/matan1905/ComfyUI-Serving-Toolkit /69Star/202410/python/inactive
  - a node toolkit to allow serving your workflow (for example using discord
  - This toolkit is designed to simplify the process of serving your ComfyUI workflow, making image generation bots easier than ever before.
  - Serve from your own computer, workflow is not inserted into the images so your secrets are 100% safe
  - Support for multiple serving options: Discord, Telegram, HTTP and WebSockets

- https://github.com/luckkyzhou/ComfyUI-API-Integration /MIT/202411/python/inactive
  - This project provides a comprehensive suite for developers to integrate ComfyUI APIs and automate image generation workflows. 
  - By encapsulating API input and output, this suite enables developers to input any workflow json file and receive the processed output image directly. 
  - Allows users to input images and receive the processed result based on selected workflows.

- https://github.com/9elements/comfyui-api /129Star/202402/python/inactive
  - You need a comfyUI server running and be able to access the "/ws" path for this server. If you have the server running localy it usually runs under "127.0.0.1:8188".
  - For simple prompt to image generation load the `base_workflow.json` and call `prompt_to_image` method with your desired parameters. 
  - For image to image generation load the `basic_image_to_image.json` and put your input image in the `input` folder. Call `prompt_image_to_image` with your desired parameters.

- https://github.com/SharCodin/comfy-gradio-api /202401/python/inactive
  - building a Python API to connect Gradio and Comfy UI for AI image generation with Stable Diffusion models.
  - connect a Gradio front-end interface to a Comfy UI backend

- https://github.com/deimos-deimos/comfy_api_simplified /MIT/202411/python/inactive
  - This is a small python wrapper over the ComfyUI API. 
  - It allows you to edit API-format ComfyUI workflows and queue them programmatically to the already running ComfyUI.
  - Only Basic auth and no auth (for local server) are supported.

- https://github.com/comfy-addons/comfy-station /28Star/MIT/202508/ts/依赖多
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
  - Download Pre-built Stable Diffusion Bentos 似乎是定制sd发行版
  - https://github.com/bentoml/BentoDiffusion

- https://github.com/Haidra-Org/hordelib /65Star/AGPL/202501/python/inactive
  - https://hordelib.org/
  - a wrapper around ComfyUI primarily to enable the AI Horde to run inference pipelines designed visually in the ComfyUI GUI.
  - The goal here is to be able to design inference pipelines in the excellent ComfyUI, and then call those inference pipelines programmatically. 
  - https://github.com/Haidra-Org/AI-Horde /1.3kStar/AGPL/202507/python
    - The AI Horde is a free community service that lets anyone create AI-generated images and text.
    - AI Horde lets volunteers share their computer power through workers to help others create AI art and writing.
    - When you make a request - like asking for "a painting of a sunset over mountains" - the AI Horde system finds available volunteer computers that can handle your job.
# sd-ui/webapp
- https://github.com/ImDarkTom/ComfyUIMini /288Star/AGPL/202501/ts/inactive
  - A mobile-friendly WebUI to run ComfyUI workflows.
  - Ensure ComfyUI is installed and functional (minimum v0.2.2-50-7183fd1 / Sep. 18th release).
  - [I created a frontend for ComfyUI that lets you run workflows from a mobile device : r/comfyui _202407](https://www.reddit.com/r/comfyui/comments/1eeimeu/i_created_a_frontend_for_comfyui_that_lets_you/)
    - It's meant to be run on the same machine alongside ComfyUI but you should be able to port forward
    - Be warned that authentication is not yet implemented so there may be a risk as anyone will be able to connect to it.
    - 👀 the only way I'm able to make this work is to use the "Save (API Format)" button in Comfy and then upload the resulting json. I tried uploading a regular workflow and it never worked 
  - [I created a frontend for ComfyUI that lets you run workflows from a mobile device : r/StableDiffusion _202407](https://www.reddit.com/r/StableDiffusion/comments/1eeijnw/i_created_a_frontend_for_comfyui_that_lets_you/)
    - It uses the built-in ComfyUI API to send data back and forth between the comfyui instance and the interface.
    - Using images as input (for masks and etc) is not yet implemented but will be added in a later update.
    - You need to put the full path so in your case `F:\ComfyUI\models\checkpoints`;

- https://github.com/jac3km4/comfyweb /72Star/MIT/202506/ts/svelte
  - a simple interface for ComfyUI that replaces graphs with beautiful forms.
  - A unified gallery view that allows you to easily preview, edit and manage both generated images as well as anything that's pending in the queue.
  - This project builds into a single HTML file. 

- https://github.com/diStyApps/ComfyUI-disty-Flow /556Star/202501/python/js/inactive
  - a custom node designed to provide user-friendly interface for ComfyUI by acting as an alternative user interface for running workflows. It is not a replacement for workflow creation.

- https://github.com/canisminor1990/kitchen-comfyui /228Star/MIT/202304/python/ts/inactive
  - A reactflow base stable diffusion GUI as ComfyUI alternative interface
  - clone ComfyUI source code and replace `ComfyUI/web` frontend with release build

- https://github.com/space-nuko/ComfyBox /669Star/GPL/202308/jupyter/ts/svelte
  - Customizable Stable Diffusion frontend for ComfyUI
  - It uses ComfyUI under the hood for maximum power and extensibility.
  - An installation of vanilla ComfyUI for the backend

- https://github.com/asantanna/DNNE-UI-Frontend /GPL/202508/ts/vue
  - Front end implementation of DNNE (Based off ComfyUI fork)
  - Vue.js-based visual editor
  - https://github.com/asantanna/DNNE-UI /GPL/202508/python
    - Distributed Neural Network Editor based on ComfyUI
    - DNNE is a visual programming environment for building neural networks and robotics control systems.
    - It transforms ComfyUI's visual node-based interface from a diffusion model platform into a comprehensive ML/robotics development environment with code export capabilities.

- https://github.com/lllyasviel/stable-diffusion-webui-forge /11.4kStar/AGPL/202506/python
  - a platform on top of Stable Diffusion WebUI (based on Gradio)
  - Forge is currently based on SD-WebUI 1.10.1 at this commit. (Because original SD-WebUI is almost static now, Forge will sync with original WebUI every 90 days, or when important fixes.)
  - [Forge Is Not Using ComfyUI as A Backend _202402](https://github.com/lllyasviel/stable-diffusion-webui-forge/discussions/169)
    - The backend is WebUI backend with Forge optimizations. (We call it Forge backend.)
    - Forge is not using Comfy as backend. But adopt lot of techniques and code used in comfy.  some of addon modules are just copied from comfy with some modification.
    - i agree, comfyui is NOT the backend 1:1; but most/a lot of the code used in the backend is comfy's code (with a1111 compat fixes which have been known to comfy users for a while now)
  - https://github.com/Panchovix/stable-diffusion-webui-reForge /202508/archived

- https://github.com/Haoming02/sd-webui-forge-classic /187Star/AGPL/202508/python
  - "Classic" mainly serves as an archive for the "previous" version of Forge, which was built on Gradio 3.41.2 before the major changes were introduced.
  - this fork is focused exclusively on SD1 and SDXL checkpoints, having various optimizations implemented, with the main goal of being the lightest WebUI without any bloatwares.
  - Most base features of the original Automatic1111 Webui should still function
  - Support `uv` package manager
    - 🐛 仅提供了windows下执行的.bat脚本，未提供linux/mac的shell脚本
  - Support new LoRA architectures
  - Support NoobAI Inpaint ControlNet
  - [2025-07-19: reForge development will continue (for now). · Panchovix/stable-diffusion-webui-reForge](https://github.com/Panchovix/stable-diffusion-webui-reForge/discussions/377)
    - As for classic, I'm pretty happy with its current state now. So I'll primarily focus on fixing and improving existing features, rather than adding more features.
    - Lately, I've been working on my own Gradio4-based branch: neo. Yes, I'm drinking the Chroma and Kontext Kool-Aid XD

- https://github.com/camenduru/stable-diffusion-webui-portable
  - This Project Aims for 100% Offline Stable Diffusion (People without internet or with slow internet can get it via USB or HD-DVD)

- https://github.com/cmdr2/stable-diffusion-ui
  - The easiest way to install and use Stable Diffusion on your computer.
# devops
- https://github.com/Tavris1/ComfyUI-Easy-Install /170Star/MIT/202508/bat
  - Portable ComfyUI for Windows, macOS and Linux 
  - Pixaroma Community Edition 

- https://github.com/ParisNeo/comfyui_proxy_server /apache2/202403/python/inactive
  - a lightweight reverse proxy server designed for load balancing and rate limiting.

- https://github.com/l3lackcurtains/Comfy_UI_Backend /202506/python
  - A Python-powered API backend featuring a custom Comfy UI, seamlessly integrated with Docker and Kubernetes for modern containerization and orchestration. 
  - Scalable, reliable, and built for efficient deployment

- https://github.com/Good-Dream-Studio/ComfyUI-Connect /17Star/MIT/202507/python
  - Expose your workflows into HTTP endpoints directly from ComfyUI itself.
  - Auto Documentation - Show all your workflows in OpenAPI format using `/api/connect` internal endpoint
  - Install by cloning this project into your `custom_nodes` folder.
  - Caching is not limited to Load Checkpoint. Each node keeping stuff in memory like models will benefit from caching.
  - A ComfyUI-Connect plugin to convert ComfyUI into a REST API, and a separate NodeJS Gateway server to handle them in a load balanced cluster.
  - [Made a custom node to turn ComfyUI into a REST API : r/comfyui _202505](https://www.reddit.com/r/comfyui/comments/1kef4xo/made_a_custom_node_to_turn_comfyui_into_a_rest_api/)
    - I’ve built a custom node for ComfyUI that lets you expose your workflows as lightweight RESTful APIs with minimal setup and smart auto-configuration.
    - I know there is already a Websocket system in ComfyUI, but it feel cumbersome.
    - Also I am building a gateway package allowing to clusterize and load balance requests
    - Can the original workflow still be used as it is in comfyui?
      - yup.
    - how does this differ to using API exported from the built in comfyui api connection in python?
      - It's basically the same, but with automation. 'Save API Endpoint' exports your current workflow to `user/default/ComfyUI-Connect/`workflows using the API format, and all the files in that folder are served as standalone API endpoints.
      - there's dynamic node input editing using `$` tags for prompts
  - https://github.com/Good-Dream-Studio/comfy-connect-gateway /MIT/202506/ts
    - Create a cluster of your ComfyUI Connect instances.
    - Works behind NAT - Your ComfyUI instances don't need to be directly accessible with IP, they connects directly to the gateway using websocket.

- https://github.com/comfy-deploy/comfydeploy /362Star/GPLv3/202509/python/ts
  - https://app.comfydeploy.com/
  - https://github.com/comfy-deploy/api /GPL/python
  - https://github.com/comfy-deploy/app /GPL/ts
  - TL; DR: We are open-sourcing ComfyDeploy again, with full platform backend + frontend.
  - [Re: Open-sourcing ComfyDeploy - Comfy Deploy _20250916](https://www.comfydeploy.com/blog/re-open-sourcing-comfydeploy)
    - In late 2023, I started ComfyDeploy as an open source project while I was working at my previous company. 
    - We got into YC with ComfyDeploy around 2.5K MRR.
    - Around the same timeframe, ComfyOrg was introduced, Stability collapsed, and Flux just came out.
    - it's inevitable that ComfyOrg will have some sort of cloud solution. 
    - As of today, ComfyDeploy is doing $29k MRR, and our last 30 days' revenue was $50k processed. Which is the highest we have ever got, but also the most depressing day I have ever had.
    - We have been working for months on our pay-as-you-go tier—no longer requiring you to talk to us, just pay for the cloud resources you use. And also, going back to our roots: open-sourcing the ENTIRE CLOUD PLATFORM while continuing to support existing customers.

- https://github.com/BennyKok/comfyui-deploy /1.4kStar/AGPL/202508/python/ts
  - https://www.comfydeploy.com/
  - open source `vercel` like deployment platform for Comfy UI
  - Open source comfyui deployment platform, a vercel for generative workflow infra. (serverless hosted gpu with vertical intergation with comfyui)
  - Stack: Clerk (Auth), NextJS, Drizzle (ORM), Neon / Vercel Postgres, R2 / S3 (Object Storage)
  - https://github.com/comfy-deploy/comfydeploy-fullstack-demo /202504/ts
    - https://demo2.comfydeploy.com/
    - Full stack demo build with Next js 15, Tailwind, Shadcn UI, Drizzle, Turso, Clerk
  - https://github.com/BennyKok/comfyui-deploy-next-example /202404/ts/inactive
    - https://demo.comfydeploy.com/
    - This project is designed to demonstrate the integration and utilization of the ComfyDeploy SDK within a Next.js application.
    - showcase how developers can get started creating applications running ComfyUI workflows using Comfy Deploy.

- https://github.com/ViewComfy/ViewComfy /461Star/AGPL/202508/ts
  - https://www.viewcomfy.com/
  - open source tool to help you create beautiful web apps from ComfyUI workflows.
  - Whether you need to turn comfy workflows into simple web apps that anyone can use, deploy them as serverless APIs, or just use the latest models on a powerful GPU, we’ve got you covered.
  - https://github.com/ViewComfy/cloud-public
  - [Show HN: Open-source app builder for comfy workflows | Hacker News _202409](https://news.ycombinator.com/item?id=41683407)
    - If you have Comfy already installed, it will run off that. Otherwise, currently, you need to install it manually beforehand.
  - [Show HN: Turn any ComfyUI workflow into a web app or API | Hacker News _202501](https://news.ycombinator.com/item?id=42714596)
    - we already have a few Hunyuan workflows running on our H100s. If you can run it on your computer, you can run it on our cloud for sure
    - I've been looking for something like that at my company, but we have really strict security guidelines.
      - We ran into quite a few people in this situation and usually offer to integrate our infra with their S3/storage solution. 
  - [Open source app builder for comfy workflows : r/comfyui _202409](https://www.reddit.com/r/comfyui/comments/1frq45l/open_source_app_builder_for_comfy_workflows/)
    - The idea is that you can turn a workflow into a web app with an easy-to-use UI
  - [How to turn a ComfyUI workflow into a web app in minutes _202410](https://www.viewcomfy.com/blog/turn-a-comfyui-workflow-into-an-app)
  - [Build and deploy a ComfyUI-powered app: A complete guide _202504](https://www.viewcomfy.com/blog/build-and-deploy-a-comfyui-powered-app-a-complete-guide)
    - in order to transform your ComfyUI workflow into a serverless API, you need to deploy it on ViewComfy Cloud. 

- https://github.com/licyk/term-sd /GPL/202508/sh
  - 多平台 Stable Diffusion 部署，管理脚本
  - Term-SD 是一款基于 Dialog 实现前端界面显示的 AI 管理器，支持安装，管理以下软件：sd-webui, comfyui, InvokeAI, fooocus
  - Term-SD 支持在 Linux，Windows，MacOS 上
  - https://github.com/licyk/sd-webui-all-in-one /80Star/GPLv3/202508/jupyter
    - 支持部署多种 WebUI 的 Jupyter Notebook，支持部署以下 WebUI：sd-webui, comfyui, InvokeAI,fooocus

- https://github.com/runpod-workers/worker-comfyui /AGPL/202508/python
  - This project allows you to run ComfyUI workflows as a serverless API endpoint on the RunPod platform.
  - Submit workflows via API calls and receive generated images as base64 strings or S3 URLs.
  - The worker exposes standard RunPod serverless endpoints (/run, /runsync, /health). 
    - By default, images are returned as base64 strings. 
    - You can configure the worker to upload images to an S3 bucket instead by setting specific environment variables 
  - https://github.com/Dekita/runpod-serverless-comfyui-worker /202311/inactive
    - serverless ComfyUI worker for Runpod.io
  - [Build a custom image-to-image app without writing a line of code _202411](https://medium.com/@guillaume.bieler/build-a-custom-image-to-image-app-without-writing-a-line-of-code-b625c9b0a402)

- https://github.com/replicate/cog-comfyui /MIT/202507/python
  - https://replicate.com/fofr/any-comfyui-workflow
  - Run ComfyUI with an API
  - You’ll need the API version of your ComfyUI workflow. This is different to the commonly shared JSON version, it does not included visual information about nodes
  - You can use LoRAs directly from CivitAI, HuggingFace, or any other URL in two ways
  - To get the best performance from the model you should run a dedicated instance.

- https://github.com/aws-samples/comfyui-on-eks /MIT/202506/python
  - It's a solution to deploy ComfyUI on Amazon EKS.
  - Optimized Use of GPU Instance Store: By fully utilizing the instance store of GPU instances, we maximize performance for model loading and switching while minimizing the costs associated with model storage and transfer.
  - Images generated are directly written to Amazon S3 using the S3 CSI driver, reducing storage costs.

- https://github.com/cancer32/ComfyEnv /8Star/apache2/202508/python 
  - ComfyEnv helps you manage isolated environments, so each project or node set can live in its own stable sandbox.
  - Isolated Conda environments per ComfyUI setup
  - ✅ Windows ✅ Linux ❌ macOS is currently not supported

- https://github.com/punitda/ComfyRun /202409/python/ts/inactive
  - open source and self-hosted solution to run your ComfyUI workflows at blazing fast speeds on cloud GPUs powered by Modal. 

- https://github.com/robertvoy/ComfyUI-Distributed /202508
  - ComfyUI extension that enables multi-GPU processing locally, remotely and in the cloud

- https://github.com/siliconflow/BizyAir /757Star/MIT/202507/python
  - BizyAir 是一款 ComfyUI 云节点插件，它可以与 ComfyUI 本地的其他插件一同使用、组建工作流。 
  - BizyAir 使用的是云计算资源，因此即使用户没有本地显卡，也可以做 AI 内容生成。
  - BizyAir 作为一款云计算产品，云节点按量付费，不做云节点运算时，不产生费用。
  - 用户可以将自己的模型上传到 BizyAir 中，再利用 BizyAir 到云算力做 AI 创作。

- https://github.com/QuickPoser/ComfyUI_Worker /8Star/apache2/202508/python 
  - ComfyUI_Worker 仅仅是一个连接到云端服务的客户端。要使其正常工作，您必须首先联系闪报工作人员为您开通云端租户账户。
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

- https://github.com/dovvnloading/Sapphire-Image-GenXL /MIT/202510/python
  - PrismXL Image Generator is a standalone desktop application designed to harness the power of diffusion models, specifically leveraging the `RunDiffusion/Juggernaut-XL-v9` model.
  - [I built a (opensource) UI for Stable Diffusion focused on workflow and ease of use - Meet PrismXL! : r/StableDiffusion _202510](https://www.reddit.com/r/StableDiffusion/comments/1oawx5t/i_built_a_opensource_ui_for_stable_diffusion/)
    - It's a standalone desktop GUI built from the ground up with PySide6 and Diffusers, currently running the fantastic Juggernaut-XL-v9 model.
    - My goal wasn't to reinvent the wheel, but to refine the experience. 
    - Live Render Preview: For 512x512 generations, you can enable a live preview that shows you the image as it's being refined at each step
    - Grid Generation & Zoom: Easily generate a grid of up to 4 images to compare subtle variations. The image viewer includes a zoom-on-click feature and thumbnails for easy switching.

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
# ai-image-provider
- https://github.com/Lingyuzhou111/Comfyui_Free_API /apache2/202508/python
  - 为ComfyUI提供多种免费AI API服务的插件，支持文本对话、图像生成、图像分析等功能
  - 精选Gemini、GLM、Qwen、Siliconflow四个官方平台的API接口，针对新用户均有免费使用额度，新手友好

- https://github.com/111496583yzy/comfyui-modelscope-qwen-image /202508/python
  - 这是一个ComfyUI自定义节点插件，用于调用魔搭(ModelScope)的Qwen-Image API生成图片。

- https://github.com/Stability-AI/stablediffusion /Stable Diffusion Version 2
  - https://github.com/CompVis/stable-diffusion
  - A latent text-to-image diffusion model

## image-gen-api

- https://github.com/iptag/jimeng-api /GPL/202511/ts
  - Free AI Image and Video Generation API Service - Based on reverse engineering of Jimeng AI (China site) and Dreamina (international site).
  - [【即梦jimeng/dreamina官网2api】10/20更新：双站均支持文生图和图生图 - 开发调优 / 开发调优, Lv1 - LINUX DO](https://linux.do/t/topic/995691)
  - 即梦 jimeng 和 dreamina 文生图和图生图的官网 api，借鉴了几位大佬的项目，但他们的参数都有些小问题，稍加改进下，稳定性强了不少，目前只测试了文生图和图生图功能
# models/loras/controlnet
- https://github.com/guoyww/AnimateDiff /11.7kStar/apache2/202407/python/inactive
  - https://animatediff.github.io/
  - the official implementation of AnimateDiff [ICLR2024 Spotlight]. 
  - It is a plug-and-play module turning most community text-to-image models into animation generators, without the need of additional training.
  - Note: The `main` branch is for Stable Diffusion V1.5; for Stable Diffusion XL, please refer `sdxl-beta` branch.
  - AnimateDiff is also officially supported by Diffusers. 
  - We created a Gradio demo to make AnimateDiff easier to use. 
  - https://github.com/Kosinkadink/ComfyUI-AnimateDiff-Evolved /3.3kStar/apache2/202508/python
    - Improved AnimateDiff for ComfyUI and Advanced Sampling Support

- https://github.com/scraed/LanPaint /485Star/GPL/202508/python
  - High quality training free inpaint for every stable diffusion model. Supports ComfyUI
  - This is the official implementation of "Lanpaint: Training-Free Diffusion Inpainting with Exact and Fast Conditional Inference". 
  - The repository is for ComfyUI extension. 
  - Universal Compatibility – Works instantly with almost any model (SD 1.5, XL, 3.5, Flux, HiDream, Qwen-Image or custom LoRAs) and ControlNet.
  - ComfyUI-Manager: Search for "LanPaint" in the manager and install it directly.

- https://github.com/RishiDesai/CharForge /MIT/202506/python
  - https://www.charforge.dev/
  - Generate character consistent images with a single reference
  - 48GB is preferred, but you can get by with 24GB
  - [Generate character consistent images with a single reference (Open Source & Free) : r/StableDiffusion _202506](https://www.reddit.com/r/StableDiffusion/comments/1lkezo2/generate_character_consistent_images_with_a/)
    - I built a tool for training Flux character LoRAs from a single reference image, end-to-end.

- https://github.com/cumulo-autumn/StreamDiffusion /10.4kStar/apache2/202412/python/inactive
  - StreamDiffusion is an innovative diffusion pipeline designed for real-time interactive generation.
  - Streamlined data processing through efficient batch operations.
  - Improved guidance mechanism that minimizes computational redundancy.
  - Improves GPU utilization efficiency through advanced Stochastic Similarity Filter.
  - https://github.com/jesenzhang/ComfyUI_StreamDiffusion
    - a simple implemention StreamDiffusion for ComfyUI
- https://github.com/rudyaa-sd/ScreenDiffusion /202510/python
  - https://screendiffusion.itch.io/screen-diffusion-v01
  - Real-time screen-to-image generator built around StreamDiffusion.
  - [Introducing ScreenDiffusion v01 — Real-Time img2img Tool Is Now Free And Open Source : r/StableDiffusion _202510](https://www.reddit.com/r/StableDiffusion/comments/1o99lt6/introducing_screendiffusion_v01_realtime_img2img/)

- https://github.com/joanrod/star-vector /apache2/202503/python
  - https://starvector.github.io/
  - StarVector is a foundation model for SVG generation that transforms vectorization into a code generation task. 
  - Using a vision-language modeling architecture, StarVector processes both visual and textual inputs to produce high-quality SVG code with remarkable precision.
  - It can be used to perform image2SVG and text2SVG generation. We pose image generation as a code generation task, using the power of multimodal VLMs
  - March 2025: StarVector Accepted at CVPR 2025
  - SVGBench and SVG-Stack datasets are now available on HuggingFace Datasets
    - https://huggingface.co/datasets/starvector/svg-bench
    - https://huggingface.co/datasets/starvector/svg-stack

- https://github.com/songweige/rich-text-to-image /800Star/MIT/python/inactive
  - https://rich-text-to-image.github.io/
  - Rich-Text-to-Image Generation
  - We use various formatting information from rich text, including font size, color, style, and footnote, to increase control of text-to-image generation. 
  - Our method enables explicit token reweighting, precise color rendering, local style control, and detailed region synthesis
  - This code was tested with Python 3.8, Pytorch 1.11 and supports a Stable Diffusion v1-5 or Stable Diffusion XL or ANIMAGINE-XL 
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

- https://github.com/lstein/PhotoMapAI /MIT/202508/python/js/webapp
  - https://lstein.github.io/PhotoMapAI/
  - PhotoMapAI is a fast, modern image browser and search tool for large photo collections. 
  - It uses the CLIP computer vision model to enable text and image-based search, image clustering, and interactive slideshows with a responsive web interface. 
  - PhotoMapAI is a Python-based web application that uses the CLIP image recognition AI model to identify similarities among images, as well as to enable text- and image-similarity searching. 
  - It runs completely on your local system, and does not make calls out to internet-based AI systems.
  - Its unique feature is a "semantic map" that clusters and visualizes your images by their content. Browse the semantic map to find and explore thematically-related groups of photos, or use text and/or image similarity search to find specific people, places, events, styles and themes.
  - Support for wide range of image formats, including Apple's HEIC
  - Integration with the InvokeAI AI image generation system
  - Extensible backend (FastAPI)
# more
- https://github.com/Comfy-Org/registry-backend /GPL/202502/go
  - https://registry.comfy.org/
  - The server that backs ComfyUI Registry, a public collection of custom node packs used in ComfyUI.
  - The backend API server for Comfy Registry and Comfy CI/CD.
  - https://github.com/Comfy-Org/registry-web /GPL/202508/ts
    - https://registry.comfy.org/
    - The frontend React App for Comfy Registry.

- https://github.com/phineas-pta/comfyui-auto-nodes-layout /202507/python/js
  - a ComfyUI extension that applies an improved node layout algorithm to ComfyUI workflows, primarily for better visualization
  - this serves as a working prototype of the proof-of-concept detailed in comfyanonymous/ComfyUI#1547
