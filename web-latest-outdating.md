---
title: web-latest-outdating
tags: [frontend, latest, outdating, web]
created: 2020-12-23T16:17:06.241Z
modified: 2020-12-23T16:19:25.169Z
---

# web-latest-outdating

# relicensing

- elasticsearch

- mapbox-gl-js
  - [Our Thoughts as MapboxGL JS v2.0 Goes Proprietary_202012](https://carto.com/blog/our-thoughts-as-mapboxgl-js-2-goes-proprietary/)

- more-relicense
  - sugar, redis, mongodb,sugar-crm
# outdating

## outdating-projects

- meteor

## [前端哪些技术优化方案已经过时了？](https://www.zhihu.com/question/385397882/answers/updated)

- activex，flash，sliverlight
  - 随着js逐渐强大，一些嵌入网页的第三方脚本方案逐渐废弃
- 语义化
  - 语义化，在当今基于组件化的开发方式来说，诉求不算太强烈
  - 得顾及跨平台的开发，面对的不只是html tag，谁还有心思纠结这种有的没的规范
  - 要考虑a11y
- jsonp
  - cors够用
- 雪碧图
  - 通过background-position和合并图片来实现减少请求的方案，
  - 但由于http2/3，和icon fonts的方案普及，和css3，ui扁平化，和前端工程化的到来，雪碧图几乎没有什么使用场合了。
- ie css expression/filter

## [Is Meteor.js dead?_201804](https://news.ycombinator.com/item?id=16782266)

- I started using Meteor in 2014. 
  - I was active for two years, posting frequently on their forums, writing packages, building MVPs, etc. 
  - As I started building more things with Meteor, I realized that it doesn't scale well. 
  - It's great for proof-of-concept work. 
  - Frameworks can be incredibly productive for low-scale work, but they are painful to scale. 
- No framework that can be simultaneously optimized for every use-case. 
  - Now, I always DIY with a router like Express.
- Meteor's problems were rooted in its real-time protocol, DDP, which had some problems. 
  - Firstly, everything is real-time by default. 
    - It's better to minimize the amount of real-time components in your application as there are very few things that need to be real-time. 
  - Secondly, the pub-sub caching mechanism made it infeasible for situations with many concurrent users. 
    - I was able to get around this by proxying some of their internal functions.

- 
