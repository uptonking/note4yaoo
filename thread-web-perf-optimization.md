---
title: thread-web-perf-optimization
tags: [optimization, thread, web]
created: 2021-02-26T16:41:28.255Z
modified: 2021-02-26T16:42:06.878Z
---

# thread-web-perf-optimization

# guide

# discuss-css-pref
- ## 

- ## 

- ## 

- ## In this little benchmark rendering 16k squares using the DOM goes at 10fps, and rendering 1M squares using raw WebGL goes at 120fps.
- https://twitter.com/fabiospampinato/status/1749500897300730165
- Are the squares absolutely positioned? Are you virtualizing only the squares in the viewport?
  - It's this demo here: https://benchmarks.slaylines.io/dom.html
  - The squares seem absolutely positioned and moved by changing the CSS transform matrix.
- Wondering if the transform is creating compositor layers
  - It doesn't look like it.
  - Layerize is the process of deciding what needs to be on what layer.
- Profile it and see where most of the work happens
  - Mostly style recalculations. Only the transform style on each element changed. I don't know this stuff seems hyper slow to me. Does this computer really need 35ms to understand that 8k elements have been moved? Probably not.
- The problem is most likely compositing because your rectangles are overlaying each other.

- its spending all its time in recalculate style which suggests you're cpu bound and not using the gpu for rendering.  A css `transform: translate` should be competitive with webgl
  - This benchmark uses `transform: translate` already: https://benchmarks.slaylines.io/dom.html
  - Somehow updating the x coordinate for each of those N squares causes the browser to spend a huge amount of time recalculating styles 

- You don’t even need to go to WebGL plain 2D context HTML canvas is sufficient for drawing responsive animated graphics. This is why you don’t render force-directed networks in SVG if they’re of any real size.

- Yes with enormous effort a faster DOM that handles this scenario is probably possible. But no one is motivated to work on that because they already invented a way to push 1 million rectangles in a web browser. There is no real use case for this and it requires ‘enormous’ effort
  - This is why we have WebGL for these edge cases.

- I need to fork this and test out raw SVG vs DOM. Even with svg.js it is faster than DOM which implies there might still be some optimization to be made in DOM.
  - https://github.com/robbiespeed/canvas-engines-comparison
  - The fork was a bit quick so there's probably a better way to do the css animation version that might actually improve perf.

- For this use case, absolutely. And probably in general. But this is not a realistic performance test. I worked on the WebGL renderer at Figma and we frequently found optimizations that would speed up e.g. 10k rectangles, but would not help real user files.
  - Yeah try blend ordered rects each with drop shadows and blurs.   The general cases are much harder to optimize even in WebGL.  And especially without framebuffer fetch exposed or a way to avoid ping pong rendering.

- The question is if you can re-implement all what the DOM does that is needed to regular site requirements in 120fps (keyboard support, layouts, a11y)

- Dom elements are not vertices. They weren't designed for that work they will never be that fast. You never see more than 1k els on screen at once "practically" It's the CSSOM, not the DOM that's the problem. They can't compete with triangle if they have no coordinate system.

- I've seen this "benchmark" and I think it is relatively useless in representing "real world" scenarios. Also DOM is largely limited by the fact that each square supports the full CSS spec, and could contain an entire website.
# discuss
- ## 

- ## ActivationTime tells you how much lead time the browser has to prerender a page. (higher=better)
- https://twitter.com/TimVereecke/status/1779079932506763405
  - Here you can see improvements to ActivationTime after I switched from eagerness conservative to moderate

- ## It hasn't been necessary to remove event listeners to prevent memory leaks for about 10 years, unless you are somehow holding on a reference to the DOM element the listener is registered on
- https://twitter.com/Shenqingchuan/status/1749722057540358169
  - 他的意思应该是不需要主动去removeEventListener，因为随着元素被销毁，eventHandler也会自动被garbage collector回收，但除了一种情况，那就是eventHandler里引用了这个元素，这样就导致循环依赖，eventHandler没法自动回收了，这种情况下就需要主动removeEventListener，打破循环依赖。
- 一般对 document、window 这样的肯定是需要的，毕竟 addEventlistener 一般都写在组件 created 这样的生命周期里，如果不 remove，确实可能在这些全局对象上保持多个 listener
- 要手动销毁，前公司调差内存泄漏时这个是主要原因之一

- ## browser javascript profiling is no longer confined to chrome devtools on your local machine
- https://twitter.com/bentlegen/status/1719891903317934374
  - you can now now analyze flame graphs and other profiling insights post-hoc in @getsentry

- ## My Top 3 of missing Performance features: 
- https://twitter.com/TimVereecke/status/1719665087865147695
  - DPR capping
  - Vary based on a specific cookie 
  - CSS property to render elements only when closed 

- ## ~3000 of the "elements" that needed a style recalculation according to @ChromeDevTools were due to this rule:
- https://twitter.com/fabiospampinato/status/1718764978499444895
  - If this isn't a bug I don't know what to call it. There isn't even a selection on this page.
  - Turns out another ~2000 "elements" of those were caused by another rule like that. Basically a very sizable chunk of the style recalculation was wasted styling selections that don't exist. You can't even have more than one selection at a time, I think.

```CSS
::selection {
  background-color: blue;
  color: white;
}
```

- ## 想要提高网页的加载体验，其实有个非常简单且实用的技巧，那就是改变请求资源的加载优先级
- https://twitter.com/zhangxinxu/status/1718665721646075925
- [聊聊Web网页中资源加载的优先级 « 张鑫旭-鑫空间-鑫生活](https://www.zhangxinxu.com/wordpress/2023/10/img-js-preload-fetch-priority/)

- ## How I typically test performance
- https://twitter.com/iamakulov/status/1661475656050556930
- When I’m optimizing Core Web Vitals, I typically focus on LCP and CLS. LCP is roughly “how quickly the page renders”, CLS is “how much the page jumps during loading”.
- When I’m profiling LCP, I like to work through http://WebPageTest.org (WPT).

- ## How to optimize style recalculations
- https://twitter.com/fabiospampinato/status/1652326018613379074
1.      Open chrome://tracing
2.      Record
3.      Manual settings -> turn on "blink.debug"
4.      Record
5.      Interact with the page
6.      Select everything
7.      Click "Slices"
8.      Click "SelectorStats"
9.      Spot overly-broad selectors
10. Make them more specific

- A bit easier in MS Edge, just turn on ‘advanced rendering instrumentation’ in the performance tab, and then the ‘selector stats’ tab will appear when you inspect a style recalc
  - Yeah way easier. For Electron apps raw tracing is the only option unfortunately.

- ## We all know what `defer` attribute on `<script>` tag means. 
- https://twitter.com/jebbacca/status/1636057114484305923
  - "the script is downloaded in parallel to parsing the page, and executed after the page has finished parsing". 
  - So we naively place this attribute on non-critical scripts. 
  - And this might be a problem 
- When the page has been parsed, ALL fully downloaded **deferred scripts are executed in a batch**, i.e. as a single task.  
  - While each one of these scripts alone may execute very fast, when executed in a batch, they can take up significant amount of time when executed as a single batch task. And this task blocks the main thread, thus delaying interactivity and hurting user experience.
  - One way to solve this is by using dynamic imports for loading non-critical scripts. This way they won't block the parsing and also won't be batched.  
  - However, this is not always possible, for example if the scripts are a UMD bundles or just separate deployables. 
  - 💡 In this case what you can do is put this script with `async` attribute at the end of `<body>` tag. **Since it's not deferred it won't be batched**. Since it's `async` and is placed at the end of body it won't block the parsing while downloaded or executed.  
  - The only downside of this approach is that it will be downloaded pretty late, but hey, we're talking about non-critical scripts, so who cares, right?

- Does `type=module` have the same problem?
  - type=module is deferred by default, so yes, it has the same problem.

- ## debugging a performance issue where running div​.style.transform = 'translateX(100px)'
- https://twitter.com/iamakulov/status/1635288731124137988
  - was triggering a style recalculation for 15K nodes
- 1) Whenever you change DOM in the document, browsers have to recalculate styles for affected DOM nodes.
  - In Chrome DevTools, it’s shown as these violet “Recalculate Style” rectangles ↑. 
  - In the Chromium codebase, this is called “UpdateLayoutTree”.
- 2) Browsers are smart about what they need to recalculate.
- 3) if you do div.​style.transform = '...' only that div will be recalc’d. 
  - That’s because you’re changing styles for one DOM node – and there’s 0 chance that will affect any other nodes.
- 4) Even though the codepen has 27K nodes, only one is recalculated. 
- 5) The document I was debugging included HTML generated in a third-party WYSIWYG text editor. 
  - If you worked with those, you know they produce a DOM soup that’s hard to modify or extend.
  - To work around an issue in the editor, a developer added the following CSS:
  - [stye*='aspect-ratio'] > :first-child { width: 100%}
  - Now, when you run div.​style.transform = '...' that not only changes styles, but also modifies the `style` attribute on the node!
  - The browser is put in the position when – due to the `[style*="aspect-ratio"]` selector – changing a one node’s style could affect other nodes.
- 6) And that’s how you get a 15K-node recalc from changing a single inline CSS `transform` rule.
- my intuition is to frame the third party editor soup into its own iframe

- ## Putting the finishing touches on my new Tree component. There are half a million fairly complex items in this demo
- https://twitter.com/fabiospampinato/status/1564010912822034434
- I like this tiny virtualized list implementation
  - https://github.com/developit/preact-virtual-list
- Is this position:absolute based virtualization?
  - Yeah he said that in a previous post

- Bare-bones and hacky implementation, but this is near-optimal virtualized list rendering on the web, while scrolling no nodes are created, destroyed or attached/detached/moved in the DOM, and no VDOMs are diffed. There's barely anything happening, just pure performance 
  - https://twitter.com/fabiospampinato/status/1562481426833977345
  - I optimized some internal details, now it does sub-millisecond scripting while scrolling, for a list containing half a million items. 
- 👉🏻 Are you doing something funky like position absolute changing on those 6 elements, so you don't need to key it?
  - Yeah exactly, here's a version with the "top" property animated, you can see items changing position. It's that plus rendering the same number of items all the time, plus reusing nodes if possible, plus keeping the order of nodes fixed, plus using Solid-like signals.
- I was always sad about having to remove recycling from Preact. It was clever and a huge performance win.
  - Why did this have to be removed?
  - It does unexpected things with any stateful DOM elements, like form inputs or `<video>, <img>`, etc. Everything doing recycling runs into it eventually, just takes a while. Not a showstopper for some use-cases, but often makes for a confusing default.
- This is non-keyed isn't it. That's always the tradeoff with going hyper-optimized. Data swap on fixed nodes using reactive bindings. What's the hacky part?
  - Yeah it's 99% just a non-keyed `<For>` that keeps the same nodes around and updates the signals. The user code, at least for this very simple use case, looks identical to what one may write for a regular `<For>` though, so the performance is kinda hassle-free.
  - The hacky (mainly just ugly really) parts are: 
  - 1) I didn't think about the fact that `<For>` could return nodes in a different order, and that would trigger the diff function, which would mess up with the near-optimality, so I patched `<ForValue>` in Voby to sort results for now.
  - 2) I didn't realize that depending on the exact scrolling state the number of items visible could vary, like maybe you can fit exactly 10 25px items in a 250px container, but if two of them are partially visible then you can see 11 items. But I need the number to be constant.

- ## how browsers parse HTML – do most browsers start parsing parts of the html _as_ they are still downloading or they have to wait until the whole HTML document is completely downloaded?
- https://twitter.com/he_zhenghao/status/1534379242657660930
  - also is parsing-while-downloading html the same as streaming html? 
- HTML parsers are piped with the network stream on document downloads, but obviously not when using something like .innerHTML.
  - HTML streaming is about streaming HTML from the server as it is SSRed, instead of waiting for it to be fully SSRed before sending it. AFAIK.

- ##  `<img>` and background-image download images differently.
- https://twitter.com/iamakulov/status/1504804839921909761
  - `<img>` tag fetches an image as soon as HTML arrives.
  - background-image fetches it much later, only when all CSS files download (even if you specify `style="background-image: …"` straight in HTML).
  - To download a background-image, the browser has to figure out *which* image to download, first.

- ## Optimum `<head>` order for performance
- https://twitter.com/smashingmag/status/1440697011985018881
- Putting the 'SEO' `meta` tags at the end of the `<head>` might be optimal for performance, it's actually very dangerous for SEO. The inclusion of scripts above those meta tags in the `<head>` increases the likelihood of search engines ignoring or improperly parsing the `meta` tags.
  - Google does indeed render in headless browsers, but not for all pages and definitely not faultlessly.
- Not all `<meta>` s should be at the top.
  - to avoid reparsing
  - since this is rendered separately, in the browser UI itself
  - since this affects layout
  - [HTML5 Boilerplate](https://github.com/h5bp/html5-boilerplate/blob/main/dist/doc/html.md)

```html
<meta charset="utf-8"><!-- 1 -->
<title>…</title><!-- 2 -->
<meta name="viewport" content="width=device-width"><!-- 3 -->
<link rel="stylesheet" href="css">
<-- everything else -->
```

- Preload of fonts should generally go before CSS if you’re reasonably confident the fonts will be used on the page. Improves waterfall, CLS, FOUT, etc. And yeah, I don’t think sync JS before sync CSS makes sense

- ## Avoid performance degradations during marketing campaigns by excluding these query strings from your (CDN) Cache Key: utm_*; fbclid; gclib
- https://twitter.com/TimVereecke/status/1439851763851579393
- Under actual traffic conditions
🎯 Better offload
🎯 Better TTFB performance 
- Or go the whole hog and select "Ignore all parameters". If your site doesn't rely on query params for driving content you'll get a very nice perf lift.

- ## How Chrome handles: `<script> in <head>` vs. `<script async>` vs. `<script defer>` vs. `<script> in <body>` ; 
- https://twitter.com/iamakulov/status/1439182424798232577
- [JavaScript Loading Priorities in Chrome](https://addyosmani.com/blog/script-priorities/)
  - Note: Loading priorities are not guaranteed to be consistent cross-browser so use this knowledge wisely and measure when unsure. 
  - Ideally, aim to delivery a great experience to the widest number of users possible.
  - If you're a web developer wondering where you can see the "Loading Priority", Chrome DevTools has an optional "Priority" column available in the Network panel. 

- ## Still using JPEG and PNG for images? 
- https://twitter.com/Steve8708/status/1400953776031285257
  - Consider using `<picture>` tags and WEBP for +30% faster loading images

- ## Spent some dev cycles over the last week working on some JS bundle improvements for @components_ai .
- https://twitter.com/4lpine/status/1382805903603163136
- Offloaded a lot of client heavy JS to API endpoints.
  - Main app serves 60% less JS
  - 80%+ reduction in large components
  - 50% improvement in build times
- The most fruitful optimizations boiled down to a few things:
  - Preprocessing large sets of data so we only send what's needed
  - Replacing large, inlined SVGs with CDN links (with caching)
  - Moving functionality requiring Babel/PostCSS/Prettier/etc. to API endpoints
- The #NextJS bundle analyzer plugin was super useful because it helped pinpoint problematic pages and modules.
  - From there it was preprocessing data and moving code around with a more clear separation between "front end" and "back end".

- ## Beyond junior, you need to understand performance of nested loops. You need to understand when to pick object vs array and what that means as your data grows. 
- https://twitter.com/dan_abramov/status/1375495411746635781
  - You need to understand how to write functions so that computation can be cached.
  - That’s not what y’all are testing.

- ## I spent some time today working on the page-load experience of my course platform. 
- https://twitter.com/JoshWComeau/status/1375237480652345347
- Some of the changes:
  - SSR the code snippets instead of lazy-loading them and doing it all on the client
  - Get SSR styles working in MDX
  - Give things concrete heights to prevent CLS between spinner/loaded content
  - [Next + next-mdx-remote + styled-components](https://twitter.com/JoshWComeau/status/1375133558734532619)
- I love how you put so much effort into all the details! Definitely learning a lot from your approach to our craft.

- ##  how to get a Core Web Vitals report in Google Data Studio. (It’s actually quick! Just clone a template and change the url.)
- https://twitter.com/iamakulov/status/1372562229413941254

- ## The built-in Link component in @GatsbyJS prefetches the page you're about to click on so it can load even faster. 
- https://twitter.com/gill_kyle/status/1370478472699682819
  - This is the kind of runtime optimization I didn't even realize was happening

- ## When it comes to performance, it's so easy to focus exclusively on speed. The numbers matter, but they're not the only lever we can pull!
- https://twitter.com/JoshWComeau/status/1365333133252558850
  - A few years ago in an OSS project, we had a process that took 20+ seconds. 
  - We improved the _perceived_ performance by adding a mini-game!
  - I feel like this area is so under-explored on the web. 
  - We could learn a lot from video games, where loading screens are a fact of life, and developers have found clever ways to keep users engaged during that time.
  - if you're curious about that mini-game loader thing, you can view the code here
  - https://github.com/joshwcomeau/guppy/tree/master/src/components/WhimsicalInstaller
- Multi-stage loaders in general are great. 
  - Think about how much better a 3-step progress indicator feels vs. an opaque endless spinner.
- It's tricky since it's harder to measure perception. It's hard to make an OKR about something so qualitative! 
  - But we can measure the downstream effects. 
  - Instead of measuring load times, we can measure bounce rate, sales numbers, etc.
