---
title: thread-domain-crawler
tags: [crawler, thread]
created: 2025-02-03T15:10:55.606Z
modified: 2025-02-03T15:11:10.478Z
---

# thread-domain-crawler

# guide

# discuss-stars
- ## 

- ## 

- ## 
# discuss-tools
- ## 

- ## 仔细看了下这些流量的来源。因为我们是套了 CF 盾的，一开始我还以为是哪个高手的绕过了 CF 盾，结果一看 UA 居然是 meta 的爬虫。
- https://x.com/arvin17x/status/1927989856053121431
  - 然后果断把这个 UA 加进 firewall deny 了，然后请求量一下子就降了下来。
  - 不过还是得夸一下 Vercel ，看了下这波爬虫 DDOS 的 rps 是直接打到了 100+ ，rpm 打到 5k+，换个小机估计就直接挂了。

- 被 bing 盯上的话也差不多，可以设置个阈值给他们响应 429 降速，不过 meta 和 bing 的爬虫重复率真的巨高，不知道一个劲在那做冗余操作有个沙雕用

- 先加到CDN的黑名单中

- ## puppeteer is the single worst library ever written
- https://x.com/ThePrimeagen/status/1892222755484942492
- use stagehand!! it's playwright + AI, and playwright is a more robust version of puppeteer.
- I have some experience with Playwright, which is not that bad. Selenium was a lot harder to get things right, although with LLMs maybe things changed on the field.

# discuss-paywall
- tools
  - medium : https://freedium.cfd/

- ## 

- ## 

- ## [I created a website to remove medium paywall : r/SideProject _202402](https://www.reddit.com/r/SideProject/comments/1az0xr0/i_created_a_website_to_remove_medium_paywall/)
- I just don't allow medium to set any cookies in my browser, it has the same effect.
- Or just clear them from site settings when you want or open in incognito
  - Doesn't works anymore. Medium just kick you out if you block the cookies

- https://codeberg.org/Freedium-cfd/web
  - How does Freedium work?
  - In the first version of Freedium, we reverse-engineered Medium.com's GraphQL endpoints and built our own parser and toolkits to show you unpaywalled Medium posts. 
  - Unfortunately, Medium closed this loophole and nowadays we just pay subscriptions and share access through Freedium. Sometimes we got a bugs because of the self-written parser, but we are working to make Freedium bug-free.
# discuss
- ## 

- ## 

- ## 

- ## Best CLI for crawling a URL and turning it into LLM-ready text... hit me
- https://x.com/mattpocockuk/status/1904208550127186104
- firecrawl, or even home made code + LLM call actually
- crawl4ai

- ## SourceHut 的站长，公开发表文章（下图），痛斥 AI 爬虫太过份，服务器无法承受访问压力，中断服务。
- https://x.com/ruanyf/status/1905419401958170675

- ## 一个需求： 把过去 24小时，小红书的爆款笔记，爆款商品拉出来。每天早晨收到这份列表
- https://x.com/huangyun_122/status/1885541683611177233
  - 1/ 我的 RPA 已经可以拉到数据
  - 2/ 用本地  ollama 模型做下笔记，商品标题提炼
  - 3/ 发送给订阅邮件/微信
- 这种 rpa 不会容易被封吗
  - 会啊，被封了好几个了。成本贼高
- 内容多了，有向sns营销行业的wind、bloomberg发展的潜质
