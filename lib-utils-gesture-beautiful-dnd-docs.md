---
title: lib-utils-gesture-beautiful-dnd-docs
tags: [docs, react-beautiful-dnd]
created: 2023-09-03T15:30:55.367Z
modified: 2023-09-03T15:31:12.260Z
---

# lib-utils-gesture-beautiful-dnd-docs

# guide

# api

- 
- 
- 
- 
- 

# docs

## Overview

- Patterns
  - Virtual lists
  - Multi drag
  - Tables
  - Reparenting a `<Draggable />` - Using our cloning API or your own portal

- There are a lot of libraries out there that allow for drag and drop interactions within React. 
- Most notable of these is the amazing `react-dnd`. 
  - It does an incredible job at providing a great set of drag and drop primitives which work especially well with the wildly inconsistent html5 drag and drop feature. 
- `@hello-pangea/dnd` is a higher level abstraction specifically built for lists (vertical, horizontal, movement between lists, nested lists and so on). 
  - Within that subset of functionality @hello-pangea/dnd offers a powerful, natural and beautiful drag and drop experience. 
  - However, it does not provide the breadth of functionality offered by react-dnd. 
  - 🚨 **One shortcoming is that grid layouts are not supported** (yet). 

## [Design principles](https://github.com/hello-pangea/dnd/blob/main/docs/about/design-principles.md)

- Foundational idea: physicality
  - we want users to feel like they are moving physical objects around
- Application 1: no instant movement (no snapping)
  - For a more natural drag we animate the movement of items as they need to move out of the way while dragging to more clearly show a drags effect. 
  - We also animate the drop of an item so that it animates into its new home position.
- Application 2: knowing when to move
  - a dragging items impact is based on its centre of gravity — regardless of where a user grabs an item from
  - A list is dragged over when the centre position of a dragging item goes over one of the boundaries of the list
  - Once the centre position of an item (A) goes over the edge of another item (B), B moves out of the way.
- Application 3: movement to communicate positioning
  - @hello-pangea/dnd relies on movement to communicate positioning. I
  - Drop shadows, lines and other affordances are useful in drag and drop contexts where natural movement is not possible.
  - The answer to these is often: snapping (where something just appears in the right spot). We are trying hard to avoid any snapping as it breaks the physicality we are trying to model.
- Application 4: maximise interactivity
  - avoid as many periods of non-interactivity as possible
  - The user should feel like they are in control of the interface and not waiting for an animation to finish before they can continue to interact with the interface. 
- Application 5: no drag axis locking
  - For now, the library does not support drag axis locking
  - The current thinking is this breaks the physical metaphor we are going for and sends a message to the user that they are interacting with a piece of software rather than moving physical objects around. 
- Application 6: natural cross list movement
  - Rather than using an index based approach for keyboard movement between lists, @hello-pangea/dnd performs cross list movement based on inertia, gravity and collisions. 

## [pattern: Reparenting a `<Draggable />` ](https://github.com/hello-pangea/dnd/blob/main/docs/guides/reparenting.md)

- There are situations were you want to change the parent element of the dragging item while a drag is occurring. 
- There are two approaches you can use to do this:
  - Using our 1st class cloning API (required for virtual lists)
  - Using your own portal with ReactDOM.createPortal

- We leave elements in place when dragging. We apply `position: fixed` on elements when we are moving them around. 
  - This is quite robust and allows for you to have `position: relative | absolute | fixed` parents. 
  - However, unfortunately `position:fixed` is impacted by `transform`.
  - This means that if you have a `transform: *` on one of the parents of a `<Draggable />` then the positioning logic will be incorrect while dragging. Lame(跛的；瘸的; 无说服力的；蹩脚的)! For most consumers this will not be an issue.
- To get around this issue, you need to move the dragging item to another location in the DOM - usually `document.body` or a direct descendent of it. 
  - This removes the impact of any parent styles on the `position:fixed`. 
  - The new parent is often referred to as a portal.

- cloning API is a first class way of reparenting a `<Draggable />`s into another DOM location while a drag is occurring. 
  - When using our cloning API, the original `<Draggable />` is removed while the drag is being performed; 
  - a new clone is rendered (using renderClone) into the container element (controllable using getContainerForClone)
  - Using our cloning API is required for compatibility with virtual lists.

- Generally you will want to render the same visual item as the one that is dragging, but you can render anything you want. 
  - The displacement(移位; 转移) will be based on the dimensions of the original item, so we strongly recommend using an element that is exactly the same size.

- You are welcome to use your own portal solution if you want to from within your `<Draggable />`. 
  - Before we had a cloning API, reparenting needed to be done by using your own portal. 
  - It is now recommended that you use the cloning API.

- Keep in mind that anything that is reparented will be rendered from scratch. 
  - So you do not want to be moving large component trees into a portal
  - otherwise you will experience large UI jank. 
- We do not recommend using reparenting out of the box because of this performance drawback.

## [pattern: Tables](https://github.com/hello-pangea/dnd/blob/main/docs/patterns/tables.md)

- why use table
  - Clean way of displaying tabular data
  - Can copy paste the table into other applications
  - Great browser support
  - Can reorder items in the table by rbd

- We have not found a way to achieve semantic reordering of table columns at this stage. 
  - This is because there is no one element that represents a table column - rather, a column is a result of cell placements within repeating rows.

- There are two strategies you can use when reordering tables.

- 👉🏻 Fixed layouts (faster and simpler)
  - In order to use this strategy the widths of your columns need to be fixed - that is, they will not change
  - This can be achieved with either a `table-layout: fixed` or `table-layout: auto` as long as you manually set the width of the cells (eg 50%).
  - The only thing you need to do is **set `display: table` on a `<Draggable />` row** while it is dragging.
  - approach of fixed layouts doesn't keep the styling once an element is being dragged. 
    - An alternative is to not set `table-layout` or `display: table` when `<Draggable />` is dragging, but rather just set the `width` of each `<td>` permanently. 
    - This avoids the need to use any event responders. E.g. in the `<Draggable />`, set each `<td>` to `width: 100px` with inline styling or css. 

- 👉🏻 Dimension locking (slower but more robust)
  - This strategy will work with columns that have automatic column widths based on content. It will also work with fixed layouts. 
  - It is **a more robust strategy than the first, but it is also less performant**.
  - When we apply `position: fixed` to the dragging item, it removes it from the automatic column width calculations that a table uses. 
  - So before a drag starts, we **lock all of the cell widths using inline styles to prevent the column dimensions from changing when a drag starts**. 
  - You can achieve this with the `onBeforeDragStart` responder.
- This has poor performance characteristics at scale as it requires: 
  - Calling render() on every row 
  - Reading the DOM (`window.getComputedStyles`) on every row
  - For tables with **less than 50 rows** this should approach be fine!

- If you want to use reparenting (cloning or your own portal) in combination with table row reordering, then there are few extra steps you need to go through.
  - First up, have a read of our reparenting pattern to get familiar with the approach.
  - When moving an existing `<tr>` into a `ReactDOM.createPortal`, it is important to know that the existing `<tr>` is unmounted and a new `<tr>` is mounted into the portal. 
  - In order to preserve the cell dimensions of the cells in the row that we are moving into a ReactDOM.createPortal we need to lock its dimensions using inline styles 
  - Sadly though, the new component does not directly have access to the information about the component that was in the tree before it moved to the portal. 
  - So in order to do this we need to obtain the cell dimensions of the `<tr>` when it is unmounting and re-apply it to the new `<tr>` when it mounted in `componentDidMount`.
  - There is no great way to do this as when `componentDidMount` is called we are not sure if the component is unmounting as the `<tr>` is no longer needed, or if it is unmounting because it is about to move into a portal.
- It seems like the only way to get things working is to:
  - In `componentWillUnmount` of the `<tr>` read the current widths of the cells from the DOM. You then store this value outside of the component so that it can be read by new components that are mounting.
  - If a component is mounting and `isDragging` is `true`, then you can see if there is a previously recorded width. If there is then you can apply that width.

## [pattern: Virtual lists](https://github.com/hello-pangea/dnd/blob/main/docs/patterns/virtual-lists.md)

- As a general rule, you will want to start using a virtual list when your list size is more than 500 items.
- @hello-pangea/dnd is designed to work with existing virtual list solutions and does not have it's own virtual list abstraction
  - We have created examples for react-window, react-virtualized, react-virtuoso
- Virtualisation libraries often have overscanning enabled by default
  - Overscanning is where a small about of non-visible items are rendered near the boundary of the window. 
  - When a scroll occurs the overscanned item can be immediately moved into view and does not need to be created. 
  - It is required that overscanning be enabled for @hello-pangea/dnd to work correctly. 
  - We require an overscanning value of one or more.
- When using a virtual list the original dragging item can be unmounted during a drag if it becomes invisible. 
  - To get around this we require that you drag a clone of the dragging item.
- A simple way to add extra space to a virtual list is to add a non-visible item to your list.

## [pattern: Multi drag](https://github.com/hello-pangea/dnd/blob/main/docs/patterns/multi-drag.md)

- Dragging multiple `<Draggable />`s at once (multi drag) is currently a pattern not out of the box
  - We have not included the interaction into the library itself. 
  - This is done because a multi drag experience introduces a lot of concepts, decisions and opinions
- We have decided on a simple, but very flexible and scalable multi drag pattern to start with.
- 👉🏻 We can break the user experience down in three phases.
  - Selection: The user selects one or more items.
  - Dragging: The user drags one item as a representation of the whole group.
  - Dropping: The user drops an item into a new location. We move all of the selected items into the new location
- Before a drag starts we need to allow the user to optionally select a number of `<Draggable />`s to drag. 
  - If a user clicks on an item the selected state of the item should be toggled
- We need to do one check in `onDragStart`. 
  - If the user is starting to drag something that is not selected then we need to clear the selection.
- When moving the items to the new list they should be inserted into the new list at the index in which the dragging item was dropped. 

- Doing a multi drag interaction in a performant way can be challenging. 
  - The core thing you want to do is to avoid calling render() on components that do not need to update. 
  - The **current best practice** for this is to use `redux` in combination with `react-redux`,  `reselect` and `memoize-one`.
- avoid calling render for selection style changes.
  - You could apply a unique data attribute to each item and then apply the selected style to it using selectors dynamically in a parent component.
  - You could look into using the dynamic shared styles pattern.

## [Combining](https://github.com/hello-pangea/dnd/blob/main/docs/guides/combining.md)

- supports the combining of `<Draggable />`s
  - In order to enable combining you need to set `isCombineEnabled` to true on a `<Droppable />` and you are good to go!

- When `isCombineEnabled` is set on a list, any item in the list can be combine with.
  - You can toggle `isCombineEnabled` during a drag
  - users are able to combine and reorder within the same list in a way that feels intuitive and natural.

- limitations
  - No granular control over which items can be combined with within the list. 
    - We could move to the `isCombineEnabled` prop from a `<Droppable />` to a `<Draggable />` to allow this sort of customisation. 
    - However, in order to ship this huge feature we went a bit simplier to start with
  - A list must be reorderable to also have items that can be combined with. 
    - It is not possible for a list to be 'combine only' at this stage

- A combine result might signify different operations depending on your problem domain.
  - When combining, a simple operation is to just remove the item that was dragging

- Drop animation
  - One of the goals of @hello-pangea/dnd is to create a drag and drop experience that feels physical. 
  - This is a bit tricky to achieve in a generic way when it comes to combining two things.
- What we have gone for out of the box in the following animation:
  - scale the dragging item down
  - move the dragging item onto the center of the item being grouped with
  - fade the opacity of the dragging item down to 0
  - This animation attempts to communicate one item moving into another item in a fairly generic way.

## [Responders](https://github.com/hello-pangea/dnd/blob/main/docs/guides/responders.md)

- Responders are top level application events that you can use to perform your own state updates, style updates, as well as to make screen reader announcements.

- Lifecycle
  - onBeforeCapture: a drag is about to start and dimensions have not been collected from the DOM
  - onBeforeDragStart: a drag is about to start and dimensions have been captured from the DOM
  - onDragStart: A drag has started
  - onDragUpdate: Something has changed during a drag
  - onDragEnd (required): A drag has ended. It is the responsibility of this responder to **synchronously** apply changes that has resulted from the drag
  - We try hard to ensure that an entire lifecycle is completed before a new one starts.

- If you need to persist a reorder to a remote data store - update the list synchronously (optimistically) on the client (such as through setState()) and fire off a request in the background to persist the change. 
  - If the remote save fails, it is up to you how to communicate that to the user and update, or not update, the list.

- `@hello-pangea/dnd` does not support the changing of the size of any `<Draggable />` or `<Droppable />` after a drag has started. 
  - We build a virtual model of every `<Draggable /> and <Droppable />` when a drag starts. We do not recollect these during a drag. 
  -  If you want to modify dimensions before a drag starts you can use `onBeforeCapture`

- It is **highly recommended** that while a user is dragging that you block any state updates that might impact the amount of `<Draggable />`s and `<Droppable />`s, or their dimensions. 
  - Please listen to `onDragStart` and block updates to the `<Draggable />`s and `<Droppable />`s until you receive at `onDragEnd`.
  - During a drag you should not apply any server updates that could effect what is visible. 
  - ignore any results from server calls during a drag (do not call setState in your component with the new data)

## [How we use DOM events](https://github.com/hello-pangea/dnd/blob/main/docs/guides/how-we-use-dom-events.md)

> Note: due to a bug in webkit, particular events such as `mousemove` will not correctly set `event.defaultPrevented` to true when `event.preventDefault()` is called.

- here are the safest event handlers that can be added on the drag handle, anywhere else higher on the tree or to the window directly.
  - `onClick`: the `event.defaultPrevented` property will be set to `true` if occurred as a part of the drag interaction. This is true even if the drag was not finished with a pre-click action such as `mouseup` or `touchend`.
  - `onKeyDown`: the `event.defaultPrevented` property will be set to `true` if it was used as a part of a drag.

- we use: event.preventDefault()
- we do not use: event.stopPropagation()
  - We do not stop the propagation of events that we call event.preventDefault() on so even though we may use a `mousemove` event for dragging we will not block that event from being published (propagating) and received by your event handlers.

- **We add all event handlers to the `window` in the capture phase**. 
  - What this means is as long as you are applying your events handlers in the bubbling phase (which is the default for event handlers), then behaviour of events will be as described on this page.

- In order to know if we have already used the event for the purpose of drag and drop you need to check the `event.defaultPrevented` property.

- Some user events have a direct impact on a drag: such as a `mousemove` when dragging with a mouse or the up arrow `keydown` event while dragging with a keyboard. 
  - These direct events will have `event.preventDefault()` called on them to prevent their default browser behaviours. 
  - Some events indirectly impact a drag such as a resize event which cancels a drag. 
  - For events that indirectly impact a drag we do not call `event.preventDefault()` on them. 
  - Generally indirect events that impact drag are events that cancel a drag such as `resize` and `orientationchange` events.

- 👉🏻 Mouse dragging
- preventDefault() is called on mousedown
  - When the user first performs a `mousedown` on a drag handle, we are not sure if they are intending to click or drag. 
  - Ideally we would not call preventDefault() on this event as we are not sure if it is a part of a drag. 
  - However, we need to call `preventDefault()` in order to avoid the item obtaining focus as it has a `tabIndex`.

- preventDefault() not called on mousemove
  - We are not sure yet if a drag will start
  - The user needs to move a small threshold before we consider the movement to be a drag. 
  - In this period of time we do not call preventDefault() on any mousemove events as we are not sure if they are dragging or just performing a sloppy click

- The user has indicated that they are not mouse dragging
  - preventDefault() not called on the event that caused the pending drag to end (such as mouseup and keydown). 
  - Any keydown event that is firered while there is a pending drag will be considered an indirect cancel
  - preventDefault() is not called on the subsequent click event if there is one

- A mouse drag has started and the user is now dragging
  - preventDefault() is called on `mousemove` events
  - preventDefault() is called on a few `keydown` events to prevent their standard browser behaviour
  - preventDefault() is not called on keyup events even if the keydown was prevented

- A drag is ending
  - preventDefault() is called on a mouseup if it ended the drag
  - preventDefault() is called on the next click event regardless of how the drag ended.

- 👉🏻 Touch dragging
- The logic for touch dragging works in a similar way to mouse dragging
  - preventDefault() is not called on touchstart.
  - It is possible to cancel a touch drag with over events such as an orientationchange or a touchcancel. We do not call preventDefault on these events.

- 👉🏻 Keyboard dragging
- We only use `keydown` events for keyboard dragging so `keyup` events never have preventDefault() called on them
- Unlike mouse dragging a keyboard drag starts as soon as the user presses the spacebar `space` key. 
  - This initial keyboard interaction has event.preventDefault() called on it.

## [How we detect scroll containers](https://github.com/hello-pangea/dnd/blob/main/docs/guides/how-we-detect-scroll-containers.md)

- @hello-pangea/dnd will automatically detect the scroll containers for your application when a drag is starting. 
  - It does this by looking at the computed `overflowX` and `overflowY` values of an element.
  - If @hello-pangea/dnd finds an element that has a computed `overflowX` or `overflowY` set to `scroll` or `auto`, then that element is marked as a scroll container.

- If only one axis has `overflow-[x|y]: hidden` and the other is `visible` (the default value), then it will be computed as `auto`.
  - visible/clip computing to auto/hidden (respectively) if one of overflow-x or overflow-y is neither visible nor clip

- `document.body` (`<body>`) is different from `document.documentElement` (the `<html>` element). 
  - Any scroll on the `html` element is considered a `window` scroll. 
  - Most of the time any scroll bar that would have appeared on the `body` will be merged with the `html` scroll bar. 
  - However, there are situations where they can have different scrollable areas.

> We have not been able to find a reliable cross browser mechanism for detecting if a `body` has an independent scroll bar to the `html` element.

- There seems to also be an additional requirement that we have not been able to accurately quantify(量化) regarding the relationship of the sizes of the `html` and `body` elements.

- It looks like when the `html` element has some `width` and `height` related properties set then this can impact things. 
- However, finding a purely javascript solution for detecting this has alluded us so far

## [sensors](https://github.com/hello-pangea/dnd/blob/main/docs/sensors/sensor-api.md)

- With our Sensor API it is possible to: Create drag and drop interactions from any input type you can think of
  - The public Sensor API is the same API that our mouse, keyboard, and touch sensors use
- You create a sensor that has the ability to attempt to claim a lock. 
  - A lock allows exclusive control of dragging within a `<DragDropContext />`. 
  - When you are finished with your interaction, you can then release the lock.
- Lifecycle
  - Try to get a lock when a sensor wants to drag an item. 
  - If a lock is obtained then there are a number of pre drag actions available to you (PreDragActions).
  - A pre drag lock can be upgraded to a drag lock, which contains a different set of APIs (FluidDragActions or SnapDragActions). Once a `<Draggable />` has been lifted, it can be moved around.
- Rules
  - Only one `<Draggable />` can be dragging at a time for a `<DragDropContext />`.
  - You cannot use outdated or aborted locks
- A sensor is a React hook.you can treat the sensor just as a function.
- Fluid dragging
  - `<Draggable />`s move around naturally in response a moving point.
  - The impact of the drag is controlled by a collision engine. (This is what our mouse sensor and touch sensor use)
- Snap dragging
  - `<Draggable />`s are forced to move to a new position using a single command. 
  - This is what our keyboard sensor uses

- A lock can be aborted at any time by the application, such as when an error occurs. 
  - If you try to perform actions on an aborted lock then it will not do anything.

- When a user presses the mouse down on an element, we cannot determine if the user was **clicking or dragging**
  - we only start a drag once the user has moved beyond a certain distance with the mouse down (the drag threshold) — more than they would if they were just making a sloppy click
  - If the drag threshold is not exceeded, then the user interaction behaves just like a regular click. 
  - If the drag threshold is exceeded, then the interaction will be classified as a drag and the standard click behaviour will not occur.
- When a drag is occurring with a mouse, the user is able to execute the following keyboard shortcuts:
  - esc - cancel the drag
- During a mouse drag the following standard keyboard events are prevented to prevent a bad experience:
  - tab - preventing tabbing
  - enter - preventing submission
  - Other than these explicitly prevented keyboard events all standard keyboard events should work as expected.

- @hello-pangea/dnd supports dragging on touch devices such as mobiles and tablets.
- When a user presses their finger (or other input) on a `<Draggable />`, we are not sure if they where intending to **tap, force press, scroll the container or drag**. 
- A user can start a drag by holding their finger on an element for a small period of time 🕑 (long press)
- If the user lifts their finger before the timer is finished, then we release the event to the browser for it to determine whether to perform the standard tap/click action. 
  - This allows you to have a `<Draggable />` that is both clickable such as a anchor as well as draggable. 
  - If the item was dragged then we block the tap action from occurring.

- If we detect a `touchmove` before the long press timer expires, we cancel the pending drag and allow the user to scroll normally. 
  - This means that the user needs to be fairly intentional and precise with their grabbing. 
  - Once the first touchmove occurs, we have to either opt in or out of native scrolling.
  - If the long press timer has not expired: allow native scrolling and prevent dragging
  - If the long press timer has expired: a drag has started and we prevent native scrolling

- Vibration API currently is only supported in Chrome on Android.

- Force press
  - Safari only

- @hello-pangea/dnd supports dragging with only a keyboard. 
  - When the user is not dragging they can use their keyboard as they normally would. 
  - While dragging we override and disable certain browser shortcuts (such as tab) to ensure a fluid experience for the user.
- When a `<Draggable />` has focus, the spacebar `space` will lift a `<Draggable />`. This will start the drag.
- Once a drag is started, the following keyboard shortcuts can be used:
  - spacebar space - drop the `<Draggable />` element
  - esc - cancel the drag
- During a drag the following standard keyboard events have their default behaviour prevented (through event.preventDefault()) to avoid a bad experience:
  - tab - preventing tabbing
  - enter - preventing submission
- When dragging with a keyboard, @hello-pangea/dnd will also perform auto scrolling operations to ensure the item can be moved around

## [Auto scrolling](https://github.com/hello-pangea/dnd/blob/main/docs/guides/auto-scrolling.md)

- When a user drags a `<Draggable />` near the edge of a container, we automatically scroll the container as we are able to in order make room for the `<Draggable />`.
  - When the center of a `<Draggable />` gets within a small distance from the edge of a container, we start auto scrolling.
- The distances required for auto scrolling are based on a percentage of the height or width of the container for vertical and horizontal scrolling respectively. 
  - By using percentages rather than raw pixel values we are able to have a great experience regardless of the size and shape of your containers.

> If the `<Draggable />` is bigger than a container on the axis you are trying to scroll - we will not permit scrolling on that axis. 

- In order to move a `<Draggable />` into the correct position, we can do a combination of a `<Droppable />` scroll, window scroll and manual movements to ensure the `<Draggable />` ends up in the correct position in response to user movement instructions. 
  - This is amazing for users with visual impairments as they can correctly move items around in big lists without needing to use mouse positioning.

## [Preset styles](https://github.com/hello-pangea/dnd/blob/main/docs/guides/preset-styles.md)

- It is a goal of the library to provide unopinioned styling. 
  - However, we do apply some reasonable `cursor` styling on drag handles by default. 
  - This is designed to make the library work as simply as possible out of the box.

- In every phase
- Phase: resting
- Phase: dragging
- Phase: dropping
- Phase: user cancel

- All styles applied are vendor prefixed correctly to meet the requirements of our supported browser matrix. This is done by hand to avoid adding to @hello-pangea/dnd's size by including a css-in-js library

## [Drop animation](https://github.com/hello-pangea/dnd/blob/main/docs/guides/drop-animation.md)

- A drop animation is an important affordance to communicate placement. 
  - Our drop animations do not prevent the user from dragging something else while the animation is running.
  - If you do have use case where it makes sense to remove the drop animation, you will need to add a `transition-duration` property of _almost_ `0s`. This will skip the drop animation.
  - Do not make the `transition-duration` actually `0s`. It should be set at a near 0s value such as `0.001s`. 
  - The reason for this is that if you set `transition-duration` to `0s` then a `onTransitionEnd` event will not fire - and **we use that to know when the drop animation is finished**.
