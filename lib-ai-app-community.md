---
title: lib-ai-app-community
tags: [ai, community]
created: 2023-02-08T06:56:25.811Z
modified: 2023-02-08T06:56:54.945Z
---

# lib-ai-app-community

# guide

# discuss-stars
- ## 

- ## 

- ## 

- ## [怎么很多人都知道chatgpt ，而不知道Stable Diffusion ？ - 知乎](https://www.zhihu.com/question/637073586)
- chatGPT的使用难度几乎为0，因为它就是个对话窗口，只要认字的都可以无障碍使用。
  - sd需要学习什么是prompt, VAE，control net, 以及其他乱七八糟的参数
- SD需要 
  - 一台配置有高性能显卡的电脑（否则只能租用云平台了，也是不便宜的） 
  - 知道如何安装和配置SD和SD对应的web ui
  - 知道SD里各种参数，大模型和laro模型的区别等等 
  - 如何收集素材，训练自己的模型等等

- ## 一个很奇怪的现象: AI 公司既然都有安卓和客户端那就说明他们内部肯定是有对应的 SDK/Library, 但是他们开源的基本上是 Node 和 Python SDK和 REST API, 为什么呢?
- https://x.com/ivyliner/status/1892808355183218914
- ChatGPT的客户端也不是拿着API key请求服务器端的，有中间层
- sdk 只是简化了接入方式。
- 对外放出的东西肯定要考虑标准化，保有量最大的也就是基于 Node 和 Python 的 rest api
  - 内部互相调用不见得用一样的接口，说不定是 rpc

- 为了避免潜在的竞争对手分流吧？毕竟app是主要的订阅盈利渠道。

- 因为都是兼容openai接口。

- ## Is there appetite for learning about the AI architecture we built for @getwebstudio ?
- https://twitter.com/oleg008/status/1715013865644101992
- What we solved so far:
  1. Multi-model interface
  2. Serialization/deserialization of messages (jsx/Tailwind)
  3. Streaming
  4. Chaining
  5. Operations
  6. Structured data

# discuss-cv
- ## 

- ## 

- ## 

- ## 大家做CV一般怎么读入图片的？譬如像FFHQ和ImageNet这样的超大数据集。感觉V100/A100这样有I/O瓶颈。。。
- https://twitter.com/JXQNHZr1yUAj5Be/status/1786553056273768723
- 各个dataloader不是有现成的机制，一个prefetch基本解决了。imagenet也不咋大啊…
  - prefetch没解决啊，CPU做图片解码和编码赶不上V100/A100过模型的速度，我自己测过torch dataloader，num_worker和prefetch，效果都不行。
- 可以简单看一下tensorflow的dataloader的机制。就是先把数据处理完。你搞一个生产消费模型用消息队列供应量也行，生产端加特效。

- 对于硬盘到内存，存数据用 webdataset 或者 h5py，充分利用顺序读写优势
  - 对于内存到显存，直接传uint8 tensor到gpu，再在gpu做augmentation
  - 内存够大建议放数据集到shm或者设计一个shared memory，把整个或者部分数据集放进去。

- 把jpg数据直接load到dynamic memory，然后硬件解码到gpu memory，一个producer，consumer队列，jpg解码和gpu独立开来
# discuss-ml-algorithms
- ## 

- ## K-Nearest Neighbours (KNN), implemented from scratch in Python:
- https://x.com/Sumanth_077/status/1809228777748418809

# discuss-ai-dev-pattern
- ## 

- ## 

- ## What are we doing right and wrong with @pydantic AI to have such a wildly different downloads/stars ratio compared to other Agent Frameworks released around the same time
- https://x.com/samuel_colvin/status/1904657385769046046
- Perhaps they market their repo better? Huggingface had 100K signups for their agents course where they might have asked explicitly for a star or two

- ## 有个习惯是有了 AI 之后我才改过来的。现在在 AI 提示下我会把敏感信息操作和普通信息操作完全隔离开来
- https://x.com/wwwyesterday/status/1892560418968654100
  - 哪怕因此表面看起来会产生些许冗余，比如我会在 models 层出现两个甚至更多的 update 方法。
  - 我现在会尽量从类型/结构定义开始就明确拆分并隔离好操作。
  - 有趣的是，在我以前的经验中，我从别人那学到很多东西，但就是没学到这一点，敏感操作和非敏感操作的完全隔离——尽管实践中大家会有意识在业务层也做好隔离。

- 现在不知道best practice的时候就会问llm，缩小范围
# discuss-ai-usage-tips
- ## 

- ## 之前发现当 Cursor 实在解决不了问题的时候，添加日志会有帮助。今天发现一个增强版 Prompt：
- https://x.com/beihuo/status/1901377491597680646
  - “思考并分析 5-7 种可能的问题来源，将其归纳为 1-2 个最可能的原因，然后添加日志来验证你的假设，在我们开始实际的代码修复之前先进行确认。”

- 我一直都会给这样的提示，让他用批判性思维自我反省, 还有让它给我按照逻辑解释（什么反向小黄鸭调试法），对于找逻辑错误还是很有用的

- ## 用 提示词：“summarize your tool in a markdown table with availability” 让 4o 列出它所能使用的工具就能检测出来了。
- https://x.com/tshenmin/status/1890675456271077584
- 我分别在网页版和 macOS 客户端上进行了测试，结果却不一样
  - 降智是和客户端有关联的，一般网页端比较容易被触发
- 所以我现在用tailscale，直接从家里的电脑出去。

- ## We’ve been working on an “ai module” for the tldraw SDK. It’s meant to help developers:
- https://x.com/steveruizok/status/1891426822883000335
  - get data out of the tldraw editor
  - generate instructions with an LLM
  - execute instructions in the editor
  - There’s a lot you can do with this pattern. Autocomplete, prompt-driven design, turn taking games, annotation, ai-guided sessions, or full on collaboration with an AI

- ## Namecheap 提醒我域名快到期了，续费价格 $17.16, 问以下 Grok 3 找一下 Promo Code 给我一个 SPSCOMTR, 最终转入价格是 $8.17, 省好多
- https://x.com/xinzhi/status/1892464984799527044
- 只要cloudflare卖的（有些域名它不支持），在cloudflare续费域名基本上是最便宜的
- 其实Namecheap和Spaceship是一家

- ## DeepResearch/DeepSearch 这类工具对于散户投资者太有用了，原来要啃半天财报研报才能找到的一些数据，现在随便问一句就可以列的清清楚楚。
- https://x.com/Blankwonder/status/1892598619808673885
- 是这样的，现在用 @perplexity_ai 做投资分析简直开心到飞起来。但是也需要有些经验和意识去识别错误信息，AI 的幻觉还没有完全解决，刚才我在让 Perplexity 介绍一家公司的管理层的时候就完全搞错成另外一家公司了。
- 对回答的答案最好在检查一遍。
- deepseek就是炒股票的人写出来的。

# discuss-async/parallel
- ## 

- ## 

- ## 

- ## Headless @cursor_ai . Allow processes to be spawned via a CLI which take the way the existing chat works and lets you run it outside of the Cursor IDE.
- https://x.com/mattpocockuk/status/1918319619615670437
  - Should be able to transition from headless to headed to inspect running processes with Cursor.

- Wingman supports this via its language server ; ) it uses JSON Rpc to accept requests and respond.
# discuss
- ## 

- ## 

- ## 

- ## 

- ## databricks已经彻底疯了，不光搞AI函数，连整个transform都用提示词写了。
- https://twitter.com/niyue/status/1674557959094018049
  - [Introducing English as the New Programming Language for Apache Spark | Databricks Blog](https://www.databricks.com/blog/introducing-english-new-programming-language-apache-spark)
  - 原来我看MarvinAI搞AI函数说用在总结/定性分析/情感分析等这些不要求精准结果的领域，砖厂这搞法对AI可靠程度信心满满啊
- 看实际效果, 云厂选 Azure 相对稳一点.

- ## tensorflow.js 真是起了个大早，不知道能不能赶上晚集。
- https://twitter.com/xicilion/status/1647143660910436356
  - 它很早就支持 wasm 和 webgpu 后端，而且性能不错，灵活性也不错，但是这次 LLM 大火，却再也没看到它的身影。
  - PyTorch 想要跨界很难，反倒是 wonnx 这样的 rust 引擎，借着 wasm 和 webgpu，杀进浏览器。
- transformers.js 是另一个在浏览器内运行 transformers 的项目，它的推理引擎用的就是 onnx wasm 版。

- ## generative ai + types
- https://twitter.com/aaronsiim/status/1614123503925760001
• image-to-VR (I2vr)
• image-to-AR (I2ar)
• text-to-code (T2C)
• brain-to-text (B2T)
• text-to-video (T2V)
• text-to-video (T2V)
• blog-to-video (B2V)
• text-to-music (T2M)
• script-to-video (S2V)
• text-to-motion (T2Mo)
