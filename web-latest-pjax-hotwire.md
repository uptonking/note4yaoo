---
title: web-latest-pjax-hotwire
tags: [frontend, hotwire, latest, pjax, web]
created: '2020-12-23T15:36:47.371Z'
modified: '2021-01-04T16:06:29.569Z'
---

# web-latest-pjax-hotwire

# pjax

- https://github.com/MoOx/pjax
  - /1.1kStar/MIT/201910/js
- Pjax loads pages using AJAX and updates the browser's current URL using `pushState()` without reloading your page's layout or any resources (JS, CSS), giving a fast page load.
  - Under the hood, it's just ONE HTTP request with a pushState() call.
- How Pjax Works
  - It listens to every click on links you want (by default all of them).
  - When an internal link is clicked, Pjax fetches the page's HTML via AJAX.
  - Pjax renders the page's DOM tree (without loading any resources - images, CSS, JS, etc).
  - It checks if all defined parts can be replaced
  - Then it updates the browser's current URL using pushState().

- pjax works by
  - fetching HTML from your server via ajax 
  - and replacing the content of a container element on your page with the loaded HTML. 
  - It then updates the current URL in the browser using `pushState`. 
- This results in faster page navigation for two reasons:
  - No page resources (JS, CSS) get re-executed or re-applied; 
  - If the server is configured for pjax, it can render only partial page contents and thus avoid the potentially costly full layout render.
- No more full page reloads. No more multiple HTTP requests.

# Hotwire

- https://github.com/hotwired/hotwire-rails
  - /141Star/MIT/202012/ruby
- **Hotwire** is an alternative approach to building modern web applications 
  - without using much JavaScript by sending HTML instead of JSON over the wire. 
- This makes for fast first-load pages, 
  - keeps template rendering on the server, 
  - and allows for a simpler, more productive development experience in any programming language, 
  - without sacrificing any of the speed or responsiveness associated with a traditional single-page application.
- The heart of Hotwire is **Turbo**. 
  - A set of complimentary techniques for speeding up page changes and form submissions, dividing complex pages into components, and stream partial page updates over WebSocket. 
  - All without writing any JavaScript at all. 
  - And designed from the start to integrate perfectly with native hybrid applications for iOS and Android.
- While Turbo usually takes care of at least 80% of the interactivity that traditionally would have required JavaScript, there are still cases where a dash of custom code is required. 
- **Stimulus** makes this easy with a HTML-centric approach to state and wiring.

- https://github.com/hotwired/turbo
- The speed of a single-page web application without having to write any JavaScript.
- Turbo Drive accelerates links and form submissions 
- Turbo Frames decompose pages into independent contexts
- Turbo Streams deliver page changes over WebSockets
- Turbo Native lets your majestic monolith form the center of your native iOS and Android apps
- It's all done by sending HTML over the wire

- https://github.com/hotwired/stimulus-rails
- Stimulus doesn’t seek to take over your entire front-end in fact, 
- it’s not concerned with rendering HTML at all. 
- Instead, it’s designed to augment your HTML with just enough behavior to make it shine. - Stimulus pairs beautifully with Turbo to provide a complete solution for fast applications with a minimal amount of effort.

# BigPipe

- https://github.com/bigpipe/bigpipe
  - /1.2kStar/MIT/201510/js
  - BigPipe is a radical(激进的；全新的；彻底完全的) new web framework for NodeJS 
  - The general idea is to decompose web pages into small re-usable chunks of functionality called Pagelets and pipeline them through several execution stages inside web servers and browsers. 
  - This allows progressive rendering at the front-end and results in exceptional front-end performance.

- bigPipe是由facebook提出来的一种动态网页加载技术。
  - 它将网页分解成称为pagelets的小块，然后分块传输到浏览器端，进行渲染。
  - 它可以有效地提升首屏渲染时间。
