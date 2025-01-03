---
title: pattern-sharing-open-graph-images
tags: [open-graph, sharing]
created: 2023-02-03T05:54:50.511Z
modified: 2023-02-03T05:55:22.102Z
---

# pattern-sharing-open-graph-images

# guide

- [The Open Graph protocol](https://ogp.me/)

- minimap可作为一种参考
  - [Content minimap - CKEditor 5 Documentation](https://ckeditor.com/docs/ckeditor5/latest/features/minimap.html)
# examples
- https://github.com/jacktuck/unfurl
  - Metadata scraper with support for oEmbed, Twitter Cards and Open Graph Protocol for Node.js
  - take a url and some options, fetch the url, extract the metadata we care about and format the result in a sane way.
  - It supports all major metadata providers and expanding it to work for any others should be trivial.

- https://github.com/itteco/iframely /js
  - https://iframely.com/
  - oEmbed proxy. Supports over 1800 domains via custom parsers, oEmbed, Twitter Cards and Open Graph
  - This is the self-hosted version of Iframely's APIs and HTML parsers.
  - Iframely takes your URL and returns its metadata. If supported on the URL, we'll add HTML of rich media embeds.
  - This package includes specific domain parsers for most popular publishers. 

- https://github.com/fabian-hiller/og-img /MPLv2/202401/ts
  - Generate dynamic Open Graph images for your website
  - This is a framework agnostic package for generating Open Graph images using `Satori` and `resvg`. 
  - Built using Web APIs, this package can be executed with Node.js and on the edge. 
  - The difference to `@vercel/og` is that this package loads the WebAssembly module needed to convert SVG to PNG lazily at runtime and provides a framework agnostic workaround for defining the content of the image using `satori-html`.

## utils

- https://github.com/jshemas/openGraphScraper /MIT/202310/ts
  - Node.js scraper service for Open Graph Info and More
  - A simple node module(with TypeScript declarations) for scraping Open Graph and Twitter Card info off a site.
  - doesn't support browser usage

- https://github.com/microlinkhq/browserless /js
  - interact with a headless browser built in top of puppeteer.

- https://github.com/weijunext/ogimage-click /MIT/202501/ts
  - https://ogimage.click/
  - Create beautiful OG images, Twitter/X Header Images & more for free, in simple clicks.
  - https://github.com/FadyMak/imgsrc-app
# blogs

## [A framework for building Open Graph images | The GitHub Blog_202106](https://github.blog/2021-06-22-framework-building-open-graph-images/)

- We recently set about creating a framework and service for automatically generating social sharing images for repositories and other resources on GitHub.
- Open Graph is a set of standards for websites to be able to declare metadata that other platforms can pick out, to get a TL; DR of the page.
- In addition to the image, we also define a number of other meta tags that are used for rendering information outside of GitHub, like `og:title` and `og:description`.
- When a crawler (like Twitter’s crawling bot, which activates any time you share a link on Twitter) looks at your page, it’ll see those meta tags and grab the image. Then, when that platform shows a preview of your website, it’ll use the information it found. Twitter is one example, but virtually all social platforms use Open Graph to unfurl rich previews for links.

- How does the image generator work?
  - our custom Open Graph image service is a little Node.js app that uses the GitHub GraphQL API to collect data, generates some HTML from a template, and pipes it to Puppeteer to “take a screenshot” of that HTML. 
  - This is not a novel idea—lots of companies and projects (like vercel/og-image) use a similar process to generate an image.
  - When our application receives a request that matches one of those routes, we use the GitHub GraphQL API to collect some data based on the route parameters and generate an image

- Generating an image takes 280ms on average. 
  - We could go even lower if we wanted to make some other changes, like generating a JPEG instead of a PNG.
  - The image generator service generates around two million unique-ish images per day. 
  - We also return a cached image for 40% of the total requests.
# discuss
- ## 

- ## 

- ## 开源的 OG Image 生成器的项目，添加了不少 SEO 内容，上线第二天就获得了谷歌搜索流量
- https://x.com/weijunext/status/1875005086549836040
  - [Free OG Image Generator](https://ogimage.click/)

- ## 如果你不知道 Open Graph Image 怎么设计可以去 OGImage Gallery 找找灵感，这边收集了上千个网站的 OGImage
- https://x.com/ccbikai/status/1810106528088674673

- ## 昨天上线的自动生成 og image 功能使用了这个项目。
- https://twitter.com/chloerei/status/1730854404461568313
  - 通过把 chromium 依赖独立成一个服务，现在主应用不需要为了应对启动 chromium 预留很多内存。
  - 把这个服务单独部署，还可以使用 fly 平台的自动休眠功能，闲时省钱了。
  - https://github.com/chloerei/htmlrenderer /ruby

- ## 在做软件的时候，经常遇到下面的需求：
- https://twitter.com/beihuo/status/1727839272454262844
  - 给一个链接，返回 preview。类似 notion 的 link bookmark
  - 给一个链接，返回干净的文章全文
  - 现在我能找到的服务，价格都非常贵。但是这个看起来也不难啊。

- 很多 corner case 比较难处理吧，这一看感觉是那种做到 80分很容易，但是做到99分甚至95分，就不那么容易的需求，千奇百怪的各类页面结构，不标准的网页代码，各种视频，图片，音频，Canvas 什么的
  - 感慨大部分需求总是越讨论越复杂的，所以以我多年的交付经验而言，最好的完美解决方案只有一个，那就是：怼回去。实在不行，不管是美人计帅哥计美食计攻心计，搞定客户，然后温柔的怼回去
- 真的不难吗？感觉第一个要*做好*就已经非常复杂了，preview 到底什么时候截取呢？observer 观察 dom 没有变化为止？经过一定时间？什么分辨率渲染？未登录跳转？cookie 弹窗？广告？这个列表可以非常非常长。
  - 至于第二个，由于页面排版的不可确定性，首先什么是“干净全文”就值得商榷

- [开一个 thread 记录一下可能的方案](https://twitter.com/beihuo/status/1727926571082875382)
- 最靠谱的方式就是在 Serverless 服务上跑一个 Headless Chrome。
  - Cloudflare 支持 Browser Rendering。Cloudflare 稍微便宜一些。而且我记得 Cloudflare 没有 egress fee。
  - AWS Lambda 灵活性更好。因为 Cloudflare 目前绑定在 NodeJS 和 puppeteer。

- ## 折腾了一下终于把外链预览图做到鼠标悬浮了
- https://twitter.com/thecalicastle/status/1656456586922164224
  - 前端组件思路很简单，主要就是搭建了一个后端 API 服务，专门用 Playwright + Chromium 可以生成截图，然后缓存起来
  - 左 PeekabooLink 组件，右 link-preview API 路由用 @shuding_ 的 Satori 渲染 img
- 有过同样的想法，但是考虑到 Chromium 可能过重，所以用了 OG 实现的
  - 一开始我的思路也是这样，后来还是想尝试截图法，其实考虑了一下，每个网址不一定都有 og image，但起码能有截图
- 截图兼容性确实高。原来有专门的服务做缓存，我还以为冷启动能做到这么快🤯

- 还有发现另一个相关的小设计，quick links 将页面的所有链接整合以方便进行快速浏览

- ## just built a link preview component using @radix_ui and puppeteer.
- https://twitter.com/anas_araid/status/1610963312761622528
- does puppeteer render the website server side? how expensive is it? (as in: how well does it scale?) 
  - yes it can be used to render web pages on the server side. 
  - I’m not exactly sure how expensive it is, but it just uses the resources of the machine it's running on. 
  - btw on my github you can find the code (it's not perfect, but it might give you some ideas)

- ## Paste tweet link, hit return
- https://twitter.com/graeme_fulton/status/1625814615295680512
  - it needs a few tweaks since some websites like medium block the node-fetch from reading the open graph data. Can be done with puppeteer instead

- ## You can now generate dynamic open graph images for your website with Google Sheets
- https://twitter.com/labnol/status/1488151835781505026?lang=en
  - @github and @vercel have their own open graph image generators that use Google's Puppeteer library
  - I am using Google Sheets as the frontend and the Google Slides API to create unique images for every page title. The generated images are stored in Google Drive. No puppeteer or programming knowledge is required.

- ## Every repo, issue, commit, etc will get a generated card like it.
- https://twitter.com/JasonEtco/status/1380194813140725761
  - And an even more special card for issues, PRs or commits!
- This is sweet. Visual + text is a great way to help people engage and not miss important information.
- I believe we'll be doing a larger blog post about it soon, but we use Puppeteer to generate a screenshot from some HTML.
  - Just out of curiosity: wouldn't something like a Canvas with html2canvas for Example be faster or more efficient Memory wise? Nice Idea btw! Love it!
- I did an open-source server for doing that exact thing some time ago
  - https://github.com/micheleriva/gauguin
  - High performances Golang server for generating open graph images dynamically. 
- I just had a look at how the @vercel team did it in their OG img generator and it’s also Puppeteer and headless chromium
  - https://github.com/vercel/og-image
