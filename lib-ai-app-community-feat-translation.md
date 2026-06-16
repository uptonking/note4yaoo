---
title: lib-ai-app-community-feat-translation
tags: [ai, community, large-language-model, translation]
created: 2026-02-01T08:24:42.310Z
modified: 2026-02-01T08:25:22.883Z
---

# lib-ai-app-community-feat-translation

# guide

# prompts-for-translation
- 中文翻译成英文: 我牙疼的受不了了，去医院看门诊， 医生给我开了甲硝唑片，吃了后牙就不疼了。
  - Natural & Standard (Recommended): "My toothache was unbearable, so I went to the hospital. The doctor prescribed Metronidazole, and the pain went away after I took it."
  - Casual / Spoken Style: "My tooth was killing me, so I went to see a doctor. He gave me a prescription for Metronidazole. Once I took the pills, the pain stopped."
# discuss-stars
- ## 

- ## 

- ## 

- ## 
# discuss-pm-translation
- ## 

- ## 

- ## 

- ## tired of waiting for books to be translated into my language, so I built BookTranslator.
- https://x.com/DottChen/status/2066748909909885064
  - [Translate Your Book Online — Upload PDF, EPUB or DOCX | BookTranslator ](https://www.booktranslator.app/translate-book)

- ## [腾讯混元离线大模型翻译APP来了 - LINUX DO _202605](https://linux.do/t/topic/2184185)
  - 腾讯专门为手机CPU设计的STQ内核，该方案实现了对SIMD指令集的完美适配。最终，3.3GB的原始模型被进一步压缩至440MB，轻松常驻后台，让内存紧张的普通手机也能顺滑进行高质量离线翻译。
  - https://huggingface.co/AngelSlim/Hy-MT1.5-1.8B-1.25bit-GGUF

- APP就是个壳子，还需要你下载模型权重。实现形式好像是你通过复制的时候，有个后台读取模式，走的悬浮窗翻译

- 有手机离线翻译需求的人不多吧，费电效果还不一定好

- 用下来，比之前的RTranslator要强一点，那个错得更离谱。当然，要是和8B的Qwen、Gemma相比，那肯定是菜鸟水平了 

- 你把在线的闭源旗舰模型和离线的本地的开源小模型进行比较，本身就有点不太公平吧 

- 占内存有点多，但是我觉得手机只有无法联网的环境才有必要用离线翻译模型。调api又快又好

- 手机最难搞的还是那种划词悬浮窗翻译，手机厂商自带的一般都比较拉而且还带反诈，想要自己配的话，要写APP也很麻烦

- ## [用 HY-MT-1.5模型做个全端的翻译软件还有市场吗？ - LINUX DO _202605](https://linux.do/t/topic/2126358)
  - 最近想着做款软件，看到混元开源了顶级的翻译模型，体积也不大，600m左右。拿来做个翻译软件，在本地终端大概有个70tokens/s。整体翻译效果还不错。想着是不是要比传统的翻译软件要翻译得好呢？

- 要是有视频翻译、文档翻译、网页翻译（直接拦截代理的）那就很牛了

- 能够做到有道的平替，没有广告，没有等待。打开即用。如果能够在科研等专属领域翻译都得到认可的话，应该会更好了。不知道这个模型的能力是不是这么强
# discuss-toolchain
- ## 

- ## 

- ## 

- ## 

- ## 

- ## [【翻译 Skill 分享】将任何格式、任意长度的外文材料变为母语译本 - LINUX DO _202606](https://linux.do/t/topic/2409217)
  - 读外文资料时，常被翻译步骤卡住。 现有的翻译服务（如沉浸式翻译 BabelDOC PDF、DeepL），速度快，但质量一般。
  - 尝试用 web 工具 将长文分片后再并行调用 LLM 翻译。有所改善，但还是有缺点： 不够方便。提取与清洗文本、术语表整理和提示词设计都得自己来。 翻译质量一般。因为分片之间的风格一致性和逻辑连贯性不太好
  - 直到发现这个项目 baoyu-translate skill。我在该项目的基础上，按自身需求不断调整，得到了现在的版本：longtext-translate skill
  - https://github.com/zlhhhh8901/longtext-translate
  - https://compare-gules.vercel.app/
  - PDF / EPUB / WORD 支持只翻译指定页码或章节范围的内容
  - 运行模型：deepseek-v4-pro（推理强度 High，ClaudeCode 环境），走完「翻译 + 审校 + 精编」全流程

# discuss-models-mt
- ## 

- ## 

- ## 

- ## Open-sourcing Hy-MT2, Three model sizes, 33 languages:  _202605
- https://x.com/TencentAI_News/status/2057400913061650805
  - 1.8B: 440MB, runs on mobile chips, beats Microsoft's API
  - 7B: best-in-class among open-source models
  - 30B-A3B: state-of-the-art, outperforms models 10x its size
- There is mismatch between “open-sourcing” and the license file

# discuss-tips
- ## 

- ## 

- ## 

- ## 
# discuss
- ## 

- ## 

- ## 

- ## 
