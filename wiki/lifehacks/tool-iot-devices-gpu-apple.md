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

# discuss-news
- ## 

- ## 

- ## 
# discuss-benchemarks
- ## 

- ## 

- ## 
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
# discuss
- ## 

- ## 

- ## 
