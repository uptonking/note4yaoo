---
title: note-office-dev
tags: [dev, office]
created: 2019-07-08T04:55:46.940Z
modified: 2020-07-14T10:32:07.321Z
---

# note-office-dev

# tips

- excel阅读器/编辑器可以自己动手实现，基本数据格式比较固定
- pdf阅读器/编辑器可参考已有解决方案
# blogs-office
- [在线 Office 解决方案调研总结 - 知乎](https://zhuanlan.zhihu.com/p/558547446)
  - window.location.href = 'ms-word:ofe|u|file:///Users/xxx/xxx/file.docx'; 

- [Onlyoffice 二次开发指南 - 知乎](https://zhuanlan.zhihu.com/p/558565903)
- [5 分钟上手 Onlyoffice 插件开发 - 知乎](https://zhuanlan.zhihu.com/p/558568422)
# discuss
- ## 

- ## 

- ## 

- ## [OnlyOffice is an alternative to LibreOffice | Hacker News_202009](https://news.ycombinator.com/item?id=24385532)
- One deal breaker for me regarding OnlyOffice is that they have absolutely no support for RTL
- The problem with OnlyOffice is non-community-oriented development and the predatory licensing model where they hold all copyrights and dual-license their code AGPL+proprietary, while forbidding others do the same (since they hold the copyrights), therefore putting themselves at the centre of their universe.
  - For OnlyOffice, the open source license is just a marketing trick and a source of occasional free patches.
- ONLYOFFICE can also do collaborative online editing, and sharing, for free (and it's also open source!

- ## [Bring back mobile editing for the community edition or at least a cheaper license for this · ONLYOFFICE/DocumentServer_202003](https://github.com/ONLYOFFICE/DocumentServer/issues/805)
  - Mobile editors available only for paid version

- ## I'm super done with SSG and think it's bad for most (maybe all?) use cases.
- https://twitter.com/tannerlinsley/status/1344356848397209602
- A silly amount of work has been put in place to make SSG attempt to do what the HTTP caching specification has had for decades (reduce unnecessary server load).
  - Everyone's making trade-offs without knowing about the standards-based alternative implemented by CDNs.
- This is the same conclusion I came to when I left my React Static library a few years ago. 
  - Once you’re in the trenches and see the weird things SSGs are doing to compete and scale, you can either choose to dig your heels in and get weirder or stop and embrace web standards.
- Yeah I’m not that one sided right. 
  - My marketing site is mostly static and it’s great. 
  - But there’s definitely dynamic parts to it that would never work for static and probably not forever as content grows. Time and place I guess. 
  - Hybrid is awesome, so I use Next.js
- I think (SSGs)they're a nice solution if the amount of content isn't too large, deploying without managing a server is nice.
  - One issue is how slow Node is, if Node SSGs were 150X faster that'd make build times much more bearable. 

    - That's the diff between Hugo and node SSGs.

  - Isn't the diff due to building an SPA instead of standalone pages? They are not building the same kind of app imho
- I just implemented a docs/reference/blog site with nextjs (~120 pages atm) and that resulted in 15 SSG routes, 2 SSR routes (search api and page) and another api route for puppeteer share previews. 
  - For a lot of "content" sites I find that hybrid approach very nice.
  - If I were to implement a shop, a news site (content not in repository). 

    - I‘d go for caching too. 
    - But my main work is in authenticated contexts where content can’t be cached (on a CDN) 
    - and I make heavy use of client side rendering with local cache. So I’m at the extremes.

- I see so many people in the community falling for the idea that SSG is *only* about perf. 
  - Looking at enterprise usage it’s often for other reasons like exposing errors at build time (instead of to users), security (less node js) and lower compute. 
  - As always ‘it depends’
  - I’ve never worked on a SSG project - but I do like to address dogmatic views on the internet. 
  - The idea that proponents of SSG (especially at scale) simply ‘didn’t know about http headers’ is ludicrous.
- SSG does have a few valid use-cases. Examples: 
  - Small personal sites for devs.
  - Ecommerce stores, with not-thousands-of-products.
  - Prerequisites for using SSG:

    - Big chunks of the content changes rarely (1000s of views per change in content)
    - A market, where load times are highly critical (10s of ms matters)

  - Especially many ecommerce sites have this dynamic. 

    - Pages viewed per purchase are high, descriptions change rarely, and dynamic stuff like inventory needs to be near-real-time, so it makes sense to load them with JS.
