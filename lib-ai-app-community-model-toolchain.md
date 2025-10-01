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

- ## [What is your primary reason to run LLM’s locally : r/LocalLLaMA](https://www.reddit.com/r/LocalLLaMA/comments/1nsjwv1/what_is_your_primary_reason_to_run_llms_locally/)
- For me, it is independence from Big Tech and venture capital. Open weight models can never be taken away from us.

- New open weight models come out like every week and I want to be able to try the ones that can can run on my PC without waiting for a subscription service to add them or paying per use.

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
# discuss-llm-tools-tips/tricks
- ## 

- ## 

- ## 

- ## [weighted/imatrix VS static quants? : r/LocalLLaMA _202405](https://www.reddit.com/r/LocalLLaMA/comments/1ck76rk/weightedimatrix_vs_static_quants/)
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
# discuss-nvidia/amd/linux
- ## 

- ## 

- ## 

- ## 

- ## 🆚 [AMD AI Max+ 395 CPU 本地大模型推理性能评测报告 - 知乎 _202509](https://zhuanlan.zhihu.com/p/1952045270763283746)
- 针对搭载AMD AI Max+ 395 CPU的零刻GTR9迷你主机进行了一系列严格的大模型推理速度测试。
  - 硬件平台: 零刻 (MINISFORUM) GTR9 迷你主机
  - 核心组件: AMD AI Max+ 395 CPU
  - 任务类型: 本地大语言模型推理
  - 性能指标: Tokens/s (每秒生成Token数) — 该数值越高，代表推理速度越快
- 设计了涵盖多种任务类型的标准化问题：
  - 综合能力: "你是谁？请详细介绍一下你能干什么。"
  - 知识问答: "作为专业人工智能专家，请告诉我如何学习深度学习？"
  - 数学计算: "如果A+B=12, A-B=10，则A的值是？"
  - 自然语言理解: "识别句子‘我将会在明天早上的8点到湖北黄陂的森林公园’中的所有地名。"
  - 代码生成: "请使用Python编写一个贪吃蛇游戏。"

- 参评大模型:
  - deepseek-r1:70b, 30
  - qwen3 系列（32b / 30b / 14b / 8b）
  - gpt-oss（120b / 20b）

```markdown

- model,          ollama, lmstudio
- deepseek-r1:70b, 4.43,   4.97
- qwen3:32b,       8.97,   10.12
- qwen3:14b,       19.47,  21.70
- qwen3:8b,        29.93,  35.96
- gpt-oss:120b,    30.84,  42.07
- gpt-oss:20b,     42.57,  60.54
- qwen3:30b,       48.93,  68.70

```

- 对比两组数据可见，同一模型在LM-Studio中的推理速度普遍优于Ollama
- AMD AI Max+ 395 CPU采用CPU/GPU共享内存的统一内存架构（UMA），这种设计天然适合运行混合专家（MoE）模型（如gpt-oss系列、qwen3:30b）。
  - MoE模型虽然总参数量庞大，但每次推理仅激活部分"专家"参数，非常契合这种大容量内存但绝对算力相对有限的硬件。
  - 相比之下，对于参数密集的传统稠密模型（如deepseek-r1:70b、qwen3:32b），由于需要更高的绝对算力，该处理器的集成显卡则稍显吃力。

- DFRobot作为在单板计算机（SBC）、AI边缘计算和开源硬件领域的创新者，此次测试结果意义非凡。若未来DFRobot推出基于AMD AI Max+ 395 CPU的单板计算机，将其强大的本地AI推理能力与DFRobot成熟的模块化传感器生态（如Gravity系列）相结合，将催生出更多实时、智能的物联网与机器人应用
# discuss-mac-mlx 🍎
- ## 

- ## 

- ## 

- ## 

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

- ## [MLX now has MXFP4 quantization support for GPT-OSS-20B, a 6.4% faster toks/sec vs GGUF on M3 Max. : r/LocalLLaMA _202508](https://www.reddit.com/r/LocalLLaMA/comments/1n4mxrj/mlx_now_has_mxfp4_quantization_support_for/)
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

- ## 🆚⚡️ [Performance of llama.cpp on Apple Silicon M-series · ggml-org/llama.cpp _202311](https://github.com/ggml-org/llama.cpp/discussions/4167)
  - 提供了各种mac, air的模型测试数据

# discuss-lmstudio-roadmap
- ## 

- ## 

- ## 

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

- ## 

- ## 

- ## 

- ## 

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

- ## [Is there an alternative to LM Studio with first class support for MLX models? : r/LocalLLaMA _202506](https://www.reddit.com/r/LocalLLaMA/comments/1l0ct34/is_there_an_alternative_to_lm_studio_with_first/)
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

- ## 

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
# discuss-vllm
- ## 

- ## 

- ## 

- ## 

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
# discuss-ai-api/tools
- ## 

- ## 

- ## 

- ## 

- ## [Jan: an open-source alternative to LM Studio providing both a frontend and a backend for running local large language models : r/LocalLLaMA _202401](https://www.reddit.com/r/LocalLLaMA/comments/193m27u/jan_an_opensource_alternative_to_lm_studio/)
- A Big problem all these LLM tools have is that they all have their own way of reading Models folders. I have a huge collection of GGUF's from llama.cpp usage that I want to use in different models. Symlinking isn't user friendly, why can't apps just make their Models folder a plain folder and allow people to point their already existing LLM folders to it
  - This is salient criticism, thank you. At the core, we're just an application framework. We should not be so opinionated about HOW users go about their filesystem.

- Ollama being the biggest offender, with that fake docker syntax for modelfiles, model import and renaming using sha hashes.

- The Stable Diffusion UI variants also had this problem - until Stability Matrix came along and resolved a number of inconveniences with model management. Wonder if something similar could be viable here too.
  - invokeai 的选择文件也是一种方案

- Its why Koboldcpp just has a file selector popup, it doesn't make sense to tie people to a location.

- Is it better to use llama.cpp instead of LM Studio? 
  - Absolutely! KoboldCpp and Oobabooga are also worth a look. 
  - I'm trying out Jan right now, but my main setup is KoboldCpp's backend combined with SillyTavern on the frontend. 
  - They all have their pros and cons of course, but one thing they have in common is that they all do an excellent job of staying on the cutting edge of the local LLM scene (unlike LM Studio).

- 
- 
- 
- 
- 
- 
- 
- 
- 

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

# discuss-model-tuning
- ## 

- ## 

- ## 

- ## [What’s the training cost for models like Qwen3 coder 30b and is the code for training it is open source or close source? : r/LocalLLaMA _202509](https://www.reddit.com/r/LocalLLaMA/comments/1njws3n/whats_the_training_cost_for_models_like_qwen3/)
- You can do fine tunes on the 4B real easy with Unsloth. LoRAs and QLoRAs, too. It won’t take much VRAM. You can fine tune a LoRA for Qwen3 30B A3B Instruct 2507 in BF16 on a single 96GB 6000 Pro in just a few hours.
  - That depends entirely on what you are training and the size of your dataset. True fine tuning, on a really small dataset will take a few hours, but if you are trying to train in new capabilities, that is going to take a much larger dataset, and could be months or over a year on a single RTX pro 6000.

- Their exact code isn't open source, but many companies train using Pytorch and Megatron-Core open source code.
  - I estimate GPU-time needed for training Qwen 30B A3B to be around 800 000 hours for H100 SXM5, so around 1.6 million dollars. That's for pretraining on 20T tokens, assuming 40% MFU.

- Stick to finetunes, you don't have the hardware or budget to pretrain models of practical size (believe me I have tried).
# discuss
- ## 

- ## 

- ## 

- ##
