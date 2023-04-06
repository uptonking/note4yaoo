---
title: thread-web-dev-latest-spec
tags: [dev, latest, spec, thread, web]
created: 2021-04-27T09:19:14.189Z
modified: 2021-04-27T09:19:37.711Z
---

# thread-web-dev-latest-spec

# discuss

- ## 

- ## 

- ## What platforms support something like AsyncLocalStorage/Async Context?
- https://twitter.com/RyanCarniato/status/1643669619318878208
  - I assumed it was off the table numerous times over the past 3 years because it was Node only. But there are many places it'd be beneficial and now that Next is strong-arming it I have to ask the question.

- Node does. Cloudflare added support last week. I imagine Bun does. Does AWS Lambda? Deno Deploy?

- have also avoided it for a different reason - people mentioned performance issues
- Performance is a concern and I've worried about this for things like page load. But one place this is amazing is keeping Request context in `server$`. We use the function arguments in Bling now. But Solid Start did a bunch of hacks to try to not mess with function signature.
  - Another is things like resuming context in Async Components. Async components are sort of an awkward design mind you for a read-based mechanism (like reactivity or really Suspense for that matter). My gut is we compile to async generators for this if desired but it's interesting.
  - This is mostly true for the Node.js implementation. Other runtimes have a different way of implementing it, but this will all be unified with AsyncContext

- We shipped on Vercel! And our TC39 representative Justin Ridgewell was a champion for the AsyncContext spec

- I think it's a mistake for any system to rely on Asnc Context for multiple reasons:
  - It's not part of the standard
  - It shouldn't be part of the standard because it hides context level state in ways that make programs harder to understand and subtle bugs harder to find.
  - I have similar issues with any library that hides sync contexts. Using the global `let currentContext` pattern.

- ## Ever read an article that says “setTimeout(..., 0) fires not in 0 ms but in 4”? 
- https://twitter.com/iamakulov/status/1643629579129503744
  - This is no longer true – at least not in Chrome and Safari, and not since a few months ago.
- 1) The HTML spec tells that `setTimeout()` calls nested 5+ levels deep must be throttled to 4 ms. This prevents poorly written sites from over-consuming CPU.
  - (Note the word “nested” – unnested `setTimeout()` s were never intended to be throttled! But we’ll get to that in a bit.)
- 2) The HTML spec only talks about nested `setTimeout()` s. However, up until 2022, Chrome and Safari were also throttling regular `setTimeout(..., 0)` calls to 1 ms!
- 3) So now, when you’re calling `setTimeout(0)` , what actually happens is:
- if it’s a fresh `setTimeout(0)` call, it will run immediately (in all browsers)
  - https://twitter.com/jaffathecake/status/1643750216569585665
  - Ehhh not quite "immediately", it still queues a task, which can allow other things to happen before it, including rendering
- if it’s a nested `setTimeout(0)` call, it will run in 4 ms after 5 (Firefox), 10 (Safari), or 15 (Chrome) nested calls
- When you call `setTimeout(fn, 0)` , `fn` is put to the end of the “task queue”.
- Before `fn` , the browser must first execute:
  - all microtasks (promises + some exotic things)
  - all tasks already in the queue (events + other timers that fired earlier but weren’t processed)

- What is meaning of nested? SetTimeout inside SetTimeout? Or setTimeout without callback func.
- https://twitter.com/bhautiktweets/status/1643640049395970048
  - nested = when you call `setTimeout()` inside another `setTimeout()` callback
  - doesn’t have to be directly inside in the code, just has to happen synchronously within the same callback.
- maybe “recursive” would’ve been a better term! but the HTML spec uses “nested”
  - Except that’s not what recursive means. To have a recursive functions, the function itself or one of its nested calls must call again the original function, pretty much forming a circular call that needs a stop condition, otherwise creating an infinite loop

```JS
setTimeout(() => {
  setAnotherTimeout()
}, 0)

const setAnotherTimeout = () => {
  setTimeout(() => {}, 0)
}
```

- ## Shipped with Chromium 91 is TablesNG, a under-the-hood rewrite regarding tables.
- https://twitter.com/bramusblog/status/1407078048730603521
- [TablesNG — Improvements to `<table>` rendering in Chromium](https://www.bram.us/2021/06/21/tablesng-improvements-to-table-rendering-in-chromium/)
- The old table implementation — from WebKit before — was very old, and limited further development. 
  - The rewrite that landed emphasizes correctness, fixing 72 bugs in one sweep.
- Subpixel geometry
- `<TD>` supports orthogonal writing modes
  - This allows us to have rotated table headers in tables, without needing to resort to extra spans and CSS rotations
- `visibility: collapse;` for table columns
  - This allows us to hide entire columns by setting `visibility: collapse;` on a column in a `<colgroup>` .
  - 可以通过css隐藏某一列
- Sections/rows can have position: that is not static
  - This one is a huge addition, as it — finally — allows us to set `position: sticky` on table headers!
- In Closing
  - While these changes are very welcome, there unfortunately are some compatibility issues: Safari still uses the “old” tables rendering engine and drags every other browser down with it that way. 
  - Firefox led the way before regarding table rendering, and can quite keep up with Chromium’s TablesNG.

- ## I was wondering if Next.js live is built on top of WebContainers? That looks like it could but not mentioned anywhere
- https://twitter.com/sebastienlorber/status/1407003336235229193
- No, Next Live is a custom ESM devserver that runs via SW (kinda similar to PolymerLabs/playground-elements)
  - https://github.com/PolymerLabs/playground-elements

- ## TIL: that you can use use css import assertion in the latest stable chrome 91 purely by enabling "Experimental Web Platform features".
- https://twitter.com/daKmoR/status/1406195981817888770
- How does it work?
  1. Imports of type css return a CSSStyleSheet
  2. Lit creates a shadow root and adopts the CSSStyleSheet to it (via adoptedStyleSheets)
- Benefits
  ➡️ CSSStyleSheet are shared across all elements
  ➡️ Parsed only once
  ➡️ Adding to a shadow dom brings encapsulation

- ## Why on earth does it take almost a second to close a photo modal? Does it tear down and rebuild all underlying DOM between state changes? 
- https://twitter.com/sebmarkbage/status/1405205123236864007
- Browsers tend to optimize things when they become the only bottleneck. There’s also async layout proposals that can help with this.
  - we’ve also been working with browser vendors to contribute to and test new specs like display locking
- Concurrency in CSS is definitely something to tackle. We do this in React Native and display locking with async preemptive(优先的) layout calculation is great.
- The way we plan on JS concurrency helping with these scenarios is to allow content that previously would've been removed from the tree alive so that the DOM can do this kind of layout work preemptively.
  - Previously keeping things "alive" would be too costly since it can interrupt the foregrounded interaction. Keeping it "dead" in JS terms but alive in DOM would leave it stale and then you pay for it all when you reactive it.
  - The sweet spot is to use concurrency to keep the tree alive but at low priority. That way all the work to restore the tree is already done by the time you need it but because things are "backgrounded" in terms of priority and connections it doesn't negatively affect interactions.
- Concurrent Rendering will improve the UX for the 250ms of JS work. Chrome will still spend 750-1000ms on CSS. On Safari the interaction should feel instantaneous.
  - Not quite. We'll switch off of display: none in Chrome and keep the tree in memory and preemptively compute updates to that tree in the background using concurrent rendering. So when we switch off of it, that work has already been amortized(分期偿还，分期付款).
  - Like we're already using concurrent rendering to keep the tree in the background (feed) alive without interrupting the foreground work. However, the way React currently does that is using `display: none` to ensure consistency. The new feature is to not use display none
  - but to do that, we need to deal with CSS relayout in the background using tricks and/or display locking and deal with some other quirks. That's a new feature.
- The **alternative of not using concurrent features by keeping the tree alive** would let it rerender in the background which would be way worse when it's opened but make closing faster. The other alternative of deleting the whole tree would make restoring it to where you were worse.

- ## With text fragments in URLs, we can link to (and highlight) parts of an HTML page, even if they have no IDs.
- https://twitter.com/rauschma/status/1404053789724844036
  - Example (requires a Chromium-based browser):
  - https://exploringjs.com/#:~:text=Essential%20JavaScript%20and%20TypeScript%20books
  - [Boldly link where no one has linked before: Text Fragments](https://web.dev/text-fragments/)
- The feature indeed only works for non-same page navigation

- ## [CSS Container Queries For Designers](https://ishadeed.com/article/container-queries-for-designers/)
- The Current State Of Responsive Design
  - Nowadays, it’s still okay to work on multiple versions of the same web layout to show how the inner parts will change **based on the viewport width**
  - In CSS, the developer needs to create three variations of this component
  - The variations above depend on media queries or the viewport width. That means, we can’t control them based on their parent width.
- The problem is that the developer is tied with using a variation of a component only when the viewport width is greater than a specific value
- What Are Container Queries?
  - First, let me define the container. 
  - It’s an element that contains another element(s), and is sometimes called a wrapper. 
  - When a component is placed within an item, it’s contained within that item. 
  - That means, we can query the width of its parent and modify it based on that.
- Sometimes, it would be better for the front-end developer to work on a completely new component rather than creating the variation with container queries.
  - If the inner parts will stay the same, or at least won’t include new ones, we can alter the component and have multiple variations 
- Use Cases For CSS Container Queries
  - Chat List
  - Sidebar
  - Accordion
  - Search
  - List
  - UserProfile
  - SocialSharing

- ## [Say Hello To CSS Container Queries](https://ishadeed.com/article/say-hello-to-css-container-queries/)

- ## HTML sanitizers are critical to web applications, mitigating the risk of XSS when working with untrusted strings. 
- https://twitter.com/mikewest/status/1386932250391023619
  - The HTML Sanitizer API is a work-in-progress (behind a flag in Chrome and Firefox) that shifts responsibility for this task to the browser
  - https://wicg.github.io/sanitizer-api/
- While using Trusted Types + document.createTextNode to inert XSS code, I find Sanitizer API useful against social attacks, like "Hey noob copy paste this inert code stored on my page into your dev tools it's a surprise". allowElements:[] will just nuke payload and it's great.
- Userland sanitizers like DOMPurify have existed for years. Browsers are now trying to pave those cowpaths.
