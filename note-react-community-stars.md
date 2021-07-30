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

- ## interesting optimization next.js does for React Hooks.__201811

```JS
// It converts this:

let [foo, setFoo] = useState(true);

// into

let { 0: foo, 1: setFoo } = useState(true);
```

- Why is object destructuring faster? Are they not both syntactic sugar?
  - "array destructuring" is actually Iterable destructuring, which makes it cost quite a bit more.
  - JavaScript array destructuring implicitly invokes the iteration protocol, which comes at a cost. Now that this pattern is becoming more common (React Hooks, anyone?), @v8js is optimizing it to minimize the overhead.
- There are some benchmarks in [this thread](https://twitter.com/_developit/status/1057636803354648582)
  - I always benchmark before tweeting. actually wrote a small vdom + hooks implementation to ensure it was representative.
  - if it's important to you, you can use this babel plugin that specifically optimizes hooks. don't write the numeric keys stuff!
- I would imagine most js bundles are still transpiled to es5 so it would end up being simple array index lookups. Maybe server rendering would be slowed down, if you transpile that with `node: current` but v8 have already announced they’re making this faster
  - indeed, I work with them and this suggestion came as a result of me looking through the optimization plans
- I feel this should be done by a compiler

- [Looks like this optimization is no longer worthwhile!__202107](https://twitter.com/jarredsumner/status/1420814310868013058)
  - Wow, nice. I didn't realize JSC and V8 had both landed the heuristic for this.

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
