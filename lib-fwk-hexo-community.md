---
title: lib-fwk-hexo-community
tags: [community, hexo, static-site-generator]
created: 2024-02-09T10:54:19.061Z
modified: 2024-02-09T10:54:44.509Z
---

# lib-fwk-hexo-community

# guide

# discuss-stars
- ## 

- ## 

- ## 

- ## I am looking for a broken link checker tool that I can run against localhost.
- https://twitter.com/alexandereardon/status/1758252484165025931
  - For clarity: the markdown is being used to generate a website, and that website is currently running on my localhost
  - I started writing my own using puppeteer - but I keep thinking that surely one already exists

- since a lot renderers use remark / mdast under the hood i was going to suggest remark-validate-links
# discuss
- ## 

- ## [Hexo的原理是什么？ - 知乎](https://www.zhihu.com/question/51588481)
- 每次运行 hexo g 命令，hexo(node.js程序)会遍历你的 source 目录，建立索引，根据你 theme 文件夹的主题生成页面到 public 文件夹。这时 public 文件夹就是一个纯由 html javascript css 等内容制作的博客

- ## 🚀 [Hexo – A fast, simple and powerful blog framework | Hacker News _201305](https://news.ycombinator.com/item?id=5766352)
- 🆚️ It would be nice to see some benchmarks, comparing with WordPress and others blogging platforms.
  - There is no need for benchmarks, because presenting static files will always be faster than dynamic web apps like WordPress.
  - Hexo (and Jekyll, Pelican, etc) pre-compile from Markdown to HTML which then gets served up as a static resource from the web server. 
  - On the other hand with Wordpress, the server has to compile the HTML every time a user visits.
  - For the server, HTML is just another static resource to transmit. You might as well ask to see benchmarks between displaying an image vs WordPress blog.
  - This can be mitigated with caching, but static resources are easier to cache and the caching logic is now handled by the app rather than CDNs.

- If you have compiled it to HTML, wouldn't it be more efficient to serve it up as static HTML files via nginx (or any web server). Why store the HTML in redis and serve off it via an application?
  - With aggressive disk caching on servers static files are probably near enough in-memory anyhow (+ I'm sure you could configure a modern web server application to cache anyhow), so yeah it's probably pretty fast.
  - However it's more limiting to simply serve static files - you're limited to what you've generated. With redis you can serve it as json data and use it dynamically for e.g. search or showing all articles with a given tag, in a given date range, etc.
  - Additionally, I'm not a big fan of a whole bunch of static files sat in a folder somewhere that needs to be regenerated every time I change something. Personal preference, perhaps
