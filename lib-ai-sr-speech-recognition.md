---
title: lib-ai-sr-speech-recognition
tags: [ai, speech-recognition]
created: 2023-02-07T07:16:03.832Z
modified: 2023-02-07T09:22:03.120Z
---

# lib-ai-sr-speech-recognition

# guide

- [人工智能的方向——NLP CV SR(语音识别) KG(知识图谱)](https://blog.csdn.net/qq_43165081/article/details/113790560)
# sr-products

## free-tts

- resources
  - [2025年10+最佳免费文字转语音生成器（最自然的机器配音） - 文武科技柜](https://www.wangdu.site/software/tools/924.html)
  - [免费好用的AI配音(TTS)平台全面指南：中国产品与国际平台对比 | 附详细URL、特色等 - 知乎 _202504](https://zhuanlan.zhihu.com/p/1891215909730903174)
# speech-to-text
- [用Python 搭配OpenAI 的GPT、Whisper API 取得Youtube 影片摘](https://medium.com/dean-lin/%E7%94%A8-python-%E6%90%AD%E9%85%8D-openai-%E7%9A%84-gpt-whisper-api-%E5%8F%96%E5%BE%97-youtube-%E5%BD%B1%E7%89%87%E6%91%98%E8%A6%81-4ceb57828732)

## Whisper

- https://github.com/openai/whisper /MIT/py/jupyter
  - Whisper is a general-purpose speech recognition model.
  - Robust Speech Recognition via Large-Scale Weak Supervision

- https://github.com/saharmor/whisper-playground
  - Instantly build realtime speech2text apps in 99 languages using OpenAI's Whisper
  - 近实时翻译，支持识别中英文混合语音
  - 支持包括中文在内的多种语音，新语音需要在第一次请求时下载该语言对应的语料包
  - 后端依赖flask，实现简单
  - 前端依赖react

- https://github.com/chidiwilliams/buzz
  - Buzz transcribes and translates audio offline on your personal computer. 
  - Powered by OpenAI's Whisper.
  - [Linux version](https://github.com/chidiwilliams/buzz/issues/176)
  - #Whisper 是 #OpenAI 开源的语音识别模型，OpenAI不仅开源代码而且还开源该模型的详细解释，有开发者基于此开发了图形界面 App，用户只需要在本地运行这个 App，就可以完成语音转录的工作，不需要网络和第三方的参与

- https://codeberg.org/pluja/web-whisper
  - https://whisper.r3d.red/
  - OpenAI's whisper on your web browser，后端go实现

- https://github.com/Ayanaminn/N46Whisper
  - N46Whisper 是基于 Google Colab 的应用。开发初衷旨在提高乃木坂46（以及坂道系）字幕组的工作效率。但本应用亦适于所有日语视频的字幕制作。
  - 此应用基于AI语音识别模型 Whisper
  - 先把视频放到Google Drive，然后从Google Colab上运行代码，调用OpenAI的Whisper API生成字幕，再借助ChatGPT的API对字幕逐行翻译，最后人工再校对就好了

- https://github.com/huggingface/distil-whisper /CodeNA
  - Distil-Whisper is a distilled version of Whisper that is 6 times faster, 49% smaller, and performs within 1% WER on out-of-distribution evaluation sets.
  - https://twitter.com/sanchitgandhi99/status/1719409022246220184

- https://github.com/Vaibhavs10/insanely-fast-whisper
  - TL; DR - Transcribe 150 minutes (2.5 hours) of audio in less than 98 seconds - with OpenAI's Whisper Large v3.
  - https://github.com/chenxwh/insanely-fast-whisper

- https://github.com/chenxwh/insanely-fast-whisper /jupyter
  - Incredibly fast Whisper-large-v3
  - An opinionated CLI to transcribe Audio files w/ Whisper on-device! Powered by Transformers, Optimum & flash-attn
  - TL; DR - Transcribe 150 minutes (2.5 hours) of audio in less than 98 seconds - with OpenAI's Whisper Large v3

- https://github.com/kadirnar/whisper-plus /apache2/python
  - Advancing Speech-to-Text Processing
  - 实现了从 Youtube 下视频，对于下载完的视频，还提供了， openai 的 whisper v3 直接转录成文本的代码 

- https://github.com/xenova/whisper-web /MIT/202405/ts
  - https://hf.co/spaces/Xenova/whisper-web
  - ML-powered speech recognition directly in your browser
  - Built with Transformers.js.
  - https://github.com/xenova/whisper-web/tree/experimental-webgpu
    - https://x.com/xenovacom/status/1799858691639796089
    - It would be perfect if there was a Whisper implementation that could handle real-time voice streaming

## more-asr

- https://github.com/wenet-e2e/wenet
  - Production Ready End-to-End Speech Recognition Toolkit
# text-to-speech
- https://github.com/frostming/tetos /apache2/202404/python
  - A unified interface for multiple Text-to-Speech (TTS) providers
  - Supported: OpenAI, Edge-TTS, 火山引擎

- https://github.com/collabora/WhisperSpeech /MIT/202401/jupyter
  - https://collabora.github.io/WhisperSpeech/
  - Open Source text-to-speech system built by inverting Whisper.
  - Previously known as spear-tts-pytorch.
  - Currently the models are trained on the English LibreLight dataset. In the next release we want to target multiple languages (Whisper and EnCodec are both multilanguage).

- https://github.com/PaddlePaddle/PaddleSpeech
  - PaddleSpeech 是基于飞桨 PaddlePaddle 的语音方向的开源模型库
  - 目前服务集成的语音任务有： asr (语音识别)、tts (语音合成)、cls (音频分类)、vector (声纹识别)以及 text (文本处理)
  - 基于规则的中文前端: 我们的前端包含文本正则化和字音转换（G2P）
  - [【超简单】之基于PaddleSpeech搭建个人语音听写服务 - 掘金](https://juejin.cn/post/7124872238825734175)
  - [💡TTS 端上部署信息汇总](https://github.com/PaddlePaddle/PaddleSpeech/issues/3037)
  - [💡离线使用 paddlespeech](https://github.com/PaddlePaddle/PaddleSpeech/issues/2909)
  - [离线语音识别的解决方案](https://github.com/PaddlePaddle/PaddleSpeech/issues/2622)
  - [这个 demo 是一个启动离线语音服务和访问服务的实现](https://github.com/PaddlePaddle/PaddleSpeech/blob/develop/demos/speech_server/README_cn.md)

- https://github.com/coqui-ai/TTS /MPL/python
  - http://coqui.ai/
  - a deep learning toolkit for Text-to-Speech
  - [Support offline mobile](https://github.com/coqui-ai/TTS/discussions/407)
    - You can use sherpa-onnx to run VITS models from Coqui on Android and also embedded devices, e.g., raspberry pi.

- https://github.com/nateshmbhat/pyttsx3
  - Fully OFFLINE text to speech conversion
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
# discuss-whisper
- ## 

- ## 

- ## whisper 已经很强大了，目前提供 whisper 商业 API 的产品大多还是提供基本的语音识别能力，有没有专门做 whisper 商业化的公司？
- https://x.com/leeoxiang/status/1855168937786253538
  1、热词支持
  2、实时识别能力
  3、vad 能力
  4、多说话人识别能力
  5、精准时间戳

- 话说都用商业 API 了, 你还关注别人是不是用 Whisper 实现的吗?  你只想要效果好就行了.  我估计你这些需求 Azure Speech 应该都能实现.

- 其实我有点好奇，为啥会有商业化支持的诉求，一线大厂的通用asr能力挺强的。我们之所以自己搞，主要是推理成本低很多和领域下的效果提升
  - 真实测试下来大厂的通用 asr 并没有那么好，比如多语言混合识别，语言自动识别方面。
# discuss-tools
- ## 

- ## 

- ## 一个快速将音视频转结构化笔记的开源工具：AudioNotes。
- https://x.com/GitHub_Daily/status/1886761635307544832
  - 基于 FunASR 和 Qwen2 构建，可快速提取音视频内容，并利用大模型能力整理成一份结构化的 Markdown 笔记，方便快速阅读。
  - 工具支持搭配 Ollama 使用本地模型，并提供了 Docker 快速部署方式。
- https://github.com/harry0703/AudioNotes /MIT/202407/python
  - 快速提取音视频内容，整理成一份结构化的markdown笔记

# discuss
- ## 

- ## 

- ## 

- ## 现在最好的语音转文本大模型还是 Whisper 吗？
- https://x.com/tualatrix/status/1830467181504520202
- 中文的话, 应该是 SenseVoice  MIT license, 可以自己部署. 
  - 英文的话, 应该还是 Whisper
- whisper 在中文识别方面并不好用，可能用的语料库是YouTube的居多，在音源不清晰时会出现幻觉，中文识别还是国内的好用些，速度和准确度方面都要好

- ## 阿里通义语音团队开源了语音基座大模型：SenseVoice和CosyVoice，语音方向卷起来了。
- https://x.com/leeoxiang/status/1809174787861925933
  - SenseVoice多语言音频理解大模型：多语言语音识别在中文和粤语上相比Whisper相对提升+50%，推理速度快15倍，并且支持SOTA的情绪识别。
  - CosyVoice多语言音频生成大模型：支持多语言、音色和情感控制，在多语言语音生成、零样本语音生成、跨语言声音合成和指令执行能力方面表现卓越。
  - https://github.com/FunAudioLLM/SenseVoice /MIT/python
  - https://github.com/FunAudioLLM/CosyVoice /apache2/python

- ## real-time in-browser speech recognition with OpenAI Whisper
- https://x.com/xenovacom/status/1799110540700078422
  - The model runs fully on-device using Transformers.js and ONNX Runtime Web, and supports multilingual transcription across 100 different languages
  - https://github.com/xenova/transformers.js/tree/v3/examples/webgpu-whisper
- here is a whisper example on Android
  - https://x.com/micksabox/status/1799136239683248555
- This uses Transformers.js (+ ONNX Runtime Web) vs. @fleetwood___ 's Ratchet library. His version would certainly be able to run in real-time too though... and is still on his TODO list I'm sure
- The universal translator: real-time, multilingual communication like in star trek

- ## #声音clone产品推荐 开源的实现：
- https://twitter.com/leeoxiang/status/1766700987627327683
  - 1、GPT-SoVITS： https://github.com/RVC-Boss/GPT-SoVITS    对中文、英文、日文支持都不错，需要 10 分钟左右的干素材，瞬时 clone 的能力还没开放。
  - 2、OpenVoice：https://github.com/myshell-ai/OpenVoice  对中文支持还可以，主打瞬时 clone，发展势头很好，一个月前测试的时候中文声音 clone 还有一股英语味道。

- 商业的产品：
  - 1、ElevenLab：https://elevenlabs.io  商业实现中支持语言种类最多的，支持 瞬时 clone，综合效果最好的一个产品，我是 22$每个月的订阅用户，已经在内部的配音产品上用上。
  - 2、Reecho：https://reecho.ai  中国团队，支持长音频声音 clone 和瞬时声音 clone，据说是和火山引擎的声音 clone 技术是同源的。
  - 3、自得语音：https://zideai.com  中国团队，支持瞬时声音 clone 和声音定制，还没测试。

- 瞬时克隆剪映也推送出了。类似 openvoice
  - 剪映这个限制很多，只能 clone自己的的。
  - 思路打开啊。你先克隆出志玲的语音，然后把剪映要你朗读的内容提前克隆出来，点朗读，然后不就也有了么，剪映主要语音加字幕比较方便。我把王者李白的声音克隆在剪映里了，志玲的训练好了，数据不小心丢了，懒得在去剪视频弄数据喂了

- 目前试过瞬时克隆的 还没有发现特别像的效果  11lab最大优点是稳定性很好  而且情绪调节做得不错 这一点比gpt- sovits好一些

- 用过 GPT-SoVITS 和 ElevenLab，目前对于克隆中文声音效果最好的是 GPT-SoVITS，非中文是 ElevenLab

- ## OpenAI 推出的开源免费 Whisper 在语音识别领域（ASR）可以说无出其右，
- https://twitter.com/Barret_China/status/1729521472669151516
  - 不过它有一个较大的局限性，就是无法进行说话人分类（Speaker diarization），尤其是在重叠语音检测（Overlapped speech detection）方面，Whisper 在训练过程中只识别了一个声音，同时将其他声音视为背景噪声。
  - 社区有一个发展了多年的音频处理工具包，pyannote-audio，它具备非常强大的音频分析、处理、识别和分类能力，在多人同时讲话的时候，也可以很准确地区分说话者内容，只不过它的 ASR 能力还是比不过 Whisper。
  - 有人想到结合两者的能力，并做了一个工程化的实践

- https://twitter.com/Barret_China/status/1733060966940922194
  - OpenAI 开源的 Whisper 在语音识别和翻译的工作上几乎达到了商用效果，但仍然存在一些问题，例如不能区分多人说话，尤其是声音重叠部分
  - Diart，https://github.com/juanmc2005/diart，是优化方案的一个代码实践，它构建在 pyannote-audio 模型之上，专为实时音频流（例如来自麦克风）而设计，能够以较强的性能实时地识别不同的说话人，效果非常不错。
  - 可以试试 https://github.com/m-bain/whisperX 整合方案

- ## 现在的视频翻译突然间火了，推友们，可以告诉我使用了什么技术吗？
- https://twitter.com/lxfater/status/1718639301813215543
- VideoReTalking：让视频中的人物的嘴型与输入的声音同步。
- [HeyGen - AI Spokesperson Video Creator](https://app.heygen.com/login)
