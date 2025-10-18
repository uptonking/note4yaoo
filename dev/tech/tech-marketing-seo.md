---
title: tech-marketing-seo
tags: [marketing, seo]
created: 2020-12-20T12:35:07.813Z
modified: 2020-12-20T12:36:17.694Z
---

# tech-marketing-seo

# guide

# hashtag
- [Twitter: How to use hashtags](https://help.twitter.com/en/using-twitter/how-to-use-hashtags)
  - People use the hashtag symbol (#) before a relevant keyword or phrase in their Tweet to categorize those Tweets and help them show more easily in Twitter search. 
  - You cannot add spaces or punctuation in a hashtag, or it will not work properly.

- [Twitter 的 #topic 、国内微博的 #话题# 是个好设计吗？ - 知乎](https://www.zhihu.com/question/19668872/answers/updated)
  - @”与“私信”功能的区别就是你可以公开向任何人可见
  - 由两个#框起来的文字，新浪官方的说法就是“话题”，简单来说就是搜索微博时用的关键字

- [手把手教你如何使用Hashtag做社交引流 - 知乎](https://zhuanlan.zhihu.com/p/53293490)
  - Hashtagify 会通过你的搜索词给你相关的hashtag流行趋势以及可能相关的hashtag词
  - Facebook的hashtag＃标签所支持的字符集也是跟其他平台一样，但是facebook没有对hashtag＃标签的数量进行限制
  - Instagram的hashtag# 标签也不支持特殊字符
  - 对于hashtag，pinterest也没有一个正式的规则和限制

- [新浪帮助-微博-微博发“话题”](https://help.sina.com.cn/i/204/422_12.html)
  - 简单地说“话题”就是微博搜索时的关键字，其书写形式是**将关键字放在两个井号之间**

- 微信 话题标签_202007
  - 朋友圈释放了“话题标签”这一重要的功能，格式为`#+文字`，这一内容就会变成一个可点击的超链接。近日，话题标签功能同样适用于微信聊天页面。
  - 微信内循环再放大招：话题标签全面打通公众号、视频号、小程序
  - 微信跟进微博，与好友聊天也能添加话题，可以点击这一话题词，跳转到的结果包括微信公众号、视频号和微信视频等。

- 头条
  - 头条文章标题不支持话题标签，内容中间支持插入热门话题 
  - 微头条test `#测试#`，支持话题标签，要用2个# 井号

- ## https://github.com/twitter/twitter-text
  - how characters are treated when composing Tweets and across the Twitter API.
  - [Counting characters | Docs | Twitter Developer Platform](https://developer.twitter.com/en/docs/counting-characters)
  - Twitter began as an SMS text-based service. This limited the original Tweet length to 140 characters (which was partly driven by the 160 character limit of SMS, with 20 characters reserved for commands and usernames). 
  - Over time as Twitter evolved, the maximum Tweet length grew to 280 characters - still short and brief, but enabling more expression. 
  - In most cases, the text content of a Tweet can contain up to 280 characters or Unicode glyphs.
# discuss-seo-tools
- ## 

- ## 

- ## 分享 GitHub 上一份 Google 索引脚本：Google Indexing Script。
- https://x.com/GitHub_Daily/status/1885591414924599779
  - 无需任何复杂技巧或黑客手段，只需简单的脚本和 Google API，即可让我们的网站在 48 小时内在 Google 上建立索引。
  - https://github.com/goenning/google-indexing-script

# discuss-seo-tips/tricks
- ## 

- ## 

- ## 

- ## 

- ## 🧩💡 [2/3 of my website traffic comes from LLM bots. : r/webdev _202510](https://www.reddit.com/r/webdev/comments/1o9d6w2/23_of_my_website_traffic_comes_from_llm_bots/)
  - If I were hosting my website with a serverless provider, I'd be spending two-thirds of my hosting fee on bots. 
  - I'm currently hosting my SQLite + Golang website on a $3 VPS, so I'm not experiencing any problems, but I really dislike the current state of the web. If I block bots, my website becomes invisible. 
  - Meanwhile, LLMs are training on my content and operating in ways that don’t require any visits. What should I do about this situation?

- Set up a sinkhole(污水井，污水池). Make it too expensive for these bots to crawl your website. Won't solve your problem personally, but if enough of us do it, not only will these companies spend thousands to crawl useless pages, they'll also have to spend hundreds of thousands to try and clean up their now-garbage-ridden data. Because fuck em.
- Interesting, can you tell us more? By a sinkhole do you mean a page with a huge wall of garbage text? How would you hide this from users? 
  - [Nepenthes](https://zadzmo.org/code/nepenthes/)
    - This is a tarpit(难题，困境) intended to catch web crawlers. Specifically, it targets crawlers that scrape data for LLMs - but really, like the plants it is named after, it'll eat just about anything that finds it's way inside.
    - It works by generating an endless sequences of pages, each of which with dozens of links, that simply go back into a the tarpit. Pages are randomly generated, but in a deterministic way, causing them to appear to be flat files that never change. 
    - Intentional delay is added to prevent crawlers from bogging down your server, in addition to wasting their time. 
    - Lastly, Markov-babble is added to the pages, to give the crawlers something to scrape up and train their LLMs on, hopefully accelerating model collapse.
- This says it blocks all crawlers. Are you really willing to get your website off of search engines just to get back at LLMs?
  - The ethical way to do this would be to serve it under a route that is explicitly disallowed for scraping in robots.txt. That way you're only catching the bad bots.

- Cloudflare has designed such a feature "AI Labyrinth"
  - [Trapping misbehaving bots in an AI Labyrinth _202503](https://blog.cloudflare.com/ai-labyrinth/)
  - we’re excited to announce AI Labyrinth(迷宫, 曲径), a new mitigation approach that uses AI-generated content to slow down, confuse, and waste the resources of AI Crawlers and other bots that don’t respect “no crawl” directives. 
  - When you opt in, Cloudflare will automatically deploy an AI-generated set of linked pages when we detect inappropriate bot activity, without the need for customers to create any custom rules.
  - AI Labyrinth is available on an opt-in basis to all customers, including the Free plan.

- I mean... bot traffic should be trivial to manage with basic caching. Nginx can serve pages from memory or even disk at incredible speeds.
  - My website has more than 152.000 pages. Bots crawl each page at regular intervals. Caching it would be like caching my entire website.

- First and foremost, look into installing a WAF (Web Application Firewall). CloudFlare, AWS .etc all provide products like this.
  - Secondly, you can also create a Honey Pot trap. Essentially this involves creating a link to another area on your site that isn’t visible to humans, and trapping the bots there with randomly generated nonsense web pages. 
  - Finally, if you really wanted to screw with bots, specifically MLMs — you could try your hand at prompt injection attacks, imbedded in your site.

- People are searching via LLM for solutions now and the LLM is searching the internet. Don't block it. It's the new Google.
  - Yeah but Google gave you visits which translates to money from ads. LLMs dont give you visits so you gain nothing. They dont even mention the site they fetched the info from
# discuss-seo
- ## 

- ## 

- ## 

- ## 原来发知乎的目的，是为了让百度能搜到, 毕竟百度已经不太索引新网站了, 以及B站图文也要发起来，权重也很高
- https://x.com/oran_ge/status/1819349551775732043
- 知乎的优点是，光站内就有连绵不绝的长尾流量，不像公众号和Twitter这样一波流，只有时效性流量
  - 站外流量算是知乎作为开放Web的自带长尾流量（原本除了SEO，还包含URL分享传播，但中国互联网环境对URL非常不友好）
- 从货币化角度来说，知乎跟substack/medium差距大，更多是社区而不是媒体/社交平台，社区不适合在内容本身上闭环，但可以在社区内闭环，最极端的例子是另一个社区——雪球，雪球会挖掘社区内KOL，让他们在雪球支持下（加入雪球公司）创建运营个人品牌的私募基金（比如丹书铁券）

- 可是知乎都屏蔽搜索引擎了呀
  - 百度好像有知乎的股份
  - 知乎只留下了百度和搜狗的蜘蛛，谷歌和bing这些都屏蔽了。这个方法可以免登陆看知乎问答
- 刚刚还在说发文章很重要，而且是文本内容，尽量少用海报，或者海报内容也要再用文字呈现，这样才能保证让人搜索到。抖音b站油管视频搜索也一样，作者除了精心准备视频，也需要精心准备文字描述，毕竟搜索关键字也是曝光视频的重要途径之一。

- ## 刚学习到一个新词 ASO，ASO 是应用商店优化（App Store Optimization）的缩写。
- https://x.com/jaywcjlove/status/1786377317960597691
  - 类似于 SEO（搜索引擎优化），是专门针对应用商店，如苹果的 App Store 和谷歌的 Google Play Store

- ## 今天将网站提交到各个搜索引擎，说下体验：
- https://twitter.com/YuTengjing/status/1757751907530289573
  - 百度：不需要 ICP 备案，但是没法提交 sitemap
  - 搜狗：需要资质认证，要 ICP 备案，域名是 cloudflare 买的，不打算提交了
  - 360：体验好评，添加站点，添加 sitemap 很顺畅
  - 谷歌：很顺畅
  - 必应：直接从谷歌控制台导入站点数据，很贴心

- ## 较基础的 SEO ，包括网站标题、描述、OG 卡片等元数据、整体结构的优化、
- https://twitter.com/xqliu/status/1748895482276127064
  - 其实一点不难，是典型的 low hanging fruit ，建议及早意识到快速并进行优化。
  - 推荐两个用于搜索引擎优化的Chrome扩展程序
  - Site checker
  - https://quickcreator.io 的 AI 内容创作工具

- 一些简单的优化原则（新手角度）
1. 重点是要理解 google 或者其他搜索引擎的爬虫怎么阅读咱们的页面，是和人类有区别的
2. 一个页面最好只有一个 H1 标签，且能完整概括或者描述本页的内容
3. H2 > H3 > H4 这类，逐步细化，像一棵树一样
4. 图片都增加 alt 属性
5. 如果能在页面上增加一些有使用价值的小工具，对跳出率留存率会有帮助，google 应该页能增加页面权重

- 一些简单的优化原则(2)
1. 适当增加多媒体，对SEO 和用户都好，比如 youtube 视频，据说 google 会增加有 youtube 视频的页面的权重（未确认）
2. 开始可以调研长尾关键词，而不是热门关键词。
3. SEO 的整个过程：调研 -> 计划 -> 实施 -> 回顾并继续进入到调研，进入下一轮闭环
- 推荐 http://semrush.com 工具来进行 SEO 调研

- SEO 是个过程，需要不断地调研、优化、监控、不是一个一成不变的结果，在不同的阶段，方式方法和结果也会有所差异，我在研究

- ## Build "alternative" pages as marketing. They rank easily and bring high quality traffic.
- https://twitter.com/Timb03/status/1711563242697535773
  - These compare & alterative pages have brought Pallyy over 300 signups so far.
  - They don't bring a lot of traffic, but the traffic is so targeted it has a high conversion rate.
  - It only took a day or so to setup, so it's well worth it.

- It indeed beneficial for targeted SEO.

- How did you pick up the right set of competitors?
  - Just went for the top 10 in the market as they have the most searches.

- how you tracking conversions?
  - Just Plausible, using events

- Do you use server side rendering for these pages?
  - Yeah, need those SEO benefits!

- This is good advice, all the best SaaS products do it. Don’t be scared to write positive things about your competitors. I think the best example I have found of alternative/comparison pages is @Mailtrap - they even go as far as doing tutorials for their competitors.

- ## [SEO网站收录一般几天](https://zhuanlan.zhihu.com/p/147597341)
- 大多数网站在上线提交之后，通常在20天左右就能够被搜索引擎收录，搜索引擎对于新网站的收录一般比较积极，
  - 但是搜索引擎对于新网站设置了1到3个月的考核期，根据网站内容质量决定内页的收录时间，不同的网站考核时间也会有所差异。
- 网站之所以没有被收录，
  - 很有可能是由于互联网上已经存在很多与该网站相同或相似的网站，而且网站的内部结构和内容相似度非常高，这样就会使搜索引擎认为 ，该网站是一个复制网站，没有任何价值可言。
  - 就会拒绝收录，因此这样的新网站就会进入到漫长的沙盒期中。
- 网站在上线之后，搜索引擎通常会在一周之内对网站的首页进行收录，而对网站的内页收录则需要10到20天左右的时间，因为很多内页内容并没有填充
- **影响SEO网站收录时间长短的因素**
- 网站层级
  - 将最重要的内容和热点内容放到首页和栏目页。
  - 搜索引擎在爬到网站中，就会默认放到首页中的链接内容就是网站的核心内容
- 新站考核期
  - 一周收录首页，两周收录内页已经成为一种普遍现象，内页的收录速度非常缓慢
  - 只需要做好网站内容建设和外链拓展，等待新站度过考核期，收录量自然能够提升。
- 网站权重
  - 要想解决网站权重问题提升网站的收录量的话，站长应该每天做好网站的更新工作，多发布一些高质量的外链，
  - 或者交换一些权重较高的友情链接，通过提升网站权重的方式来提升收录速度。
- 敏感词汇检测
  - 第1类敏感词汇是带有极限描述的词语，例如最好
  - 第2类敏感词汇则属于违反广告法的词汇

- ## [百度蜘蛛抓取与网站文件更新时间有关吗？](https://www.zhihu.com/question/266610061/answers/updated)
  - 注意，抓取后不一定被收录
  - 最好的方式是，更新文件后也更新sitemap，爬虫先爬取sitemap，如果没有sitemap在根据链接一个一个的爬。
  - 在网页更新上，建议规律化，定时，定量，定质量，特别是网站内容的质量好坏，直接决定收录！

# ref
- [更改 Googlebot 抓取速度](https://support.google.com/webmasters/answer/48620)
  - 抓取速度是指 Googlebot 在抓取网站时每秒向网站发出的请求次数，例如每秒发出 5 次请求。
    - 可以限制对根级网站（例如 www.example.com 和 http://subdomain.example.com）的抓取速度。
    - 您设置的抓取速度是 Googlebot 的抓取速度上限。请注意，Googlebot 并不一定会达到这一上限。
    - 您无法更改对非根级网站（例如 www.example.com/folder）的抓取速度。
  - 您无法更改 Google 抓取网站的频率，但如果您希望 Google 抓取网站上的新内容或更新后的内容，可以请求重新抓取。
- [google: Ask Google to recrawl your URLs](https://developers.google.com/search/docs/advanced/crawling/ask-google-to-recrawl)
  - Crawling can take anywhere from a few days to a few weeks.
    - Be patient and monitor progress using either the Index Status report or the URL Inspection tool.
  - There is a quota for submitting individual URLs.
  - Requesting a recrawl multiple times for the same URL or sitemap won't get it crawled any faster.
- [2020，百度SEO还能做吗？出路在哪里？](https://www.zhihu.com/question/399804078/answers/updated)
  - 百度seo可以做，但是要更加精细化运营，利用其它渠道不断拓展网站，提高用户粘度
- [百度 SEO 是否已经名存实亡？](https://www.zhihu.com/question/27087922/answers/updated)
  - 随着新媒体时代的到来，人们在百度上花的时间确实慢慢被一些新平台分割掉了
  - 传统的基于关键词的搜索，如今慢慢演变成语音搜索（姑且称之为：VEO）
