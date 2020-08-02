---
title: note-web-browser-blog
tags: [blog, browser, web]
created: '2020-07-10T08:47:31.574Z'
modified: '2020-08-02T07:44:09.095Z'
---

# note-web-browser-blog

## Performance best practices for Firefox front-end engineers

- [Performance best practices for Firefox front-end engineers](https://developer.mozilla.org/en-US/docs/Mozilla/Firefox/Performance_best_practices_for_Firefox_fe_engineers)

- Avoid the main thread where possible
  - The main thread is where we process user events and do painting. 
  - It's also important to note that most of our JavaScript runs on the main thread, so it's easy for script to cause delays in event processing or painting. 
  - That means that the more code we can get off of the main thread, the more that thread can respond to user events, paint, and generally be responsive to the user.
  - You might want to consider using a `Worker` if you need to do some computation that can be done off of the main thread. 
  - If you need more elevated privileges than a standard worker allows, consider using a `ChromeWorker` , which is a Firefox-only API which lets you create workers with more elevated privileges.

- Use `requestIdleCallback()`
  - If you simply cannot avoid doing some kind of long job on the main thread, try to break it up into smaller pieces that you can run when the browser has a free moment to spare, and the user isn't doing anything. 
  - You can do that using requestIdleCallback() 

- Get familiar with the pipeline that gets pixels to the screen
  - The rendering process goes through the following steps
  - js > style > layout > paint > composite
  - To achieve a 60 FPS frame rate, all of the above has to happen in 16 milliseconds or less, every frame.
  - `requestAnimationFrame()` lets you queue up JavaScript to run right before the style flush occurs. 
  - This allows you to put all of your DOM writes (most importantly, anything that could change the size or position of things in the DOM) just before the style and layout steps of the pipeline, combining all the style and layout calculations into a single batch so it all happens once, in a single frame tick, instead of across multiple frames.
  - This also means that `requestAnimationFrame(` ) is not a good place to put queries for layout or style information.

- Detecting and avoiding synchronous style flushes
  - What are style flushes?
    - When CSS is applied to a document (HTML or XUL, it doesn’t matter), the browser does calculations to figure out **which CSS styles will apply to each element**.
    - This happens the first time the page loads and the CSS is initially applied, but can happen again if JavaScript modifies the DOM.
  - Because styles are normally scoped to the entire document, the cost of doing these style calculations is proportional to the number of DOM nodes in the document (and the number of styles being applied).
  - It is expected that over time, script will update the DOM, requiring us to recalculate styles. 
  - Normally, the changes to the DOM just result in the standard style calculation occurring immediately after the JavaScript has finished running during the 16ms window, inside the "Style" step. That's the ideal scenario.
  - However, it's possible for script to do things that force multiple style calculations (or style flushes) to occur synchronously during the JavaScript part of the 16 ms window. 
  - The more of them there are, the more likely they'll exceed the 16ms frame budget. 
  - If that happens, some of them will **be postponed until the next frame** (or possibly multiple frames, if necessary), this skipping of frames is called jank.
  - Generally speaking, you force a synchronous style flush, any time you query for style information after the DOM has changed within the same frame tick
  - Depending on whether or not the style information you’re asking for has something to do with size or position, you may also cause a layout recalculation (also referred to as layout flush or reflow), which is also an expensive step
  - To avoid this: avoid reading style information if you can. 
    - If you must read style information, do so at the very beginning of the frame, before any changes have been made to the DOM since the last time a style flush occurred.
    - Historically, there hasn't been an easy way of doing this
  - If you want to queue up some JavaScript to run after the next "natural" style and layout flush, try `window.promiseDocumentFlushed`
  - promiseDocumentFlushed is only available to priviledged script, and should be called on the inner window of a top-level frame.

- Writing tests to ensure you don’t add more synchronous style flushes
  - Unlike reflow, there isn’t a “observer” mechanism for style recalculations
  - Note that your test and function must be called synchronously in order for this test to be accurate. 
  - If you ever go back to the event loop (by yielding, waiting for an event, etc), style flushes unrelated to your code are likely to run, and your test will give you a false positive.

- Detecting and avoiding synchronous reflow
  - This is also sometimes called “sync layout”, "sync layout flushes" or “sync layout calculations”
  - The first time a document (XUL or HTML) loads, we parse the markup, and then apply styles. Once the styles have been calculated, we then need to calculate where things are going to be placed on the page. 
  - This layout step can be seen in the “16ms” pipeline graphic above, and occurs just before we paint things to be composited for the user to see.
  - It is expected that over time, script will update the DOM, requiring us to recalculate styles, and then update layout. 
  - Normally, however, the changes to the DOM just result in the standard style calculation that occurs immediately after the JavaScript has finished running during the 16ms window.

- Interruptible reflow
  - Since the early days, Gecko has had the notion of interruptible reflow. 
  - This is a special type of content-only reflow that checks at particular points whether or not it should be interrupted (usually to respond to user events).
  - Because interruptible reflows can only be interrupted when laying out content, and not chrome UI, the rest of this section is offered only as context.
  - When an interruptible reflow is interrupted, 
    - what really happens is that certain layout operations can be skipped in order to paint and process user events sooner.
    - the best-case scenario is that all layout is skipped, and the layout operation ends.
    - the worst-case scenario is that none of the layout can be skipped despite being interrupted, and the entire layout calculation occurs.
  - Reflows that are triggered "naturally" by the 16ms tick are all considered interruptible. 
  - Despite not actually being interuptible when laying out chrome UI, striving for interruptible layout is always good practice because uninterruptible layout has the potential to be much worse
  - To repeat, only interruptible reflows in web content can be interrupted.

- Uninterruptible reflow
  - Uninterruptible reflow occurs when some DOM node’s styles have changed such that the size or position of one or more nodes in the document will need to be updated, and then JavaScript asks for the size or position of anything.
  - Since everything is pending a reflow, the answer isn't available, so everything stalls until the reflow is complete and the script can be given an answer. 
  - Flushing layout also means that styles must be flushed to calculate the most up-to-date state of things, so it's a double-whammy(双重灾难).
  - If you can avoid querying for the size or position of things in JavaScript, that’s the safest option
  - Note that given the same changes to the DOM of a chrome UI document, a single synchronous uninterruptible reflow is no more computationally expensive than an interruptible reflow triggered by the 16ms tick. 
  - It is, however, advantageous to strive for reflow to only occur in the one place (the layout step of the 16ms tick) as opposed to multiple times during the 16ms tick (which has a higher probability of running through the 16ms budget).

- How do I avoid triggering uninterruptible reflow?
  - [What forces layout/reflow](https://gist.github.com/paulirish/5d52fb081b3570c81e3a)
  -  Note that some items in the list may be browser-specific or subject to change, and that an item not occurring explicitly in the list doesn't mean it doesn't cause reflow.
  - When enumerating properties on DOM objects (e.g. elements/nodes, events, windows, etc.), accessing the value of each enumerated property will almost certainly (accidentally) cause uninterruptible reflow, because a lot of DOM objects have one or even several properties that do so.
  - Note that queries for size and position information are only expensive if the DOM has been written to. 
  - Otherwise, we're doing a cheap look-up of cached information. 
  - If we work hard to move all DOM writes into `requestAnimationFrame()` , then we can be sure that all size and position queries are cheap.
  - It's also possible (though less infallible than `promiseDocumentFlushed` ) to queue JavaScript to run very soon after the frame has been painted, where the likelihood is highest that the DOM has not been written to, and layout and style information queries are still cheap. 
  - This can be done by using a setTimeout or dispatching a runnable inside a requestAnimationFrame callback, for example

``` JS
requestAnimationFrame(() => {
  setTimeout(() => {
    // This code will be run ASAP after Style and Layout information have
    // been calculated and the paint has occurred. Unless something else
    // has dirtied the DOM very early, querying for style and layout information
    // here should be cheap.
  }, 0);
});
```

  - This also implies that querying for size and position information in `requestAnimationFrame()` has a high probability of causing a synchronous reflow.  

- Below you'll find some suggestions for other methods which may come in handy when you need to do things without incurring synchronous reflow. 
  - These methods generally return most-recently-calculated value for the requested value, which means the value may no longer be current, but may still be "close enough" for your needs. 
  - Unless you need precisely accurate information, they can be valuable tools in your performance toolbox.
  - `nsIDOMWindowUtils.getBoundsWithoutFlushing()`
  - `nsIDOMWindowUtils.getRootBounds()`
  - `nsIDOMWindowUtils.getScrollXY()`
- Writing tests to ensure you don’t add more unintentional reflow
  - The interface `nsIReflowObserver` lets us detect both interruptible and uninterruptible reflows

- Detecting over-painting with paint flashing
  - Painting is, in general, cheaper than both style calculation and layout calculation; 
  - still, the more you can avoid, the better.
  - Generally speaking, the larger an area that needs to be repainted, the longer it takes. Similarly, the more things that need to be repainted, the longer it takes.
  - Our graphics team has added a handy feature to help you detect when and where paints are occurring. This feature is called **paint flashing**, 
  - and it can be activated for both web content and the browser chrome. 
  - Paint flashing tints each region being painted with a randomly selected color so that it’s more easy to see what on the screen is being painted.
  - The worst case is called **over-painting**. 
    - This is when you draw multiple times over the same space. 
    - Unless transparency is involved, all but the last painting will be overwritten, becoming unnecessary.
  - Keep in mind that painting occurs on the main thread. 
  - Remember, too, that the goal is to have as little happen on the main thread as possible. 
    - That means that finding and removing (when possible) over-painting is a good place to start reducing your burden on the main thread, which will in turn improve performance.
- Consider using a different animation that can be accelerated by the GPU. 
  - These GPU-accelerated animations occur off of the main thread, and have a much higher probability of running at 60 FPS 
  - Sometimes, our graphics layer invalidates regions in ways that might not be clear to you, and a section outside of the thing that just repainted will also repaint. 
    - Sometimes this can be addressed by ensuring that the thing changing is on its own layer (though this comes at a memory cost). 
    - You can put something on its own layer by setting its `z-index` , or by setting the `will-change` on the node, though this should be used sparingly.
  - If you’re unsure why something is repainting, consider talking to our always helpful graphics team in the gfx room on Matrix

- Adding nodes using DocumentFragments
  - Sometimes you need to add several DOM nodes as part of an existing DOM tree. 
  - Inserting items into the DOM has a cost. 
  - If you're adding a number of children to a DOM node in a loop, it's often more efficient to batch them into a single insertion by creating a `DocumentFragment` , adding the new nodes to that, then inserting the `DocumentFragment` as a child of the desired node.
  - A DocumentFragment is maintained in memory outside the DOM itself, so changes don't cause reflow.

- The Gecko profiler add-on is your friend

- Don’t guess—measure.
  - If you’re working on a performance improvement, this should go without saying: ensure that what you care about is actually improving by measuring before and after.
  - Even if that means instrumenting a function with a `Date.now()` recording at the entrance, and another `Date.now()` at the exit points in order to measure processing time changes.
  - Prove to yourself that you’ve actually improved something by measuring before and after.
  - The `performance` API is very useful for taking high-resolution measurements. 
    - This is usually much better than using your own hand-rolled timers to measure how long things take. 
    - You access the API through Window.performance.

- Use the compositor for animations
  - Performing animations on the main thread should be treated as deprecated. Avoid doing it. 
  - Instead, animate using `Element.animate()` . 
  - [Animating like you just don’t care with Element.animate](https://hacks.mozilla.org/2016/08/animating-like-you-just-dont-care-with-element-animate/)
    - `Element.animate()` is the first part of the Web Animations API that we’re shipping 
    - and, while there are plenty of nice features in the API as a whole, such as better synchronization of animations, combining and morphing animations, extending CSS animations, etc., the biggest benefit of Element.animate() is performance.

- Explicitly define start and end animation values
  - Some optimizations in the animation code of Gecko are based on an expectation that the from (0%) and the to (100%) values will be explicitly defined in the @keyframes definition. 
  - Even though these values may be inferred through the use of initial values or the cascade, the offscreen animation optimizations are dependent on the explicit definition.

- Use IndexedDB for storage
  - `AppCache` and `LocalStorage` are synchronous storage APIs that will block the main thread when you use them. Avoid them at all costs!
  - `IndexedDB` is preferable, as the API is asynchronous (all disk operations occur off of the main thread), and can be accessed from web workers.
  - `IndexedDB` is also arguably better than storing and retrieving JSON from a file - particularly if the JSON encoding or decoding is occurring on the main thread. 
    - IndexedDB will do js object serialization and deserialization for you using the structured clone algorithm, 
    - meaning that you can stash(存放) things like maps, sets, dates, blobs, and more, without having to do conversions for JSON compatibility.
  - A Promise-based wrapper for IndexedDB, IndexedDB.jsm, is available for chrome code.

- Test on weak hardware
  - Look at the Firefox Hardware Report to get a sense of what our users are working with. 
  - Test on slower machines

- Consider loading scripts with the subscript loader asynchronously
  - If you've ever used the subscript loader, you might not know that it can load scripts asynchronously, and return a Promise once they're loaded. 

``` JS
Services.scriptloader.loadSubScriptWithOptions(myScriptURL, { async: true }).then(() => {
  console.log("Script at " + myScriptURL + " loaded asynchronously!");
});
```

## Tips for authoring fast-loading HTML pages

- [Tips for authoring fast-loading HTML pages](https://developer.mozilla.org/en-US/docs/Learn/HTML/Howto/Author_fast-loading_HTML_pages)

- Reduce page weight
  - Page weight is by far the most important factor in page-load performance.
  - Reducing page weight through the elimination of unnecessary whitespace and comments, commonly known as minimization, and by moving inline script and CSS into external files, can improve download performance with minimal need for other changes in the page structure.
  - Tools such as HTML Tidy can automatically strip leading whitespace and extra blank lines from valid HTML source. 
  - Other tools can "compress" JavaScript by reformatting the source or by obfuscating the source and replacing long identifiers with shorter versions.
- Minimize the number of files
- Use a Content Delivery Network (CDN)
- Reduce domain lookups
- Cache reused content
- Optimally order the components of the page
  - Download page content first, along with any CSS or JavaScript that may be required for its initial display, so that the user gets the quickest apparent response during the page loading. 
- Reduce the number of inline scripts
  - Inline scripts can be expensive for page loading since the parser must assume that an inline script could modify the page structure while parsing is in progress.
  - reduce the use of `document.write()` to output content in particular
  - Use modern AJAX methods to manipulate page content for modern browsers
    - https://developer.mozilla.org/en-US/docs/Web/Guide/AJAX
- Use modern CSS and valid markup
- Chunk your content
  - Tables for layouts are a legacy method that should not be used anymore. 
  - Layouts utilizing floats, positioning, flexbox, or grids should be used instead.
  - Tables are still considered valid markup but should be used for displaying tabular data. 
  - To help the browser render your page quicker, you should avoid nesting your tables.
- Minify and compress SVG assets
- Minify and compress your images
- Specify sizes for images and tables
  - If the browser can immediately determine the height and/or width of your images and tables, it will be able to display a web page without having to reflow the content. 
  - This not only speeds the display of the page but prevents annoying changes in a page's layout when the page completes loading. 
  - For this reason, height and width should be specified for images, whenever possible.
  - Tables should use the CSS selector: property combination: `table-layout: fixed;`
  - and should specify widths of columns using the `<col>` and the `<colgroup>` elements.
- Use lazy loading for images
- Choose your user-agent requirements wisely
- Use async and defer, if possible
  - Make the JavaScript scripts such that they are compatible with both the async and the defer attributes, and use async whenever possible, especially if you have multiple script tags.
  - With that, the page can stop rendering while JavaScript is still loading. 
  - Otherwise, the browser will not render anything that is after the script tags that do not have these attributes.
