---
title: lib-ai-app-community-chat-conversation
tags: [ai, chatgpt, community, conversation]
created: 2023-04-16T10:02:33.647Z
modified: 2023-04-16T10:02:58.738Z
---

# lib-ai-app-community-chat-conversation

# guide

# discuss-stars
- AutoGPT现在超火，它是一个由开发者 Significant Gravitas 推出的项目，​可以根据用户设置的目标，​使用 GPT-4 自动帮助完成任务。
- https://twitter.com/duanzi/status/1647284362541662213
  - ​用户只需提供 OpenAI 的 API Key，​AutoGPT 就可以根据用户设定的目标，​采用Google搜索、​浏览网站、​执行脚本等方式帮助用户完成目标
  - utoGPT 最大的特点是突破了现有的 GPT 只能做文本方面的任务的限制，​可以利用各种工具来完成目标。​AutoGPT 背后接入的语言模型可以是 GPT-4 或 GPT-3.5 的 text-davinci-003。​作者的聪明之处在于将各种操作变成命令，​让 GPT-4 模型选择，​然后根据返回的结果进行操作
  - AutoGPT 使用了一些技巧确保任务完成地更加有效，​如使用列表保存历史发送的信息，​并在每一次请求token 允许的条件下发送最多的历史消息给 GPT-4。​AutoGPT 有很多用例，​早期用户已经能够使用它来做各种各样的事情，​包括通过手机生成软件代码和为网站生成 SEO 审计。​它还可以用作互联网搜索和规划
  - AutoGPT 可以完成的任务或者决策比 HuggingGPT 更强。​要运行AutoGPT，​用户需要 Python 3.8 或更高版本、​一个 OpenAI API 密钥和一个 PINECONE API 密钥。

- AutoGPT 的 GitHub 星标超过了 Bitcoin，只用了16天。 最简单的理解它的方式就是把AI当人了。 人最厉害的是什么？使用各种工具。 怎么使用工具？让LLM来当总指挥调用其他的API工具。 在哪儿找到工具？HuggingFace 不是有一堆模型吗。

- ## One of the biggest weaknesses of ChatGPT/LLMs is that it just tells you stuff but doesn't actually *do* anything.
- https://twitter.com/DavidKPiano/status/1636020080826896389
  - So the only jobs it will be able to replace are the majority of management jobs.

- ## 多轮问答跑了一天，目前效果很稳定，可以来解释一下是如何实现的了。
- https://twitter.com/xicilion/status/1647408696312602624
  - 问答通常的实现，embedding -> search -> llm，连续语义在第一步就丢失了。
  - 我的方案是在前面，**先让 ChatGPT 解释问题，返回关键词**，流程变为：explain -> embedding -> search -> llm。
- 两次 llm 会不会慢了点
  - 第一次几乎不推理，很快。
- 类似langchain conversational chain里面的CONDENSE_QUESTION_PROMPT，让llm先对用户的提问结合历史进行重新的阐述，从而提高搜索命中率
  - 去看了一下，确实很
- 感觉还是用llm转述问题会更好些，关键词任然会丢失语义，比如用户问一个没有关键词的问题。
  - 我对比了一下，效果一样。没有关键词也不会迷失，ChatGPT 会按照要求根据上下文补齐。
- 很好的思路，本质上就是通过对每句话进行句子表述上的补全，让每句话都是独立且完整的表述，保证了能进行可靠的向量搜索
- plugins 的思路也类似这样
# discuss
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

- ## 文本模型爆发比图像晚了大约半年，所以那边发生的事情这边貌似在重新发生一次…从那边可以知道的经验至少是：prompt不会成为壁垒
- https://twitter.com/virushuo/status/1632405930015899648
- 开源模型会大力度搅局。 一部分人疯狂 hack 只是为了好玩，另一部分疯狂想着快速收割韭菜。 
  - 闭源有点自研的AI商业应用的生命周期可能只有几个月。API套壳的更可能是以周计算的。更别说 prompt 了。
- 对于我来说，壁垒是算力，毕竟图像要本地计算足够才好玩
- 那什么是壁垒？还是数据？

- ## 搜索引擎的范式转移 PageRank -> ModelRank
- https://twitter.com/Tisoga/status/1623916651996680193
- 对话式 AI 目前最显著的一个问题就是没有信息引用来源，这有很大的安全隐患！大规模语言模型并没有像人类大脑这样创造知识结构，而是训练数据源的神经网络权重，虽然提升参数规模可以神奇的产生语言逻辑的抽象概括能力，但这毕竟不是通用智能
