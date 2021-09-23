---
title: ux-usecase-stars
tags: [usecase, ux]
created: '2020-07-17T13:58:14.640Z'
modified: '2021-04-19T18:10:10.394Z'
---

# ux-usecase-stars

# comment 社交评论组件

- 限制缩进，只支持一级评论
  - twitter: 所有评论项均可以作为一条tweet查看

- 限制缩进，最多支持两级评论
  - facebook: 所有、最新、热评
    - 对于二级评论，会在每条评论前显示回复的用户名
    - 评论和子评论都采用懒加载的方式，需要一直点查看更多
  - github
    - issues只支持一级评论，discussion支持两级评论
  - 知乎、微博
    - 默认排序、最新排序；每条二级评论支持查看完整上下文

- 使用无限缩进
  - reddit
  - hacker news
# landing page for 以UGC内容分享为中心的应用
- 主要使用卡片
  - dev.to: 背景灰、卡片白
  - quora: 首页推荐的每个回答都以卡片的形式展示
  - facebook: 背景灰、白色圆角卡片且无边框
  - 微博: 皮肤背景、白色直角卡片
  - linkedin: 灰底白卡片

- 主要使用列表
  - reddit: data intensive 数据密集的列表
  - hacker news: 列表形式，但全是文字，没有分隔线
  - stackoverflow: 只显示问题标题，无描述摘要，高亮讨论多的问题项的背景，高亮导致眼花
  - hashnode: 列表每项元素过多，ux显得凌乱，灰背景白内容块
  - substack
  - tableau public: 无分隔线，图片占一大半
  - 知乎: 首页每项内容前后都有水平横线作为分隔符
  - twitter: 首页每项内容高度可以不同，符合社交应用相互回复的需求
    - 若内容中含有图片或内容引用，则以圆角卡片形式展示
  - 今日头条: 强调有吸引力的新闻标题，几乎没摘要文字，有图片
  - more
    - 语雀讨论区
    - infoq
    - csdn
    - cnblogs
    - 天涯社区

- 主要使用网格/多行多列 grid/masonry
  - observable: 多行多列展示图表和标题
  - medium: 首屏以标题+图片为主，很少使用水平横线分隔
  - instagram: 以图片展示为主
  - pinterest: 以图片展示为主
