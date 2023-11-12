---
title: lib-excel-app-list-grid-community-stars
tags: [community, grid, list, table]
created: 2021-06-29T12:45:19.734Z
modified: 2022-08-21T10:15:06.225Z
---

# lib-excel-app-list-grid-community-stars

# guide

# discuss
- ## 

- ## 

- ## 

- ## 

- ## After working on CSV parsing for the past two months, I'm convinced that 98% of the time spent on building a CSV reader is dealing with semi-broken files.
- https://twitter.com/holanda_pe/status/1650760335823970304
- yeah, same as with html where anything remotely resembling html was rendered as well.

- Let us all promote Parquet as alternative together 
  - Non-programmers just love their CSVs
- I understand why it's popular. Portable, easy to understand, but error-prone and text-based. If we have better tools and integration into common tools, i.e. Excel, adoption would be much higher. Benefits are obvious: speed, type-safety, compression.

- ## 💥 what is the best way to implement in a @reactjs app a todo list with a huge number of items more than 10k
- https://twitter.com/sseraphini/status/1409841471491031042
  - so that when 1 todo is marked as done does not rerender the whole list of todos?
  - react-virtual + recoil?
- How will you show 10k items at once?  Each item is 1px tall?
  - You're only going to have in memory only a subset of items, & on screen a smaller subset.
  - That many items I'd require tags & date &/or priority ranges to display. Too much cognitive overload otherwise.
- React-window is a successor of react-virtualized.
- I truly advise against Recoil. I've used it in a project for testing, it is really, really immature and it has a pretty high number of bugs
- I'd say virtualize the list and `React.memo` the list items should be enough.

- ## is there a company building a meta-spreadsheet-api that abstracts around google sheets / notion / coda / airtable / etc? or a module that does that?
- https://twitter.com/tmcw/status/1599893497850757121
- Curious, what’s the end product/interface where you want to consume this?
