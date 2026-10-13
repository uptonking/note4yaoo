---
title: lib-office-mineru-dev
tags: [mineru]
created: 2026-09-26T20:55:51.533Z
modified: 2026-09-26T20:55:59.290Z
---

# lib-office-mineru-dev

# guide

- pros
  - 提供了2种转换方式和架构: ocr+parse, vlm
  - 提供多种服务: openai-compatible api, mineru-router for multi-service / multi-GPU orchestration

- cons
  - license: AGPL
  - ? 未实现流式处理大的pdf文件

- features
  - LLM-aided post-processing: title leveling, cross-page table cell continuation

- 优化提取中文pdf文字的方案
  - 可参考华人团队的方案, 如 mineru
# issues

# draft

# dev-xp

- 
- 
- 
- 
- 
- 
- 

- should i use full as extra like uv tool install -U "mineru[full]>=4.0, <5", is it correct?
  - The base package already works out of the box, using ONNX CPU small models plus a llama.cpp VLM in Vulkan mode. 
  - mineru[full] adds Torch plus vLLM on Linux or LMDeploy on Windows.
  - Linux with an NVIDIA GPU: full is a good fit, since vLLM gives you the fastest VLM inference.
  - Windows with an NVIDIA GPU: full gets you LMDeploy. If you only want Torch for the small models, mineru[torch] is lighter.
  - Apple Silicon Mac: you don’t need full. Torch is installed by default there, and the VLM runs on llama.cpp. The base package is enough. 
  - CPU-only machine, or you just want to try it: use the base package. full pulls in large GPU-oriented dependencies you won’t use.
# more

# changelogs

- 
- 
- 
- 
- 
- 
- 

- [v4.0.0 _202609](https://github.com/opendatalab/MinerU/releases/tag/mineru-4.0.0-released)
  - 4.0 is a major release that rebuilds the project around tiered parsing quality, native multi-format document parsing, a local document library for agent reading, and unified SDK / API / service tools
- The 3.x pipeline / vlm / hybrid backend selection is replaced by four quality tiers: flash, basic, standard, and advanced.
  - `flash` parses native PDF text and digital documents without inference models, for discovery, preview, and indexing. 
  - `basic` runs small models for OCR, formulas, and tables, and can run on CPU. 
  - `standard` (the default reading quality) combines small models with the VLM for complex layouts. 
  - `advanced` spends more inference compute for maximum quality on difficult documents.
  - PDF and images support all four tiers; 
  - Office, OpenDocument, EPUB, OFD, HTML, and CSV/TSV are parsed locally at flash tier.
- Independent model configuration
  - Small models (ONNX or Torch) and the VLM engine (llama.cpp, vLLM, or LMDeploy) are now configured independently 
  - New 4.0 model bundles MinerU-4_models_onnx / MinerU-4_models_torch (PP-DocLayoutV2, PP-OCRv6 Tiny Det + Small Rec, PP-FormulaNet plus-M, seal OCR, and shared table models), downloaded and verified with mineru-kit models download / verify.

- Supported inputs now cover PDF, images, DOC/DOCX, PPT/PPTX, XLS/XLSX, RTF, ODT/ODS/ODP, EPUB, OFD, HTML, and CSV/TSV. 
  - DocVortex provides native document parsing: no conversion to PDF, no model downloads.
- Plain-text files (.txt, .md, ...) are read directly instead of parsed.

- New mineru command family: parse, read, find, search, show, list, watch, scan, plus cache control (invalidate, forget, cleanup) and a background service (mineru server start / status).

- Unified tools and V1 API
  - The Python SDK, stateless batch conversion (mineru-kit parse), the multi-service Router, and the Gradio WebUI (mineru-webui) share one structured result model.
  - The HTTP service is rebuilt around V1 (/v1/health, /v1/tiers, /v1/uploads, /v1/parse/jobs, /v1/files); legacy /file_parse and /tasks are not provided.

- One document model renders to Markdown, HTML, LaTeX, DOCX, EPUB, PDF, Structured Content, and Content List V1/V2; each entrypoint exposes its own subset of exports. See Output Formats and Result Contract.

- With 4.0, MinerU grows from a document conversion tool into a privacy-first document platform: tiered quality, native multi-format parsing, a searchable local library with stable citation locators for agents, and unified interfaces. 

- 
- 
- 
- 
- 
