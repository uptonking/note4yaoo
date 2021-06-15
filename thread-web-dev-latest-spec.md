---
title: thread-web-dev-latest-spec
tags: [dev, latest, spec, thread, web]
created: '2021-04-27T09:19:14.189Z'
modified: '2021-04-27T09:19:37.711Z'
---

# thread-web-dev-latest-spec

# pieces

- ## 

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
