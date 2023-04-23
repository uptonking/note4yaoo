---
title: lib-utils-gesture-dnd-kit-community
tags: [community, dnd-kit]
created: 2023-04-23T13:30:42.456Z
modified: 2023-04-23T13:30:54.152Z
---

# lib-utils-gesture-dnd-kit-community

# guide

# discuss
- ## 

- ## 

- ## [Separate context into Public and Internal context providers_202201](https://github.com/clauderic/dnd-kit/pull/569)
- Having two distinct context providers will allow to keep certain internals such as dispatch hidden from consumers. 
- It also serves as an optimization until context selectors are implemented in React, properties that will change often, such as the droppable containers and droppable rects, the transform value and array of collisions should be stored on a different context provider to limit un-necessary re-renders in useDraggable, useDroppable and useSortable.

- ## [Unnecessary rerenders cause poor performance](https://github.com/clauderic/dnd-kit/issues/389)
- We use @dnd-kit on some fairly large and complex applications at Shopify and have not run into any significant performance issues when the components that use useDraggable, useDroppable or useSortable and their child components are properly memoized.

- Sounds good. I am pretty sure our issue can be addressed with proper memoization.
  - Up to you if you want to keep this issue open for when React officially supports useContextSelector or if you want to close it.

- ## [Possible to combine sortables?](https://github.com/clauderic/dnd-kit/issues/114)
  - I'm trying to use dnd-kit on a board where cards can be reordered and combined, similar to this example from react-beautiful-dnd.
  - Is this possible to do using the current @dnd-kit/sortable package? I can probably do it with @dnd-kit/core but I assume I'd miss out on things like keyboard sorting and sorting strategies.

- Say you were building a vertical list, I'd start by forking the verticalListSortingStrategy and updating the threshold after which a node should shift positions.

- ## [Provide mouse position to collision detection algorithm](https://github.com/clauderic/dnd-kit/issues/127)
  - I need to use a collision detection algorithm that takes into account the position of the cursor inside the dragging item since it's frequently the case that the draggable is over a droppable, but the cursor is not.
- I realized this is as simple as keeping track of mousemove and using that to determine if the current mouse position is over a given rect.
- This feature just landed thanks to #556, you can now access `pointerCoordinates` in collision detection algorithms.

- ## [Is there a built-in sorting strategy for virtualized grids in `@dnd-kit/sortable` ?](https://github.com/clauderic/dnd-kit/discussions/411)
- virtualized grids aren't currently supported by any of the sorting strategies. 
  - It's been a while since I looked at this, but I believe the `rectSortingStrategy` strategy needs all elements to be mounted to work properly.
  - Having said that, you could fairly easily look at the source code of react-sortable-hoc's grid sorting logic and port it over as a custom sorting strategy for @dnd-kit
  - This isn't a feature I need so I won't be prioritizing it myself for the time being.

- Actually, I have a virtualized grid implementation which works pretty well with @dnd-kit/sortable
  - I'm using `rectSortingStrategy`, and there doesn't seem to be any issues even without all the items being rendered. 
  - The only thing I had to do was to ensure that the item currently being dragged was rendered even when it's outside of the visible range. 
