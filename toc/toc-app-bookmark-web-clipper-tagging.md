---
title: toc-app-bookmark-web-clipper-tagging
tags: [bookmark, tag, toc, web-clipper]
created: 2022-11-04T15:09:05.417Z
modified: 2022-11-11T11:04:29.007Z
---

# toc-app-bookmark-web-clipper-tagging

# guide

- tips
  - 重内容和搜索, 轻标签和管理
  - 标签管理 / clipper 通常作为产品的一个功能，而不是独立的产品
  - 主流的 CMS/多维表格 都提供了管理文章/链接的能力, 特别是搜索能力
  - 偏向 marking/cliper, 还是偏向 archiving/crawler/归档为文件, 或偏向 read-it-later

- tags vs folder
  - ❓ subpage 可以替代 nested-tags
  - 常见方案: 默认显示最近文件记录(即分页的所有文件), 点击MyDocs实际显示的是包含文件夹的collection, 文件夹名不展示为tags，点击Tag实际显示单层扁平文件，两者的实现逻辑可复用

- who is using #tags
  - mkdocs-material, nested
  - paperless-ngx, nested
  - papermerge, 非嵌套
  - archivebox
  - linkding, 非嵌套
  - wallabag, 非嵌套

- who is using #folders/subdocs
  - lasuite-docs
  - outline
  - filebrowser
# popular
- web-clipper /4.7kStar/GPLv2/202208/ts
  - https://github.com/webclipper/web-clipper
  - https://clipper.website/
  - use Web Clipper to save anything on the web to anywhere.
  - 支持收藏链接、选区文字
  - 支持
    - flowus、wolai、语雀、有道、flomo
    - notion、github、onenote、joplin
  - https://chrome.google.com/webstore/detail/web-clipper/mhfbofiokmppgdliakminbgdgcmbhbac

- https://github.com/pfcao/abookmark /202311/js
  - https://www.abookmark.org/
  - Advanced bookmark manager comes with labels, sticky notes, and trash mode.
  - Abookmark uses the native bookmarks as its database and it has some advanced features as labels, sticky notes, and trash mode
  - 基本复刻了chrome bookmark manager的功能
  - 支持list/grid视图

- https://github.com/sissbruecker/linkding /10.3kStar/MIT/202602/python/django
  - https://linkding.link/
  - https://demo.linkding.link/
  - Self-hosted bookmark manager that is designed be to be minimal, fast, and easy to set up using Docker.
  - Organize bookmarks with tags
  - Bulk editing, Markdown notes, read it later functionality
  - Share bookmarks with other users or guests
  - Automatically archive websites, either as local HTML file or on Internet Archive
  - Import and export bookmarks in Netscape HTML format
  - Installable as a Progressive Web App (PWA)
  - Admin panel for user self-service and raw data access
  - [feature request: categorizing bookmarks _202206](https://github.com/sissbruecker/linkding/issues/285)
    - Is it possible to add a feature that allows grouping multiple bookmarks in a folder-like structure? I currently only the see possibility to remotely emulate this feature by using tags, but that feels kind of clunky for that use-case.
    - I'll probably not support folders, I might consider lists or some other type of collection if some concrete use-cases come up. It would be helpful to know why tags are not sufficient for categorization for specific use-cases.
    - basically allow manual grouping of tags into groups / categories, instead of having them grouped alphabetically.
    - One way to implement this feature could be using what is called namespace or category tags. It's not a parent tag and is flat. In fact GitHub uses these. For example you can search language:rust and get a result of all the repositories that use the Rust language.
    - I like the way Obsidian does tags, with a nested hierarchical structure.
  - [Feature request: Partial tag search _202506](https://github.com/sissbruecker/linkding/issues/1103)
  - 🍴 forks
  - https://github.com/WooHooDai/linkding-cn /MIT
    - 中文本地化、功能增强、界面优化。
    - 支持🎲随机排序、📅日期筛选、🐞自定义快照脚本、♻️回收站等丰富功能，拥有搜索栏&侧边栏随屏滚动、侧边栏折叠、独立滚动条、位置&折叠状态记忆等界面优化。

- https://github.com/ArchiveBox/ArchiveBox /27.1kStar/MIT/202603/python/ts
  - https://archivebox.io/
  - self-hosted internet archiving solution to collect, save, and view websites offline.
  - Use ArchiveBox as a command-line package and/or self-hosted web app on Linux, macOS, or in Docker.
    - Once installed, you can interact with it through the: Browser Extension, CLI, self-hosted web interface, Python API, or filesystem.
    - You can feed ArchiveBox URLs one at a time, or schedule regular imports from your bookmarks or history, social media feeds or RSS, link-saving services like Pocket/Pinboard, our Browser Extension, and more.
  - It saves snapshots of the URLs you feed it in several redundant formats.
    - Saves all pages to archive.org as well by default for redundancy (can be disabled for local-only mode)
  - ArchiveBox uses standard tools like Chrome, wget, & yt-dlp, and stores data in ordinary files & folders. (no complex proprietary formats, all data is readable without needing to run ArchiveBox)
  - Powerful CLI with modular dependencies and support for Google Drive/NFS/SMB/S3/B2/etc.
  - Extracts a wide variety of content out-of-the-box: media (yt-dlp), articles (readability), code (git), etc.
  - Uses standard, durable, long-term formats like HTML, JSON, PDF, PNG, MP4, TXT, and WARC
  - Planned: support for running JS during archiving to adblock, autoscroll, modal-hide, thread-expand
  - [twitter/x posts not captured - screenshots taken before the post is fully loaded _202408](https://github.com/ArchiveBox/ArchiveBox/discussions/1490)
    - That's normal for big tech social media sites, that's why we use a ton of different methods to capture redundantly, usually a few will fail but others will work.
  - [Architecture: Support organizing archived links with folders or tags _201906](https://github.com/ArchiveBox/ArchiveBox/issues/247)
    - 202104: Tags have been around for a few versions. I don't think we'll natively support hierarchical tags anytime soon, but you can use slashes or dashes to indicate categories in your tag names somecategory/somesubcategory/sometag (similar to how gmail tagging works).

- https://github.com/floccusaddon/floccus /7.8kStar/MPLv2/202603/ts/js/vue
  - https://floccus.org/
  - Sync your bookmarks privately across browsers and devices
  - Syncs your real, native browser bookmarks directly
  - Sync via Nextcloud Bookmarks, Google Drive or any WebDAV-compatible service
  - Install the floccus Android app to access your bookmarks on your phone
  - (eventual) consistency is more important than intention preservation

- https://github.com/pawelmalak/flame /MIT/202307/ts/inactive
  - Flame is self-hosted startpage for your server. inspired (heavily) by SUI.
  - Easily manage your apps and bookmarks with built-in editors.
  - Sequelize ORM + SQLite
  - Redux + react

- https://github.com/kormyen/memex /202210/js
  - https://kormyen.github.io/memex/
  - Simple bookmarks and notes. Memex is a personal knowledge base.
  - 卡片形式

- https://github.com/WorldBrain/Memex /4.2kStar/MIT/202311/ts
  - https://worldbrain.io/
  - Browser extension to curate, annotate, and discuss the most valuable content and ideas on the web
  - Its name and functionalities are heavily inspired by Vannevar Bush's vision of a Memex.

- https://github.com/zotero/zotero /8.6kStar/AGPLv3/202401/js
  - https://www.zotero.org/
  - a free, easy-to-use tool to help you collect, organize, cite, and share your research sources.
  - Zotero is built on Firefox and depends on many other exceptional open-source projects:
    - [ace](https://ace.c9.io/)
    - Monaco Editor
    - ProseMirror
    - pdf.js
    - katex
    - Citation Style Language
    - epub.js
  - https://github.com/windingwind/zotero-better-notes /AGPLv3/202401/ts
    - Everything about note management. All in Zotero.

- https://github.com/alyssaxuu/omni /MIT/202207/js/inactive
  - The all-in-one tool to supercharge your productivity
  - With Omni you can use your browser like a pro. 
  - Manage tabs, bookmarks, your browser history, perform all sorts of actions and more with a simple command interface.
# web-clipper
- maoxian-web-clipper /596Star/MIT/202209/js
  - https://github.com/mika-cn/maoxian-web-clipper
  - A web extension to clip information from web page.
  - All file will save in local hard disk, you can control your data totally

- https://github.com/deathau/markdownload /apache2/202312/js
  - an extension to clip websites and download them into a readable markdown file. 
  - Turndown is used to convert the simplified HTML (from Readability.js) into markdown.

## known-clipper

- https://github.com/coddingtonbear/obsidian-web /ts
  - You can use Obsidian Web for sending any web content from Chrome to your Obsidian Notes easily by just clicking on a button in your toolbar.
  - use Obsidian Local REST API
  - https://github.com/SettingDust/obsidian-web-clipper
  - https://github.com/ganesshkumar/obsidian-bookmarklet-maker

- https://github.com/OneNoteDev/WebClipper /ts
  - The OneNote Web Clipper extension

## open-web-clipper

- https://github.com/zadam/trilium-web-clipper /js
  - allows user to clip text, screenshots, whole pages and short notes and save them directly to Trilium Notes.
  - Some parts of the code are based on the Joplin Notes browser extension.
  - The extension needs to connect to a running Trilium instance. 
    - By default, it scans a port range on the local computer to find a desktop Trilium instance.

- https://github.com/snowyu/h2doc.js
  - Process html to a specified format document(markdown currently), build-in Joplin Web Clipper Server for Joplin Web Clipper

- https://github.com/owenschoppe/Citable
  - The open source codebase for Citable, a Google Chrome Extension for saving quotes and notes from the web into Google spreadsheets.

- QOwnNotes Web Companion
  - https://chrome.google.com/webstore/detail/qownnotes-web-companion/pkgkfnampapjbopomdpnkckbjdnpkbkp?hl=en
  - a companion extension for QOwnNotes to interact with the note taking desktop application.
  - To use this extension QOwnNotes needs to be running.

- https://github.com/tagspaces/browser-extensions
  - https://www.tagspaces.org/products/webclipper/
  - TagSpaces Web Clipper for Chrome and Firefox

- https://github.com/butterops/refer /202105/js/inactive
  - Cross browser web clipper. Takes video notes, screenshots and extract texts or images from supported web br
# bookmark
- https://github.com/itizaworld/webev /202303/ts/archived
  - https://github.com/itizaworld/webev-server
  - https://www.youtube.com/watch?v=EmxXCfOtgMU
  - bookmark manager that improves the organization of information.
  - 依赖express、mongoose、passport、next12、nextui、swr
  - organized in a hierarchical structure.
    - 只支持文件夹，？是否支持标签
  - Visually display the information obtained by ogp.
    - 输入url，自动显示预览图

- https://github.com/hoarder-app/hoarder /AGPL/202503/ts
  - https://hoarder.app/
  - A self-hostable bookmark-everything app (links, notes and images) with AI-based automatic tagging and full text search
  - Automatic fetching for link titles, descriptions and images.
  - Full text search of all the content stored.
  - AI-based (aka chatgpt) automatic tagging. With supports for local models using ollama
  - OCR for extracting text from images.
  - An iOS app, and an Android app.

- https://github.com/Daniel31x13/linkwarden /MIT/js/代码简单
  - https://github.com/linkwarden/linkwarden
  - a self-hosted, open-source bookmark + archive manager to collect, and save websites for offline use.
  - 依赖mongodb、puppeteer、react-select
  - LinkWarden also saves a copy of the link as screenshot and PDF
  - Auto-capture a screenshot and PDF from each website.
  - Set multiple tags to each link.

- https://github.com/ndom91/briefkasten /MIT/202401/js/prisma/样式友好
  - Self-hosted bookmarking application. 
  - Works with any Prisma compatible database 
  - 依赖prisma、NextAuth.js
  - api基于pages/api
  - Organise by categories and tags
  - Save by Browser Extension
  - Import and export bookmarks from standard HTML format
  - Bookmark image fetching background job
  - Fulltext search，测试异常？
  - REST API
  - https://github.com/ndom91/briefkasten-scrape
    - Job to periodically fetch missing bookmark screenshot cover photos. 
    - This Github Action uses Playwright to periodically fetch missing screenshots of saved Bookmarks.

- https://github.com/nthiebes/booky.io
  - Online bookmark manager with a focus on simplicity, customizability, privacy, and speed.
  - booky.io + Atomic Design + BEM + React + Redux

- https://github.com/net-runner/lynx
  - https://lynxweb.vercel.app/
  - Open source platform for sharing, managing and discovering links and bookmarks
  - Database: PostgresSQL & Prisma as a ORM
  - Frontend: Next.js
  - Backend: Node.js + Hyper-Express
  - Mobile: React-Native
  - Link sharing, discovery, managing, observing link groups or users

- https://github.com/linkwarden/linkwarden /AGPLv3/202401/ts
  - https://linkwarden.app/
  - Self-hosted collaborative bookmark manager to collect, organize, and preserve webpages and articles.
  - 依赖headlessui、zustand、@mozilla/readability、prisma、nextjs、next-auth
  - Linkwarden also saves a copy of each webpage as a Screenshot and PDF
  - designed with collaboration in mind, sharing links with the public and/or allowing multiple users to work together

- https://github.com/kanishka-linux/reminiscence /AGPLv3/202401/python/js
  - Self-hosted Bookmark and Archive manager

- https://github.com/bdTechies/book-manager /201901/js
  - https://book-manager.bdtechies.com/
  - cross-platform desktop app to manage personal library.

- https://github.com/osmoscraft/osmosmemo
  - Turn GitHub into a bookmark manager
  - A browser bookmark manager optimized for capture and retrieval speed.
  - Extract page title and url into a short markdown snippet.

- https://github.com/geekape/geek-navigation /MIT/202109/ts/vue/前端+后端+管理后台
  - 极客猿导航－独立开发者的导航站
  - 前台采用的 Vue 全家桶，服务端使用的框架是 Express，数据库是 Mongodb。
  - Vue动态导航是采用的单页面方式，非常不利于 SEO 优化，所以改用了 Nuxt SSR 的方式，这也是这个版本最大的改动。
  - V3.0版本，最大的改动就是把项目拆分为三个子项目: Nuxt后台 -> Ant Design Pro后台, Express -> Eggjs
  - [强烈推荐建议适配chrome书签json结构，方便一键导出生成](https://github.com/geekape/geek-navigation/issues/101)

- https://github.com/codeverland/codever
  - Bookmarks and Snippets Manager for Developers & Co
  - frontend uses with Angular and Angular CLI.
  - backend uses ExpressJS with MongoDB and Keycloak. OpenAPI

- https://github.com/go-shiori/shiori /11kStar/MIT/202509/go/js/vue/inactive
  - bookmark manager built with Go
  - Intended as a simple clone of Pocket. 
  - You can use it as a command line application or as a web application. 
  - 依赖httprouter、sqlx、go-sqlbuilder、goquery
  - Support for sqlite3, PostgreSQL, MariaDB and MySQL as its database.

- https://github.com/clebert/bookmark.wtf
  - A free and open-source bookmark manager that uses GitHub Gist as database.

- https://github.com/helloxz/onenav
  - 使用PHP + SQLite 3开发的书签管理系统，将浏览器书签集中式管理，做到一处部署，随处访问。

- https://github.com/poulainv/tottem /202005/ts/inactive
  - Bookmark manager on steroid built with React / NextJs / Apollo Tools / Prisma 2

- https://github.com/nextcloud/bookmarks
  - This app provides you with a web interface for collecting and organizing bookmarks to the places on the web that are precious to you.
  - Sort bookmarks into folders
  - Add tags and personal notes

- https://github.com/serogbp/startpage-react
  - https://serogbp.github.io/startpage-react/
  - a Kanban-like bookmark manager 
- https://github.com/serogbp/Startpage
  - a kanban like page where you can save and organize your favorite websites. 
  - The websites are stored in the browser's Local Storage and they can be exported/imported in JSON format.
  - Developed using vanilla Javascript with the MVC pattern and Custom Elements.

- https://github.com/ivasilov/wikid
  - Wikid is an app for keeping your personal information organized. 
  - It organizes your bookmarks in a wiki format.
  - NestJS, Apollo, TypeORM

- https://github.com/Pintree-io/pintree /2.6kStar/MIT/202501/ts/inactive
  - https://app.pintree.io/
  - Pintree 是一个开源项目，旨在将浏览器书签导出成导航网站
  - 将书签文件转换成JSON格式, 生成静态导航网站
  - 使用插件导出浏览器书签，并保存 JSON 文件到本地。替换 JSON 文件

- https://github.com/raphaelsty/knowledge /GPL/202603/python
  - https://raphaelsty.github.io/knowledge/
  - Open-source personal bookmarks search engine
  - It fetches content you interact with from various platforms—GitHub, HackerNews, Zotero, HuggingFace likes, X/Twitter—and organizes it into a navigable knowledge graph.

## read-it-later

- https://github.com/omnivore-app/omnivore /16kStar/AGPL/202601/ts
  - https://omnivore.app/
  - open source read-it-later solution for people who like reading
  - Offline support
  - 依赖nextjs、swr、stitches、mozilla-readability、radix-ui、pdfjs
  - Web app written in Node.js and TypeScript; android/ios
  - Browser extensions for Chrome, Safari, Firefox, and Edge
  - Add newsletter articles via email (with substack support!)
  - Every single part is fully open source! deploy it to your own server.

- https://github.com/wallabag/wallabag /12.6kStar/MIT/202603/php
  - https://wallabag.org/
  - a self hostable application for saving web pages: Save and classify articles. Read them later. Freely.

## offline

- https://github.com/dosyago/DiskerNet /js
  - An internet on yer disk. Full text search archive from your browsing and bookmarks.
  - Two modes: archive everything or only bookmark-worthy content

- https://github.com/kanishka-linux/reminiscence /AGPLv3/202401/python/js
  - Self-hosted Bookmark and Archive manager
  - Directory based categorization of bookmarks
  - Automatic Tagging and Summarization, implemented using NLTK library

- https://github.com/akawashiro/jendeley
  - a JSON-based document organizing software.
  - the database is stored as a plain text JSON file, making it easily editable using your preferred editor. 

## bookmark-manager-as-browser-extension

- https://github.com/danny0838/webscrapbook
  - a browser extension that captures the web page faithfully with various archive formats and customizable configurations, for future retrieval, organization, annotation, and editing.

- https://github.com/ips21blank/offlinebookmarkmanager
  - Bookmark manager/editor extension for chrome browsers
  - written in TypeScript and uses React with React-Redux and sass for styles.

- https://github.com/prajjwalkapoor/kairy
  - a browser extension to manage your bookmark shortcuts and reading lists.

- https://github.com/camellia-app/camellia /好看
  - a browser extension that helps you access hundreds of bookmarks on the page that appears when you open new tab in your browser.

- https://github.com/JQuinzell/react-bookmarker
  - bookmarking browser extension implemented in react.

- https://github.com/deweyapp/dewey /201603/js/inactive
  - a Chrome app for tagging, searching and sorting your Chrome bookmarks.

## twitter-bookmarks

- https://github.com/twillot-app/twillot /202501/ts/archived
  - https://twillot.com/
  - Effortlessly search, organize, and export your X/Twitter bookmarks with AI-powered categorization - no Premium account required.
  - [竞品调研 _202403](https://github.com/twillot-app/twillot/discussions/3)

- https://github.com/prinsss/twitter-web-exporter /2.2kStar/MIT/202603/ts
  - Export tweets, bookmarks, lists and much more from Twitter(X) web app. (推文/书签/收藏/列表导出工具)
  - 支持导出json数据，但不支持导入本地json数据
  - 🐛
    - 管理功能不够强大, 可参考dewey或twillot
    - 数据保存在浏览器缓存, 容易被清理管家自动清除
    - bookmarks页面需要手动滚动才能让动态加载的书签被捕获, 对于书签很多的情况很繁琐
    - 安装扩展后，一直捕获不到bookmarks, 过了几小时，突然就捕获到了, 奇怪
  - [Content-Security-Policy (CSP) Issues _202404](https://github.com/prinsss/twitter-web-exporter/issues/19)
  - [开启插件后刷不出帖子 _202403](https://github.com/prinsss/twitter-web-exporter/issues/8)
    - 原来Tampermonkey不行， 换了violentmonkey,可以正常刷出帖子
  - [Doesn’t work with Orion anymore ](https://github.com/prinsss/twitter-web-exporter/issues/98)
    - caused by a known issue about Twitter's CSP not allowing us to inject random userscripts.
- https://github.com/afar1/fieldtheory-cli /MIT/202604/ts
  - https://fieldtheory.dev/cli
  - Sync and locally store all of your X/Twitter bookmarks. 
  - Free and open source CLI for Mac.
  - On first run, ft sync extracts your X session from Chrome and downloads your bookmarks into ~/.ft-bookmarks/.
  - Your data stays local. No telemetry, no analytics, nothing phoned home. The CLI only makes network requests to X's API during sync.
  - Chrome session sync reads cookies from Chrome's local database, uses them for the sync request, and discards them. Cookies are never stored separately.
  - The default sync uses X's internal GraphQL API, the same API that x.com uses in your browser. For the official v2 API, use ft auth + ft sync --api.

- https://github.com/viperrcrypto/Siftly /1.5kStar/MIT/202603/ts
  - Local Twitter/X bookmark organizer with AI categorization and mindmap visualization
  - Click "Export X Bookmarks" in your bookmark bar, the tool scrolls through and captures all your bookmarks automatically

- https://github.com/alexknowshtml/smaug
  - Archive your Twitter/X bookmarks (and/or optionally, likes) to markdown. Automatically.
  - Smaug uses the bird CLI which needs your Twitter session cookies.
    - Fetches bookmarks from Twitter/X using the bird CLI (can also fetch likes, or both)
  - https://github.com/jawond/bird

- https://github.com/zhaoscsc/x-bookmark-to-obsidian /MIT/202603/python/js
  - A Chrome extension + bundled macOS installer for saving X bookmarks into Obsidian.
  - 你在 x.com 点击收藏后，插件会自动抓取帖子内容，并把它保存成 Markdown 笔记写入 Obsidian。
  - 基于已有仓库 https://github.com/iamzifei/bookmark-is-learned /MIT/202602/js
  - https://github.com/JesstLe/x-bookmarks-to-obsidian
    - 自动将 X (Twitter) 书签保存到 Obsidian 的完整解决方案 - 包含 Chrome 自动化脚本、视频下载、图片提取等功能
  - https://github.com/ryanfoxeth/xmarks
    - Live sync X/Twitter bookmarks to Obsidian with AI categorization

- https://github.com/b3rntsen/twitter-bookmarks-merger /202603/python
  - Merge multiple X/Twitter bookmark exports, deduplicate, generate browsable HTML pages, and use AI to categorize your bookmarks.
  - 此扩展免费导出20条 https://chromewebstore.google.com/detail/x-bookmarks-exporter-expo/abgjpimjfnggkhnoehjndcociampccnm
# tag
- https://github.com/FelipeCortez/bmarks /django2
  - https://bmarks.net/felipecortez
  - Tag-based bookmark manager inspired by delicious and Pinboard
  - Import bookmarks saved in the Netscape format

- https://github.com/tagspaces/tagspaces /AGPLv3/202401/ts
  - https://www.tagspaces.org/
  - an offline, open source, document manager with tagging support
  - no backend, no login, file manager, organizer and browser
  - available for Windows, Linux, Mac OS and Android. 
  - provide a web clipper extension for Firefox, Edge and Chrome
  - supports two ways for tagging files. The default one embeds the tags directly in the name of the file, the other one uses a so called sidecar files for persisting the tags.
  - has integrated basic media player functionalities.
  - does not require an internet connection and any kind of online registration or service provider.
  - Note Taking - you can create and edit notes in plain text, markdown and html file formats
  - [Unable to use local folder on Self hosted Web version _202311](https://github.com/tagspaces/tagspaces/issues/2000)
    - The web version support location pointing to object storage (AWS S3, minio, S3proxy, Wasabi, R2) only
    - Yes it is technical, TagSpaces is a front-end application, which can connect to S3 back ends. For you use case you can use S3Proxy to expose a shared folder for example on a NAS and connect it with TagSpaces as S3 location.

- https://github.com/sintaxi/node-redis-tag
  - implement a tagging system into any node application.
  - A taggable object can be any model in your system. For example: post, person, etc.
  - we have 4 methods on the bookTagger object: get/set/find/top

## tag-ui

- https://github.com/yairEO/tagify
  - https://yaireo.github.io/tagify/
  - Transforms an input field or a textarea into a Tags component
  - Tags input component in VanillaJS/React/Angular/Vue

- https://github.com/react-tags/react-tags
  - a simple tagging component
  - Autocomplete based on a suggestion list
- https://github.com/olahol/react-tagsinput
  - customizable React component for inputing tags.

## tag-apps

- https://github.com/scale8/scale8-tag-manager-and-analytics
  - A simple, yet powerful Google Tag Manager alternative that is fully open-sourced and privacy-friendly.
# archiving
- https://github.com/wabarc/wayback /GPL/202601/go
  - https://docs.wabarc.eu.org/
  - An archiving tool with an IM-style interface that prioritizes privacy and accessibility, integrated with various archival services including Internet Archive, archive.today, Ghostarchive, IPFS, Telegraph, and file systems.
# browser-bookmark-utils
- https://github.com/flybayer/twitter-bookmarks-search
  - adds the ability to search your bookmarked tweets inside Twitter.
- https://github.com/twitterdev/bookmarks-search
  - uses the Bookmarks lookup endpoint to get your bookmarks

- https://github.com/raucao/webmarks
  - a bookmarking app, which lets you choose your server or provider for storing all data. 
  - It is a user-first, open-source alternative to proprietary, hosted bookmarking services like e.g. Delicious, Pinboard, et cetera.
# more-bookmark
- https://github.com/masonmcelvain/hop
  - 好看但不实用
  - a browser extension that stores links to your favorite sites in a more visually pleasing way than traditional bookmarks. 
  - Hop will try to find an icon for each link automatically, but you can use your own image if you prefer.
# bookmark-pm
- dewey. - [Save your favorite Twitter / X, LinkedIn, Bluesky, TikTok, Threads, Truth and web bookmarks all in one place _202603](https://getdewey.co/)
  - Organize: Built-in organization tools like folders, nested folders, and tags 
  - Search: Lightning-fast search of every bookmark, tag, author and note.
  - Export: easily export your entire library with one click - formatted as CSV, searchable PDFs, or a Google Sheet spreadsheet. Even export all associated media like images and videos
  - Share: let you turn on public sharing of bookmark folders to collaborate with others
  - AI Bulk Tagging
  - [Pricing - dewey. _202603](https://getdewey.co/pricing/)
    - export需付费
    - paid: auto-sync, folder, tag, ai, likes, full-thread, integrations-notion/google
# discuss
- ## 

- ## 

- ## Tag可以让内容分类有更高的自由度，但也很容易膨胀到冗余甚至失控，
- https://twitter.com/houjoe1/status/1732608680305254613
  - 不过，感觉 AI 的上帝视角可以在未来解决这个问题，帮助用户发现不用的 Tag、重复的 Tag、有更好的命名建议的 Tag，减少 Distraction
  - 比如系统自动根据首字母将tag分类
- 我 wishlist 里面就有 Readwise Reader 能够自动为我添加的文章打标。
