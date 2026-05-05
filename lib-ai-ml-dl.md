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
# discuss-toolchain-ml
- ## 

- ## 

- ## 

- ## [Hugging Face launches a new repo type: Kernels : r/LocalLLaMA _202604](https://www.reddit.com/r/LocalLLaMA/comments/1sgq6h9/hugging_face_launches_a_new_repo_type_kernels/)
- I don't know any backends with plainly swap-able kernels.
  - Transformers does it exactly, see https://huggingface.co/docs/transformers/en/kernel_doc/loading_kernels

- Predictable, but I won't be hyped about another label for simple universal data storage.
  - That's just github releases page but stored on AWS S3 instead of Azure.
  - I hope they'll follow through and add integrations with pip and community projects.
- It's more than universal data storage. It works closely with transformers. Transformers practically defines the interfaces of some commonly used operators such as attention and MoE, and now we can easily download kernels that implement these interfaces, such as FlashAttention and SageAttention.
# discuss-ml-fwk
- ## 

- ## 

- ## 

- ## 

- ## [TensorFlow、Pytorch、OneFlow，MXNet、MindSpore这些框架谁最好用？ - 知乎 _202102](https://www.zhihu.com/question/446540609)
- Tensorflow：适用工业界部署，持续演化、受众最广的开发框架
- PyTorch：轻量灵活易上手，用户爽才是真的爽
- MXNet：优化云端分布式部署，利好AWS生态参与者
- CNTK：微软风的“傻瓜式”深度学习框架
- MindSpore：软硬结合，MindSpore+昇腾，构建最优全栈方案体系

- 等你debug到哭的时候，等你在google上搜索bug information发现一个答案都没有的时候，等你为了实现一个简单的常见的功能而耗费了两个小时的时候，你就会知道自己当初选择了一个社区差甚至没有社区的框架是多裂开的一件事情。你可以在tf或torch成熟的框架和强大的社区下实现自己想要的定制化功能，在这上面花费的时间远小于你去看一些小众的仅在某些功能上突出的框架的源代码要省事儿的多。

- TF 像 C++，诞生在一批技术很强的人手里，但是不懂用户需求，被用户用脚投票。TF 2.0 开始痛定思痛（这点也和 C++ 很像），着力改善用户体验，但是相比 PyTorch 还是更傲娇一点，不会完全迎合用户
  - PyTorch 像 Javascript，是一个 made by researcher for researcher 的框架，但是早期开发者的 PL & system 功底不足留了坑，不过随后不少大佬加入之后补上了短板，现在整个项目可以说是蒸蒸日上，其他框架基本没有正面竞争的机会。
  - PaddlePaddle 和 MindSpore 像低配版的 TF，更准确地说百度和华为像低配版的 Google，但是他们和 TF / Google 有一个根本不同是 PaddlePaddle 和 MindSpore 是行政主导开发的框架，这使得他们天生就有极大的劣势，要竞争过 TF 都不乐观，更不用说 PyTorch 了。

- 

# discuss-ai-changelog
- ## 

- ## 

- ## 

- ## 

- ## 其实人工智能也是1992前后的热点。 人工神经网络，主要是BP 神经网络，在80年代末，90年代初也是热火朝天。
- https://x.com/mtrainier2020/status/2051018287988039978
  - 甚至当时的日本还设计了专门的BP神经网络的芯片，ASIC。 但是很快发现BP神经网络有很多的局限性。比如容易过拟合，可推广性差，然后就寂静了。 
  - 再往后火过一波，SVM，支撑矢量机。 模式识别领域一直在往前发展。只不过大家谁也没有想到，NLP领域的突破，最后能吃掉一切。
- NLP 吃掉一切 不算偶然。Transformer、数据规模、算力规模 三 都到位 后解锁。BP 缺数据和算力, SVM 缺泛化突破。多因素 同时到位 解锁突破 更普遍。

- NLP之前10年就已经是神经网络的天下了。主要是图像方面的最为突出。

- 神经网络数学上完全没有优美性可言，跟svm比差远了，再加上参数太多不好train, 所以得等到硬件发展到一定程度才等到机会爆发

- 科技的热点跟流星服饰一样，多少年就重复一次。这也跟王兴说创业的一个方法，每隔十年左右就用新技术解决几十年的问题，看能否成功，成功了，可能就是新的创业模式
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
