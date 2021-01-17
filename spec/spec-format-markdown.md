---
title: spec-format-markdown
tags: [format, markdown]
created: '2019-12-24T11:23:55.280Z'
modified: '2020-10-15T13:41:05.547Z'
---

# spec-format-markdown

# spec

- markdown
  - https://daringfireball.net/projects/markdown/
- GitHub Flavored Markdown Spec
  - https://github.github.com/gfm/
  - https://guides.github.com/features/mastering-markdown/

# [mdx](https://mdxjs.com/getting-started/)

- ref
  - I'm not an expert in JSX or MDX, but looking at the code example I would think MDX could also handle Web Components.

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

# ref
