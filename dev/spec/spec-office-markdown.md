---
title: spec-office-markdown
tags: [format, markdown]
created: 2019-12-24T11:23:55.280Z
modified: 2021-09-30T07:43:25.286Z
---

# spec-office-markdown

# guide

- 关于组件与文档设计
  - 复用文本过于灵活，需要各种解析器
  - 复用js函数则设计更清晰、复用更简单(特别是纯函数)
# spec
- markdown
  - https://daringfireball.net/projects/markdown/
- GitHub Flavored Markdown Spec
  - https://github.github.com/gfm/
  - https://guides.github.com/features/mastering-markdown/
  - [Basic writing and formatting syntax](https://docs.github.com/en/get-started/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax)
- ReadMe-flavored markdown 
  - https://rdmd.readme.io/docs/syntax-extensions
  - Code Tabs, Callouts, @embed
# [mdx](https://mdxjs.com/getting-started/)
- ref
  - I'm not an expert in JSX or MDX, but looking at the code example I would think MDX could also handle Web Components.
  - mdx可作为csf的完全替代，但mdx中需要显式import Story/Canvas/Meta

- MDX is an authorable format that lets you seamlessly write JSX in your Markdown documents.
- MDX syntax can be boiled down to being JSX in Markdown. 
- It’s a superset of Markdown syntax that also supports importing, exporting, and JSX.
- Markdown is good for content. 
- JSX is good for components.
  - It makes repeating things more clear and allows for separation of concerns. 
  - MDX fully supports JSX syntax. Any line that start with the < character starts a JSX block.
# [mdjs](https://rocket.modern-web.dev/docs/markdown-javascript/overview/)
- ref
  - https://open-wc.org/docs/experimental/mdjs/

- Markdown JavaScript (Mdjs) is a format that allows you to use JavaScript with Markdown, to create interactive demos. 
- It does so by "annotating" JavaScript that should be executed in Markdown.
  - To annotate we use a code block with `js script`.
- One very good use case for that can be web components. 
  - HTML already works in markdown so all you need is to load a web components definition file.
- mdjs comes with some additional helpers you can choose to import
  - mdjs-story.js
  - mdjs-preview.js
- Supported Systems
  - es-dev-server
  - storybook-addon-markdown-docs uses mdjs under the hood.
# office-2003
- [office复合文档数据结构解析“初探” OLE](https://blog.csdn.net/Cody_Ren/article/details/103886098)
- [复合文档的二进制存储格式研究[ole存储结构](word, xls, ppt...)[转] - 极简 - 博客园](https://www.cnblogs.com/AspDotNetMVC/p/3810839.html)
# spec-related
- rst
- asciidoc
- [Org Mode](https://orgmode.org/)
  - Org mode is for keeping notes, maintaining to-do lists, planning projects, authoring documents, computational notebooks, literate programming and more — in a fast and effective plain text system.
# faq
- mdx和react-live实现组件文档在线编辑时，为什么组件预览有时会消失
  - 由于 `@mdx/js-loader` 解析的限制，两行export const之间必须有空行
- markdown-comment-below-is-not-displayed (4 patterns)

[//]: # (This may be the most platform independent comment)

[//]: <> (This is also a comment.)

[comment]: <> (This is a comment, it will not be included)  

<!---
your comment goes here
and here
-->

# guide
- features
  - mdx based doc, 简单读写无需借助专业软件

- tips
  - search: markdown extensions, plugins, specification

- mdx pros
  - 支持markdown+jsx
  - 支持直接引入a.mdx作为一个组件
  - 支持定义和导出variable
- mdx cons
  - code block的语法高亮不可更改样式
  - 不支持live editor

- md插件设计
  - 列表类
  - 图表类
  - 地图类
  - 搜索类
  - 功能类
    - comment评论
    - task board
      - 任务默认添加到一个card，还能手动移动到另一个card
- GFM(GitHub Flavored Markdown)
  - syntax highlighting
  - task list
  - table
  - emoji
  - automatic linking for url
  - username mention
  - issue reference
  - SHA references
- MDX
  - parser-runtime
    - mdx
    - htmdx
  - live code editor
    - react-live在线编辑器组件可同时解决在线编辑与语法高亮的问题
    - 源码工具条：折叠展开、复制
  - table of contents
    - 目标
      - 针对一系列文档，而不是单篇文章
    - 目录的设计方案
      - 在侧边，默认只显示一级标题及折叠符号，展开才可查看二级标题
        - 文章目录放在同一侧边，放在最下层标题之下，通过竖虚线提示
        - 优点是无需滚动侧边栏就可查看全部一级标题
        - 缺点是频繁折叠展开
        - 折叠符号可以放在每行开头，也可以放在每行末尾
      - 在侧边，各级标题目录全部展开显示，随页面滚动，或有单独滚动条
        - 文章目录放右侧，可有单独滚动条，滚动后会固定到顶部，文章内容宽度较窄
        - 页面滚动时，相应位置的目录标题高亮
        - 右侧栏还可显示版本、源码、反馈
      - 可在顶部显示文章大标题路径的面包屑菜单
    - 各级标题可以放在单独页面，类似书的目录页
    - 侧边栏可折叠隐藏
  - math blocks
# blog

## [6 Things Markdown Got Wrong_202003](https://www.swyx.io/markdown-mistakes/)

- Markdown is almost a perfect content authoring format

1. Lazy List Numbering
- we read markdown more than we write it - even as the people writing it! 
- It is a design philosophy of Markdown. 
- In practice, more people will reorder their numbered lists just to make it look right in markdown (either manually, or with tooling).
- 现在不支持部分乱序，不支持删掉某个序号
- allow * for unordered lists instead of the pretty-much-universally-used - (and the never-used +)
-  it's common for lexers to recognize sets of two characters (*.) over one (*).

2. code blocks (4 spaces) over code fences (```)
- Just to be clear what we're talking about
  - Code Blocks are how you indicate code (with 4 spaces), 
  - whereas Code Fences are the thing more people probably use today (with triple backticks).
- Code Blocks probably aren't necessary, and overlap with 2 important commonly used (but not headline) Markdown syntax features.
- To produce a code block in Markdown, simply indent every line of the block by at least 4 spaces or 1 tab. 
- The problem with Code Blocks is twofold. 
  - First, they weren't designed with developer tooling in mind. 
    - Code fences have room to let you indicate the language of the code content, and have even been extended to offer other metadata
    - code fences are more extensible than code blocks,and, it turns out - useful for readers of the unprocessed markdown too
  - another smaller problem - they coincide with hanging list indents.

3. can't nest Markdown in HTML in Markdown
- A genius decision by Gruber was to have Markdown be a superset of HTML
- you can remember it as HTML-in-Markdown
- sometimes you just want to define some wrapper components, and then use Markdown for the rest
  - In other words, we want Markdown in HTML in Markdown.

4. No Syntax for Adding Classes
- It isn't a design goal of Markdown to let you do everything you can do with HTML, 
  - but still it is essentially a language that compiles down to HTML.
- normally everything Markdown does is visible to the end user - it doesn't even have comments!
- Using wrapper divs is often a great way to manage layout and spacing and other important design considerations.
- offer Pandoc's format - as a Markdown flavor

5. No ID's in Headers
- This is important for URL accessibility.
- This lets GitHub offer its nice hover effect to remind you you can copy anchor links
- offering ID's for headers would also mean taking a stance on how to slug-case content.
- 能方便创建锚点url地址链接

6. No Option for Metadata
- This is related to the "no way to specify non-visible things" complaint above, 
  - but on a whole-document level instead of a per-element level.
- Sometimes you want to offer Markdown processors some extra data about how this specific Markdown document
- 存放文档数据相关而不是显示相关的内容，如布局、标签、类别
- Instead of having to specify this data in a separate file, it'd be nice to colocate this metadata alongside the content.
- why not offered by md? it involves another language that isn't Markdown and isn't HTML.
- it seems like Jekyll was the first to introduce Front Matter as the widely accepted Markdown metadata format 
  - and it uses YAML, which predates Markdown, but only by 3 years.
  - YAML itself has plenty of vocal detractors, so it isn't perfect.
  - But something for Metadata would have been really, really nice.

- Other small gripes
  - I wish Markdown had a distinction between an `<aside>` and a `<blockquote>` as I use both often.

- Conclusion
  - I don't even want to know all the competing alternatives present at the time and have to pick between them. 
  - Sometimes, Worse is Better.
  - And in the end, Markdown was successful enough.

- discussion

- [Design Mistakes in @gruber's Markdown (imo)](https://twitter.com/swyx/status/1240719259505963010)
- you missed what I consider the single biggest mistake in Markdown’s syntax: the syntax for images completely sucks. 
  - Unintuitive, the `!` seems arbitrary, and looks way too much like the syntax for links.
- Markdown doesnt have `<figcaptions>`, but this is a GREAT "hack" around it using CSS sibling selectors!!
  - too awesome not to share.
  - I use the syntax for title tags as an alternative to captions
    - `

![alt text](./image.png "caption here")

`

- [Things Markdown got wrong](https://news.ycombinator.com/item?id=22776108)
# ref
