---
title: lib-aikit-ollama-community-mlx
tags: [apple, community, large-language-model, macos, mlx]
created: 2026-01-14T18:58:39.517Z
modified: 2026-01-14T18:59:01.949Z
---

# lib-aikit-ollama-community-mlx

# guide

# draft

# xp-mlx

- mlx不仅支持text-gen, 还支持image-gen, 对multimodal模型的支持比llama.cpp更好
# discuss-stars
- ## 

- ## 

- ## [Whats up with MLX? : r/LocalLLaMA _202603](https://www.reddit.com/r/LocalLLaMA/comments/1rvy3nk/whats_up_with_mlx/)
  - I am a Mac Mini user and initially when I started self-hosting local models it felt like MLX was an amazing thing. It still is performance-wise, but recently it feels like not quality-wise.
  - from what I see GGUF community seem to be very active: they update templates, fix quants, compare quantitation and improve it; however in MLX nothing like this seem to happen - I copy template fixes from GGUF repos
  - you open Qwen 3.5 collection in mlx-community and see only 4 biggest models; there are more converted by the community, but nobody seems to "maintain" this collection

- The main thing i would like from mlx is a robust non-python inference option

- From my benchmarks on M4 Pro 64GB with Qwen3.5 35B A3B, MLX still has a real performance edge for generation on short context: ~80 tok/s (LM Studio MLX) vs ~30 tok/s (Ollama GGUF).
  - But MLX falls apart on large contexts. Prefill TTFT on context fills: ~14s for MLX vs ~4s for GGUF - that's 3x slower. And MLX token generation degrades as context grows, while llama.cpp stays stable.
  - So the raw engine performance is still there for MLX, but I agree with the general sentiment: the ecosystem around GGUF (quant quality, community maintenance, template fixes) is way ahead. For daily coding work with large contexts, I'd recommend switching to GGUF.

- I'm not sure why the updates from mlx-community or lmstudio-community are so slow for the Qwen3.5 models. I think my main concern is the realization that MLX quantization is way worse than the state of the art GGUF, to the extent that you're better off running a smaller GGUF model. This undoes a lot of the supposed speed benefit from MLX. Also, the most advanced quantizations like DWQ don't seem to support the new Qwen architecture.
  - I currently mostly use MLX and they are a lot faster and better than GGUF. Especially MXFP4 quants. The only problem MLX had for a long time was a bad kv cache strategy which often led to reprocessing the full prompt. But MLX has improved and oMLX is far ahead of llama.cpp - at the price of longer TTFT but you can deactivate the SSD cache.
- If you say MLX quants are better than GGUF, that just tells me you haven't tested them seriously or probably not at all. You need a 4 or 5-bit MLX to get similar quality as an IQ3_XXS, very roughly. MLX can't use imatrix or any of the dynamic quant tricks people do with GGUF. DWQ changes things, but it's not supported for Qwen3.5, as already said.

- Some people benchmarked mlx and gguf equivalent models (Qwen-3.5 specifically) running on a Mac, and unfortunately for agentic coding at least the gguf versions were superior on successful tool calling in multiple-round interactions.
  - For some reason, mlx performance deteriorates after multiple rounds while llama.cpp remains consistent.

- Qwen3.5 working much better on llama.cpp than mlx. I recently changed and the prompt processing is amazing

- Qwen3.5 Hybrid attention is seems to be problematic too. I cam to the same conclusion. oMLX is impressive in raw generation speed for benchmark scenarios. In real-world use cases it plummets. There are many issues. I slowly come to the conclusion myself, that GGUF is still the way to go after a lot of testing.
  - Prompt caching is currently also broken for Qwen3.5 multimodal models in the MLX runtime. Ram filling, stability and quality seems to be a problem too.

- MLX is super useful for things other than LLMs too. I have local STT (nemotron) and TTS (chatterbox) and it runs faster than real time.

- ## 原来 mlx 上的量化不如 unsloth 的 gguf 是这个原因
- https://x.com/wey_gu/status/2037547112859365495

- https://x.com/terrywang/status/2037720685112697171
  - MLX 社区转换格式很随意：用基于 mlx-lm mlx-vlm 的脚本转换，根本去考虑量化的细节。
  - 补充：根本原因是 MLX 用统一量化（偷懒）；而 Unsloth 用 per-tensor mixed-bit quant 说人话：根据每个权重张量的敏感性分配不同的精度。
  - 一刀切对混合架构模型（不同层对精度敏感度差异巨大）来说是毁灭性的。可表现为：长输出会直接崩掉。

- MLX 也有 mixed precision quantization，不过不能用官方的 runtime
  - [JANG — 397B on a 128 GB Mac | The GGUF for MLX _202603](https://jangq.ai/)
  - https://github.com/jjang-ai/jangq /202603/python
  - MLX Studio has full native JANG support. oMLX has added JANG integration (PR #364). LM Studio, Ollama, and Inferencer do not support JANG yet — ask your favorite app's creators to add support, or use pip install "jang[mlx]".

- ## 🧩🔧 [Open source LLM compiler for models on Huggingface. 152 tok/s. 11.3W. 5.3B CPU instructions. mlx-lm: 113 tok/s. 14.1W. 31.4B CPU instructions on macbook M1 Pro. : r/LocalLLaMA _202603](https://www.reddit.com/r/LocalLLaMA/comments/1rspblk/open_source_llm_compiler_for_models_on/)
- https://github.com/pacifio/unc /MIT/202603/cpp/metal
  - HuggingFace transformer compiler for optimised native inference binaries

- ## [MLX is not faster. I benchmarked MLX vs llama.cpp on M1 Max across four real workloads. Effective tokens/s is quite an issue. What am I missing? Help me with benchmarks and M2 through M5 comparison. : r/LocalLLaMA _202603](https://www.reddit.com/r/LocalLLaMA/comments/1rs059a/mlx_is_not_faster_i_benchmarked_mlx_vs_llamacpp/)
  - Setup: Mac Studio M1 Max, 64 GB. LM Studio 0.4.5. Qwen3.5-35B-A3B, MLX 4-bit vs GGUF Q4_K_M. Warm model, temperature 0.6, thinking mode off.
  - That tok/s number only measures generation (tokens produced one at a time). It ignores prefill (processing the entire input before the first token appears). Prefill scales with context size. Generation doesn't. At 8.5K tokens of context, prefill was 94% of MLX's total response time. Thats super misleading. So even though your counter says: fast. Its super slow in practice.
  - Where MLX still wins: long output with short context. For creative, single prompt inferencing its super fast. However, in day-to-day workloads like an 8-turn agent conversation with 300-400 token replies, results swing back and forth. MLX wins most turns because the 2x generation speed compensates for slower prefill when there's enough output. 
  - GGUF again is better, for long input prompts and shorter outputs, like my document classification use case.

- Qwen 3.5 uses a hybrid attention mechanism. Llama.cpp probably supports it better than MLX. MLX is probably using a standard attention mechanism, which is why on short prompts you aren't see the difference, but on long prompts the hybrid attention will make a lot of difference.

- There is a known issue with mlx runtime in lmstudio, where prompt caching for qwen3.5 multimodal is not working, which means, that for each turn of conversation with the agent, the whole conversation history is processed again (rather than just new tokens). One way around this with current stable lmstudio version, is to use qwen3.5 version, that has vision part removed (there are a bunch of quants like that available). 

- ## I attached a benchmark chart (Apple M4 Max 128GB, 4-bit) showing vllm-mlx beating llama.cpp across multiple model families, roughly ~1.17× to 1.87× faster depending on the model. _202602
- https://x.com/mynamekarma/status/2021375707021181330
  - And it’s not just text-only either, multimodal caching is getting stupid fast (image prefix cache 21.7s → 0.78s, up to 28×).
- Compare it to mlx-server, not llama.cpp.

# discuss-news
- ## 

- ## 

- ## 

- ## Ollama is now updated to run the fastest on Apple silicon, powered by MLX _202603
- https://x.com/ollama/status/2038835449012351197
  - [Ollama is now powered by MLX on Apple Silicon in preview · Ollama Blog _202603](https://ollama.com/blog/mlx)
  - NVFP4 support: higher quality responses and production parity 
  - Ollama now leverages NVIDIA’s NVFP4 format to maintain model accuracy while reducing memory bandwidth and storage requirements for inference workloads.
  - Ollama’s cache has been upgraded to make coding and agentic tasks more efficient.

- ### [Ollama added support to MLX : r/ollama _202604](https://www.reddit.com/r/ollama/comments/1s8wk20/ollama_added_support_to_mlx/)
- Just wanted to share some quick benchmark results I got testing the new Ollama 0.19 preview with the MLX backend. 
  - Hardware: MacBook Pro M3 Max
  - Standard Backend (qwen3.5:35b) 
    - Prompt Eval (TTFT): 0.69 seconds,  Generation Speed: 31.98 tokens/second
  - MLX + NVFP4 Backend (qwen3.5:35b-a3b-coding-nvfp4)
    - Prompt Eval (TTFT): 2.57 seconds, Generation Speed: 71.45 tokens/second
  - The combination of Apple's MLX framework (avoiding CPU/GPU memory copying), the NVFP4 quantization, and the model's sparse Mixture-of-Experts architecture is incredibly efficient on Apple's unified memory.
# discuss-roadmap
- ## 

- ## 

- ## 

- ## 
# discuss-issues
- ## 

- ## 

- ## 

- ## 
# discuss-internals
- ## 

- ## 

- ## 

- ## [Multi-Token Prediction (MTP) for qwen-3.5 is coming to mlx-lm : r/LocalLLaMA _202603](https://www.reddit.com/r/LocalLLaMA/comments/1rzntv5/multitoken_prediction_mtp_for_qwen35_is_coming_to/)
  - Early support for generating multiple tokens per forward pass is in, and the gains already look solid: • 15.3 → 23.3 tok/s (~1.5x throughput boost)
- [feat: native MTP speculative decoding for Qwen3.5 · Pull Request · ml-explore/mlx-lm _202603](https://github.com/ml-explore/mlx-lm/pull/990)
  - Qwen3.5 checkpoints ship with a built-in Multi-Token Prediction head (mtp_num_hidden_layers: 1 in config) that predicts token t+2 from the backbone hidden state at t and the embedding of token t+1. 
  - This PR adds support for using it as a native speculative decoding mechanism. No separate draft model needed, at minimal extra compute (1 extra transformer layer).
  - 🐛 The PR works out of the box for the dense 27B, but MoE models (35B-A3B, 122B-A10B) fail conversion with "768 parameters not in model".  MoE acceptance rates are significantly lower than dense.

- Similar PR for llama.cpp on its way: [feat: MTP support for dense Qwen 3.5 (0.8B-27B)  · Pull Request · ggml-org/llama.cpp _202603](https://github.com/ggml-org/llama.cpp/pull/20700)
  - [Add Multi-Token Prediction (MTP) support for Qwen3.5 MoE · Pull Request · ggml-org/llama.cpp _202603](https://github.com/ggml-org/llama.cpp/pull/19937)

- This means this will give us a speed boost in ALL Qwen3.5 models? Including 35B A3B and Qwen3-Coder-Next ?
  - Nope. It is physically impossible for MTP to benefit you on a MoE unless you are batching multiple requests together. (Note: I said MTP. Yes, n-gram-mod specdec can benefit in very specific scenarios.)
# discuss-tips
- ## 

- ## 

- ## 

- ## 

- ## 

- ## 🆚 [MLX vs GGUF (Unsloth) - Qwen3.5 122b-10b : r/LocalLLaMA _202603](https://www.reddit.com/r/LocalLLaMA/comments/1rm94gy/mlx_vs_gguf_unsloth_qwen35_122b10b/)
  - I just benchmarked the newly uploaded Qwen3.5 122b a10b UD (Q5_K_XL) vs. mlx-community/Qwen3.5-122B-A10B-6bit on my M4 Max 128GB.
  - The first two tests were text summarization with a context window of 80k tokens and a prompt length of 37k and another one with a context window of 120k and a prompt length of 97k.

- Because I don’t think mlx vision does prompt caching. You’re reading speed vs much quicker response times
  - Yeah mlx is definitely slower for multi turn conversations as it doesn't prompt cache as well as a gguf does, at least that's what I've found when using lm studio.

- For agentic workflows like using Claude Code Router or OpenCode, you unfortunately have to stick with GGUF since MLX will result in cache misses on every request, causing you to process the entire prompt after each new request.
  - This is true if you use multimodal quant of qwen3.5. There are mlx quants available which have the vision part axed - prompt caching seems to work for me using those quants (I'm using lmstudio).

- The reason I prefer llama.cpp/GGUF is that llama-server is an all-in-one package:
  - good inference engine with support for anthropic-messages, openai-completions and openai-responses endpoint (meaning you can use it with any coding agent)
  - constrained output
  - killer web UI that recently added support for MCP and agentic loops.

- I'm using gguf instead of mlx because it supports mmap but mlx doesn't. If I load a large mlx model I can't do anything else even temporarily because the model uses up all the RAM, and every time I unload the model I'll have to process the prompt/context again from the beginning. But with gguf I can keep the model loaded so I won't lose the cached prompts.

- Since this post is about qwen3.5 specifically - I've read that unsloth did implement something like a tool call template fix into their gguf - I don't know if the mlx variant also needs something like this

- At 6 bits the output quality of all quants is already very high. The difference in accuracy is more noticeable with lower quants.
  - Yup, exactly this. At say 3-bits, performance of GGUF quants is similar to 4-bit MLX quants. The test from OP was actually fair because it's comparing 6-bit MLX vs 5-bit GGUF, which would be similar quality.

- I found lots of coding bugs caused by 4/5/6 bit MLX quantization (vs GGUF Q4_K_M or UD-Q4_K_XL) so I only use 8 bit MLXs now. They're a lot bigger than a GGUF of the same quality so I use MLX for small models and GGUF for large ones.
# discuss-llama.cpp-mac
- ## 

- ## 

- ## 🆚 [Gemma 4 - MLX doesn't seem better(faster) than GGUF : r/LocalLLaMA _202604](https://www.reddit.com/r/LocalLLaMA/comments/1spn7zh/gemma_4_mlx_doesnt_seem_better_than_gguf/)
- GGUF/llama.cpp has really caught up to MLX over the past few months by leaning into Metal.

- For m1-m2 macs you need to know they don't support bf16 while all pre-converted MLX models are bf16 for unquantizied weights. You are leaving a big chunk of performance by not doing a simple mlx_lm.convert --dtype fp16 for them
  - The absence of bf16 is painful.. although.. even then, Torch AMP is flaky on MPS.

- Use oMLX app, in oMLX you can quant Gemma to oQ4 with non-quant dtype set to float16 (takes 5 mins) and then run that.

- why people hate using mxfp version of MLX models?
  - MXFP4 and NVFP4 are 4 bit float point formats that some GPUs can work with natively. That way it can be much faster. It is not necessarily better than other formats, but native support means it doesn't need to be upcasted to FP16 before doing the calculation.
  - Unfortunately "some GPUs" == Nvidia Blackwell only.

- ## [New - Apple Neural Engine (ANE) backend for llama.cpp : r/LocalLLaMA _202603](https://www.reddit.com/r/LocalLLaMA/comments/1s835d5/new_apple_neural_engine_ane_backend_for_llamacpp/)
  - Note that ANE is the NPU in all Apple Silicon, not the new 'Neural Accelerator' GPU cores that are only in M5.
- At last on older M chips the NPU can only access 4gb of ram due to its addressing lanes limit

- Due to kv cache not support in NPU, and ram limitations, don’t expect too much! I research why NPU not used in mlx before, in short it can’t work at scale. we need M5 design, where NPU inside GPU instead

- This may not be that useful for LLMs but if this could be generalized for STT and TTS it would be a fairly big deal. Having something doing that sipping half a watt while leaving the rest of the system free is good
  - This 100%. During my testing, the only way to get a fully smooth voice AI on iPhone 15 is by offloading STT and TTS to ANE so the GPU can be fully utilized by the LLM.
- Bingo. In a system with an NPU and a GPU, the npu should handle the small stuff to free the GPU for the big stuff

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
- 

# discuss-mlx-gui
- ## 

- ## 

- ## 

- ## 

- ## 

- ## MLX a quick head to head between mlx-lm, omlx, LM Studio using Qwen3.6-27B-UD-Q3_K_XL model.
- https://x.com/ivanfioravanti/status/2048411835108389072
- Are these benchmarks with reasoning or without?
  - These are pure throughput with cut at 128 tokens generated so not so relevant, but evals I do think and no-think, clearly the first wins big.

- Benchmarking inference is brutal. Half the time you aren't even testing the hardware, you're just benchmarking the engine's default KV cache allocation policy.

- I find quantisation and vision support are the hardest. Most of the Apple Silicon sit on top of mlx-vlm so seem pointless to compare. Benchmarks though are difficult, there’s always something you forgot.

- 
- 
- 

- ## 🆚 MLX: there are far too many servers now: vMLX, oMLX, Osaurus, LMStudio, mlx-lm, mlx-vlm.
- https://x.com/ivanfioravanti/status/2042855890219327650
  - I'm finding all kind of different behaviors while testing inference servers on Apple Silicon. 
  - vMLX is ultra aggressive with caching, this can be good but in different runs it's getting cached elements of previous runs. How can I avoid this? I'm adding prefixes everywhere, I think I'll have to use random text here.
- https://x.com/ivanfioravanti/status/2043203888908574899
  - MLX benchmarking the various inference engines is a real mess at the moment.
  - I'm finding many issues under heavy load, wrong perf stats from some servers, wrong management of cache mixing parts of prompts from other sessions, OOM, bugs.
  - 🥇 mlx-vlm best performance overall in non cache scenarios
  - 🥈 omlx best cache management (7.3K prefill below sounds wrong to me)
  - 🥉 vmlx was unable to complete batch inference tests going in OOM with 32 parallel batch of prompt/tg 2048/128

- Very curious to hear which performs best. In LocalAI we use mlx-lm and mlx-vlm under the hood

- oMLX has a massive memory overhead, put their caching gives fast responses. But I prefer the raw performance of mlx-lm
  - Testing oMLX right now and you are right, they put a lot of emphasis on caching. I'm testing performance with and without it.
- vmlx solves this problem

- Missing Pico AI Server, which is a good one; and Ollama. Ollama was too late to the MLX game. Osaurus is my current favorite, but a little bloated with things I don't need. Pico AI Server is great, but, like most others, no Proxying. And yet, with all of these, I 'rolled my own'.

- any engine based on mlx is faster than llama.cpp on Apple Silicon, but... llama.cpp is far more stable than anything else on MLX side, at least for now.
# discuss
- ## 

- ## 

- ## 

- ## 

- ## 

- ## 

- ## 

- ## [Apple MLX framework released _202312](https://github.com/ggml-org/llama.cpp/discussions/4345)
- 202401: MLX v.0.0.9 just also added experimental GGUF file support
  - [GGUF support  · Pull Request · ml-explore/mlx](https://github.com/ml-explore/mlx/pull/350)
  - This adds GGUF support using the excellent `gguflib` 

- ## [Any experience serving LLMs locally on Apple M4 for multiple users? : r/LocalLLaMA](https://www.reddit.com/r/LocalLLaMA/comments/1ov5bpe/any_experience_serving_llms_locally_on_apple_m4/)
- vLLM, or any production grade multi user inference engine, does not support this platform.. I think the Apple multi user story is effectively "buy each user their own mac"
  - vllm works on metal now, sort of. not currently worth the trade offs in my opinion, though

- I have no experience with it, but considering how poorly it handles context I think it's safe to say it isn't going to work well at all with multiuser concurrency. It's really designed to be a single user device.

- Prompt processing is significantly slower on the Mac platform compared to nvidia so if the users are sending large contexts, they're going to see a big delay before they see output tokens. 
  - I use an m3 512 with qwen vl 30ba3b which is 1-2 seconds before outputting even with 2-3k contexts, but then also use deepseek 3.1 q4 (370 gigs) which can take up to 30 seconds to prompt process a 400-500 token input. Subsequent same requests (literally identical because of many text to image prompts) are much faster. Doing that with multiple users who are all submitting unique requests would be unbearably slow unless you submit and walk away. This is with lm studio and the mlx versions of the models. 
  - Vllm isn't correctly supported on mac, and you get a 25% speed reduction if you use ggufs compared to the mlx versions.

- ## [MLX added support for MXFP8 and NVFP4 : r/LocalLLaMA _202510](https://www.reddit.com/r/LocalLLaMA/comments/1ojpfwl/mlx_added_support_for_mxfp8_and_nvfp4/)
- I dont think native fp4 supportwill come until m6 or m7. M5 didnt have fp4 or fp8 accelerators. maybe m5 max will have dedicated fp8 support, if not then m6

- ## 🔧 [There is a space on HF where you can convert models to MLX without downloading them : r/LocalLLaMA _202503](https://www.reddit.com/r/LocalLLaMA/comments/1j3k8o8/there_is_a_space_on_hf_where_you_can_convert/)
  - Well I just learned that there is a space on HF where you can convert models, you just enter the model name and the quant and it uploads it straight to your HF profile! No need to download or do anything at all. This also means I'm not limited by my ram, I can convert any model now and so should you :)
  - https://huggingface.co/spaces/mlx-community/mlx-my-repo

- ## [Best Local LLM for MacBook Air M3 with 24GB RAM : r/LocalLLaMA _202404](https://www.reddit.com/r/LocalLLaMA/comments/1bu65s6/best_local_llm_for_macbook_air_m3_with_24gb_ram/)
- Rough rule of thumb is 2xParam Count in B = GB needed for model in FP16.
  - From there reducing precision scales more or less linearly. 
  - So 1B param model = 1GB RAM needed INT8, or 0.5GB RAM needed INT4. 

- ## [Any experiences running LLMs on a MacBook? : r/LocalLLaMA _202507](https://www.reddit.com/r/LocalLLaMA/comments/1m1t19r/any_experiences_running_llms_on_a_macbook/)
- Pretty good experience on M4 Max with 128Gb, Qwen3-30B-A3B (8bit quants). Speed on small inputs is around 40-50 toks/s, which is very very usable.
  - I have the same setup I would say not very good. lol. But that’s because I try to use models for things like cline and opencode. It’s just soooo slow on initial prompt and even later on as well. For chats with 24b’s it’s great though
- I feel that almost any thinking models feel pretty slow in coding assistants. I would prefer them to answer faster with the same quality

- Qwen3-30B-A3B is the goat on my M3 Ultra (96 gb). I asked a few coding/ML questions, and I'm getting between 55 - 70 tok/s

- I get vastly better results with qwen3 32B in 4bit than qwen3 30B in 8bit. 

- Prompt: Write a binary search function in javascript
  - All models loaded w/ max context window, lm studio, mlx backend.
- M4 Max MacBook Pro 128GB (mostly 4bit):
  kimi-dev-72b-dwq: 11 tps
  qwen3-53b-a3b: 45tps
  qwen3-30b-a3b-dwq: 96tps
  devstral-small-2507-dwq: 33tps
  gemma-3n-e4b-it: 75tps
  jan-nank-128k (8bit): 90tps
  qwen3-4b-dwq-053125: 142tps
  qwen3-1.7b-dwq-053125: 252tps
- M2 MacBook Air 24GB:
  qwen3-30b-a3b (3bit): 32tps
  qwen3-4b-dwq-053125: 30tps
  qwen3-1.7b-dwq-053125: 66tps
  devstral-small-2507-dwq: 6tps
  gemma-3n-e4b-it: 25tps
  jan-nano-128k (8bit): 16tps
  jan-nano-128k (4bit): 31tps

- I have M4 pro with 48GB RAM. I can run local models maximum 32B (4/6Q). Gemma 3 27b/Qwen 3 32B is good enough to use for general QnA purpose. For dev assistance, it lacks accuracy and generation speed on Mac M4. I would choose R1 or else in Openrouter. However definitely battery runs out faster with local models.
  - i’d recommend giving devstral small a shot it’s surprisingly really good and punches above its weight.

- Get the pro and with as much unified memory as you can afford. I’m running a M4 Max with 64GB and I regret not getting the 128
  - you might want to increase the portion of unified memory allocated to the GPU
  - LM Studio has awful default settings when you download a model, always check online what are the model’s recommended settings (Unsloth blog or model pages on huggingface are great sources for this).
  - don’t just max out context length, set one that makes sense for your hardware. You can find calculators online, or resort to the good old trial and error process. Be aware that, even if models support 128k or more tokens in the context, most of them degrade after 40/50k.

- I wouldn't recommend fine tuning on Macs - took 9hrs to train phi 3 mini on the guanaco dataset with autotrain.

- ## [MacBook Air M4/32gb Benchmarks : r/LocalLLaMA _202503](https://www.reddit.com/r/LocalLLaMA/comments/1jklk5y/macbook_air_m432gb_benchmarks/)
  - Phi4-mini (3.8b)- 34 t/s, 
  - Gemma3 (4b)- 35 t/s, 
  - Granite 3.2 (8b)- 18 t/s, 
  - Llama 3.1 (8b)- 20 t/s, 
  - Gemma3 (12b)- 13 t/s, 
  - Phi4 (14b)- 11 t/s, 
  - Gemma (27b)- 6 t/s, 
  - QWQ (32b)- 4 t/s

- I suspect it's heating up quite a bit like my 24 gb one does
  - Sure does, being completely silent is a nice tradeoff though. My old MacBook Pro would sound like a jet engine preparing to take off.

- Those figures are close to what I'm getting using accelerated ARM CPU inference on a Snapdragon X1 Elite with 12 cores. That's on a ThinkPad with fans and big cooling vents. It's incredible that the M4 Air has that much performance in a fanless design.
  - It definitely gets warm when inferencing with the larger models and longer contexts but being completely silent is pretty amazing. Models tested were Q4.

- People are angry with the MacBook Air M4. Without fans, the benchmarks drop by half compared to the Mac Mini with the same M4 chip.

- [Tested local LLMs on a maxed out M4 Macbook Pro so you don't have to : r/ollama _202503](https://www.reddit.com/r/ollama/comments/1j0by7r/tested_local_llms_on_a_maxed_out_m4_macbook_pro/)
  - 测试了qwen2.5的各种量化版
  - lmstudio的mlx比ollama快很多

- ## ⚡️ [Is M4 MacBook Air 32 + 512 good for AI/LLM? : r/macbookair _202503](https://www.reddit.com/r/macbookair/comments/1jd2cbc/is_m4_macbook_air_32_512_good_for_aillm/)
  - Some preliminary benchmark tests show that the token per second is as follows in model M4 MBA 32 GB: 
  - 7b 20.8 token/s 
  - 14b 11.0 token/s 
  - 32b 4.9 token/s 
  - Is this acceptable or good enough for playing with local AI/LLM?

- deepseek-r114b on M4 is near 14 tokens but on the 4070 it is 50!!!
  - Then deepseek 32b does like 4.7 tokens on M4 32/512 and 5.7 on the 4070 ti.
  - For LLM running i'd go for the M4 PRO with more cores and 48gb ram but that configuration is like x2 expensive over the 32/512 M4

- The problem is LLM running locally are very CPU intensive. Which equals heat, which the Air has no internal fans to handle it, which equals the CPU throttling (under clocking) itself to prevent overheating. The AIR will get Hot AF!
  - The memory and storage is in the range of what is needed. Personally I would go for a 1TB of storage but you need something with a fan which would be a MacBook Pro or mini.

- The base M4 MBP would probably be best because of the active cooling, it’ll allow for better sustained performance and also comes with a slightly bigger battery.
- Pro model recommended so the active cooling system, the MacBook Air doesn’t handled loads well.

- ## [How are people running an MLX-compatible OpenAI API server locally? : r/LocalLLaMA _202508](https://www.reddit.com/r/LocalLLaMA/comments/1mg26g0/how_are_people_running_an_mlxcompatible_openai/)
- If you are on a Mac then LM Studio is about your only choice for a mature, stable, fast, reliable, supported, maintained MLX server.

- ## [Adjust VRAM/RAM split on Apple Silicon · ggml-org/llama.cpp _202307](https://github.com/ggml-org/llama.cpp/discussions/2182)
- just do: `sudo sysctl iogpu.wired_limit_mb=<mb>` from Terminal. You’d have to do it every boot as it’s not sticky

- ## 🤔 [MLX now has MXFP4 quantization support for GPT-OSS-20B, a 6.4% faster toks/sec vs GGUF on M3 Max. : r/LocalLLaMA _202508](https://www.reddit.com/r/LocalLLaMA/comments/1n4mxrj/mlx_now_has_mxfp4_quantization_support_for/)
- The speed increase is pretty noticeable, tested with short prompts, on M4 MAX 128GB
  - mlx-community's gpt-oss-120b-MXFP4-Q8: 80tps
  - ggml 120b: 75tps, with fa enabled
  - unsloth 120b f16: 61tps, with fa enabled
- Agree with your observation, the new gpt-oss-120b-MXFP4-Q8 that was released just several days ago is indeed faster by ~25% based on my testing than the unsloth full precision (fp16) - even full FA enabled. Quality appears to be the same, because it doesn’t really matter Q8 or fp16 for that model, as 95% of the params were trained with native MXFP4 “full precision”, that is why also all unsloth quants and MLX Q4 and Q8 weights almost the same!

- it’s still has to be software optimisation right since M series chip doesn’t natively support this quantization

- ## [Upcoming MLX support news? : r/unsloth _202508](https://www.reddit.com/r/unsloth/comments/1mlsoar/upcoming_mlx_support_news/)
- will there be UD MLX quants?
  - Oh maybe if demand is more!

- That would be so amazing! Love unsloth quants and I always feel like I need to make a tough choice between them and MLX ones. 

- ## 🍎 [Apple users: Unsloth's quants could be coming to MLX - if we show interest : r/LocalLLaMA _202508](https://www.reddit.com/r/LocalLLaMA/comments/1moqhvf/apple_users_unsloths_quants_could_be_coming_to/)
- Mac user.  I would be very interested to see how they could benefit the MLX community.  
  - I highly respect Llama.cpp and GGUF but MLX DWQ quants are very high quality and faster than their GGUF cousins on this hardware. I find myself unwilling to go back unless I have to.  Thankfully MLX support, unless first party, often comes faster than Llama.cpp so we have been well served.
- Last I heard the performance delta was <10%. Id much prefer them just supporting the llama.cpp ecosystem rather than diluting their time
  - Then you've heard a while ago because the performance delta is huge now. I get 16t/s on MLX and 9t/s on llama.

- Would very much like to run unsloth dynamic mlx quants on my mac studio

- That would be amazing! MLX is great but still lack the support of other inference engines imo.

- ## 🤔 [MLX you're using in release LM Studio seems to be outdated and broken for Q8 and larger models · Issue · lmstudio-ai/mlx-engine _202411](https://github.com/lmstudio-ai/mlx-engine/issues/34)
- The next version of our app should help remedy this, since we'll be shipping the latest version of MLX.

- The guidance is incomplete and solves nothing. The correct kernel tweaks to make these work are actually:
  - Without the `disable_wired_collector` setting, the problem remains.

```sh
sudo sysctl iogpu.disable_wired_collector=1
sudo sysctl iogpu.wired_limit_mb=n
```

- To make these persistent across reboots:
  - [Persistent sysctl Settings - Apple Community _202204](https://discussions.apple.com/thread/253840320?sortBy=rank)

- ## 💡 [Run LLMs on macOS using llm-mlx and Apple’s MLX framework | Lobsters _202502](https://lobste.rs/s/1reyhf/run_llms_on_macos_using_llm_mlx_apple_s_mlx)
  - By default, MacOS allows 2/3rds of this RAM to be used by the GPU on machines with up to 36GB / RAM and up to 3/4s to be used on machines with >36GB RAM.

- I haven’t tried mlx the library yet, but when I was using LM Studio with their MLX backend, I had to run `sudo sysctl iogpu.wired_limit_mb=<something>` to increase the VRAM limit.
  - However, be aware that the system would panic when you try to load a big model or use a large context size when `<something>` is too big.

- By the way, I found that if you have models in` ~/.cache/huggingface/hub` already, due to having used mlx-lm directly, the llm mlx download-model mlx-community/… command will skip the download and just add them to llm’s index.

- When comparing popular quant q4_K_M on Llama.cpp to MLX-4bit, in average, MLX processes tokens 1.14x faster and generates tokens 1.12x faster. This is what most people would be using.

- ## [Can't run Mixtral on GPU with M2 Pro 32 gb VRAM : r/LocalLLaMA _202312](https://www.reddit.com/r/LocalLLaMA/comments/18l9kal/cant_run_mixtral_on_gpu_with_m2_pro_32_gb_vram/)
  - I was able to run Mixtral Q5 on my macbook on CPU, but when I choose Apple Metal (GPU) in LM Studio I get this error:
  - GGML Metal Error: command buffer 4 failed with status 'Error'. Insufficient Memory (00000008:kIOGPUCommandBufferCallbackErrorOutOfMemory)
  - Worked for Q4_K_M when increasing the VRAM limit

- Gpu only has access to about 22gigs on a 32gig macbook, check the Llama.cpp or this community for a thread where setting a few command line arguments disables this limit.

- By default you can have up to 22GB of RAM allocated to the GPU but you can increase that amount up to 29GB with the system running fine. Try 27-28GB if you want to run a web browser on the side. In the terminal type the following (mb=0 to reset to default settings):
  - sudo sysctl iogpu.wired_limit_mb=29256
  - sudo sysctl iogpu.wired_limit_mb=0
  - You’d have to do it every boot as it’s not sticky .
- 32GB might be too tight for 32k ctx and would usually crash the machine. 12k ctx seems to be the limit for 32GB.

- Why no one talks about the new ml framework mlx from apple? Is it not applicable here?
  - It would hit the same limit that a q5 quant of dolphin-mixtral needs more GPU memory than can be allocated on a 32GB Mac, even after tweaking the kernel limit.

- ## 🧩 [First time using MLX and MacOS for inference: getting poor results : r/LocalLLaMA _202409](https://www.reddit.com/r/LocalLLaMA/comments/1fpy26p/first_time_using_mlx_and_macos_for_inference/)
- Set sysctls `sudo sysctl iogpu.wired_lwm_mb=400000 && sudo sysctl iogpu.wired_limit_mb=150000` , reboot
- iogpu.wired_limit_mb=150000 sets the maximum amount of wired memory the GPU is allowed to allocate to 150, 000 MB (~150 GB)
  - sets the maximum GPU memory allocation to 150GB
- iogpu.wired_lwm_mb=400000 sets the low-water mark (LWM) for the GPU’s wired memory to 400, 000 MB (~400 GB).
  - In memory management, a low water mark typically represents a threshold. When the amount of free memory drops below this mark, the system might take certain actions to free up more memory.

- iogpu.disable_wired_collector=1
  - tells macOS to disable the “wired memory collector” for the GPU.
  - Normally, the collector periodically trims/reclaims GPU wired memory (VRAM allocations backed by unified RAM) when the system is under pressure.
  - Disabling it (=1) means the GPU can hold onto large wired allocations without the OS trying to recycle them. This is sometimes done when running ML/LLM workloads on Apple Silicon, because the collector can otherwise kill big GPU allocations and crash jobs.
  - Setting this to 1 disables this collector, potentially leaving GPU memory allocations "locked" and unadjusted even when the system needs memory.

- MLX is lazy so it won't load models until it needs to. So the time-to-first-token should be a lot lower on the second request.

- Run the command to expand the max VRAM allocation (needs to be done after each reboot):
  - sudo sysctl iogpu.wired_limit_mb=120000

- ## [Can the iogpu.wired_limit_mb setting on MacOS be persisted? 📣 YES! : r/LocalLLaMA _202405](https://www.reddit.com/r/LocalLLaMA/comments/1cncgqe/can_the_iogpuwired_limit_mb_setting_on_macos_be/)
- Can CPU intensive, RAM demanding tasks take RAM seemlessly when not running GPU inference?
  - Yes, this sets the higher limit. Clearly the problem is that under heavy load, GPU will take it all leaving just 8GB to the other apps and OS.

- 设置sysctl并执行

```sh
sudo mv io.github.sysctl.plist /Library/LaunchDaemons/
sudo chown root:wheel /Library/LaunchDaemons/io.github.sysctl.plist
sudo launchctl load /Library/LaunchDaemons/io.yaoo.sysctl.plist
```



```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
<dict>
 <key>Label</key>
 <string>io.github.sysctl</string>
 <key>ProgramArguments</key>
 <array>
 <string>/usr/sbin/sysctl</string>
 <string>-w</string>
 <string>iogpu.wired_limit_mb=27648</string>
 </array>
 <key>RunAtLoad</key>
 <true/>
</dict>
</plist>

```

- Rather than dealing with plist syntax, add `iogpu.wired_limit_mb=122800` on a line by itself to `/etc/sysctl.conf`. Create the file if it doesn't already exist. It should probably be owned by `root:wheel` and mode should be 644.

- ## 💡 [M1/M2/M3: increase VRAM allocation with `sudo sysctl iogpu.wired\_limit\_mb=12345` (i.e. amount in mb to allocate) : r/LocalLLaMA _202311](https://www.reddit.com/r/LocalLLaMA/comments/186phti/m1m2m3_increase_vram_allocation_with_sudo_sysctl/)
  - One note on this ... All macos systems would be happiest to have at least 8gb available for OS stuff.
  - this is not a permanent change and it automatically resets on reboot.
  - PS: to get the current value use: sudo sysctl iogpu

- I looked at what wired memory (memory that can't be swapped) was without having an LLM loaded/running and then added a margin to that. I ended up allocating 26.5GB, up from 22.8GB default.
  - It worked, but it didn't work great because I still had a bunch of other stuff running on my Mac, so (not surprisingly) swapping slowed it down. For anything more than a proof of concept test I'd be shutting all the unnecessary stuff down.

- On my 32GB Mac, I allocate 30GB. [Macs with 32GB of memory can run 70B models with the GPU. : r/LocalLLaMA](https://www.reddit.com/r/LocalLLaMA/comments/18674zd/macs_with_32gb_of_memory_can_run_70b_models_with/)
  - That's what I do and I have no swapping at all. I listed the two big things to turn off to save RAM. 
  - I don't use the GUI. Just simply logging in and doing nothing uses a fair amount of RAM. I run my Mac headless. I ssh in.
  - I stopped the `mds_stores` process from running

- consider llama.cpp instead of LM Studio to reduce RAM requirements a bit (still need to run terminal.app but this is pretty light)

- As per the latest developments in that discussion, "iogpu.wired_limit_mb" only works on Sonoma. So if you are on an older version of Mac OS, try "debug.iogpu.wired_limit" instead.

- How can I check if the changed worked? I did the intial code and said it was initially set to 0
  - One way I've verified is through the llama.cpp diagnostic output. It reports the available vram as well as the size of the model and how much vram it requires.
  - I've got 32gb total and I think the default availability is approx 22gb. So I can easily increase to 26gb and I see the difference immediately when I launch llama.cpp - the available vram will be reported as 26gb.

- ## 💡 [Macs with 32GB of memory can run 70B models with the GPU. : r/LocalLLaMA _202311](https://www.reddit.com/r/LocalLLaMA/comments/18674zd/macs_with_32gb_of_memory_can_run_70b_models_with/)
  - I recently got a 32GB M1 Mac Studio. I was excited to see how big of a model it could run. It turns out that's 70B. It is a Q3_K_S model so the 2nd smallest for 70B in GGUF format
  - Mac shouldn't be able to dedicate that much RAM to the GPU. Apple limits it to 67%, which is about 21GB. This model is 28GB. So it shouldn't fit. But there's a solution to that thanks to these smart people here.
  - This new method is just setting the value of a variable. llama.cpp even tells you the value, how much RAM, it needs.
  - > sudo sysctl iogpu.wired_limit_mb=57344 ( I did that for my 64GB, you'd want to change the 57344 )

- ≥64GB allows 75% to be used by GPU. ≤32 its ~66%. Not sure about the 36GB machines.

- I also do these couple of things to save RAM.
  - I don't use the GUI. Just simply logging in and doing nothing uses a fair amount of RAM. I run my Mac headless. I ssh in.
  - I stopped the mds_stores process from running. I saw that it was using up between 500MB and 1GB of RAM. Its the processes that indexes the drives for faster search. 
  - With all that set, the highest I've seen in use memory is 31.02GB while running a 70B Q3_K_S model. So there's headroom. 

- You may try and run one of Q4 models without problems: because llama.cpp uses mmap to map files into memory, you can go above available RAM and because many models are sparse it will not use all mapped pages and even if it needs it, it will swap it out with other pages on demand... I was able to run falcon-180b-chat. Q6_K which uses about 141GB on a 128GB Windows PC with less than 1% SSD reads during inference... I could even run falcon-180b-chat. Q8 which uses about 182GB but in this case SSD was working heavily during inference and it was unbearably slow (0.01 tokens/second)...
  - Yes. I've done that before on my other machines. Llama.cpp in fact defaults to that. The hope for me was that since the models are sparse that the OS would cache the relevant parts of the models in RAM. So the first run through would be slow but subsequent runs would be fast since those pages are cached in RAM. 

- ## 🧠 [Instantly allocate more graphics memory on your Mac VRAM Pro : r/LocalLLaMA _202504](https://www.reddit.com/r/LocalLLaMA/comments/1k1tdpa/instantly_allocate_more_graphics_memory_on_your/)
  - I built a tiny macOS utility that does one very specific thing: It unlocks additional GPU memory on Apple Silicon Macs.
  - Why? Because macOS doesn’t give you any control over VRAM — and hard caps it, leading to swap issues in certain use cases.
  - Do you need this app? No! You can do this with various commands in terminal. But wanted a nice and easy GUI way to do this.

- https://github.com/Sub-Soft/Siliv /NALic/202504/python
  - A simple macOS menu‑bar utility to adjust Apple Silicon GPU VRAM allocation
  - Siliv provides a convenient way to view and set GPU VRAM allocation on Apple Silicon Macs via `sysctl` .
  - Persistence: `sysctl` changes may reset after reboot; 

- 🤔 did you know that MLX ignores the VRAM limit global? do you know a way to make MLX use the extra VRAM allocated?
  - If you're on MacOS 15 or higher: Just run `sudo sysctl iogpu.wired_limit_mb=14336` on the terminal and replace 14336 (14GB) with your desired VRAM allocation in MB
- That's the global I use, and MLX ignores what's set for it. Using LM Studio, I can load and use q8 quants of 70B ggufs, but MLX models the same size, run out of memory.

- don't bother, this app just does this: `sudo sysctl iogpu.wired_limit_mb=24576`.
  - Yeah I already have a version of this aliased in my .zshrc file whenever I feel I need it (or to reset). 
  - Dont work , its a very old command for intel igpus ... 

- ## 🚀 [LM Studio ships an MLX backend! Run any LLM from the Hugging Face hub on Mac blazingly fast! ⚡ : r/LocalLLaMA _202410](https://www.reddit.com/r/LocalLLaMA/comments/1fz6z79/lm_studio_ships_an_mlx_backend_run_any_llm_from/)
- M1 Max 32GB, Qwen2.5-14B-Instruct
  - Q4_K_M: 15.15 t/s
  - 4 bit MLX: 23.10 t/s

- M2 Max 64GB, Qwen2.5-32B-Instruct
  - Q4_K_M: 14.78 tok/sec
  - 4 bit MLX: 17.62 tok/sec

- One bonus from MLX I hadn't anticipated but is nice is not the speed difference, but the VRAM savings
  - Running on an M2 Ultra Mac Studio 192GB Ram.
  - mlx-Llama-3.1-70B-Instruct-8Bit - 82GB RAM/VRAM used - 53 Watts Peak Power - 8.62 tk/s
  - Llama-3.1-70B-Instruct-GGUF Q8_0 - 123.15GB RAM/VRAM used (Flash Attention enabled) - 53.2 Watts Peak Power - 8.2 tk/s
- Yes, this! Plus (potentially in a future LMStudio update) with the circular buffer + infini cache, it means we can fit much stronger models in and not worry about memory footprint increases with conversation length! I can finally get 8bit 70b models comfortably in my 64gb and use them all the way up to the 100k token limit 

- just FYI the reduction in VRAM is because MLX doesn't pre-allocate memory, whereas llama.cpp does.
  - Simple calculation: Model size at Q8 is ~75 GB, KV cache for 128k context is 40GB
  - Required memory to load the model and fill the cache is at least 75+40 = 115 GB.
