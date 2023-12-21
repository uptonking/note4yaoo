---
title: thread-pm-app-tool-ideas
tags: [app, ideas, products, thread]
created: 2022-11-07T10:02:52.517Z
modified: 2022-11-07T10:58:24.512Z
---

# thread-pm-app-tool-ideas

# guide

- 产品的入口形态比较
  - 浏览器，需要用户培养习惯，优点是方便跨端
  - 系统级组件如spotlight，优点是与系统是深度集成、操作方便，缺点是通用性不强

- 某一类数据源聚合的产品
  - 搜索多个app-store，如flathub/snap
# ideas
- 数据碎片搜集
  - pc, mobile, browser ext
    - list-pin
    - 复制列表/表格数据
    - 表格行列数统计

- 大而全的产品如google/notion使用方便，但特定场景的解决方案仍然有生存空间
  - linear，挑战jira
  - zendesk，客户帮助平台
  - roadmap/feedback, canny
# datable/数据整理
- 政府数据
  - 各级统计局
  - 国外统计局

- 经典数据集
  - 权威公开数据

- 各大公司技术博客

- 中科院PubScholar公益学术平台

- color-mode-converter
  - rgb-hsl-hsv/b-contrast
# sharing
- 规避版权问题的内容讨论平台
  - 科技分享，类似hacker-news
  - 产品讨论，类似product-hunt
  - 打分评论，类似豆瓣电影与音乐
  - 论坛圈子，类似贴吧/reddit，支持一个url在不同板块重复讨论、多次讨论

- 分享设备的dock栏

- 分享有设计感的网站、主页
# integrations
- doscord message saver
  - [Discord Notebook](https://chrome.google.com/webstore/detail/discord-notebook/jeeilfacglnffgflhgmciaegglekjlod?hl=en)
  - the extension will save your messages locally in your browser storage.
  - 因为discord前端升级而不可用了，要等待作者更新
  - 可参考 betterdiscord 的 favorite media 插件
# saas

# tools/productivity
- office许可过期
  - https://github.com/infohost/infohost.github.io/blob/main/office-license-is-not-genuine.html
  - https://htmlpreview.github.io/?

## markdown-formatter

- [sumnow/markdown-formatter](https://github.com/sumnow/markdown-formatter)
- 代码块格式化时，开始3个\`会对齐到行首，末尾3个没对齐到行首，前面会有空格
  - 给代码块加上语言后，就可以自动对齐了
- link的圆括号内默认带有 `https://` ，这样粘贴url时就会重复这一段
- 带有空格的空行格式化时会单独占一行，浪费空间
- 格式化多个连续的转义字符时，斜杠会混乱
- 会自动在点号后，大写英文字母前加空格，这会破坏代码中的调用，如React. Component
# effect-playground
- 文字不可选择、不可复制
  - https://www.mingyantong.com/ju/5704496
# running
- 国内的跑步类app几乎都不支持导出数据
- 国内的gps工具类app几乎都将导出数据或批量数据操作作为付费功能
- 国外的运动、gps类app几乎都依赖google服务
- 跨国公司如nike砍掉了不盈利的nike run club网页版

> 结论是，如果要完全掌握数据，则需要选择支持导出gpx数据的硬件，不能是硬件不支持而必须在网页或app操作导出的那种产品

# study-room 自习室
- 量贩式，按小时

- 租期制，包月/季
# dormitory

# business-features

- links
  - 外链，显示链接或简化版文字可减少干扰，减少用户离开；支持付费自定义card样式

- 内容页面都可公开访问，但页面中部分敏感数据或结论默认是隐藏或付费可见
  - 敏感内容不会被seo或泄露，但普通内容可正常访问

- 付费问答或咨询
  - 提问免费，提问可发起奖励，回答者可领取奖励
  - 奖励型问题可设置回答部分可见、二次付费可见

- ActionText

- public dataset
  - 统计年鉴
  - 中国裁判文书网
# discuss
- ## 

- ## 

- ## 推荐一款语音识别 APP，Whisper Transcription，
- https://twitter.com/Barret_China/status/1730988938641449287
  - 这款软件基本属于对 Whisper 模型的本地套壳，附加了诸多体验优化和额外功能模块。看来在大模型时代只要肯动手，还是有很多机会的
  - 软件大小只有 10Mb，要支持语音识别，需要从远端将大模型下载到本地，官方 Whisper 提供了 tiny/base/small/medium/large 等不同 size 的模型，需要 large 版本（~1.5Gb）才支持多语言，这个软件竟然所有版本都支持，看来是经过了一次微调。我试了下 tiny 版本，基本可用，large 版本下载太慢了，还没测试。
- 这都能卖88，我搞了一个完全免费🆓的，看来我还是不太会做生意
- 不是的，本来小模型（tiny，small，medium）就是支持多语言的。另外，还有一套只支持英语的模型，从tiny到medium，速度更快且精度更高
  - 查了一下，是的，我记错了

- ## Any good tool to collect and organize important links from the internet?
- https://twitter.com/dobroslav_dev/status/1730985170138800213
  - Features: Make collections, see automatic link preview, etc.
- I recommend http://linkcollect.io 
- I made https://linkace.org (open source, self hosted, php)
- Use a Notion db
- Google keep
