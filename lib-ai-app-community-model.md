---
title: lib-ai-app-community-model
tags: [ai, community]
created: 2023-10-30T07:33:56.233Z
modified: 2023-10-30T07:34:03.602Z
---

# lib-ai-app-community-model

# guide

- tips
  - 大模型相关的产品研发，原理的可解释性很差，效果的可解释性也差

- [大规模语言模型：从理论到实践](https://intro-llm.github.io/)
  - 复旦大学张奇教授团队写了一本在线免费的电子书，大概有 300 页篇幅，将大模型从理论到实战的每个阶段都描述的较为清楚
# discuss-stars
- ## 

- ## 

- ## 🤔 [端侧模型会是 AI 技术演进的下一个 「必争之地」 吗？当前落地面临哪些核心瓶颈？ - 知乎](https://www.zhihu.com/question/1914319403023032351)
- TO C场景应用最大特点是硬件参差不齐。性能差能大到10多倍以上。
  - 技术栈必须满足所有主流硬件结构差异和性能性能下，保持相对一致的使用体验。这是一件极累的活儿。
  - 服务端下个开源模型搭个WEB服务写个HTML就能卖服务了。端侧想内嵌AI模型产品化，同时还要解决实时性，要解决的工程问题要多10倍不止。要自己优化模型。甚至要自己搭建模型结构，自己准备数据训练。
- 目前看端侧完全谈不上AI演进必争之地。一来硬件较弱且参差不齐，导致TO C工程保障体验极度困难和复杂。二来PC高算力硬件完全不是大众消费级的售价和定位，最后，还没有什么端侧AI落地产品的应用范式。
  - 从应用体验上，那些允许延迟500毫秒以上，对带宽需求不大的应用，都可以放到云端。
- 真需要做到端侧的，其实是那些需要即时响应的应用场景。
  - 为数不多的应用类别，比如即时交互影像相关，语音相关的，诸如游戏，需要即时交互的数字人，3D虚拟AI人，虚拟人直播等，可能会对端侧AI有部分需求
- 这类应用有3个特征： 
  - 1 即时性直接影响体验，不能等。 
  - 2 对算力要求相对低，运算本地算力能够满足，并不一定非要云算力支持。 
  - 3 对带宽要求较大，云服务的成本过高使得商业模式不成立，所以需要放入本地。
- MOBILE离端侧可能更远。 由于算力极为低下，只有很少的情况才需要手机上即时响应AI推理给出的结果。即那些把手机作为信号传感器，即时对信号运算的场合：比如表情捕捉、手势、肢体动作捕捉和识别，语音、运动数据处理和生物信号处理等。 
  - 如果手机没有专用神经/张量芯片，GPU还需要承担渲染3D图形，那么能跑的AI模型会更加受限。
  - 目前测试，某手机用NPU跑模型比不用最多能快10倍。 
  - 手机芯片商是否有动力发展，要看手机作为数据传感器即时处理数据能带来多大的应用市场。

- 本地部署模型的优势在于低延迟，这在我看来其实也是个相对偏伪的优势。
  - 事实上，现代网络环境实际上以及足够快速和稳定，无论是流量还是WiFi，辅以CDN边缘节点优化后，绝大多数主流AI应用的云端响应都能稳定在几十毫秒以内。
- 端侧设备受限于功耗、热量、算力等物理条件，往往只能部署轻量化模型

- 移动设备上长期运行一个有竞争力的大模型仍然不现实，负载、资源占用、电量消耗、发热等等问题，很难做到好的体验，更不要说物联网设备、智能音箱等低功耗产品了。
  - 很多声称自己用了端侧大模型的，实际上仍然离不开云端的协同配合，或者说主要靠云端，备用方案可能是端侧，但把端侧拿出来大肆宣扬，来做广告而已。

- 🐛 端侧模型的劣势
  - 端侧模型仍然受限于设备本身的内存、功耗和算力
  - 云端模型可以随时升级，热更新机制保证所有用户第一时间享受新一代模型
  - 端侧模型对于不同设备和硬件架构需要分别适配

- 端侧适合的场景还是隐私、极低延迟，或者全天候。

- 如果完全跑在端侧，那商业模式怎么做？现在的主流是订阅制，但完全本地的订阅制，吸引力比较低，破解风险比较高吧

- ## deepseek 3fs 其实不是很理解这样的意义是啥… 已经脱离 FS 的通用接口了，为啥要硬挂一个 FUSE VFS 层… 直接摒弃 VFS 走个私有的 protocol 不干净多了…
- https://x.com/silsrc/status/1895390926098571505
- > Most applications use FUSE client, which has a low adoption barrier. Performance-critical applications are integrated with the native client.

- 我的第一反应是现有框架应该没办法大批量改用私有的 API，比如在 Python 我就是要用 pathlib. Path 对文件做点简单操作，那确实只能是挂 FUSE 上去了

- ## 聊一聊国内大模型的安全机制： 一般是两套，分别作用于train-time和test-time。
- https://x.com/9hills/status/1840786446153921017
  - 训练的时候增加安全和价值观对齐的SFT和偏好对齐数据。最终效果类似开源的Qwen2模型，有点用但是很容易被Jailbreak。
  - 推理时增加安全算子，具体有几种
- 技术难点有两个：
  1. 训练分类器的大量非安全数据，所以说你先成为反贼才能识别反贼。
  2. 模型要做的足够小足够快，最小化影响模型ttft和tps。
  3. 流式很难，某模型最早是一句句输出的，后来才改成token级流式。
- 请教一下，现在市场上的大模型，怎么知道他们的训练数据是多久的呢？
  - 可以问一些特定时间的新闻来验证，但是其实没关系。模型的精确知识不重要，也充满幻觉。

- ## Attention is *Not* All You Need，还是有人在尝试 transformer 以外的架构，
- https://x.com/liumengxinfly/status/1835251398692508114
  - 毕竟 transfermor 推理复杂度在数学上是无法线性扩展的，早晚会走到瓶颈

- ## 国产188个大模型的excel文档： 北京69 上海22 杭州15 广东26个 江苏15个
- https://twitter.com/FinanceYF5/status/1730912502312296935
  - [国产大模型188个list - Feishu Docs](https://zw73xyquvv.feishu.cn/wiki/WXLmwBbYuiTobkkJ6Ojc2cxqnj0?sheet=2XjJlJ&table=tblS2Jv7isKtSODz&view=vewfCdOf0U)

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

- ## 
- 
- 
- 
- 

# discuss-local-llm
- ## 

- ## 

- ## 

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

- ## [如何看待苹果发布的 MLX 机器学习框架？ - 知乎 _202312](https://www.zhihu.com/question/633585779)
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

- 
- 
- 
- 
- 

# discuss-llama

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
# discuss-ai-api/tools
- ## 

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

# discuss-ai-knowledgebase
- ## 

- ## 

- ## 

- ## 一些企业描述为知识库的需求，实际上是没有办法通过当前的 RAG 来满足的，更像是一个本地的 Deepresearch 或者其他的 agent 可以 cover 的场景。 不要被带到坑里。
- https://x.com/YinsenHo_/status/1954741140307235282
- 根据我的日常经验。企业其实更倾向于半自动。通过AI大模型快速找到相关的几个类，最后汇总一下。由于审核的存在，根本无法做到全自动

- ## 🆚️ 这几天在给公司产品的 AI 助手选择知识库的数据处理工具，重新看了一遍 Marker、MinerU、Docling、Markitdown、Llamaparse 这五个工具
- https://x.com/shao__meng/status/1893984985998365096
1. Marker
技术架构
· 基于 PyMuPDF 和 Tesseract OCR，支持 GPU 加速（Surya OCR 引擎），开源轻量化
功能特性
· 专注 PDF 转 Markdown，支持公式转 LaTeX、图片内嵌保存，OCR 识别扫描版 PDF
· 多语言文档处理，但表格转换易错位，复杂公式识别精度一般
适用场景
· 科研文献、书籍等基础 PDF 转换需求，适合技术背景用户快速部署
优劣势
✅ 开源免费、处理速度快（比同类快 4 倍）
❌ 缺乏复杂布局解析能力，依赖本地 GPU 资源

1. MinerU
技术架构
· 集成 LayoutLMv3、YOLOv8 等模型，支持多模态解析（表格/公式/图像），依赖 Docker 和 CUDA 环境
功能特性
· 精准提取 PDF 正文（自动过滤页眉/页脚），支持 EPUB/MOBI/DOCX 转 Markdown 或 JSON
· 多语言 OCR（84 种语言），内置 UniMERNet 模型优化公式识别
适用场景
· 学术文献管理、财务报表解析等需高精度结构化的场景
优劣势
✅ 企业级安全合规，支持 API 和图形界面
❌ 依赖 GPU，表格处理速度较慢，配置复杂

1. Docling
技术架构
· 模块化设计，集成 Unstructured、LayoutParser 等库，支持本地化处理
功能特性
· 解析 PDF/DOCX/PPTX 等格式，保留阅读顺序和表格结构，支持 OCR 和 LangChain 集成。
· 输出 Markdown 或 JSON，适合构建 RAG 知识库
适用场景
· 企业合同解析、报告自动化，需结合 AI 框架的复杂应用
优劣势
✅ 与 IBM 生态兼容，支持多格式混合处理
❌ 需 CUDA 环境，部分功能依赖商业模型

1. Markitdown
技术架构
· 微软开源项目，集成 GPT-4 等模型实现 AI 增强处理，支持多格式转换
功能特性
· 支持 Word/Excel/PPT、图像（OCR）、音频（语音转录）转 Markdown，批量处理 ZIP 文件
· 可生成图片描述（需 OpenAI API），但 PDF 格式转换易丢失结构
适用场景
· 多格式混合内容创作，如 PPT 图表转文档、音视频转录
优劣势
✅ 格式支持最全，开发者友好（Python API/CLI）
❌ 依赖外部 API，部分功能需付费模型

1. Llamaparse
技术架构
· 专为 RAG 设计，结合 Azure OpenAI 和 KDB AI 向量数据库，优化语义检索
功能特性
· 解析含表格/图表的复杂 PDF，输出 Markdown/LaTeX/Mermaid 图表
· 支持生成知识图谱，企业级安全合规
适用场景
· 法律文档分析、技术手册问答等需结合 LLM 的智能应用
优劣势
✅ 解析精度高，支持半结构化数据语义优化
❌ 处理速度慢，免费额度有限，需 API 密钥

选型决策树 
需求优先级：
速度与轻量 → Marker
精度与多模态 → MinerU
企业级集成 → Docling/Llamaparse
多格式混合 → Markitdown

技术适配：
需 GPU 加速 → MinerU/Docling
需 API 扩展 → Markitdown/Llamaparse
需本地隐私 → Stirling-PDF（补充推荐）

成本考量：
免费开源 → Marker/MinerU
商业支持 → Llamaparse

- 我这里10000 页以上的企业级应用的方案可以分享下，我这个是经验累计下来的结果。这 10000 页解析都做过了人工校验，可以说市面上大部分方案都测试过了。最佳实践结论如下：
- PDF： 
  1. 离线（复杂）场景：MinerU + VLM识别 + LLM修复
  2. 离线（简单）场景：Marker 
  3. 在线（通用）：Llamaparse OR VLM
  [VLM 离线用 Qwen2.5 / VL 在线 gemini 2.0 flash]

- 根据我之前的调研，感觉目前还没有完美的支持多类型文档多模态的解析库。速度，准确性，成本三角里，最均衡的个人觉得反而是楼上有人说到的大模型多模态解析能力
  - 速度-准确性-成本三角，确实很重要，看需求中哪个角更看重了。
  - 多模态解析这种方式挺不错，我们也放在对比中，特别是 gemini 这种成本低多模态能力强的。

- 多模态解析这种方式挺不错，我们也放在对比中，特别是 gemini 这种成本低多模态能力强的。

- Docling也有点慢... 没有GPU加速的其他库也不快... 平均下来都是 1.x page/s , 比如MinerU一个20页的paper, 一个GPU L4, 最快也要十几秒 到生产环境不开多GPU并发, 时间上是个大问题, 

- ## Excited to share Latticework, a text-editing environment aimed to help synthesize freeform, unstructured documents _202408
- https://x.com/andy_matuschak/status/1828928979656683581 
  - It aims to help with making sense of messy piles of unstructured documents. 
  - The key idea is unifying annotation (direct reaction in context) w/ freeform text-editing (for fluid sensemaking).
- sorry, the PDF story doesn’t really exist in this prototype, but I think the design applies without alteration—just need someone to build it

- https://x.com/MatthewWSiu/status/1828929032718872734
- I explored some closely related ideas with @MagicPaperAI . You guys have pulled off the synthesis of highlights and copied fragments. I’d posit that the next key synthesis is between copied fragments and revisions of a document. Edits are partial copies.
- Great work! I like the flow of adding & organizing snippets -> augmented synthesis. The more snippets you grab under a heading, the clearer a cluster forms. That then generates 'what you're getting at' summaries & gives AI bounds to forage for related snippets. Good loop there.
# discuss-llm-architecture
- ## 

- ## 

- ## 

- ## 

- ## [如何看待观点：AI 的关键点不是prompt，而是Context Engineering？ - 知乎](https://www.zhihu.com/question/1923364519964545063)
- Context远不止是一句prompt，它包括：
  - 指令/系统提示：定义模型行为的初始指令
  - 用户提示：来自用户的即时任务或问题
  - 状态/历史：当前对话的短期记忆
  - 长期记忆：跨多次对话收集的持久
  - 知识库检索信息(RAG)：来自文档、数据库或API的外部知识
  - 可用工具：模型可以调用的所有功能定义
  - 结构化输出：对模型响应格式的定义
- 这其实就是在构建一个完整的「AI工作环境」，而不是简单地给AI下指令。

- 即使你写不好prompt，市面上也有很多AI工具可以帮你做prompt enhancement
  - 期待AI能「有记忆，懂用户」。因此，Context Engineering（上下文工程）就开始被关注到。
  - context engineering, 是指通过系统性构建、管理和优化 AI 模型的输入上下文，以提升模型在复杂任务中的理解与输出能力。
  - 第一是历史交互数据。
  - 第二，是context的总结。对话可以一直延续，但模型的上下文窗口有限，怎么记住之前的对话？当然是压缩，例如把最近5条对话的内容原封保留，再之前的内容总结一下。
  - 但更重要的，是领域知识与背景信息。
- AI的能力来源于两个方面 in-weights memory（训练集里学到的） 和 in-context memory（参考资料里学到的）。 in-weights memory基本上是很难修改的, 但in-context memory 更容易修改和更新，你只要提供新的资料，正确的资料，模型就能有「新知」

- 复杂的AI应用，不是靠chat输入提示词这么简单，而是需要自动化多次和大模型的交互，这个自动的过程中，需要能够自动产生给大模型的提示词。

- Agent = LLM + Prompt + 工具调用，但从工程视角来看，这些本质都是Context Engineering，也就是上下文工程。
  - Context Engineering就是在每次调用里，把模型完成任务所必需的信息按对的格式、在对的时机准确打包进去。

- 上下文工程，AI绘图用户早就天天在用了
  - 当你使用 Inpaint（局部重绘） 功能时，AI不是凭空想象，而是基于你留下的画布、边缘线条、光线方向、已有画风来补全区域，这就是“图像上下文”
  - 当你进行 Outpaint（图像扩展） 时，AI必须参考原图的构图逻辑、色彩渐变、风格纹理、人物透视来生成自然衔接的部分。这种对上下文的“理解”和“建模”，比提示词本身更重要
  - 当你用 Photoshop内置的Firefly进行局部修改创成式填充时，真正起决定作用的不是你说了“给我加一个灯塔”，而是AI是否准确读取了当前画面是夜晚、是水边、有光源投射、有透视消失点。
  - 上面这些功能，哪怕你根本不写提示词，好的工具也能给你脑补好，比如我现在根本放不开订阅的Photoshop AI。

- 
- 
- 
- 
- 

- ## DeepSeek最大的创新，是不需要大量的人工标注，而是直接从其他大模型蒸馏或者使用群体相对策略优化算法（GRPO）、CoT（自我反思）来给大模型反馈，
- https://x.com/seclink/status/1888011462008005030
  - 就相当于完全使用RL（或者另一个基础大模型）来替代人工标注了。
  - 这实际上是抢了Scale AI 这种公司的蛋糕，DeepSeek牛X之处在于，很多老外一开始不信，然后照着论文里的方法快速（局促地）复现，却发现竟然也能复现成功。

- cot和蒸馏之前，就通过grpo进行rl获得了相当不错的推理能力。。你这整理的不清晰。

- 这没有任何创新，GPT1就用了同样的方法，而且现在不使用是有理由的。因为deepseek模型本身不行，一个query需要RL chain才能达到可接受的答案，致使inference 效率低到可怕，虽然training便宜，但是operation cost要多好几倍，得不偿失

- 你这个说的完全不对，CoT是GPT发明的，蒸馏也早就有了，RL也早就有了，deepseek是发明了RL里的GRPO

- ## I read up on DeepSeek’s learning algo, GRPO. GRPO: group relative policy optimization
- https://x.com/virattt/status/1885102056546910672
- How GRPO works:
  1 • model generates a group of answers
  2 • compute score for each answer
  3 • compute avg score for entire group
  4 • compare each answer score to avg score
  5 • reinforce model to favor higher scores
  - This process is repeated, allowing the model to learn and improve over time.
- Other methods like PPO, use a value function model to do reinforcement learning.
  - GRPO does not, which reduces memory and computational overhead when training.

- GRPO was proposed for the first time in Feb 2024 in DeepSeekMath paper. It is not new.
  - Back then they used Neural Networks for Rewards (PRM/ORM). The magic happened when DeepSeek  replaced PRM/ORM with the exact reward (Verified Reward).

- ## 🔡 OpenAI's Deep Research is just a search+read+reasoning in a while-loop, right? here is my replicate of it in nodejs, using gemini-flash and jina reader
- https://x.com/hxiao/status/1886250705415229627
- If it includes evaluating js driven websites, including images Then yes 
  - To really replicate that, you'd probably wanna just use puppeteer, save the whole page as an image, extract the info from that, and then crunch that data

# discuss-multi-agents 🏘️
- ## 

- ## 

- ## 

- ## 🆚 今天很有趣，两家知名的公司各出了一篇文章，争论要不要使用多智能体系统。
- https://x.com/oran_ge/status/1933754019010539923
  - Claude 的官方 Anthropic ：如何构建多智能体系统
  - Devin 的官方 Cognition ：不要构建多智能体系统
- 这核心的争议点在于：Context 上下文到底应该共享还是分开？
  - Claude 这边的观点是，搜索信息的本质是压缩，单个智能体的上下文有限，面对无限的信息，压缩比太大就会失真。这是集体智慧，一起协作获得的胜利。
  - Devin 这边的观点是，多个智能体的上下文不一致，会导致信息割裂、误解、他们汇报给老板的信息经常充满了矛盾。
  - 这让我想到，软件工程从来不是追求完美，而是持续迭代。

- 没啥矛盾的。看需求。open-ended 的问题比较适合 multi-agent；目标很具体的话，就比较适合单个 agent

- 感觉和现实中的两家不同策略运营的公司差不多，没有绝对的对和错，都能走出来的可能性也超大。

- ## @KuraAIAgents 通过创新的五重 Agent 架构（规划、执行、评估）实现了 87% 的浏览器自动化准确率，超越 Claude 计算机操作 28 个百分点，同时支持低成本模型替换方案
- https://x.com/shao__meng/status/1857586562588094918
  - 包含5个专门的 Agent，其中3个核心 Agent 形成一个循环系统
  - 在 WebVoyager 基准测试中取得 87% 的成绩
  - 比 Claude 的计算机操作高出 28%
- 五个核心 Agent：
a) 初始规划者(Initial Planner)
- 负责制定高层次计划
- 使用 OpenAI o1 模型进行推理
b) 循环规划者(Agent Loop Planner)
- 评估任务是否完成或不可能完成
- 为执行者提供下一步指令
- 根据需要修改计划
c) 执行者(Executor)具备三项核心技能：
- 网址导航和返回
- 读取当前页面数据
- 执行屏幕操作(点击、滚动、输入)
d) 循环评论者(Agent Loop Critic)
- 评估执行者的表现
- 特别在复杂界面操作中起关键作用
e) 最终评论者(Final Critic)
- 评估整个任务轨迹
- 必要时提供反馈并启动新的循环

- ## OpenAI 发布多 Agent 编排框架背后的思考以及实践过程
- https://x.com/tuturetom/status/1845634978530693494
  - 核心是 OpenAI 的工程师在思考  Agent 的「路由」 + 「移交」等能力时拓展出来的一个示例，进而发现这个示例原语很普适，所以开发了 Swarm 框架
  - 所有伟大的思考都源于周末业余工作

- ## OpenAI 悄悄开源了构建多代理智能体协同框架：Swarm
- https://x.com/aigclink/status/1844936446416912628
  - 用于构建、编排和部署多代理

# discuss-news-ai-model
- ## 

- ## 

- ## 

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
# discuss
- ## 

- ## 

- ## 

- ## 做产品级搜索以后发现 3.7 效果特好但是特别贵，所以必须得做 content cache 降低成本。
- https://x.com/arvin17x/status/1896922111505285484
  - 但为了做 context cache ，发现必须得记录 token usage，不然感知不到 cache 的效果。

- 可以分享下 Context Cache 的原理么，我还以为这种东西只能在模型供应商侧做。
  - 就是在模型供应商侧做。只是 OpenAI 和 DeepSeek 做的是静默方案，而 Anthropic 和 Google 是需要开发者手动开的
- 应该是 prompt caching 吧
  - Anthropic家自己的说法是 prompt Caching. 但我感觉行业里感觉还是习惯叫 context caching 的。
  - 不过 OpenAI 官方和 Anthropic 官方都称之为 prompt caching

- 很奇怪，这玩意为啥不默认开启。
  - 某些场景下的确不一定适合，因为写入 cache 的成本是原价的 1.25倍

- ## It is common to generate train and validation sets using random splitting.
- https://x.com/_avichawla/status/1898622288737767785
  - However, in many situations, it can be fatal for model building.
  - Consider building a model that generates captions for images.
  - Group shuffle split solves this.

- ## 由于DeepSeek-R1 爆火，所以为大家带来什么是LLM蒸馏技术的笔记。
- https://x.com/karminski3/status/1882233538042597423
  - 几个助记词：教师模型，学生模型，软目标，硬目标。

- https://x.com/ShanghaoJin/status/1882679738789216456
  - 你听说过什么叫“蒸馏”么？说个大白话：就是拿人家算出来的模型参数，跳过所有数据清洗、训练，做最后一程。其实没有任何创新
  - 好像人家证明了π=3.14，他拿结果去算了圆面积。让他再自己去证明算一个e，他又抓瞎了
- 千万不要用“大白话”来解释自己都没完全理解的概念， 只能让外行拍手，懂的人只会笑话你。 你完全不知道蒸馏是在干什么。如果你知道的话，那就是完全不知道Deepseek 在做什么。
- “蒸馏”说法不正确。1. 蒸馏效果一般不会超过原模型 2. deepseek的 reasoning行为和市面上其他模型不一致(有超越人类标注的奇妙行为) 3. 开智对再训练模型有禁止并会监控 API滥用

- ## 我日常用 Cursor 写代码的场景之一：“请参考代码 @ XXX1 @ XXXn 做 YYY 事。”
- https://x.com/dotey/status/1869436413600731146
  - 简单来说就是让 AI 照葫芦画瓢，重要的是给出充足的上下文，让 AI 可以学习和模仿。剩下的就是 Review + Accept，很简单高效。
  - 特别要注意的是第一个“葫芦”要打磨好，这样后续的“瓢”才不会画歪。

- 更简单的做法有时候可以直接 @ git 某次提交

- 我现在是新项目里创建一个txt文件，里面写上想法和gpt对我想法的建议，然后让cursor 参考这个文件来开发，里面我也有时会写上步骤，首先实现什么，然后实现什么，做一段了，让cursor根据这个文件检查一下项目完成度，列出来哪些没做，这样反复迭代向前

- LM 充分证明了人类的本质就是复读机。 哪里有什么指令遵循，推理，大家都是从不同的维度用不同的方式在复读一些东西而已

- ## 如果想要让 LLM 稳定生成 JSON 对象，最简单的方式就是使用 zod 定义 schema 并配合 @vercel ai sdk的 generateObject使用，比如这里我想要从网页文本内容提取结构化的信息。
- https://x.com/FeigelC35583/status/1819558128297648412
  - 这种方式和当初 langchain 在 prompt 里写一大堆json 定义有本质区别，在于使用了 function call 的能力
  - 从请求中可以看到，本质上是在调用模型的时候，构建了一个名为 json 的 函数, 描述是 respond with a json object, 其中参数是自己定义的 schema，然后在 tool_choice 中限制必须要使用这个 json 函数，那么模型就会返回调用json 函数的参数，即你定义的 schema
  - 示例代码来自于https://github.com/DiscovAI/DiscovAI-crawl 我正在 building 的一个面向 RAG 应用的爬虫平台
- 应该只有GPT系列能用吧
  - 支持function call就可以，deepseek应该也可以的
- 在这基础上。我会考虑使用jsonrepair这个包，手动修复下，增加容错
- 如果大模型没有没有返回对应要求的字段数据，或者返回错了类型，它会怎么样，会自己补充空的，或者自动转换类型吗？
  - 不会补充，会throw error，也可以用上面推友推荐的jsonrepair手动fix

- 能支持开源模型吗
  - 取决于模型支不支持function call，支持的话就可以，效果的话要看模型的能力
- 用 function call 感觉模型的能力降了一个维度，不如直接给文本，我还是更喜欢用xml自己提取。

- 我是用伪代码➕类型声明, 也是一样的稳定输出 json
- langchain框架中有Pydantic json 解析器可以直接用，本质也是生成schema，再配合重试解析器也可以稳定生成json格式

- ## 💡 LLMs are literally the most unreliable technology of all time (followed by **ing bluetooth)
- https://x.com/Steve8708/status/1819448686424084892
  - After an absurd amount of trial and error, we've internally created a set of rules for make LLMs considerably more reliable
  - our secrets: restrict the llm to only what rag provides

- what's your stance on AI for no-code? Do people prefer drag-and-drop vs prompting?
  - i think the winning move is combining both

- Bluetooth is hell and causes frustration daily.

- ## 🌰 Firefox will use Transformers.js to power on-device features
- https://x.com/osanseviero/status/1797291569348751848
  - In their PDF Editor to generate alt text for images
  - Improve translations
  - Fully offline, open-source and with <200M models
- [Experimenting with local alt text generation in Firefox Nightly - Mozilla Hacks - the Web developer blog _202405](https://hacks.mozilla.org/2024/05/experimenting-with-local-alt-text-generation-in-firefox-nightly/)
  - https://huggingface.co/Mozilla

    - 提供了数据集和模型

- Offline and open-source is a big win for privacy-focused tools

- ## [langchain到底该怎么使用，大家在项目中实践有成功的案例吗? - 知乎](https://www.zhihu.com/question/609483833)
- LangChain之所以大火，是因为它提供了一系列方便的工具、组件和接口，大大降低了 AI 应用开发的门槛，也极大简化了大模型应用程序的开发过程。
  - LangChain框架背后的核心思想是将自然语言处理序列分解为各个部分，允许开发人员根据自己的需求高效地定制工作流程。
- Langchain有6大核心模块：
  - Models：模型，是各种类型的模型和模型集成。
  - Prompts：提示，包括提示管理、提示优化和提示序列化。
  - Memory：记忆，用来保存和模型交互时的上下文状态。
  - Indexes：索引，用来结构化文档，以便和模型交互。包括文档加载程序、向量存储器、文本分割器和检索器等。
  - Agents：代理，决定模型采取哪些行动，执行并且观察流程，直到完成为止。
  - Chains：链，一系列对各种组件的调用。
- LangChain 通常被用作「粘合剂」，将构建 LLM 应用所需的各个模块连接在一起。使用Langchain中不同组件的特性和能力，可以构建不同场景下的应用，如聊天机器人、基于文档的问答、知识管理、个人助理、Agent智能体等等。

- 你的这个认识存在一些偏差，首先，依赖API key 是为了你使用大模型厂商的服务和鉴权，这没有什么拉跨的。很多第三方的服务都需要鉴权验证，这是比较主流的方式。
- 可以企业自己部署大模型，这种成本是很高的。从我们自己的实验效果来看，13B 以下的大模型基本就是玩具，优化半天费时费力，而 34B 或者更大的模型，公司部署成本又很高。
- langchain 中的特色是它的 langchain expression language (LCEL），是一种类似 linux 管道形式的调用方式，可以很简单的实现它的 chain 相关的功能。这个，在我实际使用的时候，没有想象的那么好用，可以根据实际情况去学习。
- 最后，langchain 中还有一个叫做 langgraph 的组件，能够和 pytorch 一样用搭积木的方式去构造一个有向无环图、循环的链，比 LCEL 更高级。

- 
- 

- ## LLM搞反编译，.not care和Jvav用户再也不用折腾什么混淆了，都没用了
- https://twitter.com/geniusvczh/status/1774053196039962758
  - 文章里反编译的是x86, x86都可以，IL难度只会更低
- 大概看了一下，就是把编译出的汇编跟源代码做了一个简单的seq2seq的fine tune，训练集连混淆都没有，离让所有混淆都没用那更是还差得远。
- 17年google那篇transformer的论文就靠这样完成了自然语言的翻译，这些都是迟早的事，反编译和反混淆的训练数据都是可以批量生成的，做起来简单多了
  - 我觉得LLM对于反编译和反混淆，可能更大的作用在于生成人类友好的变量/程序结构。毕竟反编译和反混淆是猫鼠游戏，总可以想出新点子，人类的干预还是必不可少的，这种情况下，基于规则/程序分析的传统方法可能更好，然后再用LLM猜变量名
- 为了拉资金而已，钱申请到了论文就没啥用了……处理屎山留给巨头的程序员就行了，还轮不到学术圈来指点江山
- 这种局限于函数的反混淆啥用都没有，对付点三脚猫功夫的混淆还差不多

- ## 🪧 研究了一下本地大模型的场景：
- https://twitter.com/changmingY/status/1773336179296887162
  1. 不能联网的国内用户
  2. 一般用户机器配置达不到，效率太差
  3. 本地知识库算是一个刚性需求
  4. 垂直领域模型越来越多, 一个hub集中使用
  5. 小而美的模型会越来越多，完成一个特定功能

- ## ollama 的编译玩的太花了，先是吧 llama.cpp 在不同 cpu 和 gpu 的动态链接库都编译了出来避免用户在运行时再去编译，
- https://twitter.com/liumengxinfly/status/1767073319956971891
  - 然后用 go 的 embed 特性直接把这些动态库全都打包到 go 的二进制里，然后在用 cgo 和 dlfcn 加载和调用 llama.cpp，实现了一个二进制文件免编译，免安装的解决所有问题

- https://twitter.com/holegots/status/1767427148506431665
  - 不过这个本质也是 llama.cpp 套壳吧 , 底层还是 cpp, golang 并不参与实际的推理.

- ## 最新版的 OpenAI Translator 已经无缝支持本地大模型了（Ollama），无需联网，快速便捷，安全稳定！再也不怕 OpenAI 账号被封了！翻译效果对比大家可以看一下截图，大家快来下载体验一下吧！ _202402
- https://twitter.com/yetone/status/1761607398819840511
- 现在好像还不支持自定义模型？只有有限的几个模型可供选择，最好是有一个文本框可以自定义输入
- 这是Mistral多大的模型，7B的吗？
  - 是的

- 不知道这些7b 13b的小模型哪个翻译质量更高

- ## 阿里云竟然支持这么多模型了
- https://twitter.com/yihong0618/status/1746745371441967540
- http://ai.azure也包含了好多模型，昨天惊到了

- ## 越来越觉得 RAG 这东西有意思。
- https://twitter.com/wwwgoubuli/status/1737471851654160548
  - 半年前接触到这个词的时候开始我还有些不屑，搜索内容插入到提示词算什么嘛，小学二年级都能明白。尤其是看到随便丢向量库都能跑出个七七八八，越发觉得这个简单。
  - 但现在真的搞了半年，我越发的觉得这才是下一个大多数人可以参与的风口。它有门槛。
- 技巧很多 所以好玩 但风险是大部份技巧都被模型提供商玩过，80%需求都可能被他们直接覆盖
  - RAG不就是query transformation/rewrite/expanding, hybrid search, reranking, etc吗？当然还有些其他技巧啥IAG之类的。数据ingestion也有些技巧，不过我看主要还是在query上。 这些大部分OAI, Baichuan, 月之暗面内部都探索过了吧
- RAG一看就是一个有问题的区域，大模型随时下一次升级可能就会改变整个框架，3.5还胡说八道，4已经很多都是有根有据的了
- 搞到最后，还是清洗数据，RAG只用简单策略解决大多数问题，可观测。前提是所有复杂策略都要试过才知道。

- ## LangChain开源了AnythingLLM：可以与任何内容聊天的私人 ChatGPT，应该就是他们自己文档系统用的那一套。
- https://twitter.com/op7418/status/1733893368974073873
  - An efficient, customizable, and open-source enterprise-ready document chatbot solution.
  - https://github.com/Mintplex-Labs/anything-llm /MIT/js/python

- 有没有详细说明？最大可以支撑多大的文档？
  - 应该是不限大小的，拆开就好了
- 说没说硬件需求？

- ## 大模型的这些 benchmark 应该是全宇宙最没用的 benchmark 了吧？
- https://twitter.com/yihong0618/status/1721401347533324688
- 也不是全没用，也有一些有用的, 尤其细分任务上的，还是挺有用的。当前相比其他benchmark，可操作空间确实大
- 公开的只能全看自觉

- ## 中文开源模型虽多，数据集却很少开源。
- https://twitter.com/9hills/status/1718828132046942218
  - 目前英文 7B 规模的 SOTA 模型是 zephyr-7b-beta。它放弃了质量参差不齐的开源数据集，使用ChatGPT和GPT-4 全新标注了 UltraChat 和 UltraFeedback 数据集（已开源）。是 llama-index 项目实测出来唯一能够支持 Agent 的小参数模型。
- 中文数据集都是拿来卖钱的
