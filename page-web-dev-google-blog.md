---
title: page-web-dev-google-blog
tags: [blog, dev, google, web]
created: '2021-01-03T11:29:27.628Z'
modified: '2021-01-03T11:44:34.694Z'
---

# page-web-dev-google-blog

# google

## [索引toc：Fast load times - Techniques for improving site performance.](https://web.dev/fast/)

- measure, optimize, and monitor if you're to get fast and stay fast.

## [Preload critical assets to improve loading speed](https://web.dev/preload-critical-assets/)

- When you open a web page, the browser requests the HTML document from a server, parses its contents, and submits separate requests for any referenced resources. 
  - As a developer, you already know about all the resources your page needs and which of them are the most important. 
  - You can use that knowledge to request the critical resources ahead of time and speed up the loading process. 
- This post explains how to achieve that with `<link rel="preload">`.
- Preloading is best suited for resources typically discovered late by the browser.
  - In this example, Pacifico font is defined in the stylesheet with a `@font-face` rule. 
  - The browser loads the font file only after it has finished downloading and parsing the stylesheet.
- By preloading a certain resource, you are telling the browser that you would like to fetch it sooner than the browser would otherwise discover it 
  - because you are certain that it is important for the current page.
  - In this example, Pacifico font is preloaded, so the download happens in parallel with the stylesheet.
- Lazy loading of fonts carries an important hidden implication that may delay text rendering: 
  - the browser must construct the render tree, which is dependent on the DOM and CSSOM trees, before it knows which font resources it needs in order to render the text. 
  - As a result, font requests are delayed well after other critical resources, and the browser may be blocked from rendering text until the resource is fetched.
- Not all browsers support `<link rel="preload">`, and in those browsers, will just be ignored. 
  - But every browser that supports preloading also supports WOFF2, so that's always the format that you should preload.
- `<link rel="preload" href="critical.js" as="script">`
  - The browser caches preloaded resources so they are available immediately when needed. 
  - (It doesn't execute the scripts or apply the stylesheets.)
- After implementing preloading, many sites, including Shopify, Financial Times and Treebo, saw 1-second improvements in user-centric metrics such as Time to Interactive and First Contentful Paint.
- Resource hints, for example `preconnect` and `prefetch`, are executed as the browser sees fit. 
  - The `preload`, on the other hand, is mandatory for the browser. 
  - Modern browsers are already pretty good at prioritizing resources, that's why it's important to use preload sparingly and only preload the most critical resources.
  - Unused preloads trigger a Console warning in Chrome, approximately 3 seconds after the load event.
  - preload is supported in all modern browsers except Firefox.
- **Use cases**
  - Preloading resources defined in CSS
    - Fonts defined with `@font-face` rules or `background` images defined in CSS files aren't discovered until the browser downloads and parses those CSS files. 
    - Preloading these resources ensures they are fetched before the CSS files have downloaded.
  - Preloading non-critical CSS files
    - If you are using the critical CSS approach, you split your CSS into two parts. 
    - The critical CSS required for rendering the above-the-fold content is inlined in the `<head>` of the document and non-critical CSS is usually lazy-loaded with JavaScript. 
    - Waiting for JavaScript to execute before loading non-critical CSS can cause delays in rendering when users scroll, so it's a good idea to use `<link rel="preload">` to initiate the download sooner.
  - Preloading JavaScript files 
    - Because browsers don't execute preloaded files, preloading is useful to separate fetching from execution which can improve metrics such as Time to Interactive. 
    - Preloading works best if you split your JavaScript bundles and only preload critical chunks.
- Conclusion
  - To improve page speed, preload important resources that are discovered late by the browser.
  - Preloading everything would be counterproductive so use preload sparingly and measure the impact in the real-world.

- discussion

- `<link rel="preload">` does not change Chrome's internal "priority" for downloading an asset, it simply instructs Chrome when to start the download.
  - The resource is loaded with the same priority as it would otherwise, but now the browser knows about it ahead of time, allowing for the download to start earlier.
  - A stylesheet or font will still be considered Highest priority, and a video will still be considered low priority. 
  - But Chrome will start downloading an asset immediately when it encounters the `<link rel="preload">` tag.
