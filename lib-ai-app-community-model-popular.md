---
title: lib-ai-app-community-model-popular
tags: [community, large-language-model]
favorited: true
created: 2025-09-16T12:35:33.913Z
modified: 2025-09-16T19:59:57.856Z
---

# lib-ai-app-community-model-popular

# guide

- https://github.com/sst/models.dev /MIT/202511/ts
  - https://models.dev/
  - open-source database of AI model specifications, pricing, and capabilities
  - We also use it internally in opencode.
  - [OpenCode开发了一个所有AI模型(LLM)的数据库，完全开源并且可以免费通过API使用 - 知乎](https://www.zhihu.com/pin/1955588229391709336)
    - 按价格从低到高排序，你就能发现各个供应商都提供大量的免费模型。当然，免费模型都一定的额度限制。
    - 可以通过一个API路由（比如New-API：链接 ），来轮流使用这些免费模型，额度耗尽就自动切换下一家
    - 对Agent应用来说，获得一个模型的参数，比如上下文大小，可以作为程序决策的依据

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
  - [SuperCLUE中文大模型测评基准-AI评测榜单](https://www.superclueai.com/)
  - [CLUE中文语言理解基准测评](https://www.cluebenchmarks.com/)
  - [EQ-Bench 3 Leaderboard](https://eqbench.com/)
  - [UGI Leaderboard - Uncensored General Intelligence](https://huggingface.co/spaces/DontPlanToEnd/UGI-Leaderboard)

- leaderboard-tool-call
  - [Berkeley Function Calling Leaderboard (BFCL)](https://gorilla.cs.berkeley.edu/leaderboard.html)
    - claude, gpt, glm, grok, kimi, qwen3-235b, gemini-pro,watt-tool-70B,deepseek-r1
# discuss-stars
- ## 

- ## 

- ## 

- ## [为什么感觉deepseek“泯然众人”了，甚至被国内一些大模型赶超了 ](https://linux.do/t/topic/1182991)
- 不认同泯然众人，Qwen、GLM、KIMI 的最新模型都沿用来自 DeepSeek 的 MLA、DeepSeek-MoE、GRPO 等技术，虽然 “DeepSeek” 可能用的不多，但实际上处处是 “DeepSeek” 的影子。
  - 最近的 DeepSeek-OCR 从技术上一定程度补充了 “多模态” 的短板，并且一贯延续了 DeepSeek 的 “性价比” 路线，感觉可以期待下一代多模态模型表现。
  - 另外，从模型或产品体验上，DeepSeek 确实不如其他 LLM 大厂，个人认为战略定位应该更注重技术上的研发，背靠幻方或许也不急商业上的盈利。
- 认同，只看 benchmark 和效果确实可能不如那些堆算力几个月一更新的模型，但技术上确实是给国产的一系列模型很大的改变和效率提升了，本来国内进口 N 卡就受管制。

- 从 r1 开始到目前的几次更新，思维链、蒸馏、dsa 机制、vlm 等等。这些技术的目的都是在往死里压低成本。 现在国内的多模态、cli 式助手等等功能都发展得很快，但也不能因为这个去忽视 deepseek 这个模型是能够称得上有 “历史地位” 的。 没人压成本，都是 a / 那样的 opus 级别，你会用吗？4.1opus 刚出那时候，我为了尝鲜做一些试用，很简单地烧了 70 刀。对于 ai 的推广这个层面来说，贵得一笔的顶尖 ai，绝对比不上廉价而水平及格的 ai。

- 还好吧，ds 还是很好用的，泯然众人那到不至于，dsv3.2 翻译效果好而且便宜，回答小问题也不输给 qwen，就是看着没多模，属于水桶型选手，没有什么突出的点，但是遇到随机问题的效果不错

- 很正常，开创者通常不会最后的顶流

- Grok 得益于强大的社区资源，要搜集一些东西的最新情况、部分用户的小体验，非常有效。例如一些平台账号的防风控机制。

- Sam Altman 差不多每周现身频道发布新东西、参与大家讨论。 deepseek 我好像连一个主创人讲话的发布会视频都没见过。 单看品牌吸引力，我喜欢 OpenAI 和 Apple 这样的 有个明星企业人。

- LLM 想押中发展方向很难的，一个公司能押中一次都是极大的幸运了。 gpt 系列押中了数据规模的力大砖飞，deepseek 押中了 MLA 和 GRPO 的成本优化。 可你说后续你还想继续端出来这么大的提升，那太难了，全世界多少实验室多少科研人员都在努力，没道理成果都是一家出的。

- ## 💡 [The missing LLM size sweet-spot 18B : r/LocalLLaMA _202504](https://www.reddit.com/r/LocalLLaMA/comments/1jt9ig2/the_missing_llm_size_sweetspot_18b/)
- Yesh I think 16-24b is really a great sweet spot, hope we get some models of that size.

- Up your Phi4-14B quant or lower your Mistral3-24B quant. You'll probably get the effect that you're after.

- Just run an IQ3_XXS imatrixed of a 32b or similar.

- ## 🧩 [Can someone explain what a Mixture-of-Experts model really is? : r/LocalLLaMA _202511](https://www.reddit.com/r/LocalLLaMA/comments/1oqttg0/can_someone_explain_what_a_mixtureofexperts_model/)
- The core idea is that up to a certain point, more parameters means better performance through more stored information per parameter. However, activating every single neuron across every single layer in the model is extremely computationally expensive and turns out to be wasteful. So MOE tries to have the best of both worlds: a really large high parameter model, but only a fraction of them active so that uses less computation/energy per token.
  - During training, a routing network learns to send similar types of tokens to the same experts, and those experts become specialized through repetition. 
  - Nobody explicitly tells the experts what to specialize in. Instead, the specialization emerges because it's more efficient for the model to develop focused expertise. It's all happens emergently(在过程中，新兴的, 兴起的), and letting experts specialize produces lower training loss, so that's what naturally happens through gradient descent.
  - So the outcome is you get to have a relatively huge model but one that is still pretty sparse in terms of activation. So very high-performance at relatively low cost and there you go.

- The model has a router (fancy name for an FFN in MoE models) which decides which expert to use. This router is trained with the main model itself.
  - Activation parameters are just the (small portion of all parameters)/(expert) which are chosen by the router. To clarify these "small portion of all parameters" are just small FFNs nothing too fancy.

- An MoE model uses a normal embeddings and attention system, then a gate model selects n experts to pass those attended vectors to, then the output of the experts are merged into a final vector, which goes through a softmax(1 x vocab size) layer to get the probability for each possible token, same as normal models.

- ## 🤔 [Can China’s Open-Source Coding AIs Surpass OpenAI and Claude? : r/LocalLLaMA _202511](https://www.reddit.com/r/LocalLLaMA/comments/1omm6bf/can_chinas_opensource_coding_ais_surpass_openai/)
- Maybe one day, but probably not in the short term (1 year, and of course I may be wrong).
- Chinese LLM's have been catching up through (what I would say) 3 main ways:
  - Mixture of Experts and Reinforcement Learning
  - Synthetic data generation
  - Huge amounts of government and corporate funding.
- But I would argue that the main source of success is through #2, or synthetic data generation. 
  - And, often, much of that synthetic data is generated through western LLM's, a prime example being z.ai using the Gemini API for data, discovered through the similarities in word choices (also known as a "slop pattern") between Gemini flash and the glm 4 model. 
  - So, as Chinese LLM's are often trained off of western LLM's, it would be hard to ever truly get ahead. 
  - I will note, though, that this practice is slowly going away in favor of finding more efficiency gains (moe) and using RL for fine tuning. And, with strong government funding, it's possible that in the long term Chinese AI outperforms western AI.

- what china is not doing currently, but should : use mix of the models for each request, they basically should link glm/qwen/deepseek/kimi and stop fighting each other, instead colloborate

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

- ## [How come Qwen is getting popular with such amazing options in the open source LLM category? : r/LocalLLaMA _202511](https://www.reddit.com/r/LocalLLaMA/comments/1oziszl/how_come_qwen_is_getting_popular_with_such/)
- I think that Qwen will remain on top of opensource purely because of their small model sizes, almost all of their models can be run on consumer grade hardware (1 graphics card, under 16gb vram) and even when quants are needed it's usually higher than Q4 leading to less intelligence falloff.
  - I think another reason Qwen is doing so well is because they understand what the community needs, people don't want a 1trillion parameter model that *might* perform well but not be runnable on 99.8% of user hardware, they understand that most people will only be able to run

- In the image and video space, I also like that their models work together. For example, the Qwen Image latent is 100% compatible with the Wan video latent, so you can jump between them without decoding out to an image, then back to the latent space. They complement each other too, with different strengths, and if I need image edit capabilities, I can go to Qwen Image Edit, which again, keeps a large amount of compatibility, and is the best out there for that task in my opinion. Same goes for Wan.

- ## 🤔 [Why the hype around ultra small models like Granite4_350m? What are the actual use cases for these models? : r/LocalLLaMA _202510](https://www.reddit.com/r/LocalLLaMA/comments/1oku9og/why_the_hype_around_ultra_small_models_like/)
- They're super useful for testing! And almost all the new TTS architectures these days include an LLM backbone.
- So are you saying it would be good for the LLM for a super low latency STT-LLM-TTS stack?
  - No, the LLM is incorporated into the TTS itself, either by modifying the model to receive/output audio tokens, or by using the LLM as part of a larger architecture.
- ah, this is a good usage actually, they are much better than NER models.

- You can use it as a draft. Or finetune it for really simple tasks, especially for classification (although other approaches might be better). Probably useful for older devices too (again, for simple tasks).

- I have a huge Rag Faiss + BM25 database. When I need to filter results, I use small models. Even for tools. so you have embedding model + main llm and other small llm for rerank, classification, etc..

- I have a large multi agent system. With SLMs I can run everything locally.
  - No n8n or any other framework, just code for the orchestration of distributing a prompt to a multitude of other things, either agents, tools or SLM, coalescing and judging the responses of those things, and looping in the human.
  - SLMs let me run it all, to a limit obviously, locally. Even if I need to talk to 10 agents, which would be beyond what my machine can handle, I just queue them up, and the orchestrator waits for all to complete.

- It's all about context engineering. Use small models for trivial tasks that keep your orchestrator clean and focused. I use granite for detecting intent, parsing of pdf content like book indexes, summaries. I've even seen someone build a totally local mcp security "firewall" tool using SLMs.

- except embedding, i think they barely do anything good. classification, they do shit in my test. tool call?? they can't understand context at all.
  - so, in my test, the smallest usable model is qwen3 4B instruct. For embedding, nomic-1.5 can do a decent job. But i prefer embeddinggemma 300m. For 1B, I guess you have to finetune it with your own data from your real tasks.

- ## 🆚 [4B fp16 or 8B q4? : r/LocalLLaMA _202510](https://www.reddit.com/r/LocalLLaMA/comments/1ofb7mu/4b_fp16_or_8b_q4/)
- 8b q4 always wins.

- 4B FP16 ≈ 8 GB, but 8B Q4 ≈ 4 GB, there are two different sizes either way

- Bigger models with heavier quantisation are proved to perform better than smaller models with lighter quantisations.

- Perplexity changes are null at q8, manageable at q4 (lowest quant for coding/when you expect a constrained output like json), get significant a q3 (lowest quant for chat/creative writing, will not use for anything with that required accuracy.), Is arguably unusable at q2 (You start to see grammatical mistakes, incoherent sentences and infinite loop.).
  - Quantization under 4q lobotomizes the model too much. 4B q4 will perform better than 8B q2

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
# discuss-tool-call
- ## 

- ## 

- ## 

- ## 

- ## 🤔 [What’s the smallest, most effective model for function calling and AI agents? : r/LocalLLaMA _202503](https://www.reddit.com/r/LocalLLaMA/comments/1jd8lwp/whats_the_smallest_most_effective_model_for/)

- Small models don't do well with FC as a rule. They simply lack the reasoning. That said, there is the Hammer2.1-3b model at #26 on the BFCL

- From my experience, smaller models struggle with consistent tool usage, especially when multiple tools need to be chosen based on context. Even larger models like the 14b Qwen are underwhelming. That's the reality.
  - And yes, I've tried many small models 4B, 7B, 8B, 14B and adjusted context sizes and prompts without much success.

- [Open source model which good at tool calling? : r/ollama](https://www.reddit.com/r/ollama/comments/1ku4ejf/open_source_model_which_good_at_tool_calling/)
- Im using qwen3/Qwen3-30B-A3B with a specific systempromt. Works like a charm
- massive +1 Qwen3 has been way better for tool calling than Gemma3, Qwen2.5, and watt-tool
- Qwen3:8b with good prompts and examples worked great for me. Also tried mistral:7b, llama3.2, llama3.1, none of them even came close. The closet competitor in the 8B range was Qwen2.5
- We use gemma 3 and phi4 and they work really well for us. The issue we had before of the models always opting to use a tool, we solved it by adding a “send response” tool that breaks the loop.

- ## 🆚 [Why do reasoning models perform worse on function calling benchmarks than non-reasoning models ? : r/LLMDevs _202504](https://www.reddit.com/r/LLMDevs/comments/1kbj0bg/why_do_reasoning_models_perform_worse_on_function/)
- Function calling is finetuned behavior. Test time compute uses CoT behavior finetuning and RL-based rewards that weaken the function calling ability (via catastrophic forgetting?). A lot of the “thinking” chatter is also probably not improving the lost-in-the-middle attention problem either.

- ## [For local models, has anyone benchmarked tool calling protocols performance? : r/LocalLLaMA _202509](https://www.reddit.com/r/LocalLLaMA/comments/1ntcr1k/for_local_models_has_anyone_benchmarked_tool/)
  - I’ve been researching tool-calling protocols and came across comparisons claiming UTCP is 30–40% faster than MCP.
  - UTCP: Direct tool calls; native support for WebSocket, gRPC, CLI
  - MCP: All calls go through a JSON-RPC server (extra overhead, but adds control)

- UTCP seems to try and remove all of the QoL MCP has, and is just an imaginary "ok but imagine how cool it would be", but not practical.

- The communication overhead from tool calls will literally be the least relevant part of an LLM pipeline when it comes to performance. I do not see a point in using UTCP because none of the key players in the ecosystem (ie LLM front ends or APIs) are investing in it. It provides no additional value and instead just becomes an unnecessary wrapper or abstraction layer because some non-key players want to standardize an API that needs to be allowed to move incredibly fast.
# discuss-models-hot/features
- ## 

- ## 

- ## 

- ## [Nemotron 3 Nano 30B is Amazing! (TLDR) : r/LocalLLaMA](https://www.reddit.com/r/LocalLLaMA/comments/1pocsdy/nemotron_3_nano_30b_is_amazing_tldr/)
- If you want something that is almost as fast as qwen3 30b A3B but thinking in English, this is perfect.
  - it should be faster for long contexts solely because of using less than half as much memory per token of KV cache.
- Generation yes. PP, not.

- Out of curiosity, what are your use cases in which this model performed better than Qwen 3 Coder 30B A3B or Qwen 3 30B A3B 2507?
  - I'm also curious to my preliminary tests Qwen 3 Coder 30B A3B is still superior and faster
- I have something over 50 coding related prompts. I tested lots of different coding prompts with this and other Nemotron models. There was not a single AI response that would give me a code that would work out of the box.

- It is a good and fast model. And the fact that is truly open source is amazing.
  - But overall i think Qwen 30B 2507 is still better. In my tests it generated more functioning code and could follow very long conversations much better.

- ## [NVIDIA releases Nemotron 3 Nano, a new 30B hybrid reasoning model! : r/LocalLLaMA _202512](https://www.reddit.com/r/LocalLLaMA/comments/1pn8upp/nvidia_releases_nemotron_3_nano_a_new_30b_hybrid/)
  - Nemotron 3 has a 1M context window and the best in class performance for SWE-Bench, reasoning and chat.

- It's MoE, 3B active of 30B. Try Qwen A3B 30b models
  - this nvidia model is different architecture making it faster
  - "The model employs a hybrid Mixture-of-Experts (MoE) architecture, consisting of 23 Mamba-2 and MoE layers, along with 6 Attention layers. Each MoE layer includes 128 experts plus 1 shared expert, with 5 experts activated per token. The model has 3.5B active parameters and 30B parameters in total."
- There’s already DeepSeek V3.2, Granite 4, Qwen 3 Next, etc
  - Not all of those are mamba, DS3.2 is 100% attention but with sparse attention, Granite 4 is mixed mamba, Qwen 3 next is mixed gated deltanet.

- At first I though it'd be a nice drop-in replacement for Qwen3 30B A3B, but then I noticed that the Unsloth dynamic file sizes and normal quants are quite a bit larger.
  - Qwen3-30B-A3B-Thinking-2507-UD-Q4_K_XL.gguf is  17.7 GB
  - Nemotron-3-Nano-30B-A3B-UD-Q4_K_XL.gguf is      22.8 GB
- This is because the model has an architecture like gpt-oss where some dimensions aren't divisible by 128 so some cannot be quantized to lower bits and thus bigger.
  - That's also why we deleted some 1-bit and 2-bit sizes because they were exactly the same size

- Qwen 30b-a3b is quite a bit better at code generation than this Nemotron model in my testing. I wonder if Nvidia might release a coding-specific version at some point... Didn't test regular chat though.

- You still need as much memory as dense 30b model.
  - no you dont, you need the active B in gpu ram, and the inactive in system ram. I can run a 30B moe, I can't run a 14B dense mdoel

- I think people might be skipping over the fact that datasets are FULLY OPEN SOURCE!!!

- Considering that Qwen 30b is almost half a year old, it still stands strong in comparison. Impressive.

- What does it offer over Qwen3-30b?
  - Fresher training data.

- ## [Qwen3-4 2507 outperforms ChatGPT-4.1-nano in benchmarks? : r/LocalLLM _202512](https://www.reddit.com/r/LocalLLM/comments/1peav69/qwen34_2507_outperforms_chatgpt41nano_in/)
  - I know it's good but it can't be that good, surely?
  - Qwen3VL-4B Instruct just dropped. It's just as good as non VL version, and both out perf nano

- I use Qwen3:30B A3B instruct for various workflows in N8N. They run extremely well. I also use it for a very basic replacement to the cloud based providers (OpenAI etc) for simple queries. brilliant.

- ## 🆚 [Mistral 3 14b against the competition ? : r/LocalLLaMA _202512](https://www.reddit.com/r/LocalLLaMA/comments/1peql6c/mistral_3_14b_against_the_competition/)
- The instruct model is somewhat okay for non-reasoning use cases, but Qwen3 is better at the moment.
  - The reasoning model is pretty bad - it tends to infinitely overthink and hallucinates a lot.
  - In my experience in the same VRAM range gpt-oss-20B outperforms it on general tasks, and Qwen3 VL 8B is roughly on par with it for vision tasks and better for OCR. Idk about creative writing though, I think all creative writers have different opinions what a good writing is.
- I'm a die hard Mistral guy myself and I agree with your observation. Last good mistral model I used was the latest magistral. That one is very good. 

- ## [Ministral 14B vs Qwen 3 VL 30B vs Mistral Small vs Gemma 27B : r/LocalLLaMA](https://www.reddit.com/r/LocalLLaMA/comments/1pcgzkc/ministral_14b_vs_qwen_3_vl_30b_vs_mistral_small/)
  - I used Artificial Analysis to compare common benchmark.
  - I think Mistral did an awesome job: a 14B model performing almost on par with Mistral Small and Gemma and comparable with Qwen (Math apart where latest Qwen release is particularly good).

- Unfortunately benchmarks are getting more and more useless. It took me less than 5 minutes to realize Ministral 14B is not even close to Mistral Small 3.2 24B. Not that I expected it given the parameter difference.

- ## [Ministral-3 has been released : r/LocalLLaMA _202512](https://www.reddit.com/r/LocalLLaMA/comments/1pcb50r/ministral3_has_been_released/)
  - Ministral 3 14B offers frontier capabilities and performance comparable to its larger Mistral Small 3.2 24B counterpart. 
- Why would they not have a comparison to mistral small 24B? It makes no sense to not have a comparison to some larger sizes

- I also recommend the superior SmolLM3 by Huggingface which used in "Thinking mode" is also top on the iPhone SE 2022

- So it outperforms and basically replaces comparable qwen3 and gemma3 models, right?
  - I tested the 3b and 8b, and it did worse in just about every test except for translation. It failed most logic puzzles. Vision and summarization had too many hallucinations to be trustworthy.
- no, qwen3 30b vl severely outperforms ministral 14b while being faster.

- its good, but qwen beat them to the punch
  - qwen 3vl 30b just beats ministral 14b in every way. its better across the board, and its much faster, even for mixed CPU/GPU inference.

- The 14B outperforming Qwen3-14B on AIME is impressive. Are you seeing similar gains in code generation tasks, or is this mostly reasoning-focused?

- ## [Benchmark: Self-Hosted Qwen-30B (LoRA) vs. Llama-3.1-8B vs. GPT-4.1-nano. Comparison of parsing success rates and negative constraints. : r/LocalLLaMA](https://www.reddit.com/r/LocalLLaMA/comments/1p5e7mv/benchmark_selfhosted_qwen30b_lora_vs_llama318b_vs/)
  - I recently migrated a production workload off Claude Sonnet 4 ($45/1k requests) to cut costs. 
  - I ran a three-way experiment to find the best replacement: Qwen3-Coder-30B (Self-hosted) vs. Llama-3.1-8B vs. GPT-4.1-nano.
  - I expected Qwen3-Coder-30B to win on quality. It didn't.
  - The Task: Rewriting generic LeetCode problems into complex, JSON-structured engineering scenarios (Constraints, Role, Company Context).
  - My Takeaway / Question for the Community: I was surprised that Qwen3-Coder-30B couldn't beat the GPT-4.1-nano (a smaller model) on instruction adherence.

- Get a normal 30B A3B 2507 Thinking qwen instead of Coder.
  - In hindsight, you're likely right. Qwen-Coder failed on reasoning (negative constraints), not coding.

- ## [It been 2 years but why llama 3.1 8B still a popular choice to fine tune? : r/LocalLLaMA _202511](https://www.reddit.com/r/LocalLLaMA/comments/1p56v22/it_been_2_years_but_why_llama_31_8b_still_a/)
  - Llama 3.1 8b was releases in July 2024, so just over a year ago.

- Llama 3.1 8B is/was just kind of a known, fixed object particularly for researchers, and when reproducibility is a major factor, it makes sense to use the model organism so to speak. Think of it like a standard lab rat. 
  - I do think Olmo3 7B is likely to become the new mouse in the lab though. It’s a good model, just off the bat, but the multiple checkpoints and open data make it the perfect research model.
- In comparison to Llama 3.1 8B or Qwen 3 8B or Mistral 7B it uses way more memory than expected.

- I once finetuned qwen2.5-7b on a math dataset and it performed worse compared to a funetuned llama3.1-8b
  - Same, Qwens have too much knowledge baked in so don't fine tune as well.

- When Meta trained Llama-3, they started by training the 405B on fifteen trillion tokens, and then distilled the 70B and 8B from that. That means their training tokens to parameter ratio was only about 37:1, marginally above the Chinchilla threshold.
  - They didn't know it at the time, because this study hadn't been published yet, but that resulted in a model with a large set of memorized knowledge and fairly weak generalized knowledge (fewer parameters encoding heuristics), which is reflected in its skillset.
  - That makes it an excellent candidate for continued training, which cannibalizes the parameters for memorized knowledge and replaces them with more generalized knowledge the more it is trained.
  - I don't think this was deliberate, but researchers have learned by practice that Llama-3 provides an excellent vessel for whatever skills they want to pour into it.
- you’re right they are pretrained separately. just that 405b’s output is used to instruct fine tune 8b and 70b.

- It's supported everywhere and not only well characterized, but also super well supported. When training w/ Liger kernels, it is fast in a way even other supported models aren't. Every trainer has example files for Llama 3. It's also a "good enough" base (wheareas, something like Llama 2 or Mistral 7B isn't) even in late 2025 for working on (assuming you don't need to solve AIME 2025 problems).
  - Gemma 2/3 9B are way more capable, but the license makes it basically unusable IMO 
  - Qwen 3 8B is also a much smarter (benchmaxxed) model, however it has Qwen's particular trait of leaking random Chinese (and English for other language output!) - this is harder than you'd expect to fix and not a problem w/ most other models. At the the same size, Qwen models also simply train slower
  - Nemotron Nano 9B v2 - a good model, but Mamba2-Transformer Hybrid - OOTB perf was a little disappointing for things I cared about, but it's reasoning/STEM is also far beyond Llama 3
  - Olmo 3 7B - I think it's probably useful for a lot of cases (open license, easy to work with, open data/checkpoints), but I found initial eval perf for my purposes underwhelming
  - Granite 4.0 Tiny / H Tiny - I'll mention this one as another contender that left me less than whelmed w/ its OOTB perf. I find the MoEs more interesting, but the 7B didn't hit the spot for me (even the Small/H Small punched below my expectations, but I like what the Granite guys are doing)
- The other nice thing is that actually you can move down to Llama 3.2 1/3B with basically the same recipe (anything where you can move across size classes in the same family w/ is actually a big bonus).
- While you get a lot more capabilities going up to 14B class, 7-8B is realistically what you can fit in most desktop/consumer GPUs, and can even inference acceptably fast on most laptop APUs.

- I think Ministral was sort of forgotten by everyone because it was so forgettable. It wasn't so bad, but Tekken 3, interleaved SWA, ever so slightly better scores than Llama 3, wrapped in a license that basically makes it a non-starter if you're not an academic or home user.
  - While I liked Small and Magistral, and I think Voxtral is actually super neat, I'm not sure what Ministral's sell really was for anyone that wasn't Mistral. 
  - I actually recently did an eval of it on a lark when comparing 8B class base models and it's JA at least wasn't very impressive.
- I think we're actually seeing more 3-4B dense models climb into the old 7-8B class, than any new advanced 8Bs... (probably partly driven by how MoEs have been changing the landscape).

- Gemma 12B is far superior in my experience, and Solar-10.7B (NousResearch) is better for erotica, so I consider Llama 8B, and any of its finetunes, as obsolete for me.
  - Llama is still better at long context than Gemma, which was frankly abysmal in my tests.
- Fair enough, but if long context matters that much, then I'd use the 70B model.

- ## Gemini 3 明确不是 Gemini 2.5 的微调，它是全新训练的 sparse MoE 。 _202511
- https://x.com/dongxi_nlp/status/1990878844442583532
  - 也就是说，在 Gemini 2.5 已经非常出色的 RL 后训练和 parallel thinking 基础上，崭新的 backbone 让 Gemini 3 非常出色，总结这半年 Gemini 的工作：
  - 出色的 RL 后训练
  - parallel thinking
  - 崭新的 backbone
  - 一个又一个公开的对行业有益的benchmark，如 IMO-Bench

- ## [Who is using Granite 4? What's your use case? : r/LocalLLaMA _202510](https://www.reddit.com/r/LocalLLaMA/comments/1og2k8e/who_is_using_granite_4_whats_your_use_case/)
- I created a sexbot agent to test other compliance related filters etc. and surprisingly Granite handles this very well lol.
  - I am testing Granite Guardian 3.3 in my setup for both input and output. To test the output gets filtered, I told the agent to be an extremely vulgar and sexual dominatrix. Other models will reject this kind of system prompt, but not Granite 4.

- Using Small model to test MCPs I'm developing, it's very good at tool calling

- IBM recently showcased a “contract analysis” use case powered by their Granite 4.0 models. Has anyone tried these use cases yet?

- ## [Granite4 Small-h 32b-A9b (Q4_K_M) at FULL 1M context window is using only 73GB of VRAM - Life is good! : r/LocalLLaMA _202510](https://www.reddit.com/r/LocalLLaMA/comments/1nzozpg/granite4_smallh_32ba9b_q4_k_m_at_full_1m_context/)
- It’s one of the few models I’ve found to actually execute multiple native tool calls in response to a single prompt as well as GPT-OSS does, so it’s already impressed me I that regard already. It’s Mamba-based so that’s a different animal as well. It’s passing some basic RAG vibe checks, right now, but haven’t tried it with anything truly big yet.

- Totally can't code

- [Granite 4 (gguf) is useless if you try to use the full 128k context. : r/LocalLLaMA](https://www.reddit.com/r/LocalLLaMA/comments/1nzzurf/granite_4_gguf_is_useless_if_you_try_to_use_the/)
- Since IBM didn't provide recommended sampling params and said to try different ones for your usecase, I found that lowering the temperature from Unsloth's recommended 1.0 to 0.1 greatly increased its ability to do logic/math type stuff. You may want to experiment with temperature for your use-case as there is no actual reason to keep it at 1.0 besides a "default" that unsloth settled on in the absence of official guidance.
  - Yeah, this model definitely needs low temps. I noticed they added a recommended temp of 0 in their docs. https://www.ibm.com/granite/docs/models/granite
  - The Granite 4 models work best with temperature set to 0 for most inferencing tasks.

- ## [How's granite 4 small 32B going for you? : r/LocalLLaMA _202510](https://www.reddit.com/r/LocalLLaMA/comments/1nwr6sb/hows_granite_4_small_32b_going_for_you/)
  - Accuracy on some hard questions is a little challenging ( less smart than SEED OSS ) but it does good with clarifications.
  - Output length is short and to the point, doesn't spam you with emojis, fancy formatting or tables ( i like this )
  - Memory consumption is extremely low per K of context, I don't understand how i can jack the context up to 512k and run it on a 5090. Memory usage doesn't seem to climb as i fill up the context either.

- I tried pushing its context limits dumping a repo of code of about 48k and asking questions until the context filled up to 128k. The fuller its context, the “spacier” it would behave. At full, asking questions about specific files it would tend to hallucinate instead of remember what it read.
  - It’s incredibly fast. There is virtually no difference speed-wise between empty and full.

- It is fast and does not eat memory per unit context because it is not a transformer, it is a Mamba.

- I used it to summarize some Wikipedia articles and it was a lot better than GPT-OSS-20B, less chatty than Qwen 30B-A3B. I'd say it's the best of the smaller MOEs so far for RAG and text understanding. Ask it to summarize important points and it outputs just that list of points, without the usual "Here's a list of points" or some emoji nonsense.

- Pretty solid on my usual vibe check and general knowledge questions, lacking on creative writing.

- i don't really believe SSM blocks are as capable as transformer blocks. they use less resources, so that's why they are popular, but even really well designed SSM and hybrids just don't have that spark for me. that said, maybe your task will work ok? the capability difference varies per task and stuff like data extraction should be fine.

- [How has everyone been liking Granite 4? : r/LocalLLaMA](https://www.reddit.com/r/LocalLLaMA/comments/1nwnlp8/how_has_everyone_been_liking_granite_4/)
  - How's the creative writing quality compared to other models in this size range? I'm interested in whether it feels more natural or still has that AI voice.
    - Bad, it's an IBM model, it's dry, as any office clerk

- ## [Thoughts on Apriel-1.5-15b-Thinker ? : r/LocalLLaMA _202510](https://www.reddit.com/r/LocalLLaMA/comments/1nw0m6u/thoughts_on_apriel1515bthinker/)
- Tested it on multiple tasks , thinks fo way way way too long and is not as good as people make it to be.

- Based on my testing, this ai is mind blowing. It excels in Reasoning and maths, i was very impressed. It was not that great in coding.
  - The only downside is that it thinks a looooooootttttttt. I made this complaint to the creator of this ai model and he/she said we have currently set the thinking budget to high in the official space (which is where i tested it). So they might release an instruct or low/mid thinking budget one soon.

- this seems to be more tailored to reasoning and maths, not coding or creative writing 

- [So has anyone actually tried Apriel-v1.5-15B? : r/LocalLLaMA](https://www.reddit.com/r/LocalLLaMA/comments/1nvbu3h/so_has_anyone_actually_tried_aprielv1515b/)
- What's the modern model of choice in 12-30b range? Outside GPT-OSS? 
- exaone-4.0-32b
  magistral-small-2509
  mistral-small-3.2
  qwen3-30b-a3b-thinking-2507
  seed-oss-36b-instruct'

- Its reasoning is indeed interesting, but the model is severely censored. Plus, it can go off the rails trying to "reason" through conflicting instructions. Magistral, Qwen3 (both 4b and 30b) and aquif-3.5-8B-Think are much more stable.

- [don't sleep on Apriel-1.5-15b-Thinker and Snowpiercer : r/LocalLLaMA](https://www.reddit.com/r/LocalLLaMA/comments/1nv5uw8/dont_sleep_on_apriel1515bthinker_and_snowpiercer/)
  - their previous model was https://huggingface.co/ServiceNow-AI/Apriel-Nemotron-15b-Thinker which is a base model for https://huggingface.co/TheDrummer/Snowpiercer-15B-v3
- From my tests it works around Qwen3-4B-Thinking-2507 level. Only Snowpiercer 3 is kinda fun as NeMo 12b alternative. It is not even close to Qwen 3 30B A3B 2507 q6k.

- ## [What's the current best local model for function calling with low latency? : r/LocalLLaMA _202510](https://www.reddit.com/r/LocalLLaMA/comments/1ofg6w9/whats_the_current_best_local_model_for_function/)
- Generally, 3-4b models today are quite capable. I'd recommend trying out below models and picking one that works best:
  - Granite 4.0 tiny (MoE, 8b total 1b active) (should be fastest)
  - Granite 4 micro (3b, dense model)
  - Qwen3-30b-a3b Instruct-2507 (MoE, 30b total 3b active)
  - GPT-OSS-20b (MoE, 20b total 3.6b active)
  - Qwen3-4B-Instruct-2507 (4b, dense model)

- Gpt-oss-20b will be very fast even with thinking and is pretty good with tools. 
  - Another option is a non-thinking qwen model, Depending on the complexity thinking may not be needed.
  - 3bit glm air may be an option, but 3 bit quanization is pushing it.

- ## [Datarus-R1-14B-Preview, an adaptive multi-step reasoning LLM for automated data analysis : r/LocalLLaMA _202508](https://www.reddit.com/r/LocalLLaMA/comments/1mve5hp/datarusr114bpreview_an_adaptive_multistep/)
  - 14B-parameter open-weights language model fine-tuned from Qwen2.5-14B-Instruct, designed to act as a virtual data analyst and graduate-level problem solver.
  - Unlike traditional models trained on isolated Q&A pairs, Datarus learns from complete analytical trajectories—including reasoning steps, code execution, error traces, self-corrections, and final conclusions—all captured in a ReAct-style notebook format.
- we're been working on this project for almost a year even before Qwen3 was released, there'll be new releases of that might have a different base model

- ## [What is Gemma 3 270M actually used for? : r/LocalLLaMA _202508](https://www.reddit.com/r/LocalLLaMA/comments/1mwwr87/what_is_gemma_3_270m_actually_used_for/)
- Small models are terrible at storing facts and world knowledge.
  - On the other hand, they can be great at doing a specific task - summarization, translation, query rewriting, using tools, data extraction, etc.

- I am just impressed by the fact that a 270M model, which is smaller than encoder-only models like DaBERTa, can generate coherent sentences that are relevant to the input text, and not a random bunch of words put together.

- It’s meant to be fine-tuned for a specific task and from what I’ve read performs fairly well when it has been fine-tuned.

- either speculative decoding or low-resource fine-tuning.

- ## [We put a lot of work into a 1.5B reasoning model — now it beats bigger ones on math & coding benchmarks : r/LocalLLaMA _202511](https://www.reddit.com/r/LocalLLaMA/comments/1ou1emx/we_put_a_lot_of_work_into_a_15b_reasoning_model/)
  - We’re just a small team, and this model isn’t really meant to be a general chatbot right now. It was designed mainly for competitive-style math and coding problems. (You can see our table, the GPQA metric is not too high. Small models don’t have much knowledge, but they can still reason really well.)
  - We released it to support this idea: https://x.com/karpathy/status/1814038096218083497?s=20 (maybe reasoning doesn’t actually need huge parameter counts)
- Reasoning may not need huge parameter count, but knowledge does and good reasoning requires good knowledge, otherwise you're reasoning over factually incorrect hallucinations.
  - Yes, I totally agree with you. This round was just an extreme test to see if a 1.5B model can show strong reasoning ability. We’ll train a more practical version for general use and reasoning with knowledge later, which will be larger than 1.5B.

- Can you give examples of math/coding problems that this model works well with? Does it have to be prompted in a certain way?
  - For math questions: You can start with the prompt:“Let’s think step by step and output the final answer within \boxed{}.” Then input your question after that.
  - For coding problems: You can ask it to “write a Python program to achieve [your goal].” It helps if you can provide some input/output examples — or you can just describe the function to implement, similar to how problems are defined on LeetCode, AtCoder, or Codeforces.
  - Still recommend you to use competitive style math / python algorithm tasks

- With the default system prompt this model always puts the result into a box. This seems to be geared towards(调节来达到) common benchmarks where the result is expected to be boxed.
  - Good catch. Yes, the boxed output comes from math data, since most of them expect that format for easier verification.
  - Right now this version is more of a technical exploration, we’re testing how far small models can go in reasoning through training techniques. The token usage is something we’ll optimize in future, more practical versions.

- The token consumption seems rather high for simple tasks. 
  - VibeThinker is slightly larger than that Granite model and uses more tokens - on easy tasks. One reasonable thing to do during post training would be not not just show the model extensive reasoning, but also sufficient cases where this can be kept shorter. Still, it'd be an optimization. Get it right first, optimize while maintaining correctness later.

- why did you use qwen 2.5 as the base model instead of 3 series?
  - We’re mainly exploring how far small models can go in reasoning compared to large ones, and Qwen2.5 already fit our research goal.
  - Also, a lot of related work is based on Qwen2.5, so it made comparisons much easier (like DeepSeek-R1-Distill-1.5B is originated from Qwen2.5-Math-1.5B). That’s why we didn’t switch to Qwen3 for this round.
- why start with Qwen2.5-Math if it had weak math and coding ability to start with? Why not go with a Qwen3 base? 
  - Currently, a large amount of post-training work on 1.5B models is based on either Qwen2.5 1.5B or DS-distilled 1.5B (based on the Qwen2.5 Math). To ensure a fair comparison with existing work, we adopt the Qwen2.5 Math.

- I tested it and its coding skills seems similar to qwen-2.5-coder 7B or better, for my first rounds.

- Roo appears to be stuck in a loop, attempting the same action (update_todo_list) repeatedly. 
  - Not rly surprised that a 1.5B math model cannot code
- It's better suited for competitive programming, for example, you could try participating in LeetCode weekly contests.

- ## [Benchmark Results: GLM-4.5-Air (Q4) at Full Context on Strix Halo vs. Dual RTX 3090 : r/LocalLLaMA _202511](https://www.reddit.com/r/LocalLLaMA/comments/1osuat7/benchmark_results_glm45air_q4_at_full_context_on/)
  - Both tests were conducted under Debian GNU/Linux with the latest llama.cpp builds from the day of testing.
  - 3090: 5 tops
  - strix: 4 tops

- Why is the prompt processing for RTX is so low? It should be hundreds if not thousands. The model is too big and you have to spill some part to regular system RAM? These prompt processing figures make it unusable in such setup then
  - Because of offloading. It should be immediately obvious that air Q4 requires offloading for 48gb vram, yet even with offloading it still beats Strix halo. Imo energy efficiency doesn't matter too much here since <2kw is still not a significant amoun

- Prefill with cpu offload still runs pp on the GPU. The bottleneck is your pcie speed as it needs to upload all experts. I'll get you numbers for my rtx 5090 with pcie5 x16 to compare. Sounds like you did 119702 tokens? I'll do that.

- ## 🆚 [Imagine you’re stuck with one local model forever: GPT-OSS 120B or GLM 4.5 Air. Which one are you picking and why? : r/LocalLLaMA _202511](https://www.reddit.com/r/LocalLLaMA/comments/1otreir/imagine_youre_stuck_with_one_local_model_forever/)
- What speeds do you get on strix with glm air?
  - i did some tests recently, it's with full context which drops to around 5ts when you saturate context with ~130k, but lower than that it's fine. 
  - starting from around 24ts and going down with context grow 

- GPT OSS 120B on Strix Halo. The native format (MXFP4) runs at 40+ TPS with small context windows, and still fast with higher context windows.
  - GLM Air 4.5 is much slower (about half the speed)

- GLM 4.5 Air because it's more versatile. And GPT-OSS 120B gives a lot of refusals on benign things.
  - Easily fixed with a system prompt. That being said, I prefer Air.

- 120b is stronger at STEM but heavily aligned, refusals are not difficult to trigger

- ## 🆚 [GLM 4.5 Air vs GLM 4.6 vs Minimax M2 on 120gb VRAM : r/LocalLLaMA _202512](https://www.reddit.com/r/LocalLLaMA/comments/1ooq9q3/glm_45_air_vs_glm_46_vs_minimax_m2_on_120gb_vram/)
  - I've been using 4.5 Air AWQ 4-bit and it fits comfortably with a fairly high context limit and is quite usable for coding. However I'm wondering if it makes sense to try a low quant GLM 4.6 or if a quant of Minimax M2 would be a better coding assistant.
- As far as GLM Air, the REAP is working well for me for agentic coding. I run it at 6 bit with 96G vram and 145k context. You could probably fit 8 bit REAP in 128G depending on how much context you need. I feel it is a better tradeoff than lowering the bits.
  - it's really not, reap models lose way more knowledge than dropping quantization down a bit or two.

- I'm running GLM Air 4-bit mode with 96GB of RAM, and I'm encountering an out-of-memory error with a 120k context timer. I'm using llama.cpp. 

- Q2 GLM 4.6 will be much smarter than Air, but if you also want to fit a lot of context it will be a tight fit indeed. possibly REAP can work, but I have heard mixed results to say the least.

- In the last couple of days I’ve been testing Minimax M2, Q4 MLX, and Q4 UD Unsloth. GLM Air full quant surprised me, but Minimax M2 feels on par with commercial models—tool-calling and instruction-following are excellent, and its knowledge is solid. It’s my favorite now

- stick with 4.5 air for now. GLM 4.6 doesnt offer enough improvement to justify lower quants or RAM offloading, you'll lose more in infeence speed than you gain in quality tbh. Only worth upgrading it if you're hitting specific limitations with 4.5 air's coding abilities

- ## 🆚 [Any changes for the worse in deepseek V3 versions? : r/LocalLLaMA](https://www.reddit.com/r/LocalLLaMA/comments/1on6y2b/any_changes_for_the_worse_in_deepseek_v3_versions/)
- It is not worth saving the older versions, the newer releases reason better, follow instructions better, tool call accurately, hallucinate less, they are obviously superior. (V3.1 Terminus, V3.2 is slightly worse because of sparse attention)

- You missed one version: OG V3 (Dec 2024), V3 0324 and only then V3.1, Terminus, V3.2.
  - If used for creative fiction the all are very different. OG V3 AFAIR felt like classical LLM from 2024, say Mistral Large; V3 0324 is wittier and more unhinged; 3.1 is clinical but less sloppy, more natural sounding; terminus was creepy a bit; 3.2 IMHO is closer to OG V3 than to any other version.

- ## 🆚 [gemma-3-27b-it vs qwen3-32B (non-thinking) : r/LocalLLaMA _202511](https://www.reddit.com/r/LocalLLaMA/comments/1onbqtv/gemma327bit_vs_qwen332b_nonthinking/)
- Gemma3 still gets clobbered(痛打, 挫败), even in Western knowledge.

- Qwen destroys Gemma in every way, Gemma has the advantage of having a QAT model, so it would use less vram than qwen but even still I would pick qwen 

- Well you could try the newer Qwen3-VL-32B model, that has its own Instruct and Thinking models separate. And I guess it will be better than those older ones.

- ## [What is the difference between qwen3-vl-4b & qwen3-4b-2507 ? : r/LocalLLaMA _202511](https://www.reddit.com/r/LocalLLaMA/comments/1ollh15/what_is_the_difference_between_qwen3vl4b/)
- On their github and huggingface pages for the model they have a comparison of their benchmarks for the two versions.
  - tldr; for the 4b model for text it improves only pure subjective measurements, the others get worse.
  - for the 8b model it is a slight improvement across the board since there is no comparable -2507 release

- I was looking at the four 30B-A3B models - instruct, thinking, vision instruct and vision thinking.
  - I realized that the class of problems that I could address with Qwen3-30B-A3B-Thinking that I could not with Qwen3-VL-30B-A3B-Instruct was very small.
  - I said fuck it and now run the instruct vision model as my workhorse. For the everyday always on llm things that matter to me like ocr, simple questions, creative writing, summarization etc it is fast and good enough.
  - The thinking ones are good at math, stem, coding - and I need much more powerful models for those anyways. 
  - If a problem really needed thar extra knowledge, intelligence, reasoning and instruction following oomph I will have better luck at the rung up heavier model, not another 30B variant.

- The 8B VL instruct seems pretty good, and maybe better than the original Qwen 3 8B non-VL. The 30B-A3B VL instruct seems to be roughly on par with the 2507 30B-A3B instruct model for text tasks, I don’t notice any significant difference.

- ## 🆚 [GLM-4.6 vs Minimax-M2 : r/LocalLLaMA _202510](https://www.reddit.com/r/LocalLLaMA/comments/1ohq5bc/glm46_vs_minimaxm2/)
- Not even close in my use cases at least. Its still sonnet 4.5 / GPT5 codex > glm4.6 > everything else.
  - GLM4.6 is very comparable to sonnet 4 in real world use, I hope they later make a bigger model. If they made a deepseek / kimi sized model they could 100% slaughter the competition imo.

- So GLM 4.6 is better than Kimi K2?
  - For coding yes, for creative writing no.

- In this revision they reduced the number of parameters for M2 almost in half compared to M1. In my tests, using a non mainstream coding language, GLM 4.5 is better than M2. I have tried several times to get M2 to code a statistical function and it doesn't get it. GLM in the first shot nailed it

- Try it for your project. With 10B active for a size under 250B, I think knowledge is lacking and the expert won't be able to cover very edge cases. But, if they introduce something like GLM coding plan, it is properly worth to try as coding agent, not planner.

- People are always hyping whatever is the most recent. Seemingly every release crushes benchmarks, it's marketing and doesn't say much about model real world performance. Test the models in your use case and see if you like them.

- ## [🚀 New Model from the MiniMax team: MiniMax-M2, an impressive 230B-A10B LLM. : r/LocalLLaMA _202510](https://www.reddit.com/r/LocalLLaMA/comments/1oh5asg/new_model_from_the_minimax_team_minimaxm2_an/)
- Is it just me, or have the ratios of MoE models' active to total parameters grown very wane of late? Qwen3-Next is about 1:27 (80B-A3B), and this one is 1:23 (230B-A10B), which is a far cry from 235B-A22B, or 30B-A3B, let alone ye olde 8x7B (56B-A14B, a 1:4 ratio).
  - Yup, that's the direction. It's cheaper to train.
- Sparse MoE is also theoretically appealing as a research direction. The holy grail is a sparse MoE that can add new experts and tune routing online.

- ## [GLM-4.5-Flash on z.ai website. Is this their upcoming announcement? : r/LocalLLaMA _202508](https://www.reddit.com/r/LocalLLaMA/comments/1mmioub/glm45flash_on_zai_website_is_this_their_upcoming/)
- Flash is the API only free variant of their model, it's available since day one, and it's essentially a weaker version that's disturbed freely for people to test using the GLM API and capabilities, I've been using it for a while, its quite solid for being free

- Statement from Z. AI org staff members:
  - Flash is based on the Air model with inference optimizations, making the inference cost relatively low. It includes constraints on output tokens, with the main purpose of allowing community developers to experience the latest models for free.
  - it's just 106BA12B Air version but with different inference configuration to be cheaper, same weights basically.

- ## [GPT-OSS-120B vs GLM 4.5 Air... : r/LocalLLaMA _202508](https://www.reddit.com/r/LocalLLaMA/comments/1mifzqz/gptoss120b_vs_glm_45_air/)
- Same total parameter number, but OpenAI’s OSS 120b is half the size due to being offered natively in q4 precision and has 1/3 active prameters, so it’s performance is really impressive!
  - So, GPT-OSS-120b requires half the memory to host and generates token 3 times faster than GLM4.5-Air
  - I don’t know if there are any bugs in the inference of GPT-OSS-120B because it was released just today, but GLM4.5 Air is much better in coding and agentic workloads (tool calling). For the time it seems GPT-OSS-120B performs good only on benchmarks, I hope I am wrong

- Gpt-oss is native fp4 so its more like a 70GB model vs a 230GB model, and also about 10 times faster because the experts of gpt are tiny.
  - 10x faster is an exaggeration, maybe a bit over twice as fast though.

- Im currently running both models. They are about the same speed, lol, because GLM can run quantized at the same quality as GPT-OSS-120B unquantized, so speed is about the same, 80~90 tok/s on 3090s.

- ## [Granite-4.0-H-Tiny vs. OLMoE: Rapid AI improvements : r/LocalLLaMA _202510](https://www.reddit.com/r/LocalLLaMA/comments/1nwovv8/granite40htiny_vs_olmoe_rapid_ai_improvements/)
- Idk why everyone is so excited about this thing, it's pretty awful. Nemotron Nano is a much more exciting hybrid, for 1B extra params you get a model that actually works..

- Phi-mini-MoE has 7.6B total parameters and 2.4B activated parameters, that's 2, 4 times more active parameters than the new granite model(1B)

- ## IBM 其实十一也发了 Granite 4.0 系列大模型，不过没什么水花。给大家盘点一下：
- https://x.com/karminski3/status/1975509987360395552
  - granite-4.0-h-small-32B-A9B (MoE)
  - granite-4.0-h-tiny-7B-A1B (MoE)
  - granite-4.0-h-micro-3B (Dense)
  - granite-4.0-micro-3B (Dense)
  - 模型中的"h" 的意思是 hybrid (混合)，标志着模型采用了Mamba/Transformer 混合架构。
  - Mamba是一种状态空间模型（State Space Model, SSM），相比传统的 Transformer 架构在处理长文本时效率更高，能显著降低内存需求。 这种混合设计使得模型在保持高性能的同时，内存需求降低了70%以上，并能以更低的成本在更经济的 GPU 上运行。
  - reddit上有人测试 granite-4.0-h-small 可以输出1M大小上下文。但是！内容是不能用的，输出到100K左右就炸了，开始胡乱输出了

- small那款我测完就顺手删了，32B  A9B 还不如qwen3 30B A3B系列，而且看信息也看不出这是mamba还是mamba2

- 我看reddit上说这玩意废话少速度快，省token，拿来做总结挺好。

- [Granite 4.0 Language Models - a ibm-granite Collection : r/LocalLLaMA](https://www.reddit.com/r/LocalLLaMA/comments/1nw2wd6/granite_40_language_models_a_ibmgranite_collection/)
- Any plans on keeping the reasoning and non-reasoning models seperate or will future models be hybrids?
  - Near term: separate. Later this year we’ll release variants with explicit reasoning support. Worth noting that previous Granite models with reasoning include a “toggle” so you can turn on/off as needed.

- No context limit is crazy. Im so excited for advancements in hybrid mamba architecture
  - We’re big fans of Mamba in case you couldn’t tell! We’ve validated performance up to 128k but with hardware that can handle it, you should be able to go much further.

- ## [My key takeaways on Qwen3-Next's four pillar innovations, highlighting its Hybrid Attention design : r/LocalLLaMA _202510](https://www.reddit.com/r/LocalLLaMA/comments/1nwzs0k/my_key_takeaways_on_qwen3nexts_four_pillar/)
  - Hybrid Architecture: Combines Gated DeltaNet + Full Attention to context efficiency
  - Unltra Sparsity: 80B parameters, only 3B active per token
  - Stability Optimizations: Zero-Centered RMSNorm + normalized MoE router
  - Multi-Token Prediction: Higher acceptance rates in speculative decoding
  - Qwen3-Next, especially its Hybrid Attention design, might be one of the most significant efficiency breakthroughs in open-source LLMs this year
  - One thing to note is that the model tends toward verbose responses. You'll want to use structured prompting techniques or frameworks for output control.
  - It Outperforms Qwen3-32B with 10% training cost and 10x throughput for long contexts. 

- Don't get me wrong, I think it's really exciting that both Alibaba and IBM are experimenting with linear attention mechanisms (like Gated DeltaNet and Mamba2) at large scales in their open-weight releases.

- The hybrid attention is cool on paper but I've been running some tests and the memory overhead during the attention switching is actually pretty brutal if you're not careful with your batching strategy.
  - Been working with similar hybrid approaches at Anthromind and honestly the verbosity issue you mentioned is way worse than it sounds. It's not just about prompt engineering, the model genuinely struggles with knowing when to stop elaborating which becomes a real problem when you're trying to do any kind of structured output or API integration. The multi-token prediction sounds great but in practice you end up with these weird cascading errors where one bad prediction throws off the whole sequence. Still impressive work from the Qwen team but I'd def recommend extensive testing before any production deployment, especially if you're doing anything mission critical.

- ## [What’s your experience with Qwen3-Omni so far? : r/LocalLLaMA _202509](https://www.reddit.com/r/LocalLLaMA/comments/1nqg5q3/whats_your_experience_with_qwen3omni_so_far/)
- from a usage standpoint? It's really, really good. The output voices are not the greatest, but it's multimodal input understanding is top notch. It's the only openweights model that actually "understands" a video
  - Ovis2 and 2.5 are pretty good for videos too, sadly got never support in llama.cpp

- Why would you want to do anything multimodal in llamacpp? It doesn’t even handle multimodal context. 
  - llama.cpp supports mulitmodal models with `libmtmd` since Apr 10, 2025
  - You just use the text model as gguf and load the mmproj gguf containing the vision encoder
- Ya and libmtmd literally just dumps all your image tokens into the stream and has no idea what is what. Maybe for some workflows but nothing complex or multi step.
  - That is true for basically all common inference engines like vllm though. It encodes the images to tokens and has those in context, sure thats not 100% safe in long chats, but for that you need high-level multimodal orchestration. As far as I understand most inference engines work that way, Encode the image to tokens and then insert them into the model context so even multi step works, but like with everything else it degrades over time.

- Yeah the inference is catastrophic. Even if you manage to use vllm on unquant variant (>60GB VRAM), you can't use the streaming input audio feature, you have to write that code yourself. (transformers on unquant is stupidly slow, CPU bound). The model looks very good, and pretty cool, but "batteries not included" would be an understatement.

- ## 🤔 [I think I'm falling in love with how good mistral is as an AI.  : r/LocalLLaMA _202511](https://www.reddit.com/r/LocalLLaMA/comments/1oyaz1h/i_think_im_falling_in_love_with_how_good_mistral/)
  - It follows instructions very well
  - doesn't hallucinate (almost zero)
  - gives short answers for short questions and long answers for properly long questions
  - is tiny compared to SOTA while also feeling like I'm talking to something actually intelligent rather than busted up keyword prediction
  - But the benchmarks of it don't show it as impressive as phi4 or phi3 even, Qwen3, Qwen2 vl etc also. Putting it insanely lower than them. Like this is insane how awful the current benchmarks are. Completely skewed.

- How do you benchmark on writing style?
  - [EQ-Bench 3 Leaderboard](https://eqbench.com/)
  - you need to select "creative writing" and "longform writing" on the top. The would be judging the style.

- Mistral Large 123B was great for its time, and it’s a real shame they haven’t published an open-weights successor, especially with all the recent advances in MoE models in the ~100B size class.

- Mistral-24b-3.1 (I believe it's the 2503 release) is one of the best and most reliable local models I use on a daily basis. The other is Magistral-24b-2509 (based on Mistral 3.2).
  - The reason for this is that Mistral models are not as overfitted as most others.
  - When I write with Mistral-Small, I really feel that this is a damn smart model that is also most aware of its own limitations. I see less tricks and bechmaxxing with Mistral and more "real" intelligence.
  - A real example from a few days ago: I asked < 70b models about the meaning of a certain abbreviation. I tested about 10 models, and all of them simply invented a definition of the term (with overwhelming confidence), except for Mistral, which told me that it was unsure about the term and needed more context.
- We are using mistral small 3.1 2503 in production too it's great even in agentic mode. My only problem is the repetition sometimes. Have you figured a way to solve this?
  - Use Mistral Small 3.2 or even Cydonia.

- Magistral-Small-2509 gang represent. Fantastic little model. If you've got 25GB of VRAM to run it in Q8, it's really impressive for conversational English. I'm building a little toy Swift app with it as the central "talk to me to do stuff" orchestrator of other models that specialize in code, summarization, safety evaluation, privacy evaluation, etc. Magistral-Small-2509 seems to "get" me better than other models. Wish I could figure out exactly what that means LOL

- I got the best results when I switched from the Magistral 3.2 Q4_k_m to Magistral 3.2 Q6_K. It changed everything - it is way better in understanding long stories drafts and could generate text almost without skipping or distorting. It makes mistakes sometimes, though. But much less so than previous versions. P. S.: And new versions seems more uncensured, then older.
  - Your experience mirrors mine. I find Magistral-Small-2509 at Q8 to be indistinguishable from FP16 on my Mac for conversational English. It just runs twice as fast. But every quant below that? The loss of precision is palpable and the quality goes way down quickly.

- Have you tried the UGI-Leaderboard? 
  - Mistral models tend to better than qwen models at things like overall intelligence and writing ability. 
  - Qwen models tend to be focused on standard textbook info like math, wiki info, and logic, while lacking in non-academic knowledge.
  - Older models like Kunoichi-7B and Fimbulvetr-11B-v2 score particularly well compared to newer models in the Writing section's Originality ranking.

- It is no where close to Qwen 3 for my use case (RAG chatbot), but the more options the merrier

- My top local conversational models on my Mac are Magistral-Small-2509 -- even Q8 is really quite good, 
  - Magistral fails tool calls infrequently, and with just a fetch/search MCP and the ability to read the Web it is competitive... IMHO it's a better conversational partner than Grok 4 Fast, more insightful than GPT5.1 in voice mode 
  - It lacks quite a bit of world knowledge, but searching & fetching seems to make up for that a lot.

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
  - The model is incredible. It doesn't overthink and waste tokens unnecessarily in the reasoning chain.
  - The responses are focused, concise and to the point. No fluff, just tells you what you need to know.
  - The censorship is VERY minimal. My wife has been asking it medical-adjacent questions and it always gives you a solid answer.

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

- at lower temp it’s more likely to get stuck in loops

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

- ## [The phi family model: Acing tests but failing real use cases? : r/LocalLLaMA _202501](https://www.reddit.com/r/LocalLLaMA/comments/1hwsuuf/the_phi_family_model_acing_tests_but_failing_real/)
- The Phi family is going to be awful for 90%+ of Local Llama user’s use cases - it wasn’t tuned for multi-turn interactions (chats), it is too small to have an encyclopedic knowledge of things, and it doesn’t take well to fine tuning for chat, role play, or other home use cases.
  - It is very good for its size at single turn reasoning with provided context. We usually use it as a single step in larger, multi-model workflows.
  - While its primary purpose is as a research model for Microsoft to explore the limitations of synthetic data model creation, I believe the future of Phi is as a model used by larger reasoning models during their tree search for specific tasks.

- ## [Why is Phi4 considered the best model for structured information extraction? : r/LocalLLaMA _202510](https://www.reddit.com/r/LocalLLaMA/comments/1oejb8p/why_is_phi4_considered_the_best_model_for/)
  - curious, i have read multiple times in this sub that, if you want your output to fit to a structure like json, go. with Phi4, wondering why this is the case

- Phi is great it's arguably the best local AI. But it was trained on only university notebooks (smart people's notes) so you don't get exactly the same level of prompt understanding off the bat.
  - For phi you wanna treat it like it's in an exam, talk about hunceforths and explain what will make it 'lose marks' etc

- It trained in structured formats and Microsoft has lots of formats. It’s not ocnsidtent but it consistent enough to treat certain types of things as objects.

- In my testing nothing of its size comes close. Qwen3-32B (with thinking) is probably the smallest model that gets that good at structured outputs.

- ## [Phi-4 has been released : r/LocalLLaMA _202501](https://www.reddit.com/r/LocalLLaMA/comments/1hwmy39/phi4_has_been_released/)
- this model is very smart when it comes to logical tasks, and instruction following. But do not use this for creative tasks and factual(事实的：真实的) tasks, it's awful at those.

- Still 16k, was hoping for a 128k version. 

- why "SimpleQA" score is dropped to 3.0 from 7.5 of phi 3?!
  - They explain this in the paper. 
  - Phi-4 post-training includes data to reduce hallucinations, which results in the model electing to not "guess" more often. Here's a relevant figure from the technical report. You can see that the base model skips questions very rarely, while the post-trained model has learned to skip most questions it would get incorrect. This comes at the expense of not attempting some questions where the answer would have been correct, leading to that drop in the score.
- Apparently, lowering hallucinations lowers ability to answer questions it actually knows the answer for. Tradeoff.
- They fine-tuned it to refuse answering questions it doesn't know the answer to, thereby reducing its score quite drastically.

- Previous iterations of Phi were okay, but never good enough to be one of my go-to models, but I think Phi-4 breaks away in this regard.
  - It underperforms Qwen2.5-14B-Instruct for some skills, but outperforms it in others. In particular, Qwen2.5 has very poor self-critique skills, but Phi-4 performs self-critique beautifully. I've been using Big-Tiger-Gemma-27B for self-critique, but Phi-4 will do about as good a job of it, much faster, and with twice as much context (16K vs 8K), so I'm thinking Phi-4 will be my go-to for self-critique.
- Oh yeah, qwen is impossible to argue with. It would keep saying that data is from like sources 

- ## [Phi4 vs qwen3 : r/LocalLLaMA _202505](https://www.reddit.com/r/LocalLLaMA/comments/1kcxmrw/phi4_vs_qwen3/)
- I would say Qwen 3. They have explicitly stated that Phi 4 reasoning was only trained on math reasoning, not any other reasoning dataset, so for anything but math, Qwen 3 is your better go to! If it's math, though, Phi4 kills it.

- ## [Qwen3-14B vs Phi-4-reasoning-plus : r/LocalLLM _202505](https://www.reddit.com/r/LocalLLM/comments/1kbzsdo/qwen314b_vs_phi4reasoningplus/)
- It will depend strongly on your use case. So test and check.

- I didn't try Phi 4 reasoning yet, but I was comparing Phi 4 vs Gemma 3 in translation project, Gemma 3 gave me better result but Phi 4 gets less hallucination.

- To me phi4 plus thinks too long. Personally, I slightly prefer qwen

- ## 🆚 [Qwen3 14b vs the new Phi 4 Reasoning model : r/LocalLLaMA _202505](https://www.reddit.com/r/LocalLLaMA/comments/1kg5m5a/qwen3_14b_vs_the_new_phi_4_reasoning_model/)
- Qwen3 14B is smarter and can punch higher.
  - Phi4-Reasoning will follow the craziest instructions perfectly. It is near perfect at following instructions/formatting.
  - Phi4 will hopefully make fewer assumptions when explicitly instructed in its system prompt to quote only the provided information. This should make it more accurate for retrieving information instead of inserting its own ideas.

- Qwen3 14B feels more versatile overall—great reasoning + decent creativity. 
  - Phi-4 is scary good at precision tasks though, especially when formatting or strict following is needed. Depends on the use case

- I found Phi-4-reasoning to be a bit smarter (but not code), but requires almost 3x more tokens than Qwen3-14B to be so.
  - In terms of real usability, Qwen3-14B will be the better choice for the vast majority of people.
  - In terms of vibe, Phi felt like a dry brute force benchmaxxer.

- Phi4 uses a significant amount more tokens while the output is of less quality than Qwen3.
  - Qwen3 is the first local model that I can comfortabel use on my own hardware that gives me major GPT4 vibes, despite the weights being significantly lower.

- phi-4 spend more token than qwen3, so i prefer qwen3

- We evaluated Phi-4-reasoning vs Qwen3-32B in our internal application (unstructured sales data analyze). 
  - Phi-4-reasoning was a bit better: 14% failures vs qwen 17%. But Phi was 10 times slower. All testing was performed on OpenRouter.
  - Currently we are using QwQ which also have 14% percent failures and give reasonable performance. About 3 times slower compared to Qwen3.
  - Commerical Grok-3-beta and Gemini-2.5-pro have 12% failures, but much higher cost compared to QwQ.
  - P. S. qwen3-30b-a3b and qwen3-235b-a22b both gave above 20% of failures, which was a bit surprising.
  - google/gemma-3-27b-it: 11% failures and crazy fast.
  - meta-llama/llama-4-scout: 14% failures. (maverick didn't work, gave too long output)
  - Update: That's more complex. The test gave answer "should we buy" in boolean and while gemma gave "correct" results, the internal calculations were absurdly wrong. So, gemma high results is coincidence/luck and bad testing set.

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
- I've tested Phi-4-25B, cant say that it really a lot better, maybe about 10% at some specific cases.
  - In my evaluation it really depended on the kind of task performed. For many tasks Phi-4 and Phi-4-25B performed identically, but Phi-4-25B performed significantly better for code gen, science, summarization, politics, psychology, self-critique, evol-instruct, and editing tasks. Neither model performs well at multi-turn chat, and their creative writing competence is okay but not great.

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
# discuss-model-api-gateway
- ## 

- ## 

- ## 

- ## [Too many LLM API keys to manage!!?! : r/LLMDevs _202502](https://www.reddit.com/r/LLMDevs/comments/1irpjjk/too_many_llm_api_keys_to_manage/)
- Check openrouter.ai
  - It’s expensive but has some really nice features like providing costs in each response. (Why actual providers don’t do that mystifies me.)

- LiteLLM does require API key from the providers

- Check out stashbase.dev, it will help you manage all your API Keys as well as other secrets.

- ## 🤔 [Why You Need an LLM Request Gateway in Production : r/LLMDevs _202504](https://www.reddit.com/r/LLMDevs/comments/1jp6ot7/why_you_need_an_llm_request_gateway_in_production/)
- I only adopt abstractions when they prove genuinely useful. Among all the possible abstractions in the LLM ecosystem, a proxy server is likely one of the first you should consider when building production applications.
- This is where a proxy server comes in. It provides one unified interface that all your applications can use, typically mimicking the OpenAI chat completion endpoint since it's become something of a standard.
  - Your applications connect to this single API with one consistent API key. All requests flow through the proxy, which then routes them to the appropriate LLM provider behind the scenes. 
  - The proxy handles all the provider-specific details: authentication, retries, formatting, and other logic.
- Four Reasons You Need an LLM Proxy Server in Production
  - Using the best available models with minimal code changes
  - Building resilient applications with fallback routing
  - Optimizing costs through token optimization and semantic caching
  - Simplifying authentication and key management

- ## 🤼 [why are llm gateways becoming important : r/LLMDevs](https://www.reddit.com/r/LLMDevs/comments/1notvwd/why_are_llm_gateways_becoming_important/)
  - 网管层 vs 应用层
- the idea (from what i understand) is that prompts + agent requests are becoming as critical as normal http traffic, so they need similar infra:
  - routing / load balancing → spread traffic across providers + fallback when one breaks
  - semantic caching → cache responses by meaning, not just exact string match, to cut latency + cost
  - observability → track token usage, latency, drift, and errors with proper traces
  - guardrails / governance → prevent jailbreaks, manage budgets, set org-level access policies
  - unified api → talk to openai, anthropic, mistral, meta, hf etc. through one interface
  - protocol support → things like claude’s multi-context protocol (mcp) for more complex agent workflows
  - what are people here using for this gateway layer these days are you rolling your own or plugging into projects like litellm / bifrost / others curious what setups have worked best

- llm gateways are critical once you need reliability and observability across multiple providers. bifrost handles routing, semantic caching, and governance in one openai-compatible api. you get health-based failover, embedding-keyed cache, and org-level policies with zero-config startup. for production teams, this means consistent uptime, traceable requests, and budget control.
  - For a brief comparison with LiteLLM: Bifrost delivers 100 percent success at 500 rps; litellm drops below 90 percent. bifrost median latency is 804 ms, litellm is 38 seconds at scale. bifrost throughput is 424 rps, litellm is 44 rps. bifrost uses 120 mb memory, litellm uses 372 mb

- honestly I’m on the other side of the equation so i have adapters that enforce defensive strategies to deal with llm responses and tools and things. But you can see right in your diagram why the other half finds value to add in the gateway. It’s written in your diagram

- We looked at using a router but it was a single point of failure.
  - We are a node shop and we went with the Vercel AI SDK. Built some custom fallbacks, simple retries, and it's built in telemetry. I haven't been yearning for an LLM router since.

- ## [What’s the Fastest and Most Reliable LLM Gateway Right Now? : r/LLMDevs _202508](https://www.reddit.com/r/LLMDevs/comments/1mh962r/whats_the_fastest_and_most_reliable_llm_gateway/)
- I’ve been testing out different LLM gateways for agent infra and wanted to share some notes. Most of the hosted ones are fine for basic key management or retries, but they fall short once you care about latency, throughput, or chaining providers together cleanly.
  - Bifrost (Go, self-hosted): Surprisingly fast even under high load. Saw around 11µs overhead at 5K RPS and significantly lower memory usage compared to LiteLLM. Has native support for many providers and includes fallback, logging, Prometheus monitoring, and a visual web UI. You can integrate it without touching any SDKs, just change the base URL.
  - Portkey: Decent for user-facing apps. It focuses more on retries and usage limits. Not very flexible when you need complex workflows or full visibility. Latency becomes inconsistent after a few hundred RPS.
  - Kong and Gloo: These are general-purpose API gateways. You can bend them to work for LLM routing, but it takes a lot of setup and doesn’t feel natural. Not LLM-aware.
  - Cloudflare’s AI Gateway: Pretty good for lightweight routing if you're already using Cloudflare. But it’s a black box, not much visibility or customization.
  - Aisera’s Gateway: Geared toward enterprise support use cases. More of a vertical solution. Didn’t feel suitable for general-purpose LLM infra.
  - LiteLLM: Super easy to get started and works well at small scale. But once we pushed load, it had around 50ms overhead and high memory usage. No built-in monitoring. It became hard to manage during bursts or when chaining calls.

- i think if you're self-hosting on kubernetes, the kgateway + agentgateway combo crushes the rest of the competition, by a pretty large margin. (it's not just a LLM gateway, they're pioneers of the kubernetes gateway api, which is the agreed upon standard for kubernetes)
  - I think the only thing they lose to other AI gateway implementations at, is the variety of use cases that are currently supported. For example, a gateway like LiteLLM will have a broad range of supported endpoints (that aren't built well, but exist).

- [Best LLM gateway? : r/LocalLLaMA](https://www.reddit.com/r/LocalLLaMA/comments/1mh9r0z/best_llm_gateway/)
- Litellm is easy to setup but difficult to scale when you are building for production. I have seen litellm fail around 250-300 RPS. It is also quite resource hungry leading to unnecessary infra complexity.
# discuss-model-api-free
- resources
  - https://github.com/cheahjs/free-llm-api-resources
    - free access or credits towards API-based LLM usage.

- ## 

- ## 

- ## 

- ## 

- ## [佬们，像这种缝合怪的AI应用聚合站，是不是有统一的源码啊，我已经看到好几个了 _202405](https://linux.do/t/topic/98476)
- GoAmzAI, SparkAI, 奈斯猫 AI 你试试看这几个，以前见过的就这几个

- GoAmzAI 授权 2400 定制5000+

- 这都是各种闭源二开，有的卖源码，有的只卖授权，开源很少

- ## [【首发】全新高颜值的VoAPI正式发布，免授权，基于NewAPI开发，完全兼容支持 _202409](https://linux.do/t/topic/218357)
  - 断断续续花了几天时间开发的， 基于 one-api 与 new-api 开发的更好看和轻便的 AI 模型接口管理与分发系统，免授权使用。
  - 增加登录 / 对话 / 绘画 IP 记录
  - 注：本系统为闭源程序，免授权，若有介意请勿使用。

- ## [各位佬，你认为最好看的newapi二开版本是哪个？ _202508](https://linux.do/t/topic/889486)
- Veleora

- 除了特别偏的 api 源，大部分都支持 OPenAI 格式，所以对我而言，与其要求它有一堆我用不到的功能，不如要求它好看一点

- onehub 我个人觉得最简单好看

- ## [【T佬】公益站被非法倒卖，我有风险吗 _202511](https://linux.do/t/topic/1150763)
  - 我公益站资源被咸鱼上倒卖 1w，本身公益站提供 openai 服务就不合规，我有风险吗？
  - 无论事件真实性如何，受伤的都是我啊。关站已经成定局。不管真假，先关站规避风险。

- 个人觉得没事，因为你个人没有盈利。

- 先出公告，撇清责任，让买了的去退款。 还要标明你马上关服了，钱不是你收的。 先免责再说，谁收的钱找谁去。 不然交了钱的误会你是参与方就惨了, 1W 数额说大不大 说小不小, 够得上那啥了

- 自己买几个，然后去后台看是哪个渠道？顺藤摸瓜，摸到了就举报他，摸不到就封自己号，要求退款！

- 百度开发的一款 AI 法律工具 ，依据恐怕是有的 [法行宝-您的免费AI律师](https://ailegal.baidu.com/)

- ## 💰 [有没有大佬搞一个靠广告盈利的免费大模型api站 _202510](https://linux.do/t/topic/1045546)
- 广告费远不够覆盖 ai 成本的。既砸了公益口碑，还要自己往里面垫钱，何苦来哉

- 参考腾讯元宝现状

- API 站不是用户界面啊。 文本里自动插入广告会导致大量场景无法使用。
- 可以是每天隔几个小时去站点页面上看广告获取额度，但不能是在客户端输出广告。

- 把签到改成看广告了是吧。

- 我们做过这种站点，目前已经关停了，我个人认为这个模式不健康， 或者广告人需要摸索出一个新的良好模式。
  - fmvp 大佬建议的这种模式和 x 果短剧等流媒体平台类似，大家一定知道，这种注意力剥夺式的广告，并不适合 ai-api 调用，因为开发者需要保持很强的专注度，如果一个开发者在一个 case 中，刷了 3 个广告之后，思想一定无法腾空。
  - ai-api 站点如果间接瞄准用户怎么样？ 也就是开发者需要按照 api 站点给出的接口示例，将自己的产品打造成多次请求中，固定向用户展示一次广告的方式。 这样开发者成本降低、用户为 api 供应商直接献力。—— 这个玩法就太新颖了，首先很多供应商不懂广告，广告的模式也很粗暴，开发者不仅需要向供应商妥协，还破坏了用户的使用体验，这样的产品就难生存了。这一点我们以后可能会看到有人破局。
  - ai-api 广告的植入方式，有个新玩意，那就是根据 prompt-keywords 的关联度，触发一些预设语，让本次输出结果除了 “顺利交差”，还 “夹带私货”。 AI 搜索引擎产品，在结果中根据广告主投放，修改权重，就是很典型的例子。这个相对优雅，但是也差强人意 —— 这样的产品竞争力不行，用户信任度低（为什么纳米搜索狗都不用）
  - 以上是几个简单的分析，有很强的主观色彩，但有很多现货的案例可以佐证，后期可以细聊。我们运营改旗更张，现阶段也在调研公益站点的生存之道 —— 调研 —— 你需要什么样的公益站

- 结尾插广告不影响使用，广告就没效果，自然不会有广告商投钱；影响使用可能就转向别的了

- 我作为程序员，不太能接受广告的形式，在上班中弹个广告出来
  - 宁愿付费，公司还能申请报销

- ## [各位佬的公益站点是不是都不支持上传文件 _202509](https://linux.do/t/topic/971390)
  - 我摸索了几天 添加了好几个佬的公益站 发现都不支持上传文件
- 我知道的只有官方 Gemini 和 OpenAI 的 Responses API 支持传文件呀, 而且大部分公益站用的还是 2api

- 模型原生支持文件的不多，换个支持文件处理的软件解决更快

- 很多 2api 都没处理图片 

- ## [目前哪个公益站claude code体验比较好呢？ - 开发调优 - LINUX DO _202511](https://linux.do/t/topic/1114843)
- 付费站体验都没几个好的

- 收费的都崩，公益现在也难，别勉强了。 搞个 GLM 4-6 勉强蹬一蹬吧。 我用魔搭的 KEY，小蹬也算够用。

- gemini pro 只能用 5 次。 超额就变成了 gemini flash 。

- ## 🤔 [如何最大化利用社区key（自动故障转移切换） - 开发调优 - LINUX DO _202510](https://linux.do/t/topic/1098166)
  - 现在各家 ClaudeCode 中转都难保障 24 小时稳定性，自动切换显得灰常重要

- Claude Code Hub 虽然目前还不支持 auth token, 但是负载均衡和故障重试这一块儿绝对是杠杠的

- claude-relay-service: CRS暂不支持自动切换重试

- 感觉无论key还是token都可以全塞http请求头里，让中转商服务端自行忽略处理
  - 那样就不符合请求透传的原则了, CCH 的原则是除必要头部外不对请求做任何处理

- [怎么看每个公益站的RPM呢  _202510](https://linux.do/t/topic/1108753)
  - 公益别逮着一个薅，开轮询负载均衡一下
  - 我也想问一下关于轮询的问题，很多公益站的模型命名都不同，应该如何导航到同一个id，我尝试在veloera里手动把渠道模型id改为同样的id，但是当我调用的时候，当一个渠道的模型无法使用，也不会给我自动轮询到下一个渠道

- ## [CC封号太严重了，上车就翻车，平替用CC+GLM还是CodeX ？友友们有经验吗 - 开发调优 - LINUX DO _202510](https://linux.do/t/topic/1092260/10)
- glm用着用着，会有问题解决不了的。还是需要一个能力更强的AI

- 有几个渠道
  - 1. 最省钱的 直接咸鱼买 尼日利亚 app store充值卡, 差不多89 RMB = 15000 货币, 刚好14990 可以订阅claude
  - 2. Google play 绑定国内visa 卡 , 应该也可以直接订阅claude
  - 3. 虚拟卡, bybit之类的就可以随便订阅了吧
  - 我现在是方案1 , 什么时候这个不好使了我就用虚拟卡订阅, 梯子是要的, 但是这个网站里面不是到出都分享免费的梯子吗

- GLM4.6现在都敢和GPT-5并肩了？这几乎没什么可选的吧，CODEX CLI，除了慢点起码在做事, GLM4.6超卖严重，你愿意和其他人一起抢卡和抽奖可以试试。

- ## [目前有哪些公益站支持codex？ - 开发调优 - LINUX DO _202510](https://linux.do/t/topic/1095599)
  - 国庆节之后用了一段时间codex，感觉不错，期间也用了一些公益站的。不过自从openai减量之后好像都用不了了。使用team也会报账号关联的问题。
- No available OpenAI accounts support实际上是由CRS导致的BUG，原先只需管理员在后台手动重置状态即可，同时她适配的也有问题，我是使用OAI-KEY的形式接入，居然也会被限流拦截，然后不走企业微信推送

- 大多数公益站的gpt-5只能聊天，不能工具调用。偶尔有公益站用的是官逆的gpt-5，属于站长用爱发电了。 

- [公益站codex要怎么配置呀 - 开发调优 / 开发调优, Lv1 - LINUX DO](https://linux.do/t/topic/1017195)
  - 公益站里有一些余额，想使用codex。但是不知道怎么使用。下面的办法都不行，是不是有些压根就不支持？这个配了也用不了，大佬知道怎么弄吗？比如23公益和 xmdbd
- 有些公益站不支持Codex的，支持的在文档或者公告里都会说明

- [第一種： 用上env_key，需export api key as environment variable]
  - [第二種：用http_headers，需在 auth.json加上api key，但不用export env var]
- 我用的佬的23公益站，方法二调用成功了，感谢佬提供的方法

- 不知道你是怎么调用的，如果是调用作为mcp的话，那就偶尔才能成功。因为这个只有基本的chat功能，你可以找一些支持fc功能的站点

- ## [一个 Claude Code 公益站，支持 GLM, DS 3.1, Qwen 3, K2 等 - 资源荟萃 - LINUX DO](https://linux.do/t/topic/895380/1)
- 虽然我创建了 Veloera。但用 new api 而不是 veloera 原因很简单，veloera 还没有 cc 支持  

- ## [B4U公益站的Claude是只能对话吗 - 开发调优 - LINUX DO _202510](https://linux.do/t/topic/1066446)
- 算是b4u的技术问题，没有部署用原生工具调用的版本，所以效果不太稳定

- 也不支持图片呢
- 接 roocode 用挺好的。 cc 是不行。

- ## [【B4U公益站】是克劳德，我们有救了！（每周六限时开放注册） ](https://linux.do/t/topic/801848)
  - 渠道技术： Claude-SessionKey号池→claude2api→FC使能
  - 模型特点：支持工具调用、上下文 128K+、支持 RooCode，不推荐接入 ClaudeCode

- 大转盘是彩蛋，在投喂站里，投喂站从主贴进去就好了

- [B4U公益站接入Claude Code尝试(CCR接入) - 开发调优 / 开发调优, Lv1 - LINUX DO _202509](https://linux.do/t/topic/921779)
  - 在站内查看相关的帖子，站长也开了接cc的研究贴，效果不太满意
  - 当前缺点上下文太小，导致经常触发上下文压缩，损失项目信息，回应也更慢。上下文小可能是其他原因，还得研究研究。更新：最新尝试64K上下文也行，mcp调用没啥问题，但文件编辑错误次数有点多

- 上下文好像是最近A社限制了免费对话上下文的原因，以前如果开启网络搜索是可以128k，现在都是20k了似乎

- b4u之前就提供了实验性claude code，用这个不需要用ccr

- 直接配置用CC的话，前几次试过，体验不好，错误率太高了。各种报错

- 之前用这个公益 ＋ cc 的时候经常不能调用工具，体感不是很好

- B4U用的应该是Toolify，原先对Claude Code的tools支持确实有限。这几天Toolify做了几次比较重要的更新，包括工具调用的格式强调、tool_call消息的处理等等，现在工具调用的体验应该会好很多

- 1，上下文绝大部分时间仍是128K+（每天有半个小时会降至10K）
  - 2，newapi:v08660之后，就已经支持直接cc以及其他代理工具，基础功能、文件读写编辑都可以通过测试，稳定性、速度、智商我都不满意，所以不推荐接入cc
  - 3，一直用的是杯佬的toolify旧版本，新版0827经测试b4u的适配性、稳定性不如旧版

- kilo使用b4u，发现大概120k附近就会开始报错了。

- ## [请问公益站就是有老板免费提供API意思吗？  _202510](https://linux.do/t/topic/1036007)
- 有一部分是
  - 用限时免费的渠道，转到公益站
  - 批量注册薅的免费新人福利羊毛，转到公益站
  - 批量 2api 转的
  - 低成本薅注册羊毛，转到公益站，比如批量虚拟卡开号，或者用接码平台批量注册硅基获取邀请余额之类的

- 公益站稳定性非常一般。经常回答问题一半就挂掉了。做项目的话老老实实买吧。
  - 我只知道我后台的 GLM-4.6 和 Gemini-2.5-Pro 的报错率不到 2%，绝大部分报错都是传了敏感内容

- ## [公益站的api来源是什么 ](https://linux.do/t/topic/1099545)
  - 2API和投喂为主
- Gemini-2.5Pro和绘图系列为GeminiCli逆向，可以自行部署使用较为稳定的，不做项目推荐，因为在用系统系Claude魔改版本
  - Gemini-2.5-flash有个轮询分组，来源于其名称一模一样
  - GLM系类为官转，转接与官方渠道
  - GPT系类为官转，其中5-Codex来源于逆向Codex，5来源于微软AZ
  - KAT来源于快手官方平台转接
- OpenRouter、OaiPro 这种是正价官转（不过这俩不是公益），是纯官方 API
  - 其他公益站就是明确告诉你主要渠道就是 2api，公益站一般是免费站 2api，付费站则主要是 Pro/Max 2api，当然还有 GLM ￥0.01 亿万 Tokens 这种不是 2api 的随机羊毛。偶尔也有大善人 Azure、AWS 等赠金快过期了捐给公益站这种也是纯官转 API。

- [观23公益 翰林文苑有感 麻烦佬友们进来指点一二 ](https://linux.do/t/topic/1115602)
- 大部分都是平台薅羊毛或者 2api，但是都不稳定，很麻烦，没点信息渠道或者手段很难维持的，我的已经停摆了。2api 就不说了，站内一大堆，平台薅羊毛一般都是批量注册号来白嫖免费 api，再放到中转站轮询调用，我知道的有 iflow, 硅基，七牛云之类的，不过薅多了平台风控就严重了，后两个已经限制的很严重了。然后有手段的话海外的某些平台应该也能薅。你要搞的话可以试试薅快手国际版的，站内好像没见人薅，国际版的注册一个号给两千万 tokens，单邮箱就能注册，写个程序批量注册应该不难，不过只有 90 天有效期。
  - 总之我觉得搞这玩意信息差很重要呢，有些东西发站里会被蝗虫般薅秃，或者门槛高，违 f，所以比较少人分享

1. 首先你要有渠道，没有别往下看了
2. 你要有闲置资金，时间。至少要有自己的服务器吧，没有就得各种薅，折腾。
3. 有渠道，有时间，有资金。那就开始造。
4. 可以接入，newapi/one-hub/done-hub。记得在 Linuxdo connect 中申请应用接入，配置好 L 站登入。差不多就完事了。
5. 奔着公益去开公益，不是很推荐。我们都是奔着折腾，玩弄的。就比如我的，智谱年包 lite 230 / 年，netcup 服务器 55 / 月，各种七七八八还得 100 / 月。就这都还有人贴脸说各种不行。不过我很少回应。不行别用

- ## 🤔 [深入浅出，解密 L 站内中转站的秘密 - 搞七捻三 / 搞七捻三, Lv1 - LINUX DO _202509](https://linux.do/t/topic/981851)
- 目前据我所知的中转站分为两类：
  - 1 是通过类似 new api 进行转发的
  - 2 是直接提供官方账号的 sk 的

- 通过类似 new api 进行转发的，本质上连接到 claude 或者 openai，都是同一出口，中间过了中转站站长的号池，这里会出现一个差别 ** 缓存命中 **，也就是说如果同一个人，短期内都用一个模型，模型会更加容易记住自己要做什么，效率更高，费用更低
  - 改成多队列，按人分列, 提高了缓存的命中率，从而降低成本
- claude的plus和max套餐，区别在于使用的tokens，那站长们除了提高缓存命中，减少tokens消耗之外，当然就要给你的账户限制额度啦，假设一个claude max一天可以瞪1000美刀，那么一般的站长就会超发，会拆成每个人100美刀，卖15个人左右，因此你会看到中转站大多数都是按月套餐，每日限额
- 优势：轻度使用时，费用低，使用简单【不需要管节点和号池】
- 劣势：重度使用时，费用高，非同key比同key效果差【本人用中转站codex和gpt-team codex对比结果】

- 接提供官方账号的 sk 的
  - 除了缓存优势外，就是不限额，这个key只有自己在用
  - 优势：重度使用时，费用低，缓存命中高，效率高，效果好，稳定性高
  - 劣势：需要自备干净节点，具备一定的基础

- 少了一种：二开插件或者包装插件的，这种就是黑盒了。

- 公益站就多了，还是得分类
  - 如果只对编程来说，几乎比较少公益站能稳定运行，因为编程的封号概率极低，他们这些号主要来源于，别人想要激发退款流，而抛出来的账号，例如max用户，订阅是1个月，大概使用20天之后，就会抛出他们的账号，让大家刷，便于退款，公益站多数收集这些账号，途径包含L站或者隔壁站点之类的，甚至飞机上会有相对于的群聊
  - codex的途径相对简单，目前都是来自1刀team的比较多
  - 其余就是富可敌国的中转站们放出来的公益，比较没人用就是沉没成本，还不如趁机推广
  - 有以前一些AI中转站推广的时候送的余额+注册机堆积起来的，像火山，openrouter，硅基之类的，也有gpc300剩余的余额用于公益站的，渠道较多，稳定性也较高，打野的除外

- 目前的codex来源大多数是用野卡1美金开了一个月team，相当于成本很低，所以大家都拿来做公益
- 其实都是辛苦费，因为你不知道什么时候，号就掉了，掉了又要担心会不会黑卡，会不会风控，如果是境外卡，风控被冻结了，人是要去国外解冻的

- 野卡连卡都是野的，没有人在乎这个的，而且1刀team的途径很多，还有通过google pay去开通，另外openai没有claude监管严格了，应该知道自己热度不行了，封号的越来越少
- 国外一堆野鸡银行的信用卡，野卡目前也只能用来开1刀team，卡未必就真的是你的实名，月末你不还款，卡就被冻结了，但是野鸡银行申请卡非常简单，一般一次能申请20-30张

- 2API只能被拿去镜像站和酒馆，因为2API的没有function call，调用不了工具
- 不能调 function call的 还有一种，就是逆向的，说白了中转的背后和你在网页版聊天一样，这样就没有按tokens计费，这种在一些特定情况下就会不太好用

- 可以看看亚马逊对这个缓存的介绍，不是简单的问题，他默认的周期是5分钟， 系统会自动检测重复的代码模式、上下文和请求，同人同key命中率能达到90%。

- ## 看到一个同行退了，所以还是 A 厂“胜利”了
- https://x.com/tuzi_ai/status/1982641845575589987
- 这行当是时间窗口期生意, 无限开卡白嫖撬信息差杠杆, 1美金开个codex团队账号, 上百人民币往国内卖, 持续补号, 直到对手开始补漏, 生意就会进入消退期
  - 但这种信息差用不了多久就会出现一次, 跑通了渠道后就可以一直换品了
  - 最不济最后就是转成正规军呗

- ## [感觉大厂 2api 才是长期公益站的最好方案  _202508](https://linux.do/t/topic/919087)
  - 2api御三家 grok，qwen，z.ai
  - 都有共同点：注册简单，token 刷新简单/长期有效，高并发，稳定，0成本…
  - 反观其它大部分api羊毛的共同点：很难长期，渠道一公开就活不久，上某三字脚本大概率封号…
  - 不过2api缺点也明显，只能聊天，很难用于科研/代码领域

- 只是占有率还不高的吧, 占有率高了可能就去反2api了
  - 2api本来就不是很稳定的 而且还不支持很多功能

- 最好的方案当然是aws, 官转啦

- 2大厂的也有可能被封号，而且随便改点参数上点验证2就失效了

- grok4和qwen一堆新模型上线，都没改过已有模型的参数 老项目直接用
  - 有验证的只有grok一家，貌似只有亚洲ip才会触发

- 我跟佬友们保持长期良好关系，是我最好的方案

- ## 🤔 [各位运营公益站的佬，想请教公益站的key一般怎么来及封号策略 - 开发调优 - LINUX DO](https://linux.do/t/topic/838799)
- 免费轮询较多，或者2api（哪来的这么多富哥）

- 站内的稳定公益站都做的很有原则，没遇到随意封号，现在慢慢的只用稳定站了。本来是想均匀用，各站都用一点，不逮着一家薅羊毛 

- ## [关于站内各种公益站的一点困惑 - 资源荟萃 - LINUX DO](https://linux.do/t/topic/846699)
  - 首先感谢各位佬的大义，提供各种key，但是站内各种漫天飞的公益帖子 ，试过不少配置好了之后发现过几天就失效了，都让我产生一种是不是来骗赞的感觉。

- 3 级的就比较稳

- 公益站这种东西很多是朝生夕灭，毕竟免费的东西也没法要求，如果真的有持久的需求还是用正式的东西，公益的适合用在一时兴起的玩具上

- 看公益站渠道来源、大方程度（随便发个一千刀的大概就是来玩票的），其他的也区分不了，不排除部分公益是集合 L 站公益或者找个某个 2api 渠道后练手部署的，见仁见智
  - 再加上可能有号商打击，所以公益死得快是情理之中的事

- 不要对免费的东西有太多执念
- 既然公益，放出来免费用一段时间就可以，这时间可能长或短

- 可以用这样的逻辑理解：支付一个赞用以换取一个短时间的服务。这就好比淘宝上一毛钱一个的wps账号，便宜吗？确实便宜。长久吗？肯定不长久。我觉得编辑帖子花费的时间精力以及信息差本身自带的价值还是值一个赞的。

- 一个人从各种渠道获得了自己用不完的资源，打算贡献出来无偿分享给大家。这是一种美德。 对于这类人，我们应该赞扬他，而不是妄加揣测。 至于你想要找寻的稳定的公益站， @tbphp 的公益站做的非常出色，推荐。
- 放下对公益站的执念就好了，心态放稳，用的时候做好下一秒就消失的准备。当然，也有稳定的，所以T佬公益站的口碑就出来了不是。

- ## [公益站好多！已经对额度麻木了 - 搞七捻三 / 搞七捻三, Lv1 - LINUX DO](https://linux.do/t/topic/1091221/25)
- 我之前也注册了很多，后来慢慢的只剩几个主力了。因为稳定性是个大问题，工作中被打断这件事比较头疼

- 感觉kyx里面claude code不好用，上下文太短，根本写不了代码

- 没几个能用cc 的，没几个额度超过 10 刀的，没几个不是高负载、号池没号的
- 真能干活的没几个，现在用这ang。。。其他几个要么没额度，要么不能直接调用，要么截断。

- [Augment没了，接下来用啥呢  - LINUX DO](https://linux.do/t/topic/1090749)
- 能用claude code最好，不然droid凑合也行，
  - 现在cc中转站因为封号要么涨价要么降智掺水，体验可能还不如droid这个cc下位了，
  - codex我今天试了下，太慢了而且我ubuntu和他那个沙盒模式有兼容问题，这也运行不了那也没权限
- codex我因为这个沙盒问题体验很糟糕，但我看很多人也认为codex和cc是一个级别的，droid我是用了几天，我感觉比cc是能感觉出差距的，但droid免费用claude4.5+gpt5，而且速度很快，codex抛开那个在我电脑上的沙盒兼容问题外，速度也是太慢了，因为我没买那种特别贵的cc中转站，现在用的我感觉是降智很明显，所以我觉得目前我最舒服的是droid

- ## [求推荐稳定的聚合AI大模型平台 - 开发调优 - LINUX DO _202510](https://linux.do/t/topic/1084727/1)
- 满足你的要求的只有openrouter

- 公益站好像都不稳定吧？

- 站内公益站很多都很稳定啊，薄荷佬的，翰林文苑的，都稳定呀
  - 收费的那就看看富可敌国吧

- 我看现在富可敌国都是做codex和cc，没几个开放api呢

- 如果要稳定又要便宜，低价的是没怎么，原价的倒是有挺多

- www.hubagi.ai, 这个有国内的模型，比官网价格便宜，可以用api调用，也很稳定

- ## [如何聚合各家公益站的api - 开发调优 - LINUX DO _202510](https://linux.do/t/topic/1005534)
  - 站内有非常多佬提供的公益站，同时各家公益站又会有很多一样的模型，我的想法是本地搭建一个new，然后配置对接各家的公益站，通过让各家的api轮询，这样子用ai的时候就能雨露均沾了，各家api通过同一个模型名称调用，实现负载均衡
- 怎么实现的？我现在是用newapi重定向功能，的确是集合了，但是不能自动切换，还需要手动切换模型

- 之前有这个讨论，不过要注意，有些公益站是不能用new api聚合，怕二次分发，所以佬友记得要看一下公益站说明

- 很简单的, 模型名一样就可以配置负载均衡了, 自己配置一下模型名到id 的映射就行了

- 目前的方案是gpt-load+newapi, 等gpt-load更新聚合分组和重定向，自用就不用再搞个newapi了

- GitHub - atopos31/llmio: llm接口负载均衡工具 我自己写过一个

- ## [求推荐免费模型api，公益站付费的太慢了，只是用于ai中文翻译成英文，速度有要求 ](https://linux.do/t/topic/1061766)
- 免费的还要快准的 那就薅平台羊毛吧，或者本地搭建一个小模型，肯定嘎嘎快

- 4396佬的cerebras，嘎嘎快

- cerebras的快, ollama cloud的速度也很快 就是上下文砍了

- ## [佬，有哪些好用的公益站llm（个人对话，用量小）  _202509](https://linux.do/t/topic/930055)
- 很多佬的公益站是不让公开的，多水水或许就遇到了呢

- 都是站内的，只要到了等级就能看到了, 你如果的等级不够才看不到，多水就行了

- 所有公益站默认均不支持和对外分享。 除非站长本人同意了。 所有公益站发布原帖子有级别限制的， 默认不转发给级别不够的佬友。 还请新加入的佬友用心升级。

- [[KYX API 公益站] 红绿榜也来了 kunkun 背景也加上了 是ikun就来抽 ](https://linux.do/t/topic/1093602)

- ## [好奇这些公益站的商业模式是怎样的，如何赚钱维持运营 _202508](https://linux.do/t/topic/833661)
  - 论坛里一堆各种api网站，b4u inst anyrouter之类，频繁提供免费api，我一天就能嫖1k左右的货币（不知道是cny还是usd），很好奇这些网站是如何保持生存的，这种行为的目的是什么。

- 一般可能是有别的业务来回血 比如区分等级 免费付费用户之类的

- 都是玩流量的，“公益”往往都是自己用不上的资源，你白嫖他，他白嫖别人。简单几个字：倒买倒卖
  - 所以，早些时候就看到有些人吐槽“零度解说”毁资源，其实这只是愤怒的一种说辞，其实很多资源分享的人，从一开始就知道这资源分享出来不会长久，也不会刻意去想着保护资源，他有自己的目的，可能是商业性的，也可能是兴趣之余回报别人。想保护资源的往往是白嫖了，又不愿意继续分享下去的中间人，这就是人性，面对利益，都想据为己有的心态。
  - 真“公益”也有的，但往往这种极少，本身作者已经是处于社会的佼佼者了，真正能做一点自己理想中的事情了，比如linuxdo，我们看一个人怎么样，往往是这个人做了什么，从论坛创建初期，到现在为止，linuxdo始终在用金钱和责任感为大家提供着一个好的交流氛围环境，这种公益目的就不那么商业化了，主要在于作者的心态，比较随心

- b4u是逆向的，就算通过ccr用在cc也不稳定吧
- b4u是普号池啊，时boom时好的 塞进去都不知道啥时候断

- 靠爱发电啊, 我公益站流量超了都是自己掏钱的, 但实在顶不住了，一天20G流量，只好关停撤啦

- ## [Resource List to build with LLMs for 100% FREE no credit card : r/learnmachinelearning](https://www.reddit.com/r/learnmachinelearning/comments/1ihvm0c/resource_list_to_build_with_llms_for_100_free_no/)

LLM

free LLM from galadriel.com (free 4M tokens/day. This is by far THE best option and i use it myself)

free cerebras and groq -- extremely fast LLM responses but cerebras needs u to sign up on a waitlist

Gemini flash: super generous free tier (1500+ requests/day)

Monitoring

posthog and sentry for monitoring (both with generous free tiers)

Cron Jobs

Free cron jobs via ubicloud.com / github actions

Modal.com gives 30$/month for GPU usage credits

AI Training

Lightning.ai gives u GPU workspace for free

Deployment

free hosting via heroku (24 months for free from github student perks)

Digital Ocean 200$ free credits (needs cc tho)

render has some decent deployment options

Database

cockroachDB (10 GB free)

supabase for DB (500MB free)

free 5GB postgres via aiven.io

- ## [Mistral "free" LLM API is a game changer for so many developers : r/SaaS _202409](https://www.reddit.com/r/SaaS/comments/1fmxg9k/mistral_free_llm_api_is_a_game_changer_for_so/)
- free tier: It's one request per second, 500, 000 tokens per minute, and 1 billion tokens per month. Except Mistral Embed, which is two hundred billion tokens per month.

# discuss-model-abliterated/uncensored/nsfw
- ## 

- ## 

- ## 

- ## 

- ## [Best uncensored open-source models (2024–2025) for roleplay + image generation? : r/LocalLLM _202510](https://www.reddit.com/r/LocalLLM/comments/1o7qxwx/best_uncensored_opensource_models_20242025_for/)
- Midnight Rose and MythoMax are solid uncensored models for roleplay. For 10GB VRAM you'll need heavy quantization which hurts quality.

- The SillyTavern subreddit has a weekly megathread on current models (sorted by parameter range).
  - With 10GB of VRAM, you'd probably want to stick in the 8B-16B category (running around Q4).

- if you’re going fully local, open source LLMs like Mistral, LLaMA 2, or Falcon handle uncensored roleplay well, especially when paired with a lightweight frontend. For image generation, Stable Diffusion forks with ComfyUI or Flux work fine on a 10GB 3080 
# discuss
- ## 

- ## 

- ## 

- ## 

- ## 

- ## 

- ## [State of AI | OpenRouter | Paper : r/LocalLLaMA _202512](https://www.reddit.com/r/LocalLLaMA/comments/1pedmsi/state_of_ai_openrouter_paper/)
- roleplay not programming dominates Open Source model usage, I would have never guessed that
- Maybe because other uses only got good enough lately?
  - Programming has emerged as the most consistently expanding category across all models, accounting for over 50% of total token volume in recent weeks.

- And yet no big model maker has ever tried to optimise a model for creative use cases.

- Just keep in mind open router is not fully representative. For example, grok code fast 1 has been dominating for months due to being free on Kilo code

- ## [I locally benchmarked 41 open-source LLMs across 19 tasks and ranked them : r/LocalLLaMA _202509](https://www.reddit.com/r/LocalLLaMA/comments/1n57hb8/i_locally_benchmarked_41_opensource_llms_across/)
  - Ranks were computed by taking the simple average of task scores (scaled 0–1).

- Please do phi-4. I am Stuck on it because I have not been able to find anything that comes close to it in following instructions and not hallucinating

- This is really awesome! I would also add a column to "normalize" by size-see which model offers the most performance given it's size

- ## [Best uncensored open-source models (2024–2025) for roleplay + image generation? : r/LocalLLM _202510](https://www.reddit.com/r/LocalLLM/comments/1o7qxwx/best_uncensored_opensource_models_20242025_for/)
- Midnight Rose and MythoMax are solid uncensored models for roleplay. For 10GB VRAM you'll need heavy quantization which hurts quality.

- ## [What is the best LLM with 1B parameters? : r/LocalLLaMA](https://www.reddit.com/r/LocalLLaMA/comments/1nsu154/what_is_the_best_llm_with_1b_parameters/)
- In my experience LFM2 1.2B is the clear winner by a huge margin. In terms of coherence, reasoning, and creativity it's better than most 4B models.
  - Whenever I want to run LLM in CPU I usually try:
  - LFM2 1.2B or the new 2.6B
  - Qwen3 4B 2507 (and the old 0.6B but it's pretty outdated by now, there are better options)
  - Gemma3 270M or 1B
  - Among these Qwen3 4B 2507 is the smartest, but it's a big (4B) model, and it'll be pretty slow. I think LFM2 1.2B is the sweet spot at the moment for a generic usecase.

- Try MoE models, OlmoE 1B-7B, Phi-mini-Moe, Granite-4-tiny-preview, SmallThinker 4BA0.6B, EuroMoE-2.6B-A0.6B, all with active parameters under 1b

- Gemma 3 1b is pretty capable, I have also read good things about facebok mobilellm

- ## [What MoE model sizes and capabilities are currently missing in the open weight ecosystem? : r/LocalLLaMA _202510](https://www.reddit.com/r/LocalLLaMA/comments/1o86h5j/what_moe_model_sizes_and_capabilities_are/)
- The knowledge depth of ~70B models has been totally lost in the last few months with very few releases in this size range, MoE or otherwise.

- for sizes: 14b a2b (ish), 50b a5b (ish).

- ## [Best sub 14b llm for long text summaries? : r/LocalLLaMA _202509](https://www.reddit.com/r/LocalLLaMA/comments/1nj78fl/best_sub_14b_llm_for_long_text_summaries/)
- I've done a lot of these tests and the winner in that size range is almost always Llama 3.1 8B for sub-128k and Nemotron-Ultralong-8B for anything higher.
  - They're older now, but nothing recent has come out in that size that handles massive context so well.
- Thanks for pointing out Nemotron-Ultralong-8B! My usual go-to for long summary is Gemma3-12B or 27B, but their competence drops off sharply after 90K of context. When I get home next week I'll compare them to Nemotron-Ultralong-8B. Having a better long-context summarizer will be great!

- Accuracy is hardly defined for a summary, and summarization is basically among the easiest things for an LLM. Context size matters only a little since RAG has become standard and you can guide any LLM to use RAG. Hallucination mainly happens when the LLM has nothing to work with; here you have too much to work with. Just use qwen3 8b with /nothink, or use the "so cheap it's basically free" gemini flash 2.0 on openrouter for incredible context size and speed.

- ## [Best current dense, nonthinking models in the 8b-14b range? : r/LocalLLaMA _202510](https://www.reddit.com/r/LocalLLaMA/comments/1oim98t/best_current_dense_nonthinking_models_in_the/)
- gemma-3-12b-it-q4_0_s - creative tasks and general tasks
  gpt-oss-20b-Q8_0 - cuz work fast even on cpu, working tasks
  Qwen3-30B-A3B-Instruct-2507-Q6_K - cuz work fast even on cpu, working tasks and general tasks
  Llama-3.1-SuperNova-Lite-Q6_K - fast, smart for light tasks
  MN-12B-Mag-Mell-R1. Q6_K - RP tasks and general tasks
  NemoMix-Unleashed-12B-Q6_K - RP tasks and general tasks
  phi-4-Q5_K_M - working tasks / JSON tasks
  Qwen3-4B-Instruct-2507-Q6_K - insanely fast, smart for light tasks
  Qwen3-14B - working tasks and general tasks

- ## [Best Local LLMs - October 2025 : r/LocalLLaMA](https://www.reddit.com/r/LocalLLaMA/comments/1obqkpe/best_local_llms_october_2025/)
- If something beats Qwen3-30B-A3B-Thinking-2507 that's feasible on <=24GB Vram and <=64GB Memory, let me know.
  - I also think nothing under 36B parameters (dense or not) gets close to the performance and knowledge of Qwen3-30B-a3B family of models.

- ## [What's a surprisingly capable smaller model (<15B parameters) that you feel doesn't get enough attention? : r/LocalLLaMA _202511](https://www.reddit.com/r/LocalLLaMA/comments/1ouy2a6/whats_a_surprisingly_capable_smaller_model_15b/)
- Gemma 3 is also a great one for a variety of languages apart from English.

- Qwen2.5 0.5B in Q8 is surprisingly good for utility work, like summarization and search query generation. 
  - It's so tiny basically anyone can keep it loaded permanently alongside bigger models, and so fast its responses are nearly instant (400+ t/s on mid-range Ryzen CPU).

- All of the Qwen3 small models are incredibly capable for their size.

- Qwen3 4B Thinking 2507, and all the finetuned models people have made from it. Even in benchmarks, you look at all the Qwen models and this one has more than the 8B model (though it does use thinking tokens a lot. But thats apparently needed for reasoning.

- Check VibeThinker, for 1.5B is huge in reasoning, math and coding. Can't wait to try4B or 8B.
  - 基于 Qwen/Qwen2.5-Math-1.5B

- I believe that highly specialised small models will eventually replace the jack of all trades master of none small models. Large models can afford to be jack of all trades but small cannot and should specialise more.
  - I mean it depends on what you want. When it comes to writing for example there are mistral 12b fine-tunes that are better than some 70b+ models. There is medgemma 4b which sucks at everything else but gives better medical information than most other models under 100b excluding medgemma 27b.
  - A model trained solely on math and physics or a model trained only on vhdl or python for maximal effectiveness in a single field.

- IBM Granite Tiny with web search, scout-4b/scout-4b. Q8_0.gguf - great for summaries and RAG

- ## [What is the best LLM for large context under 30B? : r/LocalLLaMA _202511](https://www.reddit.com/r/LocalLLaMA/comments/1op1h9h/what_is_the_best_llm_for_large_context_under_30b/)
- almost all LLMs, local or not, struggle really hard with prompt adherence. 150k is beyond what most models work well, even the really big ones. 
  - If you split it into smaller batches, i'd imagine Mistral Small 3.2 or other mistral models of your choosing to be extremely good at this.

- There are 1M, 2M and 4M llama nemotrons. Test'em out may work.

- Gemma 12b - wtf is that? Gemma 3 starts to fall apart at 5k tokens, and by 16k tokens it starts confusing things left and right.
  - Degrade after 5k, unusable after 16k. SWA is a killer of long context performance.

- unsloth has posted the Qwen3-VL models with a 1M context. Maybe try them out. As for how useful it actually is, I don't know. Usually even when closing in at the 256k original limit, it's pushing it and they usually are not so coherent.

- ## [What is the most creative open-weight model for story writing? Whether they are heavily aligned is irrelevant I am asking about pure prose and flavor of writing. : r/LocalLLaMA _202509](https://www.reddit.com/r/LocalLLaMA/comments/1nmp5jc/what_is_the_most_creative_openweight_model_for/)
- I've experimented with a few of the models. Each model has it's own strength, so it's up to you to find a model that has a writing style you vibe with. General rule of thumb though is to avoid reasoning models. 
  - GLM and GPT-OSS are not very good at creative writing, and GPT-OSS just loses track of basic creative writing.

- GLM4-32b is interesting so that it has only 2 KV heads. That makes it extremely economical at KV (32K consumes 2 GiB only) cache but also forgetful. Performance-wise it is smarter than Mistral Small 3.2, but in terms of fluidity, stays between Mistral Small 3.1 and 3.2.

- Qwen 3 <= 32b are boring true. MoE qwen 3 priduce non-boring but strange, poorly structured prose. GLM4 is dry but not exactly boring, compared to old Mistral Small 3.0 or 3.1 which are dry and boring. Properly prompted glm4 with long very detailed prompt is interesting. At short prompts it is not good at all

- 
- 
- 
- 
- 

- ## [What models do you find yourself actually using, and what for? : r/LocalLLaMA _202510](https://www.reddit.com/r/LocalLLaMA/comments/1o1eac0/what_models_do_you_find_yourself_actually_using/)
  - I wanted to gauge what people actually use instead of just going off benchmarks. What models are you running/ which ones are your favorites? 
- qwen3-coder-30b for coding in Python or Javascript/Typescript
  - qwen3-vl-30b and qwen2.5-vl-32b for OCR/document understanding
  - gpt-oss-120b for pretty much everything else (including coding in languages other than Python/JS/TS)
- Using llama.cpp as an inference engine, all models in Q4_K_XL quants from Unsloth, except for gpt-oss-120b which is native MXFP4 quant and qwen3-vl which is AWQ 4bit running in VLLM.
  - I have 24GB VRAM though.

- You running oss-120b across system RAM, then? What kind of speeds do you see? I'm debating grabbing a couple more sticks of DDR5 so I can run it on my 9800X3D.
  - I get 11-12 tok/s running gpt-oss-120b on my 3090 (24gb VRAM) and 64 GB DDR5 using an AMD 9900X. It’s very usable.
- I have 64gb ram also and am able to run it at about 10t/s. Just barely fits as long as you split vram and ram effectively. 

- I mostly run Kimi K2, IQ4 quant (it is 555 GB GGUF file) with ik_llama.cpp. I use it a lot for programming, either by chatting directly in SillyTavern (I use "character cards" as prompt templates for various tasks) or in Roo Code when I need agentic coding (which I do almost daily). 
  - When I need thinking feature, I also use DeepSeek 671B (or as an alternative if K2 gets stuck with something).

- Mainly Mistral Small 3.2 and a bit of: Qwen14b, Qwen 30bA3b, OSS 20b.
  - Essentially any model that can fit Q6 on a 3090 or Q8/FP16. They run at like 40tps or so.
  - I use these models for writing autocomplete and n8n automation. Mistral Small has pretty solid writing and 20b has been able to do some pretty decent code stuff. Still playing around with Qwen.. not sure on its use yet.
  - For complex tasks, like having the LLM generate plugins or chapters of a novel, I use cloud models, but honestly I haven’t actually found it that useful. The local small QOL improvements have proven a lot more beneficial.

- I actually use gemini 2.5 flash lite, which is the best model for the price/performance ratio, the local models are either worse than it or more expensive than it.

- Honestly the benchmark chase can be pretty misleading when you're actually trying to get work done. I've been running mostly Qwen2.5 14B and 32B variants lately, and they're solid performers for real tasks rather than just eval scores. The 14B fits nicely in 16GB VRAM and handles most coding/reasoning stuff I throw at it without the weird quirks you sometimes get with smaller models.
  - For practical use at Anthromind we've found that model selection really depends on your specific workflow rather than general benchmarks. If you're doing a lot of structured output or need consistent formatting, something like Hermes or the newer Llama 3.1 instruct variants might serve you better than the highest scoring model on some leaderboard. The 9070XT should actually work fine with ollama if you want to revisit that setup, but honestly LM Studio is pretty solid for experimentation and the UI makes it way easier to test different quantization levels without messing with command line stuff.

- I have 4090, 3090, 128 gb ddr5 5600
  - I have a bunch of models downloaded but the only ones I actually use are gpt-oss-120b and qwen3 30ba3b coder (q6)
  - I use gpt oss for pretty much everything except for coding tools (qwen code, cline, etc) where the 10k pp/s makes a big difference
  - I can run qwen 235ba22b at 15 tok/s but gpt oss 120b is way faster and tbh i prefer its output (less sycophantic, seems more well rounded)

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
