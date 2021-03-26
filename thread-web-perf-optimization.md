---
title: thread-web-perf-optimization
tags: [optimization, thread, web]
created: '2021-02-26T16:41:28.255Z'
modified: '2021-02-26T16:42:06.878Z'
---

# thread-web-perf-optimization

# pieces

- ## 

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
