---
title: thread-web-perf-optimization
tags: [optimization, thread, web]
created: '2021-02-26T16:41:28.255Z'
modified: '2021-02-26T16:42:06.878Z'
---

# thread-web-perf-optimization

# pieces

- ## 

- ## 

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
