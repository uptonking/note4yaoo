---
title: lib-ai-nlp
tags: [ai, nlp]
created: 2023-03-03T08:06:19.133Z
modified: 2023-03-03T08:06:36.592Z
---

# lib-ai-nlp

# guide

- [NLP新宠——浅谈Prompt的前世今生 - 知乎](https://zhuanlan.zhihu.com/p/399295895)
- [通俗易懂地理解Prompt - 知乎](https://zhuanlan.zhihu.com/p/436340881)
  - Prompt是给input加的一段文字或一组向量，让模型根据input和外加的prompt做masked language modeling (MLM)。
# nlp-products

# translation
- https://github.com/mozilla/firefox-translations
  - a webextension that enables client side translations for web browsers.
  - 不支持中文
  - [Support Chinese translations](https://github.com/mozilla/firefox-translations/issues/583)

- https://github.com/jelmervdl/translatelocally-web-ext
  - https://translatelocally.com/
  - a web-extension that enables client side in-page translations for web browsers.
  - 不支持中文
  - Differences from Firefox Translations
    - Uses models from https://github.com/browsermt/students
    - Translation engine and memory is shared among all tabs and webpages
  - [Google Chrome](https://github.com/jelmervdl/translatelocally-web-ext/issues/10)

- 使用Google翻译（Translate）的离线翻译功能？有前提：你必须先在联网状态下将需要且支持离线翻译的语言下载。
  - 而离线翻译的结果会与联网翻译的结果存在结果差距。特别是翻译同一个字词语句下

- 全文翻译比较期待类似firefox做的这种离线本地翻译
  - [Firefox Translations – Get this Extension for 🦊 Firefox (en-US)](https://addons.mozilla.org/en-US/firefox/addon/firefox-translations/)

## translate-api

- https://github.com/LibreTranslate/LibreTranslate
  - https://libretranslate.com/
  - Free and Open Source Machine Translation API. 
  - Self-hosted, offline capable and easy to setup.
  - its translation engine is powered by the open source Argos Translate library.
  - 依赖flask
- https://github.com/argosopentech/argos-translate
  - Open-source offline translation library written in Python
  - Argos Translate uses OpenNMT for translations
  - 支持中日韩
