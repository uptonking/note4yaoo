---
title: lib-ai-app-community-model-dev-xp
tags: [large-language-model, stable-diffusion]
created: 2025-11-18T13:21:29.771Z
modified: 2025-11-18T13:22:22.078Z
---

# lib-ai-app-community-model-dev-xp

# guide

- models-variants
  - watching: openai, claude, qwen, deepseek, gemini/gemma, mistral/codestral, glm, kimi, minimax
  - variants: mlx, unsloth, quants
  - 测试模型时可能更希望速度快(小参数)，但做任务或规划时更希望质量好(大参数)，要取舍
  - 📱 端侧模型还要考虑电源及功耗问题, 实测macbook-air在跑模型时掉电很快
    - 端侧最好用 api-key + tiny-local-llm
  - unsloth团队提供的量化版模型会根据反馈不断更新，经常针对热门模型更新fix和优化, 而lmstudio-community的模型很少会更新

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
  - 模型的升级换代很快，喜新不喜旧，新模型对 tool-call/attention/量化的支持一般都更好
  - 大厂的模型一般都会定期升级，会有社区用户对比评测，更可靠、更有参与感

- tool-call/use
  - 针对tool-use微调优化的小模型慎用, 因为mcp的tool描述可能导致context超长

- structured-output

- donts
  - 很多带thinking的大模型不擅长计数，如within 18 words， 有的模型真的会逐个token打印出来逐个数一遍

- mac 🍎
  - 👀 在low power mode省电模式下, 模型的输出速度会比非省电模式慢2-3倍
# draft
- 现在的模型缺少 15b-23b 间的小模型，可选择第三方魔改或扩容后的版本
  - 还缺少 40b-71b 间的中模型

- task-specific leaderboard
  - rag
  - community users can upload benchmark results with device-specs from apps like lmstudio
    - 评测耗时耗力，社区参与更快捷，但会降低准确度
    - 同格式、同配置 的模型比较更有意义

- 
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
  - what is the latest version of Node.js?
  - 大漠孤烟直 出自哪里? 上下句是什么？ 表达什么意思？ 有其他地方引用过这句吗?

- cowork-model
  - macos model
  - shell model

- qwen3 🌹 /能力全/thinking开关/内容丰富
  - 4b及14b的输出内容都比较详细，经常包含表格📈

- gpt-oss-20B-A3.6B 👀 /业界标杆/输出快
  - 输出的内容特别喜欢用表格📈, 讨论代码相关问题也喜欢用表格
  - unsloth-Q5的输出速度为 11.8 tops, offcial-Q4的输出速度为 11.2 tops, 速度比qwen3-14b更快

- glm-4.7-flash-30b-a3b
  - GLM-4.7-Flash-MLX-4bit 的版本容易陷入thinking loop
    - loop时的thinking内容没有遵循带step的thinking过程
    - 💡 实测官方参数配置不好用, mlx-4bit适合 temperature-0.7
  - 🌹thinking的内容非常agentic, 带有明确的step
    - request analysis > Brainstorm > draft res > refine res > revise > polish > response
  - [DeepSeek architecture?](https://huggingface.co/unsloth/GLM-4.7-Flash-GGUF/discussions/2)
    - [DeepseekV3ForCausalLM](https://huggingface.co/zai-org/GLM-4.7-Flash/discussions/5)
    - the modular file does inherit the DSv3 module
    - And it looks like the only thing added on top of DSv3 is to ignore the MTP layer.

- nemotron-3-nano-30b-a3b
  - 中文内容丰富

- gemma3 🌹 /多语言/创意文本/vision
  - 27b 和 12b 都能较好遵循带结构的instruct输出， 27b能主动给出更多外部网页链接而12b给的链接很少

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

## mobile 📱

- lfm
  - 对 chat template 和 prompt 的要求不严格，方便测试
    - 不输入system prompt也能工作

## coding 🔡

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

- devstral-2512-24b
  - 前端landing-page是tailwind风格, 但整体白色简约，色彩不丰富
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

- [ruv/ruvltra-claude-code · Hugging Face](https://huggingface.co/ruv/ruvltra-claude-code)
  - The World's First LLM Optimized for Claude Code
  - Self-Learning Intelligence (SONA): The model continuously improves from interactions, learning your coding patterns, preferences, and project-specific conventions.

## data-viz/charting 📊

- 生成图表的方案(分析需求: 偏前端展示/偏数据分析)
  - 思路1: llm返回核心数据，客户端tool call绘图
  - 思路2: llm直接返回代码，使用coding方案实现绘图
  - 思路3: 简单场景考虑使用md-table替代，然后前端手动渲染图表或引导用户创建图表
  - 💡 思路4: 使用codeblock传输图表相关数据，参考streamdown流式解析mermaid的方案
  - 思路5: data > sql > chart, 类似chat2db的方案

- [mermaidchart/merged-mermaid-7b _202509](https://huggingface.co/mermaidchart/merged-mermaid-7b/tree/main)
  - 无文档说明

- [TroyDoesAI/BlackSheep-MermaidMistral-22B · Hugging Face](https://huggingface.co/TroyDoesAI/BlackSheep-MermaidMistral-22B)
  - /202409
  - merge: TroyDoesAI/Mermaid-22B, TroyDoesAI/BlackSheep-Mistral-22B
  - [TroyDoesAI/Mermaid-Llama-3-8B · Dataset](https://huggingface.co/TroyDoesAI/Mermaid-Llama-3-8B/discussions/1)
    - Is the dataset publicly available?
    - Yeah sure, make your own using my toolkit and my model to distill its knowledge: https://github.com/Troys-Code/AI_Research
    - [TroyDoesAI/MermaidMistral · Dataset?](https://huggingface.co/TroyDoesAI/MermaidMistral/discussions/1)
    - I do not plan to release my ~500 example hand curated dataset as that is used for my evaluation dataset in training now as I believe these are the highest of quality compared to Generated by GPT4 and do not want that public as this is my benchmarker now for how the model is improving as it is incredibly hard to evaluate a models performance on subjective things like story flow.

- [octadion/deepseek-coder-6.7b-pandas · Hugging Face](https://huggingface.co/octadion/deepseek-coder-6.7b-pandas)
  - /202403

- [pipizhao/Pandalyst-7B-V1.2 · Hugging Face](https://huggingface.co/pipizhao/Pandalyst-7B-V1.2)
  - /202310
  - https://github.com/pipizhaoa/Pandalyst
  - [【Pandalyst-7B-V1.2】 Now we can plot and much more powerful ! : r/LocalLLaMA _202310](https://www.reddit.com/r/LocalLLaMA/comments/178uxtf/pandalyst7bv12_now_we_can_plot_and_much_more/)
  - Pandalyst-7B-V1.2, which was trained on CodeLlama-7b-Python and it surpasses ChatGPT-3.5 (2023/06/13), Pandalyst-7B-V1.1 and WizardCoder-Python-13B-V1.0 in our PandaTest_V1.0.
  - 7b version is trained based on Codellama-python-7B, and achieve competitive performance with our 13B !!! (witch was trained on wizardcoder-python-13B)

## image 🖼️

- z-image-turbo 不擅长512尺寸的图片，感觉很糊
  - https://www.modelscope.cn/studios/Tongyi-MAI/Z-Image-Gallery
  - 同样prompt+step生成1024尺寸就比较清晰
  - 似乎只能生成长宽1:1比例的图片, 随机比例会抛出异常
  - 生成 2048x2048 的图片时, macbook内存爆炸，电脑重启
  - 不擅长渲染中文字体

- https://huggingface.co/AIDC-AI/Ovis-Image-7B
  - https://github.com/AIDC-AI/Ovis-Image
  - a 7B text-to-image model specifically optimized for high-quality text rendering

## translation 🌐

- 通过 promptfoo 测试多个模型的翻译能力, 鼠标hover在表头列可以看到模型信息, prompt不变时只会增量请求新加的prompt
  - hy-mt会采用更多意译，将中文的一句翻译为多句英文，所以翻译输出内容最长
  - 对中文人名称呼、中文俗语翻译较准确的是hy-mt1.5, 婶婶/脂粉堆
  - riva对 4% 的数字翻译为 4 percent, 而qwen3-4b/hy-mt能直接用原文的 4%
    - riva对于偏文本的链接列表，范围后仍为1行，但qwen3/hy-mt能输出多行而友好
    - 翻译输出内容最短
    - 🤔 似乎相对于qwen3-4b没有任何优势

- [tencent/HY-MT1.5-7B · Hugging Face _202512](https://huggingface.co/tencent/HY-MT1.5-7B)
  - /freeTill100mMAU
  - ZH<=>XX
  - > 🔠 将以下文本翻译为{target_language}，注意只需要输出翻译后的结果，不要额外解释: {source_text}
  - XX<=>XX Translation, excluding ZH<=>XX
  - > 🔠 Translate the following segment into {target_language}, without additional explanation: 
  - > 🔠 将以下<source></source>之间的文本翻译为中文，注意只需要输出翻译后的结果，不要额外解释，原文中的<sn></sn>标签表示标签内文本包含格式信息，需要在译文中相应的位置尽量保留该标签。输出格式为：<target>str</target>
  - ⚖️ [Why such an absurdly restrictive license?](https://huggingface.co/tencent/HY-MT1.5-7B/discussions/3)
  - https://github.com/Tencent-Hunyuan/HY-MT/blob/main/License.txt
    - If, on the Tencent HY version release date, the monthly active users of all products or services made available by or for Licensee is greater than 100 million monthly active users in the preceding calendar month, You must request a license from Tencent

- [google/translategemma-4b-it · Hugging Face _202601](https://huggingface.co/google/translategemma-4b-it)
  - 4b, 12b, 27b
  - supports direct translation of a text input, or text-extraction-and-translation from an image input. 
  - The models were fine-tuned from the original Gemma 3 checkpoints using parallel data from a wide variety of sources. The TranslateGemma models used 4.3 billion tokens during SFT and 10.2 million tokens during the reinforcement learning phase. 
  - Training was done using JAX and ML Pathways. 
  - 对模版要求严格，似乎不能在lmstudio直接对话

- [nvidia/Riva-Translate-4B-Instruct · Hugging Face _202506](https://huggingface.co/nvidia/Riva-Translate-4B-Instruct)
  - /free
  - mlx模型在lmstudio测试en2cn时，只会翻译第一段en英文文字
  - > 🔠 translating text from English to Simplified Chinese
  - It is a fine-tuned version of a 4B Base model that was pruned and distilled from nvidia/Mistral-NeMo-12B-Base(202405) using our LLM compression technique.
  - [Any-to-any](https://huggingface.co/nvidia/Riva-Translate-4B-Instruct/discussions/1)
  - The model currently supports the following combinations (non-English to non-English is not supported):
  - English to non-English
  - Non-English to English
  - German(de), European Spanish(es-ES), LATAM Spanish(es-US), France(fr), Brazillian Portugese(pt-BR), Russian(ru), Simplified Chinese(zh-CN), Traditional Chinese(zh-TW), Japanese(ja), Korean(ko), Arabic(ar).

## rag

- [nvidia/NVIDIA-Nemotron-Parse-v1.1 · Hugging Face](https://huggingface.co/nvidia/NVIDIA-Nemotron-Parse-v1.1)
  - designed to understand document semantics and extract text and tables elements with spatial grounding
  - Given an image, NVIDIA Nemotron Parse v1.1 produces structured annotations, including formatted text, bounding-boxes and the corresponding semantic classes, ordered according to the document's reading flow.

- [inference-net/Schematron-8B · Hugging Face](https://huggingface.co/inference-net/Schematron-8B)
  - Schematron series, Inference.net's long‑context extraction models specialized in converting noisy HTML into clean, typed JSON that conforms to your custom schema. 
  - 基于 meta-llama/Llama-3.1-8B-Instruct
  - https://x.com/samhogan/status/2018838862123196455
    - I found out today that two of the largest web scraping companies in the world are using a custom Llama 3 model we released last year to process millions of webpages per day. 
    - Schematron-3b: HTML -> JSON parsing
    - Custom LLMs for data extraction are GOATed dude! We built one for a special use case and it outperforms NLP by far.

- [inference-net/OSSAS-Qwen3-14B · Hugging Face](https://huggingface.co/inference-net/OSSAS-Qwen3-14B)
  - part of Project OSSAS, developed in collaboration with LAION and Wynd Labs to democratize access to scientific knowledge by creating structured summaries of research papers at scale.

- [zilliz/semantic-highlight-bilingual-v1 · Hugging Face](https://huggingface.co/zilliz/semantic-highlight-bilingual-v1)
  - We kept running into this problem: when we retrieve documents in our RAG system, users can't find where the relevant info actually is.
  - This work draws its core ideas and theoretical underpinnings from Provence (https://arxiv.org/abs/2501.16214)

- [apple/CLaRa-7B-Instruct · Hugging Face _202511](https://huggingface.co/apple/CLaRa-7B-Instruct)
  - instruction-tuned unified RAG model with built-in semantic document compression (16× & 128x).
  - It supports instruction-following QA directly from compressed document representations.

- [CohereLabs/c4ai-command-r7b-12-2024 · Hugging Face](https://huggingface.co/CohereLabs/c4ai-command-r7b-12-2024)
  - /cc-nc
  - [How was r7b?](https://huggingface.co/CohereLabs/c4ai-command-r7b-12-2024/discussions/3)

- [jinaai/ReaderLM-v2 _1.5B· Hugging Face _202503](https://huggingface.co/jinaai/ReaderLM-v2)
  - /cc-nc
  - converts raw HTML into beautifully formatted markdown or JSON with superior accuracy and improved longer context handling.

- [inference-net/Schematron-8B · Hugging Face](https://huggingface.co/inference-net/Schematron-8B)
  - specialized in converting noisy HTML into clean, typed JSON that conforms to your custom schema. 

## vlm

- [stepfun-ai/Step3-VL-10B · Hugging Face](https://huggingface.co/stepfun-ai/Step3-VL-10B)

- [apple/FastVLM-0.5B · Hugging Face _202412](https://huggingface.co/apple/FastVLM-0.5B)
  - We introduce FastViTHD, a novel hybrid vision encoder designed to output fewer tokens and significantly reduce encoding time for high-resolution images.
  - Our smallest variant outperforms LLaVA-OneVision-0.5B with 85x faster Time-to-First-Token (TTFT) and 3.4x smaller vision encoder.
  - Our larger variants using Qwen2-7B LLM outperform recent works like Cambrian-1-8B while using a single image encoder with a 7.9x faster TTFT.
  - [riddhimanrana/fastvlm-0.5b-captions · Hugging Face](https://huggingface.co/riddhimanrana/fastvlm-0.5b-captions)
    - a finetuned version of FastVLM-0.5B Stage 3 
    - built for efficient structured image captioning on mobile devices.

## omni

- [openbmb/MiniCPM-o-4_5 · Hugging Face _202602](https://huggingface.co/openbmb/MiniCPM-o-4_5)
  - The first full-duplex omni-modal LLM 
  - Full-duplex Omni-modal Live Streaming: The model can see, listen, and speak simultaneously in a real-time conversation without mutual blocking
  - https://x.com/OpenBMB/status/2018741614257307678
    - Leading Performance: Scoring 77.6 on OpenCompass, it outperforms GPT-4o & Gemini 2.0 Pro in vision-language tasks with 9B params
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
- [杠精大模型 _202406](https://modelscope.cn/models/maomoa/GangLLM)
  - 一个专门与用户抬杠的大模型，它的名字叫“钢蛋儿”，它可以根据用户的输入会进行杠精式的回复，该模型能够捕捉到用户言辞中的细微漏洞，并据此展开犀利的反驳，
  - 该模型在开源大模型上微调而来，基础模型采用的 InternLLM-Chat-7B 模型，采用1680条杠精式对话数据，外加100条自我认知数据进行的微调训练。

- [SicariusSicariiStuff/Assistant_Pepe_8B · Hugging Face](https://huggingface.co/SicariusSicariiStuff/Assistant_Pepe_8B)
  - 适度杠精 + 适度生产力
  - 回答比基模llama3-8b要短， 不喜欢用列表，不喜欢用表格

- [LiquidAI/LFM2-1.2B-RAG · Hugging Face _202509](https://huggingface.co/LiquidAI/LFM2-1.2B-RAG)
  - specialized in answering questions based on provided contextual documents, for use in RAG
  - We recommend using greedy decoding with a `temperature=0`.
  - The system prompt is optional. By default, the output's language follows the user prompt's language.
  - ⚠️ The model supports both single-turn and multi-turn conversations.
  - [Correct chat template ?](https://huggingface.co/LiquidAI/LFM2-1.2B-RAG/discussions/3)
    - You can use any. As mentioned, the system prompt is optional.
    - "[...]" symbolizes a truncation, which is why there's no question in the chat template example.
- [LiquidAI/LFM2-1.2B-Extract · Hugging Face _202508](https://huggingface.co/LiquidAI/LFM2-1.2B-Extract)
  - designed to extract important information from a wide variety of unstructured documents (such as articles, transcripts, or reports) into structured outputs like JSON, XML, or YAML.
  - We strongly recommend using greedy decoding with a `temperature=0`.
  - If no system prompt is provided, the model will default to JSON outputs. We recommend providing a system prompt with a specific format (JSON, XML, or YAML) and a given schema to improve accuracy 
  - ⚠️ The model is intended for single-turn conversations.
- [LiquidAI/LFM2-1.2B-Tool · Hugging Face _](https://huggingface.co/LiquidAI/LFM2-1.2B-Tool)
  - designed for concise and precise tool calling.
  - We recommend using greedy decoding with a `temperature=0`.

- [apple/CLaRa-7B-Instruct · Hugging Face](https://huggingface.co/apple/CLaRa-7B-Instruct)
  - our instruction-tuned unified RAG model with built-in semantic document compression (16× & 128x).
  - It supports instruction-following QA directly from compressed document representations.
  - ⚠️ The model supports both single-turn and multi-turn conversations.

- [nvidia/Llama-3.1-Nemotron-8B-UltraLong-4M-Instruct · Hugging Face](https://huggingface.co/nvidia/Llama-3.1-Nemotron-8B-UltraLong-4M-Instruct)
  - a series of ultra-long context language models designed to process extensive sequences of text (up to 1M, 2M, and 4M tokens) while maintaining competitive performance on standard benchmarks. 

- [Otakadelic/phi-4-abliterated-Orion-18B · Hugging Face](https://huggingface.co/Otakadelic/phi-4-abliterated-Orion-18B)
  - Orion-zhen's original wasn’t just abliteration. it is capable of portraying complex personalities, delicate emotions, sharp thoughts and inner conflict, it felt more like a katana than a model: slicing through responses with cold precision.
  - This version shifts the focus slightly toward storytelling. Still emotionally complex, still powerful under duress, captivity, or obedience—but with a more narrative-friendly tone.
  - Based on Phi-4 Abliterated (40-layer model)
  - Inspired by @mlabonne's BigQwen2.5-Echo-47B-Instruct, added exact same layers to original Phi-4 14B(40-layer model) to the middle part while keep in tact first and last parts. Though its parameter count increased(14B --> 18B), it is a structural duplicate.

- [RUC-DataLab/DeepAnalyze-8B · Hugging Face _202510](https://huggingface.co/RUC-DataLab/DeepAnalyze-8B)
  - the first agentic LLM for autonomous data science. It can autonomously complete a wide range of data-centric tasks without human intervention
  - https://github.com/ruc-datalab/DeepAnalyze

- [DatarusAI/Datarus-R1-14B-preview · Hugging Face _202508](https://huggingface.co/DatarusAI/Datarus-R1-14B-preview)
  - a 14B-parameter open-weights language model fine-tuned from Qwen2.5-14B-Instruct, designed to act as a virtual data analyst and graduate-level problem solver.
  - Unlike traditional models trained on isolated Q&A pairs, Datarus learns from complete analytical trajectories—including reasoning steps, code execution, error traces, self-corrections, and final conclusions—all captured in a ReAct-style notebook format.
  - https://github.com/DatarusAI/Datarus-JupyterAgent /MIT/python
  - [Datarus-R1: An Adaptive Multi-Step Reasoning LLM for Automated Data Analysis | Abstract](https://www.arxiv.org/abs/2508.13382)

- [Ellbendls/Qwen-3-4b-Text_to_SQL · Hugging Face _202509](https://huggingface.co/Ellbendls/Qwen-3-4b-Text_to_SQL)
  - a fine-tuned version of Qwen/Qwen3-4B designed to convert natural language queries into SQL statements
  - In scenarios where table schema context is missing, the model is trained to generate schema definitions along with the SQL query

- [jupyter-agent/jupyter-agent-qwen3-4b-instruct · Hugging Face _202509](https://huggingface.co/jupyter-agent/jupyter-agent-qwen3-4b-instruct)
  - a fine-tuned version of Qwen3-4B-Thinking-2507 specifically optimized for data science agentic tasks in Jupyter notebook environments
  - This model can execute Python code, analyze datasets, and provide step-by-step reasoning with intermediate computations to solve realistic data analysis problems.
  - Dataset domains: Primarily trained on Kaggle-style data science tasks
  - https://github.com/huggingface/jupyter-agent /202509
  - https://huggingface.co/spaces/lvwerra/jupyter-agent-2
  - Context window: Limited to 32K tokens, may struggle with very large notebooks
  - Tool calling format: Requires specific scaffolding for optimal performance
  - [jupyter-agent/jupyter-agent-qwen3-4b-thinking · Hugging Face](https://huggingface.co/jupyter-agent/jupyter-agent-qwen3-4b-thinking)
  - [Jupyter Agents: training LLMs to reason with notebooks](https://huggingface.co/blog/jupyter-agent-2)

- [mlfoundations/tabula-8b · Hugging Face _202406](https://huggingface.co/mlfoundations/tabula-8b)
  - model for prediction (classification and binned regression) on tabular data.
  - fine-tuned from the Llama-3 8B model
  - [TabuLa-8B: a foundation model for prediction on tabular data : r/LocalLLaMA](https://www.reddit.com/r/LocalLLaMA/comments/1dmnlv0/tabula8b_a_foundation_model_for_prediction_on/)

- [defog/llama-3-sqlcoder-8b · Hugging Face _202405](https://huggingface.co/defog/llama-3-sqlcoder-8b)
  - model for text to SQL generation for Postgres, Redshift and Snowflake 
  - Finetuned from model: [Meta-Llama-3-8B-Instruct]
  - 🆚 [Difference between the llama-3-sqlcoder-8b model vs. sqlcoder-7b-2 model.](https://huggingface.co/defog/sqlcoder-7b-2/discussions/47)
    - 无回复
  - https://x.com/rishdotblog/status/1788650171246551086 _202405
    - Llama-3 based SQLCoder 8b is out! Open weights with a commercially friendly cc-by-sa license. Probably the best <10B param model for Postgres text to SQL right now.
    - Our previous small model (sqlcoder-7b-2) was good at generating 0-shot SQL, but did terribly at following instructions. So while it was great in our evals, it was lacking in real-world use-cases where instruction following is much more important.
    - To address this, we trained this model with much more instruction data. We also made our original eval much harder to make sure we stayed on the right track.
    - Changes to prompt: You previously had to use our slightly idiosyncratic prompt for best results. Now, you can just use the standard Llama-3 instruct prompt.

- [defog/sqlcoder-7b-2 · Hugging Face _202402](https://huggingface.co/defog/sqlcoder-7b-2)
  - model for natural language to SQL generation.
  - Finetuned from model: [CodeLlama-7B]
  - [Use ReAct prompting with this model](https://huggingface.co/defog/sqlcoder-7b-2/discussions/37)
    - unfortunately our model is not trained for such chain-of-thought (CoT) prompting; it is only meant to be used as a direct interpreter from your question + instructions + schema to the final SQL query. This is partly due to the small size of the model

- [motherduckdb/DuckDB-NSQL-7B-v0.1 · Hugging Face _202401](https://huggingface.co/motherduckdb/DuckDB-NSQL-7B-v0.1)
  - NSQL is a family of autoregressive open-source large foundation models (FMs) designed specifically for SQL generation tasks
  - based on Meta's original Llama-2 7B model and further pre-trained on a dataset of general SQL queries and then fine-tuned on a dataset composed of DuckDB text-to-SQL pairs.
  - 200k DuckDB text-to-SQL pairs, synthetically generated using Mixtral-8x7B-Instruct-v0.1, guided by the DuckDB v0.9.2 documentation

- [distil-labs/distil-qwen3-0.6b-SHELLper · Hugging Face](https://huggingface.co/distil-labs/distil-qwen3-0.6b-SHELLper)
  - [SHELLper 🐚: Multi-Turn Function Calling with a <1B model : r/LocalLLM](https://www.reddit.com/r/LocalLLM/comments/1qnjiym/shellper_multiturn_function_calling_with_a_1b/)
  - Small models struggle with multi-turn tool calling - out of the box, Qwen3-0.6B achieves 84% accuracy on single tool calls, which drops to just 42% over 5 turns. Our tuning brings this to 100% on the test set, delivering robust multi-turn performance.
# more
- https://github.com/NVIDIA/RULER /旧测评未更新
  - What’s the Real Context Size of Your Long-Context Language Models?
  - RULER generates synthetic examples to evaluate long-context language models with configurable sequence length and task complexity.

- [Qwen3: How to Run & Fine-tune | Unsloth Documentation](https://docs.unsloth.ai/models/qwen3-how-to-run-and-fine-tune)
