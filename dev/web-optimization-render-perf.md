---
title: web-optimization-render-perf
tags: [browser, optimization, perf, web]
created: 2020-06-28T06:46:35.619Z
modified: 2021-01-04T17:09:19.278Z
---

# web-optimization-render-perf

# guide

- https://developers.google.com/web/fundamentals/performance/rendering/
- [浏览器渲染详细过程：重绘、重排和 composite 只是冰山一角](https://juejin.im/entry/590801780ce46300617c89b8)
- [浏览器的渲染过程2.0 — Composite](https://github.com/includeios/document/issues/10)
- [dom_performance_reflow_repaint.md](https://gist.github.com/faressoft/36cdd64faae21ed22948b458e6bf04d5)
- [浏览器的工作原理：浏览器幕后揭秘](https://www.html5rocks.com/zh/tutorials/internals/howbrowserswork/)
- [无线性能优化：Composite](https://fed.taobao.org/blog/taofed/do71ct/performance-composite/)
- [Things nobody ever taught me about CSS.](https://medium.com/@devdevcharlie/things-nobody-ever-taught-me-about-css-5d16be8d5d0e)

# summary

- What's the differences between rendering and painting event in Chrome DevTools Timeline View
  - Rendering events are about computing styles associated with each DOM node (i.e. "Style Recalculate") and elements position on the page ("Layout"). 
  - Paint category is about actually painting pixels and includes events like "Paint" itself and "Decode Image" / "Resize Image". 
  - In a nutshell, it's about inner structure vs. appearance -- if your page spends a lot of time rendering, this is because of the structure of its DOM and CSS (e.g. a large DOM tree), while significant paint times often mean the appearance of the page is affecting the performance (e.g. some styles are expensive to paint or an image is too large).
  - Layout has a notion of three-dimensions (z-indexes), structure (lines, boxes, flow) and parent-child relationships (trees). 
  - In painting, we flatten all of this information down to two-dimensions. The result of a paint is just a 2d-grid of pixels and their colors. It's what you see on the screen. All structure has been lost.
- 呈现器在创建完成并添加到呈现树时，并不包含位置和大小信息。计算这些值的过程称为布局或重排。
  - HTML采用基于流的布局模型，这意味着大多数情况下只要一次遍历就能计算出几何信息。处于流中靠后位置元素通常不会影响靠前位置元素的几何特征，因此布局可以按从左至右、从上至下的顺序遍历文档。
  - 布局是一个递归的过程。它从根呈现器（对应于HTML文档的 `<html>` 元素）开始，然后递归遍历部分或所有的框架层次结构，为每一个需要计算的呈现器计算几何信息。
  - 所有的呈现器都有一个“layout”或者“reflow”方法，每一个呈现器都会调用其需要进行布局的子代的layout方法。
  - 为避免对所有细小更改都进行整体布局，浏览器采用了一种“dirty 位”系统。如果某个呈现器发生了更改，或者将自身及其子代标注为“dirty”，则需要进行布局
- CSS2规范定义了绘制流程的顺序, 绘制的顺序其实就是元素进入堆栈样式上下文的顺序
  - 背景颜色、背景图片、边框、子代、轮廓
- defer vs async
  - defer与相比普通script，有两点区别：载入js文件时不阻塞HTML的解析，执行阶段被放到HTML标签解析完成之后
  - 在加载多个JS脚本的时候，async是无顺序的加载，而defer是有顺序的加载
- reflow vs repaint ? which one is more expensive ?
  - 哪个操作更占性能，要根据操作的类型、影响元素的范围来定
  - Paint is often the most expensive part of the pixel pipeline; avoid it where you can.
    - https://developers.google.com/web/fundamentals/performance/rendering/simplify-paint-complexity-and-reduce-paint-areas
  - Painting is, in general, cheaper than both style calculation and layout calculation; 
    - https://developer.mozilla.org/en-US/docs/Mozilla/Firefox/Performance_best_practices_for_Firefox_fe_engineers
  - 浏览器chrome练习结果
    - **resize**: csstrigger页面：前2组先放大再缩小，后两组先缩小再放大
      - scripting > rendering > painting > system > idle
        - 11 > 496  > 308 > 195 > 3771
        - 13 > 1425 > 493 > 296 > 2056
        - 6  > 841  > 186 > 110 > 1371
        - 10 > 712  > 365 > 227 > 3700
      - style > layout > paint > composite > UpdateLayerTree
        - 6   > 127 > 278 > 31 > 366
        - 123 > 597 > 464 > 31 > 823
        - 126 > 420 > 172 > 16 > 418
        - 6   > 224 > 345 > 23 > 483
      - **modal**/collapse-expand: 知乎回答页面
        - scripting > rendering > painting > system > idle
          - 607 > 120 > 113 > 204 > 6144
          - 603 > 117 > 96  > 192 > 6282
        - style > layout > paint > composite > UpdateLayerTree
          - 29 > 12 > 41 > 72 > 43
          - 24 > 15 > 29 > 68 > 43
      - **scroll**: bing国际版首页
        - scripting > rendering > painting > system > idle
          - 206 > 126 > 187 > 97 > 1778
          - 83  > 79  > 105 > 51 > 1613
        - style > layout > paint > composite > UpdateLayerTree
          - 22 > 6 > 25 > 163 > 59
          - 6  > 1 > 24 > 80  > 40
  - A reflow computes the layout of the page. 
    - A reflow on an element recomputes the dimensions and position of the element, 
    - and it also triggers further reflows on that element’s children, ancestors and elements that appear after it in the DOM. 
    - Then it calls a final repaint. Reflowing is very expensive.
- reflow vs layout
  - same
  - There's always at least one initial page layout together with a paint. After that, changing the input information which was used to construct the render tree may result in one or both of these:
    - parts of the render tree (or the whole tree) will need to be revalidated and the node dimensions recalculated. This is called a reflow, or layout, or layouting. Note that there's at least one reflow - the initial layout of the page
    - parts of the screen will need to be updated, either because of changes in geometric properties of a node or because of stylistic change, such as changing the background color. This screen update is called a repaint, or a redraw.
  - All of the below properties or methods, when requested/called in JavaScript, will trigger the browser to synchronously calculate the style and layout. This is also called reflow or layout thrashing, and is common performance bottleneck.
- 🤔 很多文章里说，修改opacity、transform这两个属性仅仅会触发合成，不会触发重绘和合成。所以一定要用这两个属性来实现动画，没有重绘重排，效率很高。
  - 并不一定是这样。
  - 只有一个元素在被提升为合成层之后，上述情况才成立。
  - 在合成多个合成层时，确实可以借助3D API的相关参数，从而直接实现合成层的transform、opacity效果。所以如果你将一个元素提升为合成层，然后用JS修改其transform或opacity 或者在 transform或opacity 上施加CSS过渡或动画，确实会避免CPU的Paint过程，因为transform和opacity可以直接基于GPU的合成参数来完成。
  - 对于没有提升为合成层的元素，仅仅是他自己具有transform和opacity，他是作为合成层的内容。而生成合成层的内容和写进位图或纹理是在Paint和Rasterize阶段完成的，因此这个元素的transform和opacity的实现也是在Paint和Rasterize中完成的。所以还是会重排，也就没有启用我们常说的GPU加速的动画。
- 重排Layout、强制重排Force Layout
  - 如果你改了一个影响元素布局信息的CSS样式，比如width、height、left、top等（transform除外），那么浏览器会将当前的Layout标记为dirty，这会使得浏览器在下一帧执行上述11个步骤的时候执行Layout。
    - 因为元素的位置信息变了，将可能会导致整个网页其他元素的位置情况都发生改变，所以需要执行Layout全局重新计算每个元素的位置。
    - 注意到，浏览器是在下一帧、下一次渲染的时候才重排。并不是JS执行完这一行改变样式的语句之后立即重排，所以你可以在JS语句里写100行改CSS的语句，但是只会在下一帧的时候重排一次。
  - 如果你在当前Layout被标记为dirty的情况下，访问了offsetTop、scrollHeight等属性，那么，浏览器会立即重新Layout，计算出此时元素正确的位置信息，以保证你在JS里获取到的offsetTop、scrollHeight等是正确的。这一过程被称为强制重排Force Layout，这一过程强制浏览器将本来在上述渲染流程中才执行的Layout过程提前至JS执行过程中。
    - 提前不是问题，问题在于每次你在Layout为dirty时访问会触发重排的属性，都会Force Layout，这极大的延缓了JS的执行效率
    - Layout一次的时间视DOM数量级从几十微秒到十几毫秒不等，这个开销是难以接受的。所以也就有了读写分离、纯用变量存储等避免Force Layout的方法。
    - 每次重排或者强制重排后，当前Layout就不再dirty。所以你再访问offsetWidth之类的属性，并不会再触发重排。

# Web Performance Overview

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

# Loading Performance Overview

- Regardless of the platform, network, or device, faster apps are better apps.
- https://web.dev/user-centric-performance-metrics/

# Measure performance with the RAIL model

- https://web.dev/rail/
- **RAIL** stands for four distinct aspects of web app life cycle: response, animation, idle, and load. 
- RAIL is a user-centric performance model that provides a structure for thinking about performance. 
- The model breaks down the user's experience into key actions (for example, tap, scroll, load) and helps you define performance goals for each of them.
- Tools for measuring RAIL 
  - Chrome DevTools
  - Lighthouse

# [Rendering Performance Overview](https://web.dev/rendering-performance/)

- Performance is the art of avoiding work, and making any work you do as efficient as possible.
- 60fps and Device Refresh Rates
  - Most devices today **refresh their screens 60 times a second**. 
  - If there’s an animation or transition running, or the user is scrolling the pages, the browser needs to match the device’s refresh rate and put up 1 new picture, or frame, for each of those screen refreshes
  - Each of those frames has a budget of just over 16ms (1second/60 = 16.66ms). 
  - In reality, however, the browser has housekeeping work to do, so all of your work needs to be completed inside 10ms. 
  - When you fail to meet this budget, the frame rate drops, and the content judders(抖动) on screen. 
  - This is often referred to as jank(卡顿)
- There are areas you have the most control over, and key points in the pixels-to-screen pipeline
  01. Trigger visual change by js or css
    - Typically JavaScript is used to handle work that will result in visual changes, whether it’s jQuery’s animate function, sorting a data set, or adding DOM elements to the page. 
    - It doesn’t have to be JavaScript that triggers a visual change, though: CSS Animations, Transitions, and the Web Animations API are also commonly used.
  02. Style calculations 
    - It is the process of **figuring out which CSS rules apply to which elements based on matching selectors**
    - for example, `.headline or .nav > .nav__item` . 
    - From there, once rules are known, they are applied and the final styles for each element are calculated.
  03. Layout/Reflow
    - Once the browser knows which rules apply to an element, it can begin to calculate how much space it takes up and where it is on screen. 
    - The web’s **layout model** means that one element can affect others
    - for example the width of the `<body>` element typically affects its children’s widths and so on all the way up and down the tree, so the process can be quite involved for the browser.
  04. Paint
    - Painting is the process of filling in pixels. 
    - It involves **drawing** out text, colors, images, borders, and shadows, essentially every visual part of the elements. 
    - The drawing is typically done onto multiple surfaces, often called layers.
    - Sometimes you may hear the term "rasterize" used in conjunction with paint. 
    - This is because painting is actually two tasks: 
      - creating a list of draw calls 
      - filling in the pixels.
      - The latter is called "rasterization" and so whenever you see paint records in DevTools, you should think of it as including rasterization.
      - In some architectures creating the list of draw calls and rasterizing are done in different threads, but that isn't something under developer control.
  05. Compositing(渲染层合并)
    - Since the parts of the page were drawn into potentially multiple layers, they need to be drawn to the screen in the correct order so that the page renders correctly.
    - This is especially important for elements that overlap another, since a mistake could result in one element appearing over the top of another incorrectly.
- Each of these parts of the pipeline represents an opportunity to introduce jank, so it's important to understand exactly what parts of the pipeline your code triggers.
- You won’t always necessarily touch every part of the pipeline on every frame. 
- In fact, there are three ways the pipeline normally plays out for a given frame when you make a visual change, either with JavaScript, CSS, or Web Animations:
- `JS/CSS > Style > Layout > Paint > Composite`
  - If you change a “layout” property, so that’s one that changes an element’s geometry, like its width, height, or its position with left or top, the browser will have to check all the other elements and “reflow” the page.
  - Any affected areas will need to be repainted, and the final painted elements will need to be composited back together.
- `JS/CSS > Style > Paint > Composite`
  - If you changed a “paint only” property, like a background image, text color, or shadows, in other words one that does not affect the layout of the page, then the browser skips layout
  - but it will still do paint.
- `JS/CSS > Style > Composite`
  - If you change a property that requires neither layout nor paint, and the browser jumps to just do compositing.
- If you want to know which of the three versions above changing any given CSS property will trigger, head to CSS Triggers.
  - https://csstriggers.com/
- If you want the fast track to high performance animations, read the section on changing compositor-only properties.

# Optimize JavaScript Execution

- Tips
  - Avoid `setTimeout` or `setInterval` for visual updates; always use `requestAnimationFrame` instead.
  - Move long-running JavaScript off the main thread to Web Workers.
  - Use micro-tasks to make DOM changes over several frames.
  - Use Chrome DevTools’ Timeline and JavaScript Profiler to assess the impact of JavaScript.
- JavaScript often triggers visual changes. 
  - Sometimes that's directly through style manipulations
  - Sometimes it's calculations that result in visual changes, like searching or sorting data. 
  - Badly-timed or long-running JavaScript is a common cause of performance issues. 
- The JavaScript you write is nothing like the code that is actually executed. 
  - Modern browsers use JIT compilers and all manner of optimizations and tricks to try and give you the fastest possible execution
- Use `requestAnimationFrame` for visual changes
  - The only way to guarantee that your JavaScript will run at the start of a frame is to use `requestAnimationFrame(doSth())` .
  - Frameworks or samples may use `setTimeout` or `setInterval` to do visual changes like animations, but the problem with this is that the callback will run at some point in the frame, possibly right at the end, and that can often have the effect of causing us to miss a frame, resulting in jank.
  - jQuery 3 was changed to use requestAnimationFrame
- Reduce complexity or use Web Workers
  - JavaScript runs on the browser’s main thread, right alongside style calculations, layout, and, in many cases, paint. 
  - If your JavaScript runs for a long time, it will block these other tasks, potentially causing frames to be missed.
  - In many cases you can move pure computational work to Web Workers, if, for example, it doesn’t require DOM access. Data manipulation or traversal, like sorting or searching, are often good fits for this model, as are loading and model generation.
  - Not all work can fit this model: Web Workers do not have DOM access. Where your work must be on the main thread, consider a batching approach, where you segment the larger task into micro-tasks, each taking no longer than a few milliseconds, and run inside of requestAnimationFrame handlers across each frame.
  - There are UX and UI consequences to this approach, and you will need to ensure that the user knows that a task is being processed, either by using a progress or activity indicator. In any case this approach will keep your app's main thread free, helping it to stay responsive to user interactions.
- Know your JavaScript’s “frame tax”
  - When assessing a framework, library, or your own code, it’s important to assess how much it costs to run the JavaScript code on a frame-by-frame basis. This is especially important when doing performance-critical animation work like transitioning or scrolling.
  - The Performance panel of Chrome DevTools is the best way to measure your JavaScript's cost. 
  - The Main section provides a flame chart of JavaScript calls so you can analyze exactly which functions were called and how long each took
  - You should seek to either remove long-running JavaScript, or, if that’s not possible, move it to a Web Worker freeing up the main thread to continue on with other tasks.
- Avoid micro-optimizing your JavaScript
  - It may be cool to know that the browser can execute one version of a thing 100 times faster than another thing, like that requesting an element’s `offsetTop` is faster than computing `getBoundingClientRect()`
  - but it’s almost always true that you’ll only be calling functions like these a small number of times per frame
  - so it’s normally wasted effort to focus on this aspect of JavaScript’s performance. You'll typically only save fractions of milliseconds.
- ref
  - https://zhuanlan.zhihu.com/p/39878259

# Reduce the Scope and Complexity of Style Calculations

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

# Avoid Large, Complex Layouts and Layout Thrashing(Reflow)

- Tips
  - Layout is normally scoped to the whole document.
  - The number of DOM elements will affect performance; you should avoid triggering layout wherever possible.
  - Assess layout model performance; new Flexbox is typically faster than older Flexbox or float-based layout models.
  - Avoid forced synchronous layouts and layout thrashing; read style values then make style changes.
- Layout is where the browser figures out the geometric information for elements: their size and location in the page.
- Each element will have explicit or implicit sizing information based on the CSS that was used, the contents of the element, or a parent element. 
- The process is called *Layout* in Chrome, Opera, Safari, and Internet Explorer. 
  - In Firefox it’s called *Reflow*
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

``` js
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

``` js
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

``` js
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

``` js
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

# Simplify Paint Complexity and Reduce Paint Areas

- Tips
  - Changing any property apart from transform or opacity always triggers paint.
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
  - The **best way to create a new layer is to use the `will-change` CSS property**. 
  - This will work in Chrome, Firefox and Opera, and, with a value of `transform` , will create a new compositor layer
  - For browsers that don’t support `will-change` , but benefit from layer creation, such as Safari and Mobile Safari, you need to (mis)use a 3D transform to force a new layer

``` css
  .moving-element {
    will-change: transform;
    /* 或者 */
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
  - For example, anything that involves a blur (like a `shadow` , for example) is going to take longer to paint than -- say -- drawing a red box.
  - The paint profiler will allow you to determine if you need to look at other ways to achieve effects. 
  - Ask yourself if it’s possible to use a cheaper set of styles or alternative means to get to your end result.
  - Where you can, you should try to avoid paint during animations in particular, as the 10ms you have per frame is normally not long enough to get paint work done, especially on mobile devices.

# Stick to Compositor-Only Properties and Manage Layer Count

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

``` css
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

``` css
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

``` css

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

# Debounce Your Input Handlers

- Tips
  - Avoid long-running input handlers; they can block scrolling.
  - Do not make style changes in input handlers.
  - Debounce your handlers; store event values and deal with style changes in the next requestAnimationFrame callback.
- Avoid long-running input handlers
- Avoid style changes in input handlers
- Debounce your scroll handlers

# Minimizing browser reflow

- [Minimizing browser reflow](https://developers.google.com/speed/docs/insights/browser-reflow)

- Reflow is the name of the web browser process for re-calculating the positions and geometries of elements in the document, for the purpose of re-rendering part or all of the document. 
- Because reflow is a user-blocking operation in the browser, it is useful for developers to understand how to improve reflow time and also to understand the effects of various document properties (DOM depth, CSS rule efficiency, different types of style changes) on reflow time. 
- Sometimes reflowing a single element in the document may require reflowing its parent elements and also any elements which follow it.
- Here are some easy guidelines to help you minimize reflow in your web pages:
  - Reduce unnecessary DOM depth. 
    - Changes at one level in the DOM tree can cause changes at every level of the tree - all the way up to the root, and all the way down into the children of the modified node. 
    - This leads to more time being spent performing reflow.
  - Minimize CSS rules, and remove unused CSS rules.
  - If you make complex rendering changes such as animations, do so out of the flow. 
    - Use position-absolute or position-fixed to accomplish this.
  - Avoid unnecessary complex CSS selectors 
    - descendant selectors in particular
    - which require more CPU power to do selector matching.

# REFLOWS & REPAINTS: CSS PERFORMANCE MAKING YOUR JAVASCRIPT SLOW?

- [EFLOWS & REPAINTS: CSS PERFORMANCE MAKING YOUR JAVASCRIPT SLOW?](http://www.stubbornella.org/content/2009/03/27/reflows-repaints-css-performance-making-your-javascript-slow/)

- A repaint occurs when changes are made to an elements skin that changes visibility, but do not affect its layout. 
  - Examples of this include outline, visibility, or background color. 
- According to Opera, repaint is expensive because the browser must verify the visibility of all other nodes in the DOM tree. 
- A reflow is even more critical to performance because it involves changes that affect the layout of a portion of the page (or the whole page). 
  - Reflow of an element causes the subsequent reflow of all child and ancestor elements as well as any elements following it in the DOM.
  - Reflows are very expensive in terms of performance, and is one of the main causes of slow DOM scripts, especially on devices with low processing power, such as phones. 
  - In many cases, they are equivalent to laying out the entire page again.
- causing a reflow
  - Resizing the window
  - Changing the font
  - Adding or removing a stylesheet
  - Content changes, such as a user typing text in an input box
  - Activation of CSS pseudo classes such as :hover (in IE the activation of the pseudo class of a sibling)
  - Manipulating the class attribute
  - A script manipulating the DOM
  - Calculating offsetWidth and offsetHeight
  - Setting a property of the style attribute
- How to avoid reflows or at least minimize their impact on performance
- Change classes as low in the dom tree as possible and thus limit the scope of the reflow to as few nodes as possible. 
  - For example, you should avoid changing a class on wrapper elements to affect the display of child nodes. 
- Avoid setting multiple inline styles
  - We all know interacting with the DOM is slow. We try to group changes in an invisible DOM tree fragment and then cause only one reflow when the entire change is applied to the DOM. 
  - Similarly, setting styles via the style attribute cause reflows. Avoid setting multiple inline styles which would each cause a reflow, 
  - the styles should be combined in an external class which would cause only one reflow when the class attribute of the element is manipulated.
- Apply animations with position fixed or absolute
  - Apply animations to elements that are position fixed or absolute. 
  - They don’t affect other elements layout, so they will only cause a repaint rather than a full reflow. 
- Trade smoothness for speed
  - you may want to move an animation 1 pixel at a time, but if the animation and subsequent reflows use 100% of the CPU the animation will seem jumpy as the browser struggles to update the flow. 
  - Moving the animated element by 3 pixels at a time may seem slightly less smooth on very fast machines, but it won’t cause CPU thrashing on slower machines and mobile devices.
- Avoid table for layout (or set table-layout fixed)
  - As if you needed another reason to avoid them, tables often require multiple passes before the layout is completely established 
  - because they are one of the rare cases where elements can affect the display of other elements that came before them on the DOM. 
  - Imagine a cell at the end of the table with very wide content that causes the column to be completely resized. 
  - This is why tables are not rendered progressively in all browsers (thanks to Bill Scott for this tip) and yet another reason why they are a bad idea for layout. 
  - According to Mozilla, even minor changes will cause reflows of all other nodes in the table.
  - Any value for table-layout other than "auto" will trigger a fixed layout and allow the table to render row by row 
  - In this manner, the user agent can **begin to lay out the table once the entire first row has been received**. 
  - Cells in subsequent rows do not affect column widths. 
  - Any cell that has content that overflows uses the `overflow` property to determine whether to clip the overflow content.
  - This algorithm may be inefficient since it requires the user agent to have access to all the content in the table before determining the final layout and may demand more than one pass.
- Avoid JavaScript expressions in the CSS
  - The main reason these expressions are so costly is because they are recalculated each time the document, or part of the document, reflows.
- We recommended putting a `link` tag in the head because, while it was one second slower (6.3 to 7.3 seconds) all the other methods blocked progressive rendering. 

 - 

# Pixels are expensive

- [Pixels are expensive](https://aerotwist.com/blog/pixels-are-expensive/)
01. Recalculate Style
  - This is the first part that the article looked at, and it pertains(关于) to selector matching and figuring out which styles apply to which parts of the DOM.
  - Normally, however, this is super fast unless you have a DOM tree with massive elements
  - For the most part optimizing, selector matching is going to give minimal returns.
02. Layout
  - In layout we figure out the geometry of the page, i.e. where each element is on the page. 
  - This is where things can start to get a little more computationally expensive as the way elements are laid out is contingent; where one element lives is normally affected by another. 
  - If I change the dimensions of `<body>` , then chances are the things inside of it will also need to change.
03. Paint
  - Now we know where the elements are, we need to fill in their pixels, 
  - and this is where you’re going to **spend the vast majority of your time**. 
  - If you trigger paint you’re going to feel it. Well, your users definitely will when your site struggles along.
  - If you change a layout property, you are almost certainly going to trigger paint.
04. Composite
  - we sometimes separate elements out into distinct layers, called compositor layers. 
  - When we’re done with these layers we smush them all back together, which is compositing.
- AVOIDING PERFORMANCE BOTTLENECKS
  - What it boils down to is only changing properties that trigger compositing rather than layout or paint
- TOOLS, NOT RULES AND A BRIGHTER FUTURE
  - The really good news is that things are also getting much faster. At this year’s Google I/O we showed fast, fluid, continous animations at 60fps in Chrome on Android

# What Every Frontend Developer Should Know About Webpage Rendering

- [What Every Frontend Developer Should Know About Webpage Rendering](http://frontendbabel.info/articles/webpage-rendering-101/)
- How do browsers render a web page
  1. The DOM (Document Object Model) is formed from the HTML that is received from a server.
  2. Styles are loaded and parsed, forming the CSSOM (CSS Object Model).
  03. On top of DOM and CSSOM, a rendering tree is created, 
    - which is a set of objects to be rendered (Webkit calls each of those a "renderer" or "render object", while in Gecko it's a "frame"). 
    - Render tree reflects the DOM structure except for invisible elements (like the `<head>` tag or elements that have `display:none;` set). 
    - Each text string is represented in the rendering tree as a separate renderer. 
    - Each of the rendering objects contains its corresponding DOM object (or a text block) plus the calculated styles. 
    - In other words, the render tree describes the visual representation of a DOM.
  04. For each render tree element, its coordinates are calculated, which is called "layout". 
    - Browsers use a flow method which only required one pass to layout all the elements
    - tables require more than one pass
  05. Finally, this gets actually displayed in a browser window, a process called "painting".
- Repaint
  - When changing element styles which don't affect the element's position on a page (such as background-color, border-color, visibility), the browser just repaints the element again with the new styles applied (that means a "repaint" or "restyle" is happening).
- Reflow
  - When the changes affect document contents or structure, or element position, a reflow (or relayout) happens. These changes are usually triggered by:
    - DOM manipulation (element addition, deletion, altering, or changing element order);
    - Contents changes, including text changes in form fields;
    - Calculation or altering of CSS properties;
    - Adding or removing style sheets;
    - Changing the "class" attribute;
    - Browser window manipulation (resizing, scrolling);
    - Pseudo-class activation (:hover).
- How browsers optimize rendering
  - Browsers are doing their best to restrict repaint/reflow to the area that covers the changed elements only. 
  - For example, a size change in an absolute/fixed positioned element only affects the element itself and its descendants, 
    - whereas a similar change in a statically positioned element triggers reflow for all the subsequent elements.
  - Another optimization technique is that while running pieces of JavaScript code, browsers cache the changes, and apply them in a single pass after the code was run.
  - However, accessing an element property triggers a forced reflow. 
    - This will happen if we add an extra line that reads an element property
    - As a result, we get 2 reflows instead of one. 
    - Because of this, you should group reading element properties together to optimize performance
  - There are situations when you have to trigger a forced reflow. 
    - Example: we have to apply the same property ("margin-left" for example) to the same element twice.

- **Practical advice on optimization**
- Create valid HTML and CSS, do not forget to specify the document encoding. 
  - Styles should be included into `<head>` , and scripts appended to the end of the `<body>` tag.
- Try to simplify and optimize CSS selectors (this optimization is almost universally ignored by developers who mostly use CSS preprocessors). 
  - Keep nesting levels at a minimum. 
  - This is how CSS selectors rank according to their performance (starting from the fastest ones):
    - Identificator: #id
    - Class: .class
    - Tag: div
    - Adjacent sibling selector: a + i
    - Parent selector: ul > li
    - Universal selector: *
    - Attribute selector: `input[type="text"]`
    - Pseudoclasses and pseudoelements: a:hover 
  - You should remember that browsers process selectors from right to left, that's why the **rightmost selector should be the fastest one**, either #id or .class
- In your scripts, minimize DOM manipulation whenever possible. 
  - Cache everything, including properties and objects (if they are to be reused). 
  - It's better to work with an "offline" element when performing complicated manipulations (an "offline" element is one that is disconnected from DOM and only stored in memory), and append it to DOM afterwards.
- If you use jQuery to select elements, follow jQuery selectors best practices.
  - https://learn.jquery.com/performance/optimize-selectors/
- To change element's styles, modifying the "class" attribute is one of the most performant ways. 
  - The deeper in the DOM tree you perform this change, the better (also because this helps decouple logic from presentation).
- Animate only absolute/fixed positioned elements if you can.
- It is a good idea to disable complicated `:hover` animations while scrolling (e.g. by adding an extra "no-hover" class to `<body>` ). 

# 10 Ways to Minimize Reflows and Improve Performance

- [10 Ways to Minimize Reflows and Improve Performance](https://www.sitepoint.com/10-ways-minimize-reflows-improve-performance/)

- A repaint occurs when changes are made to elements that affect visibility but not the layout. 
  - For example, opacity, background-color, visibility, and outline. 
  - Repaints are expensive because the browser must check the visibility of all other nodes in the DOM
  - one or more may have become visible beneath the changed element.
- Reflows have a bigger impact. 
  - This refers to the re-calculation of positions and dimensions of all elements, which leads to re-rendering part or all of the document. 
  - Changing a single element can affect all children, ancestors, and siblings.
- Both are browser-blocking; 
  - neither the user or your application can perform other tasks during the time that a repaint or reflow occurring. 
  - In extreme cases, a CSS effect could lead to slower JavaScript execution.
  - This is one of the reasons you encounter issues such as jerky scrolling and unresponsive interfaces.
- reflows are triggered
  - Adding, removing or changing visible DOM elements
  - Adding, removing or changing CSS styles
  - CSS3 animations and transitions
  - Using offsetWidth and offsetHeight
  - User actions like `:hover`
01. Use Best-Practice Layout Techniques
  - An inline style will affect layout as the HTML is downloaded and trigger an additional reflow. 
  - Tables are expensive because the parser requires more than one pass to calculate cell dimensions. 
  - Using `table-layout: fixed` can help when presenting tabular data since column widths are based on the header row content.
  - Using `flexbox` for your main page layout can also have a performance hit because the position and dimensions of flex items can change as the HTML is downloaded.
02. Minimize the Number of CSS Rules
  - The fewer rules you use, the quicker the reflow. You should also avoid complex CSS selectors where possible.
03. Minimize DOM depths
  - reduce the size of your DOM tree and the number of elements in each branch. 
  - The smaller and shallower your document, the quicker it can be reflowed. 
  - It may be possible to remove unnecessary wrapper elements if you’re not supporting older browsers.
04. Update Classes Low in the DOM Tree
  - Make class changes on elements as low in the DOM tree as possible
  - i.e. elements that don’t have multiple deeply nested children. 
  - This can limit the scope of the reflow to as few nodes as necessary. 
  - In essence, only apply class changes to parent nodes such as wrappers if the effect on nested children is minimal.
- 5. Remove Complex Animations From the Flow
  - Ensure animations apply to a single element by removing them from the document flow with `position: absolute;` or `position: fixed;` . 
  - This permits the dimensions and position to be modified without affecting other elements in the document.
06. Modify Hidden Elements
  - Elements hidden with `display: none;` will not cause a repaint or reflow when they are changed. 
  - If practical, make changes to the element before making it visible.
07. Update Elements in Batch
  - Performance can be improved by updating all DOM elements in a single operation. This simple example causes three reflows
  - use DOM fragment and building the nodes in memory first
08. Limit the Affected Elements
  - Avoid situations where a large number of elements could be affected.
  - Consider a tabbed content control where clicking a tab activates a different content block. The surrounding elements would be affected if each content block had a different height. 
  - You may be able to improve performance by setting a fixed height for the container or removing the control from the document flow.
09. Recognize that Smoothness Compromises Performance
  - Moving an element one pixel at a time may look smooth but slower devices can struggle. 
  - Moving the element by four pixels per frame requires one quarter of the reflow processing and may only be slightly less smooth.
10. Analyze Repaint Issues with Browser Tools
  - In Blink/Webkit browsers such as Chrome, Safari, and Opera, open the `Timeline` panel and record an activity

# Browser Under the Hood

- [Animation Performance 101: Browser Under the Hood](https://www.viget.com/articles/animation-performance-101-browser-under-the-hood/)

- Good performance means hitting the ultimate goal of 60 frames per second (FPS). 
  - That’s because most devices these days refresh their screen at a rate of 60 times a second. 
  - The browser needs to match this rate and paint a new frame on each refresh.
  - Otherwise, the animation will look like it’s not changing and move erratically
- The rendering process is a waterfall — each step triggers everything after it. 
  - If the browser does Layout, it must also do Paint and Composite Layers.
  - The higher you start on the waterfall, the more work it takes. 
- The browser has two threads — the main thread and compositor thread. 
- The main thread is where the bulk of the work happens, including Javascript, Recalculate Styles, Layout, and Paint. 
  - All the most intensive tasks are run there, leading it to routinely stall for tens to even hundreds of milliseconds at a time. Pretty scary. 
- The compositor thread is responsible for Composite Layers and other rendering operations.
- Both threads send over their work to the Central Processing Unit (CPU). 
  - It’s responsible for processing almost everything. 
  - In the past, all work was sent to the CPU; but nowadays, modern browsers are able to offload some of it onto the Graphics Processing Unit (GPU)
- Only certain types of work get kicked to the GPU. 
  - To qualify, the operation must not trigger main thread work like Layout and Javascript. 
  - This means it can be handled by the compositor thread alone. 
  - Thus, the browser can apply a compositing optimization, which results in the creation of a new compositor layer. 
  - The layer is then uploaded to and rendered by the GPU. 
  - This process is known as hardware-acceleration.
- Hardware-acceleration has huge implications for animation. 
  - When an element is on its own compositor layer, it does not touch or affect the rest of the page, 
  - so it can be moved around cheaply without triggering the waterfall on neighboring elements. 
- The only catch here is that most elements don’t get hardware-accelerated onto the GPU. 
  - The browser decides what does and does not qualify
- To reduce the browser’s workload, we should:
  - Avoid triggering the top of the rendering waterfall.
  - Avoid the main thread.
  - Take advantage of the compositor thread and GPU.
- Let’s put it all together — the most performant way to animate is **with CSS `keyframe` animations or transitions on `transform` and `opacity` only**. This meets our criteria by following these guidelines:
- Only Animate Composite Layers Properties
  - This boils down to two properties — transform and opacity. It may sound limiting, but a lot can be done with transform alone!
  - Avoid animating Layout and Paint: Paint is especially bad for low-end devices and mobile phones because of their weaker CPUs. This doesn’t mean you should never animate these properties; just be mindful and avoid whenever possible, especially if it affects a large part of the page.
- Use CSS over Javascript
  - Avoid animating with Javascript because it always runs on the main thread, making it more likely to drop frames if the thread is bogged down with other tasks. 
  - CSS-based animations are better because they can take advantage of the GPU
- Leverage Hardware-Acceleration
  - The browser automatically hardware-accelerates any element with a CSS `transition` or `keyframe` animation on transform or opacity. 
  - This is because such operations don’t trigger main thread work and can be handled by the compositor alone.
  - In order to keep the element from being reabsorbed, we need to apply `will-change`
  - Only use will-change on elements that’ll change often. 
  - Otherwise, using CSS keyframes and transitions can provide many performance benefits, along with avoiding Layout, Paint, and excess Javascript

# Analyze Runtime Performance

- [Analyze Runtime Performance](https://docs.microsoft.com/en-us/microsoft-edge/devtools-guide-chromium/rendering-tools/)
- Tips
  - Do not write JavaScript that forces the browser to recalculate layout. 
    - Separate read and write functions, and perform reads first.
  - Do not over-complicate your CSS. 
    - Use less CSS and keep your CSS selectors simple.
  - Avoid layout as much as possible. 
    - Choose CSS that does not trigger layout at all.
  - Painting may take up more time than any other rendering activity. 
    - Watch out for paint bottlenecks.
- Layout (or reflow in Firefox) is the process by which the browser calculates the positions and sizes of all the elements on a page. 
  - The layout model of the web means that one element may affect others; 
  - for example, the width of the `<body>` element typically affects the widths of any child elements, and so on, all the way up and down the tree. The process may be quite involved for the browser.
- As a general rule of thumb, if you ask for a geometric value back from the DOM before a frame is complete, you are going to find yourself with "forced synchronous layouts", which may be a big performance bottleneck if repeated frequently or performed for a large DOM tree.
  - Batch your style reads first, then do any writes.
  - Automatically batch read-write operations using FastDom library.
- Paint is the process of filling in pixels. It is often the most costly part of the rendering process. 
  - If you noticed that your page is janky in any way, it is likely that you have paint problems.
- Compositing is where the painted parts of the page are put together for displaying on screen.
  - For the most part, if you stick to compositor-only properties and avoid paint altogether, you should see a major improvement in performance

# Accurately measuring layout on the web

- [Accurately measuring layout on the web](https://nolanlawson.com/2018/09/25/accurately-measuring-layout-on-the-web/)

- the technique about how to schedule an event to fire after style/layout calculations are complete, is now captured in a web API proposal called `requestPostAnimationFrame` . There is also a good polyfill called `afterframe`
- The web rendering pipeline
  - Execute JavaScript – executing (but not necessarily compiling) JavaScript, including any state manipulation, “virtual DOM diffing, ” and modifying the DOM.
  - Calculate style – taking a CSS stylesheet and matching its selector rules with elements in the DOM. This is also known as “formatting.”
  - Calculate layout – taking those CSS styles we calculated in step #2 and figuring out where the boxes should be laid out on the screen. This is also known as “reflow.”
  - Render – the process of actually putting pixels on the screen. This often involves painting, compositing, GPU acceleration, and a separate rendering thread.
- The render step is much more complicated to measure, and indeed it’s impossible to measure accurately, because rendering is often a complex interplay between separate threads and the GPU, and therefore isn’t even visible to userland JavaScript running on the main thread.
- Style and layout calculations, however, are 100% measurable because they block the main thread. 
  - And yes, this is true even with something like Firefox’s Stylo engine – even if multiple threads can be employed to speed up the work, ultimately the main thread has to wait on all the other threads to deliver the final result.
- Now, per the HTML5 event loop spec, `requestAnimationFrame` is indeed supposed to fire before style and layout are calculated
- the spec would have two timers – one for `requestAnimationFrame` , and another for `requestAnimationFrameAfterStyleAndLayout` (or something like that)
- There’s no solution that will work perfectly to place a callback right after style and layout, but based on the advice of Todd Reifsteck, I believe this comes closest

``` JS
requestAnimationFrame(() => {
  setTimeout(() => {
    performance.mark('end')
  })
})
```

- The trick is to queue a `setTimeout` callback inside of a `rAF` , which ensures that the second callback happens after style and layout, regardless of whether the browser is spec-compliant or not.
- `Promise` doesn’t work at all, because microtasks (e.g. Promises) run immediately after JavaScript execution has completed. So it doesn’t wait for style and layout at all
