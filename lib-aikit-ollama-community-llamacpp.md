---
title: lib-aikit-ollama-community-llamacpp
tags: [ik_llama.cpp, llama.cpp, ollama]
created: 2026-05-21T15:36:43.594Z
modified: 2026-05-21T15:37:00.694Z
---

# lib-aikit-ollama-community-llamacpp

# guide

# discuss-stars
- ## 

- ## 

- ## 

- ## 
# discuss-news
- ## 

- ## 

- ## 

- ## 

- ## 

- ## 

- ## Highlighting recent advances in multi-GPU and tensor parallel support in llama.cpp 
- https://x.com/ggerganov/status/2062443065214702027
  - Over the last few months llama.cpp maintainers and engineers from NVIDIA collaborated to improve the multi-GPU performance in ggml. This resulted in significant performance gains on RTX systems and laid the groundwork for hardware-agnostic tensor parallelism in ggml.

- The real story here isn't just raw speed, it's that we can finally run tensor parallel inference across consumer GPUs without the PCIe bottleneck completely killing our token rate.

- ## The work to bring full-fledged WebGPU support in llama.cpp started about an year and a half ago. _202605
- https://x.com/ggerganov/status/2057668450076520811
- Why do this? Certainly WebGPU is worse than direct CUDA.
  - CUDA doesn’t run in the browser

- running llama models in a browser with gpu accel is genuinely wild. does it work on safari too or chrome only?
  - The demo in the blogpost should work in Chrome and Safari
# discuss-tips/tricks
- ## 

- ## 

- ## 

- ## 
# discuss-alternatives
- ## 

- ## 

- ## 

- ## 

- ## [What are the benefits of using LLama.cpp / ik_llama over LM Studio right now? : r/LocalLLaMA _202604](https://www.reddit.com/r/LocalLLaMA/comments/1s9iqya/what_are_the_benefits_of_using_llamacpp_ik_llama/)
- llama.cpp has always the latest code (newest features, fixes and optimizations)
- LM Studio just uses old llama.cpp build under the hood anyway, can take weeks for changes in llama.cpp to make it into LM Studio. Best bet is running llama.cpp / vllm from latest release or build it yourself.

- lm studio still doesn't support ubatch I think. you could gain at least 2-3x prompt processing.
  - lm studio has around 0.5gb vram overhead. makes a bit of a difference if you're tight in space.

- After the --fit, --fit-target, and --fit-ctx flags were added in llama.cpp, I stopped using --override-tensor (or -ot) because performance is usually identical anyway.
# discuss-news
- ## 

- ## 

- ## 

- ## llama.cpp now has a BUILT-IN model router  _202605
- https://x.com/fahdmirza/status/2057353958377828581
  - it completely replaces Ollama + Open WebUI for model switching
  - One server, one config file, any model on disk. Full per-model control via a simple INI file
  - Switch models instantly without restarting anything

- How does this compare with llama-swap?
  - It looks the same. All they do really is check the http request model header and start a new server process. But as it's integrated into llama.cpp they can make it faster to load and other optimizations in the runtime. 
  - Ok I was wrong, they're essentially the same, they run a parent process that listens for http request, then child processes for the models. There is no beneficial deeper integration into the runtime.
  - The fundamental architecture is the same in principle: Both `llama-swap` and the `llama.cpp` router use a parent process that manages child processes, with each model running in its own `llama-server` instance (or equivalent). There is no shared memory between models. `llama-swap` is an external Go proxy that starts/stops these processes, while the `llama.cpp` router has the same logic built directly into `llama-server` (multi-process architecture). It's the same core idea — separate processes per model instead of a single server swapping models in one process.
- However llama-swap can be used with other inference engines as well, honestly in my setup I think llama-swap may be better as it can switch between a vLLM run model or llama run model.

- I doubt it'll be as flexible as llama-swap. I use llama-swap to server llamacpp (vulkan) llamacpp (lemonade rocm) and ds4 inference servers.

- Actually while behaving the same, it also supports running multiple models in the same time, for example 1 GPT-OSS-20B and 1 Qwen 27B for local multi agent purposes and It's pretty neat.

- ## [Llama.cpp now supports distributed inference across multiple machines. : r/LocalLLaMA _202405](https://www.reddit.com/r/LocalLLaMA/comments/1cyzi9e/llamacpp_now_supports_distributed_inference/)

# discuss-issues
- ## 

- ## 

- ## 

- ## [llama.cpp PR to implement IQ_K and IQ_KS quants from ik_llama.cpp : r/LocalLLaMA _202602](https://www.reddit.com/r/LocalLLaMA/comments/1r91akx/llamacpp_pr_to_implement_iq_k_and_iq_ks_quants/)
- finally, been waiting for the ik_llama quants to land upstream. the quality gains at low bpp were wild compared to standard Q4

- Weird, is there some sort of bad blood between Llama.cpp and ik_llama.cpp? Simply assumed ik_llama.cpp was going for max speeds while llama.cpp was going for max compatibility and they diverged from opinions on design differences.
# discuss-ik_llama.cpp-tips
- ## 

- ## 

- ## 

- ## [Unofficial ik_llama.cpp release builds available for macOS, Ubuntu and Windows : r/LocalLLaMA _202602](https://www.reddit.com/r/LocalLLaMA/comments/1qwo5ig/unofficial_ik_llamacpp_release_builds_available/)
  - https://github.com/Thireus/ik_llama.cpp/releases
- Correct me if I'm wrong, but isn't ik_llama.cpp mainly aimed at CPU and CUDA inference? I mean that's what I use it for. What's the point on a Mac when you can't use the GPU?
  - Because it has SOTA speed on CPU-only inference.
- Better than mlx implementations?
- to be specific, AVX-512 CPU + CUDA; but the CPU kernels are just meh, especially so on MOE models. The kt_kernels made by k_transformers + Intel are insanely good. They were recently integrated by SGLang and are are significantly faster than llama.cpp / ik_llama.cpp CPU kernels.
  - K_transformers requires a special dance and the stars to be aligned just right to work, and their hardware support is limited. SGLang might be more stable, but is still limited in hardware support.

- Can they work without VNNI/amx or other fancy SIMD and without full massive pytorch weights? Hard to find any good hybrid + numa option besides ik. Closest second was fastllm but it has opaque documentation and can only do attention on gpu/rest on CPU splits. For DDR4 that's not that good despite the numa boost.
  - Yep… they support just about every CPU. And have real numa, to include numa sharding and duplication. Even support gguf
# discuss-ik_llama.cpp
- ## 

- ## 

- ## 

- ## 
# discuss-internals
- ## 

- ## 

- ## 
# discuss-llama-swap
- ## 

- ## 

- ## 

- ## 

- ## 

- ## 🌰 [Add mlx_lm.server example by losuler · Pull Request · mostlygeek/llama-swap _202509](https://github.com/mostlygeek/llama-swap/pull/302)
  -  I wanted to add an example for anyone else who is coming across the same problem. Which was that without useModelName being the file path, mlx_lm.server is using the model name, which causes it to download the model to the huggingface cache path, instead of using the one I manually downloaded to the specified --model path.

- [Profiles not working · Issue · mostlygeek/llama-swap](https://github.com/mostlygeek/llama-swap/issues/145)
  - Profiles were replaced with the Groups feature. 
  - Groups provide better parallel control and reduced internal complexity a bunch.

- ## 🆚 [To everyone using still ollama/lm-studio... llama-swap is the real deal : r/LocalLLaMA](https://www.reddit.com/r/LocalLLaMA/comments/1rm7nq1/to_everyone_using_still_ollamalmstudio_llamaswap/)
  - Both ollama and lm-studio have the "load models on demand" feature that trapped me. But llama-swap supports this AND works with literally any underlying provider. I'm currently running llama.cpp and ik_llama.cpp, but I'm planning to add image generation support next.
  - It is extremely lightweight (one executable, one config file), and yet it has a user interface that allows to test the models + check their performance + see the logs when an inference engine starts, so great for debugging.

- Why do you need llama-swap if llama-server also has builtin functionality with the router mode?
  - The main reason to use llama-swap over llama.cpp is if you either want to use different inference services (like have some models go to llama.cpp and others to vLLM) or if you want specific customizations for each model beyond what llama.cpp will allow without server restart.
  - llama.cpp’s built in router mode is probably enough for 95% of folks, including OP
- yep same here, I'm using vllm behind llama swap , also it allowed to proxy requests to external endpoints.
- llama.cpp's router mode already allows you to customize for each model using presets.

- llama-server router is llama.cpp-only. the moment u want ik_llama.cpp or any other backend in the mix, that option disappears. llama-swap wraps whatever inference engine u throw at it , that's the actual difference.

- If you’re only using LLM and gguf the builtin router mode will probably be enough.
  - There are a few things that I am free to add to llama-swap that probably don’t make sense in llama-server’s router:
  - audio endpoints for tts/stt
  - image gen endpoints with stablediffusion.cpp
  - filters like setParamsByID that allow toggling of reasoning mode without reloading the model
  - peer routing to remotely hosted models: another llama-swap, openrouter, vercel, etc
  - the UI playground and debug features
  - support for other engines like ik_llama, vllm, sglang, basically anything that supports an openai or anthropic api
  - I think the range of tools looks pretty good now. There are simple but more limited tools. llama-server is in the middle, more powerful but also more complex. llama-swap I’m pushing to the edge where you can have a very powerful, multi-engine, multi-model set up. It’s so great that people can choose something that match their comfort and skill level.

- https://github.com/meganoob1337/llama-swap-vllm-boilerplate
  - The repo also shows how to use vllm in docker with llama-swap

- llama-swap is very useful for me in ways that llama-server isn't. Of course the ability to use different providers is the road-blocker of llama-server. 
  - To me the real deal is the convenience features it provides.
  - It's just so much nicer to have the UI to debug and test different models and versions, and being able to swap them with almost no-downtime is awesome. i.e., when I update llama.cpp, or download a new quant for a model, I only need to update the config.yaml, and when I save it I have 2-3 seconds of downtime, and any bugs are immediately apparent thanks to the log. It's just very convenient. It feels right to have the router split from the providers. I previously used open-webui for this, but llama-swap is more convenient for many use cases I have.
  - I manage several servers and I do tons of experiments with different quantizations and providers, and llama-swap has been a blessing. But of course, this is my personal use case which may not translate to others.

- If anyone wants to have something similar but with web ui instead of config files, I built llamactl. It has full support for llama-server router mode. It also supports vllm, mlx_lm and deploying models on other hosts. The model swapping options are not as complex as llama-swap - I only support simple LRU eviction at the moment.

- I use it because llama-swap can be used for lots more than just llama.cpp. I do whispercpp and stablediffusioncpp under it at the same time as llamacpp.

- Can llama-swap start and stop different underlying providers (ollama/llama.cpp/ik_llama/vLLM/…)?
  - Yes, and it is configurable. You can define different groups of models (each with their own defined provider), and configure the evicting behavior by configuring swap and exclusive controls.
# discuss
- ## 

- ## 

- ## 

- ## [Audio processing landed in llama-server with Gemma-4 : r/LocalLLaMA _202604](https://www.reddit.com/r/LocalLLaMA/comments/1sjhxrw/audio_processing_landed_in_llamaserver_with_gemma4/)
  - llama.cpp (llama-server) now supports STT with Gemma-4 E2A and E4A models.
- I wonder if it's better than Whisper at transcription.
  - Tbf, Parakeet is already better than Whisper. Anything that doesn't make shit up on silence is better than Whisper.
- parakeet is amazing and extremely fast even on CPU. wondering how gemma4 is compared to parakeet, bummer that only E2B and E4B have it

- It seems that there are some issues left to be ironed out. In the current state it's mostly unusable for me for 5+ minutes of audio - Voxtral works way better. I'm using E4B as Q8_XL quant with BF16 mmproj (recommended, as other mmproj formats lead to degraded capabilities)

- Nice, but watch the VRAM hit: audio tokenization and STT usually push context pressure up fast. On 8GB cards this is probably GGUF-only territory unless the model is tiny; would love a rough ms/sec benchmark on CPU vs CUDA.

- ## ⚡️ [Breaking change in llama-server? : r/LocalLLaMA _202603](https://www.reddit.com/r/LocalLLaMA/comments/1s62el8/breaking_change_in_llamaserver/)
  - Migrating cache to HuggingFace cache directory
  - Old cache: /home/user/.cache/llama.cpp/
  - New cache: /home/user/GEN-AI/hf_cache/hub
  - And all of my .gguf models were moved and converted into blobs. That means that my launch scripts all fail since the models are no longer where they were supposed to be...

- The gguf reference is still there. It links to the blob.

- My .cache directory is a symlink to an NFS volume shared by multiple hosts. So no, it's not fine at all, to move all the models off my NFS share to the local host

- ## 🆚 [Ik_llama vs llamacpp : r/LocalLLaMA _202603](https://www.reddit.com/r/LocalLLaMA/comments/1rsyo23/ik_llama_vs_llamacpp/)
- Its good, I get a decent speed improvement on ik_llama.cpp though regular llama.cpp seems to have better overall support. Speed improvements are usually in the range of 15-20%, which is always appreciated. 
  - Generally I use regular llama.cpp for anything brand new and then ik_llama.cpp once I have a more established workflow/its been updated. 
  - Haven't had ik_llama.cpp crash except for some weirdness for GLM 5 Ubergarm quants so stability doesn't seem to be an issue.

- Anyone running ik_llama on AMD hardware? They have a disclaimer that the only supported setup is CPU+CUDA, so I haven't tried it yet.
  - I tried, you can't. Kawrakow has explicitly said ROCm is not supported. There was a thread a while back where he asked in a poll whether to add Vulkan support. Most people voted yes, but I haven't heard of any progress on that front.
  - It's mostly a one man show, so it's totally understandable.

- Performances of ik are far above llama.cpp but they so not support all hardware type. As the ik has a smaller team, it evolves fast and support is very active.

- ik_llama has better quants and optimization, iq-k quants run faster when you offload moe on CPU, iq-kt quants keep better fidelity within similar size.

- If your model runs entirely on gpu try vllm especially for batches. Ik_llama is for hybrid inference

- Prompt prefil is faster of ik_llama.cpp you have to enable all the flags though. Like split mode graph etc. and throughout is much faster. Tgen is also faster

- ## [using llama.cpp via remote API : r/rust _202505](https://www.reddit.com/r/rust/comments/1kssi8v/using_llamacpp_via_remote_api/)
  - What crate is recommended to connect to a remote instance of llama.cpp (running on a server), sending in data (e.g. some code) with a command what to do (e.g. "rewrite error handling from use of ? t

- ## 🖼️ [Vision support in llama-server just landed! : r/LocalLLaMA _202505](https://www.reddit.com/r/LocalLLaMA/comments/1kipwyo/vision_support_in_llamaserver_just_landed/)
  - llama.cpp supports multimodal input via `libmtmd` .
- With this the need for Ollama (to use with llama vision) is gone. We can now directly fire up llama-server and use OpenAI chat-completions. Local image tagging with good vision models is now made simple.

- ## [llama.cpp: Multi-host inference slower than single-host? : r/LocalLLaMA _202512](https://www.reddit.com/r/LocalLLaMA/comments/1pwmpcn/llamacpp_multihost_inference_slower_than/)
  - I have two computers running locally and I want to see how I can get faster generation speeds by combining them instead of running the models separately on each computer.
  - I've built a very recent version of llama.cpp on both hosts (jetson using CUDA12 and Dekstop using ROCm 6.7). I use the unsloth Qwen3 80B Q8. This model is 87GBs and hence it's larger than both hosts individually, but the entire model fits into RAM when combined.
  - Using both combined yields a generation speed of 1.1 t/s. However, if I use the desktop llama-cli command exactly the same as above but remove the --rpc "$JETSON_IP_ADDR:12400" (hence disabling multi-host), then I'm at double the speed of 2.2 t/s.

- Even with no latency, you won't get faster speed with llama.cpp, because it can't do tensor parallel, only layer splitting. It allows to serve larger models, but doesn't increase speed.
  - You can do tensor parallel with vllm, but your interconnect will be a bottleneck, unless you use RDMA capable NIC (ConnectX from NVidia/Mellanox).
  - I see you have ROCm/CUDA mix and uneven VRAM distribution, so vllm won't work either.

- ## ["Router mode is experimental" | llama.cpp now has a router mode and I didn't know. : r/LocalLLaMA _202512](https://www.reddit.com/r/LocalLLaMA/comments/1pfssoo/router_mode_is_experimental_llamacpp_now_has_a/)
- While this is cool, I still do think llama-swap is very mature and worth using rn.

- ## [Mastering llama.cpp: A Comprehensive Guide to Local LLM Integration : r/LocalLLaMA](https://www.reddit.com/r/LocalLLaMA/comments/1ov2ll9/mastering_llamacpp_a_comprehensive_guide_to_local/)
- no mention of override tensor, CPU MoE offloading, API keys, and a lot more stuff. To the people who found this Reddit post, this guide pretty surface level.

- ## [Question about "./llama-server" prompt caching : r/LocalLLaMA _202507](https://www.reddit.com/r/LocalLLaMA/comments/1lujz2h/question_about_llamaserver_prompt_caching/)
  - Does `./llama-server` support prompt caching (like `--prompt-cache` in the CLI), and if not, what’s the correct way to persist or reuse context between chat turns to avoid recomputing the full prompt each time in API-based usage (e.g., with Open WebUI)?
- Yes, it's enabled by default but only for one chat: If you have stuff in Open WebUI that makes use of the same model (title and tag generation, autocomplete, etc.) then it will be sending different requests which invalidates the main chat.

- Yes, llama-server supports it, no parameter needed. It's up to the client to make use of it. Works fine with Open WebUI (GUI) but you're asking for API. I guess you'll have to initiate a chat and send the chat_id in all your subsequent API calls. I did not test this yet.

- 🧑‍🏫 [Tutorial: KV cache reuse with llama-server · ggml-org/llama.cpp _202505](https://github.com/ggml-org/llama.cpp/discussions/13606)
  - This tutorial demonstrates how to use the slots management feature in llama-server to optimize repeated prompt processing through KV cache reuse.

- ## 🆚⚡️ [Performance of llama.cpp on Apple Silicon M-series · ggml-org/llama.cpp _202311](https://github.com/ggml-org/llama.cpp/discussions/4167)
  - 提供了各种mac, air的模型测试数据
