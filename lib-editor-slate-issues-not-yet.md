---
title: lib-editor-slate-issues-not-yet
tags: [issues, not-yet, slate-editor]
created: 2022-05-15T18:44:35.624Z
modified: 2023-02-05T19:03:12.723Z
---

# lib-editor-slate-issues-not-yet

# guide

# architecture
- [try to prevent re-rendering at the Leaf level](https://github.com/ianstormtaylor/slate/issues/2051)
  - Our current approach has a lot of benefits in terms of simplicity.
  - But this "always re-render" approach also has some downsides.
  - I think it may be possible to re-render at the `<Editor>` level for each change, but abort rendering at the `<Leaf>` level
  - This would be different from our old approach in that it would allow us to gain the "always re-renders" benefits higher up the tree, so that custom nodes can still have total flexibility in what they render. 
  - But it would hopefully give us the benefits of "selective re-rendering" that come from allowing the browser's native DOM editing to occur.
  - Would need someone to research it.
# not-yet
- [Getting the "word" under the cursor is really, really complicated.](https://github.com/ianstormtaylor/slate/issues/4162)

- [vanilla Slate - removing the React dependency](https://github.com/ianstormtaylor/slate/issues/4302)

- [Preact implementation](https://github.com/ianstormtaylor/slate/issues/2599)

- [Normalization for initial value](https://github.com/ianstormtaylor/slate/issues/3465)

- [setNodes does not work for inline nodes](https://github.com/ianstormtaylor/slate/issues/4745)
# more
- [Modify Text interface to be compatible with "universal syntax tree" (unist)](https://github.com/ianstormtaylor/slate/issues/4378)
  - https://github.com/JonasKruckenberg/slate/tree/fix-text
