---
title: lib-ai-app-community-model-dev-xp
tags: [large-language-model, stable-diffusion]
created: 2025-11-18T13:21:29.771Z
modified: 2025-11-18T13:22:22.078Z
---

# lib-ai-app-community-model-dev-xp

# guide

- models-variants
  - watching: openai, claude, qwen, deepseek, gemini/gemma, glm, mistral/codestral
  - variants: mlx, unsloth, quants
  - 测试模型时可能更希望速度快，但做任务或规划时更希望质量好，所以偏向选择大B参数的模型
  - 📱 端侧模型还要考虑电源及功耗问题, 实测macbook-air在跑模型时掉电很快
    - 端侧最好用 api-key + tiny-local-llm

- models-choices
  - 🤔 LMs are tools. Describe your use cases.
    - 分析清楚核心需求: 需要reasoning/coding/large/faster
  - moe模型的实际效果大概只有dense模型的一半，如qwen3-30B-A3B 相当于 Qwen3-14b
  - 模型占用VRAM不能太大，还要为context处理、应用程序如nextjs/comfyui预留RAM/VRAM
  - 选择模型时多用官方版/主流版，小众微调的版本可能存在tool-call/overthink/多语言multilingual/对话风格/llama.cpp不支持等问题/loop
    - 选用主流版还方便与其他用户对比速度/配置
    - 非主流版可能出现vision/rag等被去掉的问题
  - 多agent架构时，可使用不同架构的agent相互验证
  - non-thinking或输出简洁的模型适合coding

- donts
  - 很多带thinking的大模型不擅长计数，如within 18 words， 有的模型真的会逐个token打印出来逐个数一遍

- mac 🍎
  - 👀 在low power mode省电模式下, 模型的输出速度会比非省电模式慢2-3倍
# draft
- 现在的模型缺少 15b-23b 间的小模型，可选择第三方魔改或扩容后的版本
  - 还缺少 40b-71b 间的中模型

- 
- 
- 
- 
- 

# usage-xp
- 🧪 test-cases
  - Which of these objects is not like the others: orange, banana, potato, chair
  - I have 7 apples. Yesterday I ate one apple. how many apples do i have now?
  - I have 2 apples, then I buy 2 more. I bake a pie with 2 of the apples. After eating half of the pie how many apples do I have left?
  - If we lay 5 shirts out in the sun and it takes 4 hours to dry, how long would 20 shirts take to dry? Explain your reasoning step by step
  - convert inches to cm: 15.4 x 7.3 x 13.5 inches
  - 大漠孤烟直 出自哪里? 上下句是什么？ 表达什么意思？ 有其他地方引用过这句吗?

- gemma3 🌹 /多语言/创意文本/vision
  - 27b 和 12b 都能较好遵循带结构的instruct输出， 27b能主动给出更多外部网页链接而12b给的链接很少

- qwen3 🌹 /能力全/thinking开关/内容丰富
  - 4b及14b的输出内容都比较详细，经常包含表格📈

- gpt-oss-20B-A3.6B 👀 /业界标杆/输出快
  - 输出的内容特别喜欢用表格📈, 讨论代码相关问题也喜欢用表格
  - unsloth-Q5的输出速度为 11.8 tops, offcial-Q4的输出速度为 11.2 tops, 速度比qwen3-14b更快

- magistral-small-2509-24b  👀 /可以用/think+vision/欧洲多语言/产品线丰富/censor弱
  - 回复一般很短，感觉质量不高
  - mistral系列模型的知识丰富度很高, 可以降低对RAG的依赖 🤔
  - thinking时间在~~3-10~~min(2509已改进)左右，或许对于plan制定计划有用
  - 输出内容几乎不提供外部链接，2507不也提供外部链接
  - 输出内容中几乎不提供表格
  - 带thinking的模型不擅长计数，如 within 18 words

- glm4 👀 /可以用/是否善长html代码?
  - 🖼️ html中支持显示外部图片，需要形状类图标的位置能准确生成svg
  - glm4不会think，输出内容质量感觉一般
  - 输出的长度大概在30-60行，简洁是特色，对代码有用?
  - 在多轮聊天时，输出内容也会逐渐变长?
  - 输出html页面时能添加复杂的svg代码，形状类图标的位置能准确生成svg
  - 生成的html页面风格有点tailwind，也有点bootstrap
  - 生成的slider/carousel比qwen3更准确

- glm-z1 👀 /思考非常久/不擅长代码
  - z1会think5-15min，think不支持disable，输出内容的长度会比glm4多20行左右，多一些外部链接，多用很多表格，质量较好
  - z1的think时间比qwen3长很多，
  - 输出内容的长度比qwen3更少, 输出内容会有表格📈

## coding-models

- tips
  - ⚖️ coding的prompt也尽量遵循 plan + act 的结构
  - 对于ai按用户提供的模版输出html的场景，用户提供和ai输出的代码通常都是偏短的、偏静态的; 
    - 另一种思路是按模版输出markdown手动拼接，速度可能更快
  - coding模型必须要用新版才能使用最新框架的架构写法，如tailwind.v4, reactjs.v19

- 🧪 test-cases
  - landing-page + tailwind: 基本都能实现页面, 🌹 glm擅长图标和图片
    - kat-dev和qwen3都不擅长图标和图片
  - landing + threejs: 基本都能实现, 
    - qwen3-32b有时无法运行demo
  - 🤔 game-reaction-for-click: kat-dev能正确实现， qwen3-think能实现
    - glm异常，qwen3异常
  - game-typing: glm/kat-dev行, qwen3非think也行
  - 🤔 dashboard-crud: qwen3小bug，glm能做ui，kat-dev失败
  - 🤔 weather: glm大多能实现
    - kat-dev部分异常，qwen3异常
  - slider: glm擅长css动画效果，其他ai的ux效果一般
  - threejs-earth: qwen3行, glm部分异常, kat-dev异常
  - vocabulary-card: 基本都能正确调整页面, 
    - kat-dev有时样式异常

- qwen3-coder-30b-a3b 🌹 /速度快
  - 生成单页面的效果好速度快
  - 擅长用渐变色块代替图片占位符
  - 写完代码后一般还会讲解说明一段

- devstral-2507-24b /欧洲多语言/instruct

- qwen2.5-coder-32b /微调多

- qwen3-32b /thinking开关/能力全
  - 擅长渐变色文字
  - 生成单页html时， 需要形状类图标的地方会乱码
  - 不擅长显示外部图片，需要图片的地方会显示缺省占位符

- kat-dev-32B
  - 页面简洁
  - 比qwen3更擅长样式、能显示部分图标
  - 页面不是典型的tailwind风格，风格有点陈旧
  - 不擅长显示外部图片
  - 不擅长生成形状类图标，经常生成重复图标，有时会缺失部分图标

- uigen-fx-4b /擅长ui框架/能写js
  - 擅长渐变色按钮
  - 不擅长用渐变色块代替图片占位符
  - 有时能写很多js代码

- webgen-4b /擅长html页面不擅长框架和js
  - webgen生成单页面的效果远不如uigen/qwen3-coder
  - 似乎不擅长tailwind, 生成页面的风格偏非tailwind样式的传统网页
  - 经常出现部分元素样式错乱的问题
# models-features/variants
- 专用模型
- ocr
- tool-calling
  - lfm2-1.2b-tool
- edit-apply
- devops
- graphics
- computer-use
- cpu
  - [NanoAgent — A 135M Agentic LLM with Tool Calling That Runs on CPU : r/LocalLLaMA](https://www.reddit.com/r/LocalLLaMA/comments/1oomy4t/nanoagent_a_135m_agentic_llm_with_tool_calling/)

- reap
- https://huggingface.co/cerebras/GLM-4.6-REAP-268B-A32B
  - [I think the dataset is gonna have to be more diverse.](https://huggingface.co/cerebras/GLM-4.6-REAP-268B-A32B/discussions/1)
    - The method looks promising but as in other prunes, it may have REAPed too much to be viable.

- [starvector/starvector-1b-im2svg · Hugging Face _202503](https://huggingface.co/starvector/starvector-1b-im2svg)
  - StarVector is a foundation model for generating Scalable Vector Graphics (SVG) code from images and text
  - It utilizes a Vision-Language Modeling architecture to understand both visual and textual inputs, enabling high-quality vectorization and text-guided SVG creation.
  - https://github.com/joanrod/star-vector /apache2/202504/python
    - StarVector Accepted at CVPR 2025
  - [感觉不太行。。](https://huggingface.co/starvector/starvector-1b-im2svg/discussions/2)
    - This checkpoint is designed for converting images into SVGs. While we do have a text-to-SVG model, we plan to release it at a later stage.
    - The current model performs well with simple icons but has limitations with more complex images. Improving performance on complex cases is a key focus of our ongoing work.

- [lakhera2023/devops-slm-v1 · Hugging Face _202509](https://huggingface.co/lakhera2023/devops-slm-v1)
  - Based on Qwen2.5
  - a specialized language model specifically for DevOps tasks and operations only.
  - designed EXCLUSIVELY for DevOps-related tasks. It has robust filtering that will NOT respond to general questions about movies, weather, cooking, sports, music
  - [Meet the first Small Language Model built for DevOps : r/LocalLLaMA](https://www.reddit.com/r/LocalLLaMA/comments/1ndm44z/meet_the_first_small_language_model_built_for/)

- https://huggingface.co/Alibaba-EI/SmartResume /apache2/202510
  - 一个面向版面结构的智能简历解析系统，系统支持 PDF、图片及常见 Office 文档格式，融合 OCR 与 PDF 元数据完成文本提取
  - 本仓库包含 SmartResume 项目所需的两个核心权重文件，用于简历信息提取和版面分析。
  - Qwen3-0.6B: 简历文本信息提取和结构化处理
  - YOLOv10: 简历版面布局检测和区域分割
# models-exploring
- [nvidia/Llama-3.1-Nemotron-8B-UltraLong-4M-Instruct · Hugging Face](https://huggingface.co/nvidia/Llama-3.1-Nemotron-8B-UltraLong-4M-Instruct)
  - a series of ultra-long context language models designed to process extensive sequences of text (up to 1M, 2M, and 4M tokens) while maintaining competitive performance on standard benchmarks. 

- [Otakadelic/phi-4-abliterated-Orion-18B · Hugging Face](https://huggingface.co/Otakadelic/phi-4-abliterated-Orion-18B)
  - Orion-zhen's original wasn’t just abliteration. it is capable of portraying complex personalities, delicate emotions, sharp thoughts and inner conflict, it felt more like a katana than a model: slicing through responses with cold precision.
  - This version shifts the focus slightly toward storytelling. Still emotionally complex, still powerful under duress, captivity, or obedience—but with a more narrative-friendly tone.
  - Based on Phi-4 Abliterated (40-layer model)
  - Inspired by @mlabonne's BigQwen2.5-Echo-47B-Instruct, added exact same layers to original Phi-4 14B(40-layer model) to the middle part while keep in tact first and last parts. Though its parameter count increased(14B --> 18B), it is a structural duplicate.
# model-wiki/bookmarks
- 超大模型的极小量化版
  - Llama-3.3-70B-Instruct-abliterated-Q2-mlx  22.07gb
  - Qwen3-Next-80B-A3B-Instruct-q2-mlx  24.95gb
  - Mistral-Large-Instruct-2411-Q2-MLX  45.99gb
  - gpt-oss-120b-mlx-2Bit(116.8B A5.1B)  36.61gb
  - GLM-4.5-Air-2bit(106b A12B)  33.45gb
  - GLM-4.5-Air-4bit(106b A12B)  62gb
  - DeepSeek-V3.1-Terminus-mlx-2Bit  209.89gb
  - DeepSeek-R1-2bit  251.82gb
# more
- [Qwen3: How to Run & Fine-tune | Unsloth Documentation](https://docs.unsloth.ai/models/qwen3-how-to-run-and-fine-tune)
