---
title: lib-fwk-hexo-examples
tags: [examples, hexo, static-site-generator]
created: 2024-02-09T10:54:47.417Z
modified: 2024-02-09T10:55:03.085Z
---

# lib-fwk-hexo-examples

# guide

# popular
- https://github.com/next-theme/hexo-theme-next /2.2kStar/AGPLv3/202402/js/stylus
  - https://theme-next.js.org/
  - Elegant and powerful theme for Hexo.
  - https://github.com/next-theme/plugins
    - Third-party front-end plugins for Hexo theme NexT
  - https://github.com/theme-next/hexo-theme-next /AGPLv3/202107/js
    - https://theme-next.org/
    - Elegant and powerful theme for Hexo
  - https://github.com/iissnan/hexo-theme-next /MIT/201801/js
    - http://notes.iissnan.com/
    - Elegant theme for Hexo

- https://github.com/dimaslanjaka/static-blog-generator /MIT/202401/ts
  - http://www.webmanajemen.com/docs/static-blog-generator/
  - Static Blog Generator v3 using HexoJS.
  - Pre-processing of all source posts/articles before rendering using hexo.
  - With this package you can prevent using a large number of hexo plugins, because some functions (runners) are separated by task, so they are memory friendly.
  - Automatic SEO
  - Finding broken images/links
  - External link anonymizer using safelinkify
  - Export/Import Blogger and Wordpress
  - https://github.com/dimaslanjaka/sbg-themes

- https://github.com/hexojs/hexo-server /MIT/202401/js
  - Server module for Hexo.
  - options passed to serve-static
- https://github.com/KazariEX/hexo-server-live /MIT/202401/js
  - Live reload when source files change for Hexo. 
  - Support PJAX and Hot-reloading CSS.
- https://github.com/kimown/hexoserver /MIT/201701/js
  - a server for hexo , using webpack-dev-server, react-hot

- https://github.com/hexojs/hexo-fs /MIT/202402/ts
  - File system module for Hexo.
  - Use `graceful-fs` to avoid EMFILE error and various improvements.
  - Use `chokidar` for consistent file watching.

- https://github.com/hexojs/hexo-generator-archive /MIT/202210/js
  - Archive generator plugin for Hexo.
  - Order by date descending by default

- https://github.com/hexojs/hexo-pagination /MIT/202008/js
  - Pagination utilities for Hexo generator plugins.
- https://github.com/hexojs/hexo-front-matter /202402/ts
  - Front-matter allows you to specify data at the top of a file

- https://github.com/hexojs/hexo-generator-index /MIT/202103/js
  - Index generator for Hexo.
  - It generates an archive of posts on your homepage, according to the index or archive layout of your theme.
  - https://github.com/Jamling/hexo-generator-index2 /201803/js
    - Add filter feature base on the official index generator and generate some specail posts to special folder.

- https://github.com/next-theme/hexo-generator-searchdb /MIT/202212/js
  - Search data generator plugin for Hexo.
  - This plugin is used for generating a search index file, which contains all the necessary data of your articles that you can use to write a local search engine for your blog. 
  - Supports both XML and JSON format output.
  - https://github.com/theme-next/hexo-generator-searchdb /archived
  - https://github.com/theme-next/hexo-generator-search /for Hexo 3.0

- https://github.com/wzpan/hexo-generator-search /MIT/202111/js/inactive
  - This plugin is used for generating a xml/json file from your Hexo blog that provides data for searching.
  - Generate search data for Hexo 3.x and 4.x. 
  - This plugin is used for generating a search index file, which contains all the necessary data of your articles that you can use to write a local search engine for your blog. Supports both XML and JSON format output.
  - If you don't want to write search engine by yourself, there are many themes that take use this plugin for local searching that works out of box.
- https://github.com/AsemAlhaidary/hexo-search-generator /202206/js
  - an updated version of the hexo-generator-search package
  - The output file (search.xml) of the original package was missing to some informations about the posts, so I have made this updated version to add the informations that I need in my projects
- https://github.com/sumcai/hexo-generator-search-plus /202204/js
  - 在原始版本上做了以下一些修改：
  - 生成的 XML 文件 content 部分去掉了代码及 HTML Tag，这有助于减小文件体积，且可以提高搜索时的准确度；
  - 修复文章的Front-matter 中设置固定路径 permalink时url中出现\\的问题。
- https://github.com/barretlee/hexo-search-plugin-snippets /201706/js
  - 一些辅助 hexo-generator-search 插件的代码片段

- https://github.com/shundroid/hexo-search-result /MIT/202103/js
  - Add a search result page for hexo-generator-search.

- https://github.com/fengkx/hexo-generator-search-index /GPLv3/202104/js
  - Use js-search to generate index
  - Use jieba-wasm to tokenize chinese
  - It generates an object which key is the query and value is an array of document (post/page) index sorted as roguhly idftf desc.
  - It is just an experiment. With index generated it almost doubled the size of search.json. So it maybe loads slower

- https://github.com/LouisBarranqueiro/hexo-algoliasearch /MIT/202210/js
  - A plugin to index posts of your Hexo blog on Algolia
  - https://github.com/thom4parisot/hexo-algolia /202102/js
    - Index content of your hexo website in Algolia and add search within minutes

- https://github.com/JakeLaoyu/hexo-browser-search /MIT/202312/js
  - 使用koa2、redis完成hexo博客chrome浏览器地址栏搜索

- https://github.com/sergeyzwezdin/hexo-search-indexer /MIT/202005/js
  - a plugin for Hexo static site generator that generates JSON file that contains all data to implement site search
  - Generates search-ready JSON file with all data of the website.
  - Allows to define "reserved" words that won't be split during word normalize (e.g. `ASP.NET` will not be split into ASP and NET).
  - The plugin scans all posts on the website and extracts words for every post.
  - For every word stemmers are applied.

- https://github.com/dimaslanjaka/hexo-seo /apache2/202401/ts
  - Automated Search Engine Optimization (SEO) for Hexo
  - Auto add sitemap (forked from yoast seo wordpress plugin)
  - Tested on hexo instances with 1000 more posts and pages

- https://github.com/Sukwants/hexo-post-replace /MIT/202310/js
  - A plugin for Hexo, which helps to replace words in the posts.

- https://github.com/hexojs/hexo-i18n /MIT/202210/ts
  - i18n module for Hexo.

- https://github.com/adamsiwiec/hexagon /201907/js
  - A package manager for Hexo.

- https://github.com/0x-jerry/vscode-hexo-utils /MIT/202401/ts
  - A sidebar for Hexo blog system.
  - Create new article with exists template
  - Sidebar, include tags, categories, posts and drafts

- https://github.com/kaiyuanshe/git-pager /AGPLv3/202310/ts
  - https://git-pager.vercel.app/
  - Post Editor for MarkDown static Web-site generators (Hexo etc.) based on GitHub API
  - react, MobX.v5, Workbox.v7, Koa
  - 前端生产环境 + 后端调试环境

- https://github.com/0x-jerry/vscode-hexo-utils
# hexo-admin/editor
- https://github.com/jaredly/hexo-admin /201806/js/inactive
  - https://jaredforsyth.com/hexo-admin/admin/
  - An admin UI for the Hexo blog engine. Based off of the Ghost interface, with inspiration from svbtle and prose.io.
  - I haven't used Hexo in several years
  - 支持编辑

- https://github.com/D-Sketon/hexo-dashboard /MIT/202309/js/wip
  - use React 18 to refactor hexo-admin

- https://github.com/ChesterZengJian/hexo-admin-modern /MIT/202307/js
  - An admin UI for the Hexo blog engine. Based off of the Ant-React Interface.
  - Use version 1.x of this plugin only support Hexo version 5.x

- https://github.com/quincyyhuang/hexo-node-admin /MIT/202005/js
  - A Hexo management tool with responsive UI designed to make it easier for you to compose.
  - Works with 4.x, 3.x, not sure if it works with 2.x or 1.x, you can give it a try
  - Support loading the admin on subdirectory. For example, '/admin' of your blog URL.
  - Support Post Asset Folder feature. You can upload and delete post assets.

- https://github.com/ESHexoN/ESHexoN /202212/js/vue
  - https://eshexon.js.cool/
  - 简洁、强大的 Hexo 在线编辑器
  - 后端部署支持 Deno 与 Cloudflare Workers 两个平台。
  - ESHexoN 官方使用 Vue + Vuetify 构建了一个公共前端。

- https://github.com/thesadabc/hexo-myadmin /202309/js/vue
  - a hexo dashboard plugin, for live hexo server.

- https://github.com/Qexo/Qexo /1.3kStar/GPLv3/202402/python
  - 一个快速、强大、漂亮的在线 Hexo 编辑器
  - 开放 API

- https://github.com/DeepSpaceHarbor/hexo-bridge /GPLv2/202310/js
  - Admin panel for websites powered by hexo.
  - Post and page editor
  - File manager

- https://github.com/tajpure/hexo-editor /201808/js/inactive
  - https://github.com/tajpure/hexo-editor/wiki/Getting-Started
  - a web editor for hexo blog platform. You can use it to edit, generate and deploy posts over the web. 
  - This editor will auto save your post to the server by TextSync.
  - https://github.com/tajpure/TextSync /201606/js/inactive
    - Synchronize text from client to server based on the `rsync` algorithm

- https://github.com/MaLuns/hexo-editor /GPLv2/202304/ts/vue
  - 在线 Hexo 写作编辑器
  - 文章增删改和预览

- https://github.com/gethexon/hexon /GPLv3/202311/ts/vue
  - a GUI for hexo with git, run commands and manage content for you.
  - Online image management use imageur
  - https://github.com/YuJianghao/winwin-hexo-editor
    - For latest version, please visit Hexon

- https://github.com/Wexagonal/Wexagonal /GPLv3/2022204/js/inactive
  - https://wexa.top/
  - 轻量级\多平台\开箱即用的hexo后端管理器

- https://github.com/yiyingcanfeng/hexo-blog-admin /MIT/202208/js/java
  - 一个基于vue-admin-template的hexo博客后台管理。包含了文章管理，文章发布，评论管理，用户管理等功能。

- https://github.com/geekwen/hexo-local-admin /201803/js
  - This is a hexo site admin tool(works only on your local machine.). 
  - You can use this tool to manage your posts, pages, drafts and trash, even can launch hexo server and deploy your site! Try it out!

- https://github.com/Frodez/HexoPlus /202005/ts/inactive
  - Graphic User Interface implement for the Hexo
  - Angular9, Electron

- https://github.com/haojie06/gowriter /202109/js/go
  - A web-based editor for static website generator such as hugo and hexo.
  - 当前的版本面向的是将静态网站部署在自己的服务器上的用户，使用Github、Cloudflare Page部署的版本可能要未来才会有。
  - Hugo、Hexo等静态网站生成程序可以很方便的生成网站，静态网站能够节约很多资源并且部署方便。但是对于经常更新的博客等网站，有时候可能不那么方便，编写好之后还要上传
  - 我想，能不能写一个程序提供一个web编辑器界面，可以读取我们的Hugo、Hexo站点文件夹，可以对现有的文章进行编辑、添加新的文章、修改站点配置、直接在web上控制重新生成页面等等，所以有了这个项目

## server

- https://github.com/do-adams/nes-auth-blog /201812/js
  - A static blog with fun Nintendo-themed user authentication built with Hexo, Koa, and NESS.css.
  - nes-auth-blog uses Hexo with a customized aath theme to render your markdown files into a static blog. 
  - It then runs a lightning-fast Koa server with static user authentication to serve the blog.
# themes
- https://github.com/kaiiiz/hexo-theme-book /MIT/202010/js/inactive
  - https://kaiiiz.github.io/hexo-theme-book-demo/
  - book-like hexo theme with some useful features.
  - 效果类似docusaurus
  - 支持滚动时高亮toc中的标题
  - https://github.com/kaiiiz/hexo-theme-book-demo
- https://github.com/llnancy/hexo-theme-book /202301/js/中文版
  - https://lilu.org.cn/library/
  - hexo 主题：可以用来写书
  - 支持滚动时高亮toc中的标题
  - I have already migrated my note from hexo to hugo

- https://github.com/objchris/hexo-theme-bookcase /MIT/202001/js/inactive
  - https://objchris.com/hexo-theme-bookcase/
  - A clean, Gitbook style theme for HEXO.
  - 侧边栏可隐藏
  - 未实现toc标题面板

- https://github.com/nexmoe/hexo-theme-yet-the-books /MIT/202111/js/ejs
  - https://books.nexmoe.com/
  - 还有书籍，始于外表，忠于文字。一个献给热爱思考者的博客主题
  - 一个分类, 一本书
- https://github.com/KiritoKing/hexo-theme-yet-the-books-custom /202211/js
  - 基于yet-the-books定制魔改的Hexo主题
  - 去掉了评论功能
  - 修复了试图读取Page Tags（只有Post才有Tags）的Bug

- https://github.com/HiNinoJay/hexo-theme-A4 /MIT/202401/js
  - https://ninojay.top/
  - 模仿A4纸张的一个hexo极简主题。主打一个简洁，体积小，配置少。

- https://github.com/zheli-design/hexo-theme-one-paper /MIT/202212/ejs
  - https://zheli.design/one-paper
  - 专注于写作，模拟纸张阅读感受的轻量 Hexo 主题
  - 响应式设计，兼容手机端、pad 端以及 PC 端；
  - 目前版本支持的模版页：首页、文章详情页、归档页、单页；
  - 无预留评论位置（后续可能会安排）。


- https://github.com/xaoxuu/hexo-theme-stellar /MIT/202402/js/ejs
  - https://xaoxuu.com/wiki/stellar/
  - https://xaoxuu.com/wiki/stellar/examples.html
  - 内置文档系统的简约商务风Hexo主题，支持大量的标签组件和动态数据组件。

- https://github.com/zalando-incubator/hexo-theme-doc /MIT/201903/js
  - https://zalando-incubator.github.io/hexo-theme-doc
  - A documentation theme for Hexo

- https://github.com/wujun234/hexo-theme-tree /MIT/202401/js/ejs
  - https://wujun234.com/
  - 一个简洁的主题，主要功能是 “树状导航” + “树状目录”，可选配“评论”和“阅读量”功能，支持基于搜索引擎的全站搜索。通过 fancybox 支持图片点击放大。

- https://github.com/SukkaW/hexo-theme-doku /MIT/201911/js
  - 专门为在 Hexo 上撰写文档而设计的主题
  - 未实现滚动时高亮toc中的标题
  - https://github.com/SukkaW/theme-doku-docs
    - The documents & demo of hexo-theme-doku

- https://github.com/PhosphorW/hexo-theme-academia /MIT/202005/js
  - https://phosphorw.github.io/
  - light & simple & responsive page for academic websites on Hexo

- https://github.com/iTimeTraveler/hexo-theme-hipaper /MIT/202011/js
  - https://itimetraveler.github.io/hexo-theme-hipaper/
  - A fashional newspaper theme for Hexo

- https://github.com/wzpan/hexo-theme-wixo /MIT/201701/js
  - http://wzpan.github.io/hexo-theme-wixo/
  - Turn your Hexo into a Wiki
  - hexo-tag-bootstrap = 0.0.8 (optional)

- https://github.com/theme-nexmoe/hexo-theme-nexmoe /apache2/202402/js
  - https://docs.nexmoe.com/
  - A special Hexo theme focusing on pictures and images.
# examples

# plugins

- https://github.com/alexbruno/hexo-generator-json-content /MIT/202003/js
  - plugin to generate a JSON file for generic use or consumption with the contents of posts and pages.
  - It's useful to serve compact and agile content data for microservices like AJAX site search, Twitter typeahead or public API.
- https://github.com/trudbot/hexo2json /MIT/202402/ts
  - Convert blogs in hexo to JSON format
  - Use parse to convert hexo style blog text into JSON.
  - Use stringify to convert the specified JSON format into a hexo blog.

- https://github.com/yscoder/hexo-generator-restful /MIT/201804/js
  - Generate restful json data for Hexo plugins.
  - https://github.com/tjwudi/hexo-generator-api /201512/js

- https://github.com/FrontendSophie/hexo-infinite-scroll /MIT/201907/ts
  - A fake infinite loading plugin for hexo.
  - Loaders are all generated through loaders.css by ConnorAtherton.

- https://github.com/dimaslanjaka/hexo-post-parser /202401/ts
  - Parse FrontMatter Markdown Posts To Javascript Object
  - support Parsing HexoJS/Jekyll/Hugo/Frontmatter
  - Get all images from post body and push them to metadata.photos

- https://github.com/unnamed42/hexo-spoiler /202402/ts
  - Hexo plugin for spoiler



- https://github.com/Cerallin/hexo-filter-text-autospace /GPLv3/202310/js
  - hexo 插件，用于在 CJK 字符与拉丁字符中间插入适当的间距。
  - 值得注意的是，并不直接插入一个半角空格，而是精确控制插入间距的宽度，像 Word 一样。
  - 本项目独立完成，但从 text-autospace.js 中汲取许多灵感，在此对 text-autospace.js 和 findAndReplaceDomText 的作者以及维护者表示感谢。

- https://github.com/hexojs/hexo-renderer-marked /MIT/202312/js
  - This plugin uses marked as its render engine.
  - By default, this plugin contains a potential security issue: It is possible to inject Markdown containing Unsafe HTML that will not be sanitized
  - solution is to migrate to `hexo-renderer-markdown-it` which is safe by default and does not suffer from the same limitations
- https://github.com/hexojs/hexo-renderer-markdown-it /MIT/202401/js
  - This renderer plugin uses Markdown-it as a render engine on Hexo
  - Support for Markdown, GFM and CommonMark

- https://github.com/CHENXCHEN/hexo-renderer-markdown-it-plus /MIT/202208/js/inactive
  - This renderer plugin uses Markdown-it as a render engine on Hexo.
  - This renderer plugin is forked from hexo-renderer-markdown-it. Add some plugins and support third-part markdown-it plugin.

- https://github.com/hexojs/hexo-renderer-pandoc /MIT/202310/js
  - A pandoc-markdown-flavor renderer for hexo.

- https://github.com/tea3/hexo-include-markdown /MIT/201709/js
  - This plugin for Hexo can easily load another markdown files in markdown file .

- https://github.com/bennycode/remark-hexo /MIT/202310/ts
  - A remark plugin to render Hexo's tag plugins. 
  - This plugin can be used with Astro, Gatsby, Docusaurus and all other frameworks that support remark plugins.

- https://github.com/hcoona/hexo-renderer-asciidoc /MIT/202106/js
  - Add support for Asciidoc. 
  - This plugin uses asciidoctor.js as render engine.

- https://github.com/kchen0x/hexo-reference /MIT/201907/js
  - A plugin to support markdown footnotes and Wiki-Style tooltip reference in your Hexo blog posts.
- https://github.com/LouisBarranqueiro/hexo-footnotes /MIT/201711/js
  - A plugin to support markdown footnotes in your Hexo blog posts
  - This plugin is no longer maintained, I recommend you to use hexo-renderer-markdown-it which supports footnotes and many more features.

- https://github.com/njzjz/hexo-tag-publications /202402/js
  - creates a publication list. 
  - you need to create a bib file at source/_data/pub.bib
- https://github.com/Aetf/hexo-next-publist
  - A publication list tag plugin for theme-next

- https://github.com/hexojs/hexo-math /MIT/202008/js
  - A hexo plugin that uses MathJax to render math equations.
  - Embed `KaTeX` and `MathJax` in Hexo post/page via tag plugins. 
  - Equations are rendered in Hexo (server-side), so browser-side javascript library is not needed and should be removed.
  - hexo-math uses tag plugin approach due to minor incompatibility between LaTeX and marked, the default markdown renderer of Hexo (via hexo-renderer-marked).
- https://github.com/next-theme/hexo-filter-mathjax /MIT/202211/js/inactive
  - Server side MathJax Renderer Plugin for Hexo.

- https://github.com/lavas-project/hexo-pwa /MIT/202003/js
  - Progressive Web Apps (PWA) plugin for Hexo.
- https://github.com/uiolee/hexo-workbox-build /MPLv2/202402/ts
  - A hexo plugin to run workbox-build and provide convenient features of PWA and service worker.
  - This plugin doesn't provide PWA support ready out of the box.
- https://github.com/EmptyDreams/hexo-swpp /AGPLv3/202402/ts
  - 这是 swpp-backends 的 hexo 端实现，绝大多数功能由 swpp-backends 提供。
  - https://github.com/EmptyDreams/swpp-backends
    - swpp-backends（以下简称 swpp）插件的功能是为网站生成一个高度可用的 ServiceWorker（以下简称 SW），为网站优化二次加载、提供离线体验、提高可靠性，并为此附带了一些其它的功能。

- https://github.com/bubkoo/hexo-toc /MIT/201708/js
  - Insert a markdown TOC(Table Of Content) before posts be rendered.
  - Unlike the native toc helper, this plugin will inject a TOC only when a placeholder(<!-- toc -->) found in the raw markdown files. And the TOC will be injected after the placeholder.
  - All you need to do is placing a placeholder(<!-- toc -->) in your post when and where needed.

- https://github.com/hinastory/hexo-oembed /MIT/201902/js
  - Embed oEmbed item on your Hexo article.
  - Automatic Embed.ly fallback when an API key is provided

- https://github.com/Cyrusky/hexo-backlink /MIT/202209/js
  - This plugin is for transfer Obsidian-type backlink to standard hexo in-site post link.
  - A plugin to convert backlink in .md file to in-site link.
  - Can not convert link include tags, it will ignore the tags
- https://github.com/pondered/hexo-obsidian-backlink /202311/js
  - This plugin is for transfer Obsidian-type backlink to standard hexo in-site post link.
  - 根据 obsidian 中的 双链 指向具体的文件包括附件的链接
  - 本插件理论上支持 所有 wiki 链接以及 markdown 链接 `[[dd]]`/[[aa.png]]
  - obsidian 中的所有文件尽量放到 _posts 文件夹下，本插件仅读取 posts 中的内容

- https://github.com/minamo173/hexo-tag-link-preview /MIT/202201/js
  - Embed a link preview on your Hexo article.

- https://github.com/OrangeX4/hexo-link-card /MIT/202210/js
  - 使用现有 Markdown 语法将链接转换为卡片式链接（网页卡片）
  - 许多平台，例如 Bilibili，知乎，微信公众号等平台，均有将链接转换为卡片式链接的功能，如果能在书写 Markdown 阶段，就将卡片式链接的书写考虑进去，能给后续发布带来很大的便利

- https://github.com/viko16/hexo-permalink-pinyin /MIT/201905/js
  - A Hexo plugin which convert Chinese title to transliterate permalink.

- https://github.com/hvnobug/hexo-external-link /202006/js
  - 跳转外链相关插件。自动为所有html文件中外链的a标签生成对应的属性。 
  - 比如 设置 target='_blank', rel='external nofollow noopener noreferrer' 告诉搜索引擎这是外部链接, 不要将该链接计入权重。 同时自动生成外链跳转页面, 默认在根目录下go.html; 

- https://github.com/uiolee/hexo-absolute /MPLv2/202402/js
  - convert relative path to absolute URL for hexo

- https://github.com/sergiolepore/hexo-broken-link-checker /BSD/201602/js
  - This is a hexo plugin which detects links that don't work, missing images and redirects.

- https://github.com/dimaslanjaka/hexo-shortcodes /MIT/202306/ts
  - Hexo shortcodes helper. 
  - Various shortcodes for hexo, adapted from jekyll.
  - Firsly, remove old original tag renderer. Because this plugin already have all default tag (vimeo, youtube, gist, codeblock)

- https://github.com/chekun/hexo-excerpt /MIT/202201/js
  - Automatic excerpt generator for Hexo
  - This plugin runs through all your posts, if your post has more than the configured number of direct tags, then they will be the excerpt, otherwise the whole post will be used.
  - https://github.com/ashisherc/hexo-auto-excerpt /201710/js
- https://github.com/rootlexme/hexo-ai-excerpt /202310/js
  - 使用ai为您的文章生成摘要

- https://github.com/sisyphsu/hexo-enhancer /MIT/202110/js
  - enhancement plugin for Hexo.
  - Auto generate title by filename.
  - Auto generate date by filename, like Jekyll.
  - Auto generate categories by filepath.

- https://github.com/sergeyzwezdin/hexo-related-posts /MIT/202005/js
  - Hexo plugin that generates related posts list with TF/IDF algorithm
  - The plugin scans all posts on the website and extracts words for every post.
  - TF/IDF is calculated for every post.
  - https://github.com/vfasky/hexo-summarizer /201305/coffeescript

- https://github.com/tea3/hexo-related-popular-posts /MIT/202008/js
  - plugin that generates a list of links to related posts and popular posts. 
  - Sort and extracted by relevance of tags and word relevance of contents.
  - this plugin can get Visitor Counts (PV) on posts. Gets and displays the Google Analytics page view.

- https://github.com/huiwang/hexo-recommended-posts /AGPLv3/202011/js
  - 跨博客文章推荐插件
  - 此插件借助人工智能为友情链接升级换代，通过文章推荐的方式帮助大家推广博客。它从推荐引擎里获取文章推荐列表，列表里既有您博客的内部文章链接，也有使用此服务的其他博主的外部链接，自动，精准，公平的实现文章互推。

- https://github.com/hexojs/hexo-generator-category /MIT/201909/js
  - Category generator for Hexo.
- https://github.com/hexojs/hexo-generator-tag /MIT/201906/js
  - Tag generator for Hexo.

- https://github.com/xu-song/hexo-auto-category /MIT/202312/js
  - Hexo plugin, which generates categories automatically from folder structure for each post.
  - As a Hexo user, you must be troubled with front matter setting for each post. With this plugin, you don't need to set categories one by one. hexo-auto-category generates static post categories automatically based on `directory/folder` name.
- https://github.com/zthxxx/hexo-directory-category /MIT/202005/js
  - Automatically add front-matter categories to Hexo article according to the article file directory.

- https://github.com/prinsss/hexo-hide-posts /MIT/202308/js
  - 本 Hexo 插件可以在博客中隐藏指定的文章，并使它们仅可通过链接访问。
  - 当一篇文章被设置为「隐藏」时，它不会出现在任何列表中（包括首页、存档、分类页面、标签页面、Feed、站点地图等），也不会被搜索引擎索引（前提是搜索引擎遵守 noindex 标签）。
  - 只有知道文章链接的人才可以访问被隐藏的文章。
  - This post will not be shown anywhere, but you can still access it by https://hexo.test/lorem-ipsum/. (If you want to completely prevent a post from rendering, just set it as a draft.)

- https://github.com/HCLonely/hexo-calendar /MIT/202304/js
  - Insert a calendar like Github contributions into your blog.
  - Use the `git log -1 --date=iso --pretty=format:"%ad"` command in the blog root directory to output a date.

- https://github.com/Zfour/hexo-github-calendar /202103/js
  - https://zfour.github.io/hexo-github-calendar/
  - 基于hexo的github calendar贡献插件

- https://github.com/ren-34/hexo-filter-gitcalendar-pro /202310/js
  - 对原hexo-filter-gitcalendar插件的升级
  - 新增功能：git 提交日历 可以跟随主题模式进行变化。
  - https://www.npmjs.com/package/hexo-filter-gitcalendar

- https://github.com/maxchang3/hexo-markmap /MIT/202311/js
  - plugin insert mindmap in your hexo blog by markmap. 
  - From now all the syntax like HTML codes, links, inline code, markdown KaTeX, and Codeblocks are possible to use.

- https://github.com/stringbean/hexo-image-toolkit /apache2/202312/js
  - Hexo tag plugin for converting & resizing images and generating associated markup.
  - By default, the size of the input image is used for both the WEBP and fallback images.

- https://github.com/yiyungent/hexo-asset-img /MIT/202212/js
  - 本地图片插件: 转换 图片相对路径 为 asset_img
  - 本地图片 与 文章在一个文件夹, 易打包, 在无网络或网络较差时也能预览
  - https://github.com/yiyungent/clear-image-action
    - 自动清理无用冗余垃圾图片,无需再手动管理图片, 清除无用图片。

- https://github.com/cocowool/hexo-image-link /202402/js
  - 将Markdown语法的图片路径转换为asset_img的方式，使图片能够在使用typora编辑和hexo预览发布时都能正常显示。
  - 网上很多资料提示使用 hexo-asset-image 插件，但是在 hexo 4.2.0 环境下，生成的路径不对

- https://github.com/poacher2k/hexo-featured-image /MIT/202003/js
  - A Hexo plugin to allow adding featured images with featured_image in front-matter and using it in post and/or have it output in the content.json if used together with hexo-generator-json-content.
  - thumbnail is also supported, and works the same as featured_image.

- https://github.com/Troy-Yang/hexo-lazyload-image /MIT/202210/js
  - plugin which is used to have all images support lazyload automatically
  - All the lazy-load images only shows up when they are within current viewport.
  - Don't worry about lazyload SEO problem, because Google supports it already.

- https://github.com/hexojs/hexo-filter-lqip /MIT/202401/js/效果差
  - plugins which helps to introduce low quality image placeholders to the theme

- https://github.com/SpiritLingPub/hexo-images-watermark /LGPLv3/202203/js
  - hexo 开发的本地图片水印插件

- https://github.com/hexojs/hexo-filter-responsive-images /MIT/202103/js
  - Generate mutliple versions of images for responsive blogs using Hexo >= 3.x. 
  - It uses sharp library to transform images.
- https://github.com/ottobonn/hexo-image-sizes /202105/js
  - Generate multiple images sizes (thumbnail, body, etc.) for each source image in Hexo

- https://github.com/fletchto99/hexo-sliding-spoiler /MIT/201912/js
  - A sliding spoiler for hexo

- https://github.com/u2sb/hexo-tag-mmedia /apache2/202307/ts
  - hexo插入aplayer、meting、dplayer、bilibili、哔哩哔哩、西瓜视频 标签
  - 0.x 版本开发的时候受到 hexo-tag-dplayer 和 hexo-tag-aplayer 影响较大，为了兼容配置方式做了很多妥协，越到后面维护起来越麻烦，决定开发 1.x 版本，推翻重来

- https://github.com/timnew/hexo-tag-codepen /MIT/201604/js
  - Hexo tag to embed code snippet from CodePen

- https://github.com/crimx/hexo-filter-github-emojis /MIT/202204/js
  - A Hexo plugin that adds emoji support, using Github Emojis API.
  - Enable `::` emoji parsing. If off the tag and helper still work.
  - `<span class="github-emoji"><span>&#x2728;</span>`

- https://github.com/D0n9X1n/hexo-tag-cloud /MIT/202101/js
  - just another tag cloud plugin for hexo.

- https://github.com/next-theme/hexo-word-counter /LGPLv3/202308/js/rust
  - Word count and time to read for articles in Hexo blog.
  - The word count is based on Unicode® Standard Annex #29. Thus, when multiple languages are present in the post content, the total word count can be accurately counted.
  - With the power of Rust, this plugin is faster than almost all other Hexo plugins that offer similar functionality. 

- https://github.com/willin/hexo-wordcount /201809/js
  - A Word Count Plugin for Hexo

- https://github.com/theme-next/hexo-symbols-count-time /MIT/202004/js
  - Symbols count and time to read for articles in Hexo blog.
  - Better than hexo-reading-time and faster than hexo-wordcount. No external dependencies.
- https://github.com/uiolee/hexo-symbols-count-time-2 /LGPLv3/202402
  - a fork of hexo-symbols-count-time

- https://github.com/superalsrk/hexo-pdf /201612/js
  - Hexo tag for embedded pdf

- https://github.com/yscoder/hexo-helper-qrcode /MIT/201612/js
  - QRcode for Hexo helper plugins.

- https://github.com/Aetf/hexo-prism-plus /BSD/202112/js
  - Better code block highlighting with Prism for Hexo.
  - Note: this plugin uses server-side rendering combined with client-side hydration, and thus it ships with its own copy of prismjs. 

- https://github.com/ludoviclefevre/hexo-generator-seo-friendly-sitemap /MIT/202012/js
  - Generate SEO-friendly sitemap.
  - Inspired by XML Sitemap in Yoast Wordpress SEO Plugin 
  - It will generate separated sitemap files for pages, posts, categories, tags and a XSL stylesheet.

- https://github.com/JLHwung/hexo-offline /MIT/202103/js
  - intended to provide offline experience for hexo built static website. 
  - It uses `ServiceWorker` under the hood. 
  - Simply install this plugin to your website and it should be offline ready by caching most of static assets.

- https://github.com/theme-particlex/hexo-helper-crypto /MIT/202310/js
  - 用于在模板文件内加/解密数据，使用 Crypto-js。

- https://github.com/edolphin-ydf/hexo-encrypt /201806/js
  - encrypt the content of a post
  - If you want to make a permission for one post, (eg:enter an password to view the content)

- https://github.com/next-theme/hexo-optimize /MIT/202211/js/rust
  - A Hexo plugin that optimize the pages loading speed
  - It will automatically filter your html file, find the `<link rel="stylesheet">` tag and make optimizations on demand

- https://github.com/theme-next/hexo-filter-optimize /MIT/202003/js
  - A hexo plugin that optimize the pages loading speed.

- https://github.com/mamboer/hexo-filter-cleanup /MIT/201905/js
  - All in one. Minifier & Optimization plugin for Hexo
# utils
- https://github.com/hexojs/hexo-generator-alias /MIT/202009/js
  - Generates alias pages for redirecting to posts, pages or URL.

- https://github.com/xcatliu/hexo-filter-date-from-git /201610/js
  - Read git log and overwrite the front-matter properties date and updated for each posts.
  - WARNING: This plugin will overwrite the front-matter, even if you manually set a date or updated in the front-matter.

- https://github.com/kuole-o/hexo-tag-map /apache2/202402/js
  - https://blog.guole.fun/map/
  - 给你的 Hexo 文章插入交互式地图
  - 支持GoogleMap、高德地图、百度地图、Geoq地图、openstreetMap常规地图+卫星地图+卫星标注地图！一个强大的地图插件。
  - 支持各个地图缩放等级配置+经纬度配置+地图容器宽高配置+默认展示地图类型配置
  - Butterfly已验证，其他Hexo主题，欢迎体验

- https://github.com/GC-ZF/hexo-hot-article /apache2/202402/python
  - http://hexo-hot-article.vercel.app/
  - Hexo博客热门文章实时排序
  - 关于网站统计平台的选择，第一想到的是51la
  - 综合考虑，使用百度统计实现文章排行及访客地图

- https://github.com/flytam/CsdnSyncHexo /MIT/202304/ts
  - 一键同步csdn/博客园/掘金/segmentfault/腾讯云加社区/github文章生成hexo源文件

- https://github.com/LetTTGACO/elog /MIT/202401/ts
  - https://elog.1874.cool/
  - Markdown 批量导出工具、开放式跨平台博客解决方案
  - 随意组合写作平台(语雀/飞书/Notion/FlowUs)和部署平台(Hexo/Vitepress/Halo/Confluence/WordPress等)
  - Elog支持了在生成MD文件之前，将扫描到的图片上传到图床上，并对文档中的图片链接进行替换。 当前支持的图床有： 本地/阿里云oss/腾讯云cos/Github图床
  - https://github.com/LetTTGACO/elog-docs
    - Elog 的使用文档
  - https://github.com/elog-x/notion-hexo
    - Notion + Elog + Hexo + GitHub Actions + Vercel 博客解决方案

- https://github.com/mark-magic/mark-magic /MIT/202402/ts
  - https://mark-magic.rxliuli.com/
  - 一个基于 markdown 的数据连接与转换工具，解决不同工具之间数据转换以及部分常用工具之间的协调。
  - joplin => hugo 生成 blog
  - https://github.com/rxliuli/joplin-blog /archived

- https://github.com/kscript/markdown-download /MIT/202401/js
  - 谷歌浏览器插件: 将掘金、知乎、思否、简书、博客园、微信公众号、开源中国、CSDN的文章转为markdown文档并下载

- https://github.com/winniesi/obsidian-hexo-blog /202402/js
  - 通过 obsidian git 插件将文章备份到了 github 上面（介绍），现在的目标是将托管在 GitHub 上面 obsidian blog 目录下面的内容自动同步到 GitHub Hexo，然后就可以通过 vercel 等服务自动部署。（教程不包括自动部署的部分）
  - https://github.com/Chivier/obsidian2hexo /python

- https://github.com/lifeodyssey/obsidian-hexo-auto-update /MIT/202311/ts
  - The Obsidian-Hexo Integration plugin allows you to monitor changes in your Obsidian vault, specifically the `_posts` folder, and automatically commit and push them to your Hexo blog repository, without set up local node.js environment and accelerate the speed from writing to publication.

- https://github.com/meixg/notion-to-hexo /202402/ts
  - notion database to hexo pages

- https://github.com/estruyf/vscode-front-matter /MIT/202312/ts
  - https://frontmatter.codes/
  - Front Matter is a CMS running straight in Visual Studio Code. 
  - Can be used with static site generators like Hugo, Jekyll, Hexo, NextJs, Gatsby, and many more
  - Preview your site/content straight in Visual Studio Code

- https://github.com/serverless/post-scheduler /201703/js
  - The post scheduler is a serverless project that gives static site owners the ability to schedule posts (or other site content).
  - It works with any static site setup (Jekyll, Hugo, Phenomic, Gatsby etc.)

- https://github.com/TechQuery/Web-fetch /202306/ts
  - Hexo Migrator plugin for common Web pages
# alternatives-hexo
- https://github.com/EasyWebApp/MarkCell /202202/ts
  - General MDX to TSX/HTML converter, inspired by Hexo & Gatsby
  - https://github.com/EasyWebApp/mark-wiki
    - Web-site scaffold based on BootCell, MarkCell & Parcel, is a Static Web-site Generator like Hexo & Gatsby.
  - https://github.com/EasyWebApp/BootCell-document
    - Re-implemented Official Web-site of BootStrap based on WebCell, BootCell & MarkCell

- https://github.com/web-infra-dev/rspress /MIT/202402/ts/mdx
  - https://rspress.dev/
  - A fast Rspack-based static site generator
  - 依赖rsbuild、@rspress/mdx-rs、@mdx-js/react、@loadable/component、flexsearch、remark-rehype
  - Built-in Full Text Search: Automatically generates a full-text search index during building process
  - Static Site Generation: it automatically builds into static HTML files, which can be easily deployed anywhere
  - Providing a plugin system, you can customize the build process and theme according to your needs
# more
- https://github.com/statichunt/statichunt /MIT/202402/js
  - https://statichunt.com/
  - a free open-source Jamstack directory that lists hundreds of themes, starters, and resources for static sites.
  - 依赖next-mdx-remote、marked、react-infinite-scroll-component
