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

- ## 

- ## 

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

- ## Hugging Face 宣布投入 1000 万美元用于免费共享 GPU，旨在帮助小型开发者、学术界和初创公司开发新的 AI 技术，抗衡 AI 进步的集中化。
- https://x.com/glow1n/status/1791488036259434749
  - CEO Clem Delangue 表示，这一举措将通过 ZeroGPU 计划实现，促进 AI 技术的去中心化发展
  - ZeroGPU 使用 Nvidia A100 GPU 设备，提供高效的计算资源。
  - Hugging Face 的 Spaces 平台已有超过 30 万个 AI 演示。

- ## Cloudflare 的 Workers AI 每天可以免费使用 10, 000 Neurons（相当于生成100-200个LLM响应，500次翻译，500秒的语音转文字音频） ，调用方式兼容 OpenAI 
- https://x.com/scomper/status/1791804644332908646
- 好像都是小模型为主吧

# discuss
- ## 

- ## 

- ## 

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
