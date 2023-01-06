---
title: page-web-engineering-optimization
tags: [engineering, optimization, web]
created: 2020-12-16T09:30:04.797Z
modified: 2020-12-16T09:47:27.072Z
---

# page-web-engineering-optimization

# [Apply instant loading with the PRPL pattern_201811](https://web.dev/apply-instant-loading-with-prpl/)

- PRPL is an acronym(首字母缩略词) that describes a pattern used to make web pages load and become interactive, faster:
  - Push (or preload) the most important resources.
  - Render the initial route as soon as possible.
  - Pre-cache remaining assets.
  - Lazy load other routes and non-critical assets.

- Audit your page with Lighthouse
  - Click the Lighthouse tab in the devtools
  - Select the Performance and Progressive Web App checkboxes.
  - Click Run Audits to generate a report.

- Preload critical resources
  - Lighthouse shows the failed audit if a certain resource is parsed and fetched late
  - Preload is a declarative fetch request that tells the browser to request a resource as soon as possible. 
  - `<link rel="preload" as="style" href="css/style.css">`
  - The browser sets a more appropriate priority level for the resource in order to try to download it sooner while not delaying the `window.onload` event.

- Render the initial route as soon as possible 
  - Lighthouse provides a warning if there are resources that delay First Paint, the moment when your site renders pixels to the screen
  - To improve First Paint, Lighthouse recommends inlining critical JavaScript and deferring the rest using async, as well as inlining critical CSS used above-the-fold.
    - This improves performance by eliminating round-trips to the server to fetch render-blocking assets. 
    - However, inline code is harder to maintain from a development perspective and cannot be cached separately by the browser.
  - Another approach to improve First Paint is to server-side render the initial HTML of your page. 
    - This displays content immediately to the user while scripts are still being fetched, parsed, and executed.
    - However, this can increase the payload of the HTML file significantly, which can harm Time to Interactive, or the time it takes for your application to become interactive and can respond to user input.
  - There is no single correct solution to reduce the First Paint in your application, 
    - and you should only consider inlining styles and server-side rendering if the benefits outweigh the tradeoffs

- Pre-cache assets
  - By acting as a proxy, service workers can fetch assets directly from the cache rather than the server on repeat visits. 
  - This not only allows users to use your application when they are offline, but also results in faster page load times on repeat visits.
  - Use a third-party library to simplify the process of generating a service worker unless you have more complex caching requirements than what a library can provide. 

- Lazy load other routes and non-critical assets.
  - Lighthouse displays a failed audit if you send too much data over the network
  - This includes all asset types, but large JavaScript payloads are especially costly due to the time it takes the browser to parse and compile them. 
  - To send a smaller JavaScript payload that contains only the code needed when a user initially loads your application, 
    - split the entire bundle and lazy load chunks on demand.
  - If you load many images on your web page, defer all that are below the fold, or outside the device viewport, when a page is loaded
