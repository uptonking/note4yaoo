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


# discuss

- ## 

- ## 

- ## I just used OpenAI embeddings to embed half a million tweets and ended up paying ... $3!!!
- https://twitter.com/fleuria__/status/1634125805717704704
- 本义是说把过往做法中维度成千上万的特征（每个词项以及数十种人工特征构造一个巨大的one-hot）像镶钻一样嵌入(embed)一个低维流形（想象一个2维描述的三维球面），优化算法会想办法调整这些特征在球面上嵌入的位置。每个词项就需要对应它的低维表示，存下来的东西实质上就是个KV查询表(embedding)。
  - 只不过发展到现在不一定这个embedding就真的是低维度了（
  - 几十个词把embedding设成256等等之类的也很常见（
  - 甚至有研究表示over-parameterize才是正道（

