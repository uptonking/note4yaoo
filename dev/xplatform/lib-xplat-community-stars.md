---
title: lib-xplat-community-stars
tags: [cross-platform]
created: 2021-05-13T07:47:16.621Z
modified: 2021-05-13T07:47:39.619Z
---

# lib-xplat-community-stars

# guide

# discuss
- ## 

- ## 

- ## 终究都离不开我们内部一个文档的结论：一行代码都不动跨平台只是一个幻想，想要性能就必须分别写，用软件工程的手法来最大程度共享代码
- https://x.com/geniusvczh/status/1906670044605821355
- 微软折腾过这多框架api最有发言权，特么这么多年换了多少框架了，直接没开发者了

- ## OMT (off-main-thread) architecture, despite Chrome DevRels' advocacy since '19, has not become mainstream for web dev at all - no major JS frameworks appear to even explore it these days 
- https://twitter.com/Huxpro/status/1752754590305681415
  - But surprisingly, it almost dominated the Chinese frontend market 
  - It all started with WeChat mini-programs adopting OMT, mainly to sandbox third-party code while avoiding blocking its own UI thread. This soon got replicated by every Chinese tech giant for its security or perf benefit. Today, almost every Chinese frontend dev needs to know it
  - To clarify, the adoption of OMT by Chinese tech wasn't limited to their mini-program counterparts. They also adopted it in their first-party cross-platform solutions, akin to RN or SDUI. 
  - This represented an interesting alternative to how RN Fabrics approached multi-threading.
- If I remember correctly, Angular had an out-of-the-box Webworker render solution even during its 2.0 Beta stage.
- Interesting perspective! But "major JS frameworks" are not designed to sandbox your code in another in-house jail
