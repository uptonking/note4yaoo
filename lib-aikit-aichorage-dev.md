---
title: lib-aikit-aichorage-dev
tags: [aichorage, large-language-model, llama.cpp, mlx]
created: 2026-05-28T17:50:35.528Z
modified: 2026-05-28T17:50:54.646Z
---

# lib-aikit-aichorage-dev

# guide

- goals
  - playground for local ocr/vlm models
    - mlx supports stt, 可迁移实现audio-app
  - obsidian for pdf: auto-toc, history/diff, proofreading, tools
    - features-port: editor, backlinks, bases, publish, graph-view
    - sharing by mdbook
  - wiki format: okf(open-knowledge-format), obsidian-bases
  - aistudio: chat/image/video, laptop/minipc厂商都希望内置本地模型
  - built-in image/pdf/ocr for chatting with documents
    - image/pdf ux
  - port model-specific skills to aichorage
  - easy local model xp: single-model, dual-models, hot-models
  - headless api/cli/skills
  - python-first for mlx/office
  - multiple-client/ui
  - embeddable web browser
    - browser-use
  - coding-based solutions
    - comfyui也需要custom node/scripts, 视频生产也需要剪辑和拼接
  - reproducible
    - model/llamacpp config
  - tiered/hybrid-llm
    - 支持cloud与local混合的模式
  - compact prompt mode

- non-goals
  - good llm xp on cpu, but optimized for gpu
    - cpu works for ocr/translation
  - computer-use
  - cloud rag
  - multiple-server/remotes
  - web-search
# draft
- janai-cli like obsidian-cli, ollama-cli, lms-cli
  - skills for janai-cli/lms-cli/ollama-cli
  - 直接兼容 lms-cli, 使用已下载的model
  - 侧重应用层的skills如ocr， 简单实现类似ollama-skills， 容易产生先有鸡还是先有蛋的问题

- workflow
  - comfyui-compatible node
  - export ocr/translation workflow as skill programmatically

- 参考janai支持切换llamacpp/mlx, 来实现支持切换 mineru/paddleocr/docling

- runtime/backend
  - ik_llama.cpp
  - mtplx
  - ~~下载llama.cpp/mlx-vlm到本地缓存位置如.cache后， 添加固定hash后缀，避免重复下载~~ 

- model-manager
  - mlx后端不支持自定义安装最新mlx-lm/mlx-vlm版本
  - 支持针对cpu优化的backend和模型
  - 参考msty，能统一管理 local/ollama/lmstudio/huggingface/modelscope 的模型，释放空间
  - 支持多种类型的model: vlm, embedding, omni, tts

- model-specific
  - LocateAnything

- custom-backend(开箱即用的后端)
  - 针对ocr的 ppOcrv5

- speculative-decoding
  - draft model for dflash
- faster
  - mtp

- translation
  - ✨ 在原文中显示四六级词汇的翻译。 
    - ❓ 如何在不改变布局或减少reflow的目标下实现ux
    - 可配置调整译文的位置， 上下左右移动
  - 部分翻译， 仅翻译难理解的语句/四六级词汇

- bench
  - omlx-benchmark可迁移

- search in chat

- 类似openclaw的服务进程和remote control

- v0.7.6_20260127版本上, 自定义url都会失败

- lite
  - 去掉llama.cpp/mlx后端的纯客户端版本

- models
  - reproducible ai/rag/ocr
    - 不同版本的向量模型生成的数据空间维度大小是不一致的会导致后续查询数据处理啥的有问题
    - 另一种思路是通过类似jupyter的重代码工具去实现
    - 可以兼容comfyui的导出json，直接在aichorage打开
  - I really wish someone would just publish the optimal llamacpp command for all models with our hardware. We all have the same thing so we should all benefit from the same best command per model

- KV Cache on disk added to LM Studio

## local-models

- port model-specific skills to aichorage

- [skills for Deploy MiniCPM5-1B with LM Studio](https://github.com/OpenBMB/MiniCPM/blob/main/skills/minicpm5-deploy-lmstudio/SKILL.md)
  - [skills for Deploy MiniCPM5-1B with Ollama](https://github.com/OpenBMB/MiniCPM/blob/main/skills/minicpm5-deploy-ollama/SKILL.md)
# pm

## pm-issues

- chat-projects 和 task-folder/workspace 如何区分

## llm-iot

- 智能音箱目前缺少官方api的支持, 因为用户很少为月租token付费, 而适合使用本地的stt/tts/小模型
# dev-xp

# more

# devlog
- I verified against LM Studio’s current docs that their parallel-request feature is explicitly llama.cpp- first, with MLX “coming soon.”
