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

## utils

- https://github.com/jshemas/openGraphScraper /ts
  - Node.js scraper service for Open Graph Info and More!
  - A simple node module(with TypeScript declarations) for scraping Open Graph and Twitter Card info off a site.
  - doesn't support browser usage
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

- ## 

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
