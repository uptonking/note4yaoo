---
title: lib-aikit-ollama-community
tags: [community, large-language-model, llama.cpp, lmstudio, mlx, ollama]
created: 2026-01-14T18:57:15.674Z
modified: 2026-01-14T18:57:51.174Z
---

# lib-aikit-ollama-community

# guide

# discuss-stars
- ## 

- ## 

- ## 

- ## 
# discuss-news
- ## 

- ## 

- ## [Using Claude Code with Ollama local models : r/LocalLLaMA _202601](https://www.reddit.com/r/LocalLLaMA/comments/1qfwubh/using_claude_code_with_ollama_local_models/)
  - Ollama v0.14.0 and later are now compatible with the Anthropic Messages API, making it possible to use tools like Claude Code with open-source models.
- Be aware of the long system prompts and set the context size accordingly. You can check out the system prompts below.
  - Claude Code: 16.5K tokens
  - Codex: 6.5K tokens
  - Gemini-cli: 5.5K tokens
  - Smaller models<100B (especially without being fine-tuned on a specific system prompt) might not be able to follow lengthy instructions.

- I know that Claude Code performs better on SOTA or near-SOTA models, but the system prompt can be ~2x the size which for some local models changes things significantly (~10k tokens for Qwen-Code-CLI, ~21k tokens for Claude Code)

- I did this a while back using LM Studio. I got it running with gpt-oss:20b on a 16GB 4080. It’s not fast but it works great in vanilla mode with 100K context.
  - What did NOT work was trying to add skills or workflow plugins like OpenSpec.

- ## 💡 [Ollama's new app | Hacker News _202507](https://news.ycombinator.com/item?id=44739632)
- this is not electron app. It does use system webview thought.

- I am somewhat surprised that this app doesn't seem to offer any way to connect to a remote Ollama instance. The most powerful computer I own isn't necessarily the one I'm running the GUI on.

- Ollama’s tactics:
  - Vendor lock-in: AFAIK it now uses a proprietary llama.cpp fork and builts its own registry on ollama.com in a kind of docker way (I heard docker ppl are actually behind ollama) and it's a bit difficult to reuse model binaries with other inference engines due to their use of hashed filenames on disk etc.
  - Same models often run slower or give worse outputs than plain llama.cpp. Tradeoff for convenience - I know.
  - Opaque model naming: Rebrands or filters community models without transparency, biggest fail was calling the smaller Deepseek-R1 distills just "Deepseek-R1" adding to a massive confusion on social media and from "AI Content Creators", that you can run "THE" DeepSeek-R1 on any potato.
  - Difficult to change Context Window default: Using Ollama as a backend, it is difficult to change default context window size on the fly, leading to hallucinations and endless circles on output, especially for Agents / Thinking models.

- There's also Jan AI, which supports Linux, MCP, any Vulkan GPU, any Llama.cpp-compatible model, and optionally multiple cloud models as well. That seems like a better solution than this.
  - 👷: Choice is good but here is why prefer Ollama over others (I'm biased because I work on Ollama).
  - Supporting multiple backends is HARD. Originally, we thought we'd just add multiple backends to Ollama - MLX, ROCm, TRT-LLM, etc. It sounds really good on paper. In practice, you get into the lowest common denominator effect. What happens when you want to release Model A together with the model creator, and backend B doesn't support it? Do you ship partial support? If you do, then you start breaking your own product experience.
  - Supporting Vulkan for backwards compatibility on some hardware seems simple right? What if I told you in our testing, there is a portion of the supported hardware matrix getting -20% decrease in performance. What about just cherry picking which hardware to use Vulkan vs ROCm vs CUDA, etc? Do you start managing a long and tedious support matrix, where each time a driver is updated, the support may shift?
  - Supporting flash attention sounds simple too right? What if I told you over 20% of the hardware and for specific models, enabling it will cause non-trivial amount errors pertaining to specific hardware/model combinations? We are almost in a spot, where we can selectively enable flash attention per type of model architecture and hardware architecture.
  - It's so easy to add features, and hard to say no, but given any day, I will stand for a better overall product experience (at least to me since it's very subjective). No is temporary and yes is forever.

- GPUStack doesn't seem to have the problem of lowest common denominator but supports many architectures.

- 
- 
- 

- 
- 
- 
- 
- 
- 

# discuss-roadmap
- ## 

- ## 

- ## 

- ## 

- ## [Ollama GUI not working on Windows 10 Pro (22H2) _202508](https://github.com/ollama/ollama/issues/11808)
  - The Ollama GUI does not launch or work properly on my Windows 10 system. When I try to open it, nothing happens (or it closes immediately without showing the interface).

- The issue is that `msedgewebview2` is not installed by default on the system. For the Ollama user interface to work, it must be installed. A window may appear prompting you to install msedgewebview2; however, if you ignore the installation, the UI will not work and no error message will be shown.

- ## [use the macOS electron app for Windows and Linux _202410](https://github.com/ollama/ollama/issues/7135)
  - I don't understand why the electron app is only for macOS when electron is perfectly capable of running on Windows and Linux.

- ## [FR: Meaningful names of models in models/blobs dir _202501](https://github.com/ollama/ollama/issues/8466)
  - Please make models to have meaningful filenames (like user/modelname-quantization.gguf) in models/blobs directory, so they can be (easier) used with other model inference software.

- The blobs are content addressable which means that if you have two or more models which share the same content they will share the same blob which saves space on your disk and also means you don't have to pull down that data if you already have it. The format is also changing with the new engine though so it probably won't be useful with other tools unless they support the new format.

- You use less disk space because the many of the quantizations of the tensors share the same tensors.

- ## [MLX backend · Issue · ollama/ollama _202312](https://github.com/ollama/ollama/issues/1730)
- Add mlx-vlm backend also.

- Lack of MLX support is the only reason I don't use Ollama. In some cases MLX Q8 is 20% faster than GGUF, and memory usage is better handled.

- 📡 [Draft MLX go backend for new engine by dhiltgen · Pull Request · ollama/ollama _202502](https://github.com/ollama/ollama/pull/9118)
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
# discuss-gpustack
- ## 

- ## 

- ## 

- ## 

- ## [Best setup for running a production-grade LLM server on Mac Studio (M3 Ultra, 512GB RAM)? : r/LocalLLM _202511](https://www.reddit.com/r/LocalLLM/comments/1p7ei31/best_setup_for_running_a_productiongrade_llm/)
- One option that doesn't support MLX but supports GGUF is GPUStack which uses `llama-box` on Apple Silicon. GPUStack has an Open AI compatible API and can expand to multiple nodes easily. One benefit of the platform is that you can run multiple replicas of the model under the same API endpoint. I have a cluster of 2 Mac Studio Ultras with 512 GB each. It is running around the clock and supports a user base of about 200 users. I use Open Web UI, so I'm able to connect to multiple AI providers on the backend. In addition to GPUStack, I use Ollama for embedding. I started exploring Msty for MLX models.
  - Here are the details of my setup: GPUStack is installed on the two Mac Studio Ultra machines. I consider the first one as the master. The two machines are connected with a direct thunderbolt 5 cable with private IPs. (172.16.0.1, 2). The master has a token usually stored in /var/lib/gpustack/token. I join the master from the second node by running sudo gpustack start --server-url http://172.16.0.1 --worker-ip 172.16.0.2 --token your-token. You can see the cluster details on the master by simply going to http://localhost:80 or in that case http://172.16.0.1. There is a dashboard that shows the system load, the VRAM, GPU, RAM, and CPU utilization, the top users, and the usage in terms of tokens and API calls. It also shows the active models. then you have pages for adding models, deploying the models, monitoring workers and GPUs, and a model catalog. You can also chat from that interface, but I connect Open Web UI through the API interface. One thing to note about GPUStack is that the base URL for API access is http://IP-Address:80/v1-openai. Let me know if you need more details

- ## [GPUStack drops support for MacOS : r/LocalLLaMA _202511](https://www.reddit.com/r/LocalLLaMA/comments/1pe6rhs/gpustack_drops_support_for_macos/)
- llama.cpp can do ditributed inference, if that's what you are using your cluster for

- Yeah, I saw that big update that's like a full overhaul of the project. They even dropped Windows support, totally out of their mind.
  - Going down the path of containers is wild IMO. Just seems like they're hunting some very specific enterprise contract.
  - You can probably just use the prior version and update the llama-box in it and still be more or less fine for a while.
# discuss
- ## 

- ## 

- ## 

- ## 

- ## 

- ## [Do we want the benefits of Ollama API without actually using Ollama? : r/LocalLLaMA _202602](https://www.reddit.com/r/LocalLLaMA/comments/1r8gb3p/do_we_want_the_benefits_of_ollama_api_without/)
  - Apps with native Ollama API integration often have smoother setup and model management than what we get with the OpenAI API alone. For example, in Open WebUI (see image), the server is auto-detected on port 11434 and you can pull, eject, and check the status of models right from the web ui.
  - As an experiment this week I added Ollama API support to Lemonade Server. We already had the functions, so I just had to hook them up to /api endpoints.

- Is Lemonade a for profit company?
  - No Lemonade is 100% open source. It’s sponsored by AMD, which only makes money if you buy a computer. The idea is that if local AI gets increasingly awesome then more people will buy computers, so there’s no need for lemonade itself to have revenue/profits.

- llama.cpp has had server routing for models for months now. You can literally mount and unmount models on the fly.
  - lemonade literally copied and pasted the relevant snippets into their code base.
  - They did do some other stuff in there, Ill give them that at the very least. But the only thing special about it is that its optimized for AMD hardware. Thats really it.
  - My problem with the routing is that it leaves fucking models hanging in the background and OOM crashes the new model it's going to load. It's a known bug and it's aggravating as fuck. Anyone know a solution to that?
    - In llama.cpp, set the option "--models-max 1"

- the ollama API becoming a de facto standard is interesting because it happened organically. apps integrated it because ollama made local setup dead simple, and now the API itself has more adoption than some official specs.

- Llama-server now provides a mechanism to automatically swap between models. Haven't looked into it but thats an option

- ## 🖼️ pretty excited to see image generation support in @ollama powered by MLX
- https://x.com/awnihannun/status/2010394007952891973

- ## [How does Ollama truncate the context when it's too long? : r/ollama _202512](https://www.reddit.com/r/ollama/comments/1pe18c7/how_does_ollama_truncate_the_context_when_its_too/)
  - I'm trying to understand how prompts are truncated then they exceed the context limit. Let's say I have the num_ctx parameter set to 1000 tokens. I then send in a system prompt, and a whole bunch of user and assistant messages, but in total there are 2000 tokens in the context. What happens?

- if your system prompt is 100 tokens, and your message history is 1000 tokens, and your context limit is 1000, Ollama will process the full system prompt and the most recent 900 message history tokens.
  - You're supposed to manage your context yourself/using whatever app you may use Ollama with, to ensure it is within the limit.

- ## [feat: add trace log level by mxyng · Pull Request · ollama/ollama _202505](https://github.com/ollama/ollama/pull/10650)
  - OLLAMA_DEBUG= or OLLAMA_DEBUG=0 or OLLAMA_DEBUG=false: unset or empty or falsy values sets default INFO level
  - OLLAMA_DEBUG=1 or OLLAMA_DEBUG=true: set DEBUG level
  - OLLAMA_DEBUG=2: set TRACE level

- [OLLAMA_DEBUG=1 Not Showing Prompts in Logs ](https://github.com/ollama/ollama/issues/10950)
  - OLLAMA_DEBUG=2

- ## 🏠 [Web front end for Ollama? Is llama.cpp what I'm looking for? : r/ollama](https://www.reddit.com/r/ollama/comments/1p0p1pm/web_front_end_for_ollama_is_llamacpp_what_im/)
- Ollama is a wrapper and somewhat of a fork of llama.cpp. Ollama runs on a core version of llama.cpp but doesn't have the same capabilities or features as far as granular controls.
  - But they're at their heart inference engines first thst happen to have their own options front ends. I've used both with Open WebUI for about 8 months.
  - Ollama has a chat interface now that is not cli. But it's just chat and some basic rag. If you want pipelines, oauth, in depth RAG etc., you need something like OWUI, Libre Chat, AnythingLLM or LocalAI

- ## [502 Bad Gateway · Issue · ollama/ollama _202407](https://github.com/ollama/ollama/issues/5437)
- you're right, I ignored the proxy.

- [Running without network error: ollama._types. ResponseError · Issue #85 · ollama/ollama-python](https://github.com/ollama/ollama-python/issues/85)
  - Met similar issue that direct me here, fixed by turning off the global proxy.
  - Tried turning off the wifi, and it still works (on MacOS).

- [ValueError: Ollama call failed with status code 502. Details · Issue #20742 · langchain-ai/langchain](https://github.com/langchain-ai/langchain/issues/20742)

- ## [使用OllamaEmbeddings时，报错ollama._types. ResponseError(status code:502)和(status code:500)_ollama 502-CSDN博客](https://blog.csdn.net/m0_70647377/article/details/146829186)
- 1. 关闭VPN代理，重试

- 2. 在cmd中设置两步
  - set OLLAMA_HOST=0.0.0.0
  - ollama serve

- ## 💡 [Electron & root priveleges · Issue · ollama/ollama _202311](https://github.com/ollama/ollama/issues/1076)
  - This project has 84% of the codebase written in Go, but for some reason it uses Electron, which is very heavy (500MB+) both for persistent memory and RAM usage.
- 202404: I successfully migrated the ollama mac app from electron to Tauri. The app package size is only 30M and the memory usage is only 100M.

- ## 🏞️ [Can add Stable Diffusion 3.5 model？ · Issue · ollama/ollama _202412](https://github.com/ollama/ollama/issues/8047)
  - Does Olama not support the Diffusion 3.5 model? Can we add an Diffusion 3.5 model?

- Short answer is no, you shouldn't be able to as Ollama is dedicated to Large LANGUAGE models.
  - Longer answer is that in general, Stable diffusion and Large Language Models require different architectures, and while some llava models (and more recently Llama models) do have the ability to reason about images, being able to identify an image / the contents of an image is inherently different from being able to generate one, and ollama isn't designed or equiped for that.
- For stable diffusion you should be looking into something like Automatic1111, forge, comfy, or swarm (to name a few of the more popular projects).

- ### [Image generation models · Issue · ollama/ollama](https://github.com/ollama/ollama/issues/786)
- Ollama currently uses llama.cpp to do a lot of the work of actually supporting a range of large language models. This choice allowed the team to focus on delivering value in other ways. Llama.cpp's reasons for not supporting text-to-image models are probably for similar reasons.

- There are plenty of Stable Diffusion UIs and all of them are drowning in issues and features because of this:
  - Automatic1111: most popular, most fully-integrated environment
  - ComfyUI: very modular, usually has the newest features first, allows flexible workflows
  - Fooocus: restricted and opinionated but focused on providing a simple UI which produces good output out of the box (original author is the inventor of ControlNets and has a deep understanding of the inner workings of Stable Diffusion). probably the closest to Dall-E 3 (Fooocus provides a GPT2 prompt rewrite engine in the background)
  - SD. Next: fork and overhaul of Automatic1111 because everything took sooo long to implement
  - (I think all of them provide API endpoints)

- I'd recommend Stable Diffusion 1.5 because it has the lowest hardware requirements and integration is simpler and will be faster. Later models have more specifics which require more attention to detail.

- ## [image generation : r/ollama _202410](https://www.reddit.com/r/ollama/comments/1g5lp9s/image_generation/)
  - is there any model that allows image generation?

- nope, but there are some vision models that capable of taking images as input

- You can add ComfyUI, Automatic1111 or LocalAI via API to generate images in OpenWebUI, though it’s somewhat finicky. It creates images from the LLM‘s answer, not the Edit: prompt

- I am running Flux locally. It does a decent job in the dev model, there are 2 higher levels that aren’t for commercial use.

- [Image generator : r/ollama](https://www.reddit.com/r/ollama/comments/1iuzv2v/image_generator/)
  - No llm are able to generate image... However, you can let your llm reply with tool_call to fill a image promot to be sent to another ai model that generate images (chatgpt4o-dalle3 for exemple)

- [How can I generate images with ollama? : r/ollama](https://www.reddit.com/r/ollama/comments/18laoe6/how_can_i_generate_images_with_ollama/)
- Ollama doesn't yet support stable diffusion or creating images. It does support image to text though.

- If you are using Mac you can either use diffuser or diffustionbee.

- ## 🎯 Ollama 0.10! Ollama's new app is here for macOS and Windows _20250731
- https://x.com/ollama/status/1950670503376761133
- [Ollama's new app](https://ollama.com/blog/new-app)
- Ollama’s macOS and Windows now include a way to download and chat with models.
  - Ollama’s new app supports file drag and drop, making it easier to reason with text or PDFs.
  - For processing large documents, Ollama’s context length can be increased in the settings. Note: this will require more memory.
- Building on Ollama’s new multimodal engine, images can be sent to models that support them, such as Google DeepMind’s Gemma 3 model.
- Code files can be processed by models for understanding.

- Is this ollama CLI with its own GUI?
  - Ollama’s new app includes the CLI. You can also use Ollama’s API or try Ollama’s Python/JavaScript libraries.

- It would be nice it it recommended models for my hardware? or is it already doing that?
  - Not yet, but we have hand selected the top models that will run on most users' hardware.

- What would be the use case over LMStudio on Mac?
  - quality, ease of use, model support directly with the major labs, hardware support
- 🐛 I understand and appreciate ease of use and minimalism. It's really great when you'd want to chat with a model. However, as far as I understand there is still no MLX support. I'm strictly talking about MacOS version here.

- All that's missing now is MCP support.

- Can i choose where to save my models?
  - Yes, check out Ollama settings

- Feature request: Allow the user to set the Ollama endpoint. I run it on a beefy desktop computer but would like to use the app as a client.

- can you use it if the models are a other pc as a server
  - not yet. In the future, we'll add the support.

- Ollama natively support new AMD gpus?
  - We are working with @AMD to support the new GPUs

- We need our own completions API — I have the feeling that tool calling doesn't work properly with the OpenAI SDK. The tool tags need improvement; for example, DeepSeek R1 shows tool support, but the 8B version doesn’t, even though it’s based on Qwen3, so it should.

- 其实早就有第三方的了...... 不过感觉官方合并功能了后更方便了属于是

- ## Ollama 0.2 is here! Concurrency is now enabled by default.  _20240709
- https://x.com/ollama/status/1810480544976626159
  - Parallel requests: Ollama can now serve multiple requests at the same time, using only a little bit of additional memory for each request.
  - Run multiple models: Ollama now supports loading different models at the same time

- ## So this is an LLM running locally? `ollama run llama3` .
- https://x.com/eatonphil/status/1797039865470570942
  - Asking it to help me with some Postgres C code. It's complete nonsense, but it's impressive complete nonsense
  - `ollama run codestral` looks about right though.
- How much RAM am I supposed to have for the 70B model?
  - B × Q / 8 → RAM requirement for llm inference in GB
  - B: number of parameters
  - Q: quantization (16 = no quantization)
  - useful rule of thumb for RAM requirement for llm inference via hn user CobaltFire
- 3bit quantized should work with 32 GB RAM with other apps closed

- based on the download size that looks like the 7b model (smallest), which are pretty hopeless at anything beyond basic coding in my experience (codestral is a 22b iirc)
  - also if you like using models from the command line i highly rec @simonw 's `llm` cli! i believe it supports ollama

- ## 🐛 [Error: pull model manifest · ollama/ollama](https://github.com/ollama/ollama/issues/3434)
  - Error: pull model manifest: Get "https://registry.ollama.ai/v2/library/codellama/manifests/70b": read tcp 192.168.3.79:64976->172.67.182.229:443: read: operation timed out
- Error: max retries exceeded: Get "https://dd20bb891979d25aebc8bec07b2b3bbc.r2.cloudflarestorage.com/ollama/docker/registry/v2/blobs/sha256/14/1436d66b69757a245f02d000874c670507949d11ad5c188a623652052c6aa508/data?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=66040c77ac1b787c3af820529859349a%! F(MISSING)20240529%! F(MISSING)auto%! F(MISSING)s3%! F(MISSING)aws4_request&X-Amz-Date=20240529T155900Z&X-Amz-Expires=1200&X-Amz-SignedHeaders=host&X-Amz-Signature=cd4472bad19931e399f39a352a4a1b0902857996b7b784b8138f168d70532277": dial tcp 104.18.8.90:443: i/o timeout

- ## [为什么Llama2大模型可以在个人电脑上部署 ？ - 知乎](https://zhuanlan.zhihu.com/p/646939066)
- 我在Meat的官网上看到 llama2 是构建在PyTorch之上的，而ChatGPT是基于TensorFlow Probability框架的，本文里面就简称TFP。

- ## [Meta AI 为什么会开源 Llama2 呢? - 知乎](https://www.zhihu.com/question/613072688/answers/updated)
- 因为所谓的LLM开源只是公布训练好的结构和参数而已，真正重要的数据和训练代码并没有开源，更别说大部分人还没有足够的GPU。
  - 即使如此，目前mistral这样的也只开源7b不开源large，llama后续还得继续观察

- Llama2 开源但不是可以随便用的商用许可。 用户数到了一定程度就不是免费的。
  - 7亿月活

- ## [Allow listening on all local interfaces _202310](https://github.com/ollama/ollama/issues/703)
- If you’re running Ollama directly from the command line, use the
`OLLAMA_HOST=0.0.0.0 ollama serve` command

- Edit the service file: Open `/etc/systemd/system/ollama.service` and add the following line inside the [Service] section:
`Environment="OLLAMA_HOST=0.0.0.0"` 

- sudo systemctl daemon-reload
- sudo systemctl restart ollama
