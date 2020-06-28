---
tags: [browser, optimization, web]
title: note-web-optimization-render-performance
created: '2020-06-28T06:46:35.619Z'
modified: '2020-06-28T13:54:40.509Z'
---

# note-web-optimization-render-performance

## guide
- https://developers.google.com/web/fundamentals/performance/rendering/
- https://developers.google.com/web/fundamentals/performance/get-started
- https://developers.google.com/web/fundamentals/performance/why-performance-matters

## Web Performance Overview
- Sites have more features than ever before. So much so, that many sites now struggle to achieve a high level of performance across a variety of network conditions and devices.
- Performance issues vary. 
  - At best, they create small delays that are only briefly annoying to your users. 
  - At worst, they make your site completely inaccessible, unresponsive to user input, or both.
- Performance is about retaining users
- Performance is about improving conversions
- Performance is about the user experience
- Performance is about saving money for users and the company
- where to optimize
  - Mind what resources you send
  - Mind how you send resources
  - Mind how much data you send

## Loading Performance Overview
- Regardless of the platform, network, or device, faster apps are better apps.
- https://web.dev/user-centric-performance-metrics/

## Measure performance with the RAIL model
- https://web.dev/rail/
- **RAIL** stands for four distinct aspects of web app life cycle: response, animation, idle, and load. 
- RAIL is a user-centric performance model that provides a structure for thinking about performance. 
- The model breaks down the user's experience into key actions (for example, tap, scroll, load) and helps you define performance goals for each of them.
- Tools for measuring RAIL 
  - Chrome DevTools
  - Lighthouse

## Rendering Performance Overview
- Performance is the art of avoiding work, and making any work you do as efficient as possible.
- 60fps and Device Refresh Rates
  - Most devices today **refresh their screens 60 times a second**. 
  - If there’s an animation or transition running, or the user is scrolling the pages, the browser needs to match the device’s refresh rate and put up 1 new picture, or frame, for each of those screen refreshes
  - Each of those frames has a budget of just over 16ms (1 second / 60 = 16.66ms). 
  - In reality, however, the browser has housekeeping work to do, so all of your work needs to be completed inside 10ms. 
  - When you fail to meet this budget the frame rate drops, and the content judders(抖动) on screen. 
  - This is often referred to as jank(卡顿)
- There are areas you have the most control over, and key points in the pixels-to-screen pipeline
  1. Trigger visual change by js or css.
    - Typically JavaScript is used to handle work that will result in visual changes, whether it’s jQuery’s animate function, sorting a data set, or adding DOM elements to the page. 
    - It doesn’t have to be JavaScript that **triggers a visual change**, though: CSS Animations, Transitions, and the Web Animations API are also commonly used.
  2. Style calculations 
    - It is the process of **figuring out which CSS rules apply to which elements based on matching selectors**, for example, `.headline or .nav > .nav__item`. 
    - From there, once rules are known, they are applied and the final styles for each element are calculated.
  3. Layout/Reflow
    - Once the browser knows which rules apply to an element, it can begin to calculate how much space it takes up and where it is on screen. 
    - The web’s **layout model** means that one element can affect others
    - for example the width of the `<body>` element typically affects its children’s widths and so on all the way up and down the tree, so the process can be quite involved for the browser.
  4. Paint
    - Painting is the process of filling in pixels. 
    - It involves **drawing** out text, colors, images, borders, and shadows, essentially every visual part of the elements. 
    - The drawing is typically done onto multiple surfaces, often called layers.
    - Sometimes you may hear the term "rasterize" used in conjunction with paint. 
    - This is because painting is actually two tasks: 
      - 1) creating a list of draw calls 
      - 2) filling in the pixels.
      - The latter is called "rasterization" and so whenever you see paint records in DevTools, you should think of it as including rasterization.
      - In some architectures creating the list of draw calls and rasterizing are done in different threads, but that isn't something under developer control.
  5. Compositing. 
    - Since the parts of the page were drawn into potentially multiple layers, they need to be drawn to the screen in the correct order so that the page renders correctly.
    - This is especially important for elements that overlap another, since a mistake could result in one element appearing over the top of another incorrectly.
- Each of these parts of the pipeline represents an opportunity to introduce jank, so it's important to understand exactly what parts of the pipeline your code triggers.
- You won’t always necessarily touch every part of the pipeline on every frame. 
- In fact, there are three ways the pipeline normally plays out for a given frame when you make a visual change, either with JavaScript, CSS, or Web Animations:
- `JS / CSS > Style > Layout > Paint > Composite` 
  - If you change a “layout” property, so that’s one that changes an element’s geometry, like its width, height, or its position with left or top, the browser will have to check all the other elements and “reflow” the page.
  - Any affected areas will need to be repainted, and the final painted elements will need to be composited back together.
- `JS / CSS > Style > Paint > Composite`
  - If you changed a “paint only” property, like a background image, text color, or shadows, in other words one that does not affect the layout of the page, then the browser skips layout
  - but it will still do paint.
- `JS / CSS > Style > Composite`
  - If you change a property that requires neither layout nor paint, and the browser jumps to just do compositing.
- If you want to know which of the three versions above changing any given CSS property will trigger, head to CSS Triggers.
  - https://csstriggers.com/
- If you want the fast track to high performance animations, read the section on changing compositor-only properties.

## Optimize JavaScript Execution
- Tips
  - Avoid `setTimeout` or `setInterval` for visual updates; always use `requestAnimationFrame` instead.
  - Move long-running JavaScript off the main thread to Web Workers.
  - Use micro-tasks to make DOM changes over several frames.
  - Use Chrome DevTools’ Timeline and JavaScript Profiler to assess the impact of JavaScript.
- JavaScript often triggers visual changes. 
  - Sometimes that's directly through style manipulations
  - and sometimes it's calculations that result in visual changes, like searching or sorting data. 
  - Badly-timed or long-running JavaScript is a common cause of performance issues. 
- The JavaScript you write is nothing like the code that is actually executed. 
  - Modern browsers use JIT compilers and all manner of optimizations and tricks to try and give you the fastest possible execution
- Use requestAnimationFrame for visual changes
- Reduce complexity or use Web Workers
- Know your JavaScript’s “frame tax”
- Avoid micro-optimizing your JavaScript
- ref
  - https://zhuanlan.zhihu.com/p/39878259

## Reduce the Scope and Complexity of Style Calculations
- Tips
  - Reduce the complexity of your selectors; use a class-centric methodology like BEM.
  - Reduce the number of elements on which style calculation must be calculated.
- Changing the DOM, through adding and removing elements, changing attributes, classes, or through animation, will all cause the browser to recalculate element styles and, in many cases, layout (or reflow) the page, or parts of it. 
  - This process is called **computed style calculation**.
- The first part of computing styles is to **create a set of matching selectors**, which is essentially the browser figuring out which classes, pseudo-selectors and IDs apply to any given element.
- The second part of the process involves taking all the style rules from the matching selectors and figuring out what final styles the element has. 
  - In Blink (Chrome and Opera's rendering engine) these processes are, today at least, roughly equivalent in cost
  - Roughly 50% of the time used to calculate the computed style for an element is used to **match selectors**
  - and the other half of the time is used for **constructing the RenderStyle** (computed style representation) from the matched rules.
- Reduce the complexity of your selectors
- Reduce the number of elements being styled
- Measure your Style Recalculation Cost
- Use Block, Element, Modifier


## Avoid Large, Complex Layouts and Layout Thrashing(Reflow)
- Tips
  - Layout is normally scoped to the whole document.
  - The number of DOM elements will affect performance; you should avoid triggering layout wherever possible.
  - Assess layout model performance; new Flexbox is typically faster than older Flexbox or float-based layout models.
  - Avoid forced synchronous layouts and layout thrashing; read style values then make style changes.
- Layout is where the browser figures out the geometric information for elements: their size and location in the page.
- Each element will have explicit or implicit sizing information based on the CSS that was used, the contents of the element, or a parent element. 
- The process is called *Layout* in Chrome, Opera, Safari, and Internet Explorer. In Firefox it’s called *Reflow*
- Similarly to style calculations, the immediate concerns for layout cost are:
  - The number of elements that require layout.
  - The complexity of those layouts.
- Avoid layout wherever possible
  - When you change styles, the browser checks to see if any of the changes require layout to be calculated, and for that render tree to be updated. 
  - Changes to “geometric properties”, such as widths, heights, left, or top all require layout.
  - Layout is almost always scoped to the entire document. 
  - If it’s not possible to avoid layout then the key is to once again use Chrome DevTools to see how long it’s taking, and determine if layout is the cause of a bottleneck
- Use flexbox over older layout models
  - The oldest CSS layout model allows us to position elements on screen relatively, absolutely, and by floating elements.
  - Whether you choose Flexbox or not, you should still try and avoid triggering layout altogether during high pressure points of your application
- Avoid forced synchronous layouts
  - First the JavaScript runs, then style calculations, then layout. 
    - It is, however, possible to force a browser to perform layout earlier with JavaScript. 
    - It is called a **forced synchronous layout**.
  - As the JavaScript runs, all the old layout values from the previous frame are known and available for you to query. 
  - Things get problematic if you’ve changed the styles of the box before you ask for its height
  ```
  // Schedule our function to run at the start of the frame.
  requestAnimationFrame(logBoxHeight);

  function logBoxHeight() {

  box.classList.add('super-big');

    // Gets the height of the box in pixels and logs it out.
    console.log(box.offsetHeight);
  }
  ```
  - Now, in order to answer the height question, the browser must first apply the style change (because of adding the super-big class), and then run layout. Only then will it be able to return the correct height. This is unnecessary and potentially expensive work.
  - Because of this, you **should always batch your style reads and do them first** (where the browser can use the previous frame’s layout values) and then do any writes
  - Done correctly the above function would be:
  ```
  function logBoxHeight() {
    // Gets the height of the box in pixels and logs it out.
    console.log(box.offsetHeight);

    box.classList.add('super-big');
  }
  ```
  - For the most part you shouldn’t need to apply styles and then query values; using the last frame’s values should be sufficient. 
  - Running the style calculations and layout synchronously and earlier than the browser would like are potential bottlenecks, and not something you will typically want to do.
- Avoid layout thrashing
  - There’s a way to make forced synchronous layouts even worse: do lots of them in quick succession.
  ```
  function resizeAllParagraphsToMatchBlockWidth() {
    // Puts the browser into a read-write-read-write cycle.
    for (var i = 0; i < paragraphs.length; i++) {
      paragraphs[i].style.width = box.offsetWidth + 'px';
    }
  }
  ```
  - The problem is that each iteration of the loop reads a style value (box.offsetWidth) and then immediately uses it to update the width of a paragraph
  - On the next iteration of the loop, the browser has to account for the fact that styles have changed since offsetWidth was last requested (in the previous iteration), and so it must apply the style changes, and run layout. This will happen on every single iteration
  - To fix
  ```
  // Read.
  var width = box.offsetWidth;

  function resizeAllParagraphsToMatchBlockWidth() {
    for (var i = 0; i < paragraphs.length; i++) {
      // Now write.
      paragraphs[i].style.width = width + 'px';
    }
  }
  ```
  - If you want to guarantee safety you should check out FastDOM, which automatically batches your reads and writes for you, and should prevent you from triggering forced synchronous layouts or layout thrashing accidentally.


## Simplify Paint Complexity and Reduce Paint Areas
- Tips
  - Changing any property apart from transforms or opacity always triggers paint.
  - Paint is often the most expensive part of the pixel pipeline; avoid it where you can.
  - Reduce paint areas through layer promotion and orchestration of animations.
  - Use the Chrome DevTools paint profiler to assess paint complexity and cost; reduce where you can.
- Paint is the process of filling in pixels that eventually get composited to the users' screens. 
- It is often the longest-running of all tasks in the pipeline, and one to avoid if at all possible.
- Triggering Layout And Paint
  - If you trigger layout, you will always trigger paint, since changing the geometry of any element means its pixels need fixing!
  - You can also trigger paint if you change non-geometric properties, like backgrounds, text color, or shadows. In those cases layout won’t be triggered
- Use Chrome DevTools to quickly identify paint bottlenecks
  -  Open the Rendering tab and then enable Paint Flashing
- Promote elements that move or fade
  - Painting is not always done into a single image in memory.
  - In fact, it’s possible for the browser to paint into multiple images, or compositor layers, if necessary.
  - Elements that are regularly repainted, or are moving on screen with transforms, can be handled without affecting other elements. 
    - like Sketch, GIMP, or Photoshop, where individual layers can be handled and composited on top of each other to create the final image.
  - The **best way to create a new layer is to use the `will-change` CSS property**. This will work in Chrome, Firefox and Opera, and, with a value of `transform`, will create a new compositor layer
  - For browsers that don’t support `will-change`, but benefit from layer creation, such as Safari and Mobile Safari, you need to (mis)use a 3D transform to force a new layer
  ```
  .moving-element {
    will-change: transform;
    或者
    transform: translateZ(0);
  }
  ```
  - Care must be taken not to create too many layers, as each layer requires both memory and management.
  - If you have promoted an element to a new layer, use DevTools to confirm that doing so has given you a performance benefit. 
  - **Don't promote elements without profiling**.
- Reduce paint areas
  - A large challenge of paint issues is that browsers union together two areas that need painting, and that can result in the entire screen being repainted. 
  - So, for example, if you have a fixed header at the top of the page, and something being painted at the bottom of the screen, the entire screen may end up being repainted.
    - On High DPI screens elements that are fixed position are automatically promoted to their own compositor layer. 
    - This is not the case on low DPI devices because the promotion changes text rendering from subpixel to grayscale, and layer promotion needs to be done manually.
  - Reducing paint areas is often a case of orchestrating your animations and transitions to not overlap as much, or finding ways to avoid animating certain parts of the page.
- Simplify paint complexity
  - When it comes to painting, some things are more expensive than others. 
  - For example, anything that involves a blur (like a `shadow`, for example) is going to take longer to paint than -- say -- drawing a red box.
  - The paint profiler will allow you to determine if you need to look at other ways to achieve effects. 
  - Ask yourself if it’s possible to use a cheaper set of styles or alternative means to get to your end result.
  - Where you can, you should try to avoid paint during animations in particular, as the 10ms you have per frame is normally not long enough to get paint work done, especially on mobile devices.

## Stick to Compositor-Only Properties and Manage Layer Count
- Tips
  - Stick to transform and opacity changes for your animations.
  - Promote moving elements with will-change or translateZ.
  - Avoid overusing promotion rules; layers require memory and management.
- Compositing is where the painted parts of the page are put together for displaying on screen.
- There are two key factors in this area that affect page performance
  - the number of compositor layers that need to be managed
  - the properties that you use for animations
- Use transform and opacity changes for animations
  - The best-performing version of the pixel pipeline avoids both layout and paint, and only requires compositing changes
  - There are only two properties that can be handled by the compositor alone  
  ```
  transform: translate(xpx, ypx);
  transform: scale(ratio);
  transform: rotate(ndeg);
  transform: skewX/Y(ndeg);
  transform: matrix/3d(...);
  opacity: 0~1
  ```
  - The caveat for the use of transforms and opacity is that the element on which you change these properties should be on its own compositor layer. 
  - In order to make a layer you must promote the element 
- Promote elements that you plan to animate
  - You should promote elements that you plan to animate (within reason, don’t overdo it!) to their own layer
  ```
  .moving-element {
    will-change: transform;
  }
  .moving-element {
    transform: translateZ(0);
  }
  ```
  - This gives the browser the forewarning that changes are incoming 
    - depending on what you plan to change, the browser can potentially make provisions, such as creating compositor layers.
- Manage layers and avoid layer explosions
  - It’s perhaps tempting, then, knowing that layers often help performance, to promote all the elements on your page with something like the following
  ```
  * {
    will-change: transform;
    transform: translateZ(0);
  }
  ```
  - This is a roundabout way of saying that you’d like to promote every single element on the page.
  - The problem here is that every layer you create requires memory and management, and that’s not free
  - On devices with limited memory, the impact on performance can far outweigh any benefit of creating a layer. 
  - Warning: Do not promote elements unnecessarily.
- Use Chrome DevTools to understand the layers in your app
  - Enable the Paint profiler in Chrome DevTools’ Timeline

## Debounce Your Input Handlers
- Tips
  - Avoid long-running input handlers; they can block scrolling.
  - Do not make style changes in input handlers.
  - Debounce your handlers; store event values and deal with style changes in the next requestAnimationFrame callback.
- Avoid long-running input handlers
- Avoid style changes in input handlers
- Debounce your scroll handlers







