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

# discuss
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
