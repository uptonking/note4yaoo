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

- ## [Asynchronous reordering and drop animation](https://github.com/clauderic/dnd-kit/issues/833)
- It seems to act better if I use `onDragOver` to pre-emptively move items around as you drag them. 
  - But overall I'd say try to use `onDragOver` to resort the item before the gesture even ends - then it's ready for the drop animation by the time it fires.

- ## [Sort by date](https://github.com/clauderic/dnd-kit/discussions/560)
- dnd-kit is un-opinionated as to what should happen when you drop a draggable item on a droppable container.
  - It's entirely up to the consumer to decide what should happen in that scenario.
  - For example, you could decide to always insert items at the top of a column when you move a ticket from one column to another (either in `onDragOver` or `onDragEnd` )

- ## [How to prevent draggable from returning to its position when overlay leaves sortable items area.](https://github.com/clauderic/dnd-kit/issues/829)
- As for now I found a solution to disable sortable strategy at all, and use `onDragOver` for changing position.

- ## [onDragOver gets triggered with onDragStart](https://github.com/clauderic/dnd-kit/issues/958)
- This is most likely correct, because you are over your active item. If you check the `over.id` you should see that its equal to the `active.id` .

- [onDragOver is called right after onDragStart so user will never hear onDragStart announcements](https://github.com/clauderic/dnd-kit/issues/424)
- In the sortable examples, the onDragOver event happens immediately after the onDragStart event, because the picked up item is directly over its original position when lifted, so the first onDragOver event happens without user input and is redundant.

- ## [How to access OnDrag events inside of draggable](https://github.com/clauderic/dnd-kit/discussions/268)
- `useDndMonitor` hook can be used within components wrapped in a DndContext provider to monitor the different drag and drop events that happen for that DndContext.

- ## [Animating add/delete items](https://github.com/clauderic/dnd-kit/discussions/108)
- Layout animations in useSortable have a requirement that the component be mounted while its index changes. Virtualization breaks this assumption for the newly mounted elements.
  - I honestly don't think there's an elegant solution to orchestrate this from @dnd-kit alone. As you mentioned, the workaround would be to make sure there are enough overscan items to allow for the items to be mounted before their indices change.
  - For anyone stumbling on this discussion, animating insertion/deletion of items is now possible by combining the `layoutMeasuring` prop of `<DndContext>` and the `animateLayoutChanges` argument of useSortable

- ## ['Maximum update depth exceeded' error with Sortable](https://github.com/clauderic/dnd-kit/issues/496)
- Memoize your objects, so you don't pass a new ref every time, which causes the DOM tree to refresh.

- ## [Nested Multiple Containers](https://github.com/clauderic/dnd-kit/issues/735)
- there are currently two ways to approach the problem:
  - A. (Simplest solution) Don't render the dragging element, use a placeholder as the dragoverlay element.
  - B. In the custom collision strategy filter the droppable containers that are inside the element you are currently dragging. Let's say you are using closestCorners

- ## [Separate context into Public and Internal context providers_202201](https://github.com/clauderic/dnd-kit/pull/569)
- Having two distinct context providers will allow to keep certain internals such as dispatch hidden from consumers. 
- It also serves as an optimization until context selectors are implemented in React, properties that will change often, such as the droppable containers and droppable rects, the transform value and array of collisions should be stored on a different context provider to limit un-necessary re-renders in useDraggable, useDroppable and useSortable.

- ## [Possible to combine sortables?](https://github.com/clauderic/dnd-kit/issues/114)
  - I'm trying to use dnd-kit on a board where cards can be reordered and combined, similar to this example from react-beautiful-dnd.
  - Is this possible to do using the current @dnd-kit/sortable package? I can probably do it with @dnd-kit/core but I assume I'd miss out on things like keyboard sorting and sorting strategies.

- Say you were building a vertical list, I'd start by forking the verticalListSortingStrategy and updating the threshold after which a node should shift positions.

- ## [Is there a built-in sorting strategy for virtualized grids in `@dnd-kit/sortable` ?](https://github.com/clauderic/dnd-kit/discussions/411)
- virtualized grids aren't currently supported by any of the sorting strategies. 
  - It's been a while since I looked at this, but I believe the `rectSortingStrategy` strategy needs all elements to be mounted to work properly.
  - Having said that, you could fairly easily look at the source code of react-sortable-hoc's grid sorting logic and port it over as a custom sorting strategy for @dnd-kit
  - This isn't a feature I need so I won't be prioritizing it myself for the time being.

- Actually, I have a virtualized grid implementation which works pretty well with @dnd-kit/sortable
  - I'm using `rectSortingStrategy`, and there doesn't seem to be any issues even without all the items being rendered. 
  - The only thing I had to do was to ensure that the item currently being dragged was rendered even when it's outside of the visible range. 

- ## [Race condition with `useDraggable` and `useDroppable` register / un-register effects](https://github.com/clauderic/dnd-kit/issues/125)
- [Refactor DroppableContainers object into a custom Map instance](https://github.com/clauderic/dnd-kit/pull/372)

- ## [Comparison with react-beautiful-dnd · clauderic/dnd-kit](https://github.com/clauderic/dnd-kit/discussions/481)
- react-beautiful-dnd依赖redux，使用js而不是ts实现
  - 示例丰富
- react-beautiful-dnd does not seems to support grid sorting
- the main difference would be that react-beautiful-dnd is specifically built for lists, while @dndkit supports a much wider range of use cases, such as grids, trees, 2D games, and much more.

# discuss-performance
- ## [Unnecessary rerenders cause poor performance](https://github.com/clauderic/dnd-kit/issues/389)
- We use @dnd-kit on some fairly large and complex applications at Shopify and have not run into any significant performance issues when the components that use useDraggable, useDroppable or useSortable and their child components are properly memoized.

- Sounds good. I am pretty sure our issue can be addressed with proper memoization.
  - Up to you if you want to keep this issue open for when React officially supports useContextSelector or if you want to close it.

- ## [re-rendering ALL draggable items on drag start and such](https://github.com/clauderic/dnd-kit/issues/1071)
  - [React Context Performance Pitfalls](https://blog.devgenius.io/react-context-pitfalls-9fb67723183b)
  - https://codesandbox.io/p/sandbox/throbbing-moon-uvbor3
  - it seems that all draggable components will re-render when one of them is dragged, it happens because of the use of context in useDraggable and the way that the context exposes the values, for example, active (which definitely changes when you start dragging).
  - there is a way around it. the idea is to expose functions instead of values on the context value so it won't re-render all components that use it when something that is irrelevant to them changes.
  - a workaround for this issue could be creating a Draggable component that will receive the content (the actual component) as children. but then you cannot pass isDraggable and such to it
  - Or you can separate the draggable item into 2 components: DraggableItem and Item + memo the Item.


- ## [Jank when dragging fast](https://github.com/clauderic/dnd-kit/issues/799)
- This is indeed a critical issue that may affect all the multi-container apps.
  - I've tested the multi-container scenario from the storybook related to the #788 and I can confirm that it fixes the issue which is great 

- ## [perf regression: all Sortables in 5.0 rerender constantly on even smallest mouse movement](https://github.com/clauderic/dnd-kit/issues/623)
- The same problem is happening to me, 'useSortable' is causing retenders due to 'useContext'. 
  - The easiest way to fix this is to use `useContextSelector` .

# discuss-collision
- ## [Provide mouse position to collision detection algorithm](https://github.com/clauderic/dnd-kit/issues/127)
  - I need to use a collision detection algorithm that takes into account the position of the cursor inside the dragging item since it's frequently the case that the draggable is over a droppable, but the cursor is not.
- I realized this is as simple as keeping track of mousemove and using that to determine if the current mouse position is over a given rect.
- This feature just landed thanks to #556, you can now access `pointerCoordinates` in collision detection algorithms.

- ## [Snapping to droppable](https://github.com/clauderic/dnd-kit/issues/849)
  - For example draggable is inside droppable A and may be freely moved inside, once cursor leaves droppable A draggable stays as if restrictToParentElement was used, but once cursor moves nearer to droppable B than to A, draggable 'jumps' into B.

- I have written custom modifier and custom collision detection (composed)

- 参考实现基于 `onDragMove`

- ## [Canceling drag operation when using the closest center/corners collision detection](https://github.com/clauderic/dnd-kit/discussions/210)
- You can always "cancel" drag operations by not handling the onDragEnd event for a given operation.
- As for collision detection, you can fork the `closestCenter` collision detection and create your own custom collision detection algorithm that does not match droppables if they are further than a certain distance
  - 给出了实现示例

- ## [feature request: collision detection for sibling `useDraggable` ](https://github.com/clauderic/dnd-kit/issues/810)
- You can detect collisions between sibling draggables by also connecting them to `useDroppable` , similar to how the `useSortable` hook works

- ## [Is it possible to fire onDragOver more than one time for the same droppable within its bounds?](https://github.com/clauderic/dnd-kit/issues/836)
- My idea is to have custom collision detection, that will replicate beautiful-dnd behaviour.
  - It has feature that detects the side (above middle or below middle) of droppable and move draggable above or below droppable. It is very logical behaviour, and works with different sizes of objects.
- I am able to replicate it but only at the `onDragMove` callback. Because I cannot fire `onDragOver` more than one time, being over the droppable.

- ## [RectOverlap Collision Detection Algorithm](https://github.com/clauderic/dnd-kit/issues/813)
- I was trying to create the multi-container free drag and drop using dnd-kit and feel the need for something which detects collision only when there is the full intersection of Draggable and Droppable. 
  - That is why I wrote the custom Algorithm for full intersection and name it rectOverlap.

- ## [RectIntersection is not working with draggable items inside a scrollable container](https://github.com/clauderic/dnd-kit/issues/43)
- https://codesandbox.io/s/drag-item-in-scroller-with-custom-collision-detection-jbr9h

- [Cannot be dragged into the DropArea when the DragItem is at the bottom of the scroll container](https://github.com/clauderic/dnd-kit/issues/483)
- I have a workaround with a different collision detector which uses the current active item rather than the collisionRect which seems to work for the meantime

- 💡 [Refactor measuring and collision detection](https://github.com/clauderic/dnd-kit/pull/518)
- This PR reduces the number of concepts related to measuring from ViewRect, LayoutRect to just a single concept of `ClientRect`.
- Previously, all collision detection algorithms were relative to the top and left points of the document. While this approach worked in most situations, it broke down in a number of different use-cases: #43, #73, #98, #263, #325, #483, etc.
- This new approach changes the frame of comparison to be relative to the viewport. 

- ## [useSortable with variable size items and without a drag overlay](https://github.com/clauderic/dnd-kit/issues/804)
- We created a vertical list recently, with useSortable, and couldn't get the dragging / collision detection to work with our variable height items, without also using an overlay. The overlay was difficult to achieve for us, for reasons I won't go in to.
  - Anyway, we created a new collision detection strategy that allows it to work as you would expect, so if you want this I can open up a pull request. 
  - [Add verticalSortableList collision detection strategy](https://github.com/clauderic/dnd-kit/pull/805)
  - One thing to note is that it doesn't work with autoscrolling (scrolling the container while dragging). We have been using this code with the autoscrolling option turned off for a while now, and it's been working fine, so I think it's solid.
