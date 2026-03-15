---
title: toc-lib-utils-writing-reading
tags: [lib, reading, toc, utils, writing]
created: 2023-01-09T10:21:05.889Z
modified: 2023-08-31T04:01:14.658Z
---

# toc-lib-utils-writing-reading

# guide

# popular

# reading-mode
- https://github.com/mozilla/readability /11kStar/apache2/202511/js/firefox/inact 
  - A standalone version of the readability library used for Firefox Reader View.
  - firefox的reader view就是类似提取正文算法。
  - [Extracting clean data from blog and news articles](https://ujeebu.com/blog/how-to-extract-clean-text-from-html/)

- https://github.com/kepano/defuddle /4.8kStar/MIT/202603/ts
  - https://defuddle.md/
  - Get the main content of any page as Markdown.
  - Defuddle extracts the main content from web pages. 
  - It cleans up web pages by removing clutter like comments, sidebars, headers, footers, and other non-essential elements, leaving only the primary content.
  - Defuddle was created for the browser extension Obsidian Web Clipper, but it is designed to run in any environment.
  - Defuddle can be used as a replacement for Mozilla Readability with a few differences:
    - More forgiving, removes fewer uncertain elements.
    - Provides a consistent output for footnotes, math, code blocks, etc.
    - Uses a page's mobile styles to guess at unnecessary elements.
    - Extracts more metadata from the page, including schema.org data.
  - https://x.com/chenchengpro/status/2032648998851674300
    - 刚更新的最新版加了一个我觉得很实用的功能：直接解析 YouTube 链接，返回带时间戳、章节、说话人识别的 Markdown 字幕，不需要任何 API，就是直接从 YouTube 拿字幕然后整理干净。

- https://github.com/ZachSaucier/Just-Read /1.3kStar/EULA/202509/js/inactive
  - https://justread.link/
  - A customizable read mode web extension
  - Premium features can be enabled by purchasing Just Read Premium.

- https://github.com/rNeomy/reader-view /544Star/MPL/202512/js/inactive
  - https://webextension.org/listing/chrome-reader-view.html
  - Reader View extension brings Mozilla's open-source Readability implantation(植入、移植) to Chromium. 
  - Using this extension you can strip clutters from webpages and read them on the "Reader View" mode. 
  - The extension allows you to toggle between normal view and reader view by pressing the page-action button.
# more
