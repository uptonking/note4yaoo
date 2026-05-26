---
title: lib-ai-sr-community-audio-tts
tags: [audio, community, tts]
created: 2026-05-26T20:48:10.287Z
modified: 2026-05-26T20:48:55.493Z
---

# lib-ai-sr-community-audio-tts

# guide

# discuss-stars
- ## 

- ## 

- ## 

- ## 看来 TTS 对资源的消耗是远远大于 ASR，在Mac M1芯片上做个对比：
- https://x.com/leeoxiang/status/1918642940135845904
  - ASR:  Sencevoice 转录10秒的音频大概需要 300ms；
  - TTS:  F5 合成一个2秒的音频大概需要7秒；
  - 有没有效果较好，速度又快的开源TTS模型？

- Kokoro我觉得还能接受啊
- 速度最快的就是Kokoro  其他 F5 TTS/ index-tts/ MegaTTS3 / FireRedTTS  / CosyVoice 每个TTS功能侧重点不同 例如零样本 或 有的是追求语气效果
# discuss-tips
- ## 

- ## 

- ## 

- ## 
# discuss-models
- ## 

- ## 

- ## 

- ## 

- ## [Kitten TTS V0.8 is out: New SOTA Super-tiny TTS Model (Less than 25 MB) : r/LocalLLaMA _202602](https://www.reddit.com/r/LocalLLaMA/comments/1r8pztp/kitten_tts_v08_is_out_new_sota_supertiny_tts/)
  - Kitten ML has released open source code and weights for three new tiny expressive TTS models - 80M, 40M, 14M (all Apache 2.0)
  - https://github.com/KittenML/KittenTTS
  - The smallest model is less than 25 MB, and around 14M parameters. All models have a major quality upgrade from previous versions, and can run on just CPU.

- The voices are so cute!
# discuss-toolchain
- ## 

- ## 

- ## 

- ## 
# discuss-examples/cases
- ## 

- ## 

- ## 

- ## [求推荐：适合中文有声书旁白配音的 TTS 模型/方案 - LINUX DO _202605](https://linux.do/t/topic/2241670)
- 先试试像Qwen3-TTS这样写详细的控制指令能不能令你满意地处理较长旁白文本

如果不能接受，找能用 tags 如 `[laughter] / <Laughter:2>` 这种的 TTS 模型

先用 AI 将 tags 插入到旁白文本，然后用AI生成的文本生成旁白

支援的模型例子有：
OmniVoice, Step-Audio-EditX, Fish Audio S2 Pro

- 感谢佬回答，百炼平台的tts模型（包括了qwen3 tts）全都试过了，用instruct指令控制的感情效果都不太理想，第二种方案我这两天可以看看

- 个人感觉克隆的音色和模型支持的voice都比较稳定，但是感情和语速都还是硬伤

- 可以试下这个项目 OmniVoice-Studio，ElevenLabs 的开源替代方案

- 我需求是大批量的自动化配音，所以说剪映不适合

- 看看讯飞的超拟人合成方案，长文和流式都支持。音色、语调、语气、语速等都可以调

- 就音色克隆角度来说，voxcpm挺不错的，4060 8G会略爆一些显存
qwen3 TTS ，omniVoic，chatterBox在音色克隆方面非常生硬，但生成速度qwen3TTS和chatterBox是优于voxcpm，而且显存占用很小
voxcpm可以调整情绪，停顿，方言（我没试过）
部署方面，voxcpm也比较简单，qwen3TTS官方文档只有linux的，不过这四个都可以找到windows一键启动包

- 我最近也在对接微软的tts，问一下佬，如果输入的中文，但是选择的语言的是英文或者其他，输出的语音是不是也是中文，不支持翻译的?

- 前段时间我也在搞tts配音，用的qwen3tts，当时我是把1，2个章节为窗口输给llm，让llm分析角色性格，以及每一段的应该有的语气，然后使用qwentts的design模式
  - 然后发现design模式会有角色音色不一致的问题，但是clone模式又不能控制说话的情绪，于是又用找了openvoice，我看openvoice可以不改变情绪的情况下迁移音色。
  - 然后使用qwen的design模式生成有情绪的音频，同时角色第一次出现就生成角色的音色音频片段，然后送入openvoice使用角色的音色替换前面那个有情绪的音频片段。
- 佬的想法和我现在的想法差不多，都是先生成类似于剧本的json，但是我没有用VD+Clone（Qwen3 TTS） ，就是像佬所说的一样，不能用instruct控制情绪，到时候我去了解一下openvoice，看看具体的效果
- 我也有这个问题，所以我在 qwen tts 放弃了 clone 模式，使用音色控制（用预设音色 + 控制指令） 人物不多时还可以用这方法。如果用克隆音色 + 情绪指令/ tags，情绪好像不太明显

- 强烈推荐，微软的Azure，中英文发音友好，SSML能实现细颗粒度的控制
# discuss
- ## 

- ## 

- ## 

- ## 
