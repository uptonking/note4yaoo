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
  - obsidian for pdf: auto-toc, history/diff, proofreading, tools
    - features-port: editor, backlinks, bases, publish, graph-view
  - port model-specific skills to aichorage
  - headless api/cli/skills
  - python-first
  - image/pdf ux
  - embeddable web browser
  - multiple-client/ui

- non-goals
  - optimized for gpu, not cpu
    - cpu works for ocr/translation
  - cloud rag
  - multiple-server/remotes
# draft
- janai-cli like obsidian-cli, ollama-cli, lms-cli
  - skills for janai-cli/lms-cli/ollama-cli
  - 直接兼容 lms-cli, 使用已下载的model

- workflow
  - export ocr/translation workflow as skill programmatically

- 参考janai支持切换llamacpp/mlx, 来实现支持切换 mineru/paddleocr/docling

- runtime/backend
  - ik_llama.cpp
  - mtplx
  - ~~下载llama.cpp/mlx-vlm到本地缓存位置如.cache后， 添加固定hash后缀，避免重复下载~~ 

- model-manager
  - mlx后端不支持自定义安装最新mlx-lm/mlx-vlm版本
  - 支持针对cpu优化的backend和模型
  - 参考msty，能统一管理 local/ollama/lmstudio/huggingface 的模型，释放空间
  - 支持多种类型的model: vlm, embedding, omni, tts

- model-specific
  - LocateAnything

- custom-backend(开箱即用的后端)
  - 针对ocr的 ppOcrv5

- speculative-decoding
  - draft model for dflash
- faster
  - mtp

- bench
  - omlx-benchmark可迁移

- search in chat

- 类似openclaw的服务进程和remote control

- v0.7.6_20260127版本上, 自定义url都会失败

- lite
  - 去掉llama.cpp/mlx后端的纯客户端版本
# pm

# dev-xp

# more

# devlog
