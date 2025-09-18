---
title: lib-ai-app-community-model-popular
tags: [community, large-language-model]
favorited: true
created: 2025-09-16T12:35:33.913Z
modified: 2025-09-16T19:59:57.856Z
---

# lib-ai-app-community-model-popular

# guide

- tips
  - models-watching: openai, claude, gemini/gemma, mistral/codestral, qwen, deepseek, glm
  - 选择模型时多用官方版/主流版，小众微调的版本可能存在tool-call/overthink/多语言/对话风格等问题
  - 多agent架构时，可使用不同架构的agent相互验证

- leaderboard-llm
  - [Artificial Analysis LLM Leaderboard - Comparison of over 100 AI models from OpenAI, Google, DeepSeek & others](https://artificialanalysis.ai/leaderboards/models)
  - [Vellum LLM Leaderboard 2025](https://www.vellum.ai/llm-leaderboard)
  - [SEAL LLM Leaderboards: Expert-Driven Evaluations](https://scale.com/leaderboard)
  - [OpenRouter LLM Rankings](https://openrouter.ai/rankings)
  - [LiveBench](https://livebench.ai/)
  - [LMArena Leaderboard](https://lmarena.ai/leaderboard)
  - [UGI Leaderboard](https://huggingface.co/spaces/DontPlanToEnd/UGI-Leaderboard)
  - https://huggingface.co/open-llm-leaderboard /archived
  - [Find a leaderboard](https://huggingface.co/spaces/OpenEvals/find-a-leaderboard)
# model-usage-xp
- models-comparison
  - 分析清楚核心需求: 需要reasoning/coding/large/faster的模型
  - moe模型的实际效果大概只有dense模型的一半，如qwen3-30B-A3B 相当于 Qwen3-14b
  - 模型占用VRAM不能太大，还要为context处理、应用程序如nextjs/comfyui预留RAM/VRAM

- gemma3
  - 27b 和 12b 都能较好遵循带结构的instruct输出， 27b能主动给出更多外部网页链接而12b给的链接很少

- qwen3
  - think 2-3min, think支持disable
  - 4b及14b的输出都比较详细

- glm4
  - glm4不会think，输出内容质量感觉一般
  - 输出的长度大概在30-60行，简洁是特色?
  - 在多轮聊天时，输出内容也会逐渐变长?
- glm-z1
  - z1会think5-15min，think不支持disable，输出内容的长度会比glm4多20行左右，多一些外部链接，多用很多表格，质量较好
  - z1的think时间比qwen3长很多，输出内容的长度比qwen3更少

- gpt-oss-20B-A3.6B
  - unsloth-Q5的输出速度为 11.8 tops, offcial-Q4的输出速度为 11.2 tops, 速度比qwen3-14b更快

## models-coding

- qwen3-coder-30b-a3b

- qwen2.5-coder-32b

- devtral-2507-24b
# discuss-stars
- ## 

- ## 

- ## 

- ## 🆚 [The new MLX DWQ quant is underrated, it feels like 8bit in a 4bit quant. : r/LocalLLaMA _202505](https://www.reddit.com/r/LocalLLaMA/comments/1khb7rs/the_new_mlx_dwq_quant_is_underrated_it_feels_like/)
- Yep, fully agreed - the DWQs are honestly awesome (at least for 30ba3b). 
  - one of the big benefits of DWQ over AWQ is that the model support is far, far easier. From my understanding it's basically plug-and-play; any model can use DWQ. Versus AWQ which required bespoke support from one model to the next.

- What does DWQ stand for in this context? It's a slightly loaded acronym and there's a few old papers referencing the same initials, but I think they stand for something else.
  - it's distiled quant from unquantizated model, details:
https://github.com/ml-explore/mlx-lm/blob/main/mlx_lm/LEARNED_QUANTS.md

- [MLX 4bit DWQ vs 8bit eval : r/LocalLLaMA _202508](https://www.reddit.com/r/LocalLLaMA/comments/1mh7yud/mlx_4bit_dwq_vs_8bit_eval/)
  - Spent a few days finishing the evaluation for Qwen3-30B-A3B-Instruct-2507's quant instead of vibe checking the performance of the DWQ. It turns out the 4bit DWQ is quite close to the 8bit, even though the DWQ is still in an experimental phase, it's quite solid

- [New Qwen3-32B-AWQ (Activation-aware Weight Quantization) : r/LocalLLaMA](https://www.reddit.com/r/LocalLLaMA/comments/1kffj42/new_qwen332bawq_activationaware_weight/)
- GPTQ, AWQ are quant methods.
  - QAT is a method of training in which the model is trained while accounting for the fact that the weights are going to be quantised post training. Basically you simulate quantisation during training, the weights and activations are quantised on the fly.

- ## [What leaderboard do you trust for ranking LLMs in coding tasks? : r/LocalLLaMA _202411](https://www.reddit.com/r/LocalLLaMA/comments/1gve7cw/what_leaderboard_do_you_trust_for_ranking_llms_in/)
  - [What leaderboard do you trust for ranking LLMs in coding tasks? : r/ChatGPTCoding _202411](https://www.reddit.com/r/ChatGPTCoding/comments/1gve7zs/what_leaderboard_do_you_trust_for_ranking_llms_in/)

- I actually prefer livebench and SWE. 
  - Aider is Leetcode like, old, fixed problems, easy contamination. 
  - SWE is hard and for Agent-like, but it's the best for real world scenarios.
  - Livebench uses good hand craft newly added exercises, and they make updates every month. High quality data, no contamination=> my goto benchmark

- None. I perform my own tests.

- [Exploring LLM Leaderboards _202405](https://medium.com/@olga.zem/exploring-llm-leaderboards-8527eac97431)
  - This post presents a handpicked collection of leaderboards designed for MLOps and LLMOps, regularly updated based on input from AI experts to ensure accuracy. 
# discuss-tips/usage
- ## 

- ## 

- ## 

- ## 

- ## [How do you actually test new local models for your own tasks? : r/LocalLLaMA _202509](https://www.reddit.com/r/LocalLLaMA/comments/1nejogz/how_do_you_actually_test_new_local_models_for/)
- The easiest way for me to test coding ability is to check my task history for challenges I had to use Claude for and see how it performs compared to Claude. 

- I have a standard test framework with 42 prompts, testing a variety of different skills. Running it prompts the model with each prompt five times, so I can see outliers, how reliably it answers questions, and diversity in creativity.

- i have a folder in lmstudio for tasks i regularly have for local llms, i keep those chats around, and then press regenerate with different models to see how they perform in the actual things i use them

- ## [Don't try to increase the number of active experts on GPT-OSS : r/LocalLLaMA _202508](https://www.reddit.com/r/LocalLLaMA/comments/1miwzbq/dont_try_to_increase_the_number_of_active_experts/)
  - I've noticed that LM studio allows you to arbitrarily increase the number of experts, so I gave it a shot and increased it from 4 active experts to 16 (out of 32).
  - Using 16 experts, on the other hand, pretty much neuters(使无效) the model and renders it useless, resulting in the worst response I have ever seen from any model I have ever tried.
  - I plan on doing more experimentation. It's a somewhat unique MoE configuration that OpenAI has given us on the 20b MoE model, with only 3.6B active parameters on each token (including routing and embedding tokens). It's a remarkably lean model, but so far, it's performing quite strongly if you leave it on the default settings.

- Varying the number of experts used in any MoE model invites a chance of things going sideways unless the routing layer(s) get retrained to work with the new number of experts. And even then, performance not guaranteed to improve with more experts active.

- Normally 8 experts are used, as this is often optimal, I wonder why Openai went with 4.
  - Yea, I tried it with 8 experts too. Not nearly as bad as the response we got with 16, but it hallucinates quite a lot

- ## [Only 7 tokens per second at zero context running q6k qwen 2.5 32b coder on a 4090 : r/LocalLLaMA _202411](https://www.reddit.com/r/LocalLLaMA/comments/1gpaz3d/only_7_tokens_per_second_at_zero_context_running/)
- Q6K doesn't fit into VRAM, so you can't expect high speeds. Use a more appropriate quant.

- do you have everything off loaded to the GPU? I don't think you do, I'm getting that speed on ancient P40s and 22 tk/s on 3090s.

- ## [How to increase tps Tokens/Second? Other ways to optimize things to get faster response : r/LocalLLaMA _202507](https://www.reddit.com/r/LocalLLaMA/comments/1mau1nz/how_to_increase_tps_tokenssecond_other_ways_to/)
- You can offload specifc tensors to ram to increase performance instead of just offloading a certain amount of layers. it has little impact for dense models, but it's worthwhile when using MoE models.

- Use a better inference engine like SGLang or vLLM

- Run a Q4 model and lower KV Cache to Q4 as well, that's going to be the best balance between speed and size. Below Q4 things get weird and it's generally not worth it.

- ## 🤔 [What is the minimum tokens a second before a model is just unusable for you? : r/LocalLLaMA _202405](https://www.reddit.com/r/LocalLLaMA/comments/1cuqye0/what_is_the_minimum_tokens_a_second_before_a/)
- Around 1.5 t/s any lower and I'd rather get a dumber model to give me the answer faster.

- I think 4 T/s is a speed you can sort of tolerate reading the response as it generates, but any slower you want to do something else while you wait.  
  - When not watched, 4 T/s can generate paragraphs of text pretty quick. 
  - Someone made this T/s simulator which I assume is accurate: https://tokens-per-second-visualizer.tiiny.site/

- 2-3 tokens per second is my limit. Any lower, and I get frustrated and lose my mind. Any higher, and I spend the better part of a day looking for a better model because I crave intelligent computers like plants crave Brawndo.

- For interactive stuff, 5 t/s is kinda the limit. Any slower and I will start doing other stuff while it generates or get annoyed waiting for it. As a result, there's no flow to the conversation.
  - I'll take slower speeds for other tasks, like summarization though if the quality increase warrants it.

- Depends on the use case. 
  - For programming I want as much speed as possible. I don't want to sit and wait in front of the screen as the AI takes minutes to output a 50 lines function which might also not even be correct. Ideally give my 10 lines per second.
  - For storytelling or QnA I'm fine with my own reading speed, which is about 7-8 t/s.

- I would say < 10 tokens per sec is really very hard to use. I always ended up using models from 3B to 35B on A100 80GB machine. I found it as a sweet spot.

- [How many tok/s is enough? : r/LocalLLaMA _202504](https://www.reddit.com/r/LocalLLaMA/comments/1jze7v5/how_many_toks_is_enough/)
- I'm GPU poor and run LLMs on my work laptop (M2 Max, 64GB RAM). Anything above 15~20 tok/s is fine for me
  - I'm choosing Q4KM for 32B models and Q8 for 14B. I've tried some smaller ones, but it's a waste of time despite the high speed.
- inference speed drops drastically as context window increases. If a model already starts with 5-7tps, then once it reaches 12K, it would be half as slow.
  - I always reminds myself that even at this speed, I am still chatting faster than I do with a human. So, I should be patient.
- For chat? 10
  - For code generation? 30
  - For the final answer about life and everything? 1

- ## [difference between Q3_K_M and Q3_K_L? : r/LocalLLaMA _202403](https://www.reddit.com/r/LocalLLaMA/comments/1bnkszk/difference_between_q3_k_m_and_q3_k_l/)
- Why are there so few benchmarks for Q8?
  - Because it is known that the quality difference between q_6 and q_8 is negligible, so there’s no point in benchmarking. Also, not many people use q8.

- If speed is your concern you might have better results with Q4KS than with Q3KM. As long as it fits I would prefer that over Q3. I would use Q3 or Q2 only if you can't run Q4ks. I don't get why that size isn't more popular.
  - Because lot of people still think Q3 is faster than Q4, so they prefer the actually slower quants even if they would have enough space

- ## [How badly does Q8/Q6/Q4 quantization reduce the ability of larger MoE models (like Deepseek V3.1 or Qwen 235B) to do tasks and reason? : r/LocalLLaMA _202508](https://www.reddit.com/r/LocalLLaMA/comments/1n3ezr4/how_badly_does_q8q6q4_quantization_reduce_the/)
- Perhaps like this. Axis on the right is pass 2 rate on the Aider Polyglot Benchmark.

- General rule that's good enough for me:
  - Q8 is less than 1% reduction in accuracy. It's not going to be fundamentally different from full. Hardcore benchmarks are going to struggle to prove reduction.
  - Q6 is where math starts breaking down; as you need perfection. Code might not come out perfectly and linter will come a talkin. Call this 5-10% loss.
  - Q5 is much the same as Q6, this is solid 10% loss.
  - Q4_0 is going to be 15-20% drop in accuracy.
  - Q1-3 isnt useable.
  - But then better quantizations come to talk. Unsloth's dynamic, Q4_K_XL for example, that's basically Q8. Q5_K_XL is for sure Q8.

- Brokk AI tested quantized Qwen3-Coder in their Power Rank benchmark. The result was a catastrophic drop in performance - the model dropped down from being the best open source coding model to the level of Kimi K2.

- ## [Q3 is absolute garbage, but we always use q4, is it good? : r/LocalLLaMA _202505](https://www.reddit.com/r/LocalLLaMA/comments/1kzmt56/q3_is_absolute_garbage_but_we_always_use_q4_is_it/)
  - Especially for reasoning into a json format (real world facts, like how a country would react in a situation) do you think that it's worth it to test q6 8b? Or 14b of q4 will always be better?

- The difference between Q4 and Q3 is noticeable to me, but the difference between Q6 and Q4 is not.
  - Q4_K_M seems like a really sweet spot.

- Unsloths dynamic q3’s are usually really good.
  - hell yeah. its the sweet spot between Q2KXL size and Q4XL precision.

- According to Unsloth's Dynamic Quant 2.0 documentation, Q2KXL is the most efficient per size in GB, while Q4KXL is the closest to lossless while being a quarter of the size.

- I use Q8 for models up to 32B, and Q4 or Q6 for 70B models. I don't think you can generalize in this case

- Q4 is common because the majority of the performance is usually there, but the model is a quarter the size.

- Not necessarily. Q3 of Nemotron 49B is pretty good. YMMV but it's been more useful to me than any q4 32b model.

- At Q3, degradation becomes very significant, especially at precise tasks such as coding, but still may be good enough for creative writing or general use where precision does not matter that much. 
  - Remember, lowering the number literally means lowering precision. Precision in coding > Precision in creative writing.
- Creative writing imo degrades first. Q3 of Qwen2.5 32b was morepowerfull than 14b 2.5 q4 at coding but totally useless at creative writing, completely degraded.

- ## 🆚 [Q4, Q5, Q8… why? : r/LocalLLaMA _202403](https://www.reddit.com/r/LocalLLaMA/comments/1bltyis/q4_q5_q8_why/)
- math and coding capabilities degrade at lower quants dramatically.

- You can think of it like Video Resolution, Q8 is like 1440p quality and Q4 is like 720p quality. Both contain the same thing and they're pretty pretty similar at a glance. But there is a difference in size, quality, and such.

- [Quantization performance of small vs big models : r/LocalLLaMA _202503](https://www.reddit.com/r/LocalLLaMA/comments/1jbwcjb/quantization_performance_of_small_vs_big_models/)
  - I have observed that larger model with quantization like q4 performs really well as compared to <14B models. I would stick to q8 for <14B models and would use GGUF format.

- [Blind testing different quants · ggml-org/llama.cpp · Discussion _202403](https://github.com/ggml-org/llama.cpp/discussions/5962)

- [My head is spinning with all the quantization methods now. Anyone else? : r/LocalLLaMA _202306](https://www.reddit.com/r/LocalLLaMA/comments/143ozbn/my_head_is_spinning_with_all_the_quantization/)
- There is a comparison table in the github: [k-quants · Pull Request · ggml-org/llama.cpp _202306](https://github.com/ggml-org/llama.cpp/pull/1684)
  - With q6_k you can fully fit a 13B model in a 3060 12gb with just a 0.38% perplexity loss compared to the huge f16 model.

- Prio1: Picking the biggest *B that fit into ram.
  - Prio2: Pick the highest Q that fit into ram.
- Alternatively, figure out what the slowest token generation speed is you can live with and pick the biggest thing that can still stay inside it.

- Use Qx for speed gain and small size. Don't believe people saying it is not doing anything. I like Q8 for speed, but i get a lot better result using f16, with phind 34b.
# discuss-mobile-llm
- ## 

- ## 

- ## 

- ## [Meta released MobileLLM-R1 on Hugging Face : r/LocalLLaMA _202509](https://www.reddit.com/r/LocalLLaMA/comments/1nf7zhq/meta_released_mobilellmr1_on_hugging_face/)
  - fair-noncommercial-research license
  - Its not just open weights its truly open source includes all the training data for full reproducabilility..

- it still gets beaten by qwen 0.6 so whats so special?
  - It's very close but it was trained on much less data
- The headline is less training compute. (Of course this is also the headline for Qwen3-Next, so that might perform similarly if scaled down; idk.)

- ## [Best local LLMs for mobile? : r/LocalLLaMA _202503](https://www.reddit.com/r/LocalLLaMA/comments/1j0v3b2/best_local_llms_for_mobile/)
  - I'm working on a project, trying out an in-browser inference engine (WebLLM) for the first time
  - Bonus points for the LLM being "uncensored"

- best models for mobile are mostly small, think 0.5B to 3B in complete size, but for usability I'll go for 3B, maybe 1.5B.
  - Phi-4 (Mini) [For Performance]: It's almost 4B (3.8B) in size but it's a great model for it's size and quite brand new.
  - Smollm2 [Recommended For Small Size]: Comes in sizes from 135M, 360M and 1.7B, made by HuggingFaceTB specially to be a small.

- Another model I just remembered (I was very tired when I wrote the response), Gemma 2 2B. I've heard it's pretty good for writing and creative responses!

- I'd recommend Qwen3 (4B/1.7B) at the moment, just to clarify.
- Qwen3 0.6B: It can reason and seems to be really good with funcion calling.
- ERNIE 4.5 (?) 0.3B: It's a really small model that maintains coherence, I personally like it and use it in places with low amount of RAM.

- Small models don't take Quantization well, they can get really dumbed down.
# discuss-vision-llm
- ## 

- ## 

- ## [moondream 0.5B - the world's smallest vision language model : r/LocalLLaMA _202412](https://www.reddit.com/r/LocalLLaMA/comments/1h7ivts/moondream_05b_the_worlds_smallest_vision_language/)
  - https://github.com/vikhyat/moondream
  - Moondream 0.5B offers a significantly lower download size and memory usage than moondream 2B.
  - It is intended to be used as a distillation target—start building with moondream 2B, and distill your use-cases onto the 0.5B model before deployment.
  - This model was built using structured pruning on 2B with quantization-aware training. This means we can easily distill from 2B to recover accuracy on the specific target tasks an application needs, and run with int8 quantization without any loss of accuracy.
  - Today we are releasing int8 and int4 weights for moondream 0.5B, as well as fast CPU inference support in the Python client library. 16-bit weights and distillation support will be coming soon, so stay tuned!

- doesnt look like this new model has been added to ollama as yet (and no GGUFs available)

- Awesome. Florence is nice and small too, but could only really handle a finite list of specific prompts. It seems this small models retains the ability to ask free-form questions, which would make it extremely useful for mobile devices.
  - Florence 2 base is smaller. You can also fine tune it to work with any specific prompt you like if you have consistent prompts.

- ## LGM：生成高质量3D模型，支持文字生成模型、图片生成模型，分辨率512*512，5秒内即可生成。
- https://x.com/Gorden_Sun/status/1784230776311284205
  - https://github.com/3DTopia/LGM

- ## 免费玩的本地大模型，本地搭建环境推荐用Ollama和ChatbotAI
- https://x.com/vista8/status/1862696894172209476
- Vision 建议换成用 Llama 3.2 Vision 11b，比llava要好很多，且支持多语言（包括中文）的文字识别

# discuss-models-hot/features
- ## 

- ## 

- ## 

- ## 

- ## [Which do you think is better: Deepseek-R1-32B vs QWQ-32b-preview? : r/LocalLLaMA](https://www.reddit.com/r/LocalLLaMA/comments/1j2wzky/which_do_you_think_is_better_deepseekr132b_vs/)
- I've use both, but tbh i like QWQ a bit more. I also like DeepSeek-R1-Distill-Qwen-14B.i1-Q5_K_S just for speed. A lot of simple tasks can be done with 14b variant 6x faster for me.
  - I like the 14B variant-Q8 too.

- on livebench, Looks like qwq-32b performs significantly better than Deepseek-r1-distill-qwen-32b

- Before the release of QWQ (final) I was making intensive use of DeepSeek R1-Distill 32B and 14B.
  - Now I use QWQ 32B Q4_K_M on an RX 7900 XTX (LM Studio).
  - QWQ is like having a real, tiny R1 installed on your local computer. It's more powerful, smarter, more accurate, and (very importantly) has more character and personality.
  - Of course I don't ignore the importance of the "system prompt" and the model configuration parameters. My configuration is a bit 'peculiar' but it gives amazing results.

- For me QWQ-32b performs much better than Deepseek-R1-32b on my specific real world use case: Given instructions and M-Schema database - generate SQL.
  - QWQ follows instructions better and almost always one shots the result without using additional agentic revisions of the SQL.

- ## [gpt-oss-20b vs magistral:24b? : r/LocalLLaMA _202508](https://www.reddit.com/r/LocalLLaMA/comments/1mj9690/gptoss20b_vs_magistral24b/)
- gpt oss is pretty bad, and you will feel like its working against you sometimes. but it's smarter, at least for maths and multi-turn chat. 
  - magistral's thinking feels more like a hack on instead of being integrated. 
  - Qwen is much, much better though.

- Magistral is rarely spoken of here, but honestly, it kind of sucks to work with, at least locally. Magistral is just a fine-tune of Mistral Small 3.1 and hell, even requires a system prompt to get it to reason, which leads to inconsistency when the model decides its system prompt is no longer relevant. (It's hard to keep the model reasoning after 2-3 prompts.) Magistral also reasons far longer and tends to draft its entire response every time, which is kind of annoying. GPT-oss doesn't.

- Although, Magistral has the upper hand on GPT-oss by far in terms of world knowledge, and a much lower hallucination rate. If your task in any way relies on world knowledge, choose Magistral. GPT-oss would be better suited for pure reasoning tasks, like maths or other difficult problem solving. But I wouldn't even recommend it for coding as theres betters options. (Devstral, Qwen3-Coder-30B-A3B)
  - My recommendation would be; pick neither of them. 
  - If you want a model with good reasoning ability, pick Qwen-3-30B-A3B-Thinking-2507. Or if that's slightly too much system resources, Qwen 14B. 
  - If you don't mind a non-reasoning model, go with Mistral Small 3.2-Instruct-2506. Low hallucination rate, decent at coding, great for world knowledge, and same parameter count as Magistral.

- I tried OSS 20B bf16 and compared its results with same prompt with a bunch of Qwen2.5, Qwen3, DeepSeek, results are clear as day, OSS 20B is crushing any other models in speed and accurency, it s a no match. I don t get why people don t get it, maybe they are too lazy to run Benchmark and read through the results.

- Magistral (others too)I have found that Repetition Penalty 1.1 with Rep Pen Range 64 helps a lot with this and improves the quality of reasoning overall.
  - I also noticed that it's worth starting your own reasoning. For example `<think> Okay, before I answer, let me first analyze the last answer`.
  - You can direct the model to what you need - this saves me time and in my opinion the results are better.

- ## [Magistral Overthinks TOO MUCH : r/MistralAI _202506](https://www.reddit.com/r/MistralAI/comments/1l9tby1/magistral_overthinks_too_much/)
- i didn’t have this experience (using Le Chat). It only thought for one sentence and wrote a brief reply
  - Same. It tends to overthink when the problem is complex, sometimes ending in a loop. Bit never in casual chatting or simple questions.

- Until now I can say, I only had positive experience with the reasoning of Magistral. I really like the way it breaks down math problems and looks at it from different angles if it comes to the same conclusion.

- ## [new mistralai/Magistral-Small-2507 !? : r/LocalLLaMA _202507](https://www.reddit.com/r/LocalLLaMA/comments/1m85vhw/new_mistralaimagistralsmall2507/)
- The update involves the following features:
  - Better tone and model behaviour. You should experiment better LaTeX and Markdown formatting, and shorter answers on easy general prompts.
  - The model is less likely to enter infinite generation loops.
  - [THINK] and [/THINK] special tokens encapsulate the reasoning content in a thinking chunk
  - The reasoning prompt is now given in the system prompt.
- This seems more of a stability, usability & qol update. Some figures drop slightly while one scores significantly higher, probably helped by the stability improvements they mention (less loops, less stuck, better parsing, etc).
  - Interesting that they made the same stability improvements to devstral earlier. And that model also scored higher on the relevant benchmarks. They probably had some bugs that they ironed out.

- I've only tried the first release of Magistral, but it's a damn good model, and yes, it can be used without reasoning. Compared to Qwen3-14B (also my main model, usually - sometimes 30B-A3B) it's leaps ahead in terms of knowledge. It's far, far less prone to hallucinating than Qwen3 in my experience
  - It's a really good model. But if you're someone who wouldn't really utilise its reasoning, then maybe checkout Mistral Small 3.2-Instruct-2506. It's a better model for that use-case, I'd say. Plus it's multimodal. Magistral is based on 3.1.

- Yes Qwen3 has a non-reasoning mode which works exactly as you describe: immediate response with a blank think block. Simple add ‘/no_think’ at the end of your query. Make sure to adjust temps, top-k & min-p values for non-reasoning though 

- I'm happy with Devstral 24B so far. It's not as good as GLM or Qwen3-32B but it's faster than those two, with better answers compared to Gemma 3 27B. I'm beginning to hate Qwen 3's reasoning mode with a vengeance. All the other models I mentioned come up with equivalent answers in a fraction of the time.
  - In my experience, Devstral has been better than Qwen3-32B with tools, at least in Zed. But it's not fine-tuned on coding tasks yet. Can't wait for Qwen3-coder 32B though.

- So far I see the same overly long thinking process even on the recommended settings. Like many other reasoning models, it only wastes tokens and time. Without reasoning, it seems to have less issues with repetitions, but they are still there. Needs more testing, but it might be better than Mistral 3.2.

- ## [I find that "thinking mode" answers are superficial compared to normal ones : r/MistralAI _202509](https://www.reddit.com/r/MistralAI/comments/1ne82ry/i_find_that_thinking_mode_answers_are_superficial/)
- I can confirm the issue you mentioned. I primarily use it for STEM-related questions and currently avoid the thinking mode whenever possible, as its responses tend to be overly brief and blunt. In contrast, Medium 3.1 provides longer and more detailed answers. I hope a future update will bring Magistral to the level of Medium 3.1.

- agreed. thinking makes answers worse for me in most cases

- Yeah I’ve noticed the same, LeChat’s thinking mode feels tuned more for structured reasoning than longform analysis. Normal mode actually gives richer text outputs for humanities stuff.

- ## [mistralai/Magistral-Small-2506 : r/LocalLLaMA](https://www.reddit.com/r/LocalLLaMA/comments/1l7zvph/mistralaimagistralsmall2506/)
- Very excited to see how it will perform against Qwen3 32B
  - So queen 32b is far more advanced ...

- Devstral replaced GLM4 for my main local coding model. It's the best, can't ait to try this new one.
  - GLM-4 can both code and write stories. I rarely meet anything like that, the last one was Mistral Small 22b. But as coder devstral is probably better.

- Magistral uses the reinforce++-baseline algorithm from OpenRLHF.

- ## 🚀 [Magistral — the first reasoning model by Mistral AI : r/LocalLLaMA _202506](https://www.reddit.com/r/LocalLLaMA/comments/1l807c0/magistral_the_first_reasoning_model_by_mistral_ai/)
- 10x inference for 10% improvements, and general usability goes down the drain. I personally don't see the use case for this.

- You might have to add a system prompt like this one to stop it from thinking too much
  - Yeah, I made the mistake of just doing my normal "Hello" when trying this model, and it immediately deathspiraled into a reasoning loop.

- ## [Mistral is underrated for coding : r/MistralAI _202507](https://www.reddit.com/r/MistralAI/comments/1m2s6ys/mistral_is_underrated_for_coding/)
- Medium 3 is underrated, Magistral on the other hand isn't. Not their best release apparently.
- Magistral is built for reasoning tasks. I’m curious to hear which tasks are you trying it for and where it fails?
  - Regarding benchmarks, it's the least capable of all published reasoning models so far, and is even beaten by a non-reasoning model (Kimi K2), while being the *most verbose one of ALL* (150M tokens to run the AA index
- magistral has bis problems. In API calls, 90% looping.
  - yes i think they will fix it soon. magistral is their first reasoning model. i hope they will also extend the context lenght to 128k.

- I really like devstral medium with roo code. It‘s really well priced like r1 but way faster.

- ## [anything better than gemma-3-27b-it for analyzing and summarizing long texts ? : r/LocalLLaMA _202508](https://www.reddit.com/r/LocalLLaMA/comments/1mukayg/anything_better_than_gemma327bit_for_analyzing/)
- For French you could try Magistral 24B they highlight their multi-lingual ability.

- mistral is way better than gemma for summary tasks in my opinion (mistral q8 x gemma3 q8)

- I think the new qwen3 30b may be better, especially for multi-lingual tasks

- ## [Why aren't there Any Gemma-3 Reasoning Models? : r/LocalLLaMA _202505](https://www.reddit.com/r/LocalLLaMA/comments/1kfeglz/why_arent_there_any_gemma3_reasoning_models/)
- Mostly likely because forcing extra thinking did not improve scores. Extra thinking often focuses on math problems and the Gemma-3 technical reports indicates this was already a focus.

- There are still usage cases for non thinking models (besides RP and ERP) RAG, cleaning up dictated text, taking text and improve the Flesch Reading Ease Score, summarize chapters for easy reference when writing, etc.

- You can manually prompt many models to think even though they don’t support it out of the box by adding something like this to your system prompt: `“You are a helpful agent with special thinking ability. This means you will reason through the steps before formulating your final response. Begin this thought process with <think> and end it with </think>”`
- Add `<think>` prefill and you get your reasoning.
- Why? There is Synthia 27b.
  - Actually, that was released a few days after Gemma-3 was released, but it was a quick fine-tune done by one man.

- I think it's a matter of time. Every open llm now has reasoning versions.

- I understand your point of view. But, for me, what matters to me is getting the answer. I can wait for 10 or 20 sec more for that.

- [Gemma 3 Reasoning Finetune for Creative, Scientific, and Coding : r/LocalLLaMA _202504](https://www.reddit.com/r/LocalLLaMA/comments/1jqfnmh/gemma_3_reasoning_finetune_for_creative/)
  - is it trained with SFT on synthetic reasoning data or with some RL algorithm (like GRPO)?
    - Both! We went through multiple rounds of SFT, GRPO, then distillation, then back to SFT and other RL etc.

- [You can now use Google's new Gemma 3 model & GRPO to Train your own Reasoning LLM. : r/reinforcementlearning _202503](https://www.reddit.com/r/reinforcementlearning/comments/1jl7oxh/you_can_now_use_googles_new_gemma_3_model_grpo_to/)
  - We collabed with Hugging Face to create a free notebook to train your own reasoning model using Gemma 3 and GRPO & also did some fixes for training + inference
  - You'll only need 4GB VRAM minimum to train Gemma 3 (1B) with Reasoning.

- ## [After 6 months of fiddling with local AI. Here’s my curated models list that work for 90% of my needs. What’s yours? : r/LocalLLaMA](https://www.reddit.com/r/LocalLLaMA/comments/1mdjb67/after_6_months_of_fiddling_with_local_ai_heres_my/)
  - All models are from Unsloth UD Q4_K_XL except for Gemma3-27B is IQ3. 
  - Running all these with 10-12k context with 4-30 t/s across all models.
  - Most used ones are Mistral-24B, Gemma3-27B, and Granite3.3-2B. Mistral and Gemma are for general QA and random text tools. Granite is for article summaries and random small RAG related tasks. 
  - Qwen3-30B (new one) is for coding related tasks, and Gemma3-12B is for vision strictly.
  - Medgemma is for anything medical and it’s wonderful for any general advice and reading of x-rays or medical reports.

- Medgemma is... an interesting experiment. It's performance in reading chest X-rays is questionable, it likes to skip stuff that isn't really obvious but can be very important.
  - You’re right, it misses a lot, but i find that with right amount of context, it provides useful insights.

- Do you know how medgemma performs for non-english languages?
  - I haven’t tried with non English. Gemma models in general have great multilingual understanding. Try it out

- You can run MedGemma locally and talk to it about ANYTHING health related in total privacy, with about as much confidence as your local GP, for free and again.. privately.
  - Agreed. I have a family member going through severe health crisis and Medgemma has kept a good profile of all their lab results, MRI/CT scans and medications. I just feed the context at the beginning then ask any question. It seems to know exactly what i need and provides genuinely useful insights.
  - I read the MRI report and ask it to interpret that in the context of everything else. Unfortunately it can’t read the actual imaging from MRI CD.

- ## [GPT OSS 20b is Impressive at Instruction Following : r/LocalLLaMA _202508](https://www.reddit.com/r/LocalLLaMA/comments/1mypokb/gpt_oss_20b_is_impressive_at_instruction_following/)
- Another awesome thing about gpt-oss is that with a 16GB GPU (that I have), there's no need to quantize because of the `mxfp4` weights.

- 5060ti runs at 100-110 tokens per second, 64k context fits easily.

- Honestly I hate gpt-oss20b mainly because no matter what I do, it uses SO MANY FUCKING TABLES for everything.
  - I think the system prompt can help here. The model is quite good at following instructions
- I just tell it not to in system prompt and all is fine.
  - It doesn't obey the system prompt. I've tried as best I can, that fucking model just displays everything in a table.

- ## [Which quant model would be best for the GPT-OSS-20B model? : r/LocalLLaMA _202508](https://www.reddit.com/r/LocalLLaMA/comments/1mkzvgw/which_quant_model_would_be_best_for_the_gptoss20b/)
- Look at the files and use the one with `MXFP4` in it's name. 
  - The gpt-oss models come in 4-bit standard, using fp16/f32 doesn't actually add any more information to it's parameters and is only useful for fine-tuning.
- I think all of them use MXFP4 for the experts except F32.
  - They are only MXFP4 for the experts; all the other tensors are normal bf16. Looking at the file sizes, all these quants are using MXFP4 for the nominal MXFP4 parts and the given quantization is applied to the rest which is why they're all about the same size. (IDK what's going on with the fp32 though...)
  - That said, the "other tesnors" are all part of the active parameters so their quantization has a meaningful impact on speed even if the filesize is largely unchanged

- They only released the model with MXFP4 quant, so there's not much there to quantize. The 5-bit ones are probably enough.

- Why are they so similarly sized?
  - Because there are 3 types of tensors in the released model: FP32, FP16 and MXFP4. FP32 are kept at their original precision because they're important but small. Only the FP16 are quantized, and there were not many of them either. Most of the weights are the experts in MXFP4.
  - Where I say FP16 maybe they were BF16, I'm not sure.

- ## [My Experience Comparing Gemma 3 27B and GPT-OSS 20B: A Clear Winner for My Use Case : r/LocalLLaMA _202508](https://www.reddit.com/r/LocalLLaMA/comments/1mtwy39/my_experience_comparing_gemma_3_27b_and_gptoss/)
  - Here’s a breakdown of my findings:
  - GPT-OSS 20B - Promising but Underwhelming: The model struggled with understanding nuanced instructions and would frequently misunderstand the task at hand. This often led to significant hallucinations and irrelevant outputs, requiring me to restart or heavily edit my prompts.
  - Gemma 3 27B - A Surprising Powerhouse: demonstrated a solid understanding of all the tasks I threw at it. 

- Well of course a 27B dense model is always going to be better than a 20B MoE.

- MoE models are easier to run for their listed parameter count, and also underperform a dense model of the same parameter count. You'd expect GPT OSS 20B to perform roughly like a 9B parameter LLM based on its total and active parameter count.
  - If you control for a combination of model size and speed of execution, it should be competing with something more like Qwen 3 8B, Llama 3.1 8B, or maaaaybe Gemma 3 12B.
- In reality, the real comparison to Gemma 3 27B is probably GPT OSS 120B, which you'd expect to run roughly like a 24-26B parameter LLM based on its active and total parameter counts (albeit even here, on pure CPU execution the GPT OSS will be faster at inference).

- Both GPT-OSS 20 and 120B is poor for translating English to Czech while Gemma 3 12B at Q4 is good. I liked GPT-OSS for programming, but I have not tried Gemma for that so no idea how they compare.
  - 💡 OpenAI has stated themselves, GPT-OSS is trained primarily on English-only text. Of course it won't perform well on translation tasks.

- ## [Which quants for qwen3? : r/LocalLLaMA _202505](https://www.reddit.com/r/LocalLLaMA/comments/1kf660e/which_quants_for_qwen3/)
  - There are now many. Unsloth has them. Bartowski has them. Ollama has them. MLX has them. Qwen also provides them (GGUFs). So... Which ones should be used?

- I can tell that the unsloth GGUFs are way better than the ollama ones

- you can also do quants by yourself with llama.cpp

- I use AWQ quants and vLLM when available - best quality/speed trade-off, although they are actually 4-bit like.

- ## [How is your experience with Qwen3 so far? : r/LocalLLaMA _202505](https://www.reddit.com/r/LocalLLaMA/comments/1ke3heg/how_is_your_experience_with_qwen3_so_far/)
- Qwen3 made a small revolution with Qwen3-30B-A3B model, now anyone can run a decent LLM with good speed even on CPU - cheap and dirty way, it is already obvious that there is just huge demand for this type of small MoEs
  - 32b dense version (with \no_think) is around Qwen2.5 level, sometimes better sometimes worse, with thinking it is close to QwQ 32b, but again sometimes QwQ 32b is better.
  - Qwen3 14b and Qwen3-30B-A3B is roughly on the same level, something is better with 30b, something is better with 14b, codding for example is better with 14b, but overall they are close enough.

- Is Qwen3-14b better than Qwen2.5-Coder-14b-Instruct, for coding, if you've tried it?
  - I'd say Coder variant right now a bit better.

- Qwen3-30B-A3B is currently one of my favorite models of all time. I can't believe it's so fast on CPU and still performs very, very well. 
  - I also tried it with thinking disabled in coding tasks, and still did a good job, even better than Qwen2.5 32b, a dense model.
  - I'm seriously considering upgrading to 128GB RAM just so I can run Qwen3-235B-A22B, lol.
- If you are referring to M4 Max, don't do it. I tested Qwen3 235B q3 with 4k context window and the tps was 7 at best. q2 is faster but generates garbage, q3 actually has good quality but you need to offload some layers to CPU as M4 GPU can only utilize 75% of RAM you have on your system, and that maks it too slow to use. If you need any larger context window, it will be even slower.
- You can allocate more than 75%
  - After applying this change, 235b q3 is now running at 14 tps, thank you so much!

- ## [How good is Qwen3-14B for local use? Any benchmarks vs other models? : r/LocalLLaMA _202507](https://www.reddit.com/r/LocalLLaMA/comments/1ltnpsl/how_good_is_qwen314b_for_local_use_any_benchmarks/)
- Qwen3 30b benchmarks are all around the same level as qwen3 14 but performance wise it is significantly faster up to 2-3 times tokenspeed as it only uses 3b active parameters at a time.
  - Though qwen3 30b is alot more sensitive to quantisation and will at q4 and below overthink stuff alot and make more mistakes. If you use it download the q6 version at least.

- Qwen3-14B is the best in South East Asian languages. Even with 4bit quant still very cohesive and good diction choice, much better than Mistral Small 24B 2506.

- Livebench has benchmarks. It's very good. Not far off from 32B actually. 

- ## [Qwen3 local 14B Q4_K_M or 30B A3B Q2_K_L who has higher quality : r/LocalLLaMA _202505](https://www.reddit.com/r/LocalLLaMA/comments/1knx47e/qwen3_local_14b_q4_k_m_or_30b_a3b_q2_k_l_who_has/)
- When comparing both on Q8 they're relatively evenly matched in thinking mode, although the 30B has an edge in non-thinking mode. At Q3 there's a noticeable drop in quality and at Q2 it starts dropping significantly. 
  - So, when it's 14B Q4 vs 30B Q2 then go for 14B Q4 as it should lead to better results.

- I can run 30B-A3B a lot faster in thinking mode than 14B or 32B in non-thinking mode, assuming they're all the same quant. I'm willing to give up a few points in output quality while getting a 5x or 10x speedup. 
  - In daily use, I tend to use the q4_0 quant of 30B-A3B a lot more, along with Gemma 3 27B if I need more detailed and accurate answers and I'm willing to wait.

- MOE models in particular are categorically worse than dense models for given total parameter count, e.g. 30B parameter model with 3B active is estimated to be about as good as the geometric mean of these figures, around 9-10 B parameters worth. This is an empirical formula based on model scores, and not a theoretical result. 
  - Regardless, it seems roughly accurate and thus the dense 14B should win handily over 30B-A3B at full precision. However, the active 3B model will run much faster than active 14B model

- in the case of 30B A3B, it's ~9.5B, so qwen3 14B is already better at fp16 vs fp16, let alone at Q4 vs Q2.

- ## 🆚 [Which is smarter: Qwen 3 14B, or Qwen 3 30B A3B? : r/LocalLLaMA _202504](https://www.reddit.com/r/LocalLLaMA/comments/1kadwbs/which_is_smarter_qwen_3_14b_or_qwen_3_30b_a3b/)
- Just a heads up for people using different languages - from my initial testing it seems like the dense models, even while "smaller" in total parameters, stay correct in terms of grammar and overall speaking quality better than the MoE.
  - Generally speaking I'd agree, but qwen3-30b-a3b has quite a different approach to MoE, instead of making experts bigger and trigger 2 experts at a time, they made them smaller (~300m parameters), and trigger 8 experts at a time. That somehow positioning 30b-A3B model not that much behind dense 32b model really.
- the 14B should be smarter than the MoE (which should have an effective parameter count of around 10.5B)

- I don't think 30b a3b is directly comparable to a 27-32b model. It's most likely comparable to 10-14b models by the adage 30/3=10b. I'm also curious how it compares to the 14b variant. They have completely different architectures and distillation paths. 14b is likely distilled from 32b, whereas the 30b is distilled from the flagship Moe.
  - I just finished testing the 30b a3b against the 14b, and at least for my use-cases the 14b is more consistent and runs much faster on my 3060 12gb than the 30b a3b. I even ran the 30b at q6, but had more logical errors, text errors, and in general poorer responses - especially without reasoning turned on.

- I just finished testing the 30b-a3b q_6 from unsloth and for me the 14b model performed better - especially with reasoning turned off. It was more consistent (the 14b model had fewer validation errors in my pydantic_ai applicaitons), had fewer text errors (sometimes strange characters and such errors with 30b), did not get caught in weird logical loops / infinite repeated output. Otherwise they seem similar.
  - Gemma is particularly useless to me despite its very strong string writing abilities due to its limited use of context and inability to reliably use tools and structured output. 
  - Qwen 3 14b has the lowest error rate (highest validation percentage on all structured output tasks)

- what's the point of MoE?
  - Only uses a part of its brain which makes it think faster while not loosing too much of its intelligence.

- Do you run it with Vulcan backend or rocm?
  - ROCm on Arch

- ## 🆚 [Qwen 3 30B A3B vs Qwen 3 32B : r/LocalLLaMA _202505](https://www.reddit.com/r/LocalLLaMA/comments/1kcbyk4/qwen_3_30b_a3b_vs_qwen_3_32b/)
- all the 3 models are thinking (unless you tell them not to with the special token).
  - They are hybrid thinking models, so you can tell them not to think or to think.
- I don't use reasoning with Qwen 3, I always append `/no_think` to all my prompts

- I found 30B-A3B and 14B (at the same quantization) to be roughly the same quality. 
  - 30B-A3B will run faster, but 14b will require less VRAM/RAM.
  - Translation seemed rough around the edges. 30B-A3B seemed better than Google Translate but far behind Gemma 3 (even @ 4b). 14b and 32b were much better at making the translation sound natural.
  - With riddles and logic puzzles, their performance was all relatively the same.
  - 30B-A3B probably has its uses, if you absolutely need fast answers, but the dense models (14b or 32b) will probably yield better results in most use cases.
  - In my testing, 30B-A3B was roughly the same quality, if a little worse, than 14b at the same quant. While 32b preformed noticeably better (even at lower quants) but obviously slower than 14b and much slower than 30B-A3B.

- Qwen 3 32B is much better. I'd say Qwen 3 30B A3B is about as good as Qwen 3 14B, which is very impressive by the way. I'd argue that Qwen 3 14B is about as good as the text bit of gpt4o mini

- I can run the Qwen3 30B A3B relatively easily and fast. And once the model is good enough, I value the speed a lot more.
  - Even if I had 32 GB VRAM GPU, I would still likely run the Qwen3 30B A3B because of its speed.

- Qwen 3 32B is better. Because it is Dense model. For Instructruction Following Task Dense Model works great because all Parameters are active. where in MOE , only Few(1/10th here) are active for that task.
  - MoE is for speed

- I benchmark these models on translating Korean video scripts:
  - Qwen3 32b(UD q4) was ~95% accurate.
  - Qwen3 14b(UD q6) was 89-95% accurate(varies quite a bit from run to run)
  - Qwen3 30B-A3B(q6) was ~85% accurate.
  - For reference, ChatGPT o1 was 99% accurate, it could even identify nuanced memes that were not immediately obvious to native speakers
  - Consider they are running on local machine, it's not bad. But when it comes to translating, it looks like bigger parameters means better result.

- Roleplay specific:
  - Qwen-3-30B-A3B is unusable, tragically. Maybe there's a tokenizer issue? 
  - Qwen-3-32B works great but it's a bit schizo. Writing is looks good on first pass, but gradually just stops making sense entirely. 

- 32B is slightly better in theory, but on unified memory systems like Apple Silicon, 30B A3B is so absurdly fast in comparison that the tradeoff is worth it for me. 

- ## 🆚 [two models big difference in how it converses/answers. ie Qwen3 30B A3B vs Qwen3 32B : r/LocalLLaMA _202508](https://www.reddit.com/r/LocalLLaMA/comments/1mkgv1l/two_models_big_difference_in_how_it/)
  - I downloaded 2 8bit models (both use 32-33gb of ram)

- Qwen 3 30B A3B 2507 just got released and one of the biggest improvements was made to tone it seems, but Qwen 3 32B hasn't been updated and is still a part of the original Qwen 3 release. I've found Qwen 3 32B actually has better tone than the original Qwen 3 30B A3B does.
  - I really hope they come out with a Qwen 3 32b 2508 version. For my use case, the dense model wins every time, and an update with improvements on par with the other 2507 releases would be a huge win for my workflow.

- The 30B A3B model is MOE model. The A3B tells you that it's 3B active. So you get the speed of a model like it was 3B but the intelligence of a 30B model.
  - Qwen3 32B is dense, not moe, and so it's slower.

- The tone of the answers depends as much on the prompt than it does on the model. You can tell it in the system prompt how it should act and both of those should be able to handle that just fine. Just tell them to be more conversational or something like that.

- ## [It's Mamba time: Comparing Nemotron Nano v2 vs Falcon-H1 vs Qwen (og) vs Qwen (2507) : r/LocalLLaMA _202508](https://www.reddit.com/r/LocalLLaMA/comments/1my39ja/its_mamba_time_comparing_nemotron_nano_v2_vs/)
  - Conclusions
  - Nemotron Nano is the most powerful hybrid I've evaluated so far. It's major weakness is that it seems to have failed to generalize Arithmetic and it's selective attention (information-filtering ability) is noticeably weaker then SOTA transformers. Mid-tier for reasoning length.
  - While Hybrids are getting better, they don't yet beat pure Transformers when I evaluated Falcon-Mamba it got a big fat 0 - these new hybrid guys actually do work and are getting better with each iteration. I hope to see this conclusion flip in the future!
  - Qwen3-4B-Instruct-2507 is a little beast and can replace older 8B with similar if not better performance and lower token usage.

- ## 🧩🚀 [字节跳动刚刚发布了他们的文本 Diffusion 模型！—— Seed Diffusion Preview _20250801](https://x.com/karminski3/status/1950995740408553826)
  - > “The model currently supports coding tasks only; more general capabilities are coming soon.”
  - 给不太了解文本 Diffusion 模型的同学，大家都知道现在 transformer 大模型是一个字一个字蹦出来的，而文本Diffusion 模型则是跟图像Diffusion 模型差不多，是一个去噪过程，整段话随机出现文本最后组成所有输出。
  - Diffusion 文本模型的优点是巨快，字节这个有 每秒 2146 个 token 的速度（应该是现在最快？）。我让它用 Rust 写冒泡排序，几乎是秒出。
  - 当然目前 Diffusion 文本模型最大的问题还是智能太低了，很难干活。
  - 目前除了 Seed Diffusion Preview以外，还有最知名的 Mercury Coder 和 Google 的 Gemini Diffusion.

- 目前已有的文本 diffusion 模型的智能表现明显都不及常规主流的文本 AI 大模型.
  - 现在这类商用了的扩散模型只达到GPT-3.5的水平，部分达到GPT-4
- 几乎没有上下文，之前体验的gemini-diffusion几乎无法记住上下文内容。哪怕是单次输出内容过多也会开始一直复读

- Diffusion + auto regressive 是方向。

- ## [Phi Model Family: The rise of The Small Language Models (SLMs)! : r/LocalLLaMA _202502](https://www.reddit.com/r/LocalLLaMA/comments/1iz9fpc/phi_model_family_the_rise_of_the_small_language/)
- Phi-4 isn't that small (14B) and it seems to punch above its weight. 
  - I've been enjoying Phi-4-25B rather a lot. It's a self-merge of Phi-4, and benefits quite a bit from the extra layers.
  - There's also a Phi-4-45B, but it's brain-damaged to the point of uselessness. Self-merges don't always work out.

- In my evaluation it really depended on the kind of task performed.
  - For many tasks Phi-4 and Phi-4-25B performed identically, but Phi-4-25B performed significantly better for code gen, science, summarization, politics, psychology, self-critique, evol-instruct, and editing tasks.
  - Neither model performs well at multi-turn chat, and their creative writing competence is okay but not great.

- Im MS term, it seems SLM is below 10B. And yes, Phi-4-mini and multimodal is small, not 14B.

- Phi-4 doesn't support function calling, doesn't follow up system instructions well.
  - apparently the new mini model supports function calling.
- Support and does well are totally different thing. Almost all model nowadays claim support of function calling

- ## [DeepSeek’s MOE approach for lower model hope : r/LocalLLaMA _202508](https://www.reddit.com/r/LocalLLaMA/comments/1mk0fxu/deepseeks_moe_approach_for_lower_model_hope/)
  - Seeing recent Qwen3-30B-A3B, I am praying DeepSeek release something like that too

- I mean... They sort of did. Qwen3 30B was made borrowing techniques from Deepseek's public research and was distilled from the Qwen 235B MoE model which in turn was trained on outputs from R1.

- Deepseek’s distils are very strong. DeepSeek-R1-0528-Qwen3-8B is the one. It is distilled from the newer 0528 series and it literally beats Gemini at math.

- ## [DeepSeek’s new R1-0528-Qwen3-8B is the most intelligent 8B parameter model yet, but not by much: Alibaba’s own Qwen3 8B is just one point behind : r/LocalLLaMA _202506](https://www.reddit.com/r/LocalLLaMA/comments/1l41p1x/deepseeks_new_r10528qwen38b_is_the_most/)
- They are amazing for their size. Maybe, each model have a better perfomance in each benchmark and in final ranking it seems no diference. My experience:
  - Destill R1 8b is better in coding, math and reasoning on my tests
  - Qwen 8b is close in coding, but feels more natural in wrintting and multiligual tests (as a spanish native speaker I value this more ).
- R1 distill felt WAY better in writing to me, but I've only tested in english.

- That new R1-Q3-8b model has been a disaster for me. It overthinks, hallucinates, and doesn't seem to follow thinking parameters properly.

- What about qwen3-30b-a3b ?
  - It scores 55.6 on this aggregate of benchmarks, so about the same as Qwen3 14B and higher than DeepSeek V3. That also puts it 2 points below Claude 4 Opus... and 12 points below Gemini 2.5 Pro Preview (May).

- ## [如何评价 DeepSeek 于 2025 年 8 月 19 日更新的 V3.1 版本？ - 知乎 _202508](https://www.zhihu.com/question/1941218073152587548)
- 虽然我看到不少人抱怨创意写作能力变差了，但实际上如果你真的是深度ai rp玩家的话，你会发现，v3.1由于其优秀的指令遵从，改善了的上下文和逻辑能力，优秀的中文语料，实际上就是现阶段可以使用的最优秀的rp模型。2.5pro残血外加疯狂截断，claude疯狂删语料，gpt和grok更是路边一条。
- 我还在想rp模型是什么技术类别的模型, role play？
  - 是的，ds也是少数把rp专门拉出来提一嘴的模型

- 听说之前经常发癫
  - 你说的是春节版本的r1，那的确如此
  - 老r1是这样的，当时最好的其实是claude

- 从这个节点来看，[DeepSeek]  V3.1对标对象应该是Qwen Coder这类模型， Coding+Agent ，这块肉最厚，进步也是最明显的，（可能很多人没感觉到。）感觉无论意图捕捉，视觉呈现，小创意的安排，运行也更顺畅都有了很大进步。

- 人麻了, 更新前能不能在官网预告一下. 拿API做实验结果评估, 昨天还好好的今天一起来发现结果爆炸. 调了几个小时代码后发现居然是 API 偷偷更新成 3.1 了
  - deepseek官网不是一直都是这样突然就换的吗 你是第一天认识它？

- V3.1 和 R1-0528 最大的共同点，就是彻底抛弃了 DeepSeek 早期那种“跳跃式幻觉”文风，转而大量借鉴了 Gemini 的输出结构、文风和语料，实用性直接起飞
  - 但 DeepSeek 肯定不甘心只做 Gemini 的“高仿”。相比于 R1-0528 对 Gemini 文风的直接复刻，V3.1 则会克制一些，融入了不少 DeepSeek 自己的中文语料。这种中西结合，让 V3.1 在文风上保留了一定的差异感。
  - 另一个明显变化是篇幅控制。相比于 R1-0528，V3.1 对各段落的字数都做了明显的精简。情绪渲染上也不再是 R1 那种冗长、粘稠的表达，更加直接和有效，给人一种清爽的感觉。

- ## 🎯 Introducing DeepSeek-V3 _20241226
- https://x.com/deepseek_ai/status/1872242657348710721
  - 60 tokens/second (3x faster than V2!)
  - Fully open-source models & papers
  - 671B MoE parameters

- https://x.com/op7418/status/1872469838641406262
  - 他们自测的成绩整体跟 GPT-4o 和 Claude 3.5 对齐了
  - 海外社区普遍惊叹他们用 Llama 405B 十分之一的算力成本训练了一个更大更强的模型
  - Llama 3 405B 使用了 30.8M GPU 小时，而 DeepSeek-V3 看起来是一个更强大的模型，仅使用了 2.8M GPU 小时（计算量减少了约 11 倍）。
  - 并不意味着前沿 LLM 需要要大的计算集群，反而意味着你必须不能浪费你拥有的资源

- https://x.com/amasad/status/1872320808028454976
  - Craziest thing is it took only $5.5m to train. US labs spend one — maybe two — order of magnitude more for frontier models.
# discuss-model-api
- ## 

- ## 

- ## 

- ## 

- ## [Mistral "free" LLM API is a game changer for so many developers : r/SaaS _202409](https://www.reddit.com/r/SaaS/comments/1fmxg9k/mistral_free_llm_api_is_a_game_changer_for_so/)
- free tier: It's one request per second, 500, 000 tokens per minute, and 1 billion tokens per month. Except Mistral Embed, which is two hundred billion tokens per month.

# discuss
- ## 

- ## 

- ## [What kind of models can I run with my new hardware 3090 with 24GB VRAM? : r/LocalLLaMA _202507](https://www.reddit.com/r/LocalLLaMA/comments/1lrfo4i/what_kind_of_models_can_i_run_with_my_new_hardware/)
- Gemma3 27b Q4 for best multilingual
  - Qwen3 32B Q4 for best STEM and coding performance
  - Qwen 3 30B-A3B Q4 for fastest performance while maintaining fairly good quality
  - GLM-4 32B Q4 for user interfaces when webcoding
- Models around 30B with Q4 are perfect sweetspot for 24GB cards. If you dont need much context you can try them at Q5 or even Q6.

- ## [Who is ACTUALLY running local or open source model daily and mainly? : r/LocalLLaMA _202506](https://www.reddit.com/r/LocalLLaMA/comments/1ldhej3/who_is_actually_running_local_or_open_source/)
- Is there an advantage to using KoboldCPP over Ollama? 
  - koboldcpp isn't a babyfied app like interface with shit functionality. Its flexible, you can tweak anything you want, the UI is functional and straight forward. You can pair it with sillytavern if you want to. And it's feature rich

- Gemma 3 27B is amazing for real time game translation. And for quick trivia questions, both Gemma and Qwen3 are great.

- I'm using Qwen3 14b q6 with 40k context as coding assistant with tabby. Works great for rough overviews of class functionalities, generating code snippets and methods for Python/TypeScript. Of course not a comparison to cloud provided code assistants - but it helps alot. Great model for its size.
  - For code related questions which the smaller model can't answer I switch to Qwen3 32b (q6?) - but only with a 12k context.

- qwen3 32B UD Q8_K_XL I've found to be the best one. It's 38 GB and runs at ~9 tk/s on my 2 3090s. It's as smart as chat GPT at least it feels. It's like having google offline and then some. It's epic

- ## [What LLM is everyone using in June 2025? : r/LocalLLaMA _202506](https://www.reddit.com/r/LocalLLaMA/comments/1lbd2jy/what_llm_is_everyone_using_in_june_2025/)
- Qwen3 32b is currently producing the best outputs for me. 
  - I did briefly benchmark the same task against QwQ and Qwen3 32b won. 
  - I flirted with 30b, love that tps but outputs aren't quite there. 
  - Tried Qwen3 14b and it's also very good but 32b does outproduce it.

- give some love to older LLMs. The fact that some are from '24 doesn't make them outdated or unusable.
  - Mistral Large (2407 is more creative, 2411 is more STEM-oriented)
  - Command A 111B
  - Llama 3.3 70B
  - Gemma 3 27B
  - Mistral Small (2409 for creative usage, 2501/2503 for more coherent responses)
  - Mistral Nemo 12B (for truly creative and sometimes unhinged writing)

- I am using qwen3 30b a3b on my old server computer and getting really good result. Mainly use it for some small codes and fixes. 
  - it’s basically on par with GPT-4.1 and sometimes even better. maybe can beat o3-mini in some tasks

- my models
  - Qwen3-30B-A3B(Q6 GGUF): Ideal for simple tasks that can run on almost any PC with 24GB+ RAM.
  - Qwen3-32B-AWQ: Good for harder coding and STEM tasks with performance close to o3-mini, better for conversations comapred to Qwen2.5.
  - Qwen2.5-VL-7B: Suitable for OCR and basic multimodal tasks.
  - Gemma3-27B: Offers better conversational capabilities with slightly enhanced knowledge and fewer hallucinations compared to Qwen3, but 🐛 significantly lags behind Qwen in coding and mathematical tasks.
  - Llama3.3-70B/Qwen2.5-72B/Command-A: Useful for task that demands knowledge and throughput, though they may not match smaller models with reasoning.
  - Mistral Small, Phi4, Minicpm4, and GLM4-0414 are effective for specific tasks but aren't the top choice for most scenarios.

- [Which model are you using? June'25 edition : r/LocalLLaMA](https://www.reddit.com/r/LocalLLaMA/comments/1l1581z/which_model_are_you_using_june25_edition/)
- General purpose + reasoning: qwen 3 32b q8 k xl @36k ctx
  - Code FIM: qwen 2.5 coder 32b q8 k @49K Ctx
  - Creative Writing + translation + vision: gemma 27b qat q8 k xl

- ## [Understanding Local Language Models: A Beginner’s Guide : r/LocalLLaMA _202507](https://www.reddit.com/r/LocalLLaMA/comments/1mbc9d3/understanding_local_language_models_a_beginners/)
- Unlike online AI (like ChatGPT), local LLMs don’t need a cloud server—you run them directly on your machine. But to do this, you need to know about model size, context, and hardware.
- 1. Model Size: How Big Is the Brain?
  - Small Models (1–3 billion parameters)
  - Medium Models (7–13 billion parameters)
  - Large Models (30+ billion parameters)
  - Simple Rule: The bigger the model, the more “thinking power” it has, but it needs a stronger computer. A small model is fine for basic tasks, while larger models are for heavy-duty work.

- 2. Context Window: How Much Can the Model “Remember”?
  - The context window is how much text the model can “think about” at once. Think of it like the model’s short-term memory. 
  - A bigger context window lets the model remember more, but it uses a lot more memory.
  - Simple Rule: Keep the context window small unless you need the model to remember a lot of text. Bigger context = more memory needed.

- 3. Hardware: What Kind of Computer Do You Need?
  - GPU VRAM (video memory on your graphics card, if you have one).
  - System RAM (regular computer memory).
  - Simple Rule: Check your computer’s VRAM and RAM to pick the right model. If you don’t have a powerful GPU, stick to smaller models.

- you can use some clever tricks to run bigger models:
  - Quantization: This is like compressing a big file to make it smaller. It reduces the model’s memory needs by using less precise math.
  - Free Up Memory: Close other programs (like games or browsers) to give your GPU more room to work
  - Smaller Context and Batch Size: Use a smaller context window or fewer tasks at once to save memory.
