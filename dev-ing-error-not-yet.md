---
title: dev-ing-error-not-yet
tags: [dev, error, not-yet]
created: '2021-03-29T18:54:26.760Z'
modified: '2021-03-29T19:29:15.528Z'
---

# dev-ing-error-not-yet

# pieces

- ## 浏览器窗口占半屏时，直接跳转到@pgd/css docs文档页的url，若url尾部含有锚点如#button，则右边文档内容会被左边fixed的目录挡住，显得凌乱
  - 点击目录文字跳转时也会出现此问题
  - 出现此问题时，若先最大化窗口再半屏化窗口，则问题消失，正常显示
