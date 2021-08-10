---
title: dev-log-faq-web-css
tags: [css, dev, faq, web]
created: '2021-08-07T17:23:42.370Z'
modified: '2021-08-07T17:24:01.266Z'
---

# dev-log-faq-web-css

# faq-not-yet

- scss/less/css源码中要不要放图片
  - 如何处理相对路径和绝对路径
  - 对于自动生成唯一类名的css框架，后续修改图片就不方便
  - 对于app中的图片，一般都是动态修改或切换的，所以放在应用代码中导入灵活性更高

- 如何实现圆环性能更好
  - A1: 使用outline
  - A2: 使用box-shadow
  - À3: 使用:before伪元素
  - A4: 使用2个div
  - 思路
    - 尽量选择单元素的实现，多元素会有创建成本、同时对以后的动画、事件冒泡处理也有影响
    - outline不支持类似border的四边分别设置；浏览器的键盘导航事件会自动触发显示隐藏
# faq
