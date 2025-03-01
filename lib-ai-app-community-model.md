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

# discuss-llama
- ## 

- ## 

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

2. MinerU
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

3. Docling
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

4. Markitdown
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

5. Llamaparse
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

# discuss-workflow-ai
- ## 

- ## 工作流平台大家关注dify 和 coze比较多，还有一个非常不错的框架 langflow
- https://x.com/leeoxiang/status/1884945535507083426
  - 1、Flow as an API，代码优先，workflow可以直接转换为可执行的代码；
  - 2、支持丰富的逻辑判断；

- ## 又一个值得学习的爬虫&RPA开源库 Maxun
- https://x.com/yan5xu/status/1881150511220752884
  - 自带低代码后台，轻松抓取任何网页数据，自动提取整理成表格，还能处理滚动分页和验证码
  - 核心用 Playwright 做浏览器自动化，配合 puppeteer-extra-plugin-stealth/recaptcha 插件处理反爬和验证码，再用 adblocker 清理广告干扰

- ## Announcing Flows AI: A light-weight library to build agent workflows, on top of Vercel AI SDK.
- https://x.com/grabbou/status/1882139484994551861
  - Use any LLM and provider of your choice.
  - All patterns from Anthropic article provided out of the box.
  -  we have a branch open and POC of a builder project, where we want to provide a very light-weight flow-based UI for configuring and visualizing this. Standalone and CLI-like, so you can execute those workflows like JavaScript files
- There’s more than on the screenshot, including routers etc. Error handling can be done with a custom agent, overall - very simple, although I am interested to implement the missing blocks!

- No unnecessary abstractions whilst literally abstracting away the AI SDK 

- Is it capable of passing and using structured outputs and objects ?
  - Agent is a function, so simply use generate object inside. The helpers we provide operate on text for now (keeping things slim), but adding that if requested isn’t too much of work

- Does it support streaming?
  - Not yet, keeping scope limited. Theoretically possible
# discuss-multi-agents
- ## 

- ## 

- ## 

- ## 

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
