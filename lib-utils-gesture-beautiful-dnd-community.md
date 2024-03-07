---
title: lib-utils-gesture-beautiful-dnd-community
tags: [community, react-beautiful-dnd]
created: 2023-09-03T13:21:12.994Z
modified: 2023-09-03T13:21:26.939Z
---

# lib-utils-gesture-beautiful-dnd-community

# guide

# discuss-stars
- ## 

- ## 

- ## 
# discuss-news-pdnd
- ## 

- ## 

- ## 🌰 Pragmatic drag and drop 1.0 adds cross browser support for dragging into an out of iframes _202403
- https://twitter.com/alexandereardon/status/1765523608682795227
  - 示例动画
  - Some applications leverage iframes for sandboxing (eg for addons), Site builders, etc
  - I'm pretty hyped about this, as achieving something like  this on your own is really hard. pdnd makes it real safe and straight forward to set up

- postMessage?
# discuss-pdnd
- ## 

- ## 

- ## 
# discuss-rbd-issues
- ## 

- ## 

- ## [hello-pangea/dnd does not work with react-virtuoso if the rows are different heights](https://github.com/hello-pangea/dnd/issues/648)
- Is there any combination of dnd libraries + virtualized list libraries that allow for dragging cards with varying heights? Neither react-window or react-virtualized worked either

- [Support dynamic height in react-virtualized list](https://github.com/atlassian/react-beautiful-dnd/issues/1971)

- [issue with `react-beautiful-dnd` + `react-virtualized` + `cellMeasurer` for dynamic height list](https://github.com/atlassian/react-beautiful-dnd/issues/2253)
  - I converted your example to React.18, typescript, hooks, and the more supported @hello-pangea/dnd and still the issue persists.

- [Cannot get React-Virtualizer to work with with React-Beautiful-DND (Demo Included)](https://github.com/atlassian/react-beautiful-dnd/issues/2098)
  - here is the demo of dynamic height per row with react-beautiful-dnd + react-virtualized + cellMeasurer

- ## [Allow dynamic additions/removals of dimensions during a drag](https://github.com/atlassian/react-beautiful-dnd/issues/484)
- I was able to make this work with a very simple workaround. 
  - What I did was to add `onBeforeCapture={recalculateHeight}` , that function runs before `OnDragStart` , so within `OnBeforeCapture` you must change the dimesions of the child elements that are going to be calculated. 
  - For example: `const recalculateHeight = ()=>setShowOnlyInput(true);` .
  - what `setShowOnlyInput` does is that it changes the elements to be displayed of each li item, for example by showing only the title input and no other inputs

- ## [Inserting item during drag in virtual list(For expand/collapse logic)](https://github.com/atlassian/react-beautiful-dnd/issues/2063)
- [Lazy loading bug](https://github.com/atlassian/react-beautiful-dnd/issues/2014)
- react-beautiful-dnd doesn't support dynamic changes since version 11, unfortunately

- ## [Virtualized nested list (Cannot find droppable entry with id(uuid))](https://github.com/atlassian/react-beautiful-dnd/issues/2196)
- [Cant dragging nested items with Virtualization](https://github.com/atlassian/react-beautiful-dnd/issues/2157)

# discuss-rbd
- ## 

- ## 

- ## 

- ## [Drag and drop within a canvas?](https://github.com/atlassian/react-beautiful-dnd/issues/2065)
