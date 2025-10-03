---
title: lib-ai-ml-dl
tags: [ai, deep-learning, machine-learning]
created: 2023-03-21T07:53:37.428Z
modified: 2023-03-21T07:54:11.468Z
---

# lib-ai-ml-dl

# guide

- dev-xp
  - 处理数据和提取特征要花费大量精力
  - 结果的可解释性不高，调参原理和可复现性经常出现问题
  - 数据样本和计算资源壁垒很高、成本很高
  - 传统算法也可以解决分类和回归问题

- ai-use-case
  - chat and answer
  - summarization
  - translation
  - text generation

- tips
  - 数据样本，大量
  - 计算资源，GPU、集群
  - 业务变化快，可能还没训练出来就换了方向
  - 传统模型和算法效果如何，是否只是锦上添花
# resources
- [动手实战人工智能 Hands-on AI — 动手实战人工智能 Hands-on AI](https://ai.huhuhang.com/intro)
  - 从监督学习开始，带你入门机器学习和深度学习
  - 尝试剖析和推导每一个基础算法的原理，将数学过程写出来，同时基于 Python 代码对公式进行实现
  - Jupyter Notebook 能够将文字和代码结合在一起，方便阅读和理解
# discuss
- ## 

- ## 

- ## 

- ## 

- ## 

- ## [The most important AI paper of the decade. No debate : r/LocalLLaMA](https://www.reddit.com/r/LocalLLaMA/comments/1nwx1rx/the_most_important_ai_paper_of_the_decade_no/)
  - Attention is all you need
- I think "Attention is all you Need" be at the top. It gave birth to the transformer.

- Pretty much so as of now. But please don‘t forget „Efficient Estimation of Word Representations in Vector Space“, Mikolov et al. (2013). It‘s the „Word2Vec“ paper.

- Not of the 2010 decade, maybe of the 2015-2025 decade? In 2010-2019, it was almost certainly AlexNet. Without it, and its usage of GPUs (2x GTX580), neural nets wouldn't even be a thing, and Nvidia would probably still be in the billions club.

- ## When evaluating the performance of Time Series forecasting models, several metrics can be used to assess their accuracy and predictive power.
- https://twitter.com/daansan_ml/status/1718575478276239512
  - Here are 4️⃣ of the most used metrics for time series forecasting
  - 1️⃣ Mean Absolute Error (MAE)
  - 2️⃣ Mean Squared Error (MSE)
  - 3️⃣ Root Mean Squared Error (RMSE)
  - 4️⃣ Mean Absolute Percentage Error (MAPE)

- ## 在机器学习领域，过度拟合（或称过拟合、过配，英文：overfitting）是指机器学习算法模型在训练集上的误差和测试集上的误差之间差异过大。
- https://twitter.com/erchenlu1/status/1681860160711712768
  - 而在投资交易层面，当构建量化交易模型时，使用过多的参数或复杂的算法，可能导致模型在历史数据上表现良好，但在实际市场中却表现不佳。
  - 这是因为过度拟合的模型过于贴合历史数据的特征，而忽略了未来市场的不确定性和变化，尤其是许多无法被量化的科技革新和社会发展变化趋势。

- ## [机器学习，深度学习，神经网络，深度神经网络之间有何区别？ - 知乎](https://www.zhihu.com/question/50191791)
- 机器学习是很多种方法和模型的总称。
  - 神经网络是一种机器学习模型，可以说是目前最火的一种。
  - 深度神经网络就是层数比较多的神经网络。
  - 深度学习就是使用了深度神经网络的机器学习。

- ## [什么是超参数？ - 知乎](https://zhuanlan.zhihu.com/p/78137628)
  - `超参数` = 在开始机器学习之前，就人为设置好的参数。
  - `模型参数` = 通过训练得到的参数数据。
  - 超参数也是一种参数，它具有参数的特性，比如未知，也就是它不是一个已知常量。是一种手工可配置的设置，需要为它根据已有或现有的经验，指定“正确”的值，也就是人为为它设定一个值，它不是通过系统学习得到的。
  - 超参数的一些示例：

    1. 聚类中类的个数
    2. 话题模型中话题的数量
    3. 模型的学习率
    4. 深层神经网络隐藏层数
    5. 树的数量或树的深度
    6. 矩阵分解中潜在因素的数量
    7. k均值聚类中的簇数
