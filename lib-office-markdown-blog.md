---
title: lib-office-markdown-blog
tags: [blog, markdown]
created: 2023-09-21T16:44:00.025Z
modified: 2023-09-21T16:44:11.438Z
---

# lib-office-markdown-blog

# guide

# blogs

# blogs-extensions

## [MarkDown图片存储格式-Textbundle格式 - 知乎](https://zhuanlan.zhihu.com/p/368463926)

- 由于MarkDown纯文本文件的特性，其在附带图片时，图片的保存和传输成为一个大问题
- 常用的解决图片传输问题的方案
- 图片和Base64格式转换
  - 将图片信息转为Base64格式的文本信息进行保存，阅读时再转译为图片。这样可以实现纯文本与图片的转换
  - 一张图片其转译出的Base64纯文本文件比原图片文件更大，其原始是转译过程中图片的每六位数据被充实为8位，以实现存储格式的对齐
  - 对文档的存储空间和处理性能带来巨大压力，因此发现利用Base64转译不多的几张图片后，MarkDown浏览非常卡顿
  - 这样已经扭曲了MarkDown文件高效纯文本的优点
- 利用网络图床存储
  - 把图片以网络链接的形式存储，在打开MarkDown文件时同时间下载图片
  - 图片的网络存储成本和稳定性
  - 依赖于网络
- Textbundle文件格式
  - 能否使用一种通用文件标准格式来实现图片和文本的共同转移呢？ 实际上，目前Textbundle文件格式正是用来实现此目的的方案
  - `.textbundle`文件格式本质上是文件夹，因此进行如思维导图的导入导出，数据传输等整体功能时，需要进行压缩
- `.textbundle`文件夹内容
  - `assets`文件夹: 保存纯文本Markdown文件的图片等附件
  - `info.json`: 显示.textbundle文件的相关信息
  - `text.md`: 文档本体，是.textbundle文件的真正核心了
- Xmind等工具支持MarkDown文档导入和导出，其实也是支持.textbundle格式导入导出的
# more
