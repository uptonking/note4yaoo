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

## more-asr

- https://github.com/wenet-e2e/wenet
  - Production Ready End-to-End Speech Recognition Toolkit
# text-to-speech
- https://github.com/PaddlePaddle/PaddleSpeech
  - PaddleSpeech 是基于飞桨 PaddlePaddle 的语音方向的开源模型库
  - 目前服务集成的语音任务有： asr (语音识别)、tts (语音合成)、cls (音频分类)、vector (声纹识别)以及 text (文本处理)
  - 基于规则的中文前端: 我们的前端包含文本正则化和字音转换（G2P）
  - [【超简单】之基于PaddleSpeech搭建个人语音听写服务 - 掘金](https://juejin.cn/post/7124872238825734175)
  - [💡TTS 端上部署信息汇总](https://github.com/PaddlePaddle/PaddleSpeech/issues/3037)
  - [💡离线使用 paddlespeech](https://github.com/PaddlePaddle/PaddleSpeech/issues/2909)
  - [离线语音识别的解决方案](https://github.com/PaddlePaddle/PaddleSpeech/issues/2622)
  - [这个 demo 是一个启动离线语音服务和访问服务的实现](https://github.com/PaddlePaddle/PaddleSpeech/blob/develop/demos/speech_server/README_cn.md)

- https://github.com/coqui-ai/TTS
  - a deep learning toolkit for Text-to-Speech

- https://github.com/nateshmbhat/pyttsx3
  - Fully OFFLINE text to speech conversion
# discuss
- ## 

- ## 

- ## 现在的视频翻译突然间火了，推友们，可以告诉我使用了什么技术吗？
- https://twitter.com/lxfater/status/1718639301813215543
- VideoReTalking：让视频中的人物的嘴型与输入的声音同步。
- [HeyGen - AI Spokesperson Video Creator](https://app.heygen.com/login)
