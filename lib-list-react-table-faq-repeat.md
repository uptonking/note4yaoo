---
title: lib-list-react-table-faq-repeat
tags: [faq, react-table, repeat]
created: 2021-11-21T18:27:10.862Z
modified: 2021-11-21T18:27:22.494Z
---

# lib-list-react-table-faq-repeat

# guide

# faq-repeat

## 选用哪种布局 

- useAbsoluteLayout
  - adds support for headers and cells to be rendered as absolutely positioned divs (or other non-table elements) with explicit `width`. 
  - this becomes useful if and when you need to virtualize rows and cells for performance.

- useBlockLayout
  - adds support for headers and cells to be rendered as `inline-block` divs (or other non-table elements) with explicit `width`.
  - this becomes useful if and when you need to virtualize rows and cells for performance.

- useFlexLayout
  - adds support for headers and cells to be rendered as `inline-block` divs (or other non-table elements) with width being used as the `flex-basis` and `flex-grow`. 
  - This becomes useful when implementing both virtualized and resizable tables that must also be able to stretch to fill all available space.
# discuss

## [I *could* technically implement time-slicing for the CPU intensive agnostic core features of #ReactTable.](https://twitter.com/tannerlinsley/status/1480973988260048899) 

- Worth it? Is anyone using React Table to filter/sort/group 100's of thousands of rows and running into input lag?
- While I may still try this, the short answer here that while scheduling would improve the responsiveness of a table, the 2 following approaches would also, but with much less complexity to the overall system:
  - Use the server. 
    - Move your compute cycles to a faster or more naturally distributed system/language
  - Use web workers. 
    - At some threshold, serialization speed to and from a worker will be faster than main threaded filter/sort/group/aggregate

- If you've ever peeked at React's scheduler, it's pretty intense, especially given that it could be fully replaced by the platform in the future. While they may generalize and open source it in the future, it's definitely not planned.
  - And while I could spend a long time reworking it to fit my use-case, I wouldn't do it justice. 

- Combination of React-table v8 and React 18 may improve this issue at some level.
  - Maybe some things, but I'm not sure how the React 18 scheduler could possibly slice up a synchronous call to filter/sort/group/aggregate a bunch of data. I am pretty sure I would need to make React Table's internal work "incremental/resumable", and have it also use a scheduler.
  - I could be wrong (hopefully, TBH), but at some point, the update to the table would have to happen. AFAIK, if it exceeded the FPS goals, it would likely timeout in the scheduler after its respective priority duration and be forcefully completed, causing some jank)

- I do filter through a lot of data, but it's all done externally to the table so it probably doesn't apply here

- Are you thinking of worker processes or some sort of exec interleaving on the single thread js? Very interested.
  - Resumable jobs/queue style single threaded scheduling. A lot like React fiber + scheduler.
- You mean the basic filter sort method of arrays in react?
  - No, the custom sort/filter/group features of react table.
- Like using react 18 features?
  - No this is framework agnostic code
