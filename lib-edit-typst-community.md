---
title: lib-edit-typst-community
tags: [community, latex, typesetting, typst]
created: 2025-12-25T19:54:34.540Z
modified: 2025-12-25T19:54:56.482Z
---

# lib-edit-typst-community

# guide

# discuss-stars
- ## 

- ## 

- ## 
# discuss-layout
- ## 

- ## 

- ## 

- ## 

- ## [Text adapting to image : r/typst _202604](https://www.reddit.com/r/typst/comments/1s9uuy1/text_adapting_to_image/)
  - can pretext be done in typst ?
  - is the html experimental capable of doing this kind of animation for webpages?

- No that's not possible for the html output you'll have to process the compiled result you get from typst to adjust layout.
  - Animations are especially not within scope of what typst provides for html output (structured, rich text content)

- as the other fellow said, animation is not the main go of typst. But if you want a static non animated version of this, another post here in this subreddit had text adapting to image.
# discuss-spec/format
- ## 

- ## 

- ## 

- ## 🆚 [记录从obsidian迁移到typst的尝试 _202512](https://linux.do/t/topic/1370697)
- 近几年使用md遇到的痛点
  - 排版能力过弱, md只适合纯文本为主的日常随笔记录, 而难以应对绘图等要求
  - 一旦涉及嵌套callout或图表等富文本信息简直就是格式灾难
  - 自定义需要修改全局css, 不具备项目级个性化需求
  - 不具备可复现性, 一旦过多依赖插件, 可能由于ob版本更新而失效
- 尝试把工作流迁移到typst, 追求兼顾效率与排版
- 优点
  - 基本与md同等代码量即可实现灵活的图表绘制, 页面布局与自动化
  - 楼主本身就习惯源代码模式编辑, typst语法简洁直观, 无需增加心智负担
  - 可以锁定依赖版本, 且易于导出pdf
- 缺点
  - 抛弃ob的双链, 但是可以依靠手动打label替代实现更灵活的块链接
  - vscode预览无法跳转Kink, 目前利用自动化导出pdf并链接到zotero实现Link悬停浏览
  - 没有dataview归纳分类笔记

# discuss-issues
- ## 

- ## 

- ## 

- ## 
# discuss-parser/generator
- ## 

- ## 

- ## 

- ## 
# discuss-internals
- ## 

- ## 

- ## 

- ## 
# discuss-tips
- ## 

- ## 

- ## 

- ## [How do I set the page width based on amount of characters? : r/typst](https://www.reddit.com/r/typst/comments/1q13vsi/how_do_i_set_the_page_width_based_on_amount_of/)
- Note that it is important to set the font and size before the show rule for context to catch the change

# discuss
- ## 

- ## 

- ## 

- ## [Typst has ruined me : r/typst](https://www.reddit.com/r/typst/comments/1r00v8d/typst_has_ruined_me/)
  - tl; dr: typst is so empowering and it started a domino effect where i now obsess over every typographical detail and even in my daily life i couldn't stop myself from thinking "heh i bet i could remake this form/signage/poster/presentation/document in typst and make it better"

- I feel very similar. I hope you will never hear about Practical Typography by M. Butterick, because that combined with Typst will drive obsession into insanity. Me, I am done for.

- Typst is actually user friendly and I've used for all kind of cool stuff. Like making templates for Zebra printers, converting them to png and printing labels, instead of using dreadful zpl. Or actually making document templates myself. The support for csv/json and other input variables is crazy. My only dream that it had better python support to use as a library in the way.
  - I agree. For me, it feels like even though Typst is technically less capable in some aspects, at least it lets you do things more easily, as if welcoming you to be a power user

- I keep all tables as csv files, and can use the design document to generate cost estimates, timeliness, etc, which gets me 80% there already. Everyone else uses Google Docs and I can do same but faster and better in Typst. Documentation used to be a chore but now it's actually enjoyable.

- Reminds me of another reason why I find Typst so fun: the syntax. As someone with experience in Python and MATLAB, Typst's syntax lets me think programmatically, which again empowers me to do more automation and weird complex stuff I never would have done with LaTeX without hitting my head at a wall or copying stuff from the stack exchange (yeah i later realized that macros in latex are a thing but it seemed complicated at the time)

- typst is too simple syntactically and too usable as a plain markup format. When in the past I'd reach for plain markdown or, heaven forbid, libreoffice, for some notes, now my general instinct is doing it in typst because I can just suddenly also plot functions inline, draw graphics far better than i could do by hand and inputting formulas and regular text is just too easy.
  - Typst has managed to bridge the gap between "proper" document layout and just quickly writing something down for me and it is amazing.

- Just came to say this: mitex filter enables LaTeX syntax for equations, AND quarto lets you render from its markdown+programming chunks to word/typst/LaTeX/html and presentation formats via pandoc. You can get your formatting template in typst, and your text written in markdown
