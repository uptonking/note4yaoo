---
title: thread-pm-app-kickstarter-industry
tags: [industry, kickstarter, thread]
created: 2023-03-26T07:02:36.427Z
modified: 2023-03-26T07:02:48.021Z
---

# thread-pm-app-kickstarter-industry

# guide

# discuss
- ## 

- ## 

- ## 昨天跑通了类似 ChatPDF 的全离线方案，不用 ChatGPT（当然效果肯定会差一些），Embedding 使用 CoSENT 方案，内容总结生成回复使用 ChatGLM，效果很不错
- https://twitter.com/nash_su/status/1640541466761240576
  - 这样的好处是成本完全可控，并且支持私有化部署，准备在自己的客户业务上先测试下效果。
- 不知道博主是不是用的langchian，但是langchian 有文档解释自己host的各种东西。。强烈推荐langchian。
  - 没有用langchain，因为定制行很强，langchain很多功能没有
- 大佬  gpu 云服务有推荐的吗？
  - 国外就太多了，国内主流就那几个，小众青云不错
- 请问CoSENT句子embedding的效果和llama比怎么样？chatglm可以提取embedding吗？
  - 中文比llama效果好多了，chatglm还没官方embedding功能

- 一种流程
  1. 提取pdf内容，处理，清洗
  2. 对句子提取embedding存入向量数据库，并建立文档，段落到embedding的索引
  3. 输入问答，问答语句提取embedding和数据库做相似度检索
  4. 整理检索到的段落和句子进行加工，设计相关总结和提问的prompts
  5. 向chatglm提问，后处理结果返回
  - 简单的场景应该可以应付。。。。

- ## 红杉刚刚发布了AI时代的开发工具mapping，
- https://twitter.com/0xthefool/status/1639397499843792897
  - 将所有devtool根据使用场景分成了13个赛道，又根据产品的AI原生于创新程度分成了3代产品。
  - 就像我们会判断一个产品是不是crypto native那样，新时代产品也会被打上AI native的标签。
  - 传统巨头有场景有用户的优势但是船大难掉头，新玩家入场应该走一条AI原生但又能扎根行业应用场景的路。
  - [Developer Tools 2.0 | Sequoia Capital US/Europe](https://www.sequoiacap.com/article/ai-powered-developer-tools/)
- 中间这一列确实是对应左边这列的后起挑战者，但是要说对市场主体占有者的挑战，它们大多数都还处于八字没一撇的阶段。而且这些挑战大部分跟AI也没关系啊
  - 是的，大多数还没有adopt AI，前路还有一段时间
