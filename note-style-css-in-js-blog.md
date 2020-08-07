---
title: note-style-css-in-js-blog
tags: [blog, css-in-js]
created: '2020-08-07T17:50:19.599Z'
modified: '2020-08-07T17:50:44.516Z'
---

# note-style-css-in-js-blog

## [Tip: ChromeDevTools now supports CSS-in-JS!](https://twitter.com/addyosmani/status/1289818213983883270)

- This should be a standard for all other browsers. They should help  Frontend Developers' lives and make life easy. 
- Thanks for the tip! Can you recommend us posts about performance comparison of css in js vs CSS modules? Seems like CSS in JS always will be slower because it's overloading the JS main thread.
- There's CSS-in-JS libraries with zero overhead; I've used Linaria. The CSS becomes real .css files as part of the build, and there's no JS overhead (it just compiles to class name strings).
- CSS, JS and html are all needed to define some interactive component on the page. Their common concern is that component. It's separation of concern, not separation of syntax.
- for performance most libraries use Constructable Stylesheets to add those styles. Chrome did not allow to edit those before. it's fixed in chrome canary - so will be available in chrome 85.
- CSS in JS hurts load time. Especially critical CSS. The CSS is not immediately discoverable by the browser and can hurt metrics like Largest Contentful Paint
  - I recommend folks using CSS-in-JS configure their bundlers to extract/output real CSS files for production. You avoid the double-parse costs, get better caching and can still benefit from the DX. like linaria.
  - Good CSS-in-JS libraries can have the CSS extracted out into real .css files as part of the build(linaria, style-sheet). They can use atomic CSS so that growth of the CSS file is relatively small and growth slows down significantly over time
  - Plus, SSR sends only the critical CSS, so the browser has to do less work at first.
- ref
  - [google: Style editing for CSS-in-JS frameworks_chrome85_202006](https://developers.google.com/web/updates/2020/06/devtools)
  - [Firefox 79: Better source map references for SCSS and CSS-in-JS](https://hacks.mozilla.org/2020/07/firefox-79/)

## CSS-in-JS - styled vs css prop

- [CSS-in-JS - styled vs css prop](https://dev.to/a_sandrina_p/css-in-js-styled-vs-css-prop-229e)

- I like to use styled, since css prop depends on a bit more setup using babel or macro to reach the same result.

## style9: build-time CSS-in-JS

- [style9: build-time CSS-in-JS_202007](https://css-tricks.com/style9-build-time-css-in-js/)

- In April of last year, Facebook revealed its big new redesign, a rebuild of a large site with a massive amount of users. 
- To accomplish this, they used several technologies they have created and open-sourced, such as React, GraphQL, Relay, and a new CSS-in-JS library called stylex.
- This new library is internal to Facebook, but they have shared enough information about it to make an open-source implementation, style9, possible.
- style9 has the same benefits as all other CIJ solutions, as articulated by Christopher Chedeau, including scoped selectors, dead code elimination, deterministic resolution, and the ability to share values between CSS and JavaScript.
- There are, however, a couple of things that make style9 unique.
- Minimal runtime
  - Although the styles are defined in JavaScript, they are extracted by the compiler into a regular CSS file. 
  - That means that no styles are shipped in your final JavaScript file. 
  - The only things that remain are the final class names, which the minimal runtime will conditionally apply, just like you would normally do. 
  - This results in smaller code bundles, a reduction in memory usage, and faster rendering.
  - Since the values are extracted at compile time, truly dynamic values can’t be used. 
  - These are thankfully not very common and since they are unique, don’t suffer from being defined inline. 
  - What’s more common is conditionally applying styles, which of course is supported. 
  - So are local constants and mathematical expressions, thanks to babel’s path.evaluate.
- Atomic output
  - Because of how style9 works, every property declaration can be made into its own class with a single property. So, for example, if we use `opacity: 0` in several places in our code, it will only exist in the generated CSS once. 
  - The benefit of this is that the CSS file grows with the number of unique declarations, not with the total amount of declarations.
  - Since most properties are used many times, this can lead to dramatically smaller CSS files.
- Some may complain about this, that the generated class names are not semantic, that they are opaque and are ignoring the cascade. 
- This is true. We are treating CSS as a compilation target. But for good reason. By questioning previously assumed best practices, we can improve both the user and developer experience.
- In addition, style9 has many other great features, including: typed styles using TypeScript, unused style elimination, the ability to use JavaScript variables, and support for media queries, pseudo-selectors and keyframes.
- The syntax for creating styles closely resembles other libraries. 
- We start by calling `style9.create` with objects of styles
- Because all declarations will result in atomic classes, shorthands such as flex: 1 and background: blue won’t work, as they set multiple properties. Properties that can be can be expanded, such as padding, margin, overflow, etc. will be automatically converted to their longhand variants. If you use TypeScript, you will get an error when using unsupported properties.
- Summary
  - With CSS-in-JS, we are imposing a performance cost when embedding styles in our code. 
  - By extracting the values during build-time we can have the best of both worlds. 
  - We benefit from co-locating our styles with our markup and the ability to use existing JavaScript infrastructure, while also being able to generate optimal stylesheets.
