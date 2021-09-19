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
