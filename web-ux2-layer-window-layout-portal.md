---
title: web-ux2-layer-window-layout-portal
tags: [components, portal, ui, window-layout]
created: 2021-01-13T17:13:36.979Z
modified: 2021-07-29T20:39:09.187Z
---

# web-ux2-layer-window-layout-portal

# guide

# faq

## 如何将多个传统网站页面集成合并，组成一个portal门户目录，且冲突尽可能少

- 暂时没找到直接的方法，因为原本各网站的文字链接、资源url地址都会变化
- 可考虑重新开发

- ref
  - [Multiple web applications into one portal](https://stackoverflow.com/questions/8100098/multiple-web-applications-into-one-portal)
# discuss
- ## 50% of my job is reminding designers that they can't have tooltips on elements that aren't focusable. Stop it!
- https://twitter.com/devongovett/status/1430234270375636993
  - Usually it's random text (e.g. truncation), or icons. Disabled buttons are also a very common one.
- In the case of truncation, I imagine it’s similar to what Safari does natively? Is there a proper way to mimic that and retain accessibility?
  - That's the reason why I have an abstracted out Actionable utility in Arcade as well. Disabled buttons tooltips are not my favourite but we had a discussion
  - We're working on this instead: 添加一个添加的类似i的提示图标，鼠标不能聚焦到不可用button，但可以聚焦到不可用button旁边的i型icon
- I may regret asking this, but why can you not have a tooltip on a non-focusable element?
  - So that users that navigate using a keyboard can access it
  - Some users use a keyboard but not a screen reader, and the target needs to be focusable for them to access the tooltip.
# more
