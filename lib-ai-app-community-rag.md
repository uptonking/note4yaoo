---
title: lib-ai-app-community-rag
tags: [ai, community, rag]
created: 2024-09-08T20:08:04.573Z
modified: 2024-09-08T20:08:16.088Z
---

# lib-ai-app-community-rag

# guide

- usecases-rag
  - long-docs/pdf
  - chat-history
  - rag的实现还可以参考ai-coding中的实践和模式
  - 针对表格excel/脑图的rag
  - ⏳ 多版本文件的rag
# discuss-stars
- ## 

- ## 

- ## 🤔 [RAG（检索增强生成）会不会消亡呢？一旦大模型的Context Length变大，RAG还有存活的必要吗？ - 知乎](https://www.zhihu.com/question/637421964)
- RAG 的基本原理并不复杂：
  1.  将长文档切分成多个 **chunk**；  
  2.  通过向量化模型（如 [OpenAI Embeddings] 、Sentence-Transformer）为每个 chunk 生成向量，并存入数据库；  
  3.  在用户提问时，检索出 **Top-K 相似文档**；  
  4.  把这些文档与问题一起输入大模型，作为额外上下文；  
  5.  大模型基于问题 + 检索结果，生成更准确的回答。
- 简单来说，RAG 就像是给大模型装上了一个“外挂搜索引擎”。
  - 相比之下，传统的 微调（Fine-tuning） 方式虽然能把新知识写进模型，但往往成本高昂、不可逆，还可能“牺牲”原有能力。而 RAG 的优势在于：轻量、灵活、随取随用
- 目前大多数 RAG 系统其实是“Frozen RAG”——Retriever 与 LLM 是分开的，Retriever 固定不变，LLM 也不更新。它们拼在一起能跑，但模块之间并没有深度协同。
- RAG 2.0 的核心目标就是： 让检索器和生成器成为一个“可共同训练”的整体，从而达到端到端的优化。

- 从纯业务端的角度来说，不但不会消亡，还有可能在未来的3-5年里大行其道。
  - 表面原因非常简单：RAG几乎是目前唯一一种兼具门槛低+可观察+控制准+见效快的路线。
  - 最后提一嘴深层原因：RAG的技术路线极其符合国情，其本质是真理灌顶且可以随时替换，比大炼模型得到的醉拳幻觉可控得多。
  - To B和To G都是数据密集型对象，自身数据就是最大的筹码，不要指望人家会把身家性命交到AI厂商手里，去打造一个遥遥领先的大模型。
- 大模型目前没看到企业内好的落地场景。rag大部分是用于知识库，但是也就基本能用，如果提问不能从关键词和向量上匹配，那你给大模型的内容就和问题无关，自然答案就不对。并且文档拆分后，逻辑上就被拆分了，很多问题是要从各个文档逻辑上分析，不是简单的检索。

- 回顾下当前市场上企业 RAG 知识库落地的三种主流路径。
- 直接使用高层级开源框架
  - 这类框架如 RAGFlow, Dify, FastGPT 等，主要特点是提供相对完整、开箱即用的 RAG 工作流，
  - 目标是简化 RAG 应用的搭建过程，降低开发门槛。
  - 反之，劣势主要是定制化和灵活性受限，深度优化和集成特定组件时复杂度较高。
- 底层开发框架自主开发
  - 这类框架包括 LangChain, LlamaIndex, Haystack 等，都提供了一系列模块化的构建块、工具和接口。开发者可以根据需求灵活组合和编排 RAG 流程的各个环节（如数据加载、文本分割、嵌入、向量存储、检索策略、LLM 调用、记忆管理、Agent 构建等）。
  - 优势很明显就是灵度灵活，定制化能力强，能够针对特定业务场景进行深度优化和集成。适合对 RAG 流程有精细化控制需求的企业。
  - 反之劣势就是需要更多的开发工作量和技术深度。
- 云厂商 MaaS 平台方案
  - 如阿里云百炼, 百度智能云千帆, AWS Bedrock, Google Vertex AI Search 等的私有化部署方案，无论是国内还是国外的这些云服务商，都是把 RAG 相关的能力封装成服务或提供私有化部署包，通常与自家的大模型、计算资源、数据存储等深度集成。一般也会提供模型选择、微调、部署、监控等一站式服务。
  - 采用这种方案通常能提供稳定的基础设施、便捷的模型管理和部署、以及与其他云服务的良好兼容性。对于已经深度使用特定云生态的企业来说，集成成本较低。
  - 但劣势就如同使用大模型一体机一样，可能存在厂商锁定的风险，跨云迁移或集成非该厂商的服务可能会比较复杂。
  - 当然，费用和灵活性也需要考虑。
- 总结来说，实际生产场景中以上三种选择并非完全互斥，例如以底层框架为基础，但借助云厂商的部分模型服务或基础设施也是中目前常见的组合。

- RAG主要可以解决大模型幻觉问题，以及通过外挂知识，避免模型频繁进行知识更新
  - 即使模型可接受上下文长度为128k，但是我的知识库里有10w篇文档，远远超过模型的上下文长度，所以你还是需要检索。
  - 当然模型上下文长度变长，对于检索更加有好，粒度变大，召回变高，相辅相成。
  - 即使你可以接受128k的长度，但是你的设备消耗不起，更大的长度需要更多的显存，模型部署成本更高，速度更慢。
  - 如果你调用api，那token消耗也太大了，成本过高。

- Context Length 变大 ≠ 不需要 RAG
  - 成本问题: 上下文越长，推理成本（显存、时间、算力）会线性甚至超线性增加。 比如，100k tokens 处理一次就很烧钱，而 RAG 可以用较短上下文反复调用。
  - 信息检索效率: 如果你有 1TB 的知识库，把它全塞进上下文是不可能的。 RAG 先检索，再送进上下文，可以让模型专注于相关信息。
  - 噪音与干扰: 大上下文并不代表模型会忽略无关信息，相反太多无关内容会稀释关键信息，导致推理效果下降。RAG 的“检索+过滤”能提高信噪比。
- Context 变大后，RAG 的形态会演化
  - 从“查找资料”到“动态知识组织”: 未来的 RAG 可能不只是检索，而是自动生成一个临时的知识摘要/知识图谱再交给大模型
  - 多阶段推理（Multi-turn Reasoning）: 大上下文允许一次性放更多信息，但 RAG 可以在每一步推理时更新上下文，形成 交互式推理
  - Hybrid RAG（混合模式）: 把静态知识（常用信息）直接放在长上下文里，把动态数据（实时信息、搜索结果）用 RAG 方式插入。
- 为什么 RAG 在长上下文时代依然重要
  - 可更新性: 模型训练数据是静态的，RAG 可以在不重新训练的情况下引入最新知识。
  - 隐私与定制化: 私有企业或个人数据不会直接放到大模型里，而是通过 RAG 动态注入。
  - 减少幻觉: 模型直接引用检索到的原文，可以显著降低胡编乱造的概率。
  - 多模态检索: RAG 未来会不仅是文本，还会检索图片、视频、音频、结构化数据，再统一给大模型处理
- 未来 RAG 的重点会从“找文档”变成“构建最优推理上下文”，它会变得更智能、更动态。
  - 随着 Context > 1M tokens，部分场景可直接用大模型的长记忆，但 RAG 会演变为“智能知识编排器”。
  - 如果出现无限上下文且推理成本极低的模型，RAG 会退化成“数据索引工具”，主要用于加速数据组织而不是必须步骤。

- 不会。上下文长度变长只会让RAG更好用。从目前的情况来看，RAG的成本依旧低于微调，效果高于微调。然后目前llm应用的本质还是prompt，没有什么大花样，也脱离不了现有的人类学科。
  - 当然，如果有人强行说RAG就是用嵌入向量什么的，那么我只能说可能会消亡。retrieval 肯定是包括了其他方式的，我们用gemini发文件或者图片给他何尝不是一种RAG呢，不过只是人脑驱动罢了

- ## RAG is anti pattern.
- https://x.com/pelaseyed/status/1882471632129994914
  - I don’t do RAG anymore, get 10x the result just spinning up a pipeline and feed all content to Deepseek. And yes it scales to over 10K docs. 

- And you can cache it, so doesn’t even cost that much

- Does deepseek have caching like Google’s media.upload? How do you otherwise avoid rebuilding the context all the time (I’ve not used the DS APIs).

- I wish I could fit the entire Internet in the prompt for @ask_pandi but it doesn't fit. RAG is still needed for this.
  - Run multiple LLMs in parallell, you will have infinite context window.

- You put everything into context?
  - Everything in context(s)

- RAG is A pattern, just not useful when your context is under 128k token and when the context is known. Pick the right tool for the job.
# discuss-solutions
- ## 

- ## 有没有想过将自己的代码库打包然后直接塞给大语言模型来处理？也许你会想到用RAG或者用windsurf或cursor。现在有了更简单的办法——Repomix
- https://x.com/karminski3/status/1881150047276138689
  - 这个库可将整个存储库打包到一个 AI 友好的文件中，方便给大语言模型使用。

- ## 📌 A list of software that allows searching the web with the assistance of AI.
- https://x.com/tom_doerr/status/1856778512612667838

# discuss
- ## 

- ## 

- ## 

- ## LobeChat v1.85.0 优化了对话上传文件的逻辑，把大家呼声比较高的全文上传的能力做好了，不再走 分块 + embedding 的朴素 RAG 。带来的好处是速度变快了，效果也更加理想了。
- https://x.com/arvin17x/status/1921101310004179082
  - 感觉大模型再迭代个一年，朴素 RAG 可能就要退出历史舞台了
  - 比如一个文件 10w 字的内容，全文上传就是10w字全放上下文里。 RAG 是找出最相关的 N 个内容片段（假设一个片段1k，加起来 N k个字）放上下文里。 全文上传的效果在大多数情况下一定是比 RAG 要好的。
  - 现在默认上传就是全文。不过知识库读取还是原来的
- 不用 RAG，直接传给 LLM，钱包顶不住啊
- 全文上传，只有Google家才有很大的上下文吧？其他家效果就不好了
  - 不啊，现在gpt4.1mini都有1M上下文了，也便宜。测下来效果非常好

- ## 开源的 llm 系统里，带知识库功能的，目前还没找到一个做的好的。
- https://x.com/wwwgoubuli/status/1830227047173751206
  - 不过这么说倒也不是要贬低什么，我自己帮客户定制过的知识库中，做的稍微好一点的，也投入了大量的精力和成本来实现数据预处理，单单一个文本分段都找不到通用范式，得大量定制。

- 问题就是 to b 里。 to c 那一个用户丢个 pdf 算不上什么知识库。 到了 to b  领域，你看着一堆 excel ，pdf， 你的梦魇才刚开始

- 我们自己做售后客服机器人，起步是找实习生撸了1万条问答对，上线后每周根据bad case迭代继续做数据。这玩意效果就是看标注数据，想要好的效果，就好好做数据。

- 知识库如果像编程语法手册一样，那rag效果会非常好，如果像散文诗，rag效果就会很差。我们拿到手的文档一般介于两者之间，所以想提高rag效果，只好把文档本身往编程语法手册方向改

- 我现在最头疼的是pdf文档，里面全是图片的那种。，
  - 让甲方加钱，图片到文字的转换不仅需要工具，还需要人工审阅，不加钱没法干
