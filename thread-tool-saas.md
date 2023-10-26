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

- ## 

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
