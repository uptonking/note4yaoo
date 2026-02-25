---
title: lib-ai-app-community-model-vlm-ocr
tags: [large-language-model, ocr, vision, vlm]
created: 2025-11-06T18:48:41.322Z
modified: 2025-11-06T18:49:13.977Z
---

# lib-ai-app-community-model-vlm-ocr

# guide

- tips
  - 缺少pdf测试文件或资源，可以去主流pdf/ocr方案的issue里面找附件

- resources
  - [Supercharge your OCR Pipelines with Open Models _202510](https://huggingface.co/blog/ocr-open-models)
  - [PaddleOCR-VL和Deepseek-OCR部署使用体验记录 _202510](https://linux.do/t/topic/1107651)

- https://github.com/bytefer/macos-vision-ocr /MIT/202502/swift
  - A powerful command-line OCR tool built with Apple's Vision framework, supporting single image and batch processing with detailed positional information output.
# free-ocr-api
- [MinerU api](https://mineru.net/apiManage/limit)
  - 单个用户一天最多允许上传1万个文件，其中html文件最多100个
  - 优先解析额度：2000页/日, 超出部分将自动进入普通队列依次处理
  - 单个文件大小不能超过 200MB, 文件页数不超出 600 页
  - 获取单个任务结果、批量获取任务结果共用一个频控，1000次/分钟

- [PaddleOCR - 文档解析与智能文字识别 | 支持API调用与MCP服务 - 飞桨星河社区](https://aistudio.baidu.com/paddleocr/task)
  - 本服务基于该开源项目的 PaddleOCR-VL 模型构建
  - 每日调用解析页数 3000
  - 单个文件大小无限制，但为避免处理超时请控制在100页内，超出部分将被忽略不解析
  - [PaddleOCR-VL_API docs](https://ai.baidu.com/ai-doc/AISTUDIO/2mh4okm66)
  - 交互与mineru类似
  - [PaddleOCR-VL Online Demo - a Hugging Face Space by PaddlePaddle](https://huggingface.co/spaces/PaddlePaddle/PaddleOCR-VL_Online_Demo)
# models-vlm/ocr-xp
- ocr-pros
  - position data for layout and characters
  - confidence level for characters
  - faster than vlm

- ocr-cons
  - 文字是独立的图形，缺少语义，不利于提取信息
  - bad at handwriting recognition

- vlm-pros
  - 识别出的文本一般是语义化的段落， 便于提取信息
  - 对于非文档类型的文件识别更强大，如倾斜海报中的文字
  - simpler than the traditional ocr pipeline
  - powerful: ocr + qa + image-caption + translation
  - good at handwriting recognition

- vlm-cons
  - hallucination for blurry text
  - slower than ocr

- toolchain
  - 虽然很多ocr模型官方不支持， 但社区量化版可能支持，需要具体尝试
  - 不同vlm/ocr模型的输出格式不同, 统一输出内容是否存在需求? 目前对blocks/tags的定义缺乏统一规范(各项目都自定义)

- llama.cpp
  - 已支持: LightOnOCR-1B
  - 暂不支持(20260106): deepseek-ocr, dots.ocr, PaddleOCR, hunyuanocr, chandra, nanotes

- ollama
  - 支持: deepseek-ocr, qwen3vl
  - 暂不支持(20260106): mineru, paddleocr, hunyuanocr, dots.ocr
  - https://github.com/ollama/ollama/tree/main/model/models

- mlx-vlm
  - 支持: deepseek-ocr, hunyuanocr, LightOnOCR
  - 暂不支持(20260106): dots.ocr, mineru
  - [Models to port to MLX-VLM · Issue · Blaizzy/mlx-vlm _202406](https://github.com/Blaizzy/mlx-vlm/issues/39)

- 🖼️ 支持提取图片的bbox坐标
  - glm-4.6v-flash
  - Qwen3-VL
  - PaddleOCR-VL
  - dots.ocr
  - Chandra
  - Docling
  - unstructured
  - mineru-PDF-Extract-Kit(AGPL), Marker(GPL)
  - Nemotron Parse

- qwen3-vl-4b
  - 适合作为通用图片文字识别方案，识别完后一般还会解释一段，有时解释文字会冗长
- [Qwen/Qwen3-VL-2B-Instruct · Hugging Face _202510](https://huggingface.co/Qwen/Qwen3-VL-2B-Instruct)
  - [why the outputs are different ?](https://huggingface.co/Qwen/Qwen3-VL-2B-Instruct/discussions/5)
    - output is changing every time.
    - The variation you are seeing it's simply because generate() uses stochastic sampling by default. Calling model.eval() ` only disables dropout/batchnorm and it has no effect on how tokens are selected during response generation. to make your outputs identical every time, you need to turn off sampling and force greedy decoding and fix all RNG seeds. for fully deterministic setup try something like this...
  - [How different are its hardware requirements from those of the Qwen2-VL-2B?](https://huggingface.co/Qwen/Qwen3-VL-2B-Instruct/discussions/4)
    - Based on my experience, it works fine even on a CPU Qwen/Qwen3-VL-2B-Instruct is likely a merge with a 300M VisionEncoder with their previous Qwen/Qwen3-1.7B base Model.

- nanonets-ocr2-3b
  - 输出的内容markdown优先，内容及格式都很准确
    - 表格中的代码也能正确输出为markdown inline code
    - 外部链接能直接输出为markdown链接
    - 同一区域的内容会输出为同一个段落，不会按原文本显示换行
  - 识别图片中的代码块输出codeblock
  - 识别mermaid流程图，输出流程图文本
  - 能正确识别页眉页脚
  - 能识别图文混排元素，输出内容时能提供方位，如插图旁边是...
  - 能识别表格，但 表格行内容有时会错位而在中间插入空行

- deepseek-ocr-3b
  - 适合识别文档，对于普通图片文本的识别有时需要特别的prompt，实测 `extact text` 会导致模型乱回复, 而 `extact text in image` 可以准确回复图片中的文本
  - 不能识别mermaid流程图
  - 不能正确识别页眉页脚，默认忽略了
  - 同一区域的内容有时不会输出为同一个段落，会按图片中的换行输出换行，适合用来还原pdf布局
  - 识别图片中的代码块输出的内容不是codeblock而是普通文本
  - 🌹
    - 识别中文的正确率高
    - 识别图片中的表格能准确输出文本，每行内容正确
  - 极少数的场景，会将图片中的英文翻译为中文输出, 并且LOOP

- granite-docling-258m
  - 能输出带语意的自定义标签, 如 page_header, code, list_item, loc_99, text
  - 默认markdown不友好，需要手动转换自定义标签
  - 部分中文识别的错误率较高

- PaddleOCR-VL-0.9b
  - [Frequently Asked Questions on Inference and Deployment of PaddleOCR-VL PaddleOCR-VL 推理部署相关高频问题回复 ](https://github.com/PaddlePaddle/PaddleOCR/issues/16823)
    - 目前 PaddleOCR-VL 暂不支持在 macOS 系统上进行原生部署。对于搭载 x64 架构 CPU 的设备，可通过 Docker 容器方式进行部署。同时，针对 macOS 生态，我们也在评估基于 MLX-VLM 的部署方案可行性。
  - [PaddleOCR-VL-1.5 Online Demo - a Hugging Face Space by PaddlePaddle](https://huggingface.co/spaces/PaddlePaddle/PaddleOCR-VL-1.5_Online_Demo)

- MinerU2.5-1.5b
  - [通过API调用解析下载得到的图片被压缩了，没有返回原图 ](https://github.com/opendatalab/MinerU/issues/4169)
    - 目前 MinerU 的 vlm 后端（包括你用的 <2.2.0 版本）通过 API 提取图片时，所有图片都会被处理为 JPEG 格式并默认采用 PIL 的压缩参数，无法直接返回文档中的原图。这会导致图片体积变小、画质变模糊，且 API、配置文件和环境变量都没有提供控制图片质量或格式的选项。相关代码和 API 都是硬编码为 JPEG 输出，没有暴露 PNG 或无损选项，也没有参数可以调整压缩质量 
    - 如果你确实需要原图，可以考虑： 用外部工具（如 Office、Adobe Acrobat、Python-docx、PyMuPDF 等）直接从 DOC/PDF 文件提取原始图片。

- MonkeyOCR-pro-1.2b
  - MonkeyOCR-3b

- chandra

- olmocr-2-7b

- dots.ocr-3b
  - [rednote-hilab/dots.ocr · Hugging Face](https://huggingface.co/rednote-hilab/dots.ocr)
  - [helizac/dots.ocr-4bit · Hugging Face](https://huggingface.co/helizac/dots.ocr-4bit)

- [lightonai/LightOnOCR-2-1B · Hugging Face _202601](https://huggingface.co/lightonai/LightOnOCR-2-1B)
  - [Update README.md](https://huggingface.co/wangjazz/LightOnOCR-2-1B-gguf/discussions/1)
    - LightOnOCR does not require a prompt, it would degrade performance if given any input text
  - 🐛 [hallucinations on empty pages](https://huggingface.co/lightonai/LightOnOCR-2-1B/discussions/4)
  - [Tables as markdown instead of HTML](https://huggingface.co/lightonai/LightOnOCR-2-1B/discussions/6)
    - The previous version of LightOn OCR would output tables directly to markdown format, but this version is outputting tables to HTML format (more tokens generated, slower speed in out tests)
    - We have debated on this before working on the second version, but in the end we decided on HTML as output as some nested tables cannot be represented in markdown and thus we would lose some generality. Also converting from html to md after transcription is much more robust than the reverse operation, which also explains our choice. It hasn't been planned for now to give this as option but I'd say the model would be quite suited for a finetuning in this direction if it's really a deal breaker for your usage 
  - [Remove page numbers from the output](https://huggingface.co/lightonai/LightOnOCR-2-1B/discussions/5)
    - one of the main design choices compared to other solution is to include all visible text. that being said, the model can be easily finetuned to ignore headers/footers/page numbers, see the v1 blog post for an example.

- [echo840/MonkeyOCR-pro-1.2B · Hugging Face](https://huggingface.co/echo840/MonkeyOCR-pro-1.2B)
  - vlm specialized for OCR and document analysis
  - Architecture: Qwen2.5-VL (qwen2vl)
  - MonkeyOCR adopts a Structure-Recognition-Relation (SRR) triplet paradigm, which simplifies the multi-tool pipeline of modular approaches while avoiding the inefficiency of using large multimodal models for full-page document processing.
  - MonkeyOCR-pro-1.2B surpasses MonkeyOCR-3B by 7.4% on Chinese documents.
  - [dinhquangson/MonkeyOCR-pro-1.2B-Vision-GGUF · Hugging Face](https://huggingface.co/dinhquangson/MonkeyOCR-pro-1.2B-Vision-GGUF)
  - https://github.com/Yuliang-Liu/MonkeyOCR
  - https://aiwrite.wps.cn/pdf/parse/web/

- glm-4.6v-flash
  - https://github.com/zai-org/CogVLM
  - Visual Grounding. Three modes of grounding are supported:
    - Can you provide a description of the image and include the coordinates [[x0,y0,x1,y1]] for each mentioned object?
    - Can you point out children in blue T-shirts in the image and provide the bounding boxes of their location?
    - Tell me what you see within the designated area [[086,540,400,760]] in the picture.
    - Format of coordination: The bounding box coordinates in the model's input and output use the format [[x1, y1, x2, y2]], with the origin at the top left corner, the x-axis to the right, and the y-axis downward. (x1, y1) and (x2, y2) are the top-left and bottom-right corners, respectively, with values as relative coordinates multiplied by 1000 (prefixed with zeros to three digits).

- llama3.2-vision-11b
  - 似乎不支持中文

- [zai-org/GLM-OCR · Hugging Face _202602](https://huggingface.co/zai-org/GLM-OCR)
  - [Thanks for using the PP-DocLayoutV3 model from PaddleOCR-VL-1.5](https://huggingface.co/zai-org/GLM-OCR/discussions/4)
    - The complete OCR pipeline integrates PP-DocLayoutV3 for document layout analysis, which is licensed under the Apache License 2.0
  - [提取结构化信息的提示词使用demo 可以提供一下吗 ](https://github.com/zai-org/GLM-OCR/issues/23)
    - 在线版目前没有结构化提取，如需要使用本地部署
    - "请按下列JSON格式输出图中信息:\n{\n    \"id_number\": \"\",\n    \"last_name\": \"\",\n    \"first_name\": \"\",\n    \"date_of_birth\": \"\",\n    \"address\": {\n        \"street\": \"\",\n        \"city\": \"\",\n        \"state\": \"\",\n        \"zip_code\": \"\"\n    },\n    \"dates\": {\n        \"issue_date\": \"\",\n        \"expiration_date\": \"\"\n    },\n    \"sex\": \"\"\n}"
  - https://github.com/zai-org/GLM-OCR /441Star/apache2/202602/python/ts
    - a multimodal OCR model for complex document understanding, built on the GLM-V encoder–decoder architecture. I
    - It introduces Multi-Token Prediction (MTP) loss and stable full-task reinforcement learning to improve training efficiency, recognition accuracy, and generalization.
    - The model integrates the CogViT visual encoder pre-trained on large-scale image–text data, a lightweight cross-modal connector with efficient token downsampling, and a GLM-0.5B language decoder
    - Combined with a two-stage pipeline of layout analysis and parallel recognition based on PP-DocLayout-V3, GLM-OCR delivers robust and high-quality OCR performance across diverse document layouts.

- 
- 
- 
- 
- 

# 🆚 ocr/vlm-parsing-benchmarking 
- leaderboard
  - [Open VLM Leaderboard - a Hugging Face Space by opencompass](https://huggingface.co/spaces/opencompass/open_vlm_leaderboard)
  - [allenai/olmOCR-bench · Datasets at Hugging Face](https://huggingface.co/datasets/allenai/olmOCR-bench)
    - https://x.com/NielsRogge/status/2024518878655578509
    - We converted OlmOCR-Bench by @allen_ai to an official benchmark on the hub.

- https://github.com/opendatalab/OmniDocBench /1.3kStar/apache2/202512/python/mineru
  - https://opendatalab.com/omnidocbench
  - A Comprehensive Benchmark for Document Parsing and Evaluation

- [OCR Arena](https://www.ocrarena.ai/battle)
  - [I made a free playground for comparing 10+ OCR models side-by-side _202511](https://www.reddit.com/r/LocalLLaMA/comments/1p35f2c/i_made_a_free_playground_for_comparing_10_ocr/)

- [SpatialBench - AI Spatial Reasoning Benchmark](https://spicylemonade.github.io/spatialbench/)
  - https://github.com/spicylemonade/spatialbench
  - Evaluating multimodal model performance on complex 3D and 2D spatial tasks.
  - designed to evaluate the next generation of multimodal AI models on their ability to reason about space, structure, and pathing

- https://getomni.ai/ocr-benchmark
  - https://github.com/getomni-ai/benchmark
  - The goal of this benchmark is to publish a comprehensive benchmark of OCRaccuracy across traditional OCR providers and multimodal Language Models.
  - The evaluation dataset and methodologies are all Open Source, and we encourage expanding this benchmark to encompass any additional providers.

- ## OmniDocBench is getting saturated. VLMs are getting increasingly better at document understanding _202602
- https://x.com/jerryjliu0/status/2026408921385284001
  - we're quickly approaching the point where we need a new benchmark. 
  - The latest models are pushing ~95% on OmniDocBench and are already overfitting the benchmark, while still having real gaps on document capabilities.
  - The evaluation metrics of OmniDocBench depend completely on exact match and not on semantic correctness. The latter is much more important, especially in today's world where LLMs can reason over text tokens regardless of non-important formatting differences.
  - There are so many real-world documents that haven't yet been solved by even the latest models. We'd love to welcome discussion on advancing document understanding benchmarks that are more diverse and properly score models on semantic correctness.

- The issue with OCR is it’s a small piece of a larger system. we need full e2e document processing benchmarks that include NER with OCR
# discuss-stars
- ## 

- ## 

- ## 

- ## Increased thinking doesn't correlate with increased document understanding 
- https://x.com/jerryjliu0/status/2024568615320899930
  - [The Cost of Overthinking: Why Reasoning Models Fail at Document Parsing _202602](https://www.llamaindex.ai/blog/the-cost-of-overthinking-why-reasoning-models-fail-at-document-parsing)
  - Models are getting much better at reasoning which translates well for math/coding/general intelligence tasks. We did some experiments with GPT-5.2 on different thinking modes to see if it actually helps improves scores on OmniDocBench.
  - Result: it doesn't, and in fact the higher the thinking, the more the output structure might deviate from the existing input. 

- This matches what I see in practice: perception is the bottleneck. Once OCR drops pixels, no amount of reasoning brings them back. Pipelines beat monoliths

- This matches what we see in practice: more “thinking” helps compute, not perception. If retrieval/parsing is weak, you just get more confident synthesis on partial evidence, so the win is better chunking + citations/provenance before you crank reasoning depth.

- The thinking mode might need to be task-specific - for document understanding, guided summarization approaches often outperform generic reasoning prompts regardless of model size.

- ## 🖼️ [单图≠多图：多图理解时 VLM 为什么更容易“胡说”，以及一个两阶段解法 _202602](https://linux.do/t/topic/1584167)
  - 这篇文章起源于我发现在多图分析时，网页端的表现和 API 调用的结果一致性相差很大，然后我就一步步去拆为什么相差大，然后试图在工程上找补救的过程。
  - 课题是关于电池的缺陷检测和自动分拣.
  - 因为当时样本很少应该没法通过常规方法练出来能区分是否缺陷的模型，不管是图像分类还是 yolo 什么的。而课设里推荐方法是用边缘检测和 opencv 来做.
  - 一方面我不太熟悉 opencv 而且它的 typing 让我感到痛苦，于是乎我想到了 yolo 定位电池的位置和坐标.（可以通过矩形框定位中心点，顺逆时针旋转 45° 并比较矩形框长宽比来确定电池朝向和大致角度，这是为了方便判断抓取的位置和抓手角度）, 然后用 VLM (Vision-Language-Models) 即多模态模型来判断模型的是否缺陷和缺陷类型.
  - 起初在 Chatgpt, Gemini 那边上传了几组各种光照下的电池图像，它们都在识别检测的过程中达到了惊人的 100% 的准确率，而且多次回复一致性很高。即便一次上传六七张 (包括一张完好电池的参考，至于缺陷都是用提示词描述的) 也是如此.
  - 于是乎我还到 Ollama 那边下了一批 VLM 本地部署测试，一方面是提高 "工作量", 另一方面也是为了更低的延迟.
  - 一测吓一跳. 模型不知道是没法理解我的提示词，还是没法理解我发的图像。我这次测出来不管是准确率还是一致性都非常的低，准确率在 50% 左右，而且还经常前后矛盾，因为我的电池也只有两类标签，我在想着好家伙，这就是胡乱作答.
  - 但是我把图像单图发给 VLM 进行描述，我发现和网页端的 Chatgpt 的差距也不是肉眼可见的那么大.
  - 我在发单图和多图的时候，都是把图像塞到 python数组里面
  - 这个时候我想，可能真是模型差距，于是乎我又改用 gemini-flash-2.5, chatgpt-5.1-chat 之类的模型进行了一番测试 (API 调用). 但是即便使用了相同的模型，它们和我在网页端得到的准确率也相差非常大，而且图超出四张的时候，一致性也开始下降.
  - 但是即便使用了相同的模型，它们和我在网页端得到的准确率也相差非常大，而且图超出四张的时候，一致性也开始下降.
  - 而我后面跑去稍微调研了下，发现它和 Lost in the Middle 描述的长上下文检索 / 位置偏置问题非常相似.
- 网页端 API 差距这么大可能是因为:
  - 网页端可能做了 逐图预摘要 /rerank/ 选择性投喂
  - 网页端可能有 更强的系统提示词与格式约束 (比如强制输出 JSON, 强制逐图作答)
  - API 侧的参数 (temperature, max_output, tool choice, 并发顺序) 可能也影响一致性
- 多图 benchmark (如 MIBench/MMIU/MIRB) 一致表明：模型从单图到多图会出现显著性能下滑与关系理解困难；同时有工作明确指出多模态场景会遭遇 视觉 token 过多 的工程瓶颈，需要压缩.

- 在机制上，一个合理解释是：当多张图的视觉 token 与文本共同进入同一 Transformer 上下文时，会放大长上下文的检索困难与位置偏置 (例如 Lost in the Middle 所揭示的 "中间信息更难被利用").[这只是我的推测]
- base64 image 并不直接进行推理
  - image_url 之所以使用 base64 只是方便 http 传输，而模型在推理时，会将 base64 解码为图像.
  - 也就是说，VLM 看到的实际上是 user prompt + 图像.
- 图像如何被处理缩放 (token 计量)
  - Tile-based (gpt-4o/4.1/4.5 等): detail="low" 是固定 base token; detail="high" 先等比缩放到 "最长边 ≤2048, 短边 = 768", 然后按 512×512 的 tile 数计费: tokens = base + tile_tokens * tiles.
  - . Patch-based (gpt-4.1-mini/nano, o4-mini): 按 32×32 patch 覆盖图像计数，超过 1536 patch 就等比缩小到不超过为止，再乘模型倍率.
- 像素是怎么变成 vision token
  - vision token 如何与 prompt token 拼接或隔离？

- 交叉注意力: 把视觉当外部 memory, 文本按需查询，工程上更容易控制 "视觉信息预算", 更适合长序列 / 多图；但增加模块与训练复杂度.

- 实际上落地时，多图的任务很棘手，一方面是图像数量不确定 , 另一方面是图像之间的关系不确定 , 第三方面是图像和用户具体的多图任务需求和指代不确定.

- 💡 针对数量不确定，关系不确定，需求不确定还真有一个比较简单的解法，它不用动模型推理，可以简单地套用在应用里. 
  - 即把模型的图像分析和文本分析真正分成两步.
  - 对应逐图分析模式的分支，之所以分开，是为了 token 考虑，应该把它设计为可以开关的.
  - 第一步，只以一个 vision model 来分析提取图像的具体信息，注意，这个时候是不给用户最近的提示词的，而是把整个分析抽离出来，只给 vision model 一个系统提示词，和一个固定的抽取指令作为用户提示词输入，旨在得到类似这样的一个 json。 每次执行一张图像特征提取，并发处理，处理完成后就拼成一个 list 或者 dict, "p1", "p2" 这样的.
  - 第二步，就是把这整个拼凑过后的 vision summaries 和用户提示词放在一起类似这样
  - 而在这两步中间可以做的工作还有挺多，比如根据 json 某个 key 来做区分，或者耦合.
- 优点
  - 它不在乎输入的图片有几张，二三十张进来理论上也是可以的。而且进一步这些 json 可以直接作为模型的看图的一个引导，退一步模型可以直接根据这些图片来分析图片的简要内容
  - 它可以通过提示词自定义一些 json key, 来做耦合或者区分，可以分清楚图片关系
  - 它把原本显得更重，更 hard 的多图分析任务，变成了一个可以依赖文本来做回答的文本理解任务，或者说提供了参考。它让图像占比变小了，文本占比变大了，让模型更多地把味文字，也就更有可能会注意到整个上下文，也就更有可能回答出那句 嗯? 我好像看到蘑菇了? 你放蘑菇了对吧, 你放了对吧!.
  - 它可以通过提示词定制化一些任务，比如说，需要电池缺陷图像分析的任务这种比较细致的任务，就可以让模型在做 summary 时更多分析细节，表面.
- 缺点
  - 贵，不是一般的贵。每张图都要单独做一次提取，后多图还要再发一次。而提升还得图越多越明显，一两张图的反而没必要这么做。所以这个方法不应该被作为一个默认方法，而是一个额外的可开启的选项.
  - 慢，即使用了并发，它也比直接对话要多出至少一轮的对话回复时长.
- 应用 map-reduce 方法
  - 逻辑是准备十张图片，实际上是五张复制成两份
  - 确实也有个比较大的问题就是 token 消耗和上下文增长速度过快的问题。并发单张已经是不小的消耗了。而把输出的结果整合进原本的上下文会让上下文增长速度非常快，让长上下文的注意力瓶颈问题更早的出现。

- ## 🆚🛢️ [【Wiki】语言模型区分题库：从文本到多模态 _202602](https://linux.do/t/topic/286836)

- ## 🆚 [Show HN: Benchmarking VLMs vs. Traditional OCR | Hacker News _202502](https://news.ycombinator.com/item?id=43118514)
  - we released the Zerox package last year (https://github.com/getomni-ai/zerox). And we wanted to put some numbers behind it. So we’re open sourcing our internal OCR benchmark + evaluation datasets.
  1. We are using JSON accuracy as our primary metric. The end goal is to evaluate how well each OCR provider can prepare the data for LLM ingestion.
  2. This methodology differs from a lot of OCR benchmarks, because it doesn't rely on text similarity. We believe text similarity measurements are heavily biased towards the exact layout of the ground truth text, and penalize correct OCR that has slight layout differences.
  3. Every document goes Image => OCR => Predicted JSON. And we compare the predicted JSON against the annotated ground truth JSON. The VLMs are capable of Image => JSON directly, we are primarily trying to measure OCR accuracy here. Planning to release a separate report on direct JSON accuracy next week.

- As far as I'm concerned, all of these specialty services are dead compared to a generalized LLM like OpenAI or Gemini.
  - I wrote in a previous post about how NLP services were dead because of LLMs and obviously people in NLP took great offense to that. But I was able to use the NLP abilities of an LLM without needing to know anything about the intricacies of NLP or any APIs and it worked great. This post on OCR pretty much shows exactly what I meant. Gemini does OCR almost as good as OmniAI (granted I've never heard of it), but at 1/10th the cost. OpenAI will only get better very quickly. Kudos to OmniAI for releasing honest data, though.
  - Sure you might get an additional 5% accuracy from OmniAI vs Gemini but a generalized LLM can do so much more than just OCR.

- OCR seems to be mostly solved for 'normal' text laid out according to Latin alphabet norms (left to right, normal spacing etc.), but would love to see more adversarial examples. We've seen lots of regressions around faxed or scanned documents where the text boxes may be slightly rotated (e.g. https://www.cad-notes.com/autocad-tip-rotate-multiple-texts-...) not to mention handwriting and poorly scanned docs. Then there's contextually dependent information like X-axis labels that are implicit from a legend somewhere, so its not clear even with the bounding boxes what the numbers refer to. 
  - This is where VLMs really shine: they can extract text then use similar examples from the page to map them into their output values when the bounding box doesn't provide this for free.

- Looking at the sample documents, this seems more focused on tables and structured data extraction and not long-form texts. The ground truth JSON has so much less information than the original document image. I would love to see a similar benchmark for full contents including long-form text and tables.

- The benchmark I most want to see around OCR is one that covers risks from accidental (or deliberate) prompt injection - I want to know how likely it is that a model might OCR a page and then accidentally act on instructions in that content rather than straight transcribing it as text.

- ## 🆚 [Docling, how does it work with VLM? : r/LocalLLaMA _202511](https://www.reddit.com/r/LocalLLaMA/comments/1p9zvkl/docling_how_does_it_work_with_vlm/)
  - i have a need to convert PDF to text for data extraction. Regular/Traditional OCR does very good job but unfortunately it does not take into consideration the layout, so while each word is perfectly recognized the output is a gibberish (if you try to read it). Understood each word but actual text does not make sense.
  - VLMs, such as Qwen3-VL or OpenAI do a good job producing markdown considering layout, so it makes sense but unfortunately the actual OCR is not nearly as good. It hallucinates often and no coordinates where the word was found.
  - So now, i am looking at Docling, it's using custom OCR but then sends for processing to VLM.
  - Question is, What is the output of Docling? Docling tags which is a "marriage" of two worlds OCR and VLM?
  - how does it marry VLM output with OCR output? Or is it one or another?

- ## [Show HN: PDF to MD by LLMs – Extract Text/Tables/Image Descriptives by GPT4o | Hacker News _202409](https://news.ycombinator.com/item?id=41614126)
- Does it do image to MD too?
  - Unless the only thing you want is a description of the image, then the real answer is NO. You can get an LLM to do something like "If you encounter an image that is not easily convertable to standard markdown, insert a [[DESCRIPTION OF IMAGE]] here." placeholder, but at that point you've lost information that may be salient to the original PDF.
  - The reason is because these multimodal LLMs can give you descriptions/OCR/etc., but they cannot give you quantifiable information related to placement.
  - You almost need segmentation system middleware that the LLM can forward to which can cut out these images to use in markdown syntax: ! `[A tiger burning brightly](/assets/images/tiger.png)`

- you can customize this as you wish by adding it to your prompt.

- ## LlamaIndex - We’ve written a new blog post on the specific areas in which LLMs are useful for document OCR - beyond the naive answer of “screenshot everything into a VLM”
- https://x.com/jerryjliu0/status/1991624512656535664
  - Existing techniques were hand-tuned, brittle/didn’t generalize, and lacked general semantic understanding
  - LLMs are helpful for zero-shot semantic layout reconstruction
  - VLMs are helpful for both visual layout understanding as well as specialized element understanding (tables, charts)
  - So LLMs and VLMs are both more general and zero-shot. By themselves they don’t solve PDF parsing, but the trick is to incorporate them in targeted ways as part of this next-gen OCR pipeline.

- LLMs and VLMs aren’t magic alone but combining them smartly really moves the needle for document parsing

- How do you solve the issue of "off by one row" kind of problems when there is a table in page and the rows are kinda close to each other?
# discuss-pm-ocr/translation
- ## 

- ## 

- ## 

- ## [有没有能够搜索图片上文字内容的软件？ ](https://linux.do/t/topic/1512595/4)
- [Anytxt Searcher | A Desktop Search Tool with A Powerful Full-Text Search Engine. Best Google Desktop Search Alternative.](https://anytxt.net/)
  - AnyTXT Searcher has a powerful document parsing engine, which extracts the text of commonly used documents without installing any other software and combines the built-in high-speed indexing system to store the text’s metadata
  - It works perfectly on Windows 11, 10, 8, 7
  - OCR. Text In Any Image (png, jpg, bmp, scanned pdf etc.)
- 如果文件比较多，而且有不少需要 ocr 的 pdf 的话，它可能会在空闲的时候占用大量内存和 CPU，最好让它只索引图片所在的文件夹。

- 把所有图片放一起，全选右键，用 Adobe Acrobat 软件将图片合并为一个 pdf，找到编辑 (软件会自动进行 ocr 识别)，然后 ctrl+f 查找
  - 图片不断增加的，合并为 pdf 不方便

- 解决方法都是建索引。像 硅机、Nebius 等国产资源囤了好一些正经生产又用不上的可以用来自己跑个 OCR 存数据库，能把 内容⇋文件名 关联起来，不过不能直接结合 Windows 用不是很方便。

- ## [有没有能截屏自带图像翻译的开源软件 ](https://linux.do/t/topic/1445800)
  - 覆盖在原文位置的，不是单独弹框翻译的那种。 类似微信图片翻译的效果的。

- pixpin可以的，你试试

- 这种肯定都是要配外部 API 的，不可能为爱发电内置图片翻译。
# discuss-tips
- ## 

- ## 

- ## 

- ## 

- ## agentic ocr skill with multi-turn feedback with codex spark >> everything.
- https://x.com/tokenbender/status/2025587371543257091
  - [Updated global OCR combo: ocr-refiner + pdf-ocr-feedback](https://gist.github.com/tokenbender/4efebb0baeeec7cab3059cddf603b49d)
- Multi-turn feedback loops for OCR is a solid pattern - the agent correcting its own extraction before moving on makes a lot of sense for messy docs. How many feedback rounds do you typically see before accuracy plateaus? Wondering if there's a sweet spot before the token cost outweighs the gains.

- ## 🌰 [Local VLMs for handwriting recognition — way better than built-in OCR : r/Supernote _202512](https://www.reddit.com/r/Supernote/comments/1pqs7zy/local_vlms_for_handwriting_recognition_way_better/)
- I also experimented with with tessaract and was heavily disappointed. I agree that local VLM is the way to go, but that latency is kinda off putting. 

- Not only on-device recognition is not on par, but it is also too slow to be usable. Doing OCR, exporting the file somewhere, looking it up on the computer, etc... too slow and pointless. And it does nothing for my memory retention.
# discuss-solutions
- ## 

- ## 

- ## 

- ## [Most efficient way to classify rotated images before sending them to a VLM : r/LocalLLaMA](https://www.reddit.com/r/LocalLLaMA/comments/1pku9qo/most_efficient_way_to_classify_rotated_images/)
  - I have seen paddleocr supports it natively. But I still need a generic option which can work with others

- You could try using OpenCV to detect text orientation - it's pretty lightweight and works well for documents with regular text layouts. Just run a quick angle detection before your VLM pipeline
  - That works for slightly tilted or skewed texts right, afaik. Does it work for complete 90 or 180 degree rotations?

- Tesseract OCR engine orientation and script detection (OSD). It detects 90, 180, 270 degrees of rotation. https://pyimagesearch.com/2022/01/31/correcting-text-orientation-with-tesseract-and-python/
  - I did look into tesseract as well, hoping there was something lighter than this

- ## [现在怎么处理pdf文件呢 ](https://linux.do/t/topic/1420032)
- 可以用mineru提取出来，然后把图片的位置替换为对应的图片描述，gemini可以直接解析，我猜测他们应该也是对pdf做了解析，将其转为了文本；或者把pdf为每一页提取为一张图片给LLM进行处理
  - pymupdf 我是使用这个库，然后把图片给大模型解析，最后再替换 但时候这个库处理表格 解析的时候有点问题，直接按照文字提取的话 就看不出这个是表格数据了

- mineru会把表格解析成html的格式，效果还可以，但是对于一些复杂的表格，也不能保证百分百正确，你可以先大概测试一下，看一下表格的解析是否有问题，如果会出现解析错误的情况的话，可能得通过多种方式对表格分别进行解析，比如分别使用mineru、paddle，gemini等对这个表格进行解析，然后在保证结果都相同的情况下确认这个表格是被正确解析的。
  - 你直接去对mineru解析出来的中间结果进行处理，最后把处理的结果全部拼接起来，不要直接在他输出的md文档上处理。

- ## 💡 [Qwen3-VL works really good with Zoom-in Tool : r/LocalLLaMA _202511](https://www.reddit.com/r/LocalLLaMA/comments/1osiog7/qwen3vl_works_really_good_with_zoomin_tool/)
  - While Qwen3-VL-30B-A3B(Q6_ud) performs better than previous open-source models in general image recognition, it still has issues with hallucinations and inaccurate recognition.
  - On my own frontend implementation with zoom_in, Qwen3-VL can zoom in on the image, significantly improving the accuracy of content recognition. 
  - For those who haven't tried it, qwen team has released a reference implementation: https://github.com/QwenLM/Qwen-Agent/blob/main/examples/cookbook_think_with_images.ipynb

- This is what o3 did with it's visual reasoning agent, I think it should be incorporated with every VLM system it's that good - outperforms pretty much every other model in complex problems (even ones better at full-size native image comprehension like Gemini and Opus).
  - I agree that every VLM should have such tools. The official Qwen website provides these tools for Qwen-Max, but not for the 30B model. I suspect that the smaller Qwen models may suffer from repetition issues, which could cause tool usage to fail at high probabilities. (30B-A3B tends to repeat when calling multiple tools in my daily usage.)

- tools are allowed to return images???
  - MCP protocol does not work well with images. Qwen-Agent saves picture to local disks and tools receive their filenames then go to read the file.

- ## [MinerU 到底是模型还是工程产品 - V2EX](https://v2ex.com/t/1170882#reply10)
- MinerU 分为两个 backend
  - 一个是 pipeline ，集成了多种文档相关的模型，并基于后处理合并完成文档解析；
  - 另一个是 vlm backend ，目前 2.5 版本是一个 qwen 架构 1.2B 的 vlm 模型，这个模型分为两阶段，一阶段是对版面进行分析，获取区域、区域类别、区域顺序，二阶段是对区域进行解析，提取文本、表格、公式，最后后处理合并。
  - 他们的输入输出是一致的（功能一致），但使用的技术不同，效果和性能也有差异，需要根据自己场景按需选择。
- paddleocr 在 MinerU pipeline backend 被集成（完成 ocr ），但 vlm 后端两者完全没有关联

- ## LGM：生成高质量3D模型，支持文字生成模型、图片生成模型，分辨率512*512，5秒内即可生成。
- https://x.com/Gorden_Sun/status/1784230776311284205
  - https://github.com/3DTopia/LGM

- ## 免费玩的本地大模型，本地搭建环境推荐用Ollama和ChatbotAI
- https://x.com/vista8/status/1862696894172209476
- Vision 建议换成用 Llama 3.2 Vision 11b，比llava要好很多，且支持多语言（包括中文）的文字识别

# discuss-ocr
- ## 

- ## 

- ## 🆚 [GLM OCR对比Deepseek OCR 2 _202602](https://linux.do/t/topic/1563022)
- Deepseek OCR 我觉得文字识别这一块还不如 Gemini
  -  GLM OCR 任务 2 可以比 Gemini 还要强
- 我希望他们出个真正的多模态，能够读懂图片和视频

- ## [ocr 识别文字，哪个模型好？ _202602](https://linux.do/t/topic/1560543)
- gemini 用 3.0falsh 正确率应该有 95% 以上
  - 2.5 pro 正确率接近 100%

- paddle ocr 最好用了（用 docker 部署），其他的都花里胡哨的

- 手写的试过 paddle、ds、qwen，准确率基本上只能达到两三成

- Qwen3-VL-8B 虽然是视觉模型，但 OCR 效果其实也不错。

- glm-ocr 确实很强，而且很小，速度飞快，ollama 内建支持，直接就能用，都不需要配置 py 环境

- ## DeepSeek刚刚发布了OCR-V2! 用LLM替代CLIP, _202601
- https://x.com/karminski3/status/2016037684737933489
  - 用 LLM 架构直接替掉传统的 CLIP 视觉编码器！
  - CLIP 是 OpenAI 搞的一个视觉编码器，通过海量图文对比学习，让模型能把图像"翻译"成语言模型能理解的向量。DeepSeek-OCR V1 就用的 CLIP VIT (300M参数)，效果已经很不错了。但问题是，CLIP 天生是为"图文匹配"设计的，不是为"按顺序读文档"设计的——它看图像就像拍照片，一眼看全局，但不会像人一样"从头读到尾"。
  - DeepSeek-OCR-2 的核心创新叫**视觉因果流 (Visual Causal Flow)**，说白了就是让模型学会"智能阅读"。怎么做到的？用 Qwen2-0.5B 这个小型 LLM 替代 CLIP 做视觉编码——所谓视觉编码，就是把一张图片转换成一串数字序列（token），让语言模型能"看懂"图片内容。
  - 可学习的 "causal flow tokens"（因果流token）。简单理解就是，模型会生成一组"阅读指针"，这些指针可以自己学习按什么顺序去关注图像的不同区域。
  - 图像本来是2D的（有横有纵），但语言模型只能处理1D序列（一个字接一个字）。传统做法是把图像暴力展平，从左上角扫到右下角，这样复杂图案空间关系全乱了。
  - DeepSeek-OCR-2 的做法更聪明：第一层，让视觉token用双向注意力互相"看见"，保持2D空间感知（知道谁在谁旁边）；第二层，因果流token按语义逻辑重新排序（先看标题、再看正文、表格单独处理）。两层配合，就像先画一张内容地图，再规划最优阅读路线——用1D的阅读顺序，还原出2D的文档结构！

- ## 🆚⚡️ [70个模型！中文手写OCR评测更新【系列评测三】 _202601](https://linux.do/t/topic/1466649)
  - 本次共涵盖 70 个不同模型，测试样本达到 31 个，且新增数个来自中学的实拍非互联网样本。
  - 本次测试还更新了含标点、不含标点两种模式，更能符合实际不同需要参考！
  - 本次更新使用了更合理的准确率计算方式，修正了此前样本的正确答案中存在的一些纰漏。
- 中文手写准确率省流/总结
  - 冠军：Gemini3Pro（含标点/不含标点都是最强）
  - 最强国产多模态（含标点）：Doubao-1.5-UI-TARS（但快下架了）
  - 最强国产多模态（不含标点）：ERNIE-5.0-Thinking-Preview（文心5.0）
  - 最强"小"模型：Qwen3-VL-8B-Instruct / PaddleOCR-VL（0.9B，不支持提示词）。小参数大模型仍存在死循环、乱回现象，并非很可靠。
  - 最推荐本地运行：PaddleOCRv5_Server。经典的、超小超快的非大模型，不用GPU都能爽用，准确率仍不输很多大模型，业务可定制性高，可输出文字框坐标、置信度，低成本、易部署、易二次开发。
  - GPT/Claude/Grok 依旧拉跨，不用期待。
- 所有参测大模型温度设置为0.1，使用提示词如下：
  - 你是一个强大的OCR引擎，尤其擅长处理中文手写字符。请直接精确地返回图片中的所有的字符，不附带任何其他无关内容。全部使用中文标点符号。遵循原图的标点使用情况，不管是否合理，有标点才加上，没有就没有。对于手写涂改，例如插入、划掉、调换位置等，只要遵循涂改规则后的文本。
- 评测说明
  - 非大模型/不支持提示词输入/不支持温度设定的参赛选手，有夸克扫描（QuarkScan）、PaddleOCR-VL、PaddleOCRv5-Server、HunyuanOCR等。
  - 所有模型重复5遍测试，5次结果均计入最终计算。准确率基于CER计算，计算大模型返回文本与正确答案的CER值，然后用1-CER得到准确率。
  - 少于32B的各模型，在上述设定下，有概率出现死循环现象，此时会给额外机会，删掉死循环那一次结果，再次发起新的请求，否则无法出分（超长死循环会导致CER爆炸，准确率归零）。
  - 以 Q4/Q8 结尾的模型均为 Windows 下通过 LMStudio 本地运行。此外，HunyuanOCR 为本地 WSL2 下通过 vLLM 部署运行，PaddleOCRv5-Server、PaddleOCR-VL 为本地直接通过paddleocr库推理运行。
  - 还有些模型，尝试了测试，但最终未完成，未计算成绩，包括 DeepSeek-OCR（困难样本空回复）、DeepSeek-VL2（困难样本死循环、空回复）、Grok系列（已读乱回）等。
  - 即使是0.1的温度，很多模型的表现也有不少波动，重测一遍一个模型都可能会有排名上的变化，因此笔者认为，1%以内差距的模型表现可视为同一水平。
- 厂商模型表现简评
- Gemini 系列的多模态能力强势已久，在本次评测中，Gemini-2.5-Pro 表现终于超过了 Gemini-2.0-Flash，表现出了符合名字的水平。 网传的 Gemini-3-Pro 的“最强多模态模型”称号也再次在本测试中得到验证。无论是在有标点还是无标点中，都夺得头筹。Gemini-3-Flash 也紧随其后，两种场景中都位列第三。
  - 在中文手写OCR这个领域，Gemini 冠军地位并不牢固，两种场景中，Pro 和 Flash 之间都被国产大模型横插一脚，且成绩上的差距相当小，甚至可以说是误差。
  - 提一嘴 Gemma 系列，只能说对于中文手写识别非常差，应该是训练集这方面数据相当缺乏的结果，甚至不如同是国外的 NVIDIA 训练的 Nemotron-Nano-12B-v2-VL 。
  - 总之，至少在当下，想要最好的中文手写OCR效果，首选 Gemini-3-Pro 毋庸置疑；而 Gemini-2.0-Flash 仍然表现出非常高的性价比。
- Baidu是OCR的老牌选手了，大模型出来之前，国内OCR开发，百度开源的PaddleOCR一直备受青睐，虽然有些毛病，但是并没有显著强于PaddleOCR的开源竞品。
  - PaddleOCR升级到了v5版本，性能更上一层楼，更推出了大模型版本PaddleOCR-VL。
  - PaddleOCRv5_server 仅仅 0.07B 的参数量，超过了相当多的对手。值得注意的是，笔者的测试里，中文手写有不少非常潦草、不规整换行、涂涂改改的样本，对于一般的日常用途，PaddleOCRv5_server相信能表现好很多。
  - 所以 PaddleOCRv5_server 是笔者最推荐本地跑OCR的，当然，如果你需要OCR的同时做一些文本层面修改（不容易用算法实现的），那还是要依赖大模型的提示词来做的，PaddleOCRv5_server 只是一个“传统”的 OCR 模型。
  - PaddleOCR-VL-0.9B 也表现亮眼，在含标点/不含标点两种场景下，在中文手写识别这个特定任务中，都能基本持平 Qwen3-VL-8B ，是一个相当高性价比的选择。
  - 缺点呢，和上面一样，都是不支持提示词来额外做调整。
  - 百度最新的 ERNIE-5.0，即文心5.0，也没给百度丢份儿，妥妥的第一梯队，不输甚至超越 Qwen3-VL-235B 大杯版，不过定价也是其三倍
- 笔者觉得目前国内 Doubao 是最像 Gemini 的模型，从 1.5 版本后主力模型全部多模态，文字推理能力不差，视觉理解在国内也是领先的。
  - 1.5-UI-TARS 版本在 Doubao 家族中，至今仍是最强。笔者猜测，有可能是为了 UI 任务，特意强化了下 OCR 的能力，但是该模型即将下架。紧随其后的是 1.6 版本衍生的 Vision 模型，很对得其模型名字的表现。
  - Lite 结尾的模型，表现就比较一般了。
  - Doubao 的优势就是，相比其他大厂，API服务好用且大方。各模型的训练完成度都不错，没看到什么死循环、不遵循指令乱回无关内容的问题。默认的 RPM 、并发请求数都不低。
- Qwen3-VL-235B-A22B-Instruct 在含标点/不含标点两种场景下，分别排名第4、第7；当然，就如前面所说，前面几名其实差距都很小，可以说都是第一梯队。
  - 对于 Qwen 家的模型来说，Instruct 版本似乎都比 Thinking 版本在OCR上表现更好，在235B这种大杯参数上亦是如此。对于 API 调用来说这是好事，用 Instruct 版成本也就更低了。
  - 随开源大杯的大模型是 Qwen3-VL-Plus，这是基于 Qwen3 系列的表现最好的闭源版本。
  - 值得注意的是，默认的百炼平台中的 Qwen-VL-Plus 和 Qwen-VL-MAX 的最新版本号都停留在8月份，也就是说仍然是基于 Qwen2.5 系列的
  - Qwen-VL-OCR 这个看起来特化的OCR版本，表现一如第二期的拉跨，也许这个OCR是更针对印刷文字而非手写文字吧。Qwen2.5-VL-72B 已经掉到了中部，但免费渠道似乎不少，也堪用。
  - Qwen3-VL-8B-Q4 就超过了非常多大模型，包括 Qwen-VL-MAX 系列、Qwen2.5-VL-72B 这些在第二期中表现良好的模型，但也不是说就很完美，即便设定温度1.0，对于部分困难样本， Qwen3-VL-8B 包括云端 API 版本，仍然逃不出小模型容易死循环、表现不稳定的规律。
  - 至于 4B 版本，也还行，但是不如 PaddleOCRv5_server，在 OCR 任务上实用性不高。
- 最后说说，夸克扫描（QuarkScan）这个非大模型的产品，笔者是使用其中的【提取文字】功能测试的，居然表现出了非常强的准确率。对于个人用户，不是特别在乎隐私的话，非常推荐，且使用应该是免费的。
- 腾讯一直是国内发展比较慢的，在多模态能力上也表现如此，最新的改名后的 Tencent-HY-Vision-1.5 勉强打赢 Qwen3-VL-8B，有待继续努力。
- olmOCR-2-7B，表现挺好的，且训练完成度比较好，没什么死循环；值得注意的是，这个是基于 Qwen2.5-VL-7B-Instruct 进行训练的，如果能更新个版本基于 Qwen3-VL-8B 训练的估计能再上一层。
- 智谱家的，GLM4.6V，不知道为啥输给了GLM-4.6V-FlashX，但数据如此就如实写吧。表现中规中矩，反正目前GLM没有能上第一梯队的视觉模型，有待进步。
- InternVL系列，来自上海人工智能实验室，就是把Qwen系列的文本模型加上视觉训练出来的，InternVL3-78B 底座为Qwen2.5-72B，InternVL3.5-241B-A28B 来自 Qwen3-235B-A22B，就成绩上来看，距离 Qwen 自家训练的同底座视觉版本差距不小。
- GPT系列，嗯，还是那个样子，GPT-4.1-Mini 表现最好，其次是 GPT-5.2 ，感觉没啥能说的，反正应该没人用GPT来做中文手写OCR。如果有汉字需要识图 + GPT 的推理，感觉用其他模型识别出来再给 GPT 能表现更好。对了，GPT5.2以下（不含5.2）对于很多困难样本会拒绝输出，直接说【看不清楚，请提供更清晰的图片或更高分辨率的扫描件。】，重试很多次都是如此，最终成绩还是算了进去。
- Claude系列，嗯，也还是那个样子，和 GPT 一样，估计训练集都不放什么汉字图片数据的。最新的基于TPU训练的 Claude-Opus-4.5，也就那样，都是难以使用的水平。

- 佬友的评测代码有开源计划吗？这边也有OCR类的场景想要测试下不同模型的能力，想参考下评测过程。
  - 短时间内应该不开源，将来优化下会考虑开源，主要是现在的问题比较多，很多时候都是手动修修改改的，现在开源的话文档都写不了，完善一些后应该会开源的，加上年末事情多，可能要到四五月份吧

- 样本里面含手写公式吗
  - 不含的，公式识别一般是专门另测的。

- 之前测过glm4.6v和paddleOCR感觉前者更好用一些，因为可以根据我的需要返回内容
  - 是的，文中也说了，PaddleOCR是不支持提示词指令的

- 从官方技术报告和GitHub issues来说，DeepSeek-OCR应该更擅长版面解析/规整字识别，中文手写识别应该没有纳入训练目标，本次评测如果放个低分DeepSeek-OCR可能会导致低估其他方面能力，最后考虑下来就不计入了。

- ### [中文手写OCR评测【系列评测二】 _202505](https://linux.do/t/topic/687651)
- ### [中文OCR哪家强？【系列评测一】 _202505](https://linux.do/t/topic/671030)

- ## [Run structured extraction on documents/images locally with Ollama and Pydantic | Hacker News _202502](https://news.ycombinator.com/item?id=43110173&utm_source=chatgpt.com)
  - We put together an open-source collection of Pydantic schemas for a variety of document categories (W2 filings, invoices etc.), including instructions for how to get structured JSON responses from any visual input with the model of your choosing. Run everything locally.

- I'd really like to play with Qwen2.5-VL at some point, perhaps for reading data-sheets for microchips. Nicely for some applications, it's also very good at reporting position of what it finds, which many ML tools are pretty mediocre at. https://qwenlm.github.io/blog/qwen2.5-vl/

- ## [Any suggestions for Open source OCR tools [D] : r/MachineLearning _202510](https://www.reddit.com/r/MachineLearning/comments/1o4hn2c/any_suggestions_for_open_source_ocr_tools_d/)
- The biggest difference maker is whether you're using OCR for word- or sentence-level recognition with bounding boxes, or simply to transform non-textual info in textual info (say Markdown, or similar textual representations).
  - disclaimer: I'm assuming the latter, many people have already replied back with valuable recognition software.
  - IMHO Docling powered by the very cheap and efficient granite-docling-258M is your best friend, fully running on CPU and suitable for bulk operations.

- 
- 
- 
- 
- 
- 

- ## [OCR4all | Hacker News _202502](https://news.ycombinator.com/item?id=43043671)
- A little secret: Apple’s Vision Framework has an absurdly fast text recognition library with accuracy that beats Tesseract. It consumes almost any image format you can think of including PDFs.
  - After getting an iPhone and exploring some of their API documentation after being really impressed with system provided features, I'm blown away by the stuff that's available. My app experience on iOS vs Android is night and day. The vision features alone have been insane, but their text recognition is just fantastic. Any image and even my god awful handwriting gets picked up without issue.

- The problem with doing OCR with LLMs is hallucination. It creates character replacements like Xerox's old flawed compression algorithm. 
  - Graybeards like Tessaract has moved to neural network based pipelines, and they're re-inventing and improving themselves.
  - I was planning to train Tessaract with my own hand writing, but if OCR4All can handle that, I'll be happy.
- Paradoxically, LLMs should be the tool to fix traditional OCR by recognizing that "Charles ||I" should be "Charles III", "carrot ina box" should be "carrot in a box", the century of the event in context cannot be that construed through looking at the gliphs etc.
  - As someone who's learning how to do OCR in order to re-OCR a bunch of poorly digitized documents, this will not work with modern OCR. Modern OCR is too good.
  - If you're able to improve the preprocessing and recognition enough, then there's a point at which any post-processing step you do will introduce more errors than it fixes. LLM's are particularly bad as a post-processing step because the errors they introduce are _designed to be plausible_ even when they don't match the original text. This means they can't be caught just by reading the OCR results.
  - I've only learned this recently, but it's something OCR experts have known for over a decade, including the maintainers of Tesseract. 
  - OCR is already at the point where adding an LLM at the end is counterproductive. The state of the art now is to use an LSTM (also a type of neural network) which directly recognizes the text from the image. This performs shockingly well if trained properly. When it does fail, it fails in ways not easily corrected by LLM's. I've OCR'ed entire pages using Tesseract's new LSTM engine where the only errors were in numbers and abbreviations which an LLM obviously can't fix.
- Tesseract wildly outperforms any VLM I've tried (as of November 2024) for clean scans of machine-printed text. True, this is the best case for Tesseract, but by "wildly outperforms" I mean: given a page that Tesseract had a few errors on, the VLM misread the text everywhere that Tesseract did, plus more. I strongly suspect that traditional OCR systems will become obsolete, but we aren't there yet.

- Tesseract worked fine until the hand written part, then garbage. 

- I also made an AI assisted OCR API 
  - It combines Tesseract (for images) and Poppler-utils (PDF). A local open-source LLMs will extract document segments intelligently.

- I think the current sweet-spot for speed/efficiency/accuracy is to use Tesseract in combination with an LLM to fix any errors and to improve formatting, as in my open source project which has been shared before as a Show HN: https://github.com/Dicklesworthstone/llm_aided_ocr

- I maintain a searchable archive of historical documents for a nonprofit, OCR'd with Tesseract over several years. Tesseract 4 was a big improvement over previous versions, but since then its accuracy has not improved at the same rate as other free solutions.
  - These days, just uploading a PDF of scanned documents (typeset ones, not handwriting) to Google Drive and opening with Google Docs results in a text document generated with impressive quality OCR.
  - But this is not scriptable, and doesn't provide access position information, which is needed so we can highlight search results as color overlays on the original PDF. Tesseract's hOCR mode was great for that.
  - For the next version, we're planning to use one of the command-line wrappers to Apple's Vision framework, which is included free in MacOS. A nice one that provides position information is at https://github.com/bytefer/macos-vision-ocr

- Apple Vision and its wrappers provide bounding boxes for each line of text. That's slightly less convenient than Tesseract which can give you a bounding box for each word, but more than compensated by Apple Vision's better accuracy. I am planning to fudge the word boxes by assuming fixed-width letters and dividing up the overall width so that each word's width is proportional to its share of the total letters on the line.
  - Once you have those bounding boxes, it's pretty simple to use a library like (Python) or (JavaScript) to add overlay text in the right place
- https://github.com/eloops/hocr2pdf /MIT/202509/js/inactive
  - take scanned image, and hocr output from tesseract, create PDF. Thats it.

- ## [LLM Aided OCR (Correcting Tesseract OCR Errors with LLMs with Python) : r/Python _202408](https://www.reddit.com/r/Python/comments/1eo6dxz/llm_aided_ocr_correcting_tesseract_ocr_errors/)
- Nice job! I was looking at your code and noticed you are using regex to split sentences. From my own experience I know that is not ideal for this kind of job. You could try using the spaCy open source library to split sentences with NLP. It has an incredible 99% accuracy (meaning that sometimes two sentences will be grouped into a paragraph). This way you can avoid false positives like “I know Dr. Evil” being split into two separate sentences because of the dot after the abbreviated word.
  - Thanks. It’s actually not that sensitive to that because each chunk shown to the LLM contains a portion of the previous chunk so that the LLM has the context. So it doesn’t really affect the quality of the output either way.

- ## [Show HN: LLM-aided OCR – Correcting Tesseract OCR errors with LLMs | Hacker News _202408](https://news.ycombinator.com/item?id=41203306)
- In my experience, this works well but doesn't scale to all kinds of documents. For scientific papers; it can't render formulas. meta's nougat is the best model to do that. For invoices and records; donut works better. Both these models will fail in some cases so you end up running LLM to fix the issues. Even with that LLM won't be able to do tables and charts justice, as the details were lost during OCR process (bold/italic/other nuances). 
  - I feel these might also be "classical" methods. I have found vision models to be much better as they have the original document/image. 

- For any one curious on automating document processing end-to-end by leveraging llms do try Unstract. It is opens source. https://github.com/Zipstack/unstract
  - Unstract also has a commercial version of document agnostic parser which you can channel to any RAG projects. https://unstract.com/llmwhisperer/

- We've been trying to solve this with https://vlm.run: the idea is to combine the character level accuracy of an OCR pipeline (like Tesseract) with the flexibility of a VLM.
  - OCR pipelines struggle with non-trivial text layouts and don't have any notion of document structure, which means there needs to be another layer on top to actually extract text content to the right place. At the other end of the spectrum, VLMs (like GPT4o) tend to perform poorly on things like dense tables (either hallucinating or giving up entirely) and complex forms, in addition to being much slower/more expensive. Part of the fix is to allow a 'manager' VLM to dispatch to OCR on dense, simple documents, while running charts, graphs etc. through the more expensive VLM pipeline.

- If anyone is looking to compare results visually, I have created an open source OCR visualiser to help identifying missing elements (especially in tables). https://github.com/orasik/parsevision

- I did something similar about a decade ago because I was using tesseract to OCR Chinese.
  - Part of the problem is that if you use Tesseract to recognize English text it's much easier to clean it up afterwards because if it makes a mistake it's usually in only a single character, and you can use Levenstein distance to spellcheck and fix which will help a lot with the accuracy.
  - Logographic languages such as Chinese present a particular challenge to "conventional post-processing" having many words represented as two characters and often a lot of words as a single "glyph". This is particularly difficult because if it gets that glyph wrong there's no way to obvious way to detect the identification error.
  - The solution was to use image magick to "munge" the image (scale, normalize, threshold, etc), send each of these variations to tesseract, and then use a Chinese-corpus based Markov model to score the statistical frequency of the recognized sentence and vote on a winner. It made a significant improvement in accuracy.
- People's handwriting vary widely, and a human reading someone's writing faces the same problems you mention. For a language like English, humans also decipher unrecognized characters by looking at what letter would fix the word or what word would fit in the sentence, etc.

- I wonder if you could feed back the results from an LLM into the OCR model to get it to make better decisions. E.g., if it's distinguishing a 1 from an I, the LLM could provide a probability distribution.
  - Or the other direction. Tesseract can give you confidence levels for the guesses it makes about a symbol 

- ## [How can I determine OCR confidence level when using a VLM? : r/LocalLLaMA _202510](https://www.reddit.com/r/LocalLLaMA/comments/1oaum1r/how_can_i_determine_ocr_confidence_level_when/)
- One approach that works surprisingly well is running the same extraction twice with slightly different prompts and checking for consistency - if the VLM gives you different supplier names or amounts between runs, thats a strong signal the image quality is problematic and worth flagging for reupload.

- ## [Docling, how does it work with VLM? : r/LocalLLaMA _202511](https://www.reddit.com/r/LocalLLaMA/comments/1p9zvkl/docling_how_does_it_work_with_vlm/)
  - So i have a need to convert PDF to text for data extraction. 
  - Regular/Traditional OCR does very good job but unfortunately it does not take into consideration the layout, so while each word is perfectly recognized the output is a gibberish (if you try to read it). Understood each word but actual text does not make sense.
  - VLMs, such as Qwen3-VL or OpenAI do a good job producing markdown considering layout, so it makes sense but unfortunately the actual OCR is not nearly as good. It hallucinates often and no coordinates where the word was found.

- ## 🤔🆚 [Do we really need traditional OCR and layout models at this point, since VLMs have improved so much. : r/LocalLLaMA _202503](https://www.reddit.com/r/LocalLLaMA/comments/1jmcbsk/do_we_really_need_traditional_ocr_and_layout/)
- An affordable top-loading scanner can scan about 25 pages per minute.
  - If you needed to scan and OCR five hundred printed pages, how long do you think it would take a vision model to get it done?
  - Traditional OCR can work faster than the scanner scans pages, and on much more modest hardware.

- We are working on a pipeline to extract text from a specific type of paper documents. The best approach we found is to detect the layout, mask, extract using 3-4 different OCR models, majority vote, validate with VLM if there's a tie, check the output text syntax, grammar, etc with a larger LLM.
  - We are experimenting with <10B models for the VLM. The VLM comes in only to resolve conflicts, not systematically, because it's slooow in comparison to Trad OCR tools

- We use Qwen2.5 VL 72B to convert PDF files into markdown. Works significantly better than many OCR solutions out there, but it's also much slower than those.

- ## 🤔 [Replace OCR with Vision Language Models | Hacker News _202502](https://news.ycombinator.com/item?id=43187209)
- It’s an interesting idea, but still way too unreliable to use in production IMO. When a traditional OCR model can’t read the text, it’ll output gibberish with low confidence; when a VLM can’t read the text, it’ll output something confidently made up, and it has no way to report confidence. (You can ask it to, but the number will itself be made up.)
  - There’s no way to ground the model using the source text when the model is your OCR.
- Thing is, the majority of OCR errors aren't character issues, but layout issues. Things like complex tables with cells being returned under the wrong header.

- We recently published an open source benchmark specifically for evaluating VLM vs OCR. And generally the VLMs did much better than the traditional OCR models.
  - https://github.com/getomni-ai/benchmark
- VLM highlights:
  - Handwriting. Being contextually aware helps here. i.e. they read the document like a human would, interpreting the whole word/sentence instead of character by character
  - Charts/Infographics. VLMs can actually interpret charts or flow diagrams into a text format. Including things like color coded lines.
- Traditional OCR highlights:
  - Standardized documents (e.x. US tax forms that they've been trained on)
  - Dense text. Imagine textbooks and multi column research papers. This is the easiest OCR use case, but VLMS really struggle as the number of output tokens increase.
  - Bounding boxes. There still isn't really a model that gives super precise bounding boxes. Supposedly Gemini and Qwen were trained for it, but they don't perform as well as traditional models.
- There's still a ton of room for improvement, but especially with models like Gemini the accuracy/cost is really competitive.
- there are a few caveats to VLMs that folks are typically unaware of (not at all exhaustive, but the ones you highlighted):
  - 1. Long-form text (dense): Token limits of 4/8K mean that dense pages may go over limits of the LLM outputs. This requires some careful work to make them work as seamlessly as OCR.
  - 2. Visual grounding a.k.a. bounding boxes are definitely one of those things that VLMs aren't natively good at (partly because the cross-entropy losses used aren't really geared for bounding box regression). We're definitely making some strides here to improve that so you're going to get an experience that is almost as good as native bounding box regression (all within the same VLM). 

- LLMs and OCR have very different failure modes. 
  - With LLMs, there is unbounded potential for hallucination, and the entire document is at risk.
  - With OCR, errors are localized and have a greater chance of being detected when read.
  - I think for a lot of cases, the best solution is to fine-tune a model like LayoutLM, which can classify the actual text tokens in a document (whether obtained from OCR or a native text layer) using visual and spatial information. Then, there are no hallucinations and you can use uncertainty information from both the OCR (if used) and the text classification. But it does mean that you have to do the work of annotating data and training a model, rather than prompt engineering
- 100% this, combining traditional OCR with VLMs that can work with bounding boxes so that you can correlate the two is the way to go.

- An effective way that usually increases accuracy is to use an ensemble(乐团; 剧团; 歌舞团) of capable models that are trained independently (e.g., gemini, gpt-4o, qwen). If >x% of them have the same output, accept it, otherwise reject and manually review

- I've been using gemini 2 flash to extract financial data, within my sample which is perhaps small (probably 1000 entries so far), I've had one single error only so like a 99.9% success rate.
  - Many hallucinations can be avoided by telling it to use null if there is no number present.

- Modern OCR is astonishingly good, more importantly it's deterministically so. It's failure modes, when it's unable to read the text, are recognizably failures.
  - Results for VLM accuracy & precision are not good

- Tesseract doesn’t use an LLM. LLMs don’t know how confident they are; Tesseract’s model does.
  - Kind of. Tesseract's confidence is just a raw model probability output. You could easily use the entropy associated with each token coming out of an LLM to do the same thing.
- True, but LLM token probability doesn't map nearly as cleanly to "how readable was the text".
  - Why not though? Both kinds of models jumble around the data and spit out a probability distribution. Why is the tesseract distribution inherently more explainable (aside from the UI/UX problem of the uncertainty being per-token instead of per-character)?

- Why do all these OCR services only show examples with flawless screenshots of digital documents? Are there that many people trying to OCR digital data? Why not just copy the HTML?
  - If it's not intended for digital documents, where are the screenshots with fold marks, slipping lines, lighting gradients, thumbs, etc etc.

- You can also use it for robustness. Looking at e.g. historical censuses, it's amazing how many ways people found to not follow the written instructions for filling them out. Often the information you want is still there, but woe to you if you look at the columns one by one and assume the information in them to be accurate and neatly within its bounding box.

- What I want: take scan/photo of a document (including a full book), pass it to the language model, and then get out a Latex document that matches the original document exactly (minus the copier/camera glitches and angles). I feel like some kind of reinforcement learning model would be possible for this. It should be able to learn to generate Latex that reproduces the exact image, pixel for pixel (learning which pixels are just noise).

- You sort of have to use both. OCR and LLM and then correlate the two results. They are bad at very different things, but a subsequent call to a 2nd LLM to pair together the results does improve quality significantly, plus you get both document understanding and context as well as bounding boxes, etc.
  - A VLM that invokes ocr tool use is a compelling idea that could result in pretty good results, I would expect.

- The AI OCR build into snipping tool in windows is better than tesseract, albeit more inconvenient than something like powertoys or Capture2Text, which use a quick shortcut.

- I wonder what the speed of this approach vs traditional ocr techniques. Also, curious if this could be used for text detection (find a bounding box containing text within an image).

- qwen 2.5 vl was specifically trained to produce bounding boxes I believe.

- Existing solutions like Tesseract already can embed text into the image, but I'm wondering if there's a way to combine LLM with Tesseract, so that LLMs can help correcting results and finding unidentified text, and finally still embed text back to the image

- Can I use this to convert flowcharts to yaml representations?

- VLM's can't replace ocr one to one.. most hosted multimodal models seem to have a classical OCR (tesseract-based) step in their inference loop

- ## 🆚 [I benchmarked 7 OCR solutions on a complex academic document (with images, tables, footnotes...) : r/LocalLLaMA _202504](https://www.reddit.com/r/LocalLLaMA/comments/1jz80f1/i_benchmarked_7_ocr_solutions_on_a_complex/)
  - I ran a comparison of 7 different OCR solutions using the Mistral 7B paper as a reference document (pdf), which I found complex enough to properly stress-test these tools. It's the same paper used in the team's Jupyter notebook, but whatever. The document includes footnotes, tables, figures, math, page numbers, ... making it a solid candidate to test how well these tools handle real-world complexity.
  - Goal: Convert a PDF document into a well-structured Markdown file, preserving text formatting, figures, tables and equations.
  - Results (Ranked):
  - MistralAPI [cloud] → BEST
  - Marker + Gemini (--use_llm flag) [cloud] → VERY GOOD
  - Marker / Docling [local] → GOOD
  - PyMuPDF4LLM [local] → OKAY
  - Markitdown (without AzureAI) [local] → POOR* (doesn't extract images)

- New version of gemini flash seems to have improved further in my test.

- PyMuPdf uses Tesseract for OCR (just for OCR exactly, not whole process of reading document - so it's again the same "old" core solution - of course PyMuPdf have more features).

- ## [Best open-source model for parsing messy PDFs on 16GB RAM (CPU only) - Models - Hugging Face Forums _202510](https://discuss.huggingface.co/t/best-open-source-model-for-parsing-messy-pdfs-on-16gb-ram-cpu-only/168890)
  - My issue is:
  - Larger models don’t fit in my 16GB RAM system.
  - Smaller models run but give low accuracy.

- If you’re limited to 16GB RAM on CPU only, big models won’t fit unquantized. Best option is to:
  - OCR/Extract text first → use ocrmypdf or pdfplumber to clean up messy PDFs.
  - Parsing step → run a quantized 7B model (LLaMA-2 7B or Mistral-7B, 4-bit GGUF/GGML via llama.cpp). These fit in 16GB and give decent accuracy.
  - Optimize →
    - Quantize to 4-bit (saves memory).
    - Chunk PDFs so context isn’t too large.
    - Optionally train a LoRA adapter for insurance-specific fields.
- This combo (OCR + quantized 7B + a few regex rules) should give you the best balance of speed and accuracy on your setup.

- Honestly. Your specs are extremely inadequate. You’re wasting your time.

- I’ve got decent results with Qwen2.5-VL and InternVL3.5. There are also: MarkItDown, MinerU, olmOCR, Surya OCR worth trying. See also DocVQA and OCRBench benchmark leaderboards.

- ## [Is OCR accuracy actually a blocker for anyone's RAG/automation pipelines? : r/LocalLLaMA _202511](https://www.reddit.com/r/LocalLLaMA/comments/1oppykf/is_ocr_accuracy_actually_a_blocker_for_anyones/)
  - Or is "good enough" OCR + error handling downstream actually fine, and I'm overthinking this?

- this is literally my entire life for the past 8 years. We process millions of documents at Nanonets and OCR accuracy is absolutely the make-or-break factor. You're not overthinking it at all.
  - Financial documents are the absolute worst. Multi-column layouts, nested tables, footnotes that reference other footnotes... we spent months just on handling different invoice formats. 
  - Fine-tuning Qwen3-VL is smart - we went a similar route but ended up building our own models specifically for document understanding. Have you tried Docstrange btw? 

- Converting PDFs to images and sending each image to an LLM with context worked well, but it was too expensive.
  - Another approach was to cache the full PDF (such as a scanned or handwritten report) in the LLM, then query it later, e.g., “I need only page 5.”

- ## 在和客户沟通的时候，不在一线干活的某些专家也会说：OCR 问题已经被解决了。 直到我祭出真实场景的图。 Mistral OCR 连表格都识别成图片了
- https://x.com/9hills/status/1981603450254503992
- mineru和paddleocr应该都有试卷训练数据，可以试试。最保底的是gemini-2.5-pro

- Mistral识别表格的能力很强，你这个图其实不是OCR的问题，是还原被混淆图片的问题，如果非要OCR，那应该先用nano banana把公章去除。

- gemini-2.5-pro是通用模型，可能内部有些额外步骤，纯OCR的话Mistral已经做的非常好了，高质高速低价，你可以比较一下Gemini和Mistral OCR的速度

- 我觉得小的vlm 直接做端到端的 pdf->markdown  永远不会解决问题，稍微复杂点的edge case  就出错。最后可能还是得回到传统图像处理+vlm 的路子，先识别出格子和文字，然后连通坐标输到大模型生成markdown

- ## 🆚📝 [State of Open OCR models : r/LocalLLaMA _202510](https://www.reddit.com/r/LocalLLaMA/comments/1oe7orf/state_of_open_ocr_models/)
- [Supercharge your OCR Pipelines with Open Models _202510](https://huggingface.co/blog/ocr-open-models)
- Recent models transcribe texts into a machine-readable format.
- OCR models convert them into machine-readable text that comes in many different formats like HTML, Markdown and more.
- Models use different machine-readable output formats, such as DocTags, HTML or Markdown
  - The way a model handles tables and charts often depends on the output format they are using. 
- DocTag: DocTag is an XML-like format for documents that expresses location, text format, component-level information, and more. This format is employed by the open Docling models.
- HTML: HTML is one of the most popular output formats used for document parsing as it properly encodes structure and hierarchical information.
- Markdown: Markdown is the most human-readable format. It’s simpler than HTML but not as expressive. For example, it can’t represent split-column tables.
- JSON: JSON is not a format that models use for the entire output, but it can be used to represent information in tables or charts.

- Documents can have complex structures, like multi-column text blocks and floating figures. 
  - Older OCR models handled these documents by detecting words and then the layout of pages manually in post-processing to have the text rendered in reading order, which is brittle. 
  - Modern OCR models, on the other hand, incorporate layout metadata to help preserve reading order and accuracy. This metadata is called “anchor”, it can come in bounding boxes. This process is also called as “grounding/anchoring” because it helps with reducing hallucination.

- I just tried PaddleOCR and zero-shot worked super well
  - Indeed, that tiny 0.9B model does a perfect transcription and even beats the latest DeepSeek OCR. Impressive.
- for now you could try with vLLM I think, because PaddleOCR-VL comes in two models (one detector for layout and the actual model itself) it's sort of packaged nicely with vLLM AFAIK

- MinerU 2.5 and PaddleOCR both pretty much nail it. They don't do the subscripts but that's not native markdown so fair enough imo.

- [What are the best Open Source OCR models currently? : r/LocalLLaMA _202510](https://www.reddit.com/r/LocalLLaMA/comments/1okehd9/what_are_the_best_open_source_ocr_models_currently/)
- MinerU 2.5 and PaddleOCR-VL
- Paddleocr-vl, about 1B and best table extraction I’ve seen
- OLMOCR2, Deepseek-OCR, Chandra OCR

- ## [What is the best ocr model for converting PDF pages to markdown (or any text based format) for embedding? : r/LocalLLaMA _202510](https://www.reddit.com/r/LocalLLaMA/comments/1obha86/what_is_the_best_ocr_model_for_converting_pdf/)
- https://github.com/opendatalab/OmniDocBench
  - MinerU is best but bit annoying to get going
  - Dolphin and Marker are next best

- For the regular pdfs why not just use typical pdf text extraction tools? It is more accurate and has been done for forever. For the pdf images then yeah ocr makes sense.
  - I tried this, and some of my PDFs have corrupted text layers. I got a 114k line text file for a 10 page pdf, so I’d like to just ocr if possible for consistency

- Why even use a model for the OCR part itself? There are multiple tools designed specifically for that which will be far less consuming in both time and resources. I'm not being condescending, I'm just genuinely curious as to what's the benefits of using a model for that.

- ## [Nanonets-OCR2: An Open-Source Image-to-Markdown Model with LaTeX, Tables, flowcharts, handwritten docs, checkboxes & More : r/LocalLLaMA _202510](https://www.reddit.com/r/LocalLLaMA/comments/1o5nlli/nanonetsocr2_an_opensource_imagetomarkdown_model/)
  - We're excited to share Nanonets-OCR2, a state-of-the-art suite of models designed for advanced image-to-markdown conversion and Visual Question Answering (VQA).
  - It is trained on tons of financial documents. Since the output is in markdown with the tables as html, they can be converted to CSVs also. We have some samples examples for bank statements in the docstrange demo. 
  - `Nanonets-OCR2-1.5B-exp` is experimental model. Full training is not complete yet. We will release the final model when the full training is done.
  - We will add support for Ollama in coming days. Meanwhile you can use the Docstrange (https://docstrange.nanonets.com/). We do have api support there, incase of large volume.

- Can you tell me what are the exact advances over nanonets-ocr-s ? Specifically the 3B model.
  - Thanks. We have scaled our datasets by a lot (close to 3 million documents). New model should work better on multilingual, handwritten data, flowcharts, financial complex tables. 
  - This time we have added Visual Question Answering support. 
  - Fixed some of the edge-cases where model used to give infinite generation for empty tables and stuff. 
  - Also you should be able to change the prompt based on your use case. Nanonets-ocr-s does not work if you change the prompt much.

- tables will already be in html format. You can use this prompt for both getting complex table and header and footer.
  - Also for tables you should use `repetition_penalty=1` for best result. You can try in docstrange 
  - `user_prompt = """Extract the text from the above document as if you were reading it naturally. Return the tables in html format. Return the equations in LaTeX representation. If there is an image in the document and image caption is not present, add a small description of the image inside the <img></img> tag; otherwise, add the image caption inside <img></img>. Watermarks should be wrapped in brackets. Ex: <watermark>OFFICIAL COPY</watermark>. Page numbers should be wrapped in brackets. Ex: <page_number>14</page_number> or <page_number>9/22</page_number>. Prefer using ☐ and ☑ for check boxes."""`

- Can this model provide bboxes with recognized box types (header, text, table) via special prompts or special formats like it did qwen2-vl / qwen3-vl ?
  - We don't support boxes yet. That's in plan for next release.

- I do not see a comparison with the Docling document understanding pipeline from IBM.
  - We will add more evals. But generally in all evals Gemini models are in top. Thats why we first evaluated against Gemini. But for complex document these models, specially the 3B one should be better than docling.
- It will be better than mistral ocr. Our last model was better than mistral. This one is improvement on top of the last model.

- Small models like this one or Docling deliver phenomenal results when the PDFs you are dealing with are not overly complex. While they handle TeX-equations well, the difference to large LLMs becomes very obvious when presenting them graphics. 
  - Default model is trained to give small description. You can change the prompt to have detailed description. Since the model also supports VQA you can do multi-turn multiple questions.

- The issue of any ocr model its wide multilingual support. What about your model?
  - We have trained on multilingual as well as handwritten data.

- Did you also incorporate historical texts? I tried with 18th century fraktur and it often mixed up long s and f. There are quite good sets of historical training data available: https://zenodo.org/records/15764161
  - No we have not trained on historical texts, all the handwritten and multi-lingual datasets are recent data. This is because old text fonts are quite different from recent documents and texts, and these models were mainly used on recents documents. But if there is enough annotated datasets we can definitely include those in next iteration. Thanks for sharing!

- Tested with my handwritten diary (that none other model could parse anything at all) - and all text was extracted! Thank you

- Very cool and excited to see these models keep getting smaller! FWIW I've been building a collection of uv scripts that aim to make it easier to run these new VLM based OCR models across a whole dataset using vLLM for inference. They can be run locally or using HF Jobs. Just added this model to that repo! https://huggingface.co/datasets/uv-scripts/ocr

- ## [Are vision models (like qwen3-vl) good for OCR? : r/LocalLLaMA _202510](https://www.reddit.com/r/LocalLLaMA/comments/1nu7vw8/are_vision_models_like_qwen3vl_good_for_ocr/)
- Your concern about hallucination is totally valid but honestly the accuracy issues with traditional OCR like tesseract are way worse than occasional VL model hallucinations, especially for real world documents. 
  - I've been dealing with this exact problem for years and tesseract just falls apart with anything that isnt a perfect scan - weird fonts, slight rotations, quality issues, you name it. 
  - Vision models like qwen2.5-vl actually have much better accuracy because they understand context and can handle imperfect inputs way better than traditional engines.
  - The key is setting up proper prompting to minimize hallucinations - be very specific about what fields you want extracted and ask the model to indicate confidence levels or mark uncertain text.
  - We built Docstrange specifically for this use case and found that combining good prompting with validation rules catches most issues. For invoices and licenses, the structured nature actually helps a lot since VL models can understand document layout and context much better than traditional OCR engines that just see individual characters.

- I use Qwen2.5-VL for OCR all the time. Works great. I've OCR'd entire PDF scans of documents, and traditional OCR usually OCRs decently but has layout problems, whereas AI OCR usually does a good job of understanding and flattening layout. I've used it for Chinese, Japanese, German, and (of course) English.

- My best results for processing tabular PDFs has been: https://huggingface.co/ibm-granite/granite-docling-258M
  - Qwen-2.5 oddly either gives me great results, or the first row and nothing else.

- Gemma3 27b is pretty great for OCR.
# discuss-vlm 👾
- ## 

- ## 

- ## 

- ## 

- ## 

- ## 

- ## 🆚 [Benchmark Paper: Vision-Language Models vs Traditional OCR in Videos : r/LocalLLaMA _202502](https://www.reddit.com/r/LocalLLaMA/comments/1ioi4lm/benchmark_paper_visionlanguage_models_vs/)
  - A new benchmark paper just dropped evaluating how well Vision-Language Models (VLMs) perform compared to traditional OCR tools in dynamic video environments.
  - Three state-of-the-art VLMs – Claude-3, Gemini-1.5, and GPT-4o – were benchmarked against traditional OCR tools like EasyOCR and RapidOCR, using metrics such as Word Error Rate (WER), Character Error Rate (CER), and Accuracy.
  - VLMs outperformed traditional OCR in many cases, demonstrating robustness across varied video contexts.
  - Challenges persist – hallucinated text, security policy triggers, and difficulty with occluded/stylized text.

- ## 🆚 [VLM's vs PaddleOCR vs TrOCR vs EasyOCR : r/computervision _202505](https://www.reddit.com/r/computervision/comments/1kt3p8i/vlms_vs_paddleocr_vs_trocr_vs_easyocr/)
  - I am working on a hardware project where I need to read alphanumeric texts on hard surfaces(like pipes and doors) in decent lighting conditions. The current pipeline has a high-accuracy detection model, where I crop the detections and run OCR over that, but I haven't been able to achieve anything above 85%(TrOCR)(also achieved 82.56% on paddleOCR, so I prefer Paddle as the edge compute required is much lower)
- The PaddleOCR has 3 models or steps:
  - Detection (detecting bounding boxes of possible text)
  - Classification (detecting rotated text and orientation)
  - Recognition (OCR step reading cropped bounding boxes to string).
  - I had a use case where I already have bounding boxes so I only required last Recognition model to run it.

- We chose paddleOCR and quite happy with overall results and for complex layouts, we are trying to "ensemble" the results with vision model(Owen2.5-vl).

- ## 🤔 [How can I determine OCR confidence level when using a VLM : r/computervision _202510](https://www.reddit.com/r/computervision/comments/1oaukp9/how_can_i_determine_ocr_confidence_level_when/)
- Cant you prompt vlm to output its confidences, just in words, like low, medium-low, medium, medium-high, high?
  - That’s exactly what I tried to do. It usually just gives me high or “1.0” confidence Moreover, it messes up the output of my extracted fields too

- What worked best for me was use a 2-stage for OCR: use VLMs to reason which text/fields are relevant and what position, and then crop those out and feed it to an OCR module like Tesseract - performance is pretty amazing. If it's digital documents then EasyOCR or something more lightweight also works.

- ## [What is the best open-source VLM model for OCR (Multilinguage EN FR DE)? : r/LocalLLaMA _202601](https://www.reddit.com/r/LocalLLaMA/comments/1q3qda4/what_is_the_best_opensource_vlm_model_for_ocr/)
- Ministral recently released, they claim best performance in many European languages, Mistral is french after all

- Deep seek ocr or nemotron parse for document to markdown /html and then run a model for converting it in the json structure of your choice?
  - tables can be tricky sometimes. Maybe start by building a validation set und try different models and their performance on it.

- Most people jump straight to VLM model selection when the real bottleneck is usually document preprocessing. You're dealing with scanned docs, which means quality varies wildly. The OCR accuracy on those 100k documents will make or break your table extraction, regardless of which VLM you pick.
  - Before comparing more models, run a sample through your current pipeline and check how clean the text extraction actually is. Qwen2-VL-72B might give you better results than the 8B version, but if your document quality is inconsistent, you'll hit a ceiling fast. PaddleOCR or Tesseract with proper preprocessing often outperforms VLMs on pure text extraction.
  - For table structure specifically, try Table Transformer or LayoutLMv3 as a preprocessing step before the VLM. They're designed exactly for this. The VLM can then focus on converting the structured data to JSON rather than doing both detection and extraction.
  - Testing different approaches systematically, something vectorflow.dev handles well, usually reveals that the parsing stage needs more attention than the model choice.

- I tested multiple models and between Qwen3-VL faimily most of them and for my usecase also the 8B model was punching way above its weights.

- ## [ollama跑DeepSeekOCR的几种提示词输出格式 _202601](https://linux.do/t/topic/1489368)
  - 网上似乎有提示词的说明，但是很少有输出格式的说明
  - 不管用什么跑其实输出格式都是一样的
- 自由识别文字
  - Free OCR
  - 输出几乎纯文本（部分 markdown）
- 提取纯文本
  - Extract the text in the image
  - 忽略图像输出文本
- 提取为 markdown
  - Convert the document to markdown
  - 输出最全，包括定位符号和定位符号对应的文本
- 给排版定位坐标
  - Given the layout of the image
  - Parse the figure
- 概述图片
  - Describe this image in detail
  - 似乎可以简单阅读到图表内容？不仅仅是 ocr

- ## pr已合并 [model : add LightOnOCR-1B model by ngxson · Pull Request · ggml-org/llama.cpp _202510](https://github.com/ggml-org/llama.cpp/pull/16764)
  - Qwen3 as language model
  - Mistral3 as vision encoder (the difference is that LightOnOCR does not use [IMG_BREAK] token)
  - Important note: this model requires specific input structure, see the chat template

- ## 已合并pr [feat(model): deepseekocr by mxyng · Pull Request · ollama/ollama _202511](https://github.com/ollama/ollama/pull/13082)
- What's the supposed way to use it via the REST API? 

```JS
// just tried it with Postman and it worked.
{
  "model": "deepseek-ocr:3b",
  "prompt": "<image>\n<|grounding|>Convert the document to markdown.",
  "stream": false,
  "images": ["BASE64_IMAGE"]
}
```

- [How can I use deepseek-ocr:3b from the API? · Issue · ollama/ollama _202511](https://github.com/ollama/ollama/issues/13252)
  - The model is very sensitive to variations of input. Recommended prompts can be found here.
  - [deepseek-ai/DeepSeek-OCR: Contexts Optical Compression](https://github.com/deepseek-ai/DeepSeek-OCR#prompts-examples)

```sh
# //JavaScript
echo '{
    "model":"deepseek-ocr:3b-bf16",
    "messages":[{"role":"user","content":"\n<|grounding|>Describe this image.",
    "images":["'"$(base64 -w0 ./puppy.png)"'"]}],
    "stream":false
}' | curl -s localhost:11434/api/chat -d @- | jq -r .message.content
<|ref|>White Maltese puppy<|/ref|><|det|>[[113, 184, 799, 759]]<|/det|> sitting on <|ref|>a stone<|/ref|><|det|>[[0, 434, 997, 996]]<|/det|>
```

- ## [Is Deepseek-OCR SOTA for OCR-related tasks? : r/LocalLLaMA _202511](https://www.reddit.com/r/LocalLLaMA/comments/1ov2wmu/is_deepseekocr_sota_for_ocrrelated_tasks/)
- From my tests, PaddleOCR-VL, Deepseek-OCR, and MinerU-VLM are almost identical in size, performance and are all highly effective. Just make sure your GPU supports CUDA.

- Qwen3VL is a more general-purpose Model. It typically operates slower than specialized OCR models and often requires guidance from users through prompting. For specific OCR needs, consider models like MinerU, which go beyond text based tasks to extract graphical elements (images and tables) from PDFs and create an associated JSON index file. So it's way more useful if you have such needs.
- I tend to split the OCR task from the classification/extraction task.

- In our use case, convert medical pdf documents in chinese with figures to markdown, MinerU-VLM is the best one in above three.

- For my use cases Qwen 3 VL cleanly outperforms it.
- Qwen3 VL 32B definitely outperforms it, but in its size and speed class Deepseek-OCR is best in slot.

- I would like to also add OlmOCR 2 7B to the mix. It has been working really well especially with proper JSON schema for assistance. Minimal hallucinations and tolerable rare spelling mistakes for a VLM.

- ## [Is there a VLM that has bounding box support built in? : r/computervision _202508](https://www.reddit.com/r/computervision/comments/1me7ciq/is_there_a_vlm_that_has_bounding_box_support/)
- Florence 2 and PaliGemma 2

- I think Qwen 2.5 VL might be able to do it. It was trained on document understanding and bounding boxes. Prompt it to generate html from your image.

- ## [Feature Request: Support HunyuanOCR-1B · Issue · ggml-org/llama.cpp _202511](https://github.com/ggml-org/llama.cpp/issues/17509)

- ## [I've just ordered an RTX 6000 Pro. What are the best models to use in its 96GB for inference and OCR processing of documents? : r/LocalLLaMA _202511](https://www.reddit.com/r/LocalLLaMA/comments/1ouq7oe/ive_just_ordered_an_rtx_6000_pro_what_are_the/)
- For medical and legal docs you really want something that can handle tables and complex layouts. I've seen people get burned using generic OCR models on medical forms where the layout matters as much as the text.
  - The 6000 Pro should handle most models fine but for production use with multiple users... you might want to think about caching and load balancing. We had a client try to run everything on one GPU for their legal team and it became a bottleneck real quick. 
  - Maybe start with something like LayoutLMv3 or Donut for the document understanding part - they're built for this kind of structured extraction rather than just reading text.

- The best OCR model is olmOCR 2 from Ai2. Fully open weights and they provide training data, unlike everyone else. Handles complex formatting incredibly well.
  - This is really only true for PDFs. I recently built a project that tries to be like a markdown web browser for agents and it uses that olmOCR model on screenshots of the webpages. It works but doesn’t actually get markdown formatted outputs from those.

- MinerU has a feature that extracts graphical elements into an individual folder, along with a JSON index file that retains all positional information from a scanned PDF.

- The suggestion of an OCR specific model is probably a good one. I'll mention the granite docling models. Tiny but will be blazing fast for you.
  - Expect to do a lot of downloading and testing. You need to find what works for you. Then there is the never ending stream of new models to try.

- Qwen3-vl is a really solid series. I have the 4B model doing full OCR of invoices with bounding boxes for visual grounding, in a human in the loop system.

- You don’t really need a fancy LLM for this, if they’re high quality documents you could easily use tesseract. Regarding inference, any RAG approach should work
  - Any handwriting would be out. Tesseract is too old and I think shouldn't be the gold standard anymore.
- Tesseract should work well enough with high quality documents that were originally generated in Office, etc. There are plenty of other solutions out there, tesseract included, that would be drastically quicker and less resource intensive than an LLM whether tesseract, OCRopus, Calamari, Kraken.. it all depends on the nature of the documents, langauge, etc.

- ## [model : add PaddleOCR by ngxson · Pull Request · ggml-org/llama.cpp _202510](https://github.com/ggml-org/llama.cpp/pull/16701)
  - Model generate hallucinated text, likely because of the projector being incorrect
- I was really looking forward to benchmarking this model, until I saw it's limitations, on your point here "Model generate hallucinated text, likely because of the projector being incorrect" I don't think it's due to the projector, I cloned your branch to see why it's hallucinating, it seems to be due to the lack of pre-processing input done by this model "PP-DocLayoutV2"... PaddleOCR-VL is not an end to end VLM, it relies on "PP-DocLayoutV2" for detection, it's basically a glorified version of LayoutLM.
  - Yes I also almost come to the same conclusion. The main issue is that PaddleOCR is not just one monolithic model like Qwen or Deepseek-OCR, but it's more like a pipeline of multiple models glued together. Therefore, I don't think we currently have the infrastructure to bring it into llama.cpp.
  - I'll close this PR for now as it's not giving any meaningful results. For users who need to do OCR task, I would recommend having a look at the latest Qwen3-VL series, or LightOnOCR-1B

- I managed to convert the PP-DocLayoutV2 part of the pipeline into onnx format by adding a onnx conversion mapping for index_put to paddle2onnx. Do you think sharing the patch here would open up this PR again, or is this thread closed for good?
  - I've been looking into DeepSeek-OCR, but their accuracy is actually lower than PaddleOCR-VL for real-world use, and it is also only 0.9B, which makes it runnable on basically any device.

- 🐛 [PaddlePaddle/PaddleOCR-VL · GGUF or MLX support?](https://huggingface.co/PaddlePaddle/PaddleOCR-VL/discussions/2)
  - We really would love to convert this model to gguf, mlx format, to make it more accessible. 
  - It has two components, one is a 0.9b VLM, another is a layout analysis model. 
  - For the VLM, it's in pytorch/transformer compatible format, and you can find the pytorch implementation in this repo, and you can run it using vLLM, and I think it's possible to convert it into gguf/mlx with not too much efforts. 
  - For the layout analysis model, i.e., PP-DocLayoutV2, it's in paddlepaddle format, and the implementation is in PaddldOCR repository using paddlepaddle, it needs porting the implementation into pytorch, and converting the weights to pytorch compatible format. There are some glue codes between the two components, which requires some efforts. 
  - The team is much more familiar at paddlepaddle than pytorch ecosystem tools, but we really love to work with the community to make this model being supported by other projects.

- ## [Practical takeaways from recent hands-on use of PaddleOCR‑VL 0.9B : r/LocalLLaMA _202510](https://www.reddit.com/r/LocalLLaMA/comments/1obfwt9/practical_takeaways_from_recent_handson_use_of/)
  - Bottom line up front: I care most about whether complex layouts can be restored into structured data, whether handwriting tables and formulas are stable, and local inference speed and cost. 
  - Paddleocr‑VL 0.9B feels purpose built for production, especially for multi column PDFs, table structures, and formulas. 
  - Cloud models like GPT‑4o and Gemini 2.5 Pro are more general for commonsense cross domain understanding and conversational interaction, but you need to factor in cost and privacy compliance.
  - On multi column complex layouts and whether they can be directly restored into structured data, which I value highly because it decides how much human cleanup downstream automation needs. Paddleocr‑VL takes an engineering first approach: a NaViT dynamic visual encoder plus a lightweight ERNIE, combining layout understanding with structured outputs.

- I had similar experiences when we were testing different OCR solutions for Docstrange, and your point about structured outputs being more important than pretty-looking text really hits home. 
  - We found that PaddleOCR-VL's engineering-first approach does seem to handle the weird edge cases better than the general VLMs, especially when you're dealing with those nightmare scenarios like financial reports where a single misplaced table cell can mess up your entire downstream pipeline. 
  - The thing that caught my attention in our testing was how much more predictable the failure modes are with specialized models like PaddleOCR-VL compared to something like GPT-4o which might give you beautiful conversational output but completely miss that a footnote belongs to a specific table cell three pages back.
  - The cost factor you mentioned is huge too, especially if you're processing thousands of documents daily where those API calls add up fast.

- ## 🆚 [Comparison new qwen 32b-vl vs qwen 30a3-vl : r/LocalLLaMA _202510](https://www.reddit.com/r/LocalLLaMA/comments/1ocko1m/comparison_new_qwen_32bvl_vs_qwen_30a3vl/)
- Dense 32b vl is better in most benchmarks
  - Yeah but the difference is negligible in most of them. I don't know the implications behind that small gap in performance.
- 32B VL seems to be significantly better in multilingual benchmarks, at least that's a good usecase.

- So a slight increase in quality for the 32b, sacrificing a lot of speed from the MoE

- What surprises me is that the 30B is so close, knowing inference should be around 6x faster.

- ## 🆚 [[Experiment] Qwen3-VL-8B VS Qwen2.5-VL-7B test results : r/LocalLLaMA](https://www.reddit.com/r/LocalLLaMA/comments/1o9xf4q/experiment_qwen3vl8b_vs_qwen25vl7b_test_results/)
  - TL; DR: I tested the brand-new Qwen3-VL-8B against Qwen2.5-VL-7B on the same set of visual reasoning tasks — OCR, chart analysis, multimodal QA, and instruction following.
  - Qwen3-VL shows a clear generation-to-generation leap and delivers more accurate, nuanced, and faster multimodal reasoning.

- [Qwen3-VL testout - open-source VL GOAT : r/LocalLLaMA](https://www.reddit.com/r/LocalLLaMA/comments/1o9eo4f/qwen3vl_testout_opensource_vl_goat/)
  - I’ve been waiting on Qwen3-VL and finally ran the 4B on scanned tables, color-blind plates, UI screenshots, and small “sort these images” sets.
  - Tables came out clean with headers and merged cells handled better than Qwen2.5-VL.
  - Variant behavior matters. The Think build tends to over-explain and sometimes lands wrong. The Instruct build stays steadier for perception, grounding, and “read + point” jobs. 
  - My pattern is simple: let 4B handle recognition and coordinates, then hand multi-step reasoning or code-gen to a larger text model. That stays stable.
  - Net take: big lift in perception, grounding, and visual math; still weak on faithful webpage replication and hard spatial transforms. As of today, it feels like the top open-source VL at this size.

- ## 🆚 [Qwen3-VL Instruct vs Thinking : r/LocalLLaMA _202510](https://www.reddit.com/r/LocalLLaMA/comments/1nuhgxw/qwen3vl_instruct_vs_thinking/)
  - I am working in Vision-Language Models and notice that VLMs do not necessarily benefit from thinking as it applies for text-only LLMs. 
  - I created the following Table asking to ChatGPT (combining benchmark results found here), comparing the Instruct and Thinking versions of Qwen3-VL. You will be surprised by the results.

- I just want qwen3-30b-a3b-2507 with a vision component so I dont have to load multiple models. 

- I wonder how hybrid vision models do — GLM4.5V comes from the Air version which is hybrid.

- [Qwen3-VL-30B-A3B-Instruct & Thinking are here : r/LocalLLaMA](https://www.reddit.com/r/LocalLLaMA/comments/1nxhfcq/qwen3vl30ba3binstruct_thinking_are_here/)
- I wonder why the thinking version got worse IFEval than the instruct and even the previous, non-vision, thinking model.
  - yes they don't discuss yet why thinking version, that uses way more inference token budget, performs worse than the Instruct. Imo Thinking for VLMs is not necessarily beneficial
- It seems to improve reasoning in the non-thinking model and hurt it in the thinking? Besides that I guess the difference is only slight and completely mixed. Except for coding, VL makes that worse.

- ## [moondream 0.5B - the world's smallest vision language model : r/LocalLLaMA _202412](https://www.reddit.com/r/LocalLLaMA/comments/1h7ivts/moondream_05b_the_worlds_smallest_vision_language/)
  - https://github.com/vikhyat/moondream
  - Moondream 0.5B offers a significantly lower download size and memory usage than moondream 2B.
  - It is intended to be used as a distillation target—start building with moondream 2B, and distill your use-cases onto the 0.5B model before deployment.
  - This model was built using structured pruning on 2B with quantization-aware training. This means we can easily distill from 2B to recover accuracy on the specific target tasks an application needs, and run with int8 quantization without any loss of accuracy.
  - Today we are releasing int8 and int4 weights for moondream 0.5B, as well as fast CPU inference support in the Python client library. 16-bit weights and distillation support will be coming soon, so stay tuned!

- doesnt look like this new model has been added to ollama as yet (and no GGUFs available)

- Awesome. Florence is nice and small too, but could only really handle a finite list of specific prompts. It seems this small models retains the ability to ask free-form questions, which would make it extremely useful for mobile devices.
  - Florence 2 base is smaller. You can also fine tune it to work with any specific prompt you like if you have consistent prompts.
# discuss-toolchain-vlm/cor
- ## 

- ## 

- ## 

- ## 

- ## [How do I enable vision capabilities of a model ? Linux Mint 22.2, rx 6600. I ran this at bash/terminal to start the server: llama-server -m ./Qwen3-VL-8B-Instruct-Q4_K_M.gguf : r/LocalLLaMA](https://www.reddit.com/r/LocalLLaMA/comments/1p9t8tz/how_do_i_enable_vision_capabilities_of_a_model/)
- `--mmproj <mmproj file>` grab `.mmproj` file where you've got your gguf

- You should read the model card on hugging face https://huggingface.co/Qwen/Qwen3-VL-8B-Instruct-GGUF#web-chat-using-llama-server
# discuss
- ## 

- ## 

- ## 
