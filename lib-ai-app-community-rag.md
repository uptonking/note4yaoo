---
title: lib-ai-app-community-rag
tags: [ai, community, rag]
created: 2024-09-08T20:08:04.573Z
modified: 2024-09-08T20:08:16.088Z
---

# lib-ai-app-community-rag

# guide

# discuss-stars
- ## 

- ## 

- ## 

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
