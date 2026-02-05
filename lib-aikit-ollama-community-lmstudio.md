---
title: lib-aikit-ollama-community-lmstudio
tags: [community, gguf, lmstudio, mlx]
created: 2026-01-14T18:58:00.071Z
modified: 2026-01-14T18:58:32.523Z
---

# lib-aikit-ollama-community-lmstudio

# guide

# draft
- 在lmstudio支持服务端headless模式后, 将ollama wrapper替换为lmstudio wrapper
  - 💰 谨慎封装lmstudio, 因为之前lmstudio连免费工作使用都不支持

- 优化artifacts/coding的交互为类似aionui/discord-channel的收窄侧边栏效果，侧边栏并不是收窄为仅图标，而是图标+几个文字
- 采用类似vscode文件图标的方案在chat前显示图标

- 类似localsend, (通过扫描)快速让手机使用电脑的model

- mlx不仅支持text-gen, 还支持image-gen, 对multimodal模型的支持比llama.cpp更好
  - 优化基于mlx的文生图体验

- image
  - upload image by paste image url

- 是否支持split-chat

- OllamaBench ported to lmstudio
  - upload results
  - 处理thinking loop的场景

- 针对国内消费级显卡的产品
  - 摩尔线程
  - 华为昇腾

- 支持通过ui快速在提示词末尾添加`/non_think`的开关
# xp-lmstudio
- issues
  - ~~聊天内搜索~~
  - 标题名搜索，便于查看包含某关键字的chats

- mlx-engine
  - 尝试用 vllm-mlx 替换

- 
- 
- 

# xp-msty
- features
  - 支持自动扫描本地模型: ollama, huggingface
  - split-chat的布局能保持和恢复

- issues
  - huggingface缓存的模型会识别失败(Incompatible: PyTorch)

- 
- 
- 

# discuss-stars
- ## 

- ## 

- ## [why is there no LMStudio/Msty/GPT4All type app that supports backends other than llama.cpp? : r/LocalLLaMA _202501](https://www.reddit.com/r/LocalLLaMA/comments/1hy60n8/why_is_there_no_lmstudiomstygpt4all_type_app_that/)
  - ive heard that other backends, especially exllamav2 can be faster than llama.cpp in many cases especially when multiple cards or even multiple machines are running on it
- llama.cpp has the broadest support. Not only that you can offload to CPU and you can use the Vulkan back end. It's really just the most versatile one.

- broad compatibility: llama works down to Maxwell while all the better backends practically require Ampere. that's a 4 generational gap
- integration ease: llama compiles into a lib you can easily link against
- dependencies: python isn't needed. EXL2 and other better engines all require python as a dependency.

- If you're ok with Docker, I invite you to try Harbor - one unified CLI to run and configure 10 frontends and 15 inference engines.

- Transformer Lab (transformerlab.ai) is cross-platform, open-source and supports plugins for inference engines beyond Llama.cpp (and also supports fine-tuning and eval plugins). Currently has plugins for vLLM and MLX on macbooks.

- The main reason must be because with llama.cpp you can share load between CPU and GPU, or even use only CPU for inference. Not many people has enough VRAM to run their models locally. On the other hand, people that use more professional runtimes are probably comfortable with manual setup of the system.

- Private LLM (macOS and iOS only) uses mlc-llm as the inference backend, along with better quants.

- I think VLLM supports Exllama2

- ## [LM Studio is now free for use at work : r/LocalLLaMA _202507](https://www.reddit.com/r/LocalLLaMA/comments/1lux0q2/lm_studio_is_now_free_for_use_at_work/)
- LM Studio really is the nicest and most feature complete Mac UI, but with its lack of server API support I’ve fallen back to Jan.ai, which does support remote APIs but sadly lags far behind LM Studio in terms of features, configurability, and multi-modality.
  - So while it’s nice that LM Studio is permitted for work use, it may face slow adoption due to its lack of server API support.
- LM Studio's missing API end-point is my only gripe too, but you can still hack around it: fire up Ollama or text-generation-webui on a small Linux box, expose the llama.cpp server port with ssh -R, then point LM Studio’s chat window at that remote host through the custom endpoint setting (works for GPT-Q and GGUF). I keep a Jan.ai tab open for multimodal stuff and use Corellium’s K8s helm chart when I need auto-scaling GPUs. I’ve tried text-generation-webui and Jan.ai, but APIWrapper.ai just plugs the API gap when I need clean REST without rolling my own. The missing server API is still the hurdle.

# discuss-news
- ## 

- ## [0.4.0 - server native _20260128](https://lmstudio.ai/blog/0.4.0)
- Deploy LM Studio's core on cloud servers, in CI, or anywhere without GUI.
  - core of the LM Studio packaged to be server-native, without reliance on the GUI. 
- Parallel requests to the same model with continuous batching (instead of queueing).
  - concurrent inference requests to the same model
  - Parallel requests work thanks to llama.cpp's open-source continuous batching implementation, adopted in LM Studio's llm-engine. This capability has not yet made it into our MLX engine
- New stateful REST API endpoint: /v1/chat that allows using local MCPs.
- Refreshed application UI with chat export, split view, developer mode, and in-app docs.
- a brand-new CLI experience centered around the `lms chat` command
  - interactive chat session directly in your terminal, allowing you to chat with your models and download new ones.

- ## ⚖️ 0.3.39 - [Open Responses with local models via LM Studio  _20260115](https://lmstudio.ai/blog/openresponses)
- Open Responses is an open-source specification and ecosystem designed to make calling LLMs provider-agnostic.
  - It defines a shared schema and tooling layer that enables a unified experience for interacting with LLMs, streaming results, and composing agentic workflows completely independent of the model provider. 
  - This tooling layer makes real-world agentic workflows work consistently, regardless of where the model lives.

- The Open Responses API in LM Studio brings up several new useful features:
  - Logprobs for generated tokens, along with candidate tokens
  - Rich stats about cached and generated tokens
  - Provide remote image URLs to VLMs

- Log Probabilities
  - You can view the logarithms of the probability (log(probability between 0 and 1) = logprob) that a specific token was chosen by the model. 
  - The closer the logprob is to zero, the more likely the token was chosen.
  - Enabling log probabilities allows you to see more details about how confident the model was in selecting its response.

- /v1/responses update enables you to see how many tokens were cached from previous requests.

- ## ⚖️ 0.3.29 - [Use OpenAI's Responses API with local models  _202510](https://lmstudio.ai/blog/lmstudio-v0.3.29)
- This release adds support for OpenAI's /v1/responses API through the LM Studio REST server.
  - Stateful interactions - pass a previous_response_id to continue interactions without needing to manage message history yourself.
  - Custom function tool calling - bring your own function tools for the model to call, similar to in v1/chat/completions.
  - Reasoning support - parse reasoning output, and control effort with reasoning: { effort: "low" | "medium" | "high" } for openai/gpt-oss-20b.
  - Streaming or sync - use stream: true to receive SSE events as the model generates, or omit for a single JSON response.

- ## 🔍 [0.3.27: Find in Chat and Search All Chats  _202509](https://lmstudio.ai/blog/lmstudio-v0.3.27)

- ## 💰 [LM Studio is free for use at work  _202507](https://lmstudio.ai/blog/free-for-work)

- ## ⚖️ [MCP in LM Studio  _202506](https://lmstudio.ai/blog/lmstudio-v0.3.17)
  - introduces Model Context Protocol (MCP) support, allowing you to connect your favorite MCP servers to the app and use them with local models.
  - supports both local and remote MCP servers. You can add MCPs by editing the app's mcp.json file or via the new "Add to LM Studio" Button, when available.

- ## 🖼️ 0.17.0 [Introducing the unified multi-modal MLX engine architecture in LM Studio  _202505](https://lmstudio.ai/blog/unified-mlx-engine)
  - we migrated to a new unified architecture that weaves together the foundational components of each of those packages. 
  - Now mlx-lm's text model implementations are always used, and mlx-vlm's vision model implementations are modularly used as "add-ons" to generate image embeddings that can be understood by the text model.
  - text-only chats with VLMs can now benefit from prompt caching — a feature previously exclusive to text-only LLMs — resulting in drastically faster follow-up responses. 

- ## [0.3.15: RTX 50-series GPUs and improved tool use in the API  _202504](https://lmstudio.ai/blog/lmstudio-v0.3.15)
  - support for NVIDIA RTX 50-series GPUs (CUDA 12), UI touchups including a new system prompt editor UI. 

- ## [0.3.10: Speculative Decoding  _202502](https://lmstudio.ai/blog/lmstudio-v0.3.10)
  - introduce Speculative Decoding support in LM Studio's llama.cpp and MLX engines

- ## [0.3.6 Function Calling / Tool Use API  _202501](https://lmstudio.ai/blog/lmstudio-v0.3.6)
  - introduces a Function Calling / Tool Use API through LM Studio's OpenAI compatibility API.
  - support for new vision-input models: The Qwen2VL in llama.cpp and mlx

- ## [Introducing venvstacks: layered Python virtual environments  _202410](https://lmstudio.ai/blog/venvstacks)
  - In our recent announcement of Apple MLX support in LM Studio 0.3.4, we alluded to a Python utility for creating an "... integrated set of independently downloadable Python application environments".
  - Today we're excited to open source this utility: introducing venvstacks
  - venvstacks enabled us to ship our MLX engine, which is a Python application, within LM Studio without requiring the end user to install any Python depedencies.

- ## 🍎 [0.3.4 ships with Apple MLX  _202410](https://lmstudio.ai/blog/lmstudio-v0.3.4)
  - 0.3.4 ships with an MLX engine for running on-device LLMs super efficiently on Apple Silicon Macs.
- mlx-features
  - Search & download any supported MLX LLM from Hugging Face (just like you've been doing with GGUF models)
  - Use Vision models like LLaVA and more, and use them via the chat or the API (thanks to `mlx-vlm` )
  - Enforce LLM responses in specific JSON formats (thanks to `Outlines` )
  - Load and run multiple simultaneous LLMs. You can even mix and match llama.cpp and MLX models
- LM Studio's `mlx-engine` is open source
- MLX Engine is a Python module built using a combination of the following packages:
  - mlx-lm
  - mlx-vlm 
  - Outlines
- Our journey to integrate MLX into LM Studio started with Swift. While this approach worked perfectly fine, ultimately the following design goals made Python a better choice.
  - Design Goal 1: We want to iterate on the MLX engine with the community
  - Design Goal 2: We want to be able to support the latest models and techniques as soon as they are released. MLX in Python tends to receive support for new models sooner
- Adding mlx-lm support to LM Studio required the ability to deploy and run Python components in a portable, cross-platform fashion.
  - Ideally, we also want to be able to fully integrate those components with the existing C/C++ components already used in the main LM Studio application (which ended up ruling out some potential candidate solutions, such as conda environments).
- LM Studio's initial Python runtime support is built atop the python-build-standalone project, and Python virtual environments, using a soon-to-published utility that supports the creation of an integrated set of independently downloadable Python application environments that share common runtime and framework layers (after all, nobody wants to download and install multiple copies of PyTorch or CUDA if they can reasonably avoid it).
  - This "stacked virtual environments" utility uses the CPython interpreter's "site customization" feature, together with some pre-publication and post-installation adjustments to the virtual environment contents, to allow these virtual environments to be reliably transferred between machines and the included application launch modules invoked with CPython's -m command line switch.

- KV (key-value) caching across prompts is an optimization technique that enables LLM engines to reuse computations from previous interactions. This can greatly improve model response time, or "Time to First Token".
  - if we save the results of the computations in T1 and T2 to a KV CACHE, and give the engine access to the KV CACHE at T3, then the engine only has to perform computations on the new part of the prompt
  - This can greatly improve response time in T4.

- ## [0.3.5 - headless mode  _202410](https://lmstudio.ai/blog/lmstudio-v0.3.5)
  - introduces headless mode, on-demand model loading, and updates to mlx-engine to support Pixtral (MistralAI's vision-enabled LLM).
  - We've implemented headless mode, on-demand model loading, server auto-start, and a new CLI command to download models from the terminal. 
- Headless mode, or "Local LLM Service", enables you to leverage LM Studio's technology (completions, chat completions, embedding, structured outputs via llama.cpp or Apple MLX) as local server powering your app.
  - Once you turn on "Enable Local LLM Service", LM Studio's process will run without the GUI upon machine start up.
- On-demand model loading
  - simply send an inferencing request to it. If the model is not yet loaded, it'll be loaded before your request returns. This means that the first request might take a few seconds until the loading operation finishes, but subsequent calls should be zippy as usual.
  - Using per-model settings, you can predetermine which load parameters the software will use by default when loading a given model.
  - With JIT loading: returns all local models that can be loaded

- ## [0.3.0 - RAG  _202408](https://lmstudio.ai/blog/lmstudio-v0.3.0)
- LM Studio 0.3.0 comes with built-in functionality to provide a set of document to an LLM and ask questions about them.
  - If the document is short enough (i.e., if it fits in the model's "context"), LM Studio will add the file contents to the conversation in full.
  - If the document is very long, LM Studio will opt into using "Retrieval Augmented Generation", frequently referred to as "RAG". 
- OpenAI recently announced a JSON-schema based API that can result in reliable JSON outputs. LM Studio 0.3.0 supports this with any local model that can run in LM Studio
- Serve on the network

- ## 0.2.22 - [Introducing lms: LM Studio's CLI  _202405](https://lmstudio.ai/blog/lms)
  - With lms you can load/unload models, start/stop the API server, and inspect raw LLM input (not just output).

# discuss-roadmap
- ## 

- ## 

- ## 

- ## 

- ## [0.4.0 Deepseek OCR2 not working · Issue · lmstudio-ai/lmstudio-bug-tracker _202601](https://github.com/lmstudio-ai/lmstudio-bug-tracker/issues/1437)
  - LM Studio reports that the model is not supported. My runtime is up to date and uses the latest release of mlx-vlm, which lists DeepSeek OCR2 support in its changelog.

- ## [Phi 3.5 Vision Instruct Fails to Load "Trust remote code" error · Issue · lmstudio-ai/mlx-engine _202411](https://github.com/lmstudio-ai/mlx-engine/issues/29)
- 👷: If you're seeing a `Trust remote code` issue, it means that the model is not (yet) supported by `mlx-engine` . Specifically, support for that model's tokenizer and/or config has not been merged into huggingface transformers.
  - We choose to block loading a model instead of enabling remote code because we are wary of letting users download and run potentially malicious code.

- [when load mlx-community/Kimi-VL-A3B-Thinking-4bit, it prompts trust_remote_code=True. · Issue · lmstudio-ai/lmstudio-bug-tracker](https://github.com/lmstudio-ai/lmstudio-bug-tracker/issues/607)

- ## 🖼️ [Qwen3-VL kinda sucks in LM Studio : r/LocalLLaMA _202510](https://www.reddit.com/r/LocalLLaMA/comments/1ock0lc/qwen3vl_kinda_sucks_in_lm_studio/)
- LM Studio apparently downscales to 500x500 ish. llama.cpp is better for multimodal for now until LM Studio fixes this.
- LM Studio downscales images to just 1024x and gives you no way to increase it.
- LM Studio used to downscale the image to just 512x512 and it was giving terrible results at times. Now they have increased it to 1024x1024. But I still find it not as good as just running it directly on MLX.
- I believe lmstudio (currently) downscales/resizes images, while qwen3-vl can accept (and performs better with) arbitrary image sizes. There was a post a few days ago about how they were going to make it optional, but I don't know if they've done that yet.

- ## [LM Studio Fails to Load 32B 4bit Models on macOS M4 (Freezes System) While Ollama Works Normally · Issue · lmstudio-ai/lmstudio-bug-tracker _202503](https://github.com/lmstudio-ai/lmstudio-bug-tracker/issues/484)
- It seems like LM Studio isn't correctly utilizing swap memory, as there's a small spike in usage when the model is initially loaded, but afterwards it doesn’t exceed 24GB of memory.

- Only fix for this inside LM Studio that I found is to set Model loading guardrails to Custom and a memory limit to 23GB, because if it goes over 23GB it crashes macOS as LM Studio doesn't use swap memory if it uses over the total available 24GB of memory of the Mac Mini M4 Pro. With this guard setup if the model is too big and exceeds over 23GB of memory, it unloads the model and not crash macOS. For models 30B+, it's better to use Q3 or MLX 3bit because Q4/4bit is too big for 24GB of RAM. I wish I had known about this before buying the 24GB version

- ## [Incompatible type of `tool_choice` · Issue · lmstudio-ai/lmstudio-bug-tracker _202505](https://github.com/lmstudio-ai/lmstudio-bug-tracker/issues/670)
- 
- 

- [[Bug]: Invalid value for 'tool_choice' · Issue #7039 · All-Hands-AI/OpenHands](https://github.com/All-Hands-AI/OpenHands/issues/7039)
  - When I switch to use OpenAI (gpt-4o), it working fine.

- ## [Qwen3 Models not Recognized as Embedding Types for MLX Format · Issue · lmstudio-ai/lmstudio-bug-tracker _202507](https://github.com/lmstudio-ai/lmstudio-bug-tracker/issues/808)
  - Qwen3 models not recognized as embedding models in MLX format (but same models are ok in GGUF)

- From what i can understand, while the chat models are using mlx as an inference engine, LMStudio would need to use a package like `mlx-embeddings` to properly handle MLX Embeddings, and integrate it in there LM Studio MLX Runtime.
  - This would explain why the `Override Domain Type` option is not available for MLX: Only the 'LLMs' models are supported for mlx.
- there is no support for mlx embeddings in LMStudio
- The only workaround for now using LMStudio is to use the GGUF versions and take the performance hit

- [[Models] Qwen3 Embedding shown as LLM instead of an embedding model · Issue · lmstudio-ai/lmstudio-bug-tracker](https://github.com/lmstudio-ai/lmstudio-bug-tracker/issues/696)
# discuss-issues
- ## 

- ## 

- ## 

- ## 
# discuss-internals
- ## 

- ## 

- ## 

- ## 
# discuss
- ## 

- ## 

- ## 

- ## 

- ## 

- ## 🔀 is it possible in MLX-LM to have inference from multiple LLMs at the same time? 
- https://x.com/OrganicGPT/status/1982460752507085256
  - I'd like to serve multiple AI agents on MStudio simultaneously but last I checked with llama.cpp the GPU could handle only one request at a time even with multiple threads/processes
  - Mac Studio M3 Ultra's massive 512GB memory is perfect for parallel agent calling! Here I used @lmstudio to run *40* instances of @openai 's gpt-oss-20b-mlx and got 35% performance boost compared to sequential API calling. @awnihannun , next I'll do it with batching like you said!

- Running 40 instances in parallel sounds very promising for performance.

- 2 LM Studio on 2 different ports and you get it.

- Yea, you can do this with different processes. But it's much better to batch requests with the same model using a single process.
  - Each request uses up most of the memory bandwidth so having two models run simultaneously on two processes won't be much faster than running them sequentially. 
  - When you batch properly with the same model (as in `mlx_lm.batch_generate`) you don't double the memory i/o because the model weights are the same.
  - Note, this is not specific to MLX or Apple silicon. This is a general property of LLM inference on GPUs. If you have a low latency implementation it should be using most of the memory bandwidth even at batch size 1 so multi-process with multiple models *running at the same time* on the same GPU is not optimal.

- If you’re using Linux OS in production you can use vLLM which maximizes hardware utilization to handle many concurrent requests with low latency using an OpenAI-compatible API.
  - vLLM performs automatic continuous (dynamic) batching of incoming requests via its scheduler to maximize throughput.

- Yesterday I have written python script for M3 Ultra which tries to do that with batch_generate function, depends on the batch size, you can process requests in batch, other requests have to wait until batch is finished, and then another batch is processed… and so on

- If you need a load balancer, you can try https://github.com/autolocalize/lm-studio-loadbalancer

- ## [LM Studio not reading document correctly. But why? : r/LocalLLaMA](https://www.reddit.com/r/LocalLLaMA/comments/1o98vqd/lm_studio_not_reading_document_correctly_but_why/)
- So rag-v1 plugin LM Studio is using has a simple rule: if file fits into 70% of remaining context, it will be fully injected - and this is what you want. Otherwise it resorts to RAG retrieval.

- ## [In LM Studio + MoE Model, if you enable this setting with low VRAM, you can achieve a massive context length at 20 tok/sec. : r/LocalLLaMA _202510](https://www.reddit.com/r/LocalLLaMA/comments/1o6dnzc/in_lm_studio_moe_model_if_you_enable_this_setting/)
  - enable: Force Model Expert Weights onto CPU, Flash Attention
  - Worked for my 3060
- Since you offload on cpu ram the speed decrease significantly.

- If you use llamacpp directly, you can further fine tune the number of expert layers pushed to CPU rather than pushing them all out. With careful adjustment and if there is enough headroom on your GPU, you might double your t/s vs the option used by lm studio.

- You can set KVcache to Q8 and double the context size. Q8 has a very small loss in quality but might be worth it to you. 

- ## [Is there any all-in-one app like LM Studio, but with the option of hosting a Web UI server? : r/LocalLLaMA _202506](https://www.reddit.com/r/LocalLLaMA/comments/1larzxz/is_there_any_allinone_app_like_lm_studio_but_with/)
- llama.cpp's llama-server hosts a very basic webUI by default. It's hosted at the server root, without the API endpoint.

- LM Studio + OpenWebUI work quite well together and you can share it via a VPN like Tailscale if you want to access it from anywhere. 

- Anything can be anything with docker. Make a docker compose once that launches all the things

- ## [Best Opensource LM Studio alternative : r/LocalLLaMA _202508](https://www.reddit.com/r/LocalLLaMA/comments/1mrxuwd/best_opensource_lm_studio_alternative/)
- llama.cpp: `llama-server -m model.gguf` http://localhost:8080
- Add Llama-Swap to make it hot swap models. Open WebUI is a sleek interface.
- what is llama swap
  - It’s a small proxy server (portable, no installation needed) that runs your Llama Cpp instance but offers its OpenAI compatible API to any client you have. Once you connect to this proxy and request any model by name, it will load it up and serve.
- This is the only correct answer. Start here. You will not be dependent on some company that wants to make money at some point.

- The problem with the llama.cpp / llama swap configuration is that the easy install is Vulcan only and if you buy newer hardware, aka, 50 series stuff, you have to build it from source. Most of the people using lm studio or ollama are not set up for that.

- Really wanted to use jan.ai since its fully open source but its lacking many features of lmstudio 
  - Jan doesn't have RAG to chat with document files 
  - qwen 3 30b a4b runs at 3 t/s instead of 17 on lm studio. using 2080 super
  - No projects folder option like in lm studio/ chatgpt 

- Jan AI if you want an all-in-one desktop app that runs both the AI and the GUI. Open source and looks very nice. Best LM Studio alternative IMO.

- KoboldCPP feels more like LM Studio because it's available as a single binary.
  - If only it wasn't ugly as all hell. Really needs.. some.. no.. A LOT.. of UI work.
- Agreed. They should invest some in creating a new UI. Lots of good backend stuff... There is a lot I love about Oobabooga that I wish they would adopt.

- I like gpustack, they run llamabox which is based on llama.cpp

- GPT4ALL was nice but it's a dead project now.

- ## [Why do people say LM Studio isn't open-sourced? : r/LocalLLaMA _202405](https://www.reddit.com/r/LocalLLaMA/comments/1cvawmz/why_do_people_say_lm_studio_isnt_opensourced/)
- LMstudio is free in cost but it's proprietary software.

- Surely not all freeware are open source.
- The power of LM Studio is 4 things:
  - model discovery is incredibly easy, directly to huggingface gguf repositories
  - it's a direct inferencing app, can load models itself
  - able to work as a standalone endpoint server
  - it can loads multiple model on available GPUs

- i'm currently building https://kolosal.ai it's a free and opensource platform to run LLM on device, 
  - and the best part? it's only 20mb and can run on both CPU and GPUs, 
  - and it's also using `llama.cpp` as backend so the performance wouldn't be any different with lmstudio
- Is this windows only? 
  - Unfortunately currently yes. But, we're using framework that mostly is crossplatform

- because it's not open source, you cannot view their code or fork it to change it. the open source direct alternative to lmstudio is jan ai

- ## 🍎 [Is there an alternative to LM Studio with first class support for MLX models? : r/LocalLLaMA _202506](https://www.reddit.com/r/LocalLLaMA/comments/1l0ct34/is_there_an_alternative_to_lm_studio_with_first/)
  - I've been using LM Studio for the last few months on my Macs due to it's first class support for MLX models (they implemented a very nice MLX engine which supports adjusting context length etc.
- While it works great, there are a few issues with it:
  - it doesn't work behind a company proxy, which means it's a pain in the ass to update the MLX engine etc when there is a new release, on my work computers
  - it's closed source, which I'm not a huge fan of
  - I can run the MLX models using `mlx_lm.server` and using open-webui or Jan as the front end; but running the models this way doesn't allow for adjustment of context window size (as far as I know)

- Now I use MLX more because of it's GPU usage is not blocking macOS visual fluidity. My Mac screen rendering (especially when doing multitasking with Stage Manager) a lot stutter when inferencing with llama.cpp, but still fluid with MLX. Yes, there are not as mature as llama.cpp, but this factor made me swith to MLX only. I run it using LM Studio as an endpoint.

- ## 🤔 [LM Studio incredibly slow (1.2 tokens/sec) on a 3090, despite model (Qwen 2.5 32B 4xs) fitting entirely into VRAM and not yet hitting the context length. : r/LocalLLaMA _202411](https://www.reddit.com/r/LocalLLaMA/comments/1gqa5xx/lm_studio_incredibly_slow_12_tokenssec_on_a_3090/)
- increasing context size also increases Vram overhead. From what I remember it's roughly something to the tune of each 4k = 1gb vram.
  - Yeah. It's just that LM Studio shows VRAM usage and it's not yet hitting the limit. Unless it doesn't show if it goes over for some reason?
  - Halving the context to 16k allows me to fit everything.

- If you never figured it out its probably the Guardrails just go to hardware and turn them off, also bigger the context the more vram it needs, turn mmap and dont keep in ram off and turn flash attention adn K cache on.

- ## 🧩 [Does the number of bits in KV cache quantization affect quality/accuracy? : r/LocalLLaMA _202502](https://www.reddit.com/r/LocalLLaMA/comments/1iuw1kx/does_the_number_of_bits_in_kv_cache_quantization/)
- Setting the KV cache to Q8 has only a minimal influence on the results. 
  - Setting the KV cache to Q4 has quite an impact though. 
  - Setting K to F16 or Q8 and V to Q4 still achieves decent results though.
  - Just the extensive test that the author of the KV quantization in llama.cpp did that I linked above. The results make sense, as the keys are used to find the right value, and mismatching keys due to higher quantization will lead to incorrect values, whereas correctly looked up values that have been quantized will still be somewhat related to the original information.

- ## [LMStudio, KV cache and context length : r/LocalLLaMA _202502](https://www.reddit.com/r/LocalLLaMA/comments/1iyv8t6/lmstudio_kv_cache_and_context_length/)
  - I've turned on KV cache quantization because it "may lead to faster generation"
  - LMStudio's UI also mentions that when this feature is on, the context length value doesn't matter. So, I'm wondering how big the actual context is with this setting enabled?

- Multiplicative. Normal is fp16. Q4 quadruples your context length with minimal loss (except qwen)

- under the KV Cache Quantization option that "Context Length setting is ignored when using KV Cache Quantization" and unsurprisingly completely ignores whatever you have in the field.
  - Based on pasting a 10k-ish token article into a conversation, and LM Studio filling the context to 257.8%, it seems like it's set to 4096 by default... which really seems like a huge waste of being able to quantize the cache, but again there is no additional field or slider to adjust context size when quantization is enabled.
