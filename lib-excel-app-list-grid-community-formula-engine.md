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
- 
- 
- 

- ## 👥🪟📕 [Efficient and Compact Spreadsheet Formula Graphs | Hacker News_202302](https://news.ycombinator.com/item?id=34800138)
- cool! The authors exploit the fact that neighboring cells often have similar formulas to compress the evaluation graph.
- This seems odd to me. This is basically just ways of finding database-esque tables in spreadsheets to then leverage for vector/matrix operations.
  - It is a non-problem for anyone who really cares about performance as they've probably already realised they can just use a database some efficiently programmed transformations.
- Being able to have intricate computation definition being user-modifiable is a big feature. I have successfully 'appified' such Excel sheets in the past, only to be recognized as the new business rule maintenance guy. I no longer do that anymore: I identify moving parts, and these stay in the Excel world instead of going into the DB or a config file. I do clean the inputs and harden access control though.

# discuss-dataflow/reactivity
- ## 

- ## 

- ## 

- ## 🤔 [How to Recalculate a Spreadsheet | Hacker News_202011](https://news.ycombinator.com/item?id=25039393)
- [How to Recalculate a Spreadsheet – Lord.io](https://lord.io/spreadsheets/)

- Recalculating a spreadsheet efficiently is the same problem as compiling source code.

- Topological sorting has many applications. 
  - It's a DAG-computing framework in JS that allows you to listen to updates in a compute graph. It's a set of legos that I used to build both a MobX clone and a React clone
  - React and MobX are actually the same thing mathematically: reactive DAGs, so they can both be built using the exact same abstraction.

- If you're in TypeScript/JavaScript world, check out HyperFormula. There's a summarized design document in the documentation that explains the AST, dependency graph, formula evaluation and lazy CRUD operations.
  - We concentrate on making it a general purpose calculation engine and bring value by adding more formula functions (now there are about ~200 of them).
  - It should be fairly easy to make any integration.

- The dependency graph is why you should always prefer INDEX over OFFSET, unless you really can't avoid it. Every instance of OFFSET in your sheet is recalculated after each cell change. I learnt that the hard way.
  - Article doesn't explain the issue, but OFFSET lets you access cells that aren't referenced in the formula.
  - For example, OFFSET(B2, 1, 1, 1, 1) is a live reference to cell C3, which means you can use functions like COLUMN to investigate the range. C3 shows up nowhere in the formula, so there's no non-volatile way to implement it.

- While it's cool to see the CS theory used to optimize spreadsheet calculations, it also shows some important points. You can ship the first version with a poor algorithm that works. Performance improvement matters to users, but after doing what they need correctly. If you don't lead all the way to a solid solution you will be replaced by someone who does.

- The reactive programming model (or whatever you call it, honestly don’t know) is at the core of so many great tools and products - eg Terraform/Pulumi, Kubernetes, React, Mobx, Observable...

- React Hooks reminds me a lot of spreadsheets. Change a dependency and everything needs to be recalculated that depends on it and so on.

- ObservableHQ notebook works like this (for arbitrary JavaScript)

- I've always thought that these "dependency"-driven recalculations was akin to functional programming paradigms. Or am I misunderstanding functional?
- excel is like pure FP in that
  - everything you write is an expression that yields a value
  - those expressions are "pure"/"referentially transparent" bc there's no way to do side effects (like writing to another cell)
- the whole "recalculate value if any dependency changed" thing would probably fall more under "reactive" systems - you need the notion of inputs that a user can change.
  - but you're right that efficient recalculation is enabled by the calculations being side-effect-free! we know that changing a cell can only influence cells that reference it, so we only need to recalculate those, not the whole spreadsheet!

- so basically a DAG
  - Excel allows for cyclic dependencies.

- ## [Dealing with massive data structures in roguelikes : roguelikedev](https://www.reddit.com/r/roguelikedev/comments/xxiu4b/dealing_with_massive_data_structures_in_roguelikes/)
- I'm working on a game that has a silly scale (think milions of objects in a billion cube units having to talk among themselves all the time).
  - A data structure that has made my life much easier is the kd-tree. It's super easy to implement and allows for very fast lookups.

- ## [I'm stuck for reactive incremental computation. : ProgrammingLanguages](https://www.reddit.com/r/ProgrammingLanguages/comments/w8kjfl/im_stuck/)
- I would look into spatial trees (like quadtree, a 2d generalisation of binary tree, or r-tree (a n-dimension generalisation of b-tree).
  - I'm trying to understand what you're doing, and I think your spreadsheet essentially acts like a single giant 2d database table, with (i assume) dynamic typing (ie you can put any type of value in any cell).
  - In that case, assuming you have a well-defined total ordering for the values that can go in the cells, then maybe you could have a r tree acting as a single index for the entire spreadsheet.
  - You'd have to keep it updated whenever you change anything in the spreadsheet (which should be efficient since it's a tree) and in return it would allow you to quickly look up elements inside any rectangular range of cells, as well as finding their min/max values.
- Your understanding is correct and your suggestion sounds viable. I feel much better now, thanks! If `Max(a:b)` can be evaluated efficiently in log time using the single big index, then I guess I don't even need to worry about incremental evaluation yet.

- You might be looking for differential dataflow

- ## 🌰 Here's a peek behind Causal's multi-dimensional spreadsheet calculation engine — a thread (for engineers) __202201
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

- ## 🌰🪟 [A spreadsheet in fewer than 30 lines of JavaScript, no library used | Hacker News_201311](https://news.ycombinator.com/item?id=6725387)
- http://jsfiddle.net/ondras/hYfN3/
