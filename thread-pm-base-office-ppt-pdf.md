---
title: thread-pm-base-office-ppt-pdf
tags: [office, pdf, pm, ppt, presentation, thread]
created: 2021-04-19T14:51:21.033Z
modified: 2024-01-11T15:57:32.182Z
---

# thread-pm-base-office-ppt-pdf

# guide

- ppt的技术方向侧重图形编辑器，依赖计算机图形学

- ppt的方向不要投入过多精力，很多大厂意识到ppt经常浪费资源，逐渐转向word

- products
  - design-to-code
  - code-to-design
# discuss-stars
- ## 

- ## 

- ## 
# discuss-pdf
- ## 

- ## 我想要写一个 HTML 转图片/PDF 的微服务，底层是 chrome，开源。是否已经有同类项目？
- https://twitter.com/chloerei/status/1724724703317934102
  - 我可能没说清楚背景，我有个应用已经在用chrome生成图片了，但是把 chrome 打包进主应用里让镜像大了几百M，我想把调用chrome API这个部分独立成服务。
  - 类似的项目有 vercel/og。类似的服务有 htmlcsstoimage。

- ## 很多人都在问简单简历 http://easycv.cn 下载的 PDF 文件为什么效果那么好？
- https://twitter.com/vikingmute/status/1711188708316336252
- 如果你使用的 React 技术栈，使用 React PDF 肯定是没错的，可以直接使用各种 css 属性，同时完美实现渲染/下载等功能
  - 甚至还可以配合 React PDF Tailwind，使用 Tailwind.css 来写 PDF 的模版，这个是基于 React PDF 的。
  - 通过这两个，就可以实现比较完美的 PDF 样式展示和布局了。

- 我会用jspdf去构建一两页的PDF
# discuss
- ## 

- ## 

- ## 

- ## 

- ## 

- ## we want to build a layout, so we have a designer mock it up in Figma, using the box model.
- https://twitter.com/steveruizok/status/1596886646066393088
  - then, we ask an engineer to implement the spec, done by hand, again using the box model.
  - this handoff process usually takes days/weeks. yet in theory doesn’t need to exist
- steveruizok
  - First, Figma acquired the very talented Visly team a few years ago, I imagine they’ve been working on something in design to code handoff.
  - My worry would be that creating a better handoff product would make Figma a worse design product
  - Even scoped only to layouts, production layouts often contain much more information than designs. That’s okay—it’s too much to expect a design to anticipate every edge case in a responsive layout, locale and accessibility setting combinations, etc
  - The outcome is that the design will never be a source of truth for a production application unless it is the only source of truth; ie an app like framer or webflow, where the app anticipates this in every feature
  - Those sites solve a very different problem than “engineers have to rebuild designs in code”
  - 👉🏻 because code export problem is imo not an actual problem. Rebuilding layouts from figma in html/css is an extremely minor and entirely acceptable redundancy in the product pipeline; pulling in generated code would create more problems than it would solve
