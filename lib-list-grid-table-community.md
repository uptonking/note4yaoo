---
title: lib-list-grid-table-community
tags: [community, grid, list, table]
created: '2021-06-24T08:48:24.911Z'
modified: '2021-06-24T08:48:54.797Z'
---

# lib-list-grid-table-community

# pieces

- ## The new GitHub Issues project tables is built on @tannerlinsley ’s React Table library. 
- https://twitter.com/_clem/status/1407754748799995908
  - It has been an excellent tool in enabling fast iteration and a high level of control with *just enough* free stuff out of the box.
- It makes sense to ask why we didn’t opt for one of the “kitchen sink” table libraries out there that give you state and UI out of the box.
  - This is an important investment for GitHub, and we knew we’d need a very high level of control over every minute aspect of the experience.
  - React Table, on the other hand, gave us enough structure to get to an MVP quick early on that has served as our foundation the whole way through, and we can still try out crazy ideas in this thing because outside of data and state, the framework doesn’t really care what we do.
  - So really the point here is that I think we’re glad we went with something in that sweet spot of some free features and full control, instead of tons of free features and just a big list of settings to tune.
- wait I thought GitHub was all web-components
  - We have a lot of web components! But we’re by no means *all* web components. For this very user-interaction-heavy and client-side-state-heavy project, React just made a lot of sense.

- ## A new GitHub Issues is coming this Fall, with better ways to plan, track, and manage projects.
- https://twitter.com/github/status/1407731478096756739
  - https://github.com/features/issues
  - github的issues依靠用户量，要超越atlassian全家桶已经势不可挡了

- ## React Aria's data table component is coming along nicely!
- https://twitter.com/devongovett/status/1407747623268671490
  - Keyboard navigation to rows, cells, and focusable elements within cells
  - Multi selection
  - ARIA selection announcements
  - Sorting
  - Tiered headings
  - Async data loading + infinite scrolling
  - Typeahead
  - And more!
- We sometimes have tables inside a table and expanding rows. Is that something you plan to implement?
  - Yeah, we will eventually support expanding rows. We would follow the ARIA treegrid pattern for that
- Does it have the "basic" features tables proposed as in react-virtualized or react-windows?
  - Yes! Our own tables in Spectrum are all virtualized. It should work with any virtualization library. We'll add some examples to the docs. Eventually we might make our own virtualizer public as well.
