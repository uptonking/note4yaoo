---
title: toc-repos-solutions
tags: [repos, solutions, toc]
created: 2020-10-05T08:55:29.692Z
modified: 2020-12-12T19:32:36.255Z
---

# toc-repos-solutions

# guide

# crawler
- https://github.com/openzim/mwoffliner /GPLv3/202403/ts
  - Mediawiki scraper: all your wiki articles in one highly compressed ZIM file
  - 依赖linux/mac环境、redis、libzim
  - MWoffliner is a tool for making a local offline HTML snapshot of any online MediaWiki instance.
  - It goes through all online articles (or a selection if specified) and create the corresponding ZIM file. 
  - **It has mainly been tested against Wikimedia projects like Wikipedia and Wiktionary** --- but it should also work for any recent MediaWiki.

- https://github.com/apify/crawlee /11.6kStar/apache2/202403/ts
  - https://crawlee.dev/
  - A web scraping and browser automation library for Node.js to build reliable crawlers. 
  - Extract data for AI, LLMs, RAG, or GPTs. 
  - Download HTML, PDF, JPG, PNG, and other files from websites. 
  - Works with Puppeteer, Playwright, Cheerio, JSDOM, and raw HTTP. 
  - Both headful and headless mode. With proxy rotation.
  - Crawlee gives you the tools to crawl the web for links, scrape data, and store it to disk or cloud while staying configurable to suit your project's needs.
  - Pluggable storage of both tabular data and files

- https://github.com/get-set-fetch/scraper /MIT/202206/ts/inactive
  - a plugin based, nodejs web scraper(刮刀). 
  - It scrapes, stores and exports data.
  - At its core, an ordered list of plugins is executed against each to be scraped URL. 
  - Supported databases: SQLite, MySQL, PostgreSQL.
  - Supported browser clients: Puppeteer, Playwright.
  - Supported DOM-like clients: Cheerio, JSdom.
  - getsetfetch-extension /202108/ts/inactive
    - https://github.com/get-set-fetch/extension
    - https://getsetfetch.org/extension/getting-started.html
    - open source web scraper available as a cross-browser (chrome, firefox, edge) extension with csv and zip export capabilities.
    - parses pages and stores relevant data in the builtin browser database (IndexedDB)
    - Binary data (images, pdf files, …) can be exported as zip archives. Text based data can be exported as csv files.

- https://github.com/webrecorder/browsertrix-crawler /js
  - a simplified (Chrome) browser-based high-fidelity crawling system, designed to run a complex, customizable browser-based crawl in a single Docker container. 
  - uses Puppeteer to control one or more browser windows in parallel.
  - Single-container, browser based crawling with a headless/headful browser running pages in multiple windows.
  - YAML-based configuration, passed via file or via stdin.
  - Screenshotting: Ability to take thumbnails, full page screenshots, and/or screenshots of the initial page view.

- https://github.com/xiyuan-fengyu/ppspider /MIT/202012/ts/inactive
  - 基于puppeteer的web爬虫框架，提供灵活的任务队列管理调度方案，提供便捷的数据保存方案（nedb/mongodb），提供数据可视化和用户交互的实现方案

- https://github.com/yetzt/node-scrapyard /201701/js
  - Scrapyard makes scraping websites easy. I'ts a wrapper for most the things you need, comes with optional caching and retries, and opens as many connections as you like.

- https://github.com/coder-hxl/x-crawl /MIT/202311/rust
  - 一个灵活的 Node.js 多功能爬虫库。灵活的使用方式和众多的功能可以帮助您快速、安全、稳定地爬取页面、接口以及文件。
  - 异步同步 - 只需更改一下 mode 属性即可切换异步或同步爬取模式。
  - 支持爬动态页面、静态页面、接口数据、文件以及轮询操作。
  - 无间隔、固定间隔以及随机间隔，产生或避免高并发爬取。
  - 配合失败重试，自定义错误次数以及 HTTP 状态码自动轮换代理。
  - 优先队列 - 根据单个爬取目标的优先级可以优先于其他目标提前爬取。

- https://github.com/NaiboWang/EasySpider /CC-NonCommercial/202404/python/js
  - 易采集：一个可视化浏览器自动化测试/数据采集/爬虫软件，可以无代码图形化的设计和执行爬虫任务
# crawler-examples
- https://github.com/yangwenmai/github-trending-backup /202401/go
  - Github trending backup by everyday.
  - We scrape the github trending page of these languages: Go, Rust, Python, Ruby, C++, C, Java, Shell, Makefile, Swift, Objective-C, Kotlin, Jupyter-Notebook, HTML, JavaScript, TypeScript, CSS, Vue, TeX, Markdown, and push a markdown result everyday.
# gis
- https://github.com/lionsoul2014/ip2region
  - 准确率99.9%的离线IP地址定位库，0.0x毫秒级查询
  - ip2region.db数据库只有数MB
  - 提供了java, php, c, python, nodejs, golang, c#等查询绑定和Binary, B树, 内存三种查询算法。
- https://github.com/wzhe06/ipdatabase
  - 二叉树快速搜索IP地址数据库
  - 数据源采用2015年广告协会制定的IP地址标准数据库，中国互联网广告行业统一采用的标准IP库。
- https://github.com/soffchen/GeoIP2-CN
  - 更小巧、更实时的中国大陆 GeoIP2 数据库及 IP 地址段，基于 chnroutes2
  - 提供下载txt、mmdb
# screen-sharing
- https://github.com/screego/server /ts/go
  - https://screego.net/
  - share your screen with good quality and low latency.

- https://github.com/alyssaxuu/screenity /202205/js
  - The most powerful screen recorder & annotation tool for Chrome/Edge
  - 此产品很适合录制演示视频或讲课培训的场景，支持标签页、桌面、应用和摄像头，支持标注划线，也可很方便的导出视频
  - Make unlimited recordings of your tab, desktop, any application, and camera
  - Annotate by drawing anywhere on the screen, adding text, and creating arrows
# more
