---
title: thread-web-css-stars
tags: [css, thread, web]
created: '2021-07-25T12:48:41.836Z'
modified: '2021-07-25T12:49:10.410Z'
---

# thread-web-css-stars

# pieces

- ## 

- ## 

- ## 

- ## 

- ## 

- ## Inlining critical CSS can improve how quickly a page renders. 
- https://twitter.com/addyosmani/status/1419190681864658946
  - Now an opt-in feature in Next.js and the default in Angular
  - [Resource inlining in JavaScript frameworks](https://web.dev/aurora-resource-inlining/)
- I wrote https://github.com/addyosmani/critical for use-cases like static sites + gulp. 
  - For apps + webpack, https://github.com/GoogleChromeLabs/critters may be a better fit.
- Yes, sure, the problem is whether to inline CSS or not, and has nothing to do with the megabytes of JS and nothing being done server-side anymore because it’s too boring.
- using inline style will force us to protect from unsafe inline (CSP guidelines) which is an inconvenience
