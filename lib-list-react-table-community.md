---
title: lib-list-react-table-community
tags: [community, react-table]
created: '2021-02-24T10:09:46.820Z'
modified: '2021-05-13T02:53:57.772Z'
---

# lib-list-react-table-community

# guide

- tutorials
  - [Design Data Tables with Real Tables: Part 1](https://learnreact.design/2020/02/08/design-data-tables-with-real-tables-part-1)
  - [Data Grid (Table) Framer package](https://packages.framer.com/package/lintonye/data-grid-table)
    - https://github.com/lintonye/tables
# react-table-rerender
- ## [after I edit a single cell, I see the entire table being re-render.](https://github.com/tannerlinsley/react-table/issues/2824)
- You're right that that some if not most of the methods/functions attached to rows and cells are being created on every render. 
  - I truly wish it was possible to alleviate this with the v7 architecture and this makes it almost impossible to memoize the component itself like you said without also calling all of the functions first, then memoizing on their results. This even plagues(困扰、折磨) my own code in a few places
- But there is good news! I'm currently working on v8 which will not have this issue. 
  - It's taken a lot of internal refactoring and only a few breaking changes, but Row, cell and column models along with all of their methods and properties will all be stable by default. 
  - This will allow you to safely memo, useMemo and useCallback any of their properties. 
  - As of today, the rerendering story in v8 still uses a top-level rerender that propagates down the entire table tree and will, like you wish you could do today, incentivize memoization of components and computation where necessary to improve performance. 
  - It's possible that I explore more granular means of render signaling like subscription callbacks or even atom-based state like jotai, but that would significantly hinder(阻碍) the table's external controllability and complicate the innards quite a bit.
- With the stability changes I've already made though, both the library's ability and your ability to memoize and optimize when needed is at least there now. 
  - Already in v8, I've been able to convert most of the up-front repeated instantiation of the row/cell API to be lazily-invoked memoized getters, which should drastically improve performance.

- ## [[Performance] All rows are re-rendered on selecting row](https://github.com/tannerlinsley/react-table/issues/1496)
- In a nutshell, rerenders are not bad at all. They are what keep your UI up to date. Expensive rerenders however, can become a problem very quickly. Luckily, React Table v7 is built on this exact premise that rerenders are good, but expensive rerenders are bad.
  - React Table is rerender heavy. This ensures things stay up to date.
  - React Table doesn't use PureComponent or rerender bailouts. If you want to use these in your own markup, feel free to do so, but at your own risk. In most, if not all, scenarios you would do this, it could probably be solved by using a useMemo or useCallback
  - React Table uses extensive memoization, caching and change-detection to ensure that rerenders are extremely performant.
- Moral of the story: Only worry about rerenders if they are expensive or degrading performance.
# pieces
- ## 

- ## 

- ## 

- ## So, turns out react-tracked is not a good choice as a way to build a context for react-table. 
- https://twitter.com/code_tank_dev/status/1511215041856614406
  - The table instance doesn't get notified of changes (eg. isSorted). Any idea why that could be?
