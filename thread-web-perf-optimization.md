---
title: thread-web-perf-optimization
tags: [optimization, thread, web]
created: '2021-02-26T16:41:28.255Z'
modified: '2021-02-26T16:42:06.878Z'
---

# thread-web-perf-optimization

# pieces

- ## 

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
