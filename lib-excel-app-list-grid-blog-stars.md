---
title: lib-excel-app-list-grid-blog-stars
tags: [blog, grid, list]
created: 2022-06-12T21:57:03.315Z
modified: 2022-08-21T10:14:58.104Z
---

# lib-excel-app-list-grid-blog-stars

# guide

- [14 天开发一个web Excel - 第1天](https://juejin.cn/post/6924172177751638023)
  - 实现一个有虚拟滚动的 canvas 表格
  - https://jsfiddle.net/zhangchi/fgu0rm23/1/

- [Canvas 渲染优化策略](https://juejin.cn/post/6924171842483650574)
# blogs

## 🪟🌰🌲 [Building a High Performance Spreadsheet in the Browser_202306](https://wraptext.equals.com/high-performance-spreadsheets-in-the-browser/)

- Before getting to the problem though—let's clarify what we mean by Formats.
  - The word might conjure up colours, bold text, etc
  - Think of how you can mark ranges in a spreadsheet as being plaintext, number, currency, or date
  - That's essentially a layer of "runtime type information" which can be set manually by a user per-cell or across wide ranges, but also dynamically changes and propagates every time you edit a sheet
- Pulling out our performance analysis tools and diving in, a recurrent theme arose: some of the most widespread slowness wasn't coming from the actual formula calculations, ingestion of large amounts of data, or any of the "hard problems" we knew we'd have to tackle; it was coming from accesses to the Formats system.

- I'll lay out the historical journey of Format data structures as it evolved over time from prototype to production
- Proof of concept, early 2021: The first version stored per-cell metadata for everything—the cosmetic stuff, the wacky runtime types, etc. This works! Until it doesn't. 
  - It's really common for a spreadsheet power user to select entire rows and columns—which correspond to large areas of cells—and make changes to all of it. 
  - With larger datasets, this resulted in a pretty classic write fan-out problem as every cell needed to be updated—not something you want to have to deal with on a user click.
- Beta launch, mid 2021: A mitigation on that was to store either per-cell, per-row, or per-column data—so if you changed a whole column, we just made one write, rather than a bunch. 
  - This saves work in some special cases, but if the write doesn't cover a whole row/column, you're out of luck—you still have the same write problem.
- Early 2022: As the write performance became more problematic, a new approach was tried: using an append-log-based approach, where every write to a range of cells was recorded. 
  - Multiple writes could, and did, partially overlap with each other; that was resolved by reader code on a last-write-wins basis.
  - This last approach optimised for writes over reads and resolved the write problems by allowing for quick writes of ranges of any shape. 
  - But as a workbook grew, the read cost mounted steadily over time, resulting in the kind of painful sluggishness that Chris ran into when building his financial models.
- We knew that we could likely optimise our existing code further, add smarter caching and preloading, and maybe squeeze out an improvement.
  - But if your data structure is wrong, all the micro-optimisation in the world isn't going to let you scale up to 10x your current data volumes 

- What worked in practice ended up having 3 basic elements:
- 1) For core storage: we stored the rectangles in-memory as simple JS Objects in Maps keyed by numeric IDs.
  - We've learned this many times over, but working with primitive JS objects can be extremely fast if you do it right.
- 2) For read accesses: we used an R-tree 🌲 spatial index of all the rectangles. This is a slight denormalization, but well worth it.
  - if you have data corresponding to points or rectangles, r-tree is good for fast queries of the form "give me all data intersecting this range." 
  - The core concept is fairly simple: you build a tree where every leaf node is one of the rectangles you're storing, and the non-leaf nodes are the minimal bounding boxes containing them.
  - As with every real world data structure, there's quite some tricksiness to make it performant, though.
  - we ended up using the excellent rbush
- 3) For writes: we would merge together rectangles where possible, to avoid ending up with millions of small ones when a few larger ones would do.
  - from a computer science point of view, this is a "solved problem": [Graph-Theoretic Solutions to Computational Geometry Problems](https://arxiv.org/abs/0908.3916)
  - We didn't do that. This algorithm gives a guaranteed "perfect pack, " but scales with ~O(n3/2). it's complex!
  - We chose a far simpler consolidation algorithm: we repeatedly merge any adjacent rectangles which precisely share an edge, and just keep going until we can't merge any more.
  - There's a real tradeoff in this—we're no longer guaranteed a "perfect pack." Since it's a greedy algorithm, it may get stuck in local maxima; you can design pathological inputs of awkwardly interleaved inputs, like the teeth of a key, which it'll fail to merge due to its naivety.
  - But on the plus side, its worst-case runtime is only O(n). That pays for a lot of imperfect packings.
  - And in practice, we've observed exactly zero pathological(非理智的；病态的) situations resulting from this in production, while gaining the benefit of simple code and fast writes.

- Having fast access patterns for this data also allowed us to simplify and optimize several other features built on top (sorting, filtering, data imports from SQL, etc.) which previously had to hack around the limitations of the old data modeling.

- Every system has limits; at some point, I'm sure we'll have to replace this one too. But based on our projections, it should serve us long enough to scale into the millions of rows of data that we're targeting for the next generation of the app.

## 🪟🌲 [We built a spreadsheet engine from scratch. Here’s what we learned. | GRID_202206](https://medium.grid.is/we-built-a-spreadsheet-engine-from-scratch-heres-what-we-learned-e4800ab9edf1)

- we’d need a lightning-fast spreadsheet engine, compatible with Excel and Google Sheets and capable of running entirely in the browser

- The basics - it all depends
- a spreadsheet modeler declares a relationship between data elements that live in cells in a two-dimensional grid.
- To determine the order in which to do these calculations and identify which cells need to be recalculated if a value is changed, a spreadsheet engine must maintain a dependency graph. This is a directional graph with a node for every cell with a formula and links to the cells they depend on (refer to).
- Such a dependency graph is at the heart of any spreadsheet engine.

- Parsing, functions and operators
- In order to build the dependency graph and be able to calculate a cell’s value, each cell with a formula needs to be parsed. For this, we need a parser.
- A formula can consist of a combination of any of the following: constants/references/operator/functions
- These must follow a set of rules in the order and way they appear. These rules determine the syntax of the formula language.
- this language doesn’t formally have a name, but it should rightfully be called Excel formula language.
- when I started investigating GRID as an opportunity about 4 years ago I ran analysis on a few spreadsheet corpuses. In about 40, 000 spreadsheets only 109 of these functions were ever used! We used this information to prioritize the functions we initially implemented.

- A few words about implementation
- The bulk of it is written in pure JavaScript. 
  - Lately we’ve been writing parts in Rust, compiling into WebAssembly. 
  - As performance is so important, this feels like an ideal project for WebAssembly, but the fact of the matter is that JavaScript — which gets compiled to machine code on the fly — is also lightning fast so the performance advantage we have seen with WebAssembly have not been significant.
  - we still maintain a fallback JavaScript implementation for the WebAssembly code
- To be clear, open source implementations of spreadsheet engines exist, such as Formula. JS, POI and OpenOffice. 
  - We have sometimes looked at these but we’ve mostly decided that they fall short of our quality standards, or are incomplete
  - So currently, external libraries in the engine are only used for number formatting and statistical routines to draw from probability distributions, used in statistical functions like NORM. DIST.
  - That said, we do use external libraries for linting and testing the engine in a large suite of automated and scheduled tests that ensure the quality and compatibility

- Advanced features and finer details
- Spilling: While most spreadsheet functions return single values, some can return arrays. Until recently, this was merely an internal consideration in calculations, but in 2018 Excel introduced dynamic array functions that can result in so-called “spilling”. This means that returned arrays will flow (spill) into adjacent cells. 

- Optimizations
- many of the optimization opportunities are on the dependency graph level, where clever avoidance of unnecessary work can dramatically improve performance. 
- 👉🏻 Conditional branches: 
  - While conditional functions — such as IF — technically depend on every cell they refer to, only branches whose criteria are met, need to be evaluated.
- 👉🏻 Large ranges: 
  - Ranges that hold tens or even hundreds of thousands of cells, will quickly bloat memory usage and hurt performance if every cell is represented individually in the dependency graph. 
  - Say you have a lookup function like =VLOOKUP("Mickey Mouse", A2: D10000, 4) (it looks for a row matching the string “Mickey Mouse” in column A, and returns the value from column D in that same row). We don’t want this reference to be represented as ~40, 000 individual dependencies, but rather treated as one, which is what our engine does. 
  - It then uses a so-called R-Tree🌲 to efficiently find all range references that cover a particular cell.

- What’s next?
- while we’ll keep improving on performance, implement some of the remaining functions and eliminate discrepancies(差异；不一致) from the traditional spreadsheet engines, we’ve reached a stage where the most interesting development goes beyond what existing engines are capable of. 
- Three areas we’re currently working on or laying the groundwork for are:
  - Group and aggregate: Building into our engine capabilities to transform row-level data. Traditional spreadsheets tackle this use-case mainly through pivot tables, but with GRID’s separation of presentation from the data and logic in the spreadsheet, we see opportunities to build this into the spreadsheet itself
  - Compatibility mode: Our Excel-first approach has served us well, but the Google Sheets audience is also important to us, and currently we don’t offer them quite the same level of compatibility as Excel users. We plan to solve this by making our engine aware of which software a model originated in and simply doing “the right thing” for each.
  - Our own functions: We already have a set of functions in our engine that are specific to GRID, yet none have been exposed externally.many opportunities on that front have to do with the unique nature of GRID’s engine running as a part of a web document. Our — currently experimental — canvas element (see it in action here) will also come with a set of unique functions that will allow spreadsheet users to dynamically draw and make graphical representations they’ve up until now never even dreamt of.
# more
- [自研一个excel应用，需要支持哪些基本功能?](https://juejin.cn/post/6921257011560742919)
