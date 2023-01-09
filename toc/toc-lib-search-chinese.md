---
title: toc-lib-search-chinese
tags: [Chinese, search, toc, 中文搜索]
created: 2023-01-02T21:20:41.586Z
modified: 2023-01-02T21:21:24.871Z
---

# toc-lib-search-chinese

# guide
- 主流搜索引擎自身或社区大多已提供中文搜索方案
# search-chinese
- level-min /4Star/MIT/202208/ts
  - https://github.com/heyauri/level-min
  - 一个支持中文的轻量级全文搜索库，基于Node与LevelDB。
  - 依赖segmentit、natural、stopword、level8、franc
  - TF-IDF Similarity based full text search
  - With a built-in text processing procedure: Tokenizer, Porter Stemmer and Stopwords filter.

- https://github.com/xieyezi/lyra-cn
  - a tool for offline search Chinese.
  - 添加对拼音的支持，如搜索"砍伐"的结果包含"看法"

- https://github.com/chankamlam/chinese-search /201904/js
  - 全文检索组件, 基层实现依赖nodejieba中文分词和redis存储

- racci /18Star/ISC/201706/js
  - https://github.com/iinitd/racci 
  - A lightweight search engine for Node.js, Chinese supported.
  - 依赖nodejieba、segment、lowdb
  - Support two search mode: full-text search and field search

- https://github.com/sxyizhiren/cn-search
  - ch-search , a light-weight chinese search engine based on reds, english support also.

- pinyin-match /679Star/MIT/202112/js
  - https://github.com/xmflswood/pinyin-match
  - 拼音匹配，具备分词、缩写、多音字匹配能力，支持繁体版
  - 简体版27KB (gzip ≈ 19KB)，繁体版86KB (gzip ≈ 60KB)
  - [如何实现一个高效的拼音匹配库？解决多音字，首字母匹配等问题 - 掘金](https://juejin.cn/post/6844904161461403661)
  - https://github.com/ReAlign/pinyin-so /202005/ts
    - 拼音搜索方案，支持 全拼/简拼/同音字 等。
# tokenizer
- https://github.com/fxsjy/jieba
  - “结巴”中文分词：做最好的 Python 中文分词组件

- https://github.com/cxumol/jieba-wasm-html
  - 结巴分词网页版, 基于 WebAssembly 的纯前端实现; 亦可用于 Deno
  - Fast Jieba Chinese text segmentation on browser. 
- https://github.com/fengkx/jieba-wasm
  - WASM binding to jieba-rs
- https://github.com/HerrCai0907/jieba.js
  - compile cpp version to wasm and can run in javascript

- chinese-tokenizer /72Star/MIT/201906/js
  - https://github.com/yishn/chinese-tokenizer
  - Simple algorithm to tokenize Chinese texts into words using CC-CEDICT.
  - This tokenizer uses a simple greedy algorithm: It always looks for the longest word in the CC-CEDICT dictionary that matches the input, one at a time.
  - forks
  - https://github.com/tadashi-aikawa/chinese-tokenizer
    - does not depend on Node.js.

- segmentit /189Star/MIT/201902/js
  - https://github.com/linonetwo/segmentit
  - 任何 JS 环境可用的中文分词包，fork from leizongmin/node-segment
  - 本模块基于 node-segment 魔改，增加了 electron、浏览器支持，并准备针对 electron 多线程运行环境进行优化。
  - 之所以要花时间魔改，是因为 segment 和 nodejieba 虽然在 node 环境下很好用，但根本无法在浏览器和 electron 环境下运行。
  - 我把代码重构为 ES2015，并用 babel 插件内联了字典文件，全部载入的话大小是 3.8M，但如果有些字典你并不需要，字典和模块是支持 tree shaking 的
# chinese-utils
- https://github.com/ray306/CharDB
  - A Comprehensive Database and Search Engine of Chinese Characters
# more-search-chinese
