---
title: lib-excel-tanstack-virtual-community
tags: [community, tanstack-virtual]
created: 2024-03-15T03:25:20.567Z
modified: 2024-03-15T03:25:43.756Z
---

# lib-excel-tanstack-virtual-community

# guide

- 是否支持nested virtualized? 类似文档内的表格
# discuss-stars
- ## 

- ## my hate for virtual scrolling continues to grow
- https://x.com/thdxr/status/1892231011745911286
  - it is such a hack and it's very hard to keep things like control+f or selection working

- modern browsers support `content-visibility: auto;` In my experience it can be laggy though, Try scroll fast on https://uses.tech which has 25k elements

- In general, Chrome DevTools has a Performance tab where you can see exactly where time gets spent.  That lets you narrow down if it’s HTML parsing, CSS eval, JS eval, reflow, or repaint.  Lots of rows is likely HTML parsing and reflow (which they call “Layout”)

- `content-visibility` just avoids browser paint; the cost of creating the dom nodes (in latency and memory) doesn't go away unfortunately. still need to virtualize large complicated lists.

- Virtual scrolling is not suitable for the web. It works well in mobile apps, though. Pagination with a URL-persisted state is the way to go on the web.

- Limiting DOM nesting, turning off event handlers (with js or pointer-events none), not using tables (or using fixed layout), removing shadows, blurs and playing with content-visibility might already bring nice effects, it’s just not out of the box. And then there are iframes…

- Limiting DOM nesting, turning off event handlers (with js or pointer-events none), not using tables (or using fixed layout), removing shadows, blurs and playing with content-visibility might already bring nice effects, it’s just not out of the box. And then there are iframes…

- https://x.com/zack_overflow/status/1892293016527757488
  - why the hell does the browser render shit outside of the screen? It is a basic optimization used in games since the 90s

- ## [sentry: Better Code Rendering Through Virtualization _202412](https://sentry.engineering/blog/better-code-rendering-through-virtualization)
  - TL; DR: we rebuilt Codecov’s code renderer from the ground up utilizing virtual lists and some other nifty tricks to significantly decrease render blocking time, and unblock customers with files containing tens of thousands of lines.
  - We had Jake an engineer at Microsoft working on TypeScript tooling, reach out to us, letting us know he was devastated with the code renderer crashing on them while trying to render TypeScript’s checker.ts file. 
  - The problem turns out to be that the current code renderer was not built to handle files that contains this amount of code and coverage data, leading the application to crash. 
  - The objective of our initiative is to rebuild our code renderer from the ground up utilizing new techniques so that we’re able to handle these larger files with ease
- The easiest way to introduce virtualization to your application is through using a third-party library, instead of attempting to write the logic ourselves. 
  - 💡 we landed on `@tanstack/react-virtual` as it meets all the functionality requirements for our project, as well we are already using a couple other TanStack libraries and have had pretty good success with them.
- 
- 
- 

# discuss-not-yet
- ## 

- ## 

- ## [List size is capped by browser/memory _202307](https://github.com/TanStack/virtual/issues/565)
- When trying to create a list with a large count of rows, one of two things happens:
  - A. If the count is over an arbitrary number, capped by each browser individually, the scroll won't go over that row. For instance, for Chrome that number is 479348, and you can't scroll to the remaining items if there are any.
  - B. If the number is too large (for instance 150 mil), the tab will simply crash. I believe this is caused by the getMeasurements function from the virtual-core library, as it tries to create an array of the count size.
- I experienced this issue, and enabling `debug: true` show that all the time is spent is `getMeasurements` . I have timings around 100ms in this method, and the scrolling is laggy 
  - I worked around this problem by providing a smaller `count` to the virtualizer, increasing it as more pages are fetched. Scrolling is fast even with thousands of items loaded.

# discuss
- ## 

- ## 

- ## 

- ## 

- ## 🌰 Animate a @Tan_Stack Virtual list with motion @motiondotdev
- https://x.com/inkdrop_app/status/1895368977267990872
  - [How to animate a TanStack Virtual list with Motion _202502](https://www.devas.life/how-to-animate-a-tanstack-virtual-list-with-motion/)
