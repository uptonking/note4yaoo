---
title: lib-ai-app-community
tags: [ai, community]
created: 2023-02-08T06:56:25.811Z
modified: 2023-02-08T06:56:54.945Z
---

# lib-ai-app-community

# guide

# discuss
- ## 

- ## 

- ## 

- ## 

- ## 其实之前不仅仅关注LLaMA生态的一些开源大模型，国内的一些开源大模型也在关注，这里分享几个最近挺火的LLM。
- https://twitter.com/xinqiu_bot/status/1645616019103428609
- https://github.com/THUDM/ChatGLM-6B
  - 开源的、支持中英双语的对话语言模型，基于 General Language Model (GLM) 架构，具有 62 亿参数。
  - 结合模型量化技术，用户可以在消费级的显卡上进行本地部署（INT4 量化级别下最低只需 6GB 显存）
- 除了基于GLM的ChatGLM，另一种基于RNN的ChatRWKV

- ## Is it fair to think of LLMs as a database with a natural language query interface? Where does the database metaphor break?
- https://twitter.com/dvassallo/status/1644914034905579526
- The most interesting counter-argument is that LLMs seem to be practically **👀 read only**. There’s only short-term memory (so far), and no insert/update equivalent.
  - The rest still seems to stand. There’s data, a query, and a result derived from the data and the query algorithm.
- LLMs create data in response to queries, unlike traditional databases which simply retrieve data.

- ## AskBend 所有训练数据都是英文的文档，但是它可以非常自然的使用中文来回答。有没有朋友科普一下为什么🥵，不同的语言输入对于 embedding 的计算没有影响吗？
- https://twitter.com/redsun_diamond/status/1643904510883135490
- 没影响，因为是基于语意的不是基于语言的。【virtual thread】和【虚拟线程】 这个两个词的embedding差不多，余弦90%的样子。
- 没影响，中英文embedding后在同一个vector space
- 多语言的embedding模型是相互关联的。比如中文的我有一个苹果和i have an apple的embedding的相似度数值是很高的
- 因为第一层和最后一层都走的 openai, embed 走的是 open ai 的 text-embedding-ada-002 返回数据库查找是根据你的语言返回 vector 而这个 vector 的拿回的 text 也是用来问 openai 的。所以语言在这里相当于走的 openai 的 embed 猜测不同语言在 vector 里算 distance 是有差异但不是那么大的。
- 要分开来看，普通句子的差别不大的。但是一些复杂场景下的中文预料就不一样了。比如，你见到一个仇人，你问她，你吃了吧？跟你见到一个你喜欢的人，你问她，你吃了吧？所以还是要用针对性的语料进行训练吧。然后大模型神经网络本身也很容易一通百变的，到输出的时候只是组合单词

- ## One of the biggest weaknesses of ChatGPT/LLMs is that it just tells you stuff but doesn't actually *do* anything.
- https://twitter.com/DavidKPiano/status/1636020080826896389
  - So the only jobs it will be able to replace are the majority of management jobs.

- ## 文本模型爆发比图像晚了大约半年，所以那边发生的事情这边貌似在重新发生一次…从那边可以知道的经验至少是：prompt不会成为壁垒
- https://twitter.com/virushuo/status/1632405930015899648
- 开源模型会大力度搅局。 一部分人疯狂 hack 只是为了好玩，另一部分疯狂想着快速收割韭菜。 
  - 闭源有点自研的AI商业应用的生命周期可能只有几个月。API套壳的更可能是以周计算的。更别说 prompt 了。
- 对于我来说，壁垒是算力，毕竟图像要本地计算足够才好玩
- 那什么是壁垒？还是数据？

- ## 搜索引擎的范式转移 PageRank -> ModelRank
- https://twitter.com/Tisoga/status/1623916651996680193
- 对话式 AI 目前最显著的一个问题就是没有信息引用来源，这有很大的安全隐患！大规模语言模型并没有像人类大脑这样创造知识结构，而是训练数据源的神经网络权重，虽然提升参数规模可以神奇的产生语言逻辑的抽象概括能力，但这毕竟不是通用智能

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
