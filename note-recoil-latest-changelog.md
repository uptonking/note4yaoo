---
title: note-recoil-latest-changelog
tags: [changelog, react, recoil, state]
created: '2020-07-06T03:26:13.606Z'
modified: '2020-07-14T10:39:49.095Z'
---

# note-recoil-latest-changelog

# guide

- ref
  - https://github.com/facebookexperimental/Recoil/blob/master/CHANGELOG.md
  - https://recoiljs.org/blog

# changelog

- 0.0.10-20200618
  - Fix exports for snapshot hooks
- 0.0.9-20200617
  - TypeScript support now rolled into recoil package
  - Recoil Snapshot API for observing and managing global Recoil state.
  - Fix updaters in useRecoilCallback() getting current state
- 0.0.8-20200530
  - atomFamily and selectorFamily
    - these provide a standard way to create atoms and selectors using memoized functions.
    - Compared with doing this yourself, in the future these will help with memory management.
  - noWait, waitForNone, waitForAny, waitForAll
    - helpers for concurrency and other advanced logic in async selectors.
  - constSelector and errorSelector
    - selectors that always evaluate to a constant or always throw an error.
  - readOnlySelector
    - wraps a read-write atom or selector in a read-only interface, for when you need type covariance.
