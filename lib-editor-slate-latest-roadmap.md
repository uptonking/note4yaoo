---
title: lib-editor-slate-latest-roadmap
tags: [roadmap, slate-editor]
created: 2022-05-15T18:43:25.412Z
modified: 2023-02-05T19:03:12.723Z
---

# lib-editor-slate-latest-roadmap

# guide

# discussions-issues

## [Perf: decorations propagated like selectors](https://github.com/ianstormtaylor/slate/pull/4997)

- Instead of sending context updates down the react tree to all components for the decorate function, this approach follows more closely the pattern of `useSlateSelector` (update: refactored both to use the new official `useSyncExternalStoreWithSelector` hook) which means that it does not require additional components in between, and simply registers listeners that use the decoration range comparison to check for a change before choosing to rerender.
# more
