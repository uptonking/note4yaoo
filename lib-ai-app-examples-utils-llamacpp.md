---
title: lib-ai-app-examples-utils-llamacpp
tags: [examples, large-language-model, llama.cpp]
created: 2026-06-15T02:49:46.693Z
modified: 2026-06-15T02:50:01.045Z
---

# lib-ai-app-examples-utils-llamacpp

# guide

# popular

# llamacpp-wrapper/ui

# llamacpp-utils

# utils

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
# more
