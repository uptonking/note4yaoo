---
title: toc-office-markdown
tags: [doc, markdown, toc]
created: 2020-10-05T09:49:50.474Z
modified: 2021-01-04T17:26:25.032Z
---

# toc-office-markdown

# guide

# popular
- marktext /42.5kStar/MIT/202308/js/vue
  - https://github.com/marktext/marktext
  - https://www.marktext.cc/
  - simple and elegant markdown editor, available for Linux, macOS and Windows.
  - MarkText uses virtual DOM to render pages
  - 依赖electron-store、codemirror.v5、dragula、vue2、vuex、element-ui.v2、snabbdom

- https://github.com/Harry-Hopkinson/markdown-editor
  - A markdown editor written in Typescript.
  - Vite+Electron

- https://github.com/ahmedsaheed/Leaflet
  - A minimal distractionless markdown editor designed to quickly navigate between multiple `.md` files in a directory and its sub directories.
  - It features a clean mathematical typesetting, chemical equation rendering, code blocks highlighting and writing statistics 
  - 依赖codemirror6、@uiw/react-codemirror、electron

- https://github.com/foambubble/foam /14.6kStar/MIT/202401/ts
  - https://foambubble.github.io/
  - personal knowledge management and sharing system inspired by Roam Research, built on Visual Studio Code and GitHub.
  - [Add support for VSCodium](https://github.com/foambubble/foam/issues/26)
    - Foam is officially published to OpenVSX as of 0.7.5_202012

- https://github.com/atom-community/markdown-preview-plus
  - a fork of Markdown Preview that provides a real-time preview of markdown documents.

- markdoc /6.8kStar/MIT/202312/ts/inactive
  - https://github.com/markdoc/markdoc
  - https://markdoc.dev/
  - Markdoc is a Markdown-based syntax and toolchain for creating custom documentation sites and experiences.
  - 依赖markdown-it
  - We designed Markdoc to power Stripe's public docs
  - Markdoc extends Markdown with a custom syntax for tags and annotations
  - Markdoc uses `markdown-it` as a tokenizer, building an Abstract Syntax Tree (AST) from the array of tokens emitted by markdown-it.
    - The logic that parses the tag syntax is generated from a `peg.js` grammar.
  - **Markdoc has its own dedicated rendering architecture rather than relying on markdown-it to generate its output**. 
    - Developing an independent rendering system was necessary in order to handle Markdoc's custom tags and support multiple output formats.

- https://github.com/jackyzha0/quartz /MIT/202401/ts
  - https://quartz.jzhao.xyz/
  - a fast, batteries-included static-site generator that transforms Markdown content into fully functional websites
  - Quartz is a set of tools that helps you publish your digital garden and notes as a website for free. 
  - Quartz v4 features a from-the-ground rewrite focusing on end-user extensibility and ease-of-use.
# md-parser-generator
- remark 
  - https://github.com/remarkjs/remark/tree/main/packages/remark-parse
  - Parses Markdown to mdast syntax trees. 
  - Built on micromark and mdast-util-from-markdown

- marked /31.5kStar/MIT/202402/ts/NoDeps
  - https://github.com/markedjs/marked
  - https://marked.js.org/
  - A markdown parser and compiler. Built for speed.
  - light-weight while implementing all markdown features from the supported flavors & specification
  - works in a browser, on a server, or from a command line interface (CLI)
  - Marked can be extended using custom extensions. This is a list of extensions that can be used with `marked.use(extension)`.

- markdown-it /16.8kStar/MIT/202401/js
  - https://github.com/markdown-it/markdown-it
  - https://markdown-it.github.io/
  - Markdown parser done right. Fast and easy to extend.
  - Follows the CommonMark spec + adds syntax extensions & sugar (URL autolinking, typographer).
  - Community-written plugins and other packages on npm.
  - a fork of https://github.com/jonschlinkert/remarkable /js

- snarkdown /2kStar/MIT/202201/js/单文件
  - https://github.com/developit/snarkdown
  - pass a Markdown string, get back an HTML string
  - it's basically one regex and a huge if statement

- https://github.com/eczn/down-parse /ts/2019
  - markdown parser with a wonderful plugin system
# md-database
- https://github.com/datopian/markdowndb /MIT/202401/ts/sqlite
  - https://markdowndb.com/
  - JS library to turn markdown files into structured queryable database (SQL-based and simple JSON). 
  - It helps you build rich markdown-powered sites easily
  - Parses your markdown files to extract structured data (frontmatter, tags etc) and creates an index in a local `SQLite` database
  - Provides a lightweight javascript API for querying the database and importing files into your application

- https://github.com/lukesrw/md-database /202109/ts
  - Middleware for producing SQL queries from Markdown
  - Currently only SQLite is fully supported, with support for MySQL being worked on.

- https://github.com/fictorial/gg /201903/js
  - Markdown-backed database with queries, user-defined actions, validators, variable expansion, and reporters in JavaScript
  - gg is a CLI to import, query, act on, and report on local Markdown files with support for user-defined JavaScript extensions.
  - gg supports a subset of Markdown for parsing: headers, paragraphs (the "type-inferred values"), and un-nested bullet lists 

- https://github.com/daeh/zotero-markdb-connect /MIT/202401/ts
  - Zotero plugin that links your Markdown database to Zotero. 
  - Jump directly from Zotero Items to connected Markdown files.
  - Supports various Markdown databases, including Obsidian, logseq, and Zettlr
  - Supports various Markdown databases, including Obsidian, logseq, and Zettlr
# tools
- monotome /151Star/AGPLv3/202208/js
  - https://github.com/cblgh/monotome
  - a personal knowledge base system. markdown markup, runs in the browser
  - 依赖 marked
  - 原理是 根据url动态读取解析markdown文件，并渲染显示所有文件名，切换文件时会触发fetch
  - 代码量不大，思路清晰
  - Monotome has support for the common `[[wiki]]` syntax
  - Monotome keeps track of backlinks, or incoming links from one article inside monotome to another. 
  - Subjects are ordered into a simple directory structure which is mirrored by index.json.
  - You can fill index.json's subjects by hand if you want to avoid running a script. You can also run node monotome/bin/generate.js, which will update index.json for you.

- NextBook /168Star/MIT/202206/js/inactive
  - https://github.com/amiroff/NextBook
  - https://next-book.vercel.app/
  - 依赖 next11、next-mdx-remote、react、remark、tailwindcss
  - 若屏幕很窄，官方文档会显示水平滚动条，此时滚动会有严重的漂移感
  - easy way to build technical books or documentation with markdown or MDX

- https://github.com/Kffhi/markdown-reader
  - 一个简单的markdown文件解析服务，可以读取服务器指定目录下的md文件并返回相关数据用于前端展示

- https://github.com/shuding/nextra
  - 依赖next、nextra-core、react
  - powerful and flexible site generation framework with everything you love from Next.js.
  - Any change to example/docs will be re-rendered instantly.
  - Nextra first collects all your Markdown files and configurations from the pages directory, and then generates the “page map information” of your entire site, to render things such as the navigation bar and sidebar 
    - By default, the page map contains all .md and .mdx filenames and the directory structure, sorted alphabetically.
    - You can have an `_meta.json` file in each directory, and it will be used to override the default configuration of each page

- https://github.com/plantain-00/simple-doc
  - A Server-less and Build-less markdown document application.
  - 默认显示README.md

- https://github.com/plantain-00/markdown_to_pdf
  - A CLI tool to convert a markdown to a pdf file.

- silverbullet /1.5kStar/MIT/202401/ts
  - https://github.com/silverbulletmd/silverbullet
  - https://silverbullet.md/
  - SilverBullet is an extensible, open source personal knowledge platform. 
  - implemented as an open-source offline-capable web application.
  - At its core it’s a clean markdown-based writing/note taking application that stores your pages (notes) as plain markdown files in a folder referred to as a space. 
  - While SB uses a database for indexing and caching some indexes, all of that can be rebuilt from its markdown source at any time. 
  - extensible with plugs, and you can customize it
  - [Silver Bullet: Markdown-based extensible open source personal knowledge platform | Hacker News_202212](https://news.ycombinator.com/item?id=33843009)
# apps
- https://github.com/motifland/markprompt
  - Markprompt is a platform for building GPT-powered prompts. 
  - It scans Markdown, Markdoc and MDX files in your GitHub repo and creates embeddings that you can use to create a prompt

- https://github.com/rhiokim/haroopad /201606/js
  - Haroopad is a markdown enabled document processor for creating web-friendly documents.

- https://github.com/amitmerchant1990/electron-markdownify /923Star/MIT/202111/js/inactive
  - minimal Markdown Editor desktop app built on top of Electron.
  - Sync Scrolling
# import/export
- https://github.com/mark-magic/mark-magic /MIT/202402/ts
  - 一个基于 markdown 的数据连接与转换工具，解决不同工具之间数据转换以及部分常用工具之间的协调。
  - joplin => hugo 生成 blog

- https://github.com/LetTTGACO/elog /MIT/202401/ts
  - https://elog.1874.cool/
  - Markdown 批量导出工具、开放式跨平台博客解决方案
  - 随意组合写作平台(语雀/飞书/Notion/FlowUs)和部署平台(Hexo/Vitepress/Halo/Confluence/WordPress等)
  - Elog支持了在生成MD文件之前，将扫描到的图片上传到图床上，并对文档中的图片链接进行替换。 当前支持的图床有： 本地/阿里云oss/腾讯云cos/Github图床
  - https://github.com/LetTTGACO/elog-docs
    - Elog 的使用文档

- https://github.com/kscript/markdown-download /MIT/202401/js
  - 谷歌浏览器插件: 将掘金、知乎、思否、简书、博客园、微信公众号、开源中国、CSDN的文章转为markdown文档并下载
# more-md
- https://github.com/mgmeyers/obsidian-kanban /GPLv3/202309/ts
  - https://publish.obsidian.md/kanban/
  - Create markdown-backed Kanban boards in Obsidian.

- https://github.com/rstudio/rmarkdown
  - rmarkdown package helps you create dynamic analysis documents
