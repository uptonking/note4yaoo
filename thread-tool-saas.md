---
title: thread-tool-saas
tags: [saas, thread, tool]
created: 2023-05-07T18:35:34.827Z
modified: 2023-05-07T18:35:50.897Z
---

# thread-tool-saas

# guide

# discuss
- ## 

- ## 

- ## Anna的档案馆称他们获得了读秀图书数据库，包含750万本、总计359TB的中文非小说书籍的收藏，这个数字超过Library Genesis （530万本）。
- https://twitter.com/xiaohuggg/status/1721532104998105264
  - 如果哪家大模型公司能给他们提供OCR和文本提取服务，将会获得Anna的档案馆一年的独家访问权。
  - [独家访问：全球最大的中文非虚构图书馆藏，仅限LLM公司使用 - Anna’s Blog](https://annas-blog.org/duxiu-exclusive-chinese.html)

- ## 阿里云难得良心一次，2C2G3M 配置每年只要 99，看活动时间优惠持续四年
- https://twitter.com/cosmtrek/status/1721484209968259487
  - 托管于中国内地服务器上的网站，如果网站没有绑定域名，直接通过IP地址对外提供服务也需要进行ICP备案。目前阿里云ICP代备案管理系统只支持域名备案，不支持IP备案。重要无论网站是通过IP地址还是通过域名对外提供服务，未备案成功前，均不允许开通网站访问。阿里云官方

- 这类 VPS 适合自用，不适合严肃的生产环境。 有好多用途，比如当跳板机、网络代理、部署 Web app、文件中转、Grafana 统计、学习 PHP
- 长期用还是得看国外，续费同价。国内的云服务器过几年就得找下家。
- 最多能买两年吧？我续到第三年就是原价了

- ## 还没用过 Whisper 语音转文字？ 这里有一个在线版本，
- https://twitter.com/finedtune/status/1721049768464667127
  - 可以直接输入 YouTube 链接，也支持自己上传音频文件，不需要安装和部署，速度比初版 Whisper 快 70 倍， 1 小时音频 1 分钟就转好，关键还免费
- 我确实还没用过，因为找不到合适的使用场景，比如现在用的语音输入，讯飞输入法用的语音转文字也还挺顺手。如果需要做实时会议转录成文字之类的，可能用得上。
- 长远看油管视频的语音转文字没必要做，现在的很多油管视频已经包含了文字，用油管自己的功能几秒就把文字复制出来了

- ## [My IP Address - BrowserLeaks](https://browserleaks.com/ip)
- https://twitter.com/RkMonoChrome_CN/status/1719747686679597141
  - 检测ip，还能检测dns，DNS Leak Test
  - 如果DNS服务器里有自己手机or宽带的运营商的话那么运营商就已经知道你在翻墙了

- ## Misgif：一款可以将你的脸放入你喜欢的GIF 表情包中的应用
- https://twitter.com/xiaohuggg/status/1719186332319416388
  - [misgif: ai powered memes](https://misgif.app/)
  - 可以免费使用三次。

- ## 扫地机器人最大的bug是会挑衅到狗，然后被狗翻过来
- https://twitter.com/syeerzy/status/1717518202027331904

- ## 备份方法
- https://twitter.com/Ruohai/status/1717178829612187852
  - 新手：移动硬盘冷备
  - 中级：买nas组raid
  - 高级：买多套nas做321备份和功能区分
  - 骨灰：旧电脑装debian用rsync和rclone
- 我用 nuc 挂了一堆硬盘，都是独立的。
- 就想知道旧电脑不考虑功耗的么？
- 可以裝Unraid

- ## 一个有趣的网站「12英尺」，http://12ft.io，一位外国程序员受不了互联网充满了付费高墙，他撸了一个 12 英尺的高梯来帮助读者们翻越各种付费围墙——Show me a 10ft paywall, I’ll show you a 12ft ladder.
- https://twitter.com/Barret_China/status/1711042013230256476
- The idea is pretty simple, news sites want Google to index their content so it shows up in search results. So **they don't show a paywall to the Google crawler**. We benefit from this because the Google crawler will cache a copy of the site every time it crawls it.
- 有个插件叫Bypass Paywalls，可以破解看各大新闻网站的付费内容，估计实现原理是一样的，那些付费网站的付费内容为了搜索流量给谷歌爬虫开白名单，允许抓取付费内容，谷歌就有了文章缓存，然后把网站链接的内容替换为谷歌的缓存内容，以此绕过付费

- ## Cloudflare 的验证码服务 Turnstile（图一），对所有人开放了。只要加入几行代码（图二），就能免费嵌入自己的网站
- https://twitter.com/ruanyf/status/1710661567552045077
  - 再不必费劲识别图片和字符，只要点击一下就识别是否机器人，我觉得用户体验很不错，而且只要不用企业版功能，就都是免费的。

- 可以用 Google recaptcha_v3 企业版，用户连点击都不用，每个月的免费额度很高，不过还要自己实现服务端接口麻烦一点。

- 在中国加载这个js文件似乎有点慢，再等等看

- ## [What are your most used self-hosted applications? | Hacker News_202205](https://news.ycombinator.com/item?id=31260061)

- ## 最近有给自己的 SaaS 接入日志监控的需求，考察了两个服务:
- https://twitter.com/novoreorx/status/1658323720140881927
- https://betterstack.com/logtail/pricing
  - 免费版 1GB 存储，保留3天。Linear 风格黑色主题。
- https://axiom.co/pricing
  - 免费版 0.5TB 存储，保留30天。清爽干净的白色主题。
- axiom 底层来看应该是 grafana loki，和以前使用来比太像了。而且换算一下，如果是 loki 这个存储成本完全可以 cover 住

- ## Yandex 竟然有个完全免费、没有流量限制的网站统计服务
- https://metrica.yandex.com/
  - All-Round Web Analytics
