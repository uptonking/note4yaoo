---
title: lib-aigc-image-comfyui-examples-diffusers
tags: [comfyui, diffusers, examples, image]
created: 2025-08-23T11:43:02.194Z
modified: 2025-08-23T11:43:35.904Z
---

# lib-aigc-image-comfyui-examples-diffusers

# guide

# popular
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

- https://github.com/AUTOMATIC1111/stable-diffusion-webui /156kStar/AGPL/202407/python/inactive
  - A web interface for Stable Diffusion, implemented using Gradio library.
  - Original txt2img and img2img modes
  - One click install and run script 
  - 4GB video card support (also reports of 2GB working)
- https://github.com/gradio-app/gradio /39.6kStar/apache2/202508/python/ts/svelte
  - http://www.gradio.app/
  - Gradio is an open-source Python package that allows you to quickly build a demo or web application for your machine learning model, API, or any arbitrary Python function.
  - You can then share a link to your demo or web application in just a few seconds using Gradio's built-in sharing features.

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
# ai-image-generator
- https://github.com/AIDC-AI/ComfyUI-Copilot /2.5kStar/MIT/202508/python/ts
  - ComfyUI-Copilot is an AIGC intelligent assistant built on ComfyUI that provides comprehensive support for tedious workflow building, ComfyUI-related questions, parameter optimization and iteration processes
  - 🎯v2-20250814: v2.0 evolves from a "helper tool" into a "development partner"—not just assisting with workflow development, but capable of autonomously completing development tasks.
  - We now cover the entire workflow lifecycle, including generation, debugging, rewriting, and parameter tuning, aiming to deliver a significantly enhanced creative experience.
  - One-Click Debug:：Automatically detects errors in your workflow, precisely identifies issues, and provides repair suggestions.
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

- https://github.com/kijai/ComfyUI-moondream /202403/python/inactive
  - ComfyUI node to use the moondream tiny vision language model

- https://github.com/gokayfem/ComfyUI_VLM_nodes /apache2/202502/python/inactive
  - Custom ComfyUI nodes for Vision Language Models, Large Language Models, Image to Music, Text to Music, Consistent and Random Creative Prompt Generation
  - Utilizes `llama-cpp-python` for integration of LLaVa models. You can load and use any VLM with LLaVa models in GGUF format with this nodes.
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
# workflows
- https://github.com/dicksondickson/dickson-sci-fi-enhance-upscale /202505
  - These are ComfyUI workflows to upscale images to 2K, 4K, or 8K.
  - These workflows upscales images in multiple stages using a combination of upscaling models, CCSR, SUPIR and Ulitmate SD Upscale, upscaling models, SDXL and Flux.
  - Each workflow is tuned to a specific resolution with different speed variants. These workflows are continuing evolving.
# ai-image-provider
- https://github.com/Stability-AI/stablediffusion
  - https://github.com/CompVis/stable-diffusion
  - A latent text-to-image diffusion model

- https://github.com/camenduru/stable-diffusion-webui-portable
  - This Project Aims for 100% Offline Stable Diffusion (People without internet or with slow internet can get it via USB or HD-DVD)

- https://github.com/lllyasviel/stable-diffusion-webui-forge /11.4kStar/AGPL/202506/python
  - a platform on top of Stable Diffusion WebUI (based on Gradio)
  - Forge is currently based on SD-WebUI 1.10.1 at this commit. (Because original SD-WebUI is almost static now, Forge will sync with original WebUI every 90 days, or when important fixes.)
  - https://github.com/Panchovix/stable-diffusion-webui-reForge

- https://github.com/cmdr2/stable-diffusion-ui
  - The easiest way to install and use Stable Diffusion on your computer.

- https://github.com/mcmonkeyprojects/SwarmUI /3kStar/MIT/202508/csharp/js
  - SwarmUI (formerly StableSwarmUI), A Modular Stable Diffusion Web-User-Interface, with an emphasis on making powertools easily accessible, high performance, and extensibility
  - [Best way to use Qwen Image on Linux? : r/LocalLLaMA _202508](https://www.reddit.com/r/LocalLLaMA/comments/1mmx3cg/best_way_to_use_qwen_image_on_linux/)
    - It's a fairly standard UI that sits on top of it's own comfy instance. It supports nearly everything that comfyui does, and makes the full comfyUI available as a built-in tab for when you need custom workflows not doable with the main UIs parameters.

- https://github.com/joanrod/star-vector /apache2/202503/python
  - https://starvector.github.io/
  - StarVector is a foundation model for SVG generation that transforms vectorization into a code generation task. 
  - Using a vision-language modeling architecture, StarVector processes both visual and textual inputs to produce high-quality SVG code with remarkable precision.
  - It can be used to perform image2SVG and text2SVG generation. We pose image generation as a code generation task, using the power of multimodal VLMs
  - March 2025: StarVector Accepted at CVPR 2025
  - SVGBench and SVG-Stack datasets are now available on HuggingFace Datasets
    - https://huggingface.co/datasets/starvector/svg-bench
    - https://huggingface.co/datasets/starvector/svg-stack
# sd-web-ui

# diffusers

# more
