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
