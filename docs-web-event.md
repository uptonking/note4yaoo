---
title: docs-web-event
tags: [event, web]
created: '2020-08-19T13:37:04.996Z'
modified: '2020-08-19T13:37:17.123Z'
---

# docs-web-event

## guide

- ref
  - [Event developer guide](https://developer.mozilla.org/en-US/docs/Web/Guide/Events)
  - [DOM onevent handlers](https://developer.mozilla.org/en-US/docs/Web/Guide/Events/Event_handlers)
  - [Creating and triggering events](https://developer.mozilla.org/en-US/docs/Web/Guide/Events/Creating_and_triggering_events)
  - [Comparison of Event Targets](https://developer.mozilla.org/en-US/docs/Web/API/Event/Comparison_of_Event_Targets)

## event overview

- `event.target` is a reference to the object that dispatched the event. 
  - It identifies the element on which the event occurred and which may be its direct descendent.
- `event.currentTarget` always refers to the element to which the event handler has been attached. 
  - It is the element you actually bound the event to. 
  - This will never change.

## MouseEvent

- `MouseEvent.offsetX`
  - The offsetX read-only property of the MouseEvent interface provides the offset in the X coordinate of the mouse pointer between that event and the padding edge of the target node. 

- `MouseEvent.clientX`
  - The `clientX` read-only property of the MouseEvent interface provides the horizontal coordinate within the application's client area at which the event occurred (as opposed to the coordinate within the page).
  - return a double floating point value, as redefined by the CSSOM View Module. Originally, this property was defined as a long integer.
  - For example, clicking on the left edge of the client area will always result in a mouse event with a clientX value of 0, regardless of whether the page is scrolled horizontally.

- `MouseEvent.pageX`
  - The pageX read-only property of the MouseEvent interface returns the X (horizontal) coordinate (in pixels) at which the mouse was clicked, relative to the left edge of the entire document. 
  - This includes any portion of the document not currently visible.
  - Being based on the edge of the document as it is, this property takes into account any horizontal scrolling of the page. 

- `MouseEvent.screenX`
  - The screenX read-only property of the MouseEvent interface provides the horizontal coordinate (offset) of the mouse pointer in global (screen) coordinates.

- `window.pageXOffset`
  - The `pageXOffset` is an alias for `scrollX` .
- `window.scrollX`
  - returns the number of pixels that the document is currently scrolled horizontally. 
  - In practice, the returned value is a double-precision floating-point value indicating the number of pixels the document is currently scrolled horizontally from the origin, where a positive value means the content is scrolled to the left.
  - If the document isn't scrolled at all left or right, then `scrollX` is `0` .
  - In more technical terms, `scrollX` returns the X coordinate of the left edge of the current viewport. If there is no viewport, the returned value is 0.

- `MouseEvent.button`
  - The `MouseEvent.button` read-only property indicates which button was pressed on the mouse to trigger the event.
  - return a number representing a given button:
    - 0: Main button pressed, usually the left button or the un-initialized state
    - 1: Auxiliary button pressed, usually the wheel button or the middle button (if present)
    - 2: Secondary button pressed, usually the right button
    - 3: Fourth button, typically the Browser Back button
    - 4: Fifth button, typically the Browser Forward button
  - This property only guarantees to indicate which buttons are pressed during events caused by pressing or releasing one or multiple buttons. 
  - As such, it is not reliable for events such as mouseenter, mouseleave, mouseover, mouseout or mousemove.
  - Users may change the configuration of buttons on their pointing device so that if an event's button property is zero, it may not have been caused by the button that is physically left–most on the pointing device; however, it should behave as if the left button was clicked in the standard button layout.

  - 
