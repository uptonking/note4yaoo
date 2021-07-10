---
title: note-react-community-stars
tags: [community, react]
created: '2021-06-09T00:47:18.180Z'
modified: '2021-06-09T00:47:37.142Z'
---

# note-react-community-stars

# discuss-stars

- ## 

- ## 

- ## 

- ## 

- ## 6 techniques for managing large datasets in React
- https://twitter.com/housecor/status/1337073677893070849
  1. Pagination
  2. Lazy loading / Infinite scroll
  3. Windowing(react-window)
  4. Eliminate needless renders
  5. Implement uncontrolled components
  6. Analyze performance via the React dev tools
- Which is better pagination or infinite scroll? Infinite scroll is becoming a trend at my work place.
  - Pagination is preferable for a finite dataset where people are focused on finding something specific. 
  - Infinite scroll is preferable for more casual scrolling.
- for windowing, i found it to be perform even better by also recycling components keys
  - we assign keys to react components then reuse them for items that appear/disappear in viewport. it performs better because instead of unmounting and mounting components in viewport (expensive), we "recycle" components by just updating their props
- Caching / memoization
- Wonder if large dataset is really needed. Avoid problem rather than looking for a solution 
