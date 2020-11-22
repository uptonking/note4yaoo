---
title: note-web-ssr
tags: [server-side-rendering, web]
created: '2020-11-22T13:29:51.265Z'
modified: '2020-11-22T13:33:09.114Z'
---

# note-web-ssr

## ssr-solutions

- https://github.com/stereobooster/react-snap
  - /4kStar/MIT/201910/js
  - Pre-renders a web app into static HTML. 
  - Uses Headless Chrome to crawl all available links starting from the root. - Heavily inspired by prep and react-snapshot, but written from scratch. 
  - Zero configuration is the main feature. 
  - Works out-of-the-box with create-react-app - no code-changes required.
  - Does not depend on React. The name is inspired by react-snapshot but works with any technology (e.g., Vue).
  - [Behind the scenes](https://github.com/stereobooster/react-snap/blob/master/doc/behind-the-scenes.md)
    - react-snap works concurrently, by default it uses 4 tabs in the browser. 
