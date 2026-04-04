---
title: toc-app-browser-extensions
tags: [browser, extensions, toc]
created: 2020-10-05T07:49:04.680Z
modified: 2023-02-08T10:24:11.422Z
---

# toc-app-browser-extensions

# guide

- extension的settings同步
  - 可考虑用浏览器提供的api如chrome-sync，检测浏览器账户而自动拉取数据
  - 可考虑自定义实现，需要用户先提供一次身份和云存储位置(自建或第三方)，然后拉取数据

- resources
  - [Extension Development and ToolKit - WebExtension. ORG](https://webextension.org/)
# draft
- tips
  - 👾 可让ai实现一些扩展

- zhihu
  - 去掉通知私信红点
  - 去掉html标题中的 (2条新消息 )
- reddit
  - ✅ 新ui显示绝对时间
# popular
- https://github.com/JasonGrass/auto-extension-manager /APGLv3/202411/js
  - https://ext.jgrass.cc/docs/intro
  - 用于浏览器扩展管理的扩展
  - 灵活的规则自定义，自动启用或禁用指定的浏览器扩展。
  - 批量导出/导入与分享扩展
# browsers-vendors
- https://github.com/lightpanda-io/browser /AGPLv3/202502/zig
  - https://lightpanda.io/
  - the open-source browser made for headless usage
  - Compatible with Playwright, Puppeteer through CDP (WIP)
# browser-ext-devtools
- https://github.com/DaniGuardiola/browser-namespace /ts
  - Cross-browser support for the "browser" namespace in browser extensions. Fully typed.
  - Some browsers use the `browser` API namespace, while others use `chrome`. This package unifies both and provides a fully typed API.
  - In contrast with webextension-polyfill, which does a lot more, this package limits itself to providing a convenient, unified and fully typed namespace.
# self-usage
- [History Trends Unlimited](https://sites.google.com/view/history-trends-unlimited/home?authuser=0)
  - it is closed source. Copyright 2013-2022 Randy Lauen. All Rights Reserved.

- https://github.com/FallenMax/smart-toc
  - A Chrome extension for auto-generating a table of contents

- https://github.com/zxlie/FeHelper /js
  - Web前端助手
  - Chrome & Firefox & MS-Edge Extension, All in one Toolbox!
  - 支持插件化安装

- https://github.com/arthurhammer/github-toc
  - Browser extension that adds a table of contents to GitHub repos, wikis and gists.

- https://github.com/jawil/GayHub
  - 优化GitHub的阅读体验

- https://github.com/pfcao/abookmark /js
  - Advanced bookmark manager comes with labels, sticky notes, and trash mode.
  - 基本复刻了chrome bookmark manager的功能
  - 支持list/grid视图
# table
- https://github.com/jamesandres/ColumnCopy
  - Google Chrome extension which enables selecting columns from table.
- https://github.com/gebrkn/copytables
  - Chrome extension to select and copy table cells.
- https://github.com/jchamet/html-table-sort
  - Clicking on a table column header th will reorder the rows of an HTML table in ascending/descending order.
- https://github.com/Sjord/tablefilter
  - Chrome extension to filter tables
  - https://github.com/koalyptus/TableFilter
    - Javascript library making HTML tables filterable and a bit more
- https://github.com/table-of-contents-sidebar/table-of-contents-sidebar
  - An outline tool makes it easier to navigate your novel. 
# wiki
- https://github.com/n3nikita/WikiCopy
  - Google chrome extension which helps you to copy from Wikipedia.
- https://github.com/gambolputty/wikitable2csv
  - A web tool to convert Wiki tables to CSV
# local-filesystem
- https://github.com/rxliuli/image-viewer
  - 尝试使用 web fs api 的图片查看器

- https://github.com/nikochan2k/kura
  - The FileSystem API abstraction library.
# extension-starter
- https://github.com/chibat/chrome-extension-typescript-starter
  - Chrome Extension TypeScript Starter
# new-tab
- dev
  - 如何实现同步
  - 如何自定义链接、图标
  - 支持突出某类链接图标如pwa，通过标签？颜色？

- placenoter /30Star/MIT/202211/ts
  - https://github.com/sereneinserenade/placenoter
  - This extension replaces your new tab with a note taking app
  - 依赖dnd-kit、tiptap
  - 支持写笔记和添加链接

- tabliss /1.5kStar/GPLv3/202207/ts/类似页面编辑器
  - https://github.com/joelshepherd/tabliss
  - https://tabliss.io/
  - https://web.tabliss.io/
  - A beautiful, customisable New Tab page for Firefox, Chrome, and Edge.
  - 支持设置添加链接书签、时钟、搜索、note文本输入框、待办项、背景、github-calendar、天气
  - 依赖react-intl、feather-icons、date-fns

- https://github.com/alekangelov/nt-dashboard /202107/ts
  - https://alekangelov.github.io/nt-dashboard/
  - A simple, fast and customizable dashboard for your new tab.
  - Uses Redux and a persistent storage solution with rehydration, custom modal solution
  - 可添加或删除链接，首页类似搜索页
  - 未实现浏览器扩展

- https://github.com/zombieFox/nightTab /202206/js
  - https://zombiefox.github.io/nightTab/
  - Customise the layout, style, background and bookmarks in nightTab -- a custom start page.
  - 聚焦于书签管理

- https://github.com/int128/bntp /44Star/202208/ts
  - providing the New Tab Page with bookmarks and recently visited sites.
  - 支持切换bookmarks、top-sites
  - 当书签过多时，新标签页会卡死

- https://github.com/mue/mue /202208/js
  - https://demo.muetab.com/
  - 自定义主页，可添加链接
  - 样式类似macos-like ui，大量运用白背景圆角卡片
  - 依赖mui5

- https://github.com/allister-grange/startertab /202211/ts
  - https://startertab.com/
  - 样式主题偏向于透明玻璃，很有意思
  - 大量可编辑的卡片，但没有添加链接

- https://github.com/jaszhix/tab-master-5000-extension /53Star/MIT/202206/ts
  - replaces your New Tab page with a full-featured tabs, history, bookmarks, apps, extensions, and sessions manager.
  - 展示浏览器现有的状态数据

- https://github.com/reorx/sui2 /202210/js/pwa
  - https://reorx.github.io/sui2/
  - a startpage for your server and / or new tab page
  - 支持按下文字后自动focus到对应按钮
  - Originally forked from sui, sui2 adds new features like keyboard navigation and PWA to boost your productivity.
  - https://github.com/jeroenpardon/sui
    - a startpage for your server and / or new tab page
- https://github.com/ndom91/newtelco-tab
  - 类似服务器状态卡片控制台

- https://github.com/darktrojan/newtabtools /202201/js
  - New Tab Tools add-on for Firefox and Chrome
  - 链接网格

- https://github.com/mikesprague/clean-start /202211/js/提交多
  - https://cleanstart.page/
  - Open source new tab extension
  - Layout/design based on what I liked from the Momentum browser extension
  - Demo available as a progressive web app (PWA)

- https://github.com/unicar9/jizhi /MIT/js
  - 支持自定义新标签页的 Chrome/Firefox/Edge 扩展，几枝将在新标签页上展示中国传统色的层叠波浪动画效果搭配经典诗词。
  - 好看，但不实用

- https://github.com/jackyzha0/tabspace /202212/ts/tiptap
  - new tab replacement that gives you your very own scratch space to help you stay organized and focused.
  - auto-saving notes, rich text formatting and natural language due dates.
  - Auto-saves to local storage
  - Uses natural language to recognize and highlight due dates
  - 类似普通markdown编辑器
  - 依赖tiptap、zustand、d3、wouter、framer-motion

- https://github.com/maxmilton/new-tab /202206/ts
  - A list of your open tabs, recently closed tabs, and top sites.
  - built with [stage1](https://github.com/maxmilton/stage1) JavaScript framework

- mdtab /8Star/MIT/202209/ts
  - https://github.com/shaoruu/mdtab
  - Write quick notes in Markdown on any new tabs!
  - 依赖react-ace、remark
  - Save to local storage/browser sync
  - Vim mode

- https://github.com/sajadhsm/new-word-tab
  - browser extension to learn a word per new tab!

- https://github.com/serogbp/Startpage
  - a kanban like page where you can save and organize your favorite websites. 
  - The websites are stored in the browser's Local Storage and they can be exported/imported in JSON format.
  - Developed using vanilla Javascript with the MVC pattern and Custom Elements.
# browser-extensions-utils
- https://github.com/wxt-dev/wxt /MIT/202502/ts
  - https://wxt.dev/
  - Next-gen framework for developing web extensions.
  - WXT provides a "module system" that let's you run code at different steps in the build process to modify it.

- https://github.com/PlasmoHQ/plasmo /MIT/202502/ts/提交少
  - https://www.plasmo.com/
  - a battery-packed browser extension SDK
  - Build your extension and let Plasmo handle browser-specific behaviors and bundling
  - https://github.com/yousefamar/bookmarkdown
    - A browser extension that turns a webpage into a useful markdown note
# devtools
- https://github.com/shanebell/JaSON /202104/ts/inactive
  - a Google Chrome extension for testing APIs and making HTTP network requests.
  - Automatically sends cookies from Chrome. This is extremely handy for APIs which require authentication.
# extensions-manager
- https://github.com/hankxdev/one-click-extensions-manager /js
  - a simple chrome extension to manage chrome extension
# settings-sync
- https://github.com/shanalikhan/code-settings-sync
  - Synchronize your Visual Studio Code Settings Across Multiple Machines using GitHub GIST
# search
- https://github.com/kawamataryo/chikamichi
  - Command pallet for the browser. 
  - Enables fuzzy search for histories, tabs and bookmarks.
  - Inspired by the Sidekick search dialogue
# bookmarks
- https://github.com/yorkxin/copy-as-markdown /689Star/MIT/202602/ts
  - A browser extension to copy tabs and links as Markdown
  - helps you copy the following things as Markdown to your system clipboard: 
    - On the web page: selection, link, image
    - Exporting tabs in the current window
  - You can add keyboard shortcuts for copying tab(s) as Markdown. By default, Copy as Markdown does not assign any keyboard shortcuts.
  - exportLink rewrites title first, then applies format-specific rendering
    - rewrite is now a pre-processing layer for all link formats (link, link- with-date, custom-format).
  - Custom format is Mustache templating ; 
    - Mustache is logic-less - it cannot do text replacement.
    - it formats output shape, but does not provide regex/string rewrite tools.

- https://github.com/vaeth/bookmarkdupes /js
  - A WebExtension which can display/remove duplicate bookmarks or empty folders
- https://github.com/zaksid/ext-duplicate-bookmarks-finder /js
  - Find and delete duplicate bookmarks.
# twitter
- https://github.com/tweetback/tweetback
  - Take ownership of your Twitter data. 

- https://github.com/transitive-bullshit/twitter-search
  - https://twitter-search.transitivebullsh.it/
  - Instantly search across your entire Twitter history with a beautiful UI powered by Algolia.
  - Built using Algolia, Twitter API, and Vercel
# media-player
- [Video Player for Local Files](https://chromewebstore.google.com/detail/video-player-for-local-fi/kfcfjmdnmmokdhndbpfcachlkliggggc)
  - web video player for local files.
  - It works completely offline. In addition to using the mouse, it supports many useful keyboard shortcuts
# media-download
- tips
  - 更多是针对具体网站的downloader

- https://github.com/LeonardoCiaccio/GrabAnyMedia /202304/js
  - https://grabanymedia.com/
  - Browser extension for video / audio / streaming downloads

- https://github.com/yangwk/m3u8-downloader /202212/js/inactive
  - chrome插件，支持监控和下载：m3u8流媒体、视频、音频
  - 纯chrome extensions api实现，没有依赖外部组件ffmpeg

- https://github.com/tuhinpal/hls-downloader
  - I noticed that there were fewer browser-based tools available for downloading video streams that use the HTTP Live Streaming (HLS) protocol, so I saw an opportunity to fill this gap

- https://github.com/DoctorLai/VideoDownloadHelper
  - On 31/Oct/2017, Google has reinstated the extension
  - But you are still able to use the web version: https://weibomiaopai.com/download-video-parser.php

- https://github.com/ngti/svg-grabber /MIT/201803/js/inactive
  - Open source chrome extension to quickly preview, download or copy inline or embedded SVG images from a website
# userscripts/tampermonkey
- registry/sources
  - 不要在userscripts管理器上花费过多时间, 支持新特性的管理器也许对safari/firefox的支持不好, 建议用最流行的
  - 有些扩展需要配置 csp等, 不同管理器的实现不同， 建议用最流行的
  - [Greasy Fork - safe and useful user scripts](https://greasyfork.org/en)

- tampermonkey
  - 有时刚安装的script会立即自动删除, 原因是启用了auto browser sync同步脚本, 因为某种原因本地和远程脚本不一致了
    - 解决方法, 先点击reset来停止browser sync，再点击run sync将本地脚本同步到远程

- https://github.com/violentmonkey/violentmonkey /8kStar/MIT/202603/js/vue
  - https://violentmonkey.github.io/
  - provides userscripts support for browsers. 
  - It works on browsers with WebExtensions support.
  - [[Feature] Manifest V3 for Chrome ](https://github.com/violentmonkey/violentmonkey/issues/1934)
  - 🍴 forks
  - https://github.com/Zulenka/ProjectSaturn

- https://github.com/Tampermonkey/tampermonkey /5.3kStar/GPL/201301/js/inactive
  - https://www.tampermonkey.net/
  - This repository contains the source of the Tampermonkey extension up to version 2.9.  it has been closed-sourced since version 3.0
  - All newer versions are distributed under a proprietary license.
  - [Tampermonkey Source State  _202303](https://github.com/Tampermonkey/tampermonkey/discussions/1735)
    - As the developer of Tampermonkey, I have always worked on it in a private repository. The reason for this is that I enjoy working alone without having to consider external contributions or feedback regarding the implementation and architecture for example. While I did occasionally synchronize the GitHub repository with my private repository between versions 1.0.0.1 and 2.9.0 from 2010 to 2013, the syncing was sporadic and sometimes occurred with a two-year gap.
    - However, the Mozilla Add-ons and Opera teams are receiving a source package to build and review Tampermonkey with every new version, and when I worked with the Microsoft Edge team on extension support for the first version of the Edge browser, they also had full access to the source code. Additionally, Firefox recently made Tampermonkey available for their Android browser after a review.

- https://github.com/scriptscat/scriptcat /4.2kStar/GPL/202603/ts
  - https://docs.scriptcat.org/
  - https://chromewebstore.google.com/detail/scriptcat/ndcooeababalnlpkfedmmbbbgkljhpjf
  - 脚本猫，一个可以执行用户脚本的浏览器扩展
  - ScriptCat is a powerful userscript manager based on Tampermonkey's design philosophy, fully compatible with Tampermonkey scripts. 
  - It not only supports traditional userscripts but also innovatively implements a background script execution framework with rich API extensions, enabling scripts to accomplish more powerful functions. 
    - supports backend scripts and timed scripts. This is a function that tampering monkeys do not possess. 
  - It features an excellent built-in code editor with intelligent completion and syntax checking, making script development more efficient and smooth.
  - Cloud Sync

## github

- 
- 
- 
- 

- [GitHub Useful Forks](https://greasyfork.org/zh-CN/scripts/496406-github-useful-forks)
  - Adds a button to GitHub repositories to see useful forks of the repo.
- [Github 快捷查找活跃的Forks列表](https://greasyfork.org/zh-CN/scripts/494365-github-%E5%BF%AB%E6%8D%B7%E6%9F%A5%E6%89%BE%E6%B4%BB%E8%B7%83%E7%9A%84forks%E5%88%97%E8%A1%A8)

- [Github加速](https://greasyfork.org/zh-CN/scripts/495513-github%E5%8A%A0%E9%80%9F)
- [Github 增强 - 高速下载](https://greasyfork.org/zh-CN/scripts/412245-github-%E5%A2%9E%E5%BC%BA-%E9%AB%98%E9%80%9F%E4%B8%8B%E8%BD%BD)

- [复制 GitHub 仓库名](https://greasyfork.org/zh-CN/scripts/494749-copy-github-repo-name)
  - 在 GitHub 页面上添加一个按钮，点击后可以复制仓库名（owner/repo）

## twitter

- 
- 

- [Twitter: view more replies and remove useless sections](https://greasyfork.org/zh-CN/scripts/429224-twitter-view-more-replies-and-remove-useless-sections)
  - View more replies and remove useless sections from twitter
- [X.com (Twitter) - Auto Show More Replies](https://greasyfork.org/zh-CN/scripts/486830-x-com-twitter-auto-show-more-replies)

- [Twitter Block Porn](https://greasyfork.org/zh-CN/scripts/470359-twitter-block-porn)
  - 受不了评论区黄推了? 打开共享黑名单，用 Twitter-Block-Porn 插件一键批量拉黑黄推，手机上也能生效，普通人拉黑受益的是自己，大V拉黑受益的是所有人。

- [在推特上显示正常的日期和时间](https://greasyfork.org/zh-CN/scripts/462064-show-date-normally-on-twitter)
  - 看起来是这样的。70/12/31(Th) 23:59:59。

- [Twitter Bookmark Shortcut](https://greasyfork.org/zh-CN/scripts/489289-twitter-bookmark-shortcut)
  - Add a bookmark shortcut to Twitter's home page
- [X Bookmarks Organizer](https://greasyfork.org/zh-CN/scripts/496107-x-bookmarks-organizer)
  - Organize your X bookmarks into folders for free.
  - Data of script can be imported and exported.
- [Twitter Bookmark Extractor](https://greasyfork.org/zh-CN/scripts/493568-twitter-bookmark-extractor)
  - Extracts bookmarked tweets from Twitter bookmarks page
  - You can find the downloaded JSON file in your download directory and open it with any text editor.
- [Twitter Web Exporter](https://greasyfork.org/zh-CN/scripts/492218-twitter-web-exporter)
  - 从 Twitter(X) 网页版导出推文、书签、列表等各种数据，支持导出 JSON/CSV/HTML。

- [Twitter Direct](https://greasyfork.org/zh-CN/scripts/404632-twitter-direct)
  - Remove t.co tracking links from Twitter

- [Twitter Zoom Cursor](https://greasyfork.org/zh-CN/scripts/413963-twitter-zoom-cursor)
  - Distinguish between images and links on Twitter

- [Twitterᴾˡᵘˢ](https://greasyfork.org/zh-CN/scripts/387969-twitter%E1%B4%BE%CB%A1%E1%B5%98%CB%A2)
  - 增强 X(Twitter) 使用体验。读取原始画质的图片，移除广告与垃圾推文。

- [twitter-promotion-remover](https://greasyfork.org/zh-CN/scripts/453503-twitter-promotion-remover)

- 
- 
- [显示转发的日期和时间。](https://greasyfork.org/zh-CN/scripts/462070-show-ctime-of-retweets)

## 知乎/掘金/小红书/csdn

- [知乎修改器🤜持续更新🤛努力实现功能最全的知乎配置插件](https://greasyfork.org/zh-CN/scripts/423404-%E7%9F%A5%E4%B9%8E%E4%BF%AE%E6%94%B9%E5%99%A8-%E6%8C%81%E7%BB%AD%E6%9B%B4%E6%96%B0-%E5%8A%AA%E5%8A%9B%E5%AE%9E%E7%8E%B0%E5%8A%9F%E8%83%BD%E6%9C%80%E5%85%A8%E7%9A%84%E7%9F%A5%E4%B9%8E%E9%85%8D%E7%BD%AE%E6%8F%92%E4%BB%B6)
  - 页面模块自定义隐藏，列表及回答内容过滤，保存浏览历史记录，推荐页内容缓存
- [ZhiHuNock-Q](https://greasyfork.org/zh-CN/scripts/494300-zhihunock-q)
  - 一个固执己见的知乎问答的脚本，致力于提升问答审阅的信息可见性
- [ZhiHuNock](https://greasyfork.org/zh-CN/scripts/493979-zhihunock)
  - 一个固执己见的知乎的脚本，致力于提升文章审阅的信息可见性

- [JueJinNock](https://greasyfork.org/zh-CN/scripts/494579-juejinnock)
  - 一个固执己见的掘金的脚本，致力于提升文章审阅的信息可见性

- [CnBlogsNock](https://greasyfork.org/zh-CN/scripts/494487-cnblogsnock)
  - 一个固执己见的博客园的脚本，致力于提升文章审阅的信息可见性

- 
- 

- [博客网站的精简和宽屏处理](https://greasyfork.org/zh-CN/scripts/482865-%E5%8D%9A%E5%AE%A2%E7%BD%91%E7%AB%99%E7%9A%84%E7%B2%BE%E7%AE%80%E5%92%8C%E5%AE%BD%E5%B1%8F%E5%A4%84%E7%90%86)

- [CSDNock](https://greasyfork.org/zh-CN/scripts/493011-csdnock)
  - 一个固执己见的 CSDN 的脚本，致力于提升文章审阅的信息可见性

## b站

- [B站封面获取](https://greasyfork.org/zh-CN/scripts/395575-b%E7%AB%99%E5%B0%81%E9%9D%A2%E8%8E%B7%E5%8F%96)
  - 获取B站各播放页及直播间封面，支持手动及实时预览等多种模式，支持点击下载、封面预览、快速复制，可高度自定义

- [bilibili 页面净化大师](https://greasyfork.org/zh-CN/scripts/479861-bilibili-%E9%A1%B5%E9%9D%A2%E5%87%80%E5%8C%96%E5%A4%A7%E5%B8%88)
  - 净化 B站/哔哩哔哩 页面，支持「精简功能、播放器净化、过滤视频、过滤评论、全站黑白名单」，提供 300+ 功能，定制自己的 B 站

- 
- 
- 
- [下载 bilibili 原图](https://greasyfork.org/zh-CN/scripts/494018-%E4%B8%8B%E8%BD%BD-bilibili-%E5%8E%9F%E5%9B%BE)
  - 以原来的格式右键下载 bilibili 动态和评论区中的图片，而不是 webp 或 avif

- [B站评论区开盒](https://greasyfork.org/zh-CN/scripts/448434-b%E7%AB%99%E8%AF%84%E8%AE%BA%E5%8C%BA%E5%BC%80%E7%9B%92)
  - [BiliBili 评论区/空间显示IP属地 BiliBili IP Geolocation](https://greasyfork.org/zh-CN/scripts/462151-bilibili-%E8%AF%84%E8%AE%BA%E5%8C%BA-%E7%A9%BA%E9%97%B4%E6%98%BE%E7%A4%BAip%E5%B1%9E%E5%9C%B0-bilibili-ip-geolocation)

## sites(single)

- 
- 
- 
- 
- 

- [Discord Get Your Token](https://greasyfork.org/zh-CN/scripts/437442-discord-get-your-token)
  - [Discord Login with Token](https://greasyfork.org/zh-CN/scripts/483983-discord-login-with-token)

- [▲V2EX Polish - 体验更现代化的 V2EX 🟢](https://greasyfork.org/zh-CN/scripts/459848-v2ex-polish-%E4%BD%93%E9%AA%8C%E6%9B%B4%E7%8E%B0%E4%BB%A3%E5%8C%96%E7%9A%84-v2ex)
  - 一款专为 V2EX 用户设计的浏览器插件，提供了丰富的扩展功能，让原生页面焕然一新

- [MoreMovieRatings](https://greasyfork.org/zh-CN/scripts/7687-moremovieratings)
  - 豆瓣和IMDb互相显示评分

- [arxiv论文下载重命名工具](https://greasyfork.org/zh-CN/scripts/479524-arxiv-download-rename-tool)
  - 当您从arxiv.org下载论文时，它可以将pdf重命名为【日期+论文标题】的形式

## userscripts-mgr

- [Magic Userscript+ ：显示站点所有 UserJS](https://greasyfork.org/zh-CN/scripts/421603-magic-userscript-show-site-all-userjs)
  - 为当前网页查找可用的用户脚本。

- 
- 
- 
- 

## devtools

- https://github.com/ccorcos/click-perf /202504/js
  - A browser extension that monitors and logs click performance metrics on web pages.
  - Monitors page load performance
  - Real-time logging in browser console

- 
- 
- 

- [网页调试](https://greasyfork.org/zh-CN/scripts/475228-%E7%BD%91%E9%A1%B5%E8%B0%83%E8%AF%95)
  - 内置多种网页调试工具，包括：Eruda、vConsole、PageSpy、Chii，可在设置菜单中进行详细配置

## utils

- 
- 
- 
- 

- [翻译机](https://greasyfork.org/zh-CN/scripts/378277-%E7%BF%BB%E8%AF%91%E6%9C%BA)
  - 该脚本用于翻译各类常用社交网站为中文，不会经过中间服务器。

- [Picviewer CE+](https://greasyfork.org/zh-CN/scripts/24204-picviewer-ce)
  - 在线看图工具，支持图片翻转、旋转、缩放、弹出大图、批量保存

- [HTML5视频播放工具](https://greasyfork.org/zh-CN/scripts/30545-html5%E8%A7%86%E9%A2%91%E6%92%AD%E6%94%BE%E5%B7%A5%E5%85%B7)
  - 视频截图；切换画中画；缓存视频；万能网页全屏；添加快捷键：快进、快退、暂停/播放、音量、下一集、切换(网页)全屏、上下帧、播放速度。支持视频站点：油管、TED、优. 土、QQ、B站、西瓜视频、爱奇艺、A站、PPTV、芒果TV、咪咕视频、新浪、微博、网易[娱乐、云课堂、新闻]、搜狐、风行、百度云视频等；直播：twitch、斗鱼、YY、虎牙、龙珠、战旗。可增加自定义站点
- [HTML5视频播放器增强脚本](https://greasyfork.org/zh-CN/scripts/381682-html5%E8%A7%86%E9%A2%91%E6%92%AD%E6%94%BE%E5%99%A8%E5%A2%9E%E5%BC%BA%E8%84%9A%E6%9C%AC)
  - 视频增强脚本，支持所有H5视频网站，例如：B站、抖音、腾讯视频、优酷、爱奇艺、西瓜视频、油管（YouTube）、微博视频、知乎视频、搜狐视频、网易公开课、百度网盘、阿里云盘、ted、instagram、twitter等。全程快捷键控制，支持：倍速播放/加速播放、视频画面截图、画中画、网页全屏、调节亮度、饱和度、对比度、自定义配置功能增强等功能，为你提供愉悦的在线视频播放体验。还有视频广告快进、在线教程/教育视频倍速快学、视频文件下载等能力

- [视频全屏显示时间](https://greasyfork.org/zh-CN/scripts/452520-%E8%A7%86%E9%A2%91%E5%85%A8%E5%B1%8F%E6%98%BE%E7%A4%BA%E6%97%B6%E9%97%B4)
  - 这个脚本的作用只有一个，就是在视频左上角显示一个系统时间，方便全屏看视频期间随时了解时间。

- [中文字体优化](https://greasyfork.org/zh-CN/scripts/399547-%E4%B8%AD%E6%96%87%E5%AD%97%E4%BD%93%E4%BC%98%E5%8C%96)

- [杀死水印（Kill Watermark）](https://greasyfork.org/zh-CN/scripts/459646-%E6%9D%80%E6%AD%BB%E6%B0%B4%E5%8D%B0-kill-watermark)
  - 杀死水印（移除烦人的水印，还你一个干净清爽的页面）；已适配360 智脑、腾讯文档、飞书、FreeBuf 网络安全行业门户、稿定设计、爱奇艺播放页（右上角 logo、暂停时的广告）、腾讯课堂播放页漂浮水印、哔哩哔哩直播左上角 logo、CSDN C 知道、腾讯视频播放页（右上角 logo、暂停时的弹窗广告）、优酷视频播放页（右上角 logo、暂停时的弹窗广告）、语雀
# more-extensions
- https://github.com/SanderRonde/CustomRightClickMenu
  - A browser extension to add links and run scripts/stylesheets all from your right-click menu

- [Let's build a Chrome extension that steals everything](https://mattfrisbie.substack.com/p/spy-chrome-extension)
  - let’s build a Chrome extension that steals as much data as possible. 
