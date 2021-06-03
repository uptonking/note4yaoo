---
title: lib-office-remark-extensions
tags: [extensions, remark]
created: '2021-06-02T16:48:25.585Z'
modified: '2021-06-02T16:49:11.370Z'
---

# lib-office-remark-extensions

# guide

- tips
  - 可执行代码块的一种典型实现，就是mermaid
  - remark的插件，xdm用不了

- code-block-extensions-ideas
  - 高亮的代码显示在**深色背景的卡片**上
  - 给显示代码块的卡片加上标题栏，可显示文件名，也可以显示button、多个button
  - 支持wikipedia风格的footnote`^`.
  - 支持import code from file，在fence后面添加元信息
  - 支持显示多个tab，如html、css、js、ts，甚至是split view
  - 将list显示为tree

- code-block-integrations/connections
  - 对于复杂的例子，考虑嵌入codepen/codesandbox
  - 支持mermaid text/code显示为流程图
  - 支持LaTeX显示为svg
  - 支持执行jupyter代码

- ref
  - remark code block
  - remark code
  - remark render / output
  - not-yet: format, prettier
  - [remark plugins list](https://github.com/remarkjs/remark/blob/main/doc/plugins.md)
  - [prismjs vs hightlight.js: hightlight下载较高，因为创建较早](https://www.npmtrends.com/highlight.js-vs-prism-react-renderer-vs-prismjs-vs-react-highlight.js-vs-react-syntax-highlighter-vs-react-highlight)
# extensions-code-block
- https://github.com/mrzmmr/remark-code-blocks
  - Remark plugin to extract `code` nodes from markdown.
  - Remark plugin for selecting and storing code blocks from markdown.

- https://github.com/remcohaszing/remark-mdx-code-meta
  - interprets markdown code block metadata as JSX props.
- https://github.com/shawnbot/remark-fenced-props
  - Parse fenced code block "meta" strings as JSX props
- https://github.com/s0/remark-code-extra
  - Add to or transform the HTML output of markdown code blocks using remark.
- https://github.com/s0/remark-code-frontmatter
  - Extract frontmatter from markdown code blocks using remark and front-matter, and do interesting things!
  - Add properties that add indentation to your code
  - Add properties that specify links that should be attached to the HTML output of your code

- https://github.com/remark-embedder/core
  - transform a link in your markdown into the embedded version of that link.

- https://github.com/elpnt/inkdrop-code-title
  - Add a title to a fenced code block
  - 显示在左上角的title
- https://github.com/rockchalkwushock/rehype-code-titles
  - Rehype plugin for parsing code blocks and adding titles to code blocks

- https://github.com/Swizec/remark-code-screenshot
  - Remark plugin to convert code blocks into carbon.now.sh screenshots.

- https://github.com/ice-zjchen/remark-codeset
  - Adds syntax to parse sets of code blocks in markdown. Transforms them to tablist.
  - https://github.com/lwhiteley/remarkable-codegroup

- https://github.com/sergioramos/remark-prism
  - Syntax highlighter for markdown code blocks using Prism
- https://github.com/remarkjs/remark-highlight.js
  - plugin to highlight code blocks with highlight.js (via lowlight)
- https://github.com/rajinwonderland/react-code-blocks
  - 支持定制化的高亮react代码，也支持其他语言
  - support themes (i.e railscast, darcula, monokai, etc), customizable styles, and copy functionality too!
- https://github.com/craftzdog/remark-react-codemirror
  - Syntax highlighting for remark-react through CodeMirror

- https://github.com/Qard/remark-lint-code
  - Lint fenced code blocks by corresponding language tags
- https://github.com/ybiquitous/remark-lint-code-block-syntax
  - A remark-lint rule to check language syntax in a code block.
- https://github.com/leo-buneev/eslint-plugin-md
  - Allows you to lint markdown code in your *.md files.

- https://github.com/trevorblades/remark-typescript
  - Transpiles TypeScript code blocks to JavaScript and inserts them into the page

- https://github.com/kevin940726/remark-code-import
  - The plain remark version of gatsby-remark-import-code.
  - ```js file=./say-hi.js#L3-L6```.
- https://github.com/fuxingloh/remark-code-import-replace
  - code file import and optionally replace the code block.
  - ```js import=code.js render param```.
- https://github.com/jknoxville/remark-code-snippets
  - importing snippets of source files, as code blocks
  - ```js file=./say-hi.js start=start_here end=end_here```.
- https://github.com/forbesmyester/remark-unixpipe
  - Pipe the body of markdown code blocks through UNIX command specified in their meta
# integrations-code-block
- https://github.com/kevin940726/remark-codesandbox
  - Create CodeSandbox directly from code blocks
  - 基于fenced code block```jsx csb=react ```.
- https://github.com/andreystepanov/remark-merge
  - merge two or more consecutive blockquote or code elements into one

- https://github.com/temando/remark-mermaid
  - Replaces fenced code blocks in mermaid format with 
    - Links to rendered SVG files of the graph (default mode).
    - Mermaid-formatted code wrapped in `div` tags for rendering by mermaidjs (simple mode).
  - 还支持直接显示图形文件`[Link to a Graph](test/example.mmd "mermaid:")`.
- https://github.com/Braincoke/gridsome-plugin-remark-mermaid
  - Use mermaid code blocks in your markdown to generate diagrams.
  - It uses server-side rendering to generate inline SVG code during the build process.

- https://github.com/huy-nguyen/remark-github-plugin
  - replace links to GitHub files with the actual content of those files, wrapped in Markdown code blocks

- https://github.com/duanwilliam/docusaurus-remark-plugin-codetabs
  - docusaurus v2 plugin for easily making multi language code tabs

- https://github.com/jamessimone/gatsby-remark-codefence
  - Add codefence to your gatsby site's markdown
- https://github.com/raae/gatsby-remark-oembed
  - transforms oembed links into its corresponding embed code.
- https://github.com/vzhou842/gatsby-remark-code-headers
  - Add headers (like filenames) to code blocks for Gatsby.js.
- https://github.com/iamskok/gatsby-remark-code-buttons
  - Add buttons to markdown code snippets. 如复制、保存
- https://github.com/gera2ld/gatsby-remark-markmap
  - render markdown list as mindmap/tree
- https://github.com/raulrpearson/gatsby-remark-latex-blocks
  - Processes LaTeX code blocks in your markdown files and replaces them with the rendered SVG, leverages dvisvgm behind the scenes
- https://github.com/baerrach/gatsby-remark-plantuml
  - Gatsby Remark parser for PlantUML code blocks
  - https://github.com/Mogeko/gatsby-remark-plantuml-lite
- https://github.com/JosephusPaye/gatsby-remark-graphviz
  - Intercepts code-blocks written in DOT in your Markdown files and compiles them to SVG using GraphViz.
  - https://github.com/rhanekom/gatsby-remark-draw
- https://github.com/teaglebuilt/gatsby-theme-binder
  - interactive remark code blocks powered by jupyter kernels for code execution.
# [remark-official-repos](https://github.com/search?o=desc&q=user%3Aremarkjs&s=stars&type=Repositories)
- https://github.com/remarkjs/remark
- https://github.com/remarkjs/react-markdown
- https://github.com/remarkjs/remark-react
- https://github.com/remarkjs/remark-lint
- https://github.com/remarkjs/remark-toc
- https://github.com/remarkjs/remark-html
- https://github.com/remarkjs/remark-math
- https://github.com/remarkjs/remark-frontmatter
- https://github.com/remarkjs/remark-rehype
- https://github.com/remarkjs/strip-markdown
- https://github.com/remarkjs/remark-gfm
- https://github.com/remarkjs/remark-vdom
- https://github.com/remarkjs/remark-highlight.js
- https://github.com/remarkjs/remark-external-links
- https://github.com/remarkjs/remark-github

- https://github.com/remarkjs/awesome-remark
# extensions-react
- https://github.com/remarkjs/react-remark
  - a React hook and React component based way of rendering markdown into React using remark
# extensions
- https://github.com/arobase-che/remark-attr
  - adds support for custom attributes to Markdown syntax.
  - 图片!`[alt](img){ height=50 }`，设置在{}

- https://github.com/landakram/remark-wiki-link
  - This remark plugin parses and renders `[[Wiki Links]]`.

- https://github.com/zWingz/remark-container
  - markdown container like markdown-it-container
- https://github.com/Nevenall/remark-containers
  - provides parsing for containers in your markdown.

- https://github.com/remcohaszing/remark-mermaidjs
  - A remark plugin to render mermaid diagrams using puppeteer

- https://github.com/tmcw/remark-devim
  - removes newlines from paragraphs in order to make Markdown render the same between Jekyll and GitHub.
# more-remark
- https://github.com/djm/remark-shortcodes
  - A custom Markdown syntax parser for remark that adds support for shortcodes.
  - What are shortcodes? They are a way to provide hooks for macros and/or template partials inside a markdown file. 
  - `[[ MailchimpForm id="chfk2" ]]`. 可配置头尾标志
