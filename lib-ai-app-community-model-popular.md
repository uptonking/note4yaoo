---
title: lib-ai-app-community-model-popular
tags: [community, large-language-model]
favorited: true
created: 2025-09-16T12:35:33.913Z
modified: 2025-09-16T19:59:57.856Z
---

# lib-ai-app-community-model-popular

# guide

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
- gpt-oss-20b 
  - unsloth-Q5的输出速度为 11.8 tops, offcial-Q4的输出速度为 11.2 tops
# discuss-stars
- ## 

- ## 

- ## 

- ## [What leaderboard do you trust for ranking LLMs in coding tasks? : r/LocalLLaMA _202411](https://www.reddit.com/r/LocalLLaMA/comments/1gve7cw/what_leaderboard_do_you_trust_for_ranking_llms_in/)
  - [What leaderboard do you trust for ranking LLMs in coding tasks? : r/ChatGPTCoding _202411](https://www.reddit.com/r/ChatGPTCoding/comments/1gve7zs/what_leaderboard_do_you_trust_for_ranking_llms_in/)

- I actually prefer livebench and SWE. 
  - Aider is Leetcode like, old, fixed problems, easy contamination. 
  - SWE is hard and for Agent-like, but it's the best for real world scenarios.
  - Livebench uses good hand craft newly added exercises, and they make updates every month. High quality data, no contamination=> my goto benchmark

- None. I perform my own tests.

- [Exploring LLM Leaderboards _202405](https://medium.com/@olga.zem/exploring-llm-leaderboards-8527eac97431)
  - This post presents a handpicked collection of leaderboards designed for MLOps and LLMOps, regularly updated based on input from AI experts to ensure accuracy. 
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

# discuss-local-models
- ## 

- ## 

- ## 

- ## 

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

- ## [Qwen 3 30B A3B vs Qwen 3 32B : r/LocalLLaMA _202505](https://www.reddit.com/r/LocalLLaMA/comments/1kcbyk4/qwen_3_30b_a3b_vs_qwen_3_32b/)
- all the 3 models are thinking (unless you tell them not to with the special token).
  - They are hybrid thinking models, so you can tell them not to think or to think.
- I don't use reasoning with Qwen 3, I always append `/no_think` to all my prompts

- I found 30B-A3B and 14B (at the same quantization) to be roughly the same quality. 30B-A3B will run faster, but 14b will require less VRAM/RAM.
  - Translation seemed rough around the edges. 30B-A3B seemed better than Google Translate but far behind Gemma 3 (even @ 4b). 14b and 32b were much better at making the translation sound natural.
  - With riddles and logic puzzles, their performance was all relatively the same.
  - 30B-A3B probably has its uses, if you absolutely need fast answers, but the dense models (14b or 32b) will probably yield better results in most use cases.

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

- ## 

- ## 

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
