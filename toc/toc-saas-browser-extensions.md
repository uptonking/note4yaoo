---
title: toc-saas-browser-extensions
tags: [browser, extensions, toc]
created: 2020-10-05T07:49:04.680Z
modified: 2022-11-04T15:11:24.012Z
---

# toc-saas-browser-extensions

# guide

- extension的settings同步
  - 可考虑用浏览器提供的api如chrome-sync，检测浏览器账户而自动拉取数据
  - 可考虑自定义实现，需要用户先提供一次身份和云存储位置(自建或第三方)，然后拉取数据
# popular
- https://github.com/FallenMax/smart-toc
  - A Chrome extension for auto-generating a table of contents

- https://github.com/arthurhammer/github-toc
  - Browser extension that adds a table of contents to GitHub repos, wikis and gists.

- https://github.com/jawil/GayHub
  - 优化GitHub的阅读体验
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

- https://github.com/maxmilton/new-tab /202206/ts
  - A list of your open tabs, recently closed tabs, and top sites.
  - built with [stage1](https://github.com/maxmilton/stage1) JavaScript framework

- https://github.com/jackyzha0/tabspace
  - new tab replacement that gives you your very own scratch space to help you stay organized and focused.
  - auto-saving notes, rich text formatting and natural language due dates.
  - Auto-saves to local storage
  - Uses natural language to recognize and highlight due dates
  - 类似普通markdown编辑器
- mdtab /8Star/MIT/202209/ts
  - https://github.com/shaoruu/mdtab
  - Write quick notes in Markdown on any new tabs!
  - Save to local storage/browser sync
  - Vim mode

- https://github.com/sajadhsm/new-word-tab
  - browser extension to learn a word per new tab!
# browser-extensions-utils
- https://github.com/PlasmoHQ/plasmo
  - The Plasmo Framework is a battery-packed browser extension SDK made by hackers for hackers
  - https://github.com/yousefamar/bookmarkdown
    - A browser extension that turns a webpage into a useful markdown note
# devtools
- https://github.com/shanebell/JaSON /202104/ts/inactive
  - a Google Chrome extension for testing APIs and making HTTP network requests.
  - Automatically sends cookies from Chrome. This is extremely handy for APIs which require authentication. 
# settings-sync
- https://github.com/shanalikhan/code-settings-sync
  - Synchronize your Visual Studio Code Settings Across Multiple Machines using GitHub GIST
# twitter
- https://github.com/tweetback/tweetback
  - Take ownership of your Twitter data. 

- https://github.com/transitive-bullshit/twitter-search
  - https://twitter-search.transitivebullsh.it/
  - Instantly search across your entire Twitter history with a beautiful UI powered by Algolia.
  - Built using Algolia, Twitter API, and Vercel
# more-extensions
- https://github.com/SanderRonde/CustomRightClickMenu
  - A browser extension to add links and run scripts/stylesheets all from your right-click menu
