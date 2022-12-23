---
title: lib-excel-ag-grid-community-stars
tags: [ag-grid, community]
created: 2022-02-27T18:14:17.561Z
modified: 2022-08-21T09:54:22.078Z
---

# lib-excel-ag-grid-community-stars

# discuss

- ## 

- ## 

- ## 

- ## 

- ## any table that implements row virtualisation correctly won't have a limit with rendering. The bottleneck is browser heap space.
- https://twitter.com/niallcrosby/status/1605858392462999555
  - Sorting is done with JS core sort functions, so hard to do that wrong! Also hard to do a filtering algorithm badly! However a grid with 1, 000+ rows is pretty useless to humans
  - That's where row grouping is magic! AG Grid has massive performance tweaks with its grouping, eg if grouping and sort is changed, only expanded groups are actually sorted.
  - In summary, take AG Grid as the gold standard for Enterprise Component (with a UI), and TanStack Table as gold standard for headless alternative.

- ## Today we enhanced AG Grid's React performance by NOT using React... ... 
- https://twitter.com/niallcrosby/status/1496161941684985864
  - we were setting DOM Aria attributes a LOT in the Grid, and it turns out it's quicker to set them directly rather than use JSX!  
  - Lesson? Know your tools!

- ## The challenge with Data Grid's is the sheer interconnected complexity. 
- https://twitter.com/niallcrosby/status/1493964065714094083
  - You can't write one feature (eg Sorting) without considering how that feature impacts all the other features (Filtering, Editing, Grouping, Pivoting, etc). 
  - Adding features grows the complexity exponentially.
