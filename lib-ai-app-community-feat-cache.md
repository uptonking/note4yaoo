---
title: lib-ai-app-community-feat-cache
tags: [ai, cache, kvcache, large-language-model]
created: 2026-06-24T16:51:39.677Z
modified: 2026-06-24T16:51:57.846Z
---

# lib-ai-app-community-feat-cache

# guide

# cache

## kvcache

- https://github.com/LMCache/LMCache /9.1kStar/apache2/202606/python
  - https://lmcache.ai/
  - A KV Cache Management Layer for Scalable LLM Inference
  - It turns KV cache from a temporary state into reusable AI-native knowledge that can be stored persistently, reused across multiple serving engines, monitored with an observability stack, and transformed for better generation quality. 
  - As a result, LMCache reduces TTFT (time-to-first-token) and improves throughput, especially for long-context agentic, multi-turn conversation, and knowledge-augmented workloads (e.g., RAG).
  - LMCache is vendor-neutral. allows users to freely switch between serving engines and storage vendors, while reusing the stored KV caches.
  - Pluggable storage and transport backends: CPU RAM, local disk (SSD), Redis/Valkey, Mooncake, InfiniStore, S3-compatible object storage, NIXL, and GDS.
  - LMCache, as a standalone daemon process, manages KV cache independently from the inference engine process, so that KV cache will not be lost even if the inference engine crashes (i.e., no fate-sharing with engines).
  - Persistent, tiered KV cache offloading and reuse: Move KV caches out of GPU memory into a tiered storage hierarchy spanning CPU memory, local storage, and remote backends
  - Pluggable KV transformation: A simple interface for researchers to write compression, token dropping, and custom serialization through a flexible SERDE interface.
  - LMCache provides a rich set of KV cache observability metrics, including typical Kubernetes metrics 
  - PD disaggregation and KV transfer: Support KV cache transfer from prefill workers to decode workers over NVLink, RDMA, or TCP through transport layers such as NIXL.
  - https://x.com/GitHub_Daily/status/2066030400087146655
    - 已加入 PyTorch 基金会生态，NVIDIA Dynamo 也集成了它。
# discuss-stars
- ## 

- ## 

- ## 

- ## 

- ## 🧩 KV Caching in LLMs
- https://x.com/servasyy_ai/status/2053664200971686356
  - 核心现象：你用 ChatGPT/Claude 的时候，第一个字出来特别慢，后面噼里啪啦就全出来了。原因是 KV Caching。
- 6个部分讲清楚了这个机制：

1. LLM 怎么生 token：Transformer 处理所有输入 token，每个产生一个 hidden state，但只有最后一个 token 的 hidden state 用来预测下一个词。前面的都是中间产物。

2. Attention 在算什么：每层里每个 token 有 Q、K、V 三个向量。要算最后一个 token 的输出，需要它的 Q × 所有 token 的 K 和 V。

3. 冗余在哪：生成第50个 token 要用 1-49 的 K、V；生成第51个又要用 1-50 的。1-49 的 K、V 根本没变，但模型每次从头重算。浪费 O(n²) 的计算。

4. 解决办法：把算过的 K、V 存起来（cache）。每步只算新 token 的 Q、K、V，然后把新的 K、V 追加到缓存里，attention 用新 Q 对完整缓存跑。这就是 KV Caching。

5. 为什么第一个字慢：你发 prompt 的时候，模型要一次性处理整个输入，算出所有 token 的 K、V 并缓存——这叫 prefill 阶段，是最吃算力的。缓存建好后，后续每个 token 只需一次单 token 前向传播。

6. 代价是显存：KV Cache 用计算换内存。以 Qwen 2.5 72B 为例，单请求的 KV Cache 可以吃掉好几 GB 显存。并发量一大，KV Cache 比模型权重本身还大。这就是为什么有 GQA/MQA（共享 key/value head 省显存）和 Paged Attention（高效管理 KV Cache 内存）。

所有主流推理框架（vLLM、TGI、TensorRT-LLM）都基于这个思路。

- 之前压测发现kv cache占显存比模型权重还凶，batch稍大就oom，最后靠分页+淘汰策略才稳住

- KV cache 这个解释里 prefill 那段是真瓶颈，长 context 下显存反而是次要的，第一个 token 出来前的延迟才是用户体感最难绷的环节，vLLM 那套 chunked prefill 就是把这一段拆出来缓解

- ### KV Caching in LLMs, Clearly Explained
- https://x.com/_avichawla/status/2034902650534187503
- tl; dr
  - KV caching eliminates redundant computation during autoregressive generation. Previous tokens always produce the same K and V vectors, so you compute them once and store them. Each new token only needs its own Q, K, and V. Then, attention runs against the full cache.
  - 5x speedup in practice. The cost is GPU memory, which becomes the binding constraint at scale. Every LLM serving stack (vLLM, TGI, TensorRT-LLM) builds on this idea.

- Before we get into the technical details, here's a side-by-side comparison of LLM inference with and without KV caching:
- Part 1: How LLMs generate tokens
- Part 2: What Attention actually computes
- Part 3: The redundancy involved
- Part 4: The fix
- Part 5: Time-to-First-Token
- Part 6: The Tradeoff

- 
- 
- 

# discuss-LMCache
- ## 

- ## 

- ## 

- ## 

- ## 

- ## We just published a starter guide for developing vLLM + LMCache on a MacBook.
- https://x.com/lmcache/status/2069513016174100663
  - LMCache's multi-platform design decouples the GPU from most core data paths, so a single laptop is enough to clone, build, run unit tests, and verify a real cache hit on CPU. 
  - [vLLM + LMCache: A Starter Guide, No GPU Required | LMCache Blog _202606](https://blog.lmcache.ai/en/2026/06/23/vllm-lmcache-a-starter-guide-no-gpu-required/)
  - [vLLM+LMCache 零 GPU 开发指南 | LMCache Blog _202606](https://blog.lmcache.ai/zh/2026/06/23/vllmlmcache-%e9%9b%b6-gpu-%e5%bc%80%e5%8f%91%e6%8c%87%e5%8d%97/)

# discuss-internals/arch
- ## 

- ## 

- ## 

- ## 

- ## [New KV-Cache quant method: 3-4x compression, 1.3x speedup in vLLM, full accuracy : r/LocalLLM _202606](https://www.reddit.com/r/LocalLLM/comments/1twlmj8/new_kvcache_quant_method_34x_compression_13x/?sort=top)
  - a new KV-Cache quantization method in vLLM (fork) by Huawei. It beats e.g. TurboQuant by a lot in accuracy and speed (and is even faster than the fp16 baseline). 

# discuss-ssd-cache
- ## 

- ## 

- ## 

- ## Offloading KV cache to NVMe SSDs wastes 70% of GPU cycles on stalls. 
- https://x.com/sakurayukiai/status/2069179520519717347
  - The bottleneck isn't SSD bandwidth, but the CPU choking on thousands of tiny I/Os for vLLM's fragmented pages. Tutti running io_uring directly on the GPU proves CPU-centric storage is the real bottleneck??
- Can you better manage the CPU bottleneck by writing your own I/O queues and adding a better scheduling policy? I've seen that work on the SSD bottleneck issue when weights are checkpointed all once onto an NFS during a training run.
  - yeah. it’s kind of a choice/skill issue to stall the gpu. harder problem is not killing ssds with writes once you get this flying

- 🤼 deepseek v4 大量使用
  - [Deep|DeepSeek V4: The Inflection Point for Large-Scale NAND-Based KV Cache _202604](https://fundaai.substack.com/p/deepdeepseek-v4-the-inflection-point)
  - In our previous article we discussed DeepSeek V4’s architectural customization on non-NVIDIA hardware and the first round of API price cuts at 75% off. This article focuses on V4’s second round of cuts: DeepSeek separately took the input cache-hit tier further down to 1/10 of list, stacked on top of the 75% off from the previous round, with the floor at ¥0.025 per million tokens. This widens the cache hit / cache miss spread from 1/12 to 1/120 (cache hit ¥0.025 vs. cache miss ¥3). 
  - DeepSeek V4’s real-world cache hit rate in agent settings has reached 95%+, and based on our research, DeepSeek’s current SSD configuration and utilization have stepped up materially versus before. 
  - Behind this is V4 compressing KV cache size to 10% of V3.2’s, plus DeepSeek’s accumulated engineering work on SSD-based KV cache, which together migrate KV cache from expensive, capacity-limited DRAM / HBM onto larger and cheaper SSD at scale. 
  - We believe DeepSeek V4’s cache-hit repricing implies upside for SSD, with NAND demand set to grow exponentially.

- ## DeepSeek-V4-Flash with SSD KV Cache Offload on Blackwell
- https://x.com/Tono_Ken3/status/2055134669512016304
  - We achieved 63 tok/s inference of DeepSeek-V4-Flash-FP8 (284B) on 4× RTX PRO 6000 Blackwell (TP=4) with full 1M context via SSD KV cache offload! 
  - sglang + SM120 custom flash_mla kernel
  - KV cache → Optane SSD (ds4-server inspired disk offload)

- ## DeepSeek v4 small KV cache + MacBook fast SSD disks = the idea that the disk is not a good target for KV cache is, in this context, totally obsolete. It works *great* . 
- https://x.com/antirez/status/2050982689696588013
  - The session you see is opencode using my inference engine for DS4, saving, loading sessions from disk.
- wonder what magic could be done to improve prefill rate. i think that's mostly what's holding things back at the moment.
  - What I was able to achieve today was a *much* better slope in the prefill rate, that remains at 200 t/s even in very long contexts. This already makes the game a more fair one, since it does not start to degradate in a sensible way as you continue to work. In the M3 Ultra is much faster btw. I also tested there, 2x speed in prefill.
- Luce PFlash

- The Apple nvme are dramatically faster than most ssd, which makes the disk access much more tenable than it would be in most other systems.

- Wow. Being able to use disk for. Kvcache can be a huge change. Are you using any quantization. On KV cache? May I ask more details on how it perform in general and specifically in the refill phase?
  - I'm storing the already compressed KV cache of DeepSeek v4, there is no need to quantize it more, it is already small. Even for long prefills it's sub-second reads from disk. Really works great.

- Everyone spent a year obsessing over RAM capacity for long context, and the actual unlock was just compressing the KV cache enough that a fast NVMe drive can handle the I/O.

- Exactly what we do at scale, leveraging NVLink to outperform DRAM, with 1000x SSD capacities 

- the 7GB/s read on M-series SSDs makes disk-based KV cache actually viable. people are still benchmarking against spinning rust when they dismiss this

- Persisting KV to SSD turns context into a versionable artifact — system prompts and stable RAG chunks become precomputed cache files, so prefill stops being the per-session tax it used to be. The bigger shift is that "session" becomes a file format, not process state.

- ## [deepseek的缓存过了2h还是有效的？？。。难怪这么省  - LINUX DO _202605](https://linux.do/t/topic/2109381)
  - 我差不多18点半左右吧 开着会话就去吃饭了, 然后快21点的时候回来继续改点东西 看着ds后台的缓存读比例依旧很高
  - 2个半小时还有缓存啊。。实在太顶了吧 
- 硬盘缓存说是，就是不知道咋做到的(我不知道而已，因为不太懂这方面)，不过看这意思是传来传去真实成本比重新做一次prefill还低…还挺神奇

- 据说是硬盘缓存，因此容量很大，不知道用的什么协议，吞吐量和延迟都很优秀的样子，有一些服务商使用的是内存缓存

- 官方的说法是缓存时间从几个小时到几天 具体看情况
- 看到官方文档里了 也写着几小时到几天过期

- [原来这才是Deepseekv4.0大放水降价背后的真相 - LINUX DO _202605](https://linux.do/t/topic/2104188)
  - 应该是DeepSeek发现为V4做了over-prepared，准备过度，结果V4的KV Cache命中率比预想的还要高，不得不（注意是不得不）加大流量，让batch size更大。
  - DeepSeek肯定为V4准备了大量推理算力，大到他们自己都没想到V4这么『省』，V4的架构优化（更激进的KV Cache压缩）让GPU计算和带宽消耗远低于预期，KV Cache命中率也高出规划。

- [deepseek V4 pro缓存命中率知识 - LINUX DO _202605](https://linux.do/t/topic/2115383)
  - 了解到Deepseek的命中率高的原因与用法，必须把代码文件放在每次提问的绝对开头 ，且一字不差。标题、寒暄都不能有。有效期经人指正，可能几小时到几天不等。
  - 而claude则是手动标记缓存，需要用 cache_control 明确圈定 那个长文档段落，告诉系统：“这一段帮我缓存下来”。不一定在开头部分。
  - 百万上下文，有能力构建一个庞大到足以覆盖你绝大部分工作场景的“固定前缀”，从而减少token消耗量。
- ds的缓存时间老长了，有时候隔天都还有，A​:divide: 才是五分钟, 另外A的缓存标记也必须从头到尾不能中断，给你标记权是因为他的缓存要收钱，让你自己决定缓存权
# discuss
- ## 

- ## 

- ## 

- ## 

- ## [Inference provider tiers by Cache-hit rates, using openrouter data : r/LLM _202605](https://www.reddit.com/r/LLM/comments/1tlppan/inference_provider_tiers_by_cachehit_rates_using/)
- Interesting ! How did you compute it ?

- ## [我发现现在新的模型，几乎都没有提供 token 的计算规则 - LINUX DO _202606](https://linux.do/t/topic/2463199)
  - 最近想做一个 token 计算的，看看缓存到具体哪里，然后怎么算都算不对的，已经不知道这个 token 怎么算了，我记得之前 openai 还会公布一下 token 是怎么算的。 你们知道吗？ 比如千问，豆包，deeepseek 或者那些最新的大模型 ，token 都是怎么算的吗？tools又是怎么算缓存的？
- 开源模型可以直接找 tokenizer.json 文件计算，openai 的模型有个 tiktoken 库可以算，其他的闭源模型不清楚

- 就是黑盒，因为如果将来套餐赔钱的话，他就削减额度之类的
