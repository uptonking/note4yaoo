---
title: lib-excel-app-list-grid-community-pm-showcase
tags: [community, data-grid, excel, showcase]
created: 2023-05-21T15:43:54.248Z
modified: 2024-08-11T07:22:03.920Z
---

# lib-excel-app-list-grid-community-pm-showcase

# guide

# discuss-teable/eidos
- ## 

- ## 有没有 logseq/obsidian 插件玩的比较 6 的。 扩展是全局可用还是和 space 绑定，哪种方案好一点
- https://discord.com/channels/1153437530952323186/1170178651761946654/1219438282245542009
- 最近把 scripts 扩展成了 extensions，分成了下面几种扩展类型。
  - script，写代码实现任意功能
  - udf，在表格 formula 字段中使用的自定义函数
  - prompt，自定义提示词, 目前可以和文档集成
  - app，script + ui

- ob的插件只能当前仓库生效，我觉得如果可以支持全局就很不错

- ## teable 底层用 grid 库和 eidos 是同一个？
- https://discord.com/channels/1153437530952323186/1170178651761946654/1216653039176253450
- 不是。teable 是 canvas 自己画的，还没有抽象出来可用的包，目前就是内部用。
- eidos 用的 https://github.com/glideapps/glide-data-grid

- eidos 什么时候开源？  
  - 不知道，大功能做不了，小 bug 不想修。每天就是摸鱼
# discuss
- ## 

- ## 

- ## 

- ## 🚀 [Excel Labs, a Microsoft Garage Project | Hacker News _202305](https://news.ycombinator.com/item?id=36081851)
- Some things in Excel have not improved since 2003, that should be fixed before toying with "AI" . For example, when importing a CSV:
  - Excel cannot guess the encoding of the file
  - Excel cannot guess the separators either

- Excel lately is turning into a really compelling product, using functions such as sequence (dynamic arrays), lambda (pure functions) and let (defining sub-variables). You'd think you're coding in a pure functional language, and that's great

- The universal language and portability of a spreadsheet is really hard to beat.

- ## 🚀 [Bricks - Show HN: Fast Modern Spreadsheet | Hacker News _202403](https://news.ycombinator.com/item?id=39817041)
- 👷🏻 Co-founder/CTO here.
  - we wanted to make an online spreadsheet that exceeds the speed of a desktop version of Excel
  - we are running all calculations on the client-side using multithreaded WebAssembly (C++) & CRDT for collaboration. 
  - We also wrote our own optimized Canvas-based spreadsheet renderer.
  - Running calculations locally allows us to minimize cost to serve a user, to eventually implement e2e encryption, and to provide an offline mode. 
  - We will also ship a native desktop app next month to get around 4GB browser WASM limitation and to get an extra 30% speed boost.

- 
- 
- 

- ## [rowzero - Show HN: We built the fastest spreadsheet | Hacker News _202402](https://news.ycombinator.com/item?id=39551064)
- 🤔 How is the data modelled and persisted? What database and how is conflict handled? CRDT?
  - We use Apache Arrow data format, so it's fairly columnar. We have built some custom layers on top of Arrow as well to handle some fancier data types.
  - For storage and orchestration we use S3 and Dynamo.
  - Yes exactly, we use CRDTs for multiplayer stuff.

- ## 📈🔀 [Quadratic – Open-Source Spreadsheet Is Now Multiplayer | Hacker News _202402](https://news.ycombinator.com/item?id=39217440)
- Quadratic is an open-source spreadsheet application for engineers that supports Python, SQL (coming soon), and classic Formulas. 
  - Unlike other spreadsheets, Quadratic has an infinite canvas (like Figma). 
  - As a result, you can pinch and zoom to navigate large data sets, and everything renders smoothly at 60fps.
- Quadratic is built using WebGL and Rust WASM. We built our multiplayer service from scratch in Rust to handle large amounts of data smoothly. For smooth rendering of a large grid of data, cells and text are rendered using low-level WebGL for performance.

- What is the use case? You don't seem to be for application building, rather for doing analysis work
- The use case is doing analysis work as a team, with some engineers and some people only familiar with spreadsheets all being able to work together.
  - Quadratic is always free for individuals, and we will be paid for Teams, which will be shared folders that we are launching in a couple of weeks.

- I had a look at the server code. Is the idea that you will just vertically scale up the server to handle the load, or is there a mechanism for scaling out horizontally?
  - The quadratic-multiplayer service is designed to be scaled vertically. Once we hit that limit, we will need to come up with a way to route traffic to servers based on what file a user is accessing and what server is hosting that room.
  - Every other service can be scaled horizontally today. However, the Rust services are very efficient at processing traffic, and a single node can handle significant usage.

- ## [Show HN: rowsncolumns React Spreadsheet 2 | Hacker News_202311](https://news.ycombinator.com/item?id=38390714)
- Curious: since you are rendering everything via canvas, how do you do accessibility?
  - For screen readers, we are planning to add table element with plain text content, with aria regions.
  - We offer support for keyboard shortcuts and navigation, and our platform is natively compatible with both light and dark modes.
  - We also provide the option for developers to customise themes, ensuring optimal accessibility for users with low/tunnel vision.

- What about rendering it to SVG instead of canvas, with a buffer area around and let the scroll take care of itself?
  - SVG or HTML adds a lot of DOM nodes when you are displaying lot of textual content.
  - Personally I found canvas easier to work with, scroll performance was better, less browser bugs, drawing was cheaper and scales for large content (using virtualisation or multiple canvas layers)

- How do you test or plan on testing performance to prevent regressions? I’ve yet to crack this nut in a way that makes me happy.
  - The Spreadsheet is powered by ReactJS and Konva.
  - React and Konva provides a Profiler and Devtools to measure performance and to prevent any un-necessary re-renders.
  - We also measure the Canvas FPS to make sure rendering is at max 60fps. The bottleneck we have identified is with scrolling large amounts of text, especially in large 42 inch 4K monitors, where FPS limits to 55-60fps. We do have some workaround planned for large monitors, by splitting the canvas into 4 layers.
  - In terms of regression, we use Cypress for most e2e testing, but the test cases are small as of now.

- Is it able to handle tables with 1, 000, 000+ rows?
  - Spreadsheet uses virtualisation to display data, ie only data viewable in a Row x Column viewport is displayed. This improves rendering performance.
- Data performance can be improved by 
  1. Lazy loading data or Infinite scrolling. We have a built-in async hook that does this. 
  2. Only save pointers to data that is being displayed. So if you have 1M rows, on the JavaScript side, you only load 100 rows in memory and when user scrolls, you can replace this rows with new data. This will make the browser happy. 
  3. Streaming data from the server similar to google sheets.
  - But to answer your question, we have a Max row limit of 1_048_576 and max column limit of 16_384

- I can't think of a single reason someone would pay $299 for "Non-commercial use" license to a library

- ## 📈 [Tinysheet | Hacker News_202110](https://news.ycombinator.com/item?id=28967514)
- Where is the data for this stored? 
  - It appears to be stored in the url. As you update the cells there's an encoded # variable that, when removed, wipes the table.
- And if you put the URL into a URL shortener, you can (ab)use it as cloud storage for your spreadsheet.
- But... URLs have a char length limit
  - And this has a cell limit. Perfectly aligned.

- I spent several minutes trying to figure out how to add columns or rows, but it turns out you can't. It's a 'tiny sheet', after all.

- 
- 

- ## [Excel Labs, a Microsoft Garage Project | Hacker News_202305](https://news.ycombinator.com/item?id=36081851)
- Some things in Excel have not improved since 2003, that should be fixed before toying with "AI" . For example, when importing a CSV

- The universal language and portability of a spreadsheet is really hard to beat.

- ## 📈 [Show HN: DataSheetGrid, an Airtable-like React component | Hacker News_202311](https://news.ycombinator.com/item?id=38228788)
- Two things I ran into:
  - Doesn't have column resizing built in (not a deal breaker for my use)
  - I wanted to disable the "select row or column by clicking in header or gutter" functionality. 
- This is nice, but it's missing a few of the killer features from things like Airtable or MUI DataGrid: sorting/filtering, row/column pinning, aggregation rows, pivoting, etc.
  - DSG was not built to compete on features, it was built to have the best UX/UI possible and be extensible. So you would have to implement those parts yourself.
- it looks very promising. It has range selection out of the box (a pro feature in some alternative solutions) and you can customize cells. 
- I wish every new thing coming out wasn’t React based
- DSG is not meant to manage your data like tanstack (filtering, sorting, paginating...), it is meant to give your users the best possible UI / UX to edit data (which tanstack does not do since it is headless). But those two work very well together actually, I should probably write an example.

- ## open sourcing my blazing fast DOM-grid
- https://twitter.com/GabrielPeterss4/status/1658546768240599041
- https://github.com/gabrielpetersson/fast-grid
- Resuses parts of DOM-tree to reduce expensive DOM mutations
- Own event loop to prioritize tasks. Never drops a frame
- Non-passive scrolling. Rows will never be seen rows loading into the UI while scrolling
- Custom virtualization and scrolling. Not limited by browsers 15 million pixel div height limit
