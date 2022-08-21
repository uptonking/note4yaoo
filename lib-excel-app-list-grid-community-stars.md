---
title: lib-excel-app-list-grid-community-stars
tags: [community, grid, list, table]
created: 2021-06-29T12:45:19.734Z
modified: 2022-08-21T10:15:06.225Z
---

# lib-excel-app-list-grid-community-stars

# discuss-stars

- ## what is the best way to implement in a @reactjs app a todo list with a huge number of items more than 10k
- https://twitter.com/sseraphini/status/1409841471491031042
  - so that when 1 todo is marked as done does not rerender the whole list of todos?
  - react-virtual + recoil?
- How will you show 10k items at once?  Each item is 1px tall?
  - You're only going to have in memory only a subset of items, & on screen a smaller subset.
  - That many items I'd require tags & date &/or priority ranges to display. Too much cognitive overload otherwise.
- React-window is a successor of react-virtualized.
- I truly advise against Recoil. I've used it in a project for testing, it is really, really immature and it has a pretty high number of bugs
- I'd say virtualize the list and `React.memo` the list items should be enough.
