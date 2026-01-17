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
# discuss-stars
- ## 

- ## 

- ## 

- ## [Someone needs to create a "Can You Run It?" tool for open-source LLMs : r/LocalLLaMA _202501](https://www.reddit.com/r/LocalLLaMA/comments/1iaubfm/someone_needs_to_create_a_can_you_run_it_tool_for/)
- LM studio, Msty both has info on this before you download.

- You'll never guess who just spent all day making this. https://github.com/Raskoll2/LLMcalc

- Closest thing is this https://huggingface.co/spaces/NyxKrage/LLM-Model-VRAM-Calculator Quantization is just compression, look at the file size + context and see if it's less than your VRAM. If it's less it will run at max speed. If it's more you will need to partially offload, and the speed hit from that depends on how many parameters the model has and how much you're offloading. If you don't care about speed, you can run literally anything of it if it is less than your amount of RAM

- ## [AirLLM make 8GB MacBook run 70B : r/LocalLLaMA _202312](https://www.reddit.com/r/LocalLLaMA/comments/18sj1ew/airllm_make_8gb_macbook_run_70b/)
- They page the model weights from disk.

- The real question is is it noticeably faster than for example llamacpp with a partial offload? Because anyone can make a 70B in 4GB of vram claim if your not placing most of it on the GPU. I know KoboldAI United already had something similar since 2021 but it was just to slow to be any use, and then Huggingface got Accelerate (Which we moved to) which is also basically the same concept of using system memory to swap things in and out of the GPU.

- It's always been possible by reading the model from disk. Just extremely slow. Let's see how fast it is before we get impressed.

- [AirLLM enables 8GB MacBook run 70B LLM | Hacker News](https://news.ycombinator.com/item?id=38790385)
- It's very slow, according to the comments in this thread by people who tried it

- ## [Is it possible to pack LLama into an offline software that you would distribute? : r/LocalLLaMA _202404](https://www.reddit.com/r/LocalLLaMA/comments/1c9kspi/is_it_possible_to_pack_llama_into_an_offline/)
- https://github.com/Mozilla-Ocho/llamafile

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
  - [AMD Strix Halo — Backend Benchmarks (Grid View)](https://kyuz0.github.io/amd-strix-halo-toolboxes/)

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

- ## [Noob question: imatrix, yes or not? : r/LocalLLaMA](https://www.reddit.com/r/LocalLLaMA/comments/1qcfto0/noob_question_imatrix_yes_or_not/)
  - Does it make sense to use imatrix for specialized models (i.e. RP, coding, medical models) or would regular/static ggufs be a better choice for these?
  - In the past I've been told imatrix (including unsloth?) affected things like thinking, so I was wondering if it may actually hurt specialized models.
  - EDIT: To clarify, I know imatrix is better in general. What I'm asking is, if imatrix datasets are generic, the quantization process might actually be overfitting the model on that specific dataset, not sure if that may affect how a medical or coding model works.

- Always use imatrix for all quants (except for Q8). It's "free quality". Here's a perplexity comparison that I made when the feature was introduced. You can see the jumps in similarity to the unquantized model there.
  - I also ran some extensive imatrix dataset tests which show that testing for the best imatrix/quant can be rather difficult. Even an unsuitable imatrix dataset seems better than no imatrix at all.

- Below 3.5 BPW, imatrix Is the only way. When you are about 4 BPW, you can choose.
  - If you are offloading tensors / layers to CPU, It might make sense to pick a static (non imatrix) quant, like IQ4_NL
  - If you have a rtx 3000+ Nvidia GPU and you fit everything on the GPU, it's very likely that IQ4_XS imatrix quant is on par with the static one, so you can pick the static, because all layers tensors use the IQ4_XS quant, which Is more efficient then the Q4_K_S or similar quants.
  - Above 5.5 BPW imatrix Is meaningless, Q6_K, imatrix or static, are the same.
  - Usually, my suggestion Is: Always go for imatrix. Unsloth (files with UD- prefix) or Barto are my fav. The only exception Is when you are using CPU, in those cases, pick static Q4_0 or IQ4_NL, instead of imatrix ones.

- No difference between a q4km, q4ks and ud Q4 xl for my use cases.

- most recommend imatrix quants, but i haven't noticed any differences between them and the normal ones.

- ## 🧩🆚 [Choosing a GGUF Model: K-Quants, I-Quants, and Legacy Formats : r/LocalLLaMA](https://www.reddit.com/r/LocalLLaMA/comments/1q911fj/choosing_a_gguf_model_kquants_iquants_and_legacy/)
  - [Choosing a GGUF Model: K-Quants, I-Quants, and Legacy Formats _202510](https://kaitchup.substack.com/p/choosing-a-gguf-model-k-quants-i)

- Most GGUF weight formats are blockwise.
  - A matrix is split into fixed-size blocks, each block is represented with compact integer parameters, and a small set of per-block parameters reconstructs approximate floating weights at inference.

- Legacy Formats: Q_0 and Q_1
  - The legacy family of GGUF formats, Q4_0, Q4_1, Q5_0, Q5_1, Q8_0, implements classic per-block linear quantization. A block stores n-bit weight codes and either one scale (the “_0” variants, symmetric) or one scale plus one offset/zero-point (the “_1” variants, asymmetric). Dequantization is a single affine transform per block.
  - These formats are simple to decode and therefore fast. Their weakness is representational: one affine map per block cannot model skewed or heavy-tailed weight distributions as well as newer schemes.
  - At 8-bit, the difference is negligible, and Q8_0 is effectively near-lossless for most LLMs. That’s why we can still see a lot of Q8_0 models being published on the HF Hub. At 5- and especially 4-bit, legacy formats leave measurable accuracy on the table compared with modern alternatives.

- K-quants: Modern Default for 3–6 Bits
  - K-quants (Q2_K, Q3_K, Q4_K, Q5_K, Q6_K, and their mixed variants like _S, _M, _L) introduce structure beyond a single affine per block. 
  - The most common pattern is a two-level scheme: small blocks with their own scale and zero-point grouped into a super-block with an additional scale/offset.
  - The result is lower error at the same storage. For example, a typical Q4_K lands around the mid-4s bits/weight—slightly above Q4_0/1 once you count its extra parameters, but it achieves distinctly better fidelity. Q5_K and Q6_K cluster close to the original model in perplexity while remaining far smaller than FP16.
  - On modern CPUs and GPUs, K-quants generally match or beat legacy formats in throughput because you move fewer bytes for the same quality.
  - Keep in mind that for most models, you won’t see much difference in quality between S, M, and L variants, unless you are dealing with small models (let’s say <8B models).

- For very large LLMs, like DeepSeek models, you may also find a TQ1_0 version.
  - TQ1_0 encodes weights that are ternary (values in {−1, 0, +1}) using a compact packing scheme. It lands around ~1.6–1.7 bits/weight depending on packing details.

- I-quants (IQ2_XXS, IQ2_XS, IQ2_S, IQ2_M; IQ3_XXS/XS/S/M; IQ4_XS; IQ4_NL) are purpose-built to hold up at 2–4 bits.
  - They go beyond piecewise-affine by introducing non-linear and table-assisted reconstruction.
  - The pay-off is quality per bit. IQ4_XS typically bests 4-bit K-quants at similar effective size. IQ3_XS and IQ3_M tend to outperform their 3-bit K counterparts.
  - IQ2_* is the frontier that makes very large models fit in places they simply could not before.
  - IQ4_NL is a special 4-bit non-linear variant that also uses smaller blocks. It targets CPU speed while retaining the non-linear benefits.

- IQ4_XS vs Q4_K_M
  - IQ4_XS and Q4_K_M are both “4-bit class” GGUF quantizations, but they trade off size, speed, and robustness differently: Q4_K_M is the reliable default (slightly larger, generally predictable quality/perf), while IQ4_XS is compresses more aggressively (lower effective bits/weight), which can help you fit larger models/contexts and sometimes improve token generation speed, at the cost of being more sensitive to how the quant was produced (imatrix quality; see below) and to your hardware/kernel mix
  - In llama.cpp’s published Llama-3.1-8B numbers, IQ4_XS is ~4.46 bpw / 4.17 GiB vs Q4_K_M at ~4.89 bpw / 4.58 GiB, with IQ4_XS a bit faster for generation but a bit slower on prompt processing.

- IQ4_NL vs IQ4_XS
  - IQ4_NL and IQ4_XS are both llama.cpp “I-quant” GGUF formats aimed at strong quality at ~4-bit, but they optimize different things: IQ4_XS is the more aggressive/compressed option (~4.25 bpw) at the cost of being a bit more sensitive to how the quant was produced. 
  - IQ4_NL is a less compressed non-linear variant (~4.5 bpw) with a different dequantization rule and smaller-block design that’s often described as targeting CPU friendliness/speed while keeping the non-linear benefits.
  - In practice, many community benchmarks report IQ4_NL is very close to IQ4_XS (sometimes within noise), which is why some quant publishers drop IQ4_NL as “redundant” 

- ## [Why not Qwen3-30B Quantized over qwen3-14B or gemma-12B? : r/LocalLLaMA](https://www.reddit.com/r/LocalLLaMA/comments/1q62pyh/why_not_qwen330b_quantized_over_qwen314b_or/)
  - I have a 3080ti with 12GB of VRAM and 32GB of RAM and a 5900x. With this I can run qwen3-30b-a3b-thinking-2507 that does 3.3B activated parameters in LM studio 20 tok/sec which I believe is quantized right? It runs pretty well and has good answers. Why would I use the more recommended ones of qwen3-14b or gemma 12b over this that I see more often recommended for a computer of my specs?

- MoE models will have a higher "static" VRAM cost, so you have less KV-cache -> lower ceiling on parallel requests -> lower total TG. But active parameters are fewer -> so faster compute -> higher total TG.
  - In any case you have to evaluate your usecase; the quality of output and your throughput.
  - For example, if you want more speed and you don't need a lot of KV-cache/context you could try Qwen3-VL-8b at FP8 or lower quant. This will fit into your VRAM.

- The big advantage of MoE, especially for running on consumer hardware, is that the model doesn't have to fully fit into VRAM to give reasonable speed. I find models larger than 8B (active) parameters get really slow on CPU. Qwen 30BA3B or GPT-OSS-20B run quickly even on only CPU since they run as small models, but they're still big enough to be reasonably smart and useful. (And they run really fast with a hybrid GPU/CPU setup, even when they don't fully fit into VRAM).

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

- ## [New functiongemma model: not worth downloading : r/ollama _202512](https://www.reddit.com/r/ollama/comments/1pq69o5/new_functiongemma_model_not_worth_downloading/)
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

# discuss-model-tuning/internals
- ## 

- ## 

- ## [Transformer Lab - Download, interact, and train models locally : r/LocalLLaMA _202402](https://www.reddit.com/r/LocalLLaMA/comments/1awer80/transformer_lab_download_interact_and_train/)
  - We built Transformer Lab to be an open source tool that lets you interact, train, and evaluate LLMs on your own machine or in the cloud (currently Mac or Linux, Windows soon) through a simple GUI.
  - One of our goals is to make it as easy as possible to get started experimenting with LLMs regardless of what platform you have (even if you don’t have a GPU). You can do everything through the UI but it is built on an API that can be extended using plugins. When you start the app it will try to figure out what kind of system you have and install the right set of initial plugins to get you going optimally.
  - Recently we've been putting a lot of effort in trying to make it work really well for folks without a GPU but who have an Apple Silicon Mac and want to finetune models through a GUI.

- Since this is written in electron, will there be an option to host the entire app as a web server in the future?
  - Interesting. We’ve thought about this a bit. Mostly the app is just a plain React app so it could just be a website. It only does a bit of non web work in the installer which could be removed.
  - We chose to make it an app in the hope that it’s easier to install but if people really want a web version it’s something we could work on (or could use help with).

- The core Llama Training library uses the out of the box Hugging Face Trainer library which supports AMD. So at worst, it might require a bit of tweaking to the TrainingArguments when doing training in order to optimize for AMD.

- ## [Looking for a Base Model : r/LocalLLaMA _202601](https://www.reddit.com/r/LocalLLaMA/comments/1q9si66/looking_for_a_base_model/)

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
