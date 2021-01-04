---
title: web-latest-outdating
tags: [frontend, latest, outdating, web]
created: '2020-12-23T16:17:06.241Z'
modified: '2020-12-23T16:19:25.169Z'
---

# web-latest-outdating

# outdating

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
