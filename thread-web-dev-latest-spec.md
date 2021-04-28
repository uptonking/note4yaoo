---
title: thread-web-dev-latest-spec
tags: [dev, latest, spec, thread, web]
created: '2021-04-27T09:19:14.189Z'
modified: '2021-04-27T09:19:37.711Z'
---

# thread-web-dev-latest-spec

# pieces

- ## 

- ## 

- ## [Say Hello To CSS Container Queries](https://ishadeed.com/article/say-hello-to-css-container-queries/)

- ## HTML sanitizers are critical to web applications, mitigating the risk of XSS when working with untrusted strings. 
- https://twitter.com/mikewest/status/1386932250391023619
  - The HTML Sanitizer API is a work-in-progress (behind a flag in Chrome and Firefox) that shifts responsibility for this task to the browser
  - https://wicg.github.io/sanitizer-api/
- While using Trusted Types + document.createTextNode to inert XSS code, I find Sanitizer API useful against social attacks, like "Hey noob copy paste this inert code stored on my page into your dev tools it's a surprise". allowElements:[] will just nuke payload and it's great.
- Userland sanitizers like DOMPurify have existed for years. Browsers are now trying to pave those cowpaths.
