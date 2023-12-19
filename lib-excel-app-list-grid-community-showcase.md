---
title: lib-excel-app-list-grid-community-showcase
tags: [community, data-grid, excel, showcase]
created: 2023-05-21T15:43:54.248Z
modified: 2023-05-21T15:44:39.196Z
---

# lib-excel-app-list-grid-community-showcase

# guide

# discuss
- ## 

- ## 

- ## 

- ## 

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

- ## 🪟 [Tinysheet | Hacker News_202110](https://news.ycombinator.com/item?id=28967514)
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

- ## 🪟 [Show HN: DataSheetGrid, an Airtable-like React component | Hacker News_202311](https://news.ycombinator.com/item?id=38228788)
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
