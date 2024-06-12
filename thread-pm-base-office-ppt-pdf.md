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

- ## 

- ## 

- ## PDF 是一种非常难以解析的格式。 很多人发明了很多方法去解析 PDF。 这些人所花费的时间足以定义一种新的好用的文件标准。
- https://twitter.com/oran_ge/status/1774602216202240029
- pdf 的问题在于把上下文拆成一个个行了，只有每行的二维位置，其他信息都丢失了。
  - 表格更是灾难，Python Java，去处理都有缺陷
- 不是行，是方框，可以是多图层，也可以是任意方向。本质上PDF是带文本标签的组合图片。
- 感觉微信读书团队做得不错，不管是电子书还是扫描版，扔进去似乎都能给解析出来
  - 有些并不是解析的，而是云文件，和网盘功能类似，检测到A书，并不会一页一页帮你解析，而是用云端的A书给你。
- 他主要是 在啥设备 上打开格式都不会错
- pdf的惯性太强了。xps曾经试图挑战pdf，但是pdf还是很难挑战的。
- 我搭了个开源的在线pdf编辑器：http://pdfdrills.com
- PDF 相当于 windows 上的 pe 或 linux 上的 elf 。之所以有很多人试图去解析 pdf 是因为文档没有发布源码的惯例。
- 源自PostScript，本质上是驱动打印或显示设备的脚本语言，是描述性而非结构化的。

- 不知道为什么现在它被滥用在很多根本用不上固定排版的场合作为内容分发了
  - 兼容性啊！微软和金山之间的转档啊，还有mac和windows之间的字体问题啊
- 最初PDF的用途只是为了保证打印效果的一致性。但未考虑到互联网时代的内容结构化需求。事实上应该在网络上代替PDF的格式是HTML，或者Markdown。但是由于HTML的严肃排版功能一直比较拉垮，所以PDF一直没法淘汰。
- Chrome有pdf閱讀器擴展，用html渲染，顯示效果無二，打印出來格式也沒變。技術上替代pdf沒問題。
- PDF设计出来就是不让你修改的。这是根本原因。

- pdf不是编译完产物么，源文件可以看latex

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
# discuss-design-poster
- ## 

- ## 

- ## 

- ## 吉光卡片，这是一款高颜值的文字排版设计 App，提供了丰富的模板以满足各种场景需求，符合我对 iOS 用户的想象。
- https://x.com/austinit/status/1800390337082597519

# discuss
- ## 

- ## 

- ## 

- ## 

- ## 我觉得 https://ia.net/presenter 才是理想的演示文档工具，让你专注思考想要表达的是什么，忘掉样式和排版。
- https://twitter.com/chloerei/status/1785511604978917731
  - 而像 gamma 那样虽然有华丽的排版工具和 AI 辅助，却很容易造出一堆精美的废话演示。

- ## 大家用 AI 阅读长 PDF 的时候, 都会选择用哪家服务呀? 似乎支持 PDF 阅读的服务似乎文件大小都限制在20MB.
- https://twitter.com/hylarucoder/status/1781623406330626154
- Perplexity，它接受无限个数的pdf，并且如果你在一个模型上的上下文累积的很长，你可以切换模型，然后问题又大概率得到解决(可能需要重发一遍文件)。
  - 如果你要一次性处理这么大的文档的话，效果可能没有分页去传若干个小文档好诶。
  - 当然文档大也可能是图片多，那只能自己去压缩画质了，或者切换到本地的什么模型吧
- 主要是想快速检索文档中的一些点方便跳转. 如果是读研究报告的话, 这个还是挺刚需的

- ## what if you could capture frames in a video and then slice them up / re-arrange them?
- https://twitter.com/JungleSilicon/status/1779281315696656785
  - 图片被切成几条的效果

- ## [Powerpoint shapes/diagrams to Draw.io? : powerpoint_202310](https://www.reddit.com/r/powerpoint/comments/16yreii/powerpoint_shapesdiagrams_to_drawio/)
  - I made diagrams family tree in powerpoint and wanted to edit in draw.io and then edit again in powerpoint.

- I don't think you're going to have an easy time of converting PowerPoint shapes to any of the org chart/diagram flow makers. But you can use the above thought process to look through various software import/export options to see if you can find some overlap.

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
