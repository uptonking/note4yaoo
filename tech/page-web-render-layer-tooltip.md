---
title: page-web-render-layer-tooltip
tags: [layer, render, tooltip, web]
created: 2021-08-24T05:24:01.348Z
modified: 2021-08-24T05:24:53.991Z
---

# page-web-render-layer-tooltip

# [Don’t attach tooltips to document.body](https://atfzl.com/don-t-attach-tooltips-to-document-body)

```html
<body>
  <!-- temporary div, vanishes when tooltips vanishes -->
  <div>my tooltip</div>

  <body>

    <body>
      <!-- this div stays forever, just for attaching tooltips -->
      <div id="tooltips-container">
        <!-- temporary div, vanishes when tooltips vanishes -->
        <div>my tooltip</div>
      </div>

      <body>
```

- Tooltips in our app were taking >80ms. And during this time, the main thread was blocked, you couldn’t interact with anything.
- The main reason for the slowness of Tooltip was **Recalculate Style** being called at the end of `mouseover` event call stack which takes a lot of time.
- I noticed the tooltip performance was inversely proportional to number of DOM nodes currently in document.
- This investigation started off with trying to use the css property `contain` to signal the browser about the containment of a particular DOM Node so that the Recalculate Style will not affect all the nodes. 
  - But applying the property on the element where we hover didn’t help as the tooltips were being rendered outside of the element, directly as a child of the body of the page.
- Next step was to try rendering the tooltip into a separate container and not directly in the body. 
  - Then we’ll set the `contain` css property to signal the browser to not do the expensive Recalculate Style.
- To my amazement, just having a separate container without even adding the css `contain` property fixed the performance. 
- The creation/modification of the render tree is called Recalculate Style in the performance timeline.
- Layout is calculating the size and positions of elements of the render tree, to know where we have to draw exactly. 
  - This is referred to as Layout in the performance timeline.
  - Layout may need to be done again whenever there is a change in size/position of an element which affects the position of all the elements in the page. 
  - Layout is also known as Reflow.
- To render a frame in a browser, we go in this order: JavaScript runs, then there are style calculation, then layout. Ignore Paint and Composite for now.
- When we access any layout property like `offsetWidth, offsetParent, width` etc, the browser returns the value from previously calculated layout calculations, which is not expensive as the calculation was done earlier in the previous frame and now we are just reading it.
- But what happens when we change a style on an element or modify the DOM? 
  - Then the browser has its own heuristics and is smart enough to know if the browser needs to Recalculate Style/Layout in the current frame or defer it for later.
  - You can see it as `Schedule Style Recalculation` in timeline.
- The problem happens when we try to access a layout property just after we change style/modify DOM. 
  - Then the browser has to force Recalculate Style/Layout because browser has to return the current value, it cannot give you a stale value from the previous frame. 
  - This causes the problem known as Layout Thrashing.

- The First Invalidation shows where in code, the render tree was first invalidated which later caused Forced Reflow because of Recalculation Forced code.
  - Doing `setAttribute` on an element in DOM is invalidating the render tree, and then accessing the `offsetParent` causes a Forced Synchronous Layout.
  - Had this been done in the opposite direction it wouldn’t be a problem.
- Popper accessing the `offsetParent` property after attaching the tooltip to the body is causing Forced Reflow. 
  - If this property access was done before attaching the tooltip to body, the reflow would not have happened.
- But all this is not in our control as the code is in the third party library popper.js.
  - I created a separate container in the body where the tooltip would always be attached.
  - And instructed the popper to be rendered in this container.
  - Now, the performance was greatly improved, the Recalculate Style still happened but its cost was less than before. 0.79ms down from 66.57ms:
- What happened here? 
  - The tooltip was attached to the tooltip container and not to the body. 
  - This invalidated a much smaller subtree, which was the tooltip container. 
  - The tooltip container is not visible in the page, so modifying it doesn’t invalidate the complete page render tree. 
  - If the tooltip container would have been visible in the page, then the complete render tree would be invalidated but in this case only an independent subtree was invalidated.
