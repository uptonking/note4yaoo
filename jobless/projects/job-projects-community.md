---
title: job-projects-community
tags: [community, job, projects]
created: '2021-10-01T06:42:53.998Z'
modified: '2021-10-01T06:43:28.839Z'
---

# job-projects-community

# faq

# 如何实现高亮当前标题
- 目录跳转到文章，用锚点

- 高亮的原则是当前标题所在的位置到浏览器可视区域顶部的距离需要小于或等于一个固定值
  - arContentAnchor[index].getBoundingClientRect().top <= VAL
  - 当遍历 arContentAnchor 这个列表，某项的位置小于固定值，且差值最小的时候，该项对应的目录就应该被设置为高亮

- 思路1
  - 谁离顶部近就高亮谁
  - idElement.getBoundingClientRect().top <= offsetTop
- 思路2
  - 监听浏览器的滚动距离
  - 计算每个标题距~~浏览器~~顶部的高度 offsetTop
  - 匹配滚动距离在两标题之间的距离实现目录自动跳转
  - 优点：简单，在页面尾部有额外元素撑场面的时候效果好，或者最后一个元素本身就有一屏幕高的时候效果好
  - 缺点：在没有额外元素撑场面时, 底部元素 a5 无法高亮

- 思路3: 对于必会经过的，可以考虑 mouseover/out
- 思路4: IntersectionObserver

- ref
  - [详细设计一个文章页的目录插件](https://juejin.cn/post/6883292908649185288)
  - [手摸手带大家写一个锚点高亮点代码](https://juejin.cn/post/6844904008327364615)
# 如何设计一个红包雨系统？
- https://www.zhihu.com/question/394945080/answer/2093140110
