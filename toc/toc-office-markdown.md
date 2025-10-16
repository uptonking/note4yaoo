---
title: toc-office-markdown
tags: [doc, markdown, toc]
created: 2020-10-05T09:49:50.474Z
modified: 2021-01-04T17:26:25.032Z
---

# toc-office-markdown

# guide

# popular
- marktext /42.5kStar/MIT/202403/js/vue/inactive
  - https://github.com/marktext/marktext
  - https://www.marktext.cc/
  - simple and elegant markdown editor, available for Linux, macOS and Windows.
  - MarkText uses virtual DOM to render pages
  - 依赖electron-store、codemirror.v5、dragula、vue2、vuex、element-ui.v2、snabbdom
  - https://github.com/marktext/muya /549Star/MIT/202404/ts
    - markdown editor for web browser applications development
    - 依赖fuse.js、marked、katex、ot-json1、prismjs、snabbdom、turndown、vega-lite
    - Muya originated from MarkText, which was originally used in the MarkText and provides Markdown editing support for MarkText. Today, Muya is available as a stand-alone library 
    - What is the relationship between MarkText's version and the Muya's version? None

- https://github.com/Harry-Hopkinson/markdown-editor
  - A markdown editor written in Typescript.
  - Vite+Electron

- https://github.com/ahmedsaheed/Leaflet /CC-BY-NC-SA/202305/ts/inactive
  - https://leaflet.saheed.codes/
  - A minimal distractionless markdown editor designed to quickly navigate between multiple `.md` files in a directory and its sub directories.
  - 依赖codemirror6、@uiw/react-codemirror、electron
  - It features a clean mathematical typesetting, chemical equation rendering, code blocks highlighting and writing statistics 

- https://github.com/foambubble/foam /14.6kStar/MIT/202401/ts
  - https://foambubble.github.io/
  - personal knowledge management and sharing system inspired by Roam Research, built on Visual Studio Code and GitHub.
  - [Add support for VSCodium](https://github.com/foambubble/foam/issues/26)
    - Foam is officially published to OpenVSX as of 0.7.5_202012

- https://github.com/atom-community/markdown-preview-plus
  - a fork of Markdown Preview that provides a real-time preview of markdown documents.

- markdoc /7.6kStar/MIT/202508/ts
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

- https://github.com/microsoft/markitdown /MIT/202411/python
  - Python tool for converting files and office documents to Markdown.
  - a utility tool for converting various files to Markdown (e.g., for indexing, text analysis, etc.)
  - supports: PDF (.pdf) PowerPoint (.pptx) Word (.docx) Excel (.xlsx) Images (EXIF metadata, and OCR) Audio (EXIF metadata, and speech transcription) HTML (special handling of Wikipedia, etc.) Various other text-based formats (csv, json, xml, etc.)
  - https://msftmd.replit.app/
    - Powered by Microsoft MarkItDown, this tool converts various file formats to clean, structured Markdown for easy analysis and indexing.
    - https://x.com/mattppal/status/1867703377888784880
      - If you're wondering how I did this so fast, it was Agent + Assistant + deploy on Replit
  - https://x.com/kepano/status/1867664671446381017
    - https://www.getmarkdown.com/
      - Someone turned the Microsoft conversion tool into a webapp that runs on your device.
    - Very nice. But from a business point hard to understand. Microsoft‘s whole business model is based on ecosystem lock-in, not the quality of products.
    - Markdowns may be easier on ai.

- https://github.com/zcaceres/markdownify-mcp /MIT/202501/ts
  - Markdownify is a Model Context Protocol (MCP) server that converts various file types and web content to Markdown format. 
  - It provides a set of tools to transform PDFs, images, audio files, web pages, and more into easily readable and shareable Markdown text.

- https://github.com/MarkPDFdown/markpdfdown /1.5kStar/apache2/202507/python
  - 一款基于大模型视觉识别的高质量PDF转Markdown工具
  - By utilizing advanced multimodal AI models, it can accurately extract text, preserve formatting, and handle complex document structures including tables, formulas, and diagrams.
  - Customizable Model: Configure the model to suit your needs
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
  - Warning: Marked does not sanitize the output HTML
  - `const html = marked.parse('# Marked in Node.js\n\nRendered by **marked**.');`; 
  - `marked-highlight`语法高亮基于highlightjs实现

- markdown-it /16.8kStar/MIT/202401/js
  - https://github.com/markdown-it/markdown-it
  - https://markdown-it.github.io/markdown-it/
  - https://markdown-it.github.io/
  - Markdown parser done right. Fast and easy to extend.
  - Follows the CommonMark spec + adds syntax extensions & sugar (URL autolinking, typographer).
  - Community-written plugins and other packages on npm.
  - `const md = markdownit(); const html = md.render('# markdown-it rule\n');`; 
  - a fork of https://github.com/jonschlinkert/remarkable /MIT/202505/js/inactive
  - [Lazy highlighting _202408](https://github.com/markdown-it/markdown-it/issues/1045)
    - The current render code seems to do everything in one sequential flow. As soon as it finds a fenced block it passes it though the highlight function. Which works fine if the highlighter being used is ready for it.
    - Loading them all in memory at once (like `highlight.js` allows) results in a MB big minified js file which i very much like to prevent.
    - But the render mechanism in markdown-it seems to be not so happy about a on-demand highlighter.
    - I fixed this by, at parse time, "remembering which fenced blocks" went through the parser and then, once parsed, go over those blocks again and load the syntax highlighting files. That works as lazy enough. It's quite a bit more involved then this but it works. 

- snarkdown /2kStar/MIT/202201/js/单文件
  - https://github.com/developit/snarkdown
  - pass a Markdown string, get back an HTML string
  - it's basically one regex and a huge if statement

- https://github.com/eczn/down-parse /ts/2019
  - markdown parser with a wonderful plugin system
# md-database
- https://github.com/datopian/markdowndb /392Star/MIT/202503/ts/sqlite
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

- https://github.com/k-lar/dynomark /MIT/202411/go
  - Dynomark strives to be a markdown query language engine, similar to obsidian's Dataview plugin.
  - This program can be used with editors like neovim, vscode and emacs to provide a similar experience to Dataview (but very barebones for now).
  - https://github.com/k-lar/vscode-dynomark
    - This extension is a wrapper around that engine, and provides a simple way to query your markdown files.
# streaming
- https://github.com/vercel/streamdown /2.7kStar/apache2/202509/ts
  - https://streamdown.ai/
  - A drop-in replacement for react-markdown, designed for AI-powered streaming.
  - Streamdown powers the AI Elements Response component but can be installed as a standalone package for your own streaming needs.
  - Drop-in replacement for react-markdown
  - Streaming-optimized - Handles incomplete Markdown gracefully
  - GitHub Flavored Markdown - Tables, task lists, and strikethrough support
  - Unterminated block parsing - Styles incomplete bold, italic, code, links, and headings
  - Math rendering - LaTeX equations via KaTeX
  - Mermaid diagrams - Render Mermaid diagrams as code blocks with a button to render them
  - Code syntax highlighting - Beautiful code blocks with Shiki
  - Security-first - Built on harden-react-markdown for safe rendering
  - [Introducing Streamdown: Open source Markdown for AI streaming - Vercel _202508](https://vercel.com/changelog/introducing-streamdown)

- https://github.com/Simon-He95/vue-markdown-render /430Star/MIT/202510/ts/vue
  - https://vue-markdown-renderer.netlify.app/
  - A Vue 3 renderer specifically built for AI-powered streaming Markdown: Monaco incremental, Mermaid progressive, and KaTeX formula speed, with real-time updates and no jitter, ready to use out of the box.
  - Streaming diff code blocks: show diffs as they arrive for instant feedback.
  - Built for scale: optimized DOM updates and memory usage for very large documents.
  - Streaming-first rendering: render partial or incrementally-updated Markdown content without re-parsing the whole document each time. 
  - [Show HN: Vue-Markdown-render – up to 100× faster streaming Markdown for Vue 3 | Hacker News _202509](https://news.ycombinator.com/item?id=45238350)
    - Streamdown targets server-side streaming; our results are for client rendering. Ideal for AI chatbot UIs.

- https://github.com/thetarnav/streaming-markdown /266Star/MIT/202505/js
  - https://thetarnav.github.io/streaming-markdown/
  - Experiment making a streaming makdown parser à la ChatGPT.
  - It's single argument is a `Renderer` object, which is an interface to render the parsed markdown tokens to the DOM.

- https://github.com/rossrobino/robino/tree/main/packages/md /MIT/202506/ts
  - An extended markdown-it instance 
  - Syntax highlighting with shiki using the CSS variables theme to style
  - `stream` function to render and highlight a stream of markdown
    - stream streams the result of a markdown stream through the renderer/highlighter.
    - The result will come in chunks of elements instead of by word since the entire element needs to be present to render and highlight correctly.

- https://github.com/lixpi/markdown-stream-parser /MIT/202509/ts
  - https://markdown-stream-parser.lixpi.org/
  - A library designed to incrementally parse Markdown text from a stream of tokens.
  - It's built to handle the ambiguities of LLM-generated streams, which often produce imperfect or invalid Markdown.
  - It combines a finite state machine with regex patterns to determine the best match for each segment.
  - [Evaluate whether continuing with completely custom parser implementation is reasonable, or shall we leverage lexers? _202505](https://github.com/Lixpi/markdown-stream-parser/issues/5)
    - My initial implementation was extremely naive. Currently working on a complete reimagined version that uses `Tree-sitter` for parsing, but provides the same interface for the stream of parsed chunks.
# ui
- https://github.com/BlueprintLabIO/markdown-ui /412Star/MIT/202509/ts
  - https://markdown-ui.blueprintlab.io/
  - https://markdown-ui.com/
  - An open standard for rendering interactive widgets in plain Markdown
  - Readable everywhere: Preview rich UI, but if unsupported, it's still legible Markdown
  - Zero lock-in: Pure spec—works with any Markdown parser + any UI framework
  - [Show HN: Turn Markdown into React/Svelte/Vue UI at runtime, zero build step | Hacker News _202508](https://news.ycombinator.com/item?id=45024532)
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

- https://github.com/gcui-art/markdown-to-image /apache2/202412/ts
  - https://readpo.com/poster
  - This React component is used to render Markdown into a beautiful poster image, with support for copying as an image
  - The project also includes a built-in web editor that can be used as an online Markdown-to-poster editor with a simple one-click deployment.
# more-md
- https://github.com/mgmeyers/obsidian-kanban /GPLv3/202309/ts
  - https://publish.obsidian.md/kanban/
  - Create markdown-backed Kanban boards in Obsidian.

- https://github.com/rstudio/rmarkdown
  - rmarkdown package helps you create dynamic analysis documents
