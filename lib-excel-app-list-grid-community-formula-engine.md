---
title: lib-excel-app-list-grid-community-formula-engine
tags: [community, excel, formula]
created: 2023-11-12T16:47:52.424Z
modified: 2023-11-12T16:48:11.308Z
---

# lib-excel-app-list-grid-community-formula-engine

# guide

# discuss-stars
- ## 

- ## 
# discuss-formula
- ## 

- ## [Excel formulas in JavaScript | Hacker News_201404](https://news.ycombinator.com/item?id=7638879)

# discuss-reactivity
- ## 

- ## 

- ## 

- ## Here's a peek behind Causal's multi-dimensional spreadsheet calculation engine — a thread (for engineers) __202201
- https://twitter.com/lukaskoebis/status/1485944221169520645
- Causal is similar to Excel, with 3 core differences:
  - (a) instead of cells, you work with "variables" and write plain-English formulas like "Profit = Revenue - Cost"; 
  - (b) input variables can be uncertain (e.g. "10% to 20%") and Causal runs Monte-Carlo simulations to calculate the probability distributions of output variables
  - (c) variables can have dimensions (e.g. Revenue might be broken down by Product, Geography, and Time) and Causal automatically performs its calculations across all dimensions. Example: Let's say you have 1000 products, 10 geographies, 10*52 weeks, and want to run 100 Monte-Carlo samples. That means just for a single variable we have to execute 520M operations.
- Our first calculation engine was implemented in Typescript and ran in the browser. 
- The next iteration was a rewrite in Golang that sped up our engine by an order of magnitude by parallelising the calculations and having more control over memory allocations.
- Currently, we can handle models with millions of cells, but our customers will soon need billions. 
  - To get there we have to improve our in-memory cache, optimise our multi-dimensional data structures, compute the minimal set of numbers to render what the user requests, etc

- ## does your abstraction incorporate change over time? Eg:
- https://twitter.com/geoffreylitt/status/1632459743636717568
  - Reducing over a stream of increment events to derive a final count: yes, temporal
  - Recalculating a spreadsheet, by re-running formulas on current cell values: no, not temporal
- Turns out there are separate areas of work addressing those cases.
  - Functional reactive programming (FRP) models temporal processes
  - Self-adjusting computation (SAC) optimizes non-time-varying processes.
  - OK, so how do these relate to recomputing UIs..?? Subtle question.
- Anyway, I tend to agree w/ Minsky that SAC is a more useful model than FRP for much of UI.  Rerendering a UI = recalculating a spreadsheet.
  - OK, so how do we do that efficiently? This post by Lord is a fantastic survey of techniques:
  - [How to Recalculate a Spreadsheet – Lord.io](https://lord.io/spreadsheets/)
- if you want to understand SAC, an important system to know about is Adapton (http://adapton.org), by Matthew Hammer et al.
- I've also implemented a TypeScript version of miniAdapton if that helps. ~100 LOC for a demand-driven, memoized reactive graph of computations:
  - https://github.com/geoffreylitt/mini-adapton
- you might like differential dataflow, an implementation of research on incremental view maintenance

- Notion: I always hope to find a silver bullet algorithm for self-adjusting computation (the kind of reactivity Notion uses) that would make dealing with a big graph much faster, but no silver bullet has turned up yet.
- Curious, what kinds of reactive propagations end up slow in Notion?
  - Recently w/ Riffle we've moved away from Sqlite and instead using a relational database w incremental view maintenance as a way to go faster... wonder if that's a thing that could work for your app longterm
- Right now we're most of the way through making our reactive observations fine-grained – finding places we were subscribing to whole rows and switching them to  subscribe to columns of those rows or fields-inside-columns, to avoid unnecessary recomputation/rendering.
- This improved typing latency where we expected: for typing into popular rows like the current page block. But, the overhead of adding so many fine-grained nodes to our graph caused typing latency to regress at p95 across the board, most noticably on Android.
- This makes it harder to understand the tradeoff between simple graph with course-grained nodes, and more complex graph with fine-grained nodes.
- 👉🏻 Generally we debounce reactions to once per `requestAnimationFrame`, but during most typing events we synchronously force downstream dependencies to guarantee things like selection updates ContentEditable DOM writes happen during the event
  - There's plenty of obvious inefficiency in some of these reactions that show up in profiling, like O(DOM nodes) or O(text spans) scans that recompute something on the inside of their loop or could be memoized more – but those aren't new.

- I wonder if there is an equivalent of cache blocks for v8; jump between scopes too much and the “context switching” starts to dominate?

- ## [Spreadsheet is a software development paradigm | Hacker News_202104](https://news.ycombinator.com/item?id=26645253)
- 😩 To add to (usual/frequent) spreadsheet software as a database cons:
- No who when what
- No formula/value separation: Only trees, no cycles
- No named references 
- No (easy) functions
- No (easy) SQL-like
  - Views
  - Triggers
  - Default values
  - Constraints: Advisory at least, No linter
- No birdeye for a schema
- Shit typed
  - Even if you insist
- Theoretically these are all problems with Excel, not with spreadsheets in general.

- Excel is just reactive programming. One thing that I always thought was missing was the ability to do looping until a condition is met in Excel. It’s actual very possible if you enable “iterative calculation” in the settings. This will allow you to walk data structures and perform complex calculations until you reach a goal.

- I think two stated downsides have been somewhat addressed in excel in recent years:
  - The “high code duplication” downside has definitely been addressed in recent versions of excel, first with dynamic array formulas (which let you apply one formula to a number of cells, which can resize according to the data with use of unique/filter) and then with new expressions such as Let / Lambda.
  - Secondly Vlookup has been replaced with the faster, simpler and easier to read Xlookup. Using this with named ranges and dynamic arrays

- ## [How to implement a spreadsheet | Hacker News_201507](https://news.ycombinator.com/item?id=9940126)
- If you're interested in spreadsheets, don't miss sc, the Standard Unix Spreadsheet™ which nobody has ever heard of, originally written by James Gosling in the 1980s and is in Debian
- Emacs comes with a couple of built in spreadsheets: ses-mode supports emacs lisp formula in cells, org-mode tables allow simple formulas in table cells.

- You can use OpenDocument Format files. These are supported by most spreadsheet implementations. It comes in two variants: 1) a zip file with XML inside 2) a single XML file

- Every time I read about reactive patterns, I hope that some data dependency or cells like behavior is included, and every time it's just some thin wrapper around basic pub/sub.
