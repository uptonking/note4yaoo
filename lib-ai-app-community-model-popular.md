---
title: lib-ai-app-community-model-popular
tags: [community, large-language-model]
favorited: true
created: 2025-09-16T12:35:33.913Z
modified: 2025-09-16T19:59:57.856Z
---

# lib-ai-app-community-model-popular

# guide

- models-variants
  - watching: openai, claude, qwen, deepseek, gemini/gemma, glm, mistral/codestral
  - variants: mlx, unsloth, quants
  - 测试模型时可能更希望速度快，但做任务或规划时更希望质量好，所以偏向选择大B参数的模型
  - 📱 端侧模型还要考虑电源及功耗问题, 实测macbook-air在跑模型时掉电很快
    - 端侧最好用 api-key + tiny-local-llm

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
  - 🤔 LMs are tools. Describe your use cases.
    - 分析清楚核心需求: 需要reasoning/coding/large/faster
  - moe模型的实际效果大概只有dense模型的一半，如qwen3-30B-A3B 相当于 Qwen3-14b
  - 模型占用VRAM不能太大，还要为context处理、应用程序如nextjs/comfyui预留RAM/VRAM
  - 选择模型时多用官方版/主流版，小众微调的版本可能存在tool-call/overthink/多语言multilingual/对话风格/llama.cpp不支持等问题
    - 选用主流版还方便与其他用户对比速度/配置
    - 非主流版可能出现vision/rag等被去掉的问题
  - 多agent架构时，可使用不同架构的agent相互验证
  - non-thinking或输出简洁的模型适合coding

- donts
  - 很多带thinking的大模型不擅长计数，如within 18 words， 有的模型真的会逐个token打印出来逐个数一遍

- mac 🍎
  - 👀 在low power mode省电模式下, 模型的输出速度会比非省电模式慢2-3倍

- gemma3 🌹 /多语言/创意文本/vision
  - 27b 和 12b 都能较好遵循带结构的instruct输出， 27b能主动给出更多外部网页链接而12b给的链接很少

- qwen3 🌹 /能力全/thinking开关/内容丰富
  - think 2-3min
  - 4b及14b的输出内容都比较详细，经常包含表格📈

- gpt-oss-20B-A3.6B 👀 /业界标杆/输出快
  - 输出的内容特别喜欢用表格📈, 讨论代码相关问题也喜欢用表格
  - unsloth-Q5的输出速度为 11.8 tops, offcial-Q4的输出速度为 11.2 tops, 速度比qwen3-14b更快

- magistral-small-2509-24b  👀 /可以用/think+vision/欧洲多语言/产品线丰富/censor弱
  - 回复一般很短，感觉质量不高
  - mistral系列模型的知识丰富度很高, 可以降低对RAG的依赖 🤔
  - thinking时间在~~3-10~~min(2509已改进)左右，或许对于plan制定计划有用
  - 输出内容几乎不提供外部链接，2507不也提供外部链接
  - 输出内容中几乎不提供表格
  - 带thinking的模型不擅长计数，如 within 18 words

- glm4 👀 /可以用/是否善长html代码?
  - glm4不会think，输出内容质量感觉一般
  - 输出的长度大概在30-60行，简洁是特色，对代码有用?
  - 在多轮聊天时，输出内容也会逐渐变长?
- glm-z1 👀 /思考非常久/不擅长代码
  - z1会think5-15min，think不支持disable，输出内容的长度会比glm4多20行左右，多一些外部链接，多用很多表格，质量较好
  - z1的think时间比qwen3长很多，
  - 输出内容的长度比qwen3更少, 输出内容会有表格📈

- resources
  - [Qwen3: How to Run & Fine-tune | Unsloth Documentation](https://docs.unsloth.ai/models/qwen3-how-to-run-and-fine-tune)

## models-coding

- tips
  - 对于ai按用户提供的模版输出html的场景，用户提供和ai输出的代码通常都是偏短的、偏静态的
  - coding模型必须要用新版才能使用最新框架的架构写法，如tailwind.v4, reactjs.v19

- qwen3-coder-30b-a3b 🌹 /速度快
  - 生成单页面的效果好速度快
  - 擅长用渐变色块代替图片占位符
  - 写完代码后一般还会讲解说明一段

- devstral-2507-24b /欧洲多语言/instruct

- qwen2.5-coder-32b /微调多

- qwen3-32b /thinking开关/能力全

- uigen-fx-4b /擅长ui框架/能写js
  - 不擅长用渐变色块代替图片占位符
  - 有时能写很多js代码

- webgen-4b /擅长html页面不擅长框架和js
  - webgen生成单页面的效果远不如uigen/qwen3-coder
  - 似乎不擅长tailwind, 生成页面的风格偏非tailwind样式的传统网页
  - 经常出现部分元素样式错乱的问题

## models-exploring

- [starvector/starvector-1b-im2svg · Hugging Face _202503](https://huggingface.co/starvector/starvector-1b-im2svg)
  - StarVector is a foundation model for generating Scalable Vector Graphics (SVG) code from images and text
  - It utilizes a Vision-Language Modeling architecture to understand both visual and textual inputs, enabling high-quality vectorization and text-guided SVG creation.
  - https://github.com/joanrod/star-vector /apache2/202504/python
    - StarVector Accepted at CVPR 2025
  - [感觉不太行。。](https://huggingface.co/starvector/starvector-1b-im2svg/discussions/2)
    - This checkpoint is designed for converting images into SVGs. While we do have a text-to-SVG model, we plan to release it at a later stage.
    - The current model performs well with simple icons but has limitations with more complex images. Improving performance on complex cases is a key focus of our ongoing work.

- [lakhera2023/devops-slm-v1 · Hugging Face _202509](https://huggingface.co/lakhera2023/devops-slm-v1)
  - Based on Qwen2.5
  - a specialized language model specifically for DevOps tasks and operations only.
  - designed EXCLUSIVELY for DevOps-related tasks. It has robust filtering that will NOT respond to general questions about movies, weather, cooking, sports, music
  - [Meet the first Small Language Model built for DevOps : r/LocalLLaMA](https://www.reddit.com/r/LocalLLaMA/comments/1ndm44z/meet_the_first_small_language_model_built_for/)
# discuss-stars
- ## 

- ## 

- ## 

- ## [How to use Qwen2.5-Coder-Instruct without frustration in the meantime : r/LocalLLaMA _202411](https://www.reddit.com/r/LocalLLaMA/comments/1gpwrq1/how_to_use_qwen25coderinstruct_without/)
  - Don't use high repetition penalty! Open WebUI default 1.1 and Qwen recommended 1.05 both reduce model quality. 
  - 📃 Use recommended inference parameters in your completion requests https://huggingface.co/Qwen/Qwen2.5-Coder-32B-Instruct/blob/main/generation_config.json

- ## [最近发的国产大模型为什么都没有reasoning版本（k2，qwen3）? - 知乎 _202507](https://www.zhihu.com/question/1931294740818665889)

- 有些模型把reasoning的过程没放think标签里，输出很长的基本都是。
  - thinking给用户的体验并不是很好，等待时间太长
  - 大部分问题其实用不着reasoning

- Sam Altman 就提过一个观点：用户虽然能从大模型里得到答案，但他们最想要的其实是——直接拿到那个最好的、正确的答案。
  - 验证者问题”：怎么判断一个答案是正确或者优秀的？
  - 这个问题其实可以分成两种情况：一种是在模型内部就能验证的，另一种是要靠外部来验证的。
  - 比如说，自主Reasoning类的大模型在处理问题时，会先设定好“当这个问题被解决时应该满足什么条件”，或者同时尝试多种路径，看它们能不能都指向同一个结果。这种情况下，它自己就能判断对错，适合用在数学题、逻辑推理题这类任务上。
  - 但像写作、写代码这些更常见的应用场景呢？它们的验证机制其实并不在模型内部，而是在外部——也就是说，需要人来判断输出是不是符合要求。 这时候真正起作用的不是 Reasoning，而是 [Prompt Iteration](提示词迭代)：人作为“验证器”给模型反馈，让它不断调整输出内容，直到满意为止。这种方式看起来不那么“高科技”，但在日常工作中反而是最实用的。
  - 其他大部分的时候 Reasoning LLM都在无效思考，为什么呢？因为模型会有一个第一直觉，而它又没有其他的验证途径，来验证它的第一直觉是对是错，比如非数学题，所以它会一直在第一直觉里空转，消耗tokens，最终输出的结果，其实跟不Reason，是一样的。
  - 用户其实是开发者群体，追求的是效率和快速迭代能力。这就依赖于两个方面：一个是输出速度快，另一个是模型的第一反应——也就是基于大量数据训练出来的模式识别能力。
- 当然，Reasoning 也有其他用途。它还有一个很大的优势，就是在面对多个冲突目标的时候，可以通过内部博弈找到一个平衡点。比如做规划类的任务，就非常适合用 Reasoning 来处理。
  - 还有一个我认为特别有用的方向，就是把 Reasoning 和工具使用结合起来，Reasoning的过程可以被视为一个行为过程。比如说把单轮搜索升级成多轮搜索。普通的单轮搜索加改写，搜出来的东西往往比较浅；但如果做成多轮搜索，就可以把上一轮的结果当成上下文，用来反思和优化下一轮的搜索策略。
  - 如果你的业务场景中只有单轮搜索，没有多轮反馈机制，那就算你用了 Reasoning，最终的效果也是有限的。因为缺少了根据外部信息持续优化的过程。

- 现在这些大模型通过Reasoning在那些可以内部验证的问题上刷出高分，但很多时候，我们面对的问题是真实世界的问题，需要不断迭代提示词，让模型与真实世界进行校准。

- ## 🆚 [Interesting (Opposite) decisions from Qwen and DeepSeek : r/LocalLLaMA _202508](https://www.reddit.com/r/LocalLLaMA/comments/1mwpmkb/interesting_opposite_decisions_from_qwen_and/)
- Qwen
  - (Before) v3: hybrid thinking/non-thinking mode
  - (Now) v3-2507: thinking/non-thinking separated
- DeepSeek:
  - (Before) chat/r1 separated
  - (Now) v3.1: hybrid thinking/non-thinking mode

- They don't necessarily disagree on results. These decisions are simply driven by different objectives. 
  - Qwen is more GPU-rich (they're Alibaba, for God's sake), they can train and serve more models and do more experiments.
  - Original Qwen3 was disappointing. Now they have Q3-2507 as general assistant, Q3-2507-Thinking as powerful reasoner, and Q3-coder as SWE agent.
  - DeepSeek has V3-0324 as an assistant, R1-0528 as a reasoner, and V3.1 as an SWE-agent, but they don't want to maintain and serve separate models, so V3.1 is also a (token-efficient, likely cheaper in practice than Qwen) reasoner and an assistant. 

- The two models have two different architectures:
  - Deepseek has 671B parameters with 37B active, with 64 layers and a larger architecture
  - Qwen has 235B parameters with 22B active, with 96 layers and a more deep architecture
  - It can be that these differences lead also to different performances in the merging of the two "inference modes": maybe the larger deepseek's architecture leads to more favourable conditions to make it happen.

- GPT-OSS provides low, medium, high reasoning efforts.
- NVIDIA's V2 Nemotron has token-level reasoning control https://huggingface.co/nvidia/NVIDIA-Nemotron-Nano-9B-v2

- ## 🆚 [How does MLX quantization compare to GGUF? : r/LocalLLaMA](https://www.reddit.com/r/LocalLLaMA/comments/1gc0t0c/how_does_mlx_quantization_compare_to_gguf/)
- The GGUF quantization is often more accurate than MLX at the same bit depth. 
  - For example, if you compare a GGUF q4_k_m with a 4-bit MLX model, GGUF tends to maintain better text quality and reduce errors, especially for larger models like 70b and 123b. 
  - However, MLX is generally faster, though this speed can come at the cost of precision, particularly in 2-bit quantization, where grammatical errors are more frequent.

- MLX's quants are a lot simpler and contains less information than llama.cpp's K quants.

- is it really worth it running a 123B model at 2-bit? Have you noticed any issues running it at that low of a precision?
  - I find ML 123B 'surprisingly' usable at IQ2M, better or on a par with 70B @ Q4KM for some tasks.

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
# discuss-tips/usage 💡
- ## 

- ## 

- ## 

- ## 

- ## 

- ## [Your settings are (probably) hurting your model - Why sampler settings matter : r/LocalLLaMA _202311](https://www.reddit.com/r/LocalLLaMA/comments/17vonjo/your_settings_are_probably_hurting_your_model_why/)
- Temperature
  - What Temperature actually controls is the scaling of the scores. 
  - Every time a token generates, it must assign thousands of scores to all tokens that exist in the vocabulary (32, 000 for Llama 2) and the temperature simply helps to either reduce (lowered temp) or increase (higher temp) the scoring of the extremely low probability tokens.

- Top K is doing something even more linear, by only considering as many tokens are in the top specified value, 
  - so Top K 5 = only the top 5 tokens are considered always. 
  - I'd suggest just leaving it off entirely if you're not doing debugging.

- Top P
  - This is the most popular sampling method, which OpenAI uses for their API. However, I personally believe that it is flawed in some aspects.
  - With Top P, you are keeping as many tokens as is necessary to reach a cumulative sum.

- Min P
  - we are setting a minimum value that a token must reach to be considered at all. The value changes depending on how confident the highest probability token is
  - So if your Min P is set to 0.1, that means it will only allow for tokens that are at least 1/10th as probable as the best possible option. If it's set to 0.05, then it will allow tokens at least 1/20th as probable as the top token, and so on...
  - "Does it actually improve the model when compared to Top P?" Yes. And especially at higher temperatures.
  - You might think, "but doesn't this limit the creativity then, since we are setting a minimum that blocks out more uncertain choices?" Nope. In fact, it helps allow for more diverse choices in a way that Top P typically won't allow for.
  - Min P emphasizes a balance, by setting a minimum based on how confident the top choice is.
  - 0.05 - 0.1 seems to be a reasonable range to tinker with, but you can go higher without it being too deterministic, too, with the plus of not including tail end 'nonsense' probabilities.

- Repetition Penalty
  - This penalty is more of a bandaid fix than a good solution to preventing repetition; However, Mistral 7b models especially struggle without it.
  - I call it a bandaid fix because it will penalize repeated tokens even if they make sense 
  - I recommend that if you use this, you do not set it higher than 1.20 and treat that as the effective 'maximum'.

- ## [Can someone explain what Top K and Top P are and what they do and how to use them? : r/AIDungeon _202408](https://www.reddit.com/r/AIDungeon/comments/1eppgyq/can_someone_explain_what_top_k_and_top_p_are_and/)
- Top K sampling is a method used to limit the number of potential tokens (words or characters) that a language model considers at each step during text generation.
  - During generation, the model predicts a probability distribution over the vocabulary for the next token. Instead of sampling from the entire vocabulary, Top K sampling only considers the top K most probable tokens.
  - A smaller K makes the output more deterministic and focused, while a larger K allows more diversity and creativity in the generated text.
- Top P sampling, also known as Nucleus Sampling, is an alternative to Top K that dynamically adjusts the number of tokens considered based on their cumulative probability.
  - Instead of choosing a fixed number of top tokens (like in Top K), Top P sampling selects the smallest set of tokens whose cumulative probability exceeds a threshold P (a value between 0 and 1). 
  - For example, if P = 0.9, the model will consider the smallest number of tokens whose combined probability is 90%.
  - Top P sampling is more adaptive than Top K. It allows for flexible token selection, which can lead to more diverse outputs while maintaining fluency. This method is particularly useful when you want to ensure that the model doesn’t pick from an overly broad or too narrow set of options.
- a high Top P (closer to 1.0) with a low Top K (under 50) often results in outputs that are more predictable and less diverse. 
  - Conversely, a high Top K (above 100 or so) with a low Top P (closer to 0) can result in outputs that are less coherent, with a mix of overly predictable and randomly selected tokens.

- Min-P is a much better sampler that replaces both Top K and Top P. 
  - The user set parameter is a percentage. Tokens within the selection pool must be more probable than the top token probability x the parameter. 
  - So, if you set it to 0.1 and the top token has a score of .9, every token with a probability over 0.09 is a possible choice. 
  - What min-p does better than the other two is adjust the size of the token pool dynamically to ensure you have a decent selection. The more likely that top token is, the higher the cutoff is. As it drops, you start getting more options, which is positive because you aren’t as sure of that top token anymore. This is pretty standard at this point in the local model world.

- ## [Memory Tests using Llama.cpp KV cache quantization : r/LocalLLaMA _202406](https://www.reddit.com/r/LocalLLaMA/comments/1dalkm8/memory_tests_using_llamacpp_kv_cache_quantization/)
  - Now that Llama.cpp supports quantized KV cache, I wanted to see how much of a difference it makes when running some of my favorite models. 

- how do you enable caching in llamacpp? is it only kv cache or also prefix cache?
  - The KV cache is always used. Its part of how llama.cpp generates. This post is about enabling quantization on the KV cache
  - llama.cpp server will do some caching by default depending on how you're using it. You can use "cache_prompt" when using the text completion endpoint. It also has a "slots" system for maintaining cache between requests.

- For future reference: if you want to cache using the v1/chat/completions OAI-compatible endpoint, with the OpenAI client, pass cache_promot as an extra_body parameter 

- ## 🤔 [Using KV Cache, Do You Notice any Quality Drop? : r/LocalLLaMA _202408](https://www.reddit.com/r/LocalLLaMA/comments/1ej8tjn/using_kv_cache_do_you_notice_any_quality_drop/)
- Use Q8 for K, Q4 for V is fine. Here is a comment from the guy who did the implementation in llama.cpp

- I've noticed a slight quality drop but the benefits outweigh the loss for me.
  - That's what I am experiencing too.

- On llama.cpp yes. On exllama not not as much.

- For me, q4 cache doing summaries of YouTube videos with llama 3.1 the number of hallucinations increases significantly compared with not using it.

- ## [What's with the obsession with reasoning models? : r/LocalLLaMA _202509](https://www.reddit.com/r/LocalLLaMA/comments/1nfqe2c/whats_with_the_obsession_with_reasoning_models/)
  - Why are practically all AI model releases in the last few months all reasoning models? Even those that aren't are now "hybrid thinking" models.

- Reasoning is great for making AI follow prompt and instructions, notice small details, catch and fix mistakes and errors, avoid falling into tricky questions etc. I am not saying it solves every one of these issues but it helps them and the effects are noticeable.
  - Sometimes you need a very basic batch process task and in that case reasoning slows you down a lot and that is when instruct models becomes useful, but for one on one usage I always prefer reasoning models if possible

- It is better at coding and math

- You nailed it, reasoning helps to reduce hallucination. Because there is no real way to eradicate hallucination, making LLM smarter becomes the only viable path even at the expense of token. The state of art is how to achieve a balance as seen in gpt 5 struggling with routing. Of course nobody wants over reasoning for simple problem, but hwo to judge the difficulties of a given problem, maybe gtp5 has some tricks.

- Reasoning models have their place, but not every model should be a reasoning models. Also not too big on hybrid reasoning models either since it feels like a worst of both worlds which is probably why the Qwen team split the instruct and thinking models for the 2507 update.

- I've found that all reasoning models have been massively superior for creative writing compared to their non-reasoning counterparts, 

- Another example is my Devstral Small 1.1 24B doing tremendously better than GPT-OSS-20B/120B, Qwen3 30B A3B 2507 all series, in Solidity problems. A non-reasoning model that spends less tokens compared to the latter models.
  - However, major benchmarks puts Devstral in the backseat, except in SWE bench. Even latest ERNIE 4.5 seems to be doing the exact opposite of what benchmarks say.

- I think there are two main appeals:
  - First, reasoning models achieve more or less what RAG achieves with a good database, but without the need to construct a good database. Instead of retrieving content relevant to the prompt and using it to infer a better reply, it's inferring the relevant content.
  - Second, there are a lot of gullible chuckleheads out there who really think the model is "thinking". It's yet another manifestation of The ELIZA Effect, which is driving so much LLM hype today.
  - The main downsides of reasoning vs RAG are that it is slow and compute-intensive compared to RAG, and that if the model hallucinates in its "thinking" phase of inference, the hallucination corrupts its reply.

- Reasoning models are exceptionally good at filtering through rules, injected corpo-required bias, overriding and ignoring the user's prompt, requiring injection of RAG and tool use to further deviate from the user's request and tokens used, correcting the pathways on way, and finally reasoning refusal and guardrails.

- ## 🆚 [Can someone explain the difference between a 4bit pre-quantized model and a quantized model? : r/LocalLLaMA _202409](https://www.reddit.com/r/LocalLLaMA/comments/1f92brm/can_someone_explain_the_difference_between_a_4bit/)
- Normal 4bit version process: [Download 16bit weights => Quantize to 4bit on the fly] => 4bit QLoRA / inference
  - Pre-quantized Unsloth weights instead: Download 4bit weights which is equivalent to [Download 16bit weights => Quantize to 4bit on the fly] => 4bit QLoRA / inference
  - So there's 0 difference between both, except I just pre-quantize it and save it so people can skip downloading all 16bit weights (16GB or so) and download a 4GB file + get 1GB or so less VRAM usage due to reduced fragmentation.
- Do you need 'load_in_4bit=True' when using pre-quantized model?
  - When using Unsloth, yes

- do I run the BF16 with "load in 4bit" checked and it's the same thing as the 4bit version?
  - Yes, this is the answer. The 4-bit models on Unsloth's page are quite literally just models that have been loaded in 4-bit and then saved to disk. So the quality will be exactly the same.
  - The main purpose is just to enable you to skip the download of the huge full model when you just intend to run it in 4-bit anyway. Which would be a waste of bandwidth and disk space.

- ## [Qwen3 30B A3B unsloth GGUF vs MLX generation speed difference : r/LocalLLaMA _202505](https://www.reddit.com/r/LocalLLaMA/comments/1kugp9h/qwen3_30b_a3b_unsloth_gguf_vs_mlx_generation/)
- Don’t use Q8_K_XL on a Mac. They use bf16 which is not good on a Mac
  - So what would you recommend? 6_K_XL or 8_0?
- 8_0 or fp16 in your case
- Definitely give Q8_0 a try! I might have to place a warning BF16 is slower for Mac devices
  - I did and yes apparently it was the issue. Now I am getting 75t/s with 8_0

- As someone mentioned below, Q8_K_XL might not function well on Mac due to BF16 being used - best to check Q8_0 directly - if Q8_0 still has reduced perf, it's most likely a llama.cpp backend issue.

- I’m having similar results but for Llama 4 Scout, when comparing an older Bartowski quant to the newer Unsloth quants. I’m getting about DOUBLE the speed with Bartowski’s IQ2_XS (46tps) vs Unsloth’s IQ2_XXS (22tps). I’ve even tried removing the vision encoder for Unsloth (it’s not supported by Bartowski) and Unsloth is still much slower.
  - Unsloth also seems to occupy less RAM and more VRAM than I’d expect, even though in both cases I’ve selected 48/48 layers offloaded to GPU, and there’s about 2.5GB of VRAM available.

- ## [Qwen3 30B A3B unsloth GGUF vs MLX generation speed difference : r/LocalLLaMA](https://www.reddit.com/r/LocalLLaMA/comments/1kugp9h/qwen3_30b_a3b_unsloth_gguf_vs_mlx_generation/)

- ## [188GB VRAM on Mac Studio M2 Ultra - EASY : r/LocalLLaMA _202401](https://www.reddit.com/r/LocalLLaMA/comments/192uirj/188gb_vram_on_mac_studio_m2_ultra_easy/)
- I think "time for first token" is slow because people don't use --mlock option, which preloads model and force it to stay in RAM and this is not default. It should not be a problem if use it.
  - This is true and will keep the model in along with additional memory for context which, depending in what you are using may not be allocated until it is required. MLX uses lazy allocation, only grabbing memory when it is needed. So, mlock is something you would always want set so the model doesn’t get swapped or paged out.

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

- ## 

- ## [Mistral 3.2-24B quality in MoE, when? : r/LocalLLaMA _202508](https://www.reddit.com/r/LocalLLaMA/comments/1mxmyhx/mistral_3224b_quality_in_moe_when/)
  - While the world is distracted by GPT-OSS-20B and 120B, I’m here wasting no time with Mistral 3.2 Small 2506. An absolute workhorse, from world knowledge to reasoning to role-play, and the best of all “minimal censorship”. 
  - GPT-OSS-20B has about 10 mins of usage the whole week in my setup. I like the speed but the model is so bad at hallucinations when it comes to world knowledge, and the tool usage broken half the time is frustrating.
  - The only complaint I have about the 24B mistral is speed. On my humble PC it runs at 4-4.5 t/s depending on context size. If Mistral has 32b MOE in development, it will wipe the floor with everything we know at that size and some larger models.

- The Qwen team has been killing it with MoE performance and quality at the same time. Definitely don’t go lower quality for the sake of speed.

- I use the same model alongside Qwen3-30B-A3B-2507 (reasoning) and it's kinda crazy how much obscure knowledge Mistral is able to pack into just a 24B param dense model. I rely on tool-calling with Qwen via RAG to get accurate information, but Mistral rarely requires that. 
  - A mixture-of-experts version of Mistral Small 3.2 would be incredible imo. And if they go that route, I really hope they use more active parameters than just 3-3.5B like Qwen & GPT-OSS do.
  - An MoE version of this model using 7-8B active parameters would be a dream. Hopefully at the very least Mistral are working on a successor to Mixtral(2023)/Pixtral.

- Tbh, recent Qwen3 thinking (both a3b and 4b) are crazy good for their size, especially in abliterated variants. However, the more you work with them, the more mistakes you notice, and going back to Mistral 24b feels like going back to a reliable (but predictable) setup.

- I would really love that. Mistral is not only intelligent, but also uncensored and creative. I'm usually disappointed with new small models because they all tend to be bland, despite being capable for their size.
  - My current dream right now is a Mistral Nemo 2 with clear improvements on the model's shortcomings.

- ## [Magistral Small 2509 - Jinja Template Modification (Based on Unsloth's) - No thinking by default _202509](https://www.reddit.com/r/LocalLLaMA/comments/1nnj83s/magistral_small_2509_jinja_template_modification/)
  - 80%~ of my tasks can be done without thinking really, 
  - From my tests Magistral without thinking performs similar to regular Mistral Small 3.2, Two models in one, why not, fast answers for simple tasks, thinking for complex.
  - This small mod is based on Unsloth's Jinja template: Magistral model will answer without any thinking by default, but if you add "/think" tag anywhere in system prompt, model with start thinking as usual, quick and simple solution for LM Studio etc.

- ## [Magistral 1.2 is incredible. Wife prefers it over Gemini 2.5 Pro. : r/LocalLLaMA _202509](https://www.reddit.com/r/LocalLLaMA/comments/1nmii5y/magistral_12_is_incredible_wife_prefers_it_over/)
- I tested the latest release of Magistral Small 2509 in three case scenarios using LM Studio.
  - Extract text from an educational YouTube video using an MCP server
  - Create a summary
  - Once the summary is complete, create a "clean" document from the informative text extracted from the video.
- I compared it with: -Qwen 4b no thinking -GPT 20b thinking medium -Magistral Small 2509 thinking -Qwen 30b instruct
- The best extraction with an MCP server was performed by Qwen 4b. 
  - Magistral Small looped even at low temperatures. 
  - GPT 20 was slower in processing the prompt, but everything was fine. 
  - Qwen 30b was slower than 4b, but the result was the same.
- In the summary, Qwen 30b won out, both in formatting and in terms of ease of reading and rewriting the video in a clean and presentable format (removing chatter, etc.). 
  - Unfortunately, Magistral was the worst, producing answers that were too concise, even when reworking the prompt. 
  - For this specific assignment, Qwen 4b + 30b is the best solution for both speed and final result. Using the MCP tools (YouTube search, video text extraction, Google search) was perfect. 
  - I'm keeping it(magistral) only for its image reading capabilities (OCR). 
  - I haven't tested other LLMs because I try to beat the current best (for me) in the real world use case. I suggest testing Magistral 1.2 in other real-world situations.

- translates better than qwen, yes

- For me, the vision capabilities exceed anything I've found on something I can run locally. Better than gemma 3, better than qwen 2.5vl, better than llava. It can read handwritten text and think about what it should be when it's a little sloppy. Can identify pictures with great accuracy and the contents and asking about the picture. The thoughts give helpful information.

- I pretty much only use VLMs for chart analysis and Magistral Small 1.2 seems comparable to Qwen2.5VL 72B, but I prefer Qwen's output 

- ## [Just dropped: Qwen3-4B Function calling on just 6GB VRAM : r/LocalLLaMA _202509](https://www.reddit.com/r/LocalLLaMA/comments/1nmkswn/just_dropped_qwen34b_function_calling_on_just_6gb/)
  - Fine-tuned on 60K function calling examples

- Qwen 3 4B 2507 versions were already excellent at tool calling tho. What improvements have you made over that?
  - DPO with extreme negative pairs on top of the base model with the same amount of samples. It’s the best checkpoint will post the tensor board, worked quite well with codex on initial testing. 

- ## [Would it be possible to run gemma3 27b on my MacBook Air M4 with 32GB of Memory/RAM? : r/LocalLLaMA _202503](https://www.reddit.com/r/LocalLLaMA/comments/1jig91a/would_it_be_possible_to_run_gemma3_27b_on_my/)
- I happen to have just purchased this exact configuration (MacBook Air M4 with 32GB)
  - I installed LM Studio today and did a couple of tests with Gemma 3 12B and Gemma 3 27B (both Q4_K_M). 
  - Gemma 3 12B produced output at about 10 tokens per second vs 4-5 tokens per second for Gemma 3 27B. 
  - Both sets of answers were on point, but I'd give the edge to Gemma 3 27B. However, Gemma 3 27B put a lot more pressure on memory and (especially) CPU.
  - The bottom line is that I can see myself using Gemma 3 12B a lot more often than Gemma 3 27B. 
  - I don't think the slight increase in quality makes up for waiting twice as long for the answer, and draining the MacBook Air battery while doing it.

- ## [Qwen3 is very.... talkative? And yet not very... focused? : r/LocalLLaMA _202506](https://www.reddit.com/r/LocalLLaMA/comments/1lh4ynv/qwen3_is_very_talkative_and_yet_not_very_focused/)
  - Is this the expected Qwen output? Is it just designed to act like an extremely chatty person with ADHD?

- Yes it is how it is, I tested 14b, 32b, 30b-3a, and smaller ones too. You can't really stop it from doing this. It is annoying
  -  I also don't like Qwen3's obsession of overusing line breaks.

- Yep I feel both Gemma and qwen3 are a bit talkative and not delivering the same raw straight to the point no bullshit wrapper words like deepseek v3 and r1 does.

- Another thing then these settings everybody said, is the "prompt template" (like ChatML, Alpaca, Llama 2, etc.). I found it affects the length of the answer if you get the wrong one.

- ## [Qwen 3 8B, 14B, 32B, 30B-A3B & 235B-A22B Tested : r/LocalLLaMA _202504](https://www.reddit.com/r/LocalLLaMA/comments/1kaqi3k/qwen_3_8b_14b_32b_30ba3b_235ba22b_tested/)
  - They all seem to struggle a bit in non english languages.
  - Coding is top notch, even with the smaller models.

- In my limited testings so far with Qwen3 - in a nutshell, they feel very strong with thinking enabled. With thinking disabled however, they seems worse than Qwen2.5.

- Ollama is slow compared to VLLM already... Less efficient.

- In my early testing the true magic with qwen 3 is in instruction following, tool use, and consistent a d reliable structured/formatted output. To me these are the most important qualities of a small/medium model so I am very happy.

- ## [46pct Aider Polyglot in 16GB VRAM with Qwen3-14B : r/LocalLLaMA _202505](https://www.reddit.com/r/LocalLLaMA/comments/1kukjoe/46pct_aider_polyglot_in_16gb_vram_with_qwen314b/)
  - After some tuning, and a tiny hack to aider, I have achieved a Aider Polyglot benchmark of pass_rate_2: 45.8 with 100% of cases well-formed, using nothing more than a 16GB 5070 Ti and Qwen3-14b, with the model running entirely offloaded to GPU.
  - That result is on a par with "chatgpt-4o-latest (2025-03-29)" on the Aider Leaderboard. 
  - The method was to start with the Qwen3-14B Q6_K GGUF, set the context to the full 40960 tokens, and quantized the KV cache to Q8_0/Q5_1. To do this, I used llama.cpp server, compiled with GGML_CUDA_FA_ALL_QUANTS=ON. 
  - Aider was then configured to use the "/think" reasoning token and use "architect" edit mode. The editor model was the same Qwen3-14B Q6, but the "tiny hack" mentioned was to ensure that the editor coder used the "/nothink" token and to extend the chat timeout from the 600s default.

- So, the combo Qwen3-14b-thinking as architect with Qwen3-14b no-thinking as coder, surpasses¹ the combo QwQ-32B as architect + Qwen 2.5-32b Coder (26.2%). It also surpasses² plain Qwen3-32b no-thinking (no architect) which scored 40%. That's impressive.

- ## [Qwen3-14B vs Phi-4-reasoning-plus : r/LocalLLM _202505](https://www.reddit.com/r/LocalLLM/comments/1kbzsdo/qwen314b_vs_phi4reasoningplus/)
- It will depend strongly on your use case. So test and check.

- I didn't try Phi 4 reasoning yet, but I was comparing Phi 4 vs Gemma 3 in translation project, Gemma 3 gave me better result but Phi 4 gets less hallucination.

- To me phi4 plus thinks too long. Personally, I slightly prefer qwen

- ## [Qwen3 14b vs the new Phi 4 Reasoning model : r/LocalLLaMA _202505](https://www.reddit.com/r/LocalLLaMA/comments/1kg5m5a/qwen3_14b_vs_the_new_phi_4_reasoning_model/)
- Qwen3 14B is smarter and can punch higher.
  - Phi4-Reasoning will follow the craziest instructions perfectly. It is near perfect at following instructions/formatting.
  - Phi4 will hopefully make fewer assumptions when explicitly instructed in its system prompt to quote only the provided information. This should make it more accurate for retrieving information instead of inserting its own ideas.

- I found Phi-4-reasoning to be a bit smarter (but not code), but requires almost 3x more tokens than Qwen3-14B to be so.
  - In terms of real usability, Qwen3-14B will be the better choice for the vast majority of people.

- Phi4 uses a significant amount more tokens while the output is of less quality than Qwen3.
- Qwen3 is the first local model that I can comfortabel use on my own hardware that gives me major GPT4 vibes, despite the weights being significantly lower.

- phi-4 spend more token than qwen3, so i prefer qwen3

- I recently tried qwen3-14b and aider.chat . Sometimes had trouble following format and would start doing weird things. Even qwen3-32b-q8 was hard to work with. Sometimes reasoning is off, also following exact directives and producing simpler solutions is a bit off. Of course that is compared to chatgpt-4o or claude 3.7

- My experience is that Qwen 3 is lot more smarter. I had high hopes for Phi-4. I want to love it. Being from Microsoft, it is lot easier to deploy it in the corporate environment compared to Qwen. But it was not great

- ## 🆚 [Qwen3-32b /nothink or qwen3-14b /think? : r/LocalLLaMA _202506](https://www.reddit.com/r/LocalLLaMA/comments/1l3yjeb/qwen332b_nothink_or_qwen314b_think/)
- from tests I've been running with medical exams, the qwen models scored as follows (all at Q8)
  - 32B /think - 85.5%
  - 14B /think - 84.5%
  - 32B /no_think - 84.5%
  - 14B /no_think - 77.5%
  - 8B /think - 77.5%
  - it was clear to me in testing them that the reasoning boosted them a lot for this task, that /think models often competed with the next /no_think model above it, and that when compared to other models, they all punch above their weight. 

- On 24GB VRAM, 14B Thinking (Q8_0) did slightly better than 32B non-thinking (Q4_K_M) in my testing.

- I prefer Qwen3-14B over the 30B-A3B model. While the MoE model obviously has more knowledge, its overall performance is rather inconsistent compared to the dense 14B in my experience

- If you're curious about actual benchmarks, the models are basically equivalent, with the only difference being speed
  - Thanks for this. Benchmarks between 30B-A3B and 14B are indeed nearly identical. Where the 30B shines is in tasks that require general world knowledge, obviously because it's larger.

- I don't use it with nothink very much. It performs with think so fast that you get the faster inference you're after with 14B but with intelligence a bit closer to 32B

- The more I use 30b the more "disappointed"I am. I'm not sure 30b beats 14b. It used to be my go-to-model, but then I noticed I started using 14b, 32b 
  - I think 30-A3B is more like an 12B that runs at 3B speed. It's a weird model... it's good at some domains while being hopeless at others.

- I am a Qwen3-14b shill. You get so much context and speed. 32b is good, but doesn’t give enough breathing room for large context.
  - 14b even beats larger models like mistral small for me.
  - This is all for coding — maybe I just prompt best with 14b but its been my fav model so far.

- I use Qwen3 30B instead of the 14B model, they are equivalent but for me the 30B runs faster, (30B Q5KM on gpu 50-75 tps, 14B Q6K on gpu 35 tps)
  - They are not equivalent. They are quite different tbh. My experience has been that the 14b runs better.
  - Also a rough estimate of the size is sqrt(A*T), A is active parameters and T is total parameters. The 30B is like a model of ~10B in size. 6B active would be closer to a 14B model.

- 32B /nothink for code, 30B-A3B in rambling mode for almost everything else.

- ## [Qwen3-14B vs Gemma3-12B : r/LocalLLaMA _202505](https://www.reddit.com/r/LocalLLaMA/comments/1kx2hcm/qwen314b_vs_gemma312b/)
- Qwen 3 for all technical stuff, and gemma 3 for creative/general autocomplete tasks for me.
  - Second this. Gemma3 is great at writing. Qwen3 is great for science and thinking. Mistral Small 3.1 would be the one off I would put here for second in both categories.

- For pure programming go with qwen, for the UX and UI design go with Gemma that can take screenshots as input.

- I have noticed that Qwen3 is not good in programming questions
  - Apparently qwen3 degrades a lot for coding under q6

- Why not use the 30b Qwen MoE? I think it will perform similarly to the 14b but run faster. I find the 30b to be a good model, it's only slight weakness for me is coding tasks
  - In my tests its much closer to 32b than to 14b really.

- Qwen seems less censored than Gemma. If you are going to use Gemma, I recommend an uncensored finetune.

- ## [Gemma 3 - GGUFs + recommended settings : r/LocalLLaMA _202503](https://www.reddit.com/r/LocalLLaMA/comments/1j9hsfc/gemma_3_ggufs_recommended_settings/)
  - Confirmed with the Gemma + Hugging Face team, that the recommended settings for inference are 
  - temperature = 1.0
  - top_k = 64
  - top_p = 0.95

- Do you have an explanation for why the recommended temperature is so high? Google's models seem to do fine with a temperature of 1 but llama goes crazy when you have such a high temperature. It is very very high for most models. Mistral Small goes completely off the rocker at 0.8.
  - The models are trained at temp 1.0
  - Reducing temp will make the output more conservative
  - To reduce outliers try min_p or top_p

- ## 🆚 [which model is less demanding on resources, gpt-oss-20b or qwen3-30b-a3b. : r/LocalLLaMA _202508](https://www.reddit.com/r/LocalLLaMA/comments/1mvjdxh/which_model_is_less_demanding_on_resources/)
- Briefly and in general:
  - Total parameters is proportional to memory requirements (more parameters more memory)
  - Active parameters is inversely proportional to inference speed (more active parameters less speed)

- gpt oss is A3.6B and qwen is A3B. qwen should be slightly faster, but it uses more memory (assuming similar quant levels).

- While the number of active parameters increases the memory bandwidth requirements which usually are the bottleneck for inference, they aren't everything. 
  - Especially for these small active parameter counts, some minor design aspects can affect performance much more. 
  - So ultimately you usually have to test on your hardware to really say. 
  - These two are generally super close, but, e.g., MXFP4 hardware support can impact performance a lot.
- One thing worth mentioning is that I have found Qwen3-30B to fall of with longer contexts much faster so even if they are competitive at the start, gpt-oss will be faster at the end
- Finally, with gpt-oss-20B being a smaller total size, you can fit a lot more context on a given GPU

- There's 2 resources you should be concerned about: memory and compute.
  - gpt-oss-20b uses ~33% less memory than Qwen3-30B-A3B, but because of the similar number of active parameters, the compute cost is similar.
- If you've got at least ~24GB of VRAM, go for Qwen3-30B-A3B. In my experience, Qwen3-30B-A3B is a more capable model, and it happens to hallucinate a lot less. You can also run Qwen3-Coder-30B-A3B if you want to use the model for code generation.
  - If you don't have enough VRAM, you'll just have to settle for gpt-oss-20b.

- Honestly, at these sizes just try them both on your setup and see which performs better. In my experience they're super close, although qwen3 requires more ram.

- I'd say both models are fairly comparable in capabilities, but they vary in style enough that they're both interesting to mess around with in their own way. Qwen also gives you more experience with the chatML prompt structure, which is more commonly used across many local models right now.

- ## [qwen3-30b-a3b thinking vs non-thinking : r/ollama _202508](https://www.reddit.com/r/ollama/comments/1mhjpe3/qwen330ba3b_thinking_vs_nonthinking/)
- For coding , thinking >> non thinking with same quant.
- why don’t they add reasoning capabilities to coding model?
  - Efficiency. It's more practical at execution not having thinking tokens. Unless you need extra brain power to solve more complex issues, that's where reasoning might help.
  - Different tools for different jobs.

- Some say Thinking model is better for coding. Theoretically it should, but in my personal testing, it wasn't, where Instruct was better.
  - Not saying Thinking model is worse overall, the point is, test in your own scenarios.

- I will stick with the previous version, because the answers come much faster and accuracy is nearly the same but much better than current instruct version.

- ## [Is a heavily quantised Q235b any better than Q32b? : r/LocalLLaMA _202507](https://www.reddit.com/r/LocalLLaMA/comments/1lx2dw4/is_a_heavily_quantised_q235b_any_better_than_q32b/)
  - I've come to the conclusion that Qwen's 235b at Q2K~, perhaps unsurprisingly, is not better than Qwen3 32b Q4KL but I still wonder about the Q3? 
  - Gemma2 27b Q3KS used to be awesome, for example. Perhaps Qwen's 235b at Q3 will be amazing?
- Q3 of Qwen3 235B may still be better than 32B, but likely much slower if you are short on VRAM and still have some quality issues associated with heavy quantization.
  - I agree. R1 is better & not much slower in token generation. But, prompt processing of Qwen3 235B q4 is quite faster.
  - I also tested Qwen3 235B q4 is better than Qwen3 32B Q8

- I run the official Qwen3 235B A22B INT4 GPTQ quant in vLLM using Qwen’s recommended settings.
  - It’s fabulous for coding and technical work. I love it. Destroys Qwen2.5 72B 8bpw exl2 in all my use cases.
  - However it drops off quickly at larger contexts. Once you get past ~ 16k it gets significantly dumber, makes syntax mistakes, etc. close to 32k tokens and it’s pretty bad.
  - But working inside that first 16k feels like I have a SOTA model right next to me. Fantastic.

- I use 2q from unsloth. It's better than the 32b, but it also uses like 6x the memory the 32b @ 4q does. The main advantage is speed. If it wasn't that, there's more bang for your RAM with other dense models. 

- I tried Qwen 235B at Q2_K; it's definitely not lobotomized at that point, it performed quite well in my test. I guess it might even be better than the 32B at Q8, but that would require a deeper comparison, which I haven’t done.

- ## [Running Qwen2.5-Coder-32b-q6-gguf entirely on cpu : r/LocalLLaMA _202508](https://www.reddit.com/r/LocalLLaMA/comments/1miqxdc/running_qwen25coder32bq6gguf_entirely_on_cpu/)
- 1 t/s. For CPU. 
  - Use the Qwen3-30B-A3B-Instruct-2507-GGUF. You will get roughly 15 t/s output, as its a MOE, but it's not as good as the 32b.

- Supposing you have dual channel memory set up right: 3200MHz * 8B * 2ch = 51.2GBps. The 32B @ Q6 (6.5bpw) is 26GB so theoretical max is 51.2GB/s / 26GB/tok = ~2tok/s. You should derate that by about 50% for normal CPU efficiency and you do indeed wind up with about 1tok/s.

- similar 32GB 5600g setup here if you're ok running latest debian sid (unstable), I managed to get 8-9 t/s using CPU/GPU offloading. (GPU here being the onboard APU). you could go up to 24GB for the apu.
  - debian unstable provides llama.cpp, rocm, etc, some custom kernel options at boot time and BIOS options for graphics memory.

- ## [What hardware do I need to run Qwen3 32B full 128k context? : r/LocalLLM _202507](https://www.reddit.com/r/LocalLLM/comments/1m5lze2/what_hardware_do_i_need_to_run_qwen3_32b_full/)
  - unsloth/Qwen3-32B-128K-UD-Q8_K_XL.gguf : 39.5 GB Not sure how much I more ram I would need for context?

- if you choose the 30Ba3B... I ran it on the AMD AI Max 395+ (Asus Flow Z 2025, 128G ram version)
  - and it runs amazingly well.
  - and lmstudio already provides rocm runtime for it (which my hx370 handle doesn't)
  - Somehow, I feel this would be the cheapest hardware? since you can get a mini-PC with this processor with the price less than a 5090?

- You don't need a GPU, AI Max 395+ has a 4060-level integrated GPU.
  - thus, with my personal test, it runs kinda slow with Qwen3 32B (Dense) model with <20 TPS, but with MOE models like 30Ba3B, it provides steady >30 TPS.

- KV cache will take 32Gb for 128K context. I'm using it with 64K context and it takes 16Gb.

- ## 🎯 [Magistral Small 2509 has been released : r/LocalLLaMA _202509](https://www.reddit.com/r/LocalLLaMA/comments/1njgovj/magistral_small_2509_has_been_released/)
  - Building upon Mistral Small 3.2 (2506), with added reasoning capabilities, undergoing SFT from Magistral Medium traces and RL on top
  - Multilingual: Supports dozens of languages: English, French, German...
  - Updates compared with Magistral Small 1.1
  - Multimodality: The model now has a vision encoder and can take multimodal inputs
  - Better tone and persona: You should experience better LaTeX and Markdown formatting
  - The model is less likely to enter infinite generation loops.
  - Reasoning prompt: The reasoning prompt is given in the system prompt.
- We release the model with `mistral_common` to ensure correctness
  - We welcome by all means community GGUFs with chat template - we just provide mistral_common as a reference that has ensured correct chat behavior
  - It’s not true that you need mistral_common to convert mistral checkpoints, you can just convert without and provide a chat template

- Small 1.2 is better than medium 1.1 by a fair amount? Amazing.

- 🐛 vLLM implementation of tool calling with Mistral models are broken, any chance they could be fixed?
  - I came to ask about tool calling as that was not mentioned and doesn’t seem to be much of a topic in this thread. Seems like so many open multimodal models (Gemma3, Phi4, Qwen2.5VL) are plagued with tool calling issues

- The GGUF isn't working for me with llama.cpp.
  - I changed to the unsloth version, it's working fine.

- Long context performance is very very very meh(普通的) compared to qwen3 14b (and above obviously)
  - It get lost at ~20-30k tokens, doesn't "really" reason and tries to output tool call in reasoning.

- For code, I did some small tests and I think devstral is still better along side qwen coder 30b, glm 32b and GPT oss 20b

- ## 🆚 [My simple test: Qwen3-32b > Qwen3-14B ≈ DS Qwen3-8 ≳ Qwen3-4B > Mistral 3.2 24B > Gemma3-27b-it, : r/LocalLLaMA _202507](https://www.reddit.com/r/LocalLLaMA/comments/1m1ylw0/my_simple_test_qwen332b_qwen314b_ds_qwen38/)
  - I have an article to instruct those models to rewrite in a different style without missing information, Qwen3-32B did an excellent job, it keeps the meaning but almost rewrite everything.
  - It's not writing, it's re-style an existing article.
  - Qwen3-14B, 8B tend to miss some information but acceptable
  - Qwen3-4B miss 50% of information
  - Mistral 3.2, on the other hand does not miss anything but almost copied the original with minor changes.
  - Gemma3-27: almost a true copy, just stupid
  - Structured data generation: Another test is to extract Json from raw html, Qweb3-4b fakes data and all others performs well.
  - Article classification: long messy reddit posts with simple prompt to classify if the post is looking for help, Qwen3-8, 14, 32 all made it 100% correct, Qwen3-4b mostly correct, Mistral and Gemma always make some mistakes to classify.
  - Overall, I should say 8b is the best one to do such tasks especially for long articles, the model consumes less vRam allows more vRam allocated to KV Cache

- There is a strong possibility that your test is overfitted to Qwen, leading to poor performance on other models.

- it might just be the problem with your prompt, or for whatever reason thinking models are super suited to your tasks.

- In my tests and workflows, which specifically do drive rewrites of large pieces of text, Gemma3-27b significantly outperforms Qwen3-32b which cannot follow the instructions well enough a lot of the time.

- Qwen3-32b has been the best local model to me. It is the only one I trust enough to handle some simple coding tasks with Aider. I do find Gemma 3 a little bit better in portuguese, though
  - Q6_K feels like the sweet spot to me. But the difference from Q4_K_M or Q8 is subtle
- qwen3:32b at full BF16 model size is phenomenal. Much better than Q8 for difficult questions, albeit at 0.3 t/s on a 128GB M3 Macbook.

- 32b is massively better than 30b. I use 30b as my main coding assistant model cause it stupidly fast, but it is not even comparable to 14b, let alone 32b.

- ## [Mistral small 24B 3.2 VS Qwen 3 30b/14b : r/LocalLLaMA _202507](https://www.reddit.com/r/LocalLLaMA/comments/1lt0a4n/mistral_small_24b_32_vs_qwen_3_30b14b/)
- Mistral Small 3 is an actual multilanguage model with a tokenizer specifically for that usecase. You can also try Mistral Nemo 12b, but in my experience it was slightly worse.

- Mistral is much stronger than Qwen models when it comes to swedish language.
- At least with Spanish, mistral was stronger in my use-case.

- Small 3.2 has way better general knowledge compared to Qwen 3. Where Qwen 3 excels is logic and coding.

- Mistral is way better at instruction following, it feels like a small version of Claude to an extent. If you need to code, try Devstral, and if you need reasoning, try Mistral.

- ## 🆚 [Mistral Small/Medium vs Qwen 3 14/32B : r/LocalLLaMA _202505](https://www.reddit.com/r/LocalLLaMA/comments/1knnyco/mistral_smallmedium_vs_qwen_3_1432b/)
  - Mistral medium is definitely an improvement over mistral small, but not by a whole lot, mistral small in itself is a very strong model. 
  - Qwen is a clear winner in coding, even the 14b beats both mistral models.
  - The NER (structured json) test Qwen struggles but this is because of its weakness in non English questions.
  - Overall, I feel Qwen 32b > mistral medium > mistral small > Qwen 14b. But again, as with anything llm, YMMV.

- To those claiming Gemma 3 27B is miles better than Mistral Small-3, how do you explain Mistral Small outperforming Gemma in most of those tests?
  - Mistral Small 25xx is unusable as a chatbot or creative writer, as it is very dry compared to Gemma 3 and suffer from extreme repetitions 

- ## [Daydreaming of a new Gemma model : r/LocalLLaMA _202508](https://www.reddit.com/r/LocalLLaMA/comments/1mgm8d3/daydreaming_of_a_new_gemma_model/)
- Gemma models is very underrated, has very impressive multi language and conversational capabilities. Probably the open source model with the most humanized style. but i can understand who do not have high praises, i think the biggest demand in local LLMs is for coding, a thing thats Gemma is not good at.
  - And the second biggest demand is uncensored writing, which Gemma is also not good at.

- Gemma 3 27B was the only local LLM that sucessfully annotated texts in non-english languages. Do you suggest any good < 130B parameter model for European language understanding? (Mistral was also not that bad)

- As a big fan of Gemma-2, I was very excited about Gemma-3, and of course it was cool to finally have more context, and the vision modality is also a valuable bonus, but what I personally loved about Gemma-2 was unfortunately a disappointment in Gemma-3. Namely, the subtle nuances and personality. That was ruined with Gemma-3.
  - In Gemma-3, it's somehow only superficially interesting. It has personality, but somehow it doesn't. A lot of it seems exaggerated or overfitted. In some tests I conduct privately, the Gemma-2 models perform significantly better than their successors.

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

- ## 🎯 [new mistralai/Magistral-Small-2507 !? : r/LocalLLaMA _202507](https://www.reddit.com/r/LocalLLaMA/comments/1m85vhw/new_mistralaimagistralsmall2507/)
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
  - Qwen team are also moving away from hybrid reasoning as they found it degrades performance. If that's what you're after try the recently released EXAONE 4.0

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
- smaller models need to think to get good results. The 30B MOE is guilty of overthinking too often to the point that I've given up on it.

- Qwen3 30b benchmarks are all around the same level as qwen3 14 but performance wise it is significantly faster up to 2-3 times tokenspeed as it only uses 3b active parameters at a time.
  - Though qwen3 30b is alot more sensitive to quantisation and will at q4 and below overthink stuff alot and make more mistakes. If you use it download the q6 version at least.

- Qwen3-14B is the best in South East Asian languages. Even with 4bit quant still very cohesive and good diction choice, much better than Mistral Small 24B 2506.

- Livebench has benchmarks. It's very good. Not far off from 32B actually.

- 🤔 Your last bullet point is the only one that matters. LLMs are tools. Describe your use cases.
  - most of the tasks i will be doing includes, RAG, Data Extraction from textual context, and few logical based QnA

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
  - The first one was Qwen3 30B A3B Instruct 2507 8bit. This model is much nicer it seems more "Human like" ie like a Nexus 6 vs a Nexus 4 etc.. The answers and modeled behaviors are much more interesting and personable. faster ie 72 tokens per second
  - The second one Qwen3 32B 8bit 8BIT seems more like just getting wikipedia answers, more of a formal Rigid feel to its behavior. slower ie less tokens per second 15 tokens per second.

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

- ## 

- ## [LiquidAI bet on small but mighty model LFM2-1.2B-Tool/RAG/Extract : r/LocalLLaMA _202510](https://www.reddit.com/r/LocalLLaMA/comments/1nuyjp9/liquidai_bet_on_small_but_mighty_model/)
  - So LiquidAI just announced their fine-tuned LFM models with different variants - Tool, RAG, and Extract. Each one's built for specific tasks instead of trying to do everything.
  - This lines up perfectly with that Nvidia whitepaper about how small specialized models are the future of agentic AI. Looks like it's actually happening now.

- ## [Best instruct model that fits in 32gb VRAM : r/LocalLLaMA _202509](https://www.reddit.com/r/LocalLLaMA/comments/1nqnabr/best_instruct_model_that_fits_in_32gb_vram/)
- For coding, this is SEED OSS 36B. it's a slower, but very smart model for it's size, and it may also do good on text. I know asking it various asian trivia produces great results versus qwen3 30B/32B ( SEED is more accurate and detail oriented, Qwen 30B is more like a speed reader )

- Honestly for summarization and question answering from RAG (In my case web results, ) GLM-4 32B has been very good and quite easy to manage. 
  - I have tested 30B A3B for several tasks and RP scenarios and it just does not perform anywhere near as well as a dense model. Yes, it is very efficient, and yes, it is quite fast, but if accuracy and steerability are important to you, I highly recommend dense models over these mini MoE releases.
- GLM4 suffers from severe context forgetfulness. Arcee-AI has fixed the base model to have better grip on context, and someone else made an instruct from tha

- GLM 4 32b has a very strong instruct variant that handles complex tasks well and might be worth a look.

- Since it's just text summarization you probably don't need a thinking/reasoning at all.

- ## [I'll show you mine, if you show me yours: Local AI tech stack September 2025 : r/LocalLLaMA _202509](https://www.reddit.com/r/LocalLLaMA/comments/1nnb8sq/ill_show_you_mine_if_you_show_me_yours_local_ai/)
- Qwen3 coder 30b is usable with qwen code CLI. You just need to run it with vllm with patched template and parser. Almost zero tool calling issues since then
  - [Qwen/Qwen3-Coder-30B-A3B-Instruct · How to achieve reliable native function calling](https://huggingface.co/Qwen/Qwen3-Coder-30B-A3B-Instruct/discussions/12)

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
