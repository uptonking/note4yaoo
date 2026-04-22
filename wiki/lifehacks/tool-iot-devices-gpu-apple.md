---
title: tool-iot-devices-gpu-apple
tags: [apple, gpu, metal-mps]
created: 2026-01-15T15:42:27.356Z
modified: 2026-01-15T15:43:25.456Z
---

# tool-iot-devices-gpu-apple

# guide

# discuss-stars
- ## 

- ## 

- ## 

- ## [Will apple make a macbook pro with an ultra chip? : r/LocalLLaMA](https://www.reddit.com/r/LocalLLaMA/comments/1o8ax0f/will_apple_make_a_macbook_pro_with_an_ultra_chip/)
  - Just imagine 1 tb of ram on a m5 or m6 ultra MacBook Pro? The price will be absurd and the battery will be short? Maybe they will restrict the ram, since it will use more power? 
- It's well known for people that work with computing hardware that RAM requires a lot of power and consumption grows as RAM increases. 
  - The issue is that data in RAM has a short life and has to be refreshed regularly or it gets corrupted/disappears. That's why laptops are always RAM constrained and desktops are not. 
  - There's more to it about scale and speed that requires workstation class machines to get to have extremely large RAM.

- ## 🆚📌 [Memory Bandwidth Comparisons - Planning Ahead : r/LocalLLaMA _202402](https://www.reddit.com/r/LocalLLaMA/comments/1amepgy/memory_bandwidth_comparisons_planning_ahead/)
- Epyc actually has 12 channels of ram. The latest 9004 series has 460.8 GB/s. Threadripper is the one that comes with quad and octa channel variants.
  - Note: The upcoming Epycs(zen 5) are supposed to have even more bandwidth due to the new out-of-the-box ram speed being 6000mhz instead of the current 4800mhz
- 6000 MT/s would be nice, giving 4090-like memory bandwidth over 24 channels in a 2P system, but with a minimum of 384GB instead of a maximum of 24GB. That's assuming all else is equal/negligible, which isn't quite the case.
- Yeah, an ideal environment for sparse MoE like Mixtral

- Lpddr5x at 120gb/s I have a core ultra 7 155h with lpddr5 at 100gb/s. You can ask me for some tests if you want

- Is there any reason that regular consumer motherboards can't support quad or 8 channel RAM? I feel like if we can have 8 channels DDR6, we'd be at around 600 to 800GB/s, which is very similar to gpu vram speeds. Maybe this is what we should ask AMD to do instead of GPU's with 46gb or 96gb RAM for consumers at reasonable prices.
  - It would normalize everyone potentially having great bandwidth for local inference, wouldn't require a GPU at all, and would basically explode the number of devices that could locally inference at reasonable speed. This would open the flood gates for local llm's - open or closed source, because now everyone and their grandma would be able to use it effectively.
  - And unlike GPU's, you'd never be limited by how many GB's of RAM you want to install, and therefore not be dependent on NVIDIA (or whomever) to hopefully one day release a card with more VRAM. The power would go back to consumer. And the bandwidth would double again for DDR7 and so on.
  - I just don't know if putting quad or 8 channels on a motherboard is somehow difficult and can only done at high price to the consumer, which is why only pro-sumer or server level mobos do it.
- They could, but the main limiting factor is the memory controllers are on the CPU. Intel, AMD, and the others use number of channels as a market segmentation method. But ultimately it boils down to memory channels equal $$.

- The bandwidth numbers for the Apple M1/2/3 SoC are just the raw totals from the memory, but depending one which cluster is using it (P-cores, E-cores, GPU) they have their own limitations. Here is the explanation for the M1 series
  - On the M1 Max with 400GB/s the CPU can get maximum 204GB/s when using the P cores only or 243GB/s when using both the P and E cores.

- ## 🆚⚡️ [Performance of llama.cpp on Apple Silicon M-series · ggml-org/llama.cpp _202311](https://github.com/ggml-org/llama.cpp/discussions/4167)
  - 提供了各种mac, air的模型测试数据

- LLaMA 7B

```markdown
- Mac, bandwidth(gb/s), gpu-cores, 7b-Q4-PP, 7b-Q4-TG
- M1,     68,           7,          107,     14
- M1Pro,  200,          14,         230,     35
- M1Max,  400,          24,         400,     54
- M1Ult,  800,          64,         1030,    83

- M2,     100,          8,          145,     21
- M2Pro,  200,          16,         294,     37
- M2Max,  400,          30,         537,     60
- M2Ult,  800,          76,         1238,    94

- M3,     100,          10,         186,     21
- M3Pro,  150,          14,         269,     30
- M3Max,  400,          40,         759,     66
- M3Ult,  800,          60,         1073,    88
- M3Ult,  800,          80,         1471,    92

- M4,     120,          10,         221,     24
- M4Pro,  273,          16,         364,     49
- M4Max,  410,          32,         713,     69
- M4Max,  546,          40,         885,     83

- M5,     153,          10,         247,     29
- M5N,    153,          10,         636,     31
- M5Pro,  307,          16,         3xx,     4x
- M5Max,  460,          32,         7xx,     6x
- M5Max,  614,          40,         8xx,     6x

```

# discuss-news
- ## 

- ## 

- ## 

- ## 

- ## [Apple unveils M5 Pro and M5 Max, citing up to 4× faster LLM prompt processing than M4 Pro and M4 Max : r/LocalLLaMA](https://www.reddit.com/r/LocalLLaMA/comments/1rjqsv6/apple_unveils_m5_pro_and_m5_max_citing_up_to_4/)
  - M5 Pro supports up to 64GB of unified memory with up to 307GB/s of memory bandwidth, while M5 Max supports up to 128GB of unified memory with up to 614GB/s of memory bandwidth.
- I desperately need to see pre-fill benchmarks. The M3 Ultra mac studio takes 10+ minutes on pre-fill for large models and contexts
  - The main difference in the M5 is the newly introduced matmul, specifically for boosting prompt processing speed. This paired with 1.2TB/s makes the combo wild. Still, not too many GPU cores compared to the spark (packed with 6k cuda cores), but for inference, on paper, it might be a better value for money.

- ## [M5 using neural accelerators in the GPU is up to 3.65x faster for prefil in test : r/LocalLLaMA](https://www.reddit.com/r/LocalLLaMA/comments/1ocousf/comment/nko6m47/?force-legacy-sct=1)
- How is it different to the neural engines in previous iterations?
  - Think of the new approach as equivalent to nvidias tensor cores. 
  - The old approach was using dedicated npus that were outside of the gpu. Same deal as Intel and amd cpus with npus in them.
  - While npus are more efficient than just doing small tasks on the cpu, they just can’t offer the same performance as something like a tensor core. This is something that amd has been struggling to realize and only now changing it in rdna5.
- this is AI cores inside the M5, previous M chips didn't have accelerators
  - they have "neural engine" cores though - aren't those meant to do the same thing - accelerate machine learning, ie matmul?
- The neural engine can only be accessed through CoreML. Ie: not used for LLMs at all.
  - M5 adds matmul instructions and/or accelerators on the GPU.
- MLX does not use the Neural Engine
  - [ANE support · Issue #18 · ml-explore/mlx](https://github.com/ml-explore/mlx/issues/18)
  - ANE can be supported with light warpper of kernel in pytorch/mlx module level. In M3 Ultra , ANE is far behind GPU cores, that is why apple won't support it

- [M5 Neural Accelerator benchmark results from Llama.cpp : r/LocalLLaMA](https://www.reddit.com/r/LocalLLaMA/comments/1ogwf6b/m5_neural_accelerator_benchmark_results_from/)
  - M5 和 M4 的token generation 速度提升大致一点点 24.1 -> 26.5， 但prompt processing的速度提升了很多 221 -> 608
# discuss-benchemarks
- ## 

- ## 

- ## 

- ## 

- ## 

- ## [M5 Max vs M3 Max Inference Benchmarks (Qwen3.5, oMLX, 128GB, 40 GPU cores) : r/LocalLLaMA _202603](https://www.reddit.com/r/LocalLLaMA/comments/1s5np41/m5_max_vs_m3_max_inference_benchmarks_qwen35_omlx/)
  - Ran identical benchmarks on both 16” MacBook Pros with 40 GPU cores and 128GB unified memory across three Qwen 3.5 models (122B-A10B MoE, 35B-A3B MoE, 27B dense) using oMLX v0.2.23.
  - Quick numbers at pp1024/tg128:
  - 35B-A3B: 134.5 vs 80.3 tg tok/s (1.7x)
  - 122B-A10B: 65.3 vs 46.1 tg tok/s (1.4x)
  - 27B dense: 32.8 vs 23.0 tg tok/s (1.4x)
  - The gap widens at longer contexts. At 65K, the 27B dense drops to 6.8 tg tok/s on M3 Max vs 19.6 on M5 Max (2.9x). 
  - Prefill advantages are even larger, up to 4x at long context, driven by the M5 Max’s GPU Neural Accelerators.
  - Batching matters most for agentic workloads. M5 Max scales to 2.54x throughput at 4x batch on the 35B-A3B, while M3 Max batching on dense models degrades (0.80x at 2x batch on the 122B). The 614 GB/s vs 400 GB/s bandwidth gap is significant for multi-step agent loops or parallel tool calls.
  - [M5 Max vs M3 Max: LLM Inference Benchmarks | Claude _202603](https://claude.ai/public/artifacts/c9fba245-e734-4b3b-be44-a6cabdec6f8f)

- There has to be more at play here than higher memory bandwidth ... must be because of MLX / software optimizations. 35A3B pp speeds and tg speeds are way higher than my Radeon AI Pro R9700 - but memory bandwidth is actually lower than the R9700 (640 GB/s)
  - Yeah they’re shipping Transformer-optimized MatMul cores in the new M5 chips. By all data I’ve seen they’re the absolute best token/Joule chip ever built. 
- Same reaction same card. Really goes to show how much ROCm and Vulkan leave on the table
  - Wait until you try to run VLLM on R9700, then you really leave stuff on the table, lol
# discuss-issues
- ## 

- ## 

- ## 

- ## 

- ## 

- ## 

- ## [For MAC LLM Prompt processing speeds Gemma 3 seems like an ideal LLM : r/LocalLLaMA _202510](https://www.reddit.com/r/LocalLLaMA/comments/1o0mph2/for_mac_llm_prompt_processing_speeds_gemma_3/)
  - as the conversation grows the prompt processing times are significant. For example on a 100K context window the Qwen 3 MOE A3B 30B takes about 3-5 minutes of processing time depending on your context type. And that is a LOT and not practical.
  - So enter GEMMA 3 12B GGUF (llama.cpp) Q8. I've tested this model (Not MLX) and noticed that although its tokens per second might not be a match with the MLX variant, it makes up a whole lot more with prompt processing times.
  - My test using this model with "flash attention (experimental)" on on LM studio on a 100K context window has been stellar. Initial prompt processing 1-3 minutes and subsequent prompts take about 15-30 seconds roughly the same amount of time the GEMINI 2.5 flash takes to process.
  - This tells me that enterprise grade prompt processing times on MAC is not just possible, but its already here and proven in a model as dense as 12B which is vision capable and surprisingly the solution seems to be the llama.cpp framework and not MLX.
  - I've tried other gguf quants with other models with flash attention, none gave me the same results as this one. If someone with actual technical understanding can understand what makes this particular 12B architecture almost instant, then I truly see MACs competing with Nvidia in daily use cases.
  - Im using MAC studio M3 Ultra with 256GB ram. Using LM Studio as a backend server and openweb UI as front end. With my test, this model even out performs the QWEN3 4b MLX model with same amount of tokens in prompt processing speed.

- If you use a gguf then you can use prompt caching in llama cpp, I'm not sure if it's available or standard in mlx or ggufs through lm studio. The command to add in llama cpp is --cache-reuse 256. This results in your historic prompts being cached and only your most recent prompt being evaluated, so it doesn't slow down as context increases. Edit. I'm not sure if it caches everything, might need to play around with the cache options.
  - It’s also available on MLX, and LM Studio should handle prompt caching without any trouble.
- Yeah I know you have kv cache, but I'm not sure how that interacts with cache reuse, or the other prompt caching options.

- If you enable prompt caching, the response time won't increase as a conversation gets longer.

- [Qwen3-Coder-480B on Mac Studio M3 Ultra 512gb : r/LocalLLaMA](https://www.reddit.com/r/LocalLLaMA/comments/1qjpwbr/qwen3coder480b_on_mac_studio_m3_ultra_512gb/)
  - I have been using Qwen coder 480b for a while on the M3 Ultra. It’s slow. I found it works ok with Cline, but context processing is go away and come back in an hour. It definitely works, so for a background task it does a good job. Code quality is much better than smaller models. Output speed is good too, just than darn prompt processing - you’re looking at 100’s of tokens a second so on a 100k context it’s 1000 seconds. The box in general is awesome - being able to have lots of models to hand, and just fire up a different model or two is perfect for R&D. Production wise it’s ok if you have slow agentic flows. Just don’t expect snappy interactions

- ## [How to speed up prompt evaluation? : r/LocalLLaMA _202411](https://www.reddit.com/r/LocalLLaMA/comments/1grwy5p/how_to_speed_up_prompt_evaluation/)
- Unfortunately Macs are known for being weak with prompt processing part.
  - If you already tried all the baseline ways to speed things up (lower quants, quantized KV cache, etc), the only actionable advice is to cap context size at a level reasonable for your use-case, that way there'll be upper boundary.

- I reset to a new chat at every possible juncture. 

- ## [How Prompt Size Dramatically Affects Speed : r/LocalLLaMA _202411](https://www.reddit.com/r/LocalLLaMA/comments/1h0bsyz/how_prompt_size_dramatically_affects_speed/)
  - We all know that longer prompts result in slower processing speeds.
  - I measured speed with various prompt sizes using llama.cpp with Llama-3.1-8B-Instruct-q4_K_M. I ran each test as one shot generation (not accumulating prompt via multiturn chat style). I also enabled flash attention and set the temperature to 0.0 and the random seed to 1000 for each test.
  - For rtx-4090, it went from 153.45tk/s to 73.31tk/s.
  - For M3 Max, It went from 62.43tk/s to 33.29tk/s.
  - As the prompt size grows, the speed for RTX-4090 also decreases similarly as M3-Max. However, rtx-4090 processes prompt 15.7x faster and generates new tokens 2.5x faster than M3Max.

- Prompt processing is a major weakness of apple systems. There's been a couple benchmarks done previously. M4 has the same problem.

- Mac can do processing at like 800 tokens where a rtx Nvidia is in the 8000 tokens range. Mac is 10x slower under ideal conditions for the Mac. So essentially the longer your instructions and the conversation the slower it is by a multiple.

- if you have a mac with 64GB, being able to feed 49k prompt tokens to 70b-q4_K_M model or 25k tokens to 70b-q5_K_M model is great despite the wait time!

- the longer the prompt the heavy computational wise. if you really want fast prompt speed on 4090, exl2 or sgl would improvement by huge margin over llama cpp
# discuss-tips/xp
- ## 

- ## 

- ## 
# discuss-cluster-mac
- ## 

- ## 

- ## 

- ## 

- ## 
# discuss
- ## 

- ## 

- ## 

- ## 

- ## List of Apple Macs with Thunderbolt 5:
- https://x.com/anemll/status/2046784844320121204
  - MacBook Pro (2024, M4 Pro / M4 Max)
  - Mac Studio (2025, M4 Max / M3 Ultra)
  - MacBook Pro (2026, M5 Pro / M5 Max)
  - Base models MacBook Pro have Thunderbolt 4. As do the MacBook Air, Mac Mini, and iMac.
- MLX's implementation of RDMA (Remote Direct Memory Access) over Thunderbolt on macOS, can now be used as an independent library by anyone. It is the gem that powers Mac clusters for local AI, and is an order of magnitude faster than protocols over TCP.
- tcp was the ceiling for mac to mac. the interesting part is whether this makes cluster wide kv cache sharing practical, since that is where most local llm setups actually fall apart, not raw tensor throughput.
