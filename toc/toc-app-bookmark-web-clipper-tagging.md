---
title: toc-app-bookmark-web-clipper-tagging
tags: [bookmark, tag, toc, web-clipper]
created: 2022-11-04T15:09:05.417Z
modified: 2022-11-11T11:04:29.007Z
---

# toc-app-bookmark-web-clipper-tagging

# guide

- tips
  - 标签管理通常作为产品的一个功能，而不是独立的产品
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

- https://github.com/alyssaxuu/omni
  - The all-in-one tool to supercharge your productivity
  - With Omni you can use your browser like a pro. 
  - Manage tabs, bookmarks, your browser history, perform all sorts of actions and more with a simple command interface.

- https://github.com/pawelmalak/flame /MIT/202307/ts
  - Flame is self-hosted startpage for your server. inspired (heavily) by SUI.
  - Easily manage your apps and bookmarks with built-in editors.

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
# web-clipper
- maoxian-web-clipper /596Star/MIT/202209/js
  - https://github.com/mika-cn/maoxian-web-clipper
  - A web extension to clip information from web page.
  - All file will save in local hard disk, you can control your data totally

- https://github.com/deathau/markdownload /202210/js
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

- https://github.com/Daniel31x13/linkwarden /MIT/js/代码简单
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

- https://github.com/floccusaddon/floccus /MPLv2/202401/ts/js/vue
  - https://floccus.org/
  - Sync your bookmarks privately across browsers and devices
  - Syncs your real, native browser bookmarks directly
  - Sync via Nextcloud Bookmarks, Google Drive or any WebDAV-compatible service
  - Install the floccus Android app to access your bookmarks on your phone
  - (eventual) consistency is more important than intention preservation

- https://github.com/linkwarden/linkwarden /AGPLv3/202401/ts
  - https://linkwarden.app/
  - Self-hosted collaborative bookmark manager to collect, organize, and preserve webpages and articles.
  - 依赖headlessui、zustand、@mozilla/readability、prisma、nextjs、next-auth
  - Linkwarden also saves a copy of each webpage as a Screenshot and PDF
  - designed with collaboration in mind, sharing links with the public and/or allowing multiple users to work together

- https://github.com/ArchiveBox/ArchiveBox /MIT/202401/python
  - https://archivebox.io/
  - self-hosted internet archiving solution to collect, save, and view websites offline.
  - Use ArchiveBox as a command-line package and/or self-hosted web app on Linux, macOS, or in Docker.
  - It saves snapshots of the URLs you feed it in several redundant formats.
  - It uses normal filesystem folders to organize archives (no complicated proprietary formats), and offers a CLI + web UI.
- https://github.com/kanishka-linux/reminiscence /AGPLv3/202401/python/js
  - Self-hosted Bookmark and Archive manager

- https://github.com/bdTechies/book-manager /201901/js
  - https://book-manager.bdtechies.com/
  - cross-platform desktop app to manage personal library.

- https://github.com/osmoscraft/osmosmemo
  - Turn GitHub into a bookmark manager
  - A browser bookmark manager optimized for capture and retrieval speed.
  - Extract page title and url into a short markdown snippet.

- https://github.com/codeverland/codever
  - Bookmarks and Snippets Manager for Developers & Co
  - frontend uses with Angular and Angular CLI.
  - backend uses ExpressJS with MongoDB and Keycloak. OpenAPI

- https://github.com/go-shiori/shiori /MIT/202312/go/js
  - bookmark manager built with Go
  - Intended as a simple clone of Pocket. 
  - You can use it as a command line application or as a web application. 

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

## offline

- https://github.com/dosyago/DiskerNet /js
  - An internet on yer disk. Full text search archive from your browsing and bookmarks.
  - Two modes: archive everything or only bookmark-worthy content

- https://github.com/kanishka-linux/reminiscence /python
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
# discuss
- ## 

- ## 

- ## Tag可以让内容分类有更高的自由度，但也很容易膨胀到冗余甚至失控，
- https://twitter.com/houjoe1/status/1732608680305254613
  - 不过，感觉 AI 的上帝视角可以在未来解决这个问题，帮助用户发现不用的 Tag、重复的 Tag、有更好的命名建议的 Tag，减少 Distraction
  - 比如系统自动根据首字母将tag分类
- 我 wishlist 里面就有 Readwise Reader 能够自动为我添加的文章打标。
