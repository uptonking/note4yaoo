---
title: lib-ai-app-community-model-toolchain
tags: [community, large-language-model, toolchain]
created: 2025-09-16T12:35:55.935Z
modified: 2025-09-16T12:36:12.968Z
---

# lib-ai-app-community-model-toolchain

# guide

- model with UD(unsloth dynamic quants)

- models-config
  - 大模型的测试经常需要修改参数，支持一键恢复默认配置更好

- tips-ai-tools
  - lm studio底层用的也是llama.cpp, 不必寻找替代，深入底层更容易替代和扩展

- mlx
  - mlx的优点之一是方便支持在iphone上运行

- ollama-pros
  - stable and rich models
  - 对 embedding 模型额支持更好

- ollama-cons
  - 对 mlx 模型的支持落后

- lmstudio-pros
  - ui操作体验友好

- lmstudio-cons
  - 对mlx格式的 embedding 模型额支持有问题, 但gguf格式模型支持好
# lmstudio-xp
- not-yet
  - 聊天内搜索
  - 标题名搜索，便于查看包含某关键字的chats

- 
- 
- 
- 

# discuss-stars
- ## 

- ## 

- ## 

- ## [Is Q8 KV cache alright for vision models and high context : r/LocalLLaMA](https://www.reddit.com/r/LocalLLaMA/comments/1py4xp6/is_q8_kv_cache_alright_for_vision_models_and_high/)
- I don't have a mathematical evidence, but with KV at Q8 in all my cases qwen3 Vision couldn't do any tasks correctly in browser use cases with very low consistency, the same for picture tagging and descriptions.
  - The difference when observing logs is accuracy, where the model interprets small differences in inputs so differently they give the wrong outcome in terms of tool calls.

- Ruins the output even at a really short context (with gemma-3, pixtral-large, qwen2-72b-vl)

- I cant say anything about vision models as i haven't tested but when it comes to kv cache and llm's i never go below fp 16 because lowering the precision wrecks it. seems that trend would transfer over as well. but who knows maybe someone here sees things differently after experiments..

- ## 🏠 [Scaling with Open WebUI + Ollama and multiple GPUs? : r/LocalLLaMA _202510](https://www.reddit.com/r/LocalLLaMA/comments/1o9ssqd/scaling_with_open_webui_ollama_and_multiple_gpus/)
  - At our organization, I am in charge of our local RAG System using Open WebUI and Ollama. So far, we only use a single GPU, and provide access to only our own department with 10 users. Because it works so well
  - The final goal will be to provide all our around 1000 users access to Open WebUI (and LLMs like Mistral 24b, Gemma3 27b, or Qwen3 30b, 100% on premises).
  - To provide sufficient VRAM and compute for this, we are going to buy a dedicated GPU server, for which currently the Dell Poweredge XE7745 in a configuration with 8x RTX 6000 Pro GPUs (96GB VRAM each) looks most appealing atm.
  - However, I am not sure how well Ollama is going to scale over several GPUs. Is Ollama going to load additional instances of the same model into additional GPUs automatically to parallelize execution when e.g. 50 users perform inference at the same time? Or how should we handle the scaling?
  - Would it be beneficial to buy a server with H200 GPUs and NVLink instead?

- Instead of complicating and getting overkill hardware, just check and learn out vLLM. Its much suitable for these usecases.
  - yep vLLM just `--data-parallel-size 8` out the entire system, and works well with Ray cluster so it has internal model router and LB for multiple model. and it has KV store backend, so multiple GPU can access the same already compute KV Cache
  - although you can use NGINX as model router (as in api router, not internal of MoE model)

- We just went through this exact scaling problem at Anthromind - started with one GPU for our internal team, then had to figure out multi-GPU serving when other departments wanted in. Ollama doesn't automatically parallelize across GPUs the way you're thinking.. it'll load one model instance per GPU but won't split a single request across multiple cards.
  - For 1000 users you're gonna need to run multiple ollama instances behind a load balancer, each managing different GPUs. 
  - The H200s with NVLink would be overkill for just inference honestly - those RTX 6000s should handle it fine if you set up proper request routing. 
  - We ended up using a simple nginx setup to distribute requests across ollama instances, each pinned to specific GPUs.

- I use LiteLLM to distribute my LLM requests to different ollama instances, running on different servers. This will solve your scaling challenge of the GPU. Also make sure, your embedding is also using a LLM instance, afaik default is cpu embedding in openweb zu instance

- Maybe vllm or sglang with some load balancer, although a single RTX 6000 Blackwell may have enough FLOPS for 50 concurrent requests.

- ## [What is your primary reason to run LLM’s locally : r/LocalLLaMA](https://www.reddit.com/r/LocalLLaMA/comments/1nsjwv1/what_is_your_primary_reason_to_run_llms_locally/)
- For me, it is independence from Big Tech and venture capital. Open weight models can never be taken away from us.

- New open weight models come out like every week and I want to be able to try the ones that can can run on my PC without waiting for a subscription service to add them or paying per use.

- ## 🆚 [what is the bottom line difference between GGUF and FP8? : r/comfyui _202512](https://www.reddit.com/r/comfyui/comments/1pu6t8e/what_is_the_bottom_line_difference_between_gguf/)
  - You should ask about regular FP8, scaled FP8, and mixed FP8, instead of comparing it to GGUF because those FP8 differences can affects the quality/accuracy vs the base BF16 model.
  - Even FP8_e4 vs FP8_e5 can generates a different things on the same prompt & seed.
  - Meanwhile, GGUF are designed for low VRAM with the ability to offload some part of it on RAM/CPU.

- [Comparison of Qwen-Image-Edit GGUF models : r/StableDiffusion](https://www.reddit.com/r/StableDiffusion/comments/1my3lq0/comparison_of_qwenimageedit_gguf_models/)
  - Based on those result FP8 is close to Q4_K_M

- so what is the difference between fp8 and scaled fp8 (have not come across weights labeled mixed fp8 yet)?

- FP8 (8-bit Floating Point): Uses 8 bits divided into a sign, exponent, and mantissa. It is a "native" format for modern GPUs (RTX 40-series and newer), meaning the hardware can do the math directly in this format without converting it first.
- GGUF (e.g., Q5/Q6): These use integer-based quantization with "K-quants" (block-wise scaling). The model is broken into small blocks, and each block has its own scaling factor. This allows Q5 (5-bit) or Q6 (6-bit) to often retain more intelligence than a simple 8-bit float because it "allocates" precision more intelligently where it's needed most.
- does it mean we should go for G8 over FP8 if we can, considering they're around the same size? I mean, if G5/G6 is better than FP8, then G8 should be even better, right?
  - yes

- from my personal experience, i'd go for a higher precision gguf over an fp8… i can't give u a technical explanation, but i think in a like for like quants, the gguf is a better option.
  - It may be better Quality but it will likely be a lot slower, as thats how .gguf works.

- there's no real difference between an fp8 safetensor and a Q8 gguf except that your gpu might natively accelerate the fp8. A gguf will unpack to the native data type your gpu supports (bf16/fp16/fp32). So that unpacking is negligible but not insignificant.

-Depends on your GPU if it's 40xx or 50xx series with fp8 native acceleration fp8 is better (at lest for Wan 2.2 and ZiT), despite the model being over your VRAM it would be faster. If you're with older Nvidia card Q8 and Q6 are faster. I've done tests on RTX 3060 12GB and 5070ti... and 5070ti is faster with the fp8 models. 

- ## 🧩 [The difference between quantization methods for the same bits : r/LocalLLaMA _202307](https://www.reddit.com/r/LocalLLaMA/comments/159nrh5/the_difference_between_quantization_methods_for/)
  - Using GGML quantized models, let's say we are going to talk about 4bit
  - I see a lot of versions suffixed with either 0, 1, k_s or k_m
- [k-quants · Pull Request · ggml-org/llama.cpp _202306](https://github.com/ggml-org/llama.cpp/pull/1684)

- K-quantization options are labeled "S", "M", and "L" and stand for small, medium, and large model sizes, respectively. 
  - Option "0" represents baseline quantization without extra calibration. 
  - In terms of quality and speed: 0 (lowest quality, fastest speed) < S < M < L (highest quality, slowest speed).

- k models are k-quant models and generally have less perplexity loss relative to size. A q4_K_M model will have much less perplexity loss than a q4_0 or even a q4_1 model.
- Generally, the K_M models have the best balance between size and PPL, so q3_K_M, q4_K_M, q5_K_M, etc. I like q5, and q4 best usually. 

- Aside from the number of bits per weight in a scaling group being obvious, here are the main differences:
  - Type _0 compression gives each group of weights a shared scale, but they are "symmetric" weights about 0. Type _1 weights add in a "bias" - an offset for each group of weights which allows them to be better resolved if they are mainly shifted away from zero. Type K is an enhancement in the way hierarchal groups are encoded to squeeze a little more compression into the mix. Finally, after the K we now have nothing, M, S and L variants - these actually refer to which tensors have the base precision. In the K_S models, all weight tensors have the stated precision. The simple K, K_M and K_L models specify varying amounts of weight tensors that will actually use higher precision to improve accuracy, typically 4-6 bits. This will no doubt keep expanding over time. Note that the PR referred to by u/lemon07r also contains descriptions of all the formats.

- With the older quantisation method, 4_0 is 4.5 bits per weight and 4_1 is 5 bits per weight.
  - The K quantisation methods are newer. Hopefully, they will get slightly better accuracy for roughly the same file size compared to the old methods.
- That’s not correct. You will get the best speed with q4_K_S oder q4_K_M. This is because 3-bit and 2-bit needs more calculations.
  - If memory bandwidth is your bottleneck and not processor speed, then smaller is faster.

- [Is IQ4_XS closer to Q4 or Q3 in terms of quality? : r/LocalLLaMA _202512](https://www.reddit.com/r/LocalLLaMA/comments/1pk1zpq/is_iq4_xs_closer_to_q4_or_q3_in_terms_of_quality/)
- it was accepted that IQ4_XS beat all Q3 quants, as well as the legacy Q4_0 quants. Bartowski has a table on every model that he uploads where he mentions that IQ4_XS is comparable in quality to Q4_K_S but smaller.

- All IQ4_XS I've tried were worse than Q4_K_M at creative writing.

- i1 means imatrix, IQ is the quantization type you are asking about, don't mix these concepts up. You can see that anything about about 5 bits with imatrix is getting quite close to max possible accuracy, and imatrix IQ4_something is very good as well.

- ## [AMA with the Unsloth team : r/LocalLLaMA _202509](https://www.reddit.com/r/LocalLLaMA/comments/1ndjxdt/ama_with_the_unsloth_team/)
- What’s your go-to quant for most models? I usually pick Q4_K_XL dynamic, but if I have enough VRAM, is there another Q4 you’d recommend for better accuracy?
  - Yes correct, usually always got for the K_XL quants as they have the best ratios in terms of accuracy/speed/size etc 
  - My goto is probably Q3_K_XL as my laptop is incapable of handling anything larger

- 🍎 Do you plan to support Apple/MLX?
  - Yes definitely, it has been a super high request and we know there are soooo many Mac users out there so we'd be silly to not to. As for when, mmm to be honest maybe late this year? Unfortunately we are team constrained at the moment

- Any plannings on the TPU full integration?
  - It is possible yes but probably after MLX/AMD/Intel etc first
- I think they have it in the roadmap but I do not think anytime soon. I think it would be better for Unsloth if they are support Apple/MLX first and then TPU
  - Yes, AMD/Intel/ MLX will come first then TPU

- I’d like to use your model in a distributed llama cluster using all my old computer at home. Any planning?
  - We support multiGPU which might help with your setup but won't be officially announcing multigpu until maybe later this year as it's not up to the standard we would like!

- 
- 

- ## [Poor performance qwen3 235B 2507 mlx vs. unsloth variant : r/LocalLLaMA _202508](https://www.reddit.com/r/LocalLLaMA/comments/1mj7m20/poor_performance_qwen3_235b_2507_mlx_vs_unsloth/)
  - I just downloaded the Qwen3 235B 2507 instruct model for LmStudio on a M2 studio ultra. 
  - I got the MLX 4bit and Unsloth q4_0 versions. 
  - I am getting very low generation speeds on the MLX version ~0.3 tokens/s while on the other hand I am getting ~27 tokens/s on the Unsloth variant.

- Unsloth is highly optimized with advanced quantization for massive models, while MLX is known to have performance issues with models larger than ~22B parameters, which explains the speed difference you're seeing.
  - Where can I read more about MLX having problems with >22B parameters? First time hearing about it

- For unsloth would recommend q3_k_xl or q4_k_xl, should be more accurate than simple q4_o quant… MLX should be faster, maybe the full model is not loaded to GPU?
  - Thanks. I double checked if all layers were loaded onto the GPU and that's the case, so I don't know what is the problem

- [Performance Qwen3 30BQ4 and 235B Unsloth DQ2 on MBP M4 Max 128GB : r/LocalLLaMA _202504](https://www.reddit.com/r/LocalLLaMA/comments/1kbacf2/performance_qwen3_30bq4_and_235b_unsloth_dq2_on/)
  - I was wondering what performance I could get out of the Mac MBP M4 Max 128GB
  - LMStudio Qwen3 30BQ4 MLX: 100tokens/s
  - LMStudio Qwen3 30BQ4 GUFF: 65tokens/s
  - LMStudio Qwen3 235B USDQ2: 2 tokens per second?
  - So I tried llama-server with the models, 30B same speed as LMStudio but the 235B went to 20 t/s!!! So starting to become usable

- ## 🆚 [MLX vs. UD GGUF : r/LocalLLaMA _202505](https://www.reddit.com/r/LocalLLaMA/comments/1kpqrzz/mlx_vs_ud_gguf/)
- I benchmarked Unsloth's Qwen3-30B-A3B Dynamic 2.0 GGUF against the MLX version. Both models are the 8-bit quantization. Both are running on LM Studio with the recommended Qwen 3 settings for samplers and temperature.
  - MLX: 3, 516 tokens generated, 1.0s to first token, 70.6 tokens/second
  - UD GGUF: 3, 321 tokens generated, 0.12s to first token, 23.41 tokens/second
  - This is on an MacBook M4 Max with 128 GB of RAM, all layers offloaded to the GPU.

- UD q8 xl is not efficient for Mac. Use normal q8_0

- Isn't the entire point of using the UD XL GGUF for higher quality responses? If you were comparing for speed alone why not use the normal Q8 GGUF?
  - UD also uses less VRAM. I was hoping if it was comparable in speed, UD would be more resource efficient.
- They use less vram than 16 bit, not 8 bit. The goal is better accuracy through selective quantization so it should use more memory than standard q8. This is also why there’s XL in the name.

- Turn on flash attention if you haven’t. I wish I could use MLX, it it faster but the output by comparison was worse by a margin I’ve never seen before between the formats. I have an M1 ultra 64gb. It’s even worse with Qwen3 32B

- In my experience MLX is only marginally faster, less than 10% usually; it has an edge when it comes to speculative decoding, though.

- ## 🤔 [Genuine question: Why are the Unsloth GGUFs more preferred than the official ones? : r/LocalLLaMA _202505](https://www.reddit.com/r/LocalLLaMA/comments/1ksw070/genuine_question_why_are_the_unsloth_ggufs_more/)
- They often write "getting started" blog posts along with their quants of popular models where they share insights. That's valuable to newcomers. 

- They waste their time on stuff so you don't have to. When some meta data is wrong or a model outputs gibberish for some reason, they check it out and update it with a fix. The other top uploaders aren't bad either and do the same I imagine if an issue get raised. But random uploaders, who knows. And the official model creators do weird shit on their uploads like require login tokens on HF because they don't want you to download from them.

- There was a nicely done test recently that showed that they (quants by unsloth, bartowski, mrademacher) are all good. There is no clear winner. 
  - However, the "official" quants were often released without imatrix or broken / different in some other way. That's why those unofficial quants are usually preferred.
  - Also, unsloth made large MoE models usable on non-server machines with their dynamic Q2_XXS quants.
- The biggest difference I would say isn't the quants, but rather our bug fixes for every model
# discuss-model-speed ⚡️
- resources
  - [LocalScore - Local AI Benchmark](https://www.localscore.ai/)
    - LocalScore is an open benchmark which helps you understand how well your computer can handle local AI tasks.

- ## 

- ## 🆚 [When should you choose F16 over Q8_0 quantization? : r/LocalLLaMA _202512](https://www.reddit.com/r/LocalLLaMA/comments/1q0ci23/when_should_you_choose_f16_over_q8_0_quantization/)
  - We've all read about how Q8_0 is "virtually indistinguishable" from F16 when doing inference.

- Every time I download native safetensors I'm amazed at just how good my Q4KL was the entire time. I don't ever recall being impressed by Q8 or BF16 over Q4KL.

- If it's a VLM I will choose F16, if it's text only model - Q8.
  - VLMs in higher precision have significantly better image understanding and bounding box accuracy.
- Do you mean the `mmproj`-part should be f16? Or also the LLM part?
  - I personally found a lot of success with even harsh quantization of the base model, but unquantized vision encoder, without much degradation in image understanding personally.
- I can't upvoter this enough. In llama.cpp I found huge accuracy improvements for some of my use cases by swapping the mmproj file to the F16 or F32 version, and increasing the number of tokens generated from each image. With those tweaks I can get away with running Qwen3-VL 8b instead of a much larger VL model. Especially when I'm using it as part of an agent system to just handle visual descriptions and letting another larger text only LLM handle final analysis and writing. This lets me balance my local agent deployments better and get much better token rates with almost no loss of analytical quality.

- PDE stuff is often done in FP64
  - Highly recurrent/compounding math, such as interest rate calculations or number theory, is often done in higher than 64 but such as 128 bit, 512 bit or 1024 bit etc

- In Agentic Coding you will ALWAYS see differences between FP16 and Q8.

- Got-oss should be left at f16 since it’s already quantized
  - Vision encoders should also be left at f16
  - Otherwise q8 is great and even q4kl is very good.

- ## [Most used models and performance on M3u 512 gb : r/LocalLLaMA _202511](https://www.reddit.com/r/LocalLLaMA/comments/1ouogiq/most_used_models_and_performance_on_m3u_512_gb/)
  - Overall GLM 4.6 is queen right now.
- Model: GLM 4.6
  - Token Gen speed: generally 10-20
Use Case: vibe coding (slow but actually can create working software semi-autonomously with Cline); creative writing; expository/professional writing; general quality-sensitive use
PP Speed: 4 bit MLX 50-70 t/s at large context sizes (greater than 40k)
- Model: Kimi K2 thinking
  - Token gen speed: 3ish to 2
Use case: idk it's just cool having a huge model running local. I guess I will use it for brainstorming stuff, medical stuff, other questionable activities like academic writing. PP speed/context size is too limited for a lot of agentic workflows but it's a modest step above other open source models for pure smarts
PP speed: Q3 GGUF 19 t/s (26k context) faster with lower context; 
- Model: Minimax-m2
  - Token gen speed: 40-50 at modest sizes
Use case: Document review, finance, math. Like a smarter OSS 120.
PP Speed: MLX 4 bit 3-400 at modest sizes (10k ish)
- Model: GPT-OSS-120
  - Token gen speed: about 80 at medium context sizes
Use case: Agentic searching, large document ingesting; general medium-quality, fast use
PP speed: 4 bit MLX near 1000 at modest context sizes. But context caching doesn't work, so has to reprocess every turn.
- Model: Deepseek 3.1:
  - Token gen speed: 3-20 depending on context size
Use case: Used to be for roleplay, long context high quality slow work. Might be obsoleted by glm 4.6... not sure it can do anything better
PP Speed: Q3 GGUF: 50 t/s

- I’m ngl 4.6 running around 10-20tps is kinda disappointing for a $10k+ computer when you can run the same model on cpu for 2-3tps on a $1500~ ddr5 rig (pre price jump).
  - Don't get me wrong I’d still love those speeds, but idk if that’s worth spending an extra $500 per token in extra speed (at least for my use case); definitely reshapes my perspective of everything.
  - if the main reason of buying an expensive computer is to run big models faster, it’s a valid metric; how much value are you getting out of a $10k computer when a computer at 10% of the cost can do the same thing, just barely slower. I’d want to see at least 30-40tps out of a $10k computer.

- For comparison 12 3090 gets me 12k prompt processing with VLLM and 20 tokens per second for GLM and Minimax.

- ## [M2 Ultra Mac Studio with 64GB RAM and Ilama3.1 70b : r/ollama _202410](https://www.reddit.com/r/ollama/comments/1g0gycc/m2_ultra_mac_studio_with_64gb_ram_and_ilama31_70b/)
- I have M3 Max with 64 GB RAM and it can handle 70B (4 bit quantized) models. However, in my case, inference with 70B models isn’t at a comfortable speed.
  - Here’s the benchmark for Qwen2.5:72B with Ollama and MLX-ML:
  - • MLX (mlx-community/Qwen2.5-72B-Instruct-4bit): 8.14 t/s
  - • Ollama (Qwen2.5:72B): 6.95 t/s
  - • Ollama (Gemma2:27B): 19.39 t/s
- How much RAM does it use to run that 70B model?
  - About 55 out of 64Gb. I have the browser open at the same time, but it doesn’t slow down web browsing.

- ## [Any m3 ultra test requests for MLX models in LM Studio? : r/LocalLLaMA _202503](https://www.reddit.com/r/LocalLLaMA/comments/1jdvk7c/any_m3_ultra_test_requests_for_mlx_models_in_lm/)
  - Got my 512 gb. Happy with it so far. Prompt processing is not too bad for 70b models -- with about 7800 tokens of context, 8 bit MLX Llama 3.3 70b processes at about 145 t/s per second. It then generates at about 8.5 t/s.
  - 70b 8 bit llama 3 at 7800 context: 8.5 t/s generation; 150 t/s prompt eval; 
  - 70b 4 bit llama 3 at 7800 context: 15.5 t/s generation; 150 t/s prompt eval; 
  - 70b 4 bit llama 3 fine-tune at low context with speculative decoding (and coding related prompt): 23.89 t/s generation; 
  - Gemma 3 27b 4 bit at 2317 context: 331 t/s processing; 29.20 t/s generation
  - Gemma 3 27b 8 bit at 3310 context: 255 t/s processing; 18.71 t/s generation 

- ## [M3 Ultra Mac Studio Benchmarks (96gb VRAM, 60 GPU cores) : r/LocalLLaMA _202505](https://www.reddit.com/r/LocalLLaMA/comments/1kvd0jr/m3_ultra_mac_studio_benchmarks_96gb_vram_60_gpu/)
  - I loaded each model freshly in LMStudio, and input 30-40k tokens of Lorem Ipsum text (the text itself shouldn't matter, all that matters is token counts)
  - Input Context Size (tokens): 32k ~ 40k
  - Model Name & Size	Time to First Token (s)	Tokens / Second
  - Mistral Large 123B (4-bit/dense)	900.61	7.75
  - Gemma 3 27B (4-bit)	108.15	29.55
  - Qwen3 30b-a3b (8-bit)	67.74	34.62

- I have the same machine as the OP (96GB, 60 cores) and am running Qwen3-30B-A3B 8bit and Qwen3-32b 6bit concurrently - great combo to use in Aider architect mode. Which two models have you chosen to work with in Roo Code? What has been your experience?
  - I typically use Qwen3 32b as Orchestrator and Architect, Qwen 2.5 32b 128 K as coder and debugger. I use Unsloth versions of all. They can handle certain projects just fine. Especially languages like python. If I run into issues, I mix in deepseek r1 or v3 from openrouter.

- Are you generally satisfied? Or would you rather have the 256GB version? Or the one with 80 GPU?
  - I have the 256 GB version with 60 cores. I would go for the 80 core if given the choice again. Every little bit helps with inference speed. However I can load several 32b 8 bit models concurrently which is great for things like orchestrator mode in Roo Code. Everything works, just could be faster.
- I have the 256 / 60 too. I’m not sure that the 80 would make such a big différence. With lama4 scout it would probably amount to 25 secs of pp time gain in the exemple given. But you still have to wait 80 seconds, which makes it too slow for conversational inférence.

- I also have the 96GB/60 core. I am just a casual user and I couldn't justify another 2000€ for 256GB Ram or 80 core. And I think 256GB is not worth it for my purpose. I can use dense models up to 70B (at Q5) for chatting. Mistral Large and Command A (at Q4) are okayish but everything larger will be way too slow. So the only benefit of 256GB is for MoE models.
  - Shortly after I bought mine, Qwen3 235B A22B came out. Right now, this is the only reason (for me) wanting 256GB. But is it worth 2000€? No, not right now. If that model becomes everybodies darling for finetuning, then maybe.

- Can you explain how to load several models?
  - I use LM Studio, and you just keep loading models until you’ve either loaded all of the ones that you need, or when you reach 85% of your memory capacity. It’s a good practice not to fill more than that.

- That's quite slow, on my 2x3090 I have
  - google_gemma-3-12b-it-Q8_0 - 30.68 t/s
  - Qwen_Qwen3-30B-A3B-Q8_0 - 90.43 t/s

- ## 🆚 [[Benchmark] Quick‑and‑dirty test of 5 models on a Mac Studio M3 Ultra 512 GB (LM Studio) – Qwen3 runs away with it : r/LocalLLaMA _202505](https://www.reddit.com/r/LocalLLaMA/comments/1kfi8xh/benchmark_quickanddirty_test_of_5_models_on_a_mac/)
  - M3 Ultra, 128 CPU / 80 GPU cores, 512 GB unified RAM
- Model	Quant. / RAM footprint 	Speed (tok/s)	Tokens out	1st‑token latency
  - MLX Deepseek‑R1‑4bit	402.17 GB	16.55	 2 062	 15.01 s
  - MLX deepseek‑V3‑0324‑4bit	355.95 GB	19.34	 755	17.29 s
  - MLX Qwen3‑235‑A22B‑8bit	233.79 GB	18.86	 3 096	 9.02 s
  - GGFU Qwen3‑235‑A22B‑8bit	 233.72 GB	14.35	 2 883	 4.47 s
  - MLX Gemma‑3‑27b‑it‑bf16	 52.57 GB	11.19	 1 317	 1.72 s
- TL; DR
  - Qwen3‑8bit dominates – PhD‑level answers, fast enough, reasoning quick.
  - Thinking time isn’t the bottleneck; quantization + memory bandwidth are (if any expert wants to correct or improve this please do so).
  - Mac Studio M3 Ultra is a silence‑loving, power‑sipping, tiny beast—just not the rig for GPU fiends or upgrade addicts.

- Useful test as far as the raw numbers, but not an eval. Not even for quick and dirty. You can give a model the same prompt and get a "bad answer" once, then an amazing answer the next time. This is why some of the tests will run the same prompt 3 or 5 times.

- One thing I'd like to know is how you compare the MLX vs GGFU performance (for same models)?
  - I just run a simple test, based only on that I would only use ggfu if a MLX doesn't exist. It gave me almost the same output, definitely same quality, but almost 30% more fast.

- ## [M2 Ultra 192 gb + GLM Air 4.5/4.6 for local coding agents? : r/LocalLLaMA _202510](https://www.reddit.com/r/LocalLLaMA/comments/1o7k78o/m2_ultra_192_gb_glm_air_4546_for_local_coding/)
- M2 Ultra 192 GB Running GLM 4.5 Air Q8_0 with flashattention in llama.cpp. 10k token prompt, responding with ~400 tokens.
  - prompt eval time =   29693.60 ms / 10565 tokens (2.81 ms per token, 355.80 tokens per second)
  - eval time =   14221.61 ms /   374 tokens ( 38.03 ms per token, 26.30 tokens per second)

- 4.6 at 4bit will need more than 192gb vram, you could use a 3 bit quant though.

- ## [GLM 4.6 already runs on MLX : r/LocalLLaMA _202510](https://www.reddit.com/r/LocalLLaMA/comments/1nujx4x/glm_46_already_runs_on_mlx/)
- My Epyc workstation has 12 RAM channels and I have 8 sticks of 16GB each so I'll max at 192 GB sadly. To run this you'll want 12 sticks of 32 GB to get to 384GB. The RAM will cost roughly $2400.
  - I have DDR5-4800 which is the slowest DDR-5 (base JDEC standard) does 38.4GB/s
  - DDR4-3200, the highest supported speed on EPYC 7003 Milan, does 25.6 GB/s.
  - If you use DDR5-6400 on a 9005 series CPU it is roughly twice as fast. But the new EPYC processors support 12 channels vs 8 with DDR4, so you get an additional 50% bump.

- what's the prompt-processing speed? It sucks to wait 10 minutes every request.
  - As lim context->infinity, pp rate is proportional to attention speed, which is O(n2) and dominates the equation
  - Attention is usually tensor fp16 non-sparse, so 142 TFLOPs on a RTX 3090, or 57.3 TFLOPs on the M3 Ultra.
  - So about 40% the perf of a 3090. In practice, since FFN performance does matter, you'd get ~50% performance.
- Here is my M2 Ultra’s performance: context/prompt: 69780 tokens Result: 31.43tokens/second, 6574 tokens, 151.24s to first token. 
  - Model: Qwen-Next 80B at FP16
  - That is 500/s, but using full precision sparse MoE.
  - About 300/s for a dense 70b model, which you are not using to code. It will be faster for a 30b dense model which many use to code. Same for a 235billion sparse MoE, or in the case of GLM4.6 taking up 165gb, it is about 400/s. 

- CLine/Roo regularly uses up to 100k tokens on the context, it's slow even with GPUs.

- ## [I know nobody has asked before, but what is GLM 4.5 like on an M3 Ultra? : r/LocalLLaMA _202509](https://www.reddit.com/r/LocalLLaMA/comments/1n80nxn/i_know_nobody_has_asked_before_but_what_is_glm_45/)
  - Google claims m3 ultra ram bandwidth is barely slower than 3090 bandwidth. Does this mean I would get barely lower tps compared to a machine with 20 x 3090?
- I just tested 4bit MLX quant with simple task of creating calculator in single html page. This is a standard test I run to see how the model works with one shot tasks that are very well specified.
  - Compared to Air (I tested 4, 6 and 8 bit MLX quants there), it provided better working result on the first prompt.
  - Mac Studio M3 ultra with 256GB ram
  - 19.08 tok/sec • 10013 tokens • 14.29s to first token

- People suggesting Macs for LLMs are often not mentioning that they can have prompt processing times of ten minutes for every single large prompt. Personally I think that it is rather negligent to not mention this to people.
  - I have an M3 Ultra and based on how slow things are with any non-trivially sized context length, I am not even bothering to try a model as big as GLM 4.5
- Not to mention switching models to test different parameters. It is only strictly better than pure RAM setup

- 10 minutes would imply a prompt of around 200, 000 tokens. Is that actually a common use case for you?
- You need to factor in the prompt processing speed of the model/gpu and how big the context is, because pp speed slows down as context gets bigger.
  - Reaching 10 minutes of pp time is pretty easy on my 512 m3u, for example 60k of context with gguf deepseek.
  - But for smaller models it can be quite decent. Mlx gpt oss will be maybe only 1-2 minutes for that same prompt.

- M3 Ultra RAM bandwidth is 819.2 Gb/s while 3090 RAM bandwidth is 936 Gb/s 
  - So it’s probably true that for token generation, which is largely RAM bandwidth limited, that the M3 Ultra is “comparable” to a 3090
  - What’s actually different here is prompt processing speed which is compute bound.  In this realm a 3090 would be many multiples faster.  

- M3 Ultra, 512 GB RAM, 32/80-core variant.
  - I have a script processing files roughly 30-50k tokens in length, which I cache, and then ask subsequent questions of. I just fired it up on GLM4.5 4 bit MLX quant. For a 35000 token document, prompt processing took ~247 seconds. In subsequent turns of conversation generation speed was 10 tokens per second roughly speaking.
  - GLM4.5 Air, same document was ~104 seconds for prompt processing, and then generation is at 30 tokens per second or so.
# discuss-quantized
- ## 

- ## 

- ## 

- ## 

- ## 🆚 [MiniMax M2.1 quantization experience (Q6 vs. Q8) : r/LocalLLaMA _202601](https://www.reddit.com/r/LocalLLaMA/comments/1q3579f/minimax_m21_quantization_experience_q6_vs_q8/)
  - I was using Bartowski's Q6_K quant of MiniMax M2.1 on llama.cpp's server with Opencode and it was giving me some very strange results.
  - The usual way I test coding models is by having them write some of the many, many missing unit tests.
  - I stepped up to Q8 just to see and it nailed everything on the first try with a tiny fraction of the tokens.
  - That's a small sample size and there's always the possibility of a random outcome. But, wow, yikes, I won't be trying Q6 again in a hurry.

- Minimax does not quantize like other models, and is native FP8. You can try my NVFP4 if you have Blackwell GPU’s

- I had that happen with Q8 KV cache. Not worth it.

- Did you try tweaking the settings, such as setting a repetition penalty, or other settings that are designed to reduce the amount of rambling a model does. A q6 should be virtually identical to a q8, there's a good chance it was just random. I always use rep pen of 1.05 for the qwen model I use, and have never encountered rambling with it set.
  - Also you're using a quant with an imatrix, and imatrices can mess up reasoning chains. I don't ever use imatrix quants for reasoning models. And at q6 or q8 you don't need an imatrix quant, it won't make the model any better than without.
- Im pretty sure unsloth uses imatrices. I don't have any references, it's from my own experience and I also remember bartowski talking about it in a thread once, which suggests it's a known issue. I normally use mradermachers non imatrix quants.

- ## 🆚 [Benchmarks for Quantized Models? (for users locally running Q8/Q6/Q2 precision) : r/LocalLLaMA _202512](https://www.reddit.com/r/LocalLLaMA/comments/1pyrjke/benchmarks_for_quantized_models_for_users_locally/)
- Nope! Definitely a need for such a thing. Quantization has been around for a while but is still the wild-west of LLM's in terms of documenting the results/impact.

- Most of the benchmarks are too annoying or slow to run, unfortunately. MMLU-Pro compsci only isn't too terrible and Aider 'Polyglot' limited to python only (or whatever your preferred language is) is ok, too.
- [Unsloth Dynamic GGUFs on Aider Polyglot | Unsloth Documentation](https://unsloth.ai/docs/basics/unsloth-dynamic-2.0-ggufs/unsloth-dynamic-ggufs-on-aider-polyglot)

- Devstral-Small-2-24B-Instruct-2512-Q8_0.gguf Lm-studio community VS Devstral-Small-2-24B-Instruct-2512-UD-Q4_K_XL.gguf Unsloth
  - It's a dense model, but it all fits comfortably in a 96GB RTX 6000, even with very long runs. The card is set to 450W instead of 600W.
  - The problem is simple: The Q4_K_XL version of unsloth returned the modified HTML file but without some of the required fixes, while the Q8 version solved every problem.
  - Obviously, it's only one test, but I definitely prefer the slower execution speed and greater precision. Now I'll try the Q6.

- I found MXFP4 definitely superior to Q4 across a variety of models considering their applied weights (MXFP4+F32), even better than Q8 in the few cases I tried - at the exception where GPT-OSS-20B MXFP4 was not as good as Unsloth slightly heavier F16.

- Primary CUDA maintainer for llama.cpp/ggml here, given enough time I'll eventually do it for quality control and publish the results here https://github.com/JohannesGaessler/elo_hellm
# discuss-llm-tools-tips/tricks
- ## 

- ## 

- ## 

- ## [New functiongemma model: not worth downloading : r/ollama](https://www.reddit.com/r/ollama/comments/1pq69o5/new_functiongemma_model_not_worth_downloading/)
  - I have a valid MCP toolset that works great with other very small models such as qwen3:1.7b. I obtain quite reliable function calls. So, an even smaller model that could do this with the same quality sounds great. 
  - I downloaded the functiongemma:270m-it-fp16 version of 552MB and deleted after the second test
- I believe the purpose of this model is to be fine-tuned further on your specific tool use case.

- In practice I’ve had the best luck with models that were explicitly trained for tool use / JSON (and I still add strict schemas + validation + retry).
  - If you want to stay local, I’d try Qwen2.5-Instruct (7B) or Llama 3.1 Instruct (8B) as a baseline and then see how far down you can compress without breaking tool calls.

- It’s a 270m parameter model. MCP dumps massive JSONs. Comparing it to Qwen1.7b is literally 6x its size. I think this model is good for small, focused use cases - not something like MCP.

- ## 💡 [Suggestions to improve RAG with 200+ pdfs : r/Rag _202412](https://www.reddit.com/r/Rag/comments/1h8205b/suggestions_to_improve_rag_with_200_pdfs/)
- I’m working on a company where we are running a RAG for a company with more than 4.000.000 documents (more than 200.000.000 embeddings) so this might help you.
  - We start with an ingestion process where all PDFs or documents (regardless of source) are converted into markdown using LLMSherpa, an open-source library we’ve fine-tuned for our needs. The markdown is then subdivided into sections, which are further broken down into smaller chunks. These chunks undergo a context retrieval process to add additional relevant information before being stored.
  - Next, we generate embeddings for these chunks using BAAI/bge-m3 and store them in a PostgreSQL database managed via pgvector.
  - When a user interacts with our playground, they send a message, which includes the chat history. To handle this, we first make an initial LLM call to rephrase the prompt and incorporate additional context. This step is crucial for questions referencing prior chat history, ensuring clarity and proper fine-tuning before the main LLM call.
  - The rephrased prompt is then matched against all the stored chunks in our database using inner product similarity, with a predefined threshold to filter the most relevant chunks. After retrieving these, a reranker further narrows the results to the top 50 most relevant chunks.
  - Finally, the rephrased prompt and the refined chunks are sent to the LLM, which generates the user’s final answer. To ensure fast and efficient database queries, we use HNSW (Hierarchical Navigable Small World) indexing, enabling low-latency and scalable retrieval.

- Converting the PDFs to images and using an LLM like Claude 3.5 Sonnet to convert it with custom instructions works quite well, though it's slower and pricier. I convert all my PDFs like that.

- ## [Best AI to search in large folder of PDFs : r/AI_Agents _202503](https://www.reddit.com/r/AI_Agents/comments/1j1pum1/best_ai_to_search_in_large_folder_of_pdfs/)
- You don’t want an AI, you want a robust indexing and search engine that feeds relevant docs/chunks to an LLM for a simple summarization. You can do that with RAG, vector DB, or just old school ELK stack. Plenty of options.

- Notebooklm can take up to 50 files. And it has the great podcast summary.

- I have efficient semantic chunking + STORM + meilisearch integration specifically for this problem.

- ## [How does having a very long context window impact performance? : r/LocalLLaMA _202507](https://www.reddit.com/r/LocalLLaMA/comments/1lxuu5m/how_does_having_a_very_long_context_window_impact/)
- Basically, the longer the context window the more memory is needed to store the model and the KV cache. The more memory the model takes up, the longer it will take for the GPU to read the model from memory.
  - keep in mind many models claim 128K context length, but their ability to recall information deep within a block of text will degrade as it fills up. QWQ appears to be one of best models for long context recall and creative writing.

- You should not max out the context window. You should be extracting what's valuable and reinjection it when necessary.
  - This is a lot more complex than it seems. But context summarization into RAG and MCP servers probably help get you there.

- My experience with Gemma3 27B is that speed fell off the cliff once the context is more than 4 windows (ie over 4K). I’m using a 5070ti and I get 30t/s using Q3KM model under 4K. Beyond 4K context it requires a lot more compute to look back and remember things is my understanding. So you get loooong prompt processing time. In my case it’s 5t/s… Probably better off using Mistral Small which is what I’m doing, something a bit longer context and less cliff.
  - You can also write in auto-summarizing function just before it hits context limit. Or use something that has it. And when the sessions get very long use RAG.

- Gemma 3 had a very memory heavy context. Q4 quant with 32k context was barely fitting into 32gb vram. But people praised it for good attention to context. Then Google "fixed" it, introducing SWA, which made it lightweight, but after this I've seen many complaints about the model forgetting things very fast.
- Gemma3 does not understand long context that well. Even at 8k it is becoming quite inconsistent (contradicting what was in context before).

- ## [LLM with large context : r/LocalLLaMA _202505](https://www.reddit.com/r/LocalLLaMA/comments/1kdnbhj/llm_with_large_context/)
- The current mainstream open-source LLMs have a context length of around 128K, but there are already some options that support longer contexts (Llama4, Minimax-Text, Qwen2.5-1M). 
  - However, the GPU memory overhead for long contexts is substantial. For example, Qwen2.5-1M-7B mentions that it requires approximately 120GB of GPU memory to deploy a model supporting a 1M context. 
  - It's difficult to fully run a model with a 1M context locally. However, such models might perform better than regular models in tasks requiring longer inputs(64K-128K) refer to Qwen2.5-1M.
- A significant issue with using long-context LLMs is that most LLMs' long contexts are extrapolated (for instance, Qwen-2.5 has a pre-training length of 4K → long context training of 32K → Yarn extrapolation to 128K, and Llama3.1 has pre-training up to 8K → Rope scaling extrapolation to 128K), and only a small amount of long-context data is used during training. 
  - As a result, performance may degrade in actual long conversations (I believe most models start to degrade above 8K length, and performance notably worsens beyond 32K). 
  - Of course, if you only aim to extract some simple information from a long text, this performance degradation might be acceptable.

- Attention mechanism right now just don't handle large context very well. If there's too much hard distractors within context, the model just won't do too well.

- But fan of Qwen 3 8B or 32B. You can fit 128K with model in 24GB of VRAM, but you will have to trade Q8 for Q4 for KVcache on the 32B model. 

- 32k is where all models degrade, even if stated otherwise.
  - Qwen 3 are better ones though.
  - There is also Llama 3.1 8b Nemotron 1M, 2M and 4M; I had mixed success with them - they are strange, weird models, but handle context well.

- 1m context's kv cache takes too much vram for local use case. https://www.reddit.com/r/LocalLLaMA/comments/1jta5vj/vram_requirement_for_10m_context/

- [How large is your local LLM context? : r/LocalLLaMA _202505](https://www.reddit.com/r/LocalLLaMA/comments/1j6xpvt/how_large_is_your_local_llm_context/)
  - Most local LLMs are massively degraded by 32K context. Both token quality and generation speed. I would say there's no point going over that, and you should try not to even get close. You have to do more work to fit in only the relevant context but that's the tradeoff with going local
- No I don't unless it's required. Having large input tokens impacts the throughput, so it's better to optimize the input tokens length.

- ## 🆚 [Comparing Unsloth's GLM-4.6 IQ2_M -vs- GLM-4.6-REAP-268B Q2_K_XL : r/LocalLLaMA _202511](https://www.reddit.com/r/LocalLLaMA/comments/1ozq14d/comparing_unsloths_glm46_iq2_m_vs_glm46reap268b/)
  - During my limited coding testing I'm seeing:
  - REAP_Q2_K_XL sometimes perform better but fail more often, including sometimes looping and some broken code outputs.
  - Full_IQ2_M retains more general and contextual knowledge and seems more consistent, but perhaps less chance of a great output.

- Tested REAP vs IQ a lot. IQ always better. Minimax M2 ---> same
- I had the same experience with GLM 4.6 and GLM 4.5 air. Eventually I think reap will work but at the current stage I view it as a tech demo.

- The trade‑offs you describe mirror the differences between quantization and Mixture‑of‑Experts pruning at a systems level.
  - A Runpod overview notes that moving from FP32 to INT8 or 4‑bit quantization can cut memory use by 60–80 % while preserving over 95 % of model accuracy. 
  - By contrast, REAP (Router‑weighted Expert Activation Pruning) evaluates the router’s gate values and expert activation norms to remove low‑impact experts, achieving near‑lossless compression even after pruning 50 % of experts on code‑generation tasks.

- All the reaps I tried were slower and dumber. Then again i didn't use them for code as intended.

- Far as roleplay goes, I personally find that REAP loses a ton of flavor and personality. It just doesn't feel good.

- ## [What tools or workflows save you hours every week? : r/PKMS](https://www.reddit.com/r/PKMS/comments/1p00u1x/what_tools_or_workflows_save_you_hours_every_week/)
- A digital file cabinet (PKMS) to store/organize my notes/documents/files
  - For enhanced features, I use pkms app Devonthink; accessed with a Mac and iPad
  - Integrated scripting for workflow automations
  - I use AppleScript on my Mac

- Knowledge management: Mostly Note app + NotebookLM for long and hard PDF (I put that into the app and it turns that to podcasts!)
  - Daily planning: Brain dump + Saner: I basically just offload my thoughts and the app turn it to tasks with reminders automatically

- Zettelkasten for idea incubation/research/serendipity, PARA as archiving method, GTD/ZTD for running tasks. A personal combination of them

- ## [Best small LLM (≤4B) for function/tool calling with llama.cpp? : r/LocalLLM _202505](https://www.reddit.com/r/LocalLLM/comments/1kdva3y/best_small_llm_4b_for_functiontool_calling_with/)
- So far qwen3 is really the only game in town for consistent tool calling for me at small sizes. 
  - when I test I do not tell the model exactly what tools to use and try to keep my prompts sort of vague because I want to be able to ask for something without for example knowing a table name in a database.
  - I’ve only really tried 4b and up. I had downloaded 1.7b and it worked like once out of the 3 runs I tried with it. I’d imagine a smaller model would do worse. If you’re very instructionally verbose it may work better though.
  - 4b, 8b, 14b, 32b all call functions really well and consistently.
  - 8b, 14b, 32b can digest the returned agent information and transform it.
  - 14b, 32b can transform it well and provide better context.
  - 32b is not noticeably better for agentic at least for my use cases than 14b
  - Sweet spot for me is 8b/14b. I’ve used 8b extensively. It fails like 10% depending on instruction vagueness and how strict I am with temperature.

- Everyone’s talking about Qwen which makes sense due to its recent release but for an alternative, I’ve had good success with the Gemma 3 4B and 12B models. Once you get around the Google ReAct logic it’s pretty manageable and it seems to be smart enough for my use cases

- ## [Cerebras REAP'd GLM4.6: 25%, 30%, 40% pruned FP8 checkpoints on HF! : r/LocalLLaMA _202510](https://www.reddit.com/r/LocalLLaMA/comments/1oefu29/cerebras_reapd_glm46_25_30_40_pruned_fp8/)
  - The models deployed in Cerebras prod inference API are not pruned, and we don't have such plans for GLM4.6. The REAP pruning work is for research purposes and to give more efficient models to the community

- The MoE is sparse, yes. But the REAP technique appears to leverage the fact that “experts” are more or less just certain parameters highly correlated with other parameters. It’s not like there’s a programming expert, a language expert, etc. it’s more like you have some number of tokens that seem to be the strongest correlated to other sets of tokens, so an invocation of that token or closely related tokens results in that particular part of the neural net lighting up.

- I actually have the opposite question. Can we reduce the number of experts from 8 to 6 or 4 and still maintain good performance. Experts are largely CPU bound and would go a long way in speeding up the models.
  - my experience with qwen3 30b a3b
  - with 7 things are ok , but it fails sometimes (i would say 10% of the times you noticed is worse than the default)
  - with 6 it fails more often
  - with 4 it lose coherence in the majority of times
  - but increasing also doesnt help a lot
  - with 9-10 i barely see an improvement over 8
  - with 12-16 the output gets worse

- ## [I did not realize how easy and accessible local LLMs are with models like Qwen3 4b on pure CPU. : r/LocalLLaMA _202510](https://www.reddit.com/r/LocalLLaMA/comments/1o1z3hj/i_did_not_realize_how_easy_and_accessible_local/)
  - I hadn't tried running LLMs on my laptop until today. I thought CPUs were too slow and getting the old igpu working (AMD 4650U, so Vega something) would be driver hell. So I never bothered.
  - I downloaded LM Studio, downloaded Qwen3 4b q4, and I was getting 5 tok/sec generation with no hassle at all with the automatic Vulkan setup. Not bad
  - Then, just to be sure, I disabled the GPU and was surprised to get 10 tok/sec generation with CPU only! Wow! Very usable.
  - This means I can just buy any used laptop off ebay, install linux, and go wild??? It has a built in monitor, low power draw, everything for $200-300? My laptop only has DDR4-3200, so anything at that speed or above should be golden. Since async processing is fine I could do even more if I dared. Maybe throw in whisper.

- Qwen3-4B is really a good choice for 16GB laptops (common choice for general consumers). I use it for local PDF rag and it can provide me with accurate in-line citations + clear structured report.

- Or you can just run it much faster with a $60 GPU and have your low power kitchen computer connect to that via wifi.

- ## 🆚 [8B models at full-size, or 32B models at Q4? : r/LocalLLaMA](https://www.reddit.com/r/LocalLLaMA/comments/1o13oyn/30b_models_at_fullsize_or_120b_models_at_q4/)
- Q4 isn't much of a degradation and the base is so much stronger.
- The degradation depends on the models original size and architecture as MOE can be more sensitive but overall I would always pick the larger models when possible so long as you still have enough space for context.

- ## [Mixed precision KV cache quantization, Q8 for K / Q4 for V : r/LocalLLaMA _202505](https://www.reddit.com/r/LocalLLaMA/comments/1kddcdp/mixed_precision_kv_cache_quantization_q8_for_k_q4/)
- Plenty of KV cache quantization literature suggest K is more sensitive to quantization than V (SKVQ, QAQ, etc.
  - No one can really answer whether K8V4 is good enough as this is highly model-task-setting-whatever else dependent, 
  - but conventional wisdom suggests: Granting Key cache more budget is generally the right move.
  - You probably need some kind of "fancy" KV cache quantization techniques — like our KIVI, 

- Yes.. I try it all the time. 4/4 is really bad, 8/4 is as low as I'm willing to go. Don't forget to compile llama.cpp with all kernels.

- ## [Does Q4-8 'KV cache' quantization have any impact on quality with GGUF? : r/LocalLLaMA _202409](https://www.reddit.com/r/LocalLLaMA/comments/1flw4of/does_q48_kv_cache_quantization_have_any_impact_on/)
- Yes in my test. I was testing the summarizing ability of llama3.1 8B q5_ks on oobabooga a while back on youtube transcripts.
  - With q4 kv cache the accuracy was about 82%. (something like that) I think even q8 had a performance drop that was unacceptable. (if I remember correctly)
  - Without cache quantisation bullet point accuracy went up to 97.6% accuracy. This was over at least 5 youtube videos of 2-12 minutes each. (If I remember)

- Q8 is pretty painless, but Q4 can be pretty rough, although is usually usable. Smaller models will feel it worse. Just like with model quantization.

- Yes, I noticed some larger models suffer even with q8 so I don't even bother using it

- ## [Recommendation for getting the most out of Qwen3 Coder? : r/LocalLLM _202508](https://www.reddit.com/r/LocalLLM/comments/1mrzi5x/recommendation_for_getting_the_most_out_of_qwen3/)
- Setting K quantization to q4_0 has a pretty big impact on model’s quality of output. 
  - K is much more sensitive to quantization than V. 
  - You can get away with q4_0 for V but for K the lowest i’d go is q5_1 and ideally q8_0

- [Why is my llama so dumb? : r/LocalLLaMA](https://www.reddit.com/r/LocalLLaMA/comments/1ljn4h8/why_is_my_llama_so_dumb/)
  - I know a lot of models don't like going that small. Try upping that to Q8_0 or even fp16/bf16.
  - Q4_0 is a fairly very aggressive quantization. Quantization noise leads to loops.
  - Ive personally never used a model that didnt have a noticable decrease in quality at q4, often even at q8. Just leave it at fp16.

- [What's the best models available today to run on systems with 8 GB / 16 GB / 24 GB / 48 GB / 72 GB / 96 GB of VRAM today? : r/LocalLLaMA](https://www.reddit.com/r/LocalLLaMA/comments/1k4avlq/whats_the_best_models_available_today_to_run_on/)
  - I wouldn't go as low as q4_0 for K cache, quality impact is quite noticeable. q4_0 on V cache seems fine though.
  - I use in larger models (nemotron 253B, deepseekv3 03-25) ctk q8_0 and ctv q4_0, haven't noticed much differences vs fp16 (on deepseek I had to test at like 4k ctx lol)

- ## [LM Studio released new version with Flash Attention - 0.2.22 : r/LocalLLaMA _202405](https://www.reddit.com/r/LocalLLaMA/comments/1cir98j/lm_studio_released_new_version_with_flash/)
- Must be because llama.cpp merged it recently.
  - Yes, from the changelog
- ROCm version already released you need to get the link from LMstudio discord sever

- The flash attention benefit becomes noticeable at LONG LONG contexts - at 26k, its the diff between 30 tok/sec and 10 tok/sec w/ LLama 3 8B on an M3 Max.

- the difference shows up at long contexts.

- Quick check for me didn't see any difference between flash attention on and off for llama3 8b. On a Macbook pro
  - Made huge difference for me on m2 max Mac studio in terms of ftimr to first token and general response rate for decently sized contexts. Details are also remembered much better
- Try with more context, or models like Mixtral. In llama.cpp (which LMStudio uses) I get about 4+ tokens a second higher and no real downside. I can store a lot more context at the same time.

- Flash Attention works on Mac? I always thought CUDA only.
  - Not only does it work it seems to be giving a bigger performance boost, at least on some quick tests

- ## 🆚 [weighted/imatrix VS static quants? : r/LocalLLaMA _202405](https://www.reddit.com/r/LocalLLaMA/comments/1ck76rk/weightedimatrix_vs_static_quants/)
- Imatrix quants were introduced a couple of months ago and are recommended over static quants because they have better output quality. 
  - For example, a Q4_K_M quant made with imatrix should be closer to a Q5_K_M non-imatrix quant in quality.

- Importance matrix is used to choose vocabulary to preserve precision for.
  - Both normal Q_k quants and IQ quants can use imatrix.
  - IQ quants, I don't know the expansion of the I, but they attempt to approximate the original value at runtime. They do extra math, and slow down CPU inference but GPUs generally are still memory speed limited.

- Are there any disadvantages? I usually go for Q4k_m and tried iq4_nl or something, the IQ is slightly smaller in file size but inference speed seems to be basically the same. If imatrix is better why do people still release/use static? 

- [Static vs imatrix? : r/SillyTavernAI](https://www.reddit.com/r/SillyTavernAI/comments/1ggfpo8/static_vs_imatrix/)
  - imatrix is distinct from i-quants.
  - i-quants are better if your hardware(CPU in this case, not GPU/RAM/VRAM) is beefy enough to run them at a speed you find usable.
  - K-quants if your CPU is struggling with i-quants.

- [How does any of this work? : r/LocalLLaMA](https://www.reddit.com/r/LocalLLaMA/comments/1p8up6n/how_does_any_of_this_work/)
  - i-matrix quants use special calibration matrix, they essentially maintain quality on selected type of tasks sacrificing anything else. 
  - My experience suggest that imatrix quants are ever so slightly messed up, especially for creative writing.

- ## [Getting counter-intuitive results with local KV Cache Quantization Benchmark - am I doing something wrong? : r/LocalLLaMA _202509](https://www.reddit.com/r/LocalLLaMA/comments/1nn2nqz/getting_counterintuitive_results_with_local_kv/)
  - I've been running some benchmarks on KV cache quantization for long-context tasks, and I'm getting results that don't make much sense to me. 
  - The Weird Results: I was expecting to see a clear trend where higher quantization (like q4_0) would lead to a drop in accuracy compared to the f16 baseline. Instead, I'm seeing the opposite. My best performing combination is k-f16_v-q5_0 with 16.79% accuracy, while the f16-f16 baseline only gets 13.74%.

- You see scattered reports of quantized KV increasing accuracy because it “fuzzes” attention in a way that actually benefits (specifically) low bit weight quants. Basically it acts as an implicit smoothing function. I’ve not had amazing luck with llama.cpp’s implementation, but EXllama’s KV cache quants seem to perform exceptionally well at even 4-bits. 

- ## [国内外大模型API平台体验对比 - 知乎](https://zhuanlan.zhihu.com/p/1914700194517345472)

- 如果想使用国内的模型API，推荐使用国内云厂商提供的API服务或第三方代理平台。
  - 如果想在国内使用国外的模型API，或者想同时使用很多不同系列的模型，推荐使用第三方代理平台。
  - 如果服务器在国外，想调用国外的某个API模型，则推荐使用国外云厂商，或第三方代理平台。

- 2025/9/1 更新：
  - 1. 增加DMXAPI，一个不错的API中转商，模型比较全。
  - 2. 删除博阅，因为其不开放新用户充值。
  - 3. 降低openrouter的推荐指数，因为使用过程遇到稳定性问题比较多 
  - 4. 降低硅基流动的推荐指数，因为限流TPM太小，影响使用。
  - 5. 增加GLM、Kimi、Minimax模型的推荐厂商

- openrouter 背后的供应商比较乱, 有些模型版本不是最新的. 还需要自己排除供应商

- ## 🔧 [Open WebUI vs. LM Studio vs. MSTY vs. _insert-app-here_... What's your local LLM UI of choice? : r/LocalLLM _202502](https://www.reddit.com/r/LocalLLM/comments/1ij3j8m/open_webui_vs_lm_studio_vs_msty_vs_insertapphere/)
- Ollama vanilla CLI in tmux with vim copy/paste between terminals. I like pain

- All of them; don’t lock into one solution.

- Open WebUI + LibreChat. LibreChat mainly for creating agents for RAG. Most painless interface for RAG.

- Open Web UI. MSTY is no alternative because it is an all-in-one solution.
  - Closed source right?
- Yep, they are selling it for businesses.

- KoboldAI Lite running on KoboldCpp. Most others aren't as flexible and just focused on instruct. This one can do instruct, but it can also do regular text generation for example. 
  - KoboldCpp meanwhile is a single executable with text gen, image gen, image recognition, speech to text and text to speech support. And it emulates the most popular API's if you prefer another UI (KoboldAI LIte doesn't need the backend to have any UI code so if its not open in the browser it does not effect you).

- ## [intel的cpu连大模型都没法跑, 怎么还天天在推aipc? - 知乎](https://www.zhihu.com/question/668042879/answers/updated)
- 对于端侧AI，我个人的想法，最大的价值应该是拉高上下文窗口，在本地做个人知识库，以及本地批量推理，比如做科研的，懒得读论文，让AI批量总结写个综述。这两种做法如果调用线上的API，其实挺贵的。阅读一篇论文少则几千tokens，多则两三万tokens。本地使用32768的上下文长度的Qwen3 8B，也能完成得不错
  - 做长窗口本身就需要资源，transformer的kqv计算是个o(n^2)的复杂度

- 端侧 AI 现在的应用场景实在是太小。尤其是设备无时无刻在线的情况下，我为什么放着免费的强大的在线 AI 不用，转而去用不能联网搜索、更弱，更卡、更耗电的端侧的 AI 呢？
  - 我本地部署了chatgml 的 6B 和秋叶的 [SD 整合包] ，但是用到的真的不多，得到的结果也比不了在线的

- ## 🆚 [为什么都在用ollama而lm studio却更少人使用? - 知乎](https://www.zhihu.com/question/654357364)
- 需要注意的是，不同于全部代码在github开源、甚至可以自己动手编译的ollama，lm studio至今仍是闭源商业软件（仅一部分非核心代码除外）

- Ollama 于 5 月份推出的全新多模态引擎。基于多模态引擎，Ollama 可以支持运行能同时处理图像、文本的模型。新架构不仅解决当前多模态挑战，也为集成更复杂的能力（语音、生成等）和优化性能（更长上下文、更高并发）打下基础。

- 我的体会：
  - ollama用起来和docker一样的感觉，pull模型，run模型，ls看模型，ps看运行。非常顺手丝滑，入手无门槛。
  - llama的中文，微调各种chat，code，够用。而且都是量化好的，随拉随用，4090就跑的起来。尤其是在国内拉模型速度极快，我的环境最高可达15m/s
  - ollama是llama.cpp实现模型推理，模型小，速度快。
  - ollama提供11434端口的web服务，重要的是还兼容openai的端点接口，可以和各种前端配合，比如ollama自己open webui，国产的chatbox，连后端带界面，一套搞定
  - ollama是系统服务形式（也能容器运行），前后端分离（ 严格来说没有前端，只有命令行入口），耦合小，搭配灵活。
- ollama的迭代很快，现在多模型并发的问题已经解决了

- ollama现在支持分布式推理吗
  - 现在不支持，但支持单机多gpu运行

- 拉模型麻烦就困扰很多人了，ollama照着教程做，基本没有问题

- ollama配合open webui不错的

- ollama看着速度快，其实它最大问题是修改个上下文都很麻烦
  - 可以用chatbox之类的聊天框

- lm studio 也提供openai-like的api后端，支持前后端分离，也支持llama.cpp（在mac还支持mlx框架）. 模型基本上也都支持，而且都是从hf上一键式下载部署（不过网络确实是问题）
  - 总的说，linux上部署还是合适，不用ollama，还有vllm，lmdeloy，以及sglang，都是开源的，很适合开发人员或者是组织内部部署。windows上都差点，lmstudio界面耦合，闭源，拉模型走镜像点，不能分布式推理，个人自己实验性跑跑好一些。

- LM图形化界面也可以微调大量的模型运行参数，ollama这方面就对小白不够友好了，只能使用命令行参数
  - LM做server服务器时，界面有动态反馈的执行信息可以供用户观察到，调试问题方便。
  - LM最新的版本在chat界面下，还支持了ollama不支持的LaTex数学公式表达，和本地RAG文档信息检索，这些都是ollama还不提供的特性。

- ollama 和 LM studio 均可以支持不同大模型的本地部署，并且会优先使用 GPU 进行推理。如果没有发现 GPU，就会使用 CPU 推理，因此也会占用一部分内存。从实际使用来看，笔记本内存应该至少为 8GB 才能正常运行。

- 写程序和ollama交互真的是顺滑，几句代码模型快速切换。

- ollama跟vllm、sglang、trtllm相比是个玩具
  - lm studio连玩具都不如

- 感受上原因是ds最火的时候，铺天盖地的自媒体教程都是ollama，提到lm的少的多。这个东西一旦形成宣传效应了，除了专门搞这个的，就不会有人深入研究了。

- lm studio能像ollama那样同时使用chat和embedding吗？lm studio每次都要预先加载。

- ## 🍎 [如何看待苹果发布的 MLX 机器学习框架？ - 知乎 _202312](https://www.zhihu.com/question/633585779)
- MLX是一个类似NumPy数组的框架，目的是可以在苹果的芯片上更加高效地运行各种机器学习模型，当然最主要的目的是大模型。
  - MLX的设计受到PyTorch、Jax和ArrayFile的启发，目的是设计一个对用户极其友好，但同时在训练和部署上也非常高效的框架。
  - 所以，它的接口你会非常熟悉，因为它的Python接口与NumPy很相似，而它的神经网络模型的接口和PyTorch非常类似。

- 2023年了，真的还需要为了自家芯片从零开始构建一个深度学习训练框架吗
  - 有的，感觉是专门针对uma优化的
- 毕设是深度学习后门攻击相关 设备是macmini m4 从pytorch框架切换到mlx框架 同样的实验同样的训练量 mlx速度快了好几倍 实打实的提升
  - 但是需要重构训练代码，我一套pytorch代码，只需做少量适配，可以自动在昇腾、nVidia、mps之间切换。而且，mlx确实比mps提升好几倍，但是我如果用nvidia或者昇腾910B，mlx性能还有差距。
- 在 MacBook Air m3 上，mlx 的矩阵乘法、SVD分解运行速度明显快于 PyTorch
  - 如果不使用 mlx 来进行深度学习，仅用于常规科研计算或优化任务，实际上还是蛮适合的。
  - 然而，mlx 目前甚至不支持 float64，开发团队当前考虑的是它们 GPU 反正用不到，这对一些高精度计算需求又是一种限制，更不用说一些未实现的算法或者数据类型还需要从零写了。

- 要是keras后续能够支持mlx后端就好了，这样苹果设备上写的代码不至于到别的平台上跑不了还要重构了。

- [苹果向英伟达生态妥协了！MLX框架主动适配CUDA - 知乎 _202507](https://zhuanlan.zhihu.com/p/1929178251202376826)
  - 苹果一直以来都以“封闭”著称，但随着英伟达CUDA生态在AI开发领域占据绝对主导地位，苹果这下也不得不转变姿态了。
  - 过让MLX框架主动适配CUDA，今后苹果开发者也能利用英伟达GPU训练模型。其本质是增加了对CUDA的后端支持，方便开发者在Windows/Linux的英伟达显卡上训练模型，然后再部署回Mac、iPhone等设备。
  - 是给Win-vidia/Lin-vidia做MLX支持，不是给Mac版MLX做CUDA驱动

- 这两天尝试去学习了一下 mlx 和 mlx 的源码，粗略的看法有 2 点：
  - 宏观上，框架的设计很棒，整体设计上很好地吸取了前人的经验，在保证易用性的前提下，保留了足够高的优化上限；
  - 微观上，项目的 C++ 水平比较一般，比较像是几个工程师的 side project，如果要变成长青树，内部大量的实现都需要重构
- 关于架构。我觉得之前几年，训练框架上的实践总结了这样的一些经验：
  - pytorch 和 tensorflow 的争斗结果告诉我们，让大家写 python，而不是在 python 里写 DSL，提升易用性是很重要的；
  - torchscript、libtorch 的各种坑告诉我们，完全依赖在 python 上，图优化很棘手，扔手机这样没有 python runtime 的地方也是真的头疼。最好不要纯 eager 模式，而是能让框架提取出来一些子图。或者是有个固定点的 c api，给不训模型的工程师们留条活路；
  - transformer 告诉我们，也许从学术角度来说，控制流优化起来很性感，但是实际应用中，全是一条路走到黑；
- 之前我觉得 jax 就是训练框架上的集大成者，各种设计真的很漂亮。可是它拖了个重重的 XLA 的尾巴，可能是为了跑在 TPU 上，也可能是 jax 的成员中有很多 tf 里做编译优化的人吧。这使得早期的 jax 对用 nv 显卡的用户很不友好，等 pytorch/huggingface 成了气候，也就无力回天了。
- 现在 mlx 基本吸收了 jax 的经验，
  - 采用了 numpy api + lazy evaluation；
  - 有一个比较干净的 c api，甚至已经有了 swift binding；
  - 内部留出了简单的图优化接口 mlx.core.compile ，保证了优化的上限。

- 看了一眼框架源码，完全是重新搞了一套框架，API尽量对标PyTorch，目前也只支持少量API。这样框架适配成本感觉有点大，连前端Python API都要自己构建，复刻大量代码逻辑且不说，PyTorch社区的全量feature的跟踪演进就会是一个难题。
  - 感觉Apple和昇腾走向了两个方向的极端，昇腾是完全依赖原生的插件化，会想尽一切办法复用原生逻辑，实在不行就复刻；Apple则是完全抛弃原生逻辑，端到端重新搞一套。

- 看了下代码，苹果是重新造了个轮子，前端干的事和PyTorch和Jax没啥区别，感觉重点还是在Apple Silicon的后端上。目前的实现还是挺小巧的，用来学习的话还不错，但要在feature上对齐现有的框架还有不少的活要干。

- 个人感觉这玩意有点鸡肋。
  - mac写代码、调试，然后服务器完成整个训练。这就有问题了，服务器不支持MLX框架。
  - mac写代码、调试，然后mac完成整个训练。 正常公司跑模型，如果少量数据使用几张淘汰下来的1080就可以，价格还便宜。数据量大，要使用分布式并行训练，那就没mac什么事情了。
  - 最近火热的大模型训练，哪家公司会用mac搭建集群训练大模型，并且训练完成后使用mac做推理。用不到mac就没MLX什么事情了。

- 我觉得可以参考早期swift，一年一个版本，让你感到崩溃，虽然这次开源，但是主力应该还是苹果自己

- [阿里巴巴发布了与苹果 MLX 架构兼容的 Qwen3 升级版，新版本都有哪些新特性？ - 知乎 _202506](https://www.zhihu.com/question/1918255662552582106)
  - MLX是苹果专为Apple Silicon芯片（M系列）设计的开源机器学习框架，它的核心优势在于深度整合苹果硬件特性，尤其以“统一内存模型”为核心创新
  - 统一内存架构：数据存储在CPU与GPU共享的内存空间中，跨设备计算时无需显式拷贝数据，相比传统框架（如PyTorch）减少90%以上的内存传输开销。

- ## [如何看待 Google 最新开源的 Gemma-3 系列大模型？ - 知乎 _202503](https://www.zhihu.com/question/14777841836)

- Gemma-3主打的卖点是单卡可跑+多模态。
- Gemma-3的核心竞争力在于效率革命。其27B版本仅需单张H100显卡即可运行，而竞品达到同等性能往往需要10倍算力。这种效率提升并非简单的参数压缩，而是架构层面的创新
  - 知识蒸馏技术：基于Gemini 2.0的"教师模型"进行蒸馏，将大模型能力迁移到小模型，实现"用1/10参数达到80%性能"的效果。
- 尽管Gemma-3表现亮眼，仍需注意以下问题： 
  - 1. 长尾任务缺陷：在数学推理和伦理判断等特定场景，实测结果显示其表现不如Qwen2.5-Max。 
  - 2. 多模态精度瓶颈：处理复杂图像时，SigLIP编码器的细节识别能力仍落后于专业CV模型。 
  - 3. 训练数据依赖：虽然支持140种语言，但实际表现存在"英语最优，小语种次之"的问题。 
- 未来可能的突破方向包括： 
  - 动态架构：根据输入内容自动切换计算资源分配，例如视频处理时临时调用更多GPU核心。 
  - 跨模态生成：从"理解多模态"升级到"生成多模态"，例如根据文本描述直接生成3D模型。 
  - 边缘端优化：进一步压缩模型体积，在手机端实现实时多模态交互。

- 开源Gemma系模型正式迭代到第三代，原生支持多模态，128k上下文。
  - Gemma 3一共开源了四种参数，1B、4B、12B和27B。最最最关键的是，一块GPU/TPU就能跑模型。
  - 在LMArena竞技场中，Gemma 3拿下了1339 ELO高分，仅以27B参数击败了o1-preview、o3-mini high、DeepSeek V3，堪称仅次于DeepSeek R1最优开源模型。
  - Gemma3系1B、4B、12B、27B分别基于2T、4T、12T、14T token数据完成训练。
  - 与闭源Gemini 1.5和2.0相比，Gemma 3-27B基本上略逊色于Flash版本。
- 采用与Gemini 2.0模型相同的研究和技术打造。

- 最大的17GB是稳稳可以跑在拥有24GB显存的Nvidia90系显卡的。

- Gemma 3n 是一款专为移动设备量身打造的多模态 AI 架构，它不仅支持图像、音频、视频和文本的输入输出，还通过创新的 MatFormer 架构和 Per-Layer Embeddings 技术，实现了高性能与低内存占用的完美平衡。
  - E2B 和 E4B 两种模型版本，分别仅需 2GB 和 3GB 内存即可运行，而且还能通过 Mix-n-Match 方法灵活调整模型大小，满足不同场景的需求。

- Gemma 3n 提供了多种部署选项，包括 Google GenAI API、Vertex AI、SGLang、vLLM 和 NVIDIA API Catalog 等。
  - 此外，Gemma 3n 还与 Hugging Face、Google AI Edge、Ollama、MLX 等多种工具和平台无缝集成，让开发者可以快速上手，轻松集成到现有项目中。

- ### [Difference between Gemma and Gemini - Marvik _202407](https://blog.marvik.ai/2024/07/03/difference-between-gemma-and-gemini/)
- While Gemma is open source and lightweight, Gemini is proprietary and heavyweight. 

- ## [如果本地要装大模型，建议哪个开源大模型？ - 知乎](https://www.zhihu.com/question/653255605)
- ollama原始的版本是并不兼容 OpenAI 格式的请求，因此在使用比如 langchain、llamaindex 等框架的时候，会遇到一些麻烦的地方，需要再转化下。
  - 现在，更新到新版本的时候，就提供了 OpenAI 格式的接口调用
  - 目前这个 OpenAI-compatible API 还处于测试阶段，并不支持 function calling 的功能。

- 我本地ollama跑一张P40/24G显存，玩了一年多了。我一般跑量化过的32B的模型，再往上速度太慢或者量化太狠，都没太大实用价值。

- 看你显存大小适合多少B的模型。评估时候要考虑量化int4、int8还是float16。可以利用huggingface上的计算器评估 https://hf-accelerate-model-memory-usage.hf.space
  - 除了ollama官方列表 也可以去找hugging face上量化好的模型。
- ollama是基于llama.cpp, 所以也可以基于llama.cpp 自己折腾一遍，从转换模型为gguf到量化为int4 还是int8，可以按照我之前写的教程自己走一遍，可玩性更强一点。我电脑mac m1 跑通义千问的7b的int4量化模型，大约每秒12个token。

- 非专业人士的话，ollama和localai，这两无脑部署运行。同时这两不局限你有没有GPU，cpu也可以搞。

- 太小的模型，想1.5b大小的，性能肯定差一些，不过结合rag这些，实现本地知识库也差不多了。做实验，正常还是用7b左右的。

- 自己本地搭建的数据量太少了，联想关键词困难

- ## [目前有什么可以本地部署的大模型推荐? - 知乎](https://www.zhihu.com/question/648879790)
- 开源大模型更新迭代太快，今年刚推出的模型可能过几个月就过时了。
- 一是如何找到最新的大模型，
  - huggingface可以理解为对于AI开发者的GitHub，提供了模型、数据集（文本|图像|音频|视频）、类库（比如transformers|peft|accelerate）、教程等。
  - huggingface有时存在网络不稳定的问题, 这里推荐国内比较好的平台modelscope
- 二是如何判断本地硬件资源是否满足大模型的需求，
  - 本地可以部署什么大模型，取决于你的硬件配置（尤其关注你GPU的显存）。
  - 在没有考虑任何模型量化技术的前提下： 公式：模型显存占用（GB） = 大模型参数（B）*2
  - 在4bit量化的情况，满足本地机器GPU显存（GB） >= 大模型参数（B）/2，可以尝试本地部署。
- 三是如何快速部署大模型。
  - ollama pull llama3

- 我说的本地，指的不是一台个人电脑上，跑一个7B、13B参数的大模型。而是在企业本地算力服务器上，私有化部署的700亿参数以上规模的大模型，这种参数规模的大模型，才有更好的指令依从性，结合RAG、Agent等技术，能有效的完成你分配给他的任务。 
# discuss-model-file-formats ⚖️ 
- ## 

- ## 

- ## 

- ## There are two FP4 formats circulating right now: MXFP4 and NVFP4 (NV for Nvidia).
- https://x.com/awnihannun/status/1961500133990043967
  - Both formats quantize weights to 4-bit floating point (e2 m1) with a unique scale per group. 
  - The difference is the group size and how the scale for each group is encoded. 
  - MXFP4 uses an e8m0 scale (fixed-point, 8-bit) with a group size of 32. It gets raised to the power of 2 before multiplying the weight. 
  - NVFP4 uses an e4m3 (fp8) scale with a group size of 16. It is multiplied with the weight directly
  - The scale encoding in MXFP4 is pretty suboptimal because it doesn't have representations for a lot of values in the range we need.

- ah, the eternal battle of formats. MXFP4 might be the underdog, but NVFP4 sounds like the crowd favorite. Just wait till someone tries to quantify their existential dread, then we'll really see some innovation. 

- ## [Why does it seem like GGUF files are not as popular as others? : r/LocalLLaMA _202511](https://www.reddit.com/r/LocalLLaMA/comments/1ood0kn/why_does_it_seem_like_gguf_files_are_not_as/)
  - I feel like it’s the easiest to setup and it’s been around since the beginning I believe, why does it seem like HuggingFace mainly focuses on Transformers, vLLM, etc which don’t support GGUF

- It's pretty easy to support gguf, it's honestly weird that they haven't bothered.
  - The issue isn't really the format so much as all the possible quants. There's very little value in "supporting GGUF" if the code can't, say, multiply IQ3_XXS matrices. Supporting all those qants (which can be different per-matrix too, BTW) adds code complexity and can make optimizing difficult.
  - Also, I believe that GGUF doesn't support FP8 and only somewhat supports FP4. (IIRC some tenors are forced to FP32 in GGUF, but that might be wrong.) So for an engine is focused on only providing GPU floating point inference supporting gguf would be silly since it would basically be the bf16 .safetensors but worse.

- My guess because large scale inference providers need efficient inference for a multi-user environment and only care about GPU inference, and vLLM provides that. As of transformers, it is much easier to add support for new architectures there in most cases.
  - So, implementation complexity to support GGUF is generally higher. Vision models and Qwen Next are good example when it takes a while to get support for GGUF.
  - the main reason why I use GGUF is because `ik_llama.cpp` is good for CPU+GPU inference for a single user.
  - I am sure it will get there in time, but the point is, adding GGUF support is very hard, and requires either hiring professional programmer(s) or relying on the community to implement the support themselves.

- Transformers is going to be running the original, unmodified model; it was trained, tested, etc for this experience. You're getting the purest experience.
  - GGUF is a conversion to make it more compatible for the rest of us. The way inferencing occurs, there is a possibility of differences between gguf and the original intended experience, and also a possibility of speed differences as well.
  - ggufs are VERY popular amongst individual users and runners, and folks with limited/specific hardware. But if you're serving to other users, and you have the base hardware expected for Transformers, then you're probably doing that.
# discuss-mac-mlx 🍎
- ## 

- ## 

- ## 

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
# discuss-llama.cpp
- ## 

- ## 

- ## 

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

# discuss-lmstudio-roadmap
- ## 

- ## 

- ## [Phi 3.5 Vision Instruct Fails to Load "Trust remote code" error · Issue · lmstudio-ai/mlx-engine _202411](https://github.com/lmstudio-ai/mlx-engine/issues/29)
- 👷: If you're seeing a `Trust remote code` issue, it means that the model is not (yet) supported by `mlx-engine` . Specifically, support for that model's tokenizer and/or config has not been merged into huggingface transformers.
  - We choose to block loading a model instead of enabling remote code because we are wary of letting users download and run potentially malicious code.

- [when load mlx-community/Kimi-VL-A3B-Thinking-4bit, it prompts trust_remote_code=True. · Issue #607 · lmstudio-ai/lmstudio-bug-tracker](https://github.com/lmstudio-ai/lmstudio-bug-tracker/issues/607)
- 
- 
- 
- 
- 

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
# discuss-lmstudio
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
# discuss-ollama-roadmap
- ## 

- ## 

- ## 

- ## [FR: Meaningful names of models in models/blobs dir _202501](https://github.com/ollama/ollama/issues/8466)
  - Please make models to have meaningful filenames (like user/modelname-quantization.gguf) in models/blobs directory, so they can be (easier) used with other model inference software.

- The blobs are content addressable which means that if you have two or more models which share the same content they will share the same blob which saves space on your disk and also means you don't have to pull down that data if you already have it. The format is also changing with the new engine though so it probably won't be useful with other tools unless they support the new format.

- You use less disk space because the many of the quantizations of the tensors share the same tensors.

- ## [MLX backend · Issue · ollama/ollama _202312](https://github.com/ollama/ollama/issues/1730)
- Add mlx-vlm backend also.

- Lack of MLX support is the only reason I don't use Ollama. In some cases MLX Q8 is 20% faster than GGUF, and memory usage is better handled.

- 📡 [Draft MLX go backend for new engine by dhiltgen · Pull Request · ollama/ollama _202502](https://github.com/ollama/ollama/pull/9118)
# discuss-ollama

```sh
# ollama原始的版本是并不兼容 OpenAI 格式的请求
curl http://localhost:11434/api/chat -d '{
  "model": "gemma3:4b",
  "messages": [
    { "role": "user", "content": "why is the sky blue?" }
  ]
}'
# 模型响应输出如下 
{"model":"gemma3:4b","created_at":"2025-07-31T16:54:00.804772Z","message":{"role":"assistant","content":"That"},"done":false}

```

- ## 

- ## 

- ## 

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
# discuss-janai-roadmap
- ## 

- ## 

- ## [idea: MLX support · Issue · janhq/jan _202506](https://github.com/janhq/jan/issues/5485)
  - Jan does not currently support MLX as an inference engine
- Once we finish with the llama.cpp extension, I think supporting MLX won't be too difficult. We already bundle `uvx` with Jan.

# discuss-janai
- ## 

- ## 

- ## 

- ## 🆚 [LM Studio no new runtimes since weeks..? : r/LocalLLaMA _202510](https://www.reddit.com/r/LocalLLaMA/comments/1o4m7yt/lm_studio_no_new_runtimes_since_weeks/)
- Given Jan is actually open source and development is progressing more rapidly AND it's consistently more up-to-date, I don't see a reason to use LM Studio anymore other than nostalgia.
  - Do you know why Jan lags behind in making the latest models accessible through their model hub? GOtta give it to LM Studio for their super neat integration that lists models as soon as they appear on HF, whether you can run them or not...

- LM Studio gets kickbacks for promoting certain models in their model hub. For example, OpenAI paid them to promote the GPT-OSS rollout and it was one of the largest chunks of money they've ever made for anything they've ever done.
  - So Jan doesn't care as much about funneling people to their "hub" to download specific hand-picked models. I agree it's something LM Studio does much better and Jan could do better though. Until Jan allows actual search of Hugging Face and a similar compatibility screen to help new users, it will continue to be worse in this area.

- I was one of the first supporters of Jan and love to hear those great news. I saw that it is possible to import .ggufs into Jan, but with super large models such as GLM-4.6 that I downloaded through LMStudio, it is split into three .gguf files. Do you know how I can reuse them instead of re-downloading them?
  - cat model.gguf-split-a model.gguf-split-b model.gguf-split-c > model.gguf
  - [or on windows powershell] Get-Content model.gguf-split-a, model.gguf-split-b, model.gguf-split-c -Raw | Set-Content model.gguf -NoNewline
- If they're legitimately split models, I don't think that works. That method was for manual split.

- ## [Is it possible to use Jan AI server instead of LM Studio server in Obsidian Copilot? : r/LocalLLaMA _202409](https://www.reddit.com/r/LocalLLaMA/comments/1f5vswt/is_it_possible_to_use_jan_ai_server_instead_of_lm/)
- You could also try changing Jan port to 1234 to attempt to use original (unchanged) LM Studio option. If Obsidian doesn't use any uncommon API features, maybe it could work.

- Yep, there's a local API server. In the left ribbon, click the icon right above settings. Turn on the server. Visit: http://127.0.0.1:1337 to verify (there should be an api playground)
  - Make sure you are on v0.5.3+

- ## [Jan vs LM Studio : r/LocalLLaMA _202503](https://www.reddit.com/r/LocalLLaMA/comments/1j7qol7/jan_vs_lm_studio/)
- LM studio does have Rocm support, but only for RX6800 or higer or newer variants(7600, 7600XT, 7800....).
- I recommend you to stay with LM Studio, which responds more quickly to newer models than other frontends. Jan was just a full of frustrating experience as I tried it.

- Check settings in Jan i think it doesn’t offload all layers to gpu fully by default

- ## [Jan. AI with Ollama (working solution) : r/LocalLLaMA _202507](https://www.reddit.com/r/LocalLLaMA/comments/1lsoflk/janai_with_ollama_working_solution/)
  - I already have lot of downloaded local llms in my system via ollama.

- Go to Settings > Model Providers
  - Click OpenAI
  - In API Key field add `ollama` as api key & in Base URL enter `http://localhost:11434/v1` equivalent endpoint.
  - In Models list you can see many already available models of OpenAI you can keep it or delete it (but it's optional)
  - In Models there is and option to add new model (there is plus icon), so click on it and add you local ollama model name in my case it was `qwen2.5-coder:14b` (to see available models with exact name run ollama list command in terminal)

- ## 🎯 [Jan now auto-optimizes llama.cpp settings based on your hardware for more efficient performance : r/LocalLLaMA _202510](https://www.reddit.com/r/LocalLLaMA/comments/1nvzeuh/jan_now_autooptimizes_llamacpp_settings_based_on/)
  - It works with Mac too! Although it is still experimental, so do let us know how it works for you.
  - We don't support MLX yet (only gguf and llama.cpp), but we will be looking into it in the near future.

- Can the Jan server serve multiple models (swapping them in/out as required) similar to Ollama?
  - You can definitely serve multiple models similar to Ollama. Although the only caveat is that you would also need to have enough VRAM to run both model at the same time also, if not you would need to manually switch out the model on Jan.
  - Under the hood we are basically just proxying `llama.cpp` server as Local API Server to you with an easier to use UI
- The manual switching out of the models is what I’m trying to avoid. It would be great if Jan could automatically swap out the models based on the requests.
  - We used to have this, but it makes us deviate(背离, 偏离) too much away from llama.cpp and make it hard to maintain, so we have to deprecate it for now.
  - We are looking into how to bring it back in a more compartmentalize way, so that it is easier for us to manage. Do stay tune tho, it should be coming relative soon!
- I believe this is what llama-swap does?

- What is the use case for a chat tool without RAG? How is this better than the llama.cpp integrated Webserver? 
  - Jan supports MCP so you can have it call a search tool for example
  - It can reason - use tool - reason just like chatgpt
  - As for the use case, it's the only open source AIO(All-In-One) solution that nicely wraps llama.cpp with multiple models
- You can actually run MCP that search your own files too! A lot of our user do that through Filesystem MCP that come pre-config with Jan
  - Any file over 5MB will flood the context and become truncated. It is not an alternative. 

- RAG is definitely on our roadmap, however, like other user has pointed out, implementing RAG with a smooth UX is actually a non-trivial task. A lot of our users don't have access to high compute power, so balance between functionality and usability has always been a huge pain point for us.

- I really wish Jan would be a capable RAG-system (like GPT4all) but with regular updates and support of any gguf-models (unlike GPT4all).

- What “All-In-One” practically means for Jan
  - Runtime + engine: includes llama.cpp (local inference) plus cloud provider options so you can run models locally
  - Model management / hub
  - UI: chat UI, model hub, model settings, downloads
  - Tool / integration layer: supports MCP
  - Server/API & multi-tenant features

- Does it support multi-GPU optimization?
  - Yes, it does!
  - It does handle multi-GPU setups, but not automatically yet. 
- I found the optimizer doesn't check if the model fits in a single GPU without layer offloading to CPU. It should put -1

- Does Jan allow one to create their own agents and/or agent routing?
  - Not yet, but soon! Right now, we only have Assistant, which is a combination of custom prompt and model temperature settings

- ## 🎯 [Jan now runs fully on llama.cpp & auto-updates the backend : r/LocalLLaMA _202507](https://www.reddit.com/r/LocalLLaMA/comments/1mdy1at/jan_now_runs_fully_on_llamacpp_autoupdates_the/)
  - Jan v0.6.6 is out. Over the past few weeks we've ripped out Cortex, the backend layer on top of llama.cpp. It's finally gone, every local model now runs directly on llama.cpp.
  - Plus, you can switch to any llama.cpp build under Settings, Model Providers, llama.cpp (see the video above).
- We had different plans for Cortex, that's why we insisted on keeping it for a while, but maintaining it with the new plans became pretty tough. It just made more sense to support llama.cpp directly instead of going through an extra layer.
  - Well I'm glad the team changed direction. This more polished, cleaner, leaner, faster way of Jan development is bound to result in great progress!
- Cortex was the engine behind Jan. It ran on llama.cpp and worked kind of like an alternative to Ollama. We used to update it whenever llama.cpp got updated. Since we've changed our plans, we removed it with Jan v0.6.6.

- I see that the Linux version became 850MB lighter. Is that because of the Cortex removal?
  - Yes, Cortex removal is part of it. We also trimmed down the app by moving out unused dependencies like CUDA 11/12 and extra llama.cpp builds. 
  - Jan now fetches the right llama.cpp version after install, so no need to be bundled in the app itself, which makes the download much lighter
- Although it would be great to keep at least 1 version of llama.cpp, so the install would be portable.

- Does Jan allow selectively offloading model tensors to CPU? (For MoE models) If yes, I would migrate from LM Studio to Jan just for that!
  - oh - not yet, but we're adding it to the roadmap. Thanks for the request!
- this is the killer feature all the slick frontends are missing.

- Allowing ik_llama as a backend would be cool too!

- Llama cpp has so many options, there really should be a "custom arguments" option (input field that gets passed through to llama).

- Koboldcpp have this feature iirc

- Would be great if we could also use llama.cpp forks such as ik_llama.cpp or the Unsloth fork
  - llama.cpp forks: Each fork comes with its own changes, and integrating them cleanly would add a lot of maintenance overhead. We're keeping an eye on where things go, but sticking with official llama.cpp keeps Jan more stable for now.

- MLX support has been on the table for a while... it's something we revisit from time to time. We made several roadmap changes around it, but no final decision yet

- ## 🏠 [Jan got an upgrade to v0.6.0: New design, switched from Electron to Tauri, custom assistants, and 100+ fixes - it's faster & more stable now : r/LocalLLaMA _202506](https://www.reddit.com/r/LocalLLaMA/comments/1lf5yog/jan_got_an_upgrade_new_design_switched_from/)
  - [Release 0.6.0 · menloresearch/jan _20250619](https://github.com/menloresearch/jan/releases/tag/v0.6.0)
  - Switched from Electron to Tauri for lighter and more efficient performance
  - You can create your own assistants with instructions & custom model settings
  - Fully redesigned UI

- Tauri helps us bring Jan to new platforms like mobile. It's also lighter and faster, which gives us more room to improve performance in upcoming updates.
  - Tauri allows us to reuse our existing React and JavaScript codebase, which helps us move faster while keeping the design clean and modern. 
  - Qt and similar native toolkits don't integrate well with the web stack.

- Wails doesn't support mobile, and we're planning to bring Jan to mobile too - so we went with Tauri.

- As someone who is finalizing a port of a small app (atv-desktop-remote) from electron to tauri: If most of your code is in the renderer, the transition is easy. If you have lots of stuff in main.js, you’ll need to reimplement that in rust. The IPC line is still there (between main and renderer processes), you can move stuff around if you need to.

- what makes Jan different from / better than LM Studio? It seems you have same backend and similar frontend?
  - Jan is open-source 
  - We're experimenting with MCP support using our own native model, Jan-nano that outperforms DeepSeek V3 671B in tool use. It's available now in the Beta build.

- Been looking for some opensource UI for openrouter for a long time. It looks very promising, but I haven't figured out how to output reasoning yet.
  - reasoning output isn't supported yet - it's still on the todo list to check.

- Can we edit the responses?
  - No, you can't. why do you want to edit the responses?
- That's an easy way to steer the story in the direction you want it to go. Say, you draft a chapter and ask the model to develop the story; it starts well, but in the middle of generation makes an unwanted twist, and the story starts going in the wrong direction. Sure, you could just delete the response and try again, or try editing your prompt, but it is much, much easier to just stop generation, edit the last line of text, and hit "resume". So, editing AI responses is a must-have for writing novels.

- Jan supports OpenAI-compatible setup for APIs. So if it's empty, it won't work, even if the remote endpoint itself doesn't require one. We should add a clearer indicator for this, but in the meantime, try entering any placeholder key and see if that works.
  - Plus, Ollama doesn't support OPTIONS requests on all endpoints (like /models), which breaks some standard web behavior. We're working on improving compatibility.

- Jan doesn't work with Ollama llms out of the box is my biggest grip . Still unable to add ollama to Jan. Anyone succeeded?
- can it be used with lmstudio ?
  - i tried it and it doesnt work. not sure which one is wrong
  - jan is using OPTION request to list model while lmstudio only serve /v1/models on GET

- When using Ollama if the model does not fit in my GPU it will use the GPU and offload to the CPU but the same did not work with jan.
  - you can update the number of GPU layers manually in model settings (Model Providers -> llama.cpp).
  - We're planning to add automatic GPU offloading soon, once it's merged upstream in llama.cpp

- Please add MLX as a future inference engine

- The app is huge in size. I thought Tauri didn't ship the whole browser.
  - Totally fair. The app's size is due to the universal bundle - we're working on slimming it down soon.
  - Universal bundle on Mac means the app includes native code for both Apple Silicon & Intel Macs, so it's basically twice the size.

- I love Jan! Is there an option for it to autostart on boot with the API server enabled? I couldn't find any way to do that with the previous versions of Jan so I went with LM Studio for my backend unfortunately.

- Jan doesn't support chatting with files or image generation yet. We're going to add chatting with files feature soon. As for image generation, it's not available right now - we'll take a look at it as well.

- What do you feel differentiates your app from all the others? I keep downloading chat apps and they all pretty much offer the same functionality and interface. What is Jan's approach for separating yourself from the herd?

- Is chat history formatted into some portable standard?
  - We're using the same format as previous versions. It loosely follows OpenAI's thread structure but isn't a strict match. It's extension-based, so it can be replaced or exported to other formats if needed.

- on Linux Tauri uses WebKitGTK for now, so performance isn't as good as Chromium. We're refactoring to reduce app size, and once that's done, we'll look into bundling a better browser. Tauri gives us flexibility there, unlike Electron.

- ## [Cortex.cpp: llama.cpp Engine · menloresearch/cortex.cpp _202409](https://github.com/menloresearch/cortex.cpp/discussions/1156)
- We submodule llama.cpp
  - How we handle different llama.cpp versions (e.g. AVX, CUDA etc)
  - Documents which llama.cpp versions we bundle into Cortex/Jan
  - Switching logic for CPU/GPU inference

- ## [Are people not using JAN a lot? : r/LocalLLaMA _202408](https://www.reddit.com/r/LocalLLaMA/comments/1eza2kl/are_people_not_using_jan_a_lot/)
- I think that Jan still lacks a lot of “nice haves” that are present in LM Studio
  - Built in RAG support

- I'm Emre from Jan. Really appreciate this post - it's going to be super helpful as we keep improving Jan! Let me share a few things we're working on:
  - Improving Jan's performance across different hardware (with a new engine that is compatible with various hardware)
  - Revamping the new model hub, providing better
  - Experimenting with something that we'll share soon in homebrew.ltd, our R&D lab which is also the company behind Jan.
- Responding only to features and ideas without addressing the questions of struggling users is called exploitation(广告，宣传).

- Jan has a lot of potential, but is let down by its model management when it’s not the server. Please invest in Ollama and OpenAI compatible APIs. Jan has a lot of potential but not being able to simply connect to your server and select models from a list makes it a pain to use when you already have Ollama / OpenAI compatible servers other clients use.

- I don’t know if Im Studio has it, but I am waiting for tts and stt support in Jan. As for the online based tts it would nice to have different options like elevenlabs, oai whisper, google tts, amazon poly etc For a local tts it would be cool to have at least something that is friendly to limited hardware like piper.
  - Msty for example has implemented stt in the meantime. They just use oai‘s whisper api.

- It's probably due to the "competition" from other excellent easy-to-use software such as Koboldcpp, LM Studio, Ollama, etc. Additionally, Jan has historically been lacking in some functionality that the alternatives have. Maybe this is not the case anymore, as it was a few months ago I last tried Jan.

- I love using JAN but there are a few things that made me switch to openwebui.
  - First I need a more robust API. Running the same time as my threads. Why does it not let me chat in threads if I turn on the API? 
  - I also tried to do some simple things like get the currently loaded model and swap the loaded model for another one. I still have not been able to do this.
  - Why is there so many manual steps involved in adding a model that is not included in the hub? Can't we just provide the huggingface link and it pull the info it needs?
  - I could not find a way to add a custom extension. I want to add image generation using SearmUI. But I don't think I'm able to create extensions yet.
  - I would really love to come back to Jan but the features I need are already there on openwebui.

- JAN is poorly build and thought out unfortunately. 
  - They really need to address support of already existing GGUF models, new quantization types (IQ quants), proper and easy ways to switch prompt/system messages and have presets for things like ChatML, LLama 2/3/3.1, Mistral, etc.
  - Also things like longer context, Flash Attention, KV Cache, More useful debugging/error messages and proper Apple Silicon support is needed badly.
  - It generates a bunch of random and weird output on a lot of new models and quant types.
  - It's too bad that after all this time it is still very buggy and clunky.. I had high hopes for it

- jan has stopped supporting the WebUI, so browser functions are not available.

- ## [Jan: An open source alternative to ChatGPT that runs on the desktop | Hacker News _202403](https://news.ycombinator.com/item?id=39782876)
- GPT4All makes it annoyingly difficult to run any other than their "approved" models. I'd like to kick the tires on a whole host of random GGUF quantizations on Hugging Face, please.
  - I use text-gen-ui (Oobabooga) as a back-end and have it run with `--api` to use the front end of my choice.

- ## [Jan: an open-source alternative to LM Studio providing both a frontend and a backend for running local large language models : r/LocalLLaMA _202401](https://www.reddit.com/r/LocalLLaMA/comments/193m27u/jan_an_opensource_alternative_to_lm_studio/)
- A Big problem all these LLM tools have is that they all have their own way of reading Models folders. I have a huge collection of GGUF's from llama.cpp usage that I want to use in different models. Symlinking isn't user friendly, why can't apps just make their Models folder a plain folder and allow people to point their already existing LLM folders to it
  - This is salient(显著的, 突出的) criticism, thank you. At the core, we're just an application framework. We should not be so opinionated about HOW users go about their filesystem.
  - [/pr已合并 - epic: Better files & links · Issue · menloresearch/jan _202401](https://github.com/menloresearch/jan/issues/1494)

- Ollama being the biggest offender, with that fake docker syntax for modelfiles, model import and renaming using sha hashes.

- The Stable Diffusion UI variants also had this problem - until Stability Matrix came along and resolved a number of inconveniences with model management. Wonder if something similar could be viable here too.
  - invokeai 的选择文件也是一种方案

- Its why Koboldcpp just has a file selector popup, it doesn't make sense to tie people to a location.
  - Koboldcpp also has an OpenAI compatible server on by default, so if the main thing you wish for is an OpenAI endpoint (or KoboldAI API endpoint) with bigger context processing enhancements its worth a look.
  - Koboldcpp is a bit of a hybrid since it also has its own bundled QT UI. We also have GGUF support as well as every single version of GGML.

- This is the best example of why LLMs wont replace devs.
  - IMO, work is the tedious processes of begrudgingly implementing common design patterns. 
  - Did anyone building LLM frameworks/dev tools think they'd be building model library browsers drawing from itunes and calibre? If they're smart. How many people used itunes just because it had better browsing/searching than winamp? (Jumping back to hugging face for the model card and details is already less frequent.)
  - We all want different things.

- Is it better to use llama.cpp instead of LM Studio? 
  - Absolutely! KoboldCpp and Oobabooga are also worth a look. 
  - I'm trying out Jan right now, but my main setup is KoboldCpp's backend combined with SillyTavern on the frontend. 
  - They all have their pros and cons of course, but one thing they have in common is that they all do an excellent job of staying on the cutting edge of the local LLM scene (unlike LM Studio).

- It really needs a custom folder and scan directory function to incorporate already available local GGUF files. I also don't understand the weird implementation of needing a config/JSON file for each model. Why not just use the GGUF metadata and filename to determine the proper settings like other apps are doing?
  - local configs give you an ability to override specific parameters for every model - like to have a custom prompt, custom context length, rope settings etc. Without having local configs there would be no such place to put all your overrides. 
  - But of course no inference software should require them by default and should take everything it can from metadata (where applicable). 
  - And generate those Configs automatically only if you change some parameter from its default value.

- it's nice and simple, but as a consequence of being so new it lacks a lot of QoL stuff that I would expect with more mature apps. 
  - Also I find that the app loads/unloads LLM models into the RAM with every query, unlike LLMStudio which leaves it in RAM until you eject the model. I don't know which is better, but I am a bit concerned about that constant load on my computer.

- I don't like ollama. It keeps loading and unloading models Everytime you do Inference.

- It looks to have an openai API compatibility, wonder if I can use oobabooga textgen as a backend

- I am looking for a GUI that lets me set a -ve CFG without hassle. Does this GUI let me do that?

- Is it some kind of electron app bundled with llama.cpp? Can it be used as a web UI over network?
# discuss-vllm

```shell
vllm serve google/gemma-3-270m  --max-num-batched-tokens 32768 --chat-template /Users/yaoo/Documents/opt/configs/llm/chatemplates/template_chatml.jinja

vllm serve RUC-DataLab/DeepAnalyze-8B --max-num-batched-tokens 40000 --max-model-len 28000
```

- vllm处理prompt的典型日志

```log
[entrypoints/logger.py:37] Request chatcmpl-7ada460412e8448999ef5c40b74f9f3d details: prompt: '<｜begin▁of▁sentence｜><｜User｜># Instruction\nthe northwinds excel contains the sales data for

[entrypoints/logger.py:47] Received request chatcmpl-7ada460412e8448999ef5c40b74f9f3d: params: SamplingParams(n=1, presence_penalty=0.0, frequency_penalty=0.0, repetition_penalty=1.0, temperature=0.4
127.0.0.1:55718 - "POST /v1/chat/completions HTTP/1.1" 200 OK
[v1/engine/async_llm.py:360] Added request chatcmpl-7ada460412e8448999ef5c40b74f9f3d
[v1/engine/core.py:880] EngineCore loop active.

[entrypoints/logger.py:76] Generated response chatcmpl-7ada460412e8448999ef5c40b74f9f3d (streaming delta): output: '<Understand>', output_token_ids: [151673], finish_reason: None
```

- ## 

- ## 

- ## 

- ## 🆚 [Is vLLM worth it? : r/LocalLLaMA](https://www.reddit.com/r/LocalLLaMA/comments/1p9t5c8/is_vllm_worth_it/)
- vLLM currently has way too many bugs related to gpt-oss (or even qwen3) and other important features (such as structured outputs). 
  - After trying multiple releases of their official docker images I gave up and moved onto sglang. And oh god I wish I did it much earlier because after an hour of setup it worked like a charm: 3x higher throughout and properly working structured outputs (for both qwen and gpt-oss). 
  - So my advice is to try sglang docker image, key thing is to set the correct reasoning parser and you're good to go

- ## ValueError: To serve at least one request with the models's max seq len (60000), (8.24 GiB KV cache is needed, which is larger than the available KV cache memory (4.00 GiB). 
  - Based on the available memory, the estimated maximum model length is 29056. 
  - Try increasing `gpu_memory_utilization` or decreasing `max_model_len` when initializing the engine.

- ## 🆚 [Has vLLM made Ollama and llama.cpp redundant? : r/LocalLLaMA _202507](https://www.reddit.com/r/LocalLLaMA/comments/1mb6i7x/has_vllm_made_ollama_and_llamacpp_redundant/)
- vLLM: Extremely well optimized code. Made for enterprise, where latency and throughput is the highest importance. 
  - Only loads a single model per instance. 
  - Uses a lot of modern GPU features for speedup, so it doesn't work on older GPUs. 
  - It has great multi-GPU support (spreading model weights across the GPUs and acting as if they're one GPU with combined VRAM). 
  - Uses very fast caching techniques (its major innovation being a paged KV cache which massively reduces VRAM usage for long prompt contexts). 
  - It pre-allocates 90% of your VRAM to itself for speed regardless of how small the model is. 
  - 🐛 It does NOT support VRAM offloading or CPU-split inference. It's designed to keep the ENTIRE model in VRAM. So if you are able to fit the models in your VRAM, then vLLM is better, but since it was made for dedicated enterprise servers it has the downside that you have to restart vLLM if you want to change model.
- Ollama: Can change models on the fly and automatically unloads the old model and loads the new one. 
  - It works on pretty much any GPU. 
  - It's able to do split inference and RAM offloading so that models which don't fit on the GPU will use offloading and still be able to run even if you have too little VRAM. 
  - And it's also very easy for beginners.
- they serve two totally different purposes. Ollama is way better and way more convenient for most home users. And vLLM is way better for servers and people who have tons of VRAM and want the fastest inference. That's it. 
  - I found a nice post where someone did a detailed benchmark of vLLM vs Ollama. The result was simple: vLLM was up to 3.23x faster than Ollama in an inference throughput/concurrency test

- vLLM has become the inference back-end of choice for the corporate world (Red Hat has based RHEAI on it). Because of that, hardware companies with a vested interest in making inference work well on their hardware have poured engineering-hours into making it maximally performant for corporate use-cases. It seems like the obvious back-end in which to invest one's time and efforts, if one expects to develop corporate LLM applications for a living.
  - Meanwhile, llama.cpp is becoming the swiss army pocketknife of LLM inference, the neatly self-contained do-it-all (with training/finetuning coming back to the project soon). It isn't always the most performant, and it's not great for concurrent inference, but it's very reliable.
  - vLLM by comparison is not very self-contained. It has many sprawling external dependencies, which can make it difficult to get working. 

- Does vLLM support switching models on the fly yet? if not, that’s a very important feature
  - That's a really good question and it seems the answer is no. I read something saying that vLLM is tightly optimized for high-throughput serving of a single model loaded into memory, using shared KV cache and GPU-accelerated paging (which allows it to support very long input contexts while reducing VRAM usage).
  - And that it therefore loads 1 model per instance and cannot switch without restarting vLLM.

- ## [Best frontend for vllm? : r/LocalLLaMA _202506](https://www.reddit.com/r/LocalLLaMA/comments/1ldokl7/best_frontend_for_vllm/)
  - I use LM studio for an easy inference of llama.cpp but was wondering if there is a gui for more optimised inference.

- I've been using text-generation-webui as a combo back-end & front-end since I started with local models over two years ago now, and IMO nothing else comes close as an all-rounder for LLM work. You can also use it as a server, exposing an OpenAI API endpoint to utilize elsewhere if you want to use another front-end or need to make API calls from other programs.

- Been using Lmstudio as well but you could try https://jan.ai/docs as a free open source alternative.

- What we do is build Gradio UIs. Nowadays with LLMs it's super easy to create them and customize them to your liking.

- ## [TIL: For long-lived LLM sessions, swapping KV Cache to RAM is \~10x faster than recalculating it. Why isn't this a standard feature? : r/LocalLLaMA _202511](https://www.reddit.com/r/LocalLLaMA/comments/1olouiw/til_for_longlived_llm_sessions_swapping_kv_cache/)
  - TIL: For long-lived LLM sessions, swapping KV Cache to RAM is ~10x faster than recalculating it. Why isn't this a standard feature?
  - I was diving into how vLLM and similar inference servers work and had a thought about optimizing memory for long-lived but inactive chat sessions. 
  - The standard approach seems to be either keeping the KV Cache in precious VRAM or evicting it and recalculating from scratch when the user returns. I think there might be a better way.
  - Here's the core idea: Implement a swapping mechanism for the KV Cache of inactive sessions, moving it from VRAM to system RAM (and back), instead of deleting it.
  - We always focus on the high cost of moving data between CPU and GPU, but we often forget the cost of recalculating that data.
  - The math is pretty compelling. Swapping is roughly 7-15x faster than a full recalculation. For a user, waiting 200ms for their chat history to "wake up" is a much better experience than waiting 2+ seconds.
  - This wouldn't be for high-throughput, always-online inference, but specifically for managing many long-lived sessions (e.g., support chatbots, document analysis with breaks, multi-user systems with intermittent activity). It's a classic space-time tradeoff, but in this case, using slightly more "space" (system RAM) saves a huge amount of "time" (latency on reactivation).

- i had the same concern op. the cache saving should work. - https://docs.vllm.ai/en/stable/examples/others/lmcache.html?h=lmcache this exists i want to test it with moon shot ai db. i feel like kimi k2 guys uses the same

- Seems to be compatible with vllm now - https://docs.vllm.ai/en/stable/examples/others/lmcache.html?h=lmcache
  - awesome finding! I should have studied better how to Google properly

- It depends on the backend... vLLM has https://github.com/LMCache/LMCache for example (as someone already mentioned here), but it is mostly limited to GPU-only inference.
  - For CPU+GPU inference for a single user, I find ik_llama.cpp to be the best choice though.

- Llama.cpp does not work like that. It evicts cache only you suplly a prompt with no common prefix with what is in cache already.
  - "inactive" in this context means when the VRAM is not enough to store existing pages of KV cache when new requests are coming, with different prompts. As far as I understand this is how vllm works - it just evicts older pages. A sort of LRU ( least recently used ) buffer

- ## [大模型推理框架，SGLang和vLLM有哪些区别？ - 知乎](https://www.zhihu.com/question/666943660)
- PagedAttention vs RadixAttention：内存管理的两种哲学
- 先说vLLM的PagedAttention。
  - 还记得操作系统课上的虚拟内存吗？vLLM就是把这套玩法搬到了GPU上。我第一次看到这个设计时，直接惊了——居然能把内存利用率从20%干到96%
- SGLang的RadixAttention。
  - 用的是Radix树（就是那个压缩前缀树）。
  - 像是给KV cache建了个"族谱"
  - 在多轮对话场景，SGLang确实爽。
  - 部署起来是真的麻烦

- 编程体验：
  - vLLM的API设计，怎么说呢，就是那种"傻瓜式"的（褒义）。三行代码跑起来
  - SGLang的编程模型, 这个DSL（领域特定语言）学习曲线有点陡

- 可是，通常部署都是只作为后端提供 API，而不是答主这样在 Python 里直接加载模型。所以答主的做法比较少见啦。

- sglang不稳定具体指的是？
  - 各种内存泄漏，oom，crash，代码规模不大，就开始屎山堆屎，生产别用，也别追更，merge master基本的回归测试都会直接跳过的。做开源的，就这

- vllm 仅支持 NVIDIA GPU、部署复杂、显存需求大
# discuss-cpu-llm
- ## 

- ## 

- ## 

- ## [llama.cpp and llama-server VULKAN using CPU : r/LocalLLaMA _202511](https://www.reddit.com/r/LocalLLaMA/comments/1ooyr6r/llamacpp_and_llamaserver_vulkan_using_cpu/)
  - llama.cpp and llama-server VULKAN appears to be using CPU. I only noticed when i went back to LM Studio and got double the speed and my Computer didnt sound like it was about to take off.
- First, it doesn't hurt to set ngl 99. Second, cache quantization hurts speed. Other than these two points, I don't know why llama.cpp could get slower than lms.

# discuss-ai-api/tools
- ## 

- ## 

- ## 

- ## [How is Cloud Inference so cheap : r/LocalLLaMA _202601](https://www.reddit.com/r/LocalLLaMA/comments/1q2jwsn/how_is_cloud_inference_so_cheap/)
  - How do cloud inference companies like DeepInfra, Together, Chutes, Novita etc manage to be in profit regarding to the price of the GPUs/electricity and the fact that I guess it's difficult to have always someone to serve ?

- DeepInfra and Together are VC funded. Probably safe to assume they run at a loss for now.
  - Chutes runs on a decentralized network (bittensor), i.e. it's crowdsourced and they pay individual miners.
  - I haven't tried Novita but they're a tiny team of 10 and their blog has some posts about how they optimize e.g. quantization. They're also a little more expensive than the others.

- Scale is more efficient, batching is more efficient, horizontal scaling is more efficient, and a lot of them quantize

- Batching. One gpu can serve hundreds of uses at once. https://artificialanalysis.ai/benchmarks/hardware
- Good God the B200 is a beast!
  - I got a dgx spark and it has the same architecture. I’m getting 600tok/s doing batch inference with qwen3 next 80b. It’s not as good as the big boys but it’s doing batch data classification quite well.

- Inference providers are operating at a loss, hoping that their competitors run out of money before they do. Last man standing wins.

- Data is the new currency.

- same reason the USA is 38 trillion in debt. they built the datacenters to pump corporate profits sheets up. doesn't matter how much money they lose. as long as they are 'winning' uncle sam will cash out. money is about social control. it does not measure resources.

- ## openrouter 是真方便，一个 Key 所有模型都能用。
- https://x.com/pengchujin/status/1894375539726803201
- 模型价格一样，充值 5% 的手续费。还有个好处是有一部分免费模型，比如Az的R1啥的
  - 价格一样的，官方降价他也跟着降
- Qwen的key，火山的key也是这样的

- ## deepseek 最近开源的前面几个项目可能我不了解, 今天这个3fs, smallpond 正好是我们这个行业的, 我理解并没有像技术炸弹吧, 都是比较成熟稳定的技术了
- https://x.com/baotiao/status/1895395027129655691
- y1s1 这里的难点是砍需求，不做什么

- ## DeepSeek 开源周的 5 号炸弹来啦！又是集束炸弹！3FS 和 smallpond！
- https://x.com/karminski3/status/1895280320989274560
  - 我不敢相信DeepSeek甚至颠覆了存储架构...... 我上次为网络文件系统震惊还是HDFS和CEPH. 但这些都是面向磁盘的分布式文件系统. 现在一个真正意义上面向现代SSD和RDMA网络的文件系统诞生了！
  - 飞火流星文件系统（3FS）- 一种利用现代 SSD 和 RDMA 网络全带宽的并行文件系统
  - 这个文件系统可以在 180 节点集群中达到6.6 TiB/s 总读取吞吐量，每个客户端节点 KVCache 查找峰值吞吐量 40+ GiB。
  - 另一个 smallpond（小池塘）是基于 3FS 的数据处理框架！
  - 这个框架由 DuckDB 提供的高性能数据处理，可扩展以处理 PB 级数据集！
  - 我看了下应该还是KV存储的（毕竟面向机器学习），并不是块存储。因此NAS佬还是不太能用得上的。  一致性协议基于CRAQ，毕竟KV存储，基于链式复制的，写操作仍然需要通过整个链，所以写延迟大。但估计其实给训练归档用，写延迟大无所谓。异步归档而已。
- 是文件系统，元数据放foundationdb里，数据放xfs里

- 另外Intel的DAOS其实我感觉做的更极致，直接用SPDK操作裸盘，还利用NVMe-oF技术充分发挥RDMA零拷贝的特性，只可惜元数据系统依赖于NVM硬件，而NVM硬件已经凉凉，DAOS也卖给Dell了

- ceph有object store呀… 头一次见到真的有人用chain replication的…latency不要啦？rdma硬件这么贵直接靠硬件砸吗？
- 数据中心，土豪玩法，颠覆不至于吧

- ## 我才知道 工具调用是个单独的 call 一旦调用其他什么事情都干不了 怎么这个 llm 现在这么草台班子。。。
- https://x.com/Lakr233/status/1894950577416901018
  - 还有 Agent 这种概念，叫全自动编排检索工具使用不好么搞的这么高大上到头来还是 GPT 3.5 就能干的活。。。

- tools 就是一轮新的对话，告诉 AI 可以调这个，然后把调用结果拼接到上一轮对话后面。
  - agent 就是 pipeline/orchestration/scheduler。
  - embedding/RAG 就是 search。
  - LLM framework 就是 HTTP API calls。
- 你这样，PPT还怎么编，团队预算怎么批

- 也有一些异步调用 +event 的玩法, 但是整个 Agent 确实就是建立在无限的文本生成上的
  - Agent = FunctionCall + LLM + LOOP

- 工具调用其他什么事情都干不了指的是？可以并发处理其他问题呀？

- ## 海外大模型接入使用openrouter 已经是最佳实践了嘛？
- https://x.com/leeoxiang/status/1887714022327525797
  1、支持了市面上大部分模型；
  2、可以设置模型的消耗额度；
  3、能支持模型的负载均衡；
  4、支持一套api适配大多数模型；
  5、支持多个模型的失败重试；

- 太贵了！而且特殊模型还是要添加自己的API Key

- ## We ( @jamesmurdza ) have been building Open Computer Use - 100% open source computer use agent.
- https://x.com/mlejva/status/1877054558481813799
  - The agent is using @e2b_dev 's Desktop Sandbox as virtual computer.
  - The agent is using 3 different LLMs: 🔸Llama 3.2 ( @AIatMeta ) 🔸Llama 3.3 🔸OS-Atlas ( @Alibaba_Qwen )
  - It's slow and makes mistakes but this is a big milestone for OS AI community!

- ## 想要部署本地模型但是不会计算 vRAM 占用 
- https://x.com/tuturetom/status/1842492423848804686
  - https://huggingface.co/spaces/hf-accelerate/model-memory-usage

- ## 看来大家终于达成共识了：langchain 是玩具，如果非要在生产环境用它，那它就会变成工业垃圾。
- https://x.com/beihuo/status/1840058205768167699
  - 看这代码比较，langchain 就像一个没有太多工程经验，但是又看了太多设计模式教程的人写出来的东西。使用它来实现一个生产系统，就是一个灾难。
- 同感 longchain构建思维链不如直接按照工作逻辑人工构建思维链。真正的连思维链都不清楚的创造发明，现在用AI来做为时尚早。

- ## 💄 生成式知识 UI 最核心的基础设施，目前围绕此类形态设计的 http://Me.bot 也比较受欢迎
- https://x.com/tuturetom/status/1835349759848333340

- ## Hugging Face 宣布投入 1000 万美元用于免费共享 GPU，旨在帮助小型开发者、学术界和初创公司开发新的 AI 技术，抗衡 AI 进步的集中化。
- https://x.com/glow1n/status/1791488036259434749
  - CEO Clem Delangue 表示，这一举措将通过 ZeroGPU 计划实现，促进 AI 技术的去中心化发展
  - ZeroGPU 使用 Nvidia A100 GPU 设备，提供高效的计算资源。
  - Hugging Face 的 Spaces 平台已有超过 30 万个 AI 演示。

- ## Cloudflare 的 Workers AI 每天可以免费使用 10, 000 Neurons（相当于生成100-200个LLM响应，500次翻译，500秒的语音转文字音频） ，调用方式兼容 OpenAI 
- https://x.com/scomper/status/1791804644332908646
- 好像都是小模型为主吧

# discuss-model-internals/tuning
- ## 

- ## 

- ## 

- ## 

- ## [Which small model is best for fine-tuning? We tested 12 of them by spending $10K - here's what we found : r/LocalLLaMA _202512](https://www.reddit.com/r/LocalLLaMA/comments/1pi8z74/which_small_model_is_best_for_finetuning_we/)
  - TL; DR: We fine-tuned 12 small models to find which ones are most tunable and perform best after fine-tuning. Surprise finding: Llama-3.2-1B showed the biggest improvement (most tunable), while Qwen3-4B delivered the best final performance - matching a 120B teacher on 7/8 tasks and outperforming by 19 points on the SQuAD 2.0 dataset.
  - 12 models total - Qwen3 (8B, 4B, 1.7B, 0.6B), Llama (3.1-8B, 3.2-3B, 3.2-1B), SmolLM2 (1.7B, 135M), Gemma (1B, 270M), and Granite 8B.
  - Tested on 8 benchmarks: classification tasks (TREC, Banking77, Ecommerce, Mental Health), document extraction, and QA (HotpotQA, Roman Empire, SQuAD 2.0).
  - I guess the title is a little click-baity. To get the total number, you have to account for the synthetic data we generated for each benchmark. That's the reason we could easily scale the training to many tasks and domains.
  - You are right that the training itself was not 10k, but running the whole pipeline adds up to the number. We didnt think that _that_ would be the main discussion point.

- i did this test back then with qwen 2.5 models for our work project, and interally we found that qwen2.5 7b was the most consistent model with the best result for its size, where the 2.5 3b had issues following instructions at times. did the qwen 3 4b model ever had this happen or was it able to execute all tasks without fail?
  - I wouldn't say "without fail", it's definitely not perfect, but it's pretty good at following instructions overall. On some tasks there was little difference between the 8B & 4B Qwen3 models (the harder the task, the more important param count is).

- Can this also apply to VL models? Qwen3 VL personally.
  - Not yet, but doing this same for vision models is on our roadmap!

- The Qwen team hit it out of the park with Qwen3-4B-Instruct-2507. This model keeps coming up all over the place and it deserves the praise it gets. I hope whatever secret sauce they used for that model is further propagated to their other models. Actually what I really would like is a deep dissection and a full whitepaper on why the hell this little model hits so much above its belt.

- I recommend strongly HuggingFaceTB/SmolLM3-3B. Got the same perfs as Qwen3-4B-Instruct-2507 for my task but with faster inference 

- [Which small model is best for fine-tuning? We tested 12 of them by spending $10K - here's what we found : r/LocalLLM](https://www.reddit.com/r/LocalLLM/comments/1pi98l9/which_small_model_is_best_for_finetuning_we/)

- ## [Convert Dense into MOE model? : r/LocalLLaMA _202512](https://www.reddit.com/r/LocalLLaMA/comments/1pfxrv5/convert_dense_into_moe_model/)
- Contrary to many of the other answers here, it's definitely possible but usually not worth the trade-offs.
  - The thing is, you are better off using a model that was trained from scratch to be an MoE (since MoE are cheaper to train anyway) or just using a smaller dense model with more predictable performance.
  - They were able to convert a dense Llama model into an MoE with 25% activation and still have non-trivial performance without any retraining (and of course it does better with retraining). However, the MoE is not nearly as good as the original dense model.

- ## [In light of Kimi Linear, reposting Minimax's article on Linear Attention : r/LocalLLaMA _202511](https://www.reddit.com/r/LocalLLaMA/comments/1oorvd0/in_light_of_kimi_linear_reposting_minimaxs/)
  - MiniMax M2 Tech Blog 3: Why Did M2 End Up as a Full Attention Model?

- until we have some gated delta net models with way more active parameters, i don't think we can really come to any solid conclusions right now. gpt-oss is 100% transformer and also sucks the same way as these really sparse hybrid models.

- Feels like "You never really know what’s going to happen until you scale up." might be one big reason why qwen will keep with Next type models for the time being. The reasoning could have been: their some performance penalty at inference, but for the gpu/time cost of one 32b dense, we can train 10+ different "good enough" 80b hybrid MoE. Allows us to iterate faster, detect issues faster, experiment more (more parameters? more experts? different training methods?). All of which could benefit full attention down the line.

- ## [What’s the training cost for models like Qwen3 coder 30b and is the code for training it is open source or close source? : r/LocalLLaMA _202509](https://www.reddit.com/r/LocalLLaMA/comments/1njws3n/whats_the_training_cost_for_models_like_qwen3/)
- You can do fine tunes on the 4B real easy with Unsloth. LoRAs and QLoRAs, too. It won’t take much VRAM. You can fine tune a LoRA for Qwen3 30B A3B Instruct 2507 in BF16 on a single 96GB 6000 Pro in just a few hours.
  - That depends entirely on what you are training and the size of your dataset. True fine tuning, on a really small dataset will take a few hours, but if you are trying to train in new capabilities, that is going to take a much larger dataset, and could be months or over a year on a single RTX pro 6000.

- Their exact code isn't open source, but many companies train using Pytorch and Megatron-Core open source code.
  - I estimate GPU-time needed for training Qwen 30B A3B to be around 800 000 hours for H100 SXM5, so around 1.6 million dollars. That's for pretraining on 20T tokens, assuming 40% MFU.

- Stick to finetunes, you don't have the hardware or budget to pretrain models of practical size (believe me I have tried).
# discuss-terminal/fs
- ## 

- ## 

- ## 

- ## Introducing SQLite-Agent, a groundbreaking SQLite extension that allows your database to run autonomous AI agents directly inside SQLite itself. _202512
- https://x.com/_marcobambini/status/2000599613271892369
  - With SQLite-Agent, your data becomes active: agents can read, reason, act, and write back results without leaving the database engine. This turns SQLite into a fully self-contained automation and intelligence platform for apps, devices, and edge environments.
- https://github.com/sqliteai/sqlite-agent /c
  - A SQLite extension that enables SQLite databases to run autonomous AI agents, using other SQLite AI extensions. 

- ## at @llama_index we came up with 𝗮𝗴𝗲𝗻𝘁𝗳𝘀-𝗰𝗹𝗮𝘂𝗱𝗲, a small demo that combines @claudeai and AgentFS by @tursodatabase with our Agent Workflows  _202512
- https://x.com/itsclelia/status/2000623632629002579
  - to create a harnessed and secure environment where the agent can perform all operations in a virtual filesystem without affecting your real one
  - Coding Agents are great, but giving them unfiltered access to your filesystem might be a very bad idea
  - Bonus: we also gave the agent understanding of unstructured documents, by parsing them with LlamaParse

# discuss
- ## 

- ## 

- ## 

- ## 🆚 [[Experiment] Three identical Qwen2.5:7b runs, three distinct behavioral strategies. One hit max reported metrics and started failing to execute actions. [Full data + code] : r/LocalLLaMA _202510](https://www.reddit.com/r/LocalLLaMA/comments/1obkn0d/experiment_three_identical_qwen257b_runs_three/)
- 
- 
- 

- ## 🧩 [Qwen3-30B-A3B 2507 Instruct vs Thinking : r/LocalLLaMA](https://www.reddit.com/r/LocalLLaMA/comments/1o8529x/qwen330ba3b_2507_instruct_vs_thinking/)
- My understanding is that 
  - GPQA is general knowledge, 
  - AIME25 is Math, 
  - LiveCodeBench is coding, 
  - Arena-Hard is a predictor of how well it will perform at LMArena 
  - and BCFL is about tool calling.

- i'm guessing the t/s will be low if you use CPU (~5t/s) so just use instruct if you don't want to wait like 5 minutes for an answer with reasoning

- Reasoning only helps on logic-intensive tasks. On anything else, it’s a waste of time at best, and can actually make things worse if the chain of thought focuses on the wrong thing.

- ## [Why do people like Ollama more than LM Studio? : r/LocalLLaMA _202501](https://www.reddit.com/r/LocalLLaMA/comments/1icta5y/why_do_people_like_ollama_more_than_lm_studio/)
- I think many of us are programmers, personally I prefer open-source applications. Of course as a programmer, I have no problems with using command line.
- You can search for models using the the website of Ollama. Downloading models is just one command ollama pull `<model_name>` . The same for removing or serving a model.
- And you can use Ollama with HuggingFace GGUF now too.

- Ollama depends on llama.cpp which was created by the guy (Georgi Gerganov) who invented GGUF.
  - Ollama does have its own registry though that stores the GGUF files in its own MODELFILE format.
  - You can use any GGUF with Ollama

- As a programmer I don't understand why more people don't use koboldcpp
  - It was a pain in the ass to get going properly. Also it might be just me, but I couldn't figure out how to serve multiple models at the same time with kobold.
- KoboldCPP seems oriented towards Windows. A lot of programmers are on Mac/Linux. (At least compared to the average population). Sure KoboldCPP seems to work on Mac/Linux. But, the docs are very Windows-centric. And so I'd rather use something more focused on my environment.

- Does llama-server allow serving multiple models at once? I couldn't figure out how to get that going, but it was a killer feature for me since I swap models on a task by task basis.
  - Well, kind of. You can start multiple llama-server instances and have multiple models loaded simultaneously, resources permitting. Otherwise, you can always hot load llama-server in your code.

- I use LM Studio even in production. You can start it as service. When product is new you need to babysit it , testing different params and models in pretty OK in LM Studio. I was using it from 0.1 to new 0.3 , new interface and multi-model support is pretty good.

- you can use ollama commercially without problems. lm studio writes that you have to contact them.

- Headless is a feature not a bug. I'm using multiple frontends to talk to the same server (Tabby, OpenWebUI, custom programs, etc). And, I'm running the inference on a separate machine from where I'm accessing it anyways.
  - Basically, programmers like Ollama, Llama.cpp Server, and other programmer oriented servers and libraries.

- Why don't people talk about OOBABOOGA? It's better than all listed, yes, including LM Studio!
  - Python programs take like 5 hours to install to then fail on some dependency conflict. Then you start again. I used OOBA for a bit but my python env and everything broke with every update.

- For me, the biggest advantage of Ollama is loading models on demand. I have a few automation scripts that use different models, plus it serves OpenWebUI, cline and aider, and dynamic loading/unloading is the way to go for me, otherwise I’d just use pure llama.cpp.

- ## [Are there any better offline/local LLMs for computer illiterate folk than Llama? Specifically, when it's installed using Ollama? : r/LocalLLaMA _202411](https://www.reddit.com/r/LocalLLaMA/comments/1gnjev5/are_there_any_better_offlinelocal_llms_for/)
- LMStudio uses llama.cpp backend on PC, and can additionally use MLX on Mac, so the model selection is somewhat broader on Mac. 
- MSTY uses bundled Ollama and can connect to other servers, including ChatGPT. It will also pick up models already downloaded by another Ollama installation.
- Msty is quite easy to set up and use: https://msty.app/ But which model they run depends on the computer. If necessary need to use some online API service like OpenRouter, which Msty also supports.

- ## [LM Studio vs Ollama vs Jan vs Llama.cpp vs GPT4All : r/LocalLLaMA _202502](https://www.reddit.com/r/LocalLLaMA/comments/1isazyj/lm_studio_vs_ollama_vs_jan_vs_llamacpp_vs_gpt4all/)
- llama-swap, which I use to proxy llama.cpp and koboldcpp.
  - llama-swap provides two important features: on-demand model load/unload; manage the parameters for launching the models
  - I am now able to "save" the way I launch llama.cpp for each model I want to use. I no longer need to keep a CLI open to stop/start llama.cpp or ollama when I want to change models.
- Agree. I started with ollama but slowly shifting towards llama-swap because it's simpler and provides better control over parameters.
  - I know I can create alter parameters in ollama to a great extent but having everything in a single config file is just better.

- LM Studio, mainly because it now has the "Auto unload unused JIT loaded models" feature.

- LM Studio as it just works. I really don’t care about open/closed source. I want something that looks nice and just works well on my hardware.
  - same here. lm studio outperforms ollama anythingllm msty gpt4all in terms of speed and ease and model intelligence actually. I tried them all.
- Until it doesnt and you could do nothing about it.

- Quick note: Cortex powers Jan, and we're adding backend-level features to Jan through Cortex. Once Cortex becomes multi-engine, Jan will also support multiple engines alongside llama.cpp.

- KoboldCpp for obvious reasons, but the main advantages are that its not limited to just instruct models as it also has regular text completion modes. Its a server rather than just a local app so it can be used remotely, and for those that the bundled UI isn't suitable for it can be used with third party UI's trough the multiple API's it supports and emulates.

- GPT4ALL is my favorite on paper, but the devs refuse to fix a big issue with response streaming. I want to couple it with Open WebUI and the responses don't show up.

- Ooba because you can use quantized KV cache with Context Shift (LLM_Streaming). It's a must have if you roleplay and have low VRAM.
  - LLM Streaming to my knowledge is not the same as Context Shift like in KoboldCpp. Context Shift is compatible with things that should stay in memory, it shifts after the tokens that persisted. While traditional LLM Streaming implementations tend to fade out the old bits including context you may need. If I am out of the loop and ooba's implementation does now work like Kobolds feel free to correct me but this was not originally the case.

- LMStudio but their REST API is kinda of restrictive. I use hugging models loaded on ray sometimes for better API functionality. Wish i could try vLLM but not working on windows

- I use llama.cpp, because it is relatively simple and self-contained (not a lot of external dependencies), and something for which I could develop features and maintain.
  - It has the potential to be the "do-everything tool" for LLM technology; 
  - it used to have training and fine-tuning example code, but it was taken out and is in the process of being re-implemented so it can take advantage of any supported back-end (CUDA, SYCL, Vulkan, etc). 
  - The GGUF file format is well thought-out and people are taking good advantage of its metadata features, so you don't have to chase down inference-time parameters from obscure corners of the web.
  - I might be forced to learn vLLM eventually if my employer decides to start using Red Hat Enterprise AI, but until then llama.cpp is all I want or need.

- ## 🆚 [What's the point of OpenUI Web vs Piniochio or Jan.ai? The ladder of which being substantially easier to install : r/LocalLLaMA _202412](https://www.reddit.com/r/LocalLLaMA/comments/1hc20u7/whats_the_point_of_openui_web_vs_piniochio_or/)
- Lmstudio and Jan are examples of kitchen sink LLM apps, they merge model management with backend and frontend.
- OpenWebUI is just a frontend, so it makes most sense for folks that already have both a backend (and thus already have docker, etc all configured) and a way to manage models loaded on that backend.
- There are also several middle grounds:
  - Ollama has backend and model management, but no frontend.
  - Koboldcpp has backend and frontend, no model management.

- The kitchen sinks are a great place to start but if you're wondering what their downsides are: you are stuck to their model management system and whatever quants they support. Batch/multi-user performance is also not a priority for these apps.
  - To pick a concrete example, to my knowledge there's no all in one's support EXL2 and can spin me up a tabbyAPI with tensor parallel and a big context cache. So how easy it is to install doesn't matter to me, vs doing what I want.

- I don't use any of these and instead sometimes have to resort to fixing bugs in python myself in ooga/text-generation-webui, 
  - because I want to use top_a, tail_free or mirostat sampling, use GBNF-grammar restrictions, use DRY penalty, define custom stop tokens or token bias, control the order the samplers are applied, toggle if the BOS token is prefixed or not, edit the Models responses on the fly, change the chat template, adjust the RoPe-scale, choose the quantization datatype, etc...
- Most interfaces have some subset of these but rarely all. Some are pretty stubborn when I want to use the folder where I store all my models and not have them download the model again together with some stupid specific template file.
- text-generation-webui is a pretty crappy(差劲的，很糟的) UI and can be quite the hassle(麻烦, 不方便) to install and update, but the closest feature set relative to writing custom python code using llama.cpp or hf-transformers.

- Simplest "chat to LLM" is llama.cpp's server. The newest release.
  - It's 5 MB in size, has a well-looking web frontend, stores past conversations in browser memory. And is super lightweight and works fast.
- You say "simplest", but... one of these you can just download an app and double click it, and it's not llama.cpp. I have no trouble compiling llama.cpp myself, and I can also navigate HuggingFace to find a good model in the right quant and download that myself, but this is asking a lot of the average person.

- ## [What is your preferred front-end/back-end these days? (Q2 2024) : r/LocalLLaMA _202406](https://www.reddit.com/r/LocalLLaMA/comments/1dad0rh/what_is_your_preferred_frontendbackend_these_days/)
- Personal (single user, power-user) use: SillyTavern frontend, oobabooga's text-generation-webui backend (EXL2, HF). KoboldCpp backend if I need to run a GGUF for some reason (I prefer EXL2 for speed, especially with big contexts).
  - Professional (multi user, end-user) use: Open WebUI frontend, Ollama backend (simple) or vLLM/Aphrodite Engine (fast). Aphrodite Engine is a fork of vLLM that I prefer, supports more formats and is more customizable.
- I like to call SillyTavern the LLM IDE for power users: it gives you complete control over generation settings and prompt templates, editing chat history or forking entire chats, and offers many other useful options. There are also extensions for advanced features such as RAG and web search, real-time voice chat, etc. I love it and use it all the time. Once you learn it, you can use any backend, both local and online.
  - But it's not for everyone. Some just want a ChatGPT alternative, a simple chat interface, and advanced options would just confuse them. That's true for most users who aren't AI developers or enthusiasts, and that's who Open WebUI is ideal for. I run it as a local AI chat interface at work for my colleagues, while I prefer to use SillyTavern myself.

- I currently use koboldcpp for both back and front ends. I love how fast the team integrates upstream llamacpp fixes/additions. Has a multiuser batching function with nice GUI for the Mrs to use, and "just works" no matter what I throw at it.

- jan failed for me with codestral. It never answered back, tried multiple times, and different PCs as well. I can get llama3 8B just fine tho.

- I started with lm-studio but now i prefer librechat as frontend and ollama as backend. Supports pretty much all online apis and ollama. Supports a rag database and search. Is very simple to setup and i dont need to manage all the model setup (ollama just works) im just limited to the available models unless i write a modelfile myself.

- What i didnt like about lm studio but got with librechat:
  - using Local ai and online apis seamlessly in the same chat
  - not have to manage presets to run models correctly and efficiently
  - Search in chats
  - Rag database
  - TTS
- What i miss from using lm-studio:
  - accessing huggingface models directly
  - performance metrics
