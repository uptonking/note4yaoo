---
title: lib-ai-app-community-model-small-edge
tags: [community, large-language-model, mobile, phone]
created: 2026-01-23T13:08:23.483Z
modified: 2026-01-23T13:10:20.291Z
---

# lib-ai-app-community-model-small-edge

# guide

# local-models
- local-hardware
  - [Hardware – Hugging Face](https://huggingface.co/hardware)

- local-model
  - [GPU Poor LLM Arena - a Hugging Face Space by k-mktr](https://huggingface.co/spaces/k-mktr/gpu-poor-llm-arena)

- https://github.com/fiveoutofnine/whatcanirun /202603/ts
  - https://whatcani.run/
  - Find the best local models based on real data
  - https://x.com/fiveoutofnine/status/2038728823861367233
    - whatcani.run is based on real runs submitted by people
    - canirun.ai provides estimates across a wider variety of models and devices
    - it filters all submissions by CPU + GPU + RAM, and so far that's the only model that has any benchmark data submitted for it

- https://github.com/AlexsJones/llmfit /MIT/202603/rust/ts
  - https://www.llmfit.org/
  - Hundreds of models & providers. One command to find what runs on your hardware.
  - A terminal tool that right-sizes LLM models to your system's RAM, CPU, and GPU. Detects your hardware, scores each model across quality, speed, fit, and context dimensions, and tells you which ones will actually run well on your machine.
  - Ships with an interactive TUI (default) and a classic CLI mode. Supports multi-GPU setups, MoE architectures, dynamic quantization selection, speed estimation, and local runtime providers (Ollama, llama.cpp, MLX, Docker Model Runner).

- https://github.com/outsourc-e/bench-loop /MIT/202605/python
  - https://bench-loop.com/
  - Local-first CLI for benchmarking LLMs on real hardware — quality, speed, reliability, and a real multi-turn agent loop.
  - BenchLoop is a local-first CLI + web app for benchmarking LLMs running on your own hardware. 
  - It scores models across seven repeatable suites — quality, speed, reliability, agentic tool use, coding, instruction following — and gives you receipts: per-task outputs, latency, token counts, machine info, scores.
  - No accounts, no telemetry, no API keys. Your model, your machine, your numbers.
# discuss-stars
- ## 

- ## 

- ## 
# discuss-browser-ai
- ## 

- ## 

- ## 

- ## 

- ## 

- ## 🧭 [Chrome's Local AI Model in production (Gemini Nano) 41% eligibility, 6x slower and $0 cost : r/LocalLLaMA _202601](https://www.reddit.com/r/LocalLLaMA/comments/1qkph45/chromes_local_ai_model_in_production_gemini_nano/)
  - reading about Chrome's built in AI model (Gemini Nano 1.8b) and tried implementing it, this is my story.
  - Google ships Chrome with the capability to run Gemini Nano, but not the model itself.
  - Multiple models, no control. Which model you get depends on an undocumented benchmark. You don't get to pick.
  - ~1.5-2GB download. Downloads to Chrome's profile directory. Multiple users on one machine each need their own copy.
  - On-demand. The model downloads the first time any site requests it.
  - Background download. Happens asynchronously, independent of page load.
  - Think of the requirements like a AAA video game, not a browser feature.
  - Inference Performance:
  - Gemini Nano (on-device)	7.7s
- 👀 At p99, Nano hits 52.9 seconds while Gemma is at 2.4 seconds. Worst case for Nano was over 9 minutes. Gemma's worst was 31 seconds.
  - prompt-processing 速度太慢
- What Surprised Us
  - No download prompt. The 1.5GB model download is completely invisible. No confirmation, no progress bar. Great for adoption. I have mixed feelings about silently dropping multi-gigabyte files onto users' machines though.
  - Abandoned downloads aren't a problem. Close the tab and the download continues in the background. Close Chrome entirely and it resumes on next launch (within 30 days).
  - Local inference isn't faster. I assumed "no network latency" would win. Nope. The compute power difference between a laptop GPU and a datacenter overwhelms any latency savings.
  - You can really mess up site performance with it We ended up accidentally calling it multiple times on a page due to a bug..and it was real bad for users in the same way loading a massive video file or something on a page might be.
- By the numbers, there's no reason to use Gemini Nano in production:
  - It's slow
  - ~60% of users can't use it
  - It's not cheaper than API calls (OpenRouter is free for Gemma)
- We're keeping it anyway. I think it's the future. Other browsers will add their own AI models. We'll get consistent cross-platform APIs. I also like the privacy aspects of local inference. The more we use it, the more we'll see optimizations from OS, browser, and hardware vendors.

# discuss-small-llm-hot
- ## 

- ## 

- ## 
# discuss-local-hardware
- ## 

- ## 

- ## 

- ## [香橙派+MiniCPM-V-4.6, 本地化的极致小模型推理方案 - LINUX DO _202605](https://linux.do/t/topic/2241870)
  - 这次轮到手头的这个国产小板子（香橙派AI Pro，昇腾310B芯片）。由于国产生态问题，其实这个板子很少有人去适配模型
  - 20TOPS版本大概2000块，8T版本更便宜，只要899。折合一下FP16算力差不多也有1080TI水平了，用的unified memory, 24GB内存。最近没啥人折腾，还是要祭出天才程序员，这次不是写CUDA，而是写AscendC自定义算子，把MiniCPM-V-4.6支持起来。
  - 一个完全从零写的 C++/AscendC 推理引擎, 把 MiniCPM-V 4.6 跑在 Orange Pi AIPro 20T 板载的 Ascend 310B NPU 上。 文本和图像对话都完全跑在 NPU 上, Python 端只在 CPU 上做 tokenize 和图像预处理, 推理热路径完全不依赖 torch_npu。
  - 通过三轮 cube unit / 自定义 kernel 工作, 单 batch 解码从 2.88 → 5.90 tokens/s(~2×), 跑的是完整 24 层 hybrid 线性 + full attention 模型(hidden 1024, vocab 248094, fp16)

- 这是个边缘计算的板子吧？其实我没想明白它的家用场景。 如果只是低功耗长期运行的话，理论上ESP32+glm flash免费api就可以实现可用了，效果还会好点。

- 这速度看起来还不如3*2T=6Tops的rk3588

- 310p的性能依托，堪称昇腾界的k80，胶水核心，推理能力依托，严肃要求换成930，天才程序员一晚上才把驱动什么的打好，官网甚至没说驱动不支持高版本内核

- 我的macmini m4 丐版 部署过几个本地模型后 发现基本没有什么可用性, 还是老老实实买套餐

- 昇腾一直就不支持高版本linux内核……都是坑

- ## We’re launching @huggingface Hardware: → trending GPUs & CPUs  _202605
- https://x.com/julien_c/status/2057084823097794772
  - nvidia: 45%
  - amd: 5%
  - apple: 16%
  - cpu: 32%

- from tracking public training logs, A100s still dominate open-source runs by a wide margin. the interesting part is consumer GPUs — 4090s and M-series are quietly becoming the fine-tuning workhorses. real bottleneck for most people isn't compute, it's VRAM. wonder if your data shows the same split

- The reverse would be great too: input my hardware (GPU + VRAM) and get the best models I can run locally right now, with quant suggestions.

- 
- 
- 
- 

# discuss
- ## 

- ## 

- ## 

- ## 

- ## 
