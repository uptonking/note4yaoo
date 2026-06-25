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

- ## [2026年了，目前最好用的pdf翻译工具是什么 - LINUX DO _202606](https://linux.do/t/topic/2422644)
- 翻译只是小问题。排版问题真的很难解决，只能大概保持排版

- 几种方法：
  - 直接去doc2x，一个多功能翻译网站，适合想要无脑直接翻译的，而且目前做得最好
  - PDF转成md，适合全是文字而且不考虑排版只要信息的，具体怎么转换和skill可以问AI，有好几个开源GitHub项目了，文字提取和OCR等等都有
  - 如果是需要阅读论文（有很多排版和数学公式，图表这些的），arXiv上几乎绝大部分的论文都可以下载tex源码（硬性要求的），你可以下载tex源码到本地让AI翻译成中文版的tex源码再编译，这是我目前读论文的办法，熟练工作流之后就非常舒服了，完美保留数学公式和图表的前提下，论文的布局还很好看（直接翻译很多时候由于中文和英文长度不同，可能排版不太好看）
  - PDF有很多种，本身也不简单，有压缩有各种处理，并没有一个一概而论的好办法，具体翻译要根据你的类型，要求来定。我最早想要直接解码PDF，翻译PDF的源码，但很多时候有压缩加密等等搞起来很麻烦，也没有统一，上述的几种是目前我总结的方法，

- 我倒是找到了一个方案：让codex等把pdf转为html，html大概率可以把原文档的编排格式保留下来，如果有差异，可以通过chrome mcp，让codex自己对比和改。然后再让dpsk把html翻译为中文，得到中文的html。最后可以通过nginx或扔到github.io上查看

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

- ## [智能多阶段翻译工具 - 基于AI的精准翻译解决方案 - LINUX DO _202606](https://linux.do/t/topic/2471487)
  - 基于宝玉的翻译提示词实现了对应的可视化页面，并在此基础上更进一步，引入领域自适应翻译能力，即通过大模型首先判断当前文本所属领域，并动态分析其中涉及到的专有名词，再通过直译、发现问题、意译的3步推导，得到理想的翻译结果。
  - https://github.com/ws1993/translationAgent

# discuss
- ## 

- ## 

- ## 

- ## 

- ## 

- ## [佬友们有做AI翻译系统的么，怎么才能实现高准确度翻译 - LINUX DO _202606](https://linux.do/t/topic/2462679)
  - 直接调用大模型效果肯定是不理想的，如果追求高准确度高标准的翻译，佬友们有过什么实现经验么。目前还在研究中的就是术语库。不过感觉术语库怎么建设应该也是有点说法的。再一个就是参考标准译文例句。用这两个作为提示语料给AI作为翻译新语料的依据。不过目前依然会遇到歧义词、语序等等问题，不知道佬友们有没有这方面经验。
- 可以试试跟你你翻译内容的领域先让ai去建立术语库，搜索信息ai还是可以干的。建完了让几个ai去交叉核对校验就好了，这种劳动可以交给ai。
翻译也是可以让速度快的模型去先快速翻译，然后交给高级模型按照你的要求和术语库审核纠错。感觉在改错纠正的时候ai会更遵从定下的翻译规范。
想要高质量准确翻译，关键感觉是要让ai自检或者交叉检验。
就是一套下来速度会比较慢，实时翻译可能就只能纯靠提示词，找找提示词了。

- 那你是要专业术语的翻译？那就找个翻译对照表，用开源的翻译模型然后喂对照表自己续训一个模型出来就行了
