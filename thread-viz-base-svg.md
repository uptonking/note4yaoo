---
title: thread-viz-base-svg
tags: [svg, thread, viz]
created: 2021-03-11T11:17:49.598Z
modified: 2021-03-11T11:26:06.670Z
---

# thread-viz-base-svg

# guide

# discuss-stars
- ## 

- ## threadsvg: Instantly convert any SVG logo to 3D
- https://x.com/MalayVasa/status/1809627318308032827
  - https://www.threedsvg.com/
- it would be sick if we could download the three.js render you have on the right as a webpage with a few different environments

# discuss
- ## 

- ## 

- ## TIL `document.createElementNS()` for SVGs while debugging Wordpress...if you call `document.createElement("svg")` you get an HTMLUnknownElement
- https://x.com/RogersKonnor/status/1800228594561818666

- ## SVG is used on >65% of websites. Yet, browsers have been *refusing* to work on SVG, ignoring pressure and pain points from web devs.
- https://x.com/LeaVerou/status/1791860519315419358
  - Tons of work (SVG 2, fill & stroke, and more) has sat unimplemented for years. At this point, in standards circles, we know not to touch SVG with a barge pole.
  - Case that prompted this post, Custom SVG elements. 7y of pressure, a cornucopia of use cases, yet “no implementer interest”

- ## use CSS transforms on part of an SVG icon 
- https://twitter.com/jh3yy/status/1716920662525116741
  - https://codepen.io/jh3y/pen/poGJowE

- ## 💡 My latest blog post goes in-depth on why & how to remove SVGs from your JS bundle
- [Breaking Up with SVG-in-JS in 2023 | Jacob Groß | kurtextrem.de](https://kurtextrem.de/posts/svg-in-js)

- I use Iconify library which you could fetch the icon and embed the svg on the runtime and keep the bundle free + have all the advantages to animate or color you icon

- ## Know of any SVG to pdf libraries that support shadows?
- https://twitter.com/steveruizok/status/1512533051154305027
- PrinceXML/DocRaptor
- A hunch: if you use puppeteer to generate the PDF it might preserve shadows. Though may not be the most optimal conversion

- ## A modern SVG rendering engine is ready.: resvg-js 2.0 Alpha with WASM support. 
- https://twitter.com/yisibl/status/1493597768904212482
  - now you can even convert SVG to PNG in Web Worker. for Node.js, 
  - with resvg-js you can get rid of the heavy Puppeteer or node-canvas

- ## TIL that the transform origin property of an SVG element is relative to the SVG image, rather than the center of the transforming element like it is in CSS.
- https://twitter.com/steveruizok/status/1440730385248260104
- Did you use `transform-box: fill-box;` on the SVG element to transform on its origin instead of the SVG image?
  - Today I learned that too! I used `rotate(degrees, centerX, centerY)`

- ## I was that close to a cool screenshot approach based on an SVG image with `foreignObject` HTML rendered to a canvas that would then be `toBlob()` 'ed, but the canvas is always tainted(腐坏的，受污染的)
- https://twitter.com/tomayac/status/1418266133568888834
  - Blobs taint the canvas immediately, and data URLs (see last comment on the bug) somehow don’t work and seem to simply strip out all HTML in foreignObject. HTML2Canvas exists (and is 42kb gzipped) for a reason.
- I thought this is how DOM-to-canvas techniques currently worked.
- Why can’t we render, say, an iframe to a canvas anyway
  - Because an iframe (or any element) can contain all kinds of things you shouldn't have pixel access to
  - Same origin iframes can contain cross origin (or otherwise private) data

- ## Sometimes I wish there's a language which combines CSS and SVG
- https://twitter.com/yuanchuan23/status/1379586675517444096
- JavaScript
- If you are feeling masochistic, build XSLT to transform your SVG.
- Surprise! That language exists, and it is SVG and CSS.
  - They are entwined, in that you can use CSS in SVG. And to a limited extent, you can use SVG (images, path strings, clip paths, masks, filters) in CSS.
  - But that only makes it more frustrating when you bump into the areas where they don't play nice together.

- ## Too Many SVGs Clogging Up Your Markup? Try `use` .
- https://css-tricks.com/too-many-svgs-clogging-up-your-markup-try-use/
- Recently, I had to make a web page displaying a bunch of SVG graphs for an analytics dashboard. I used a bunch of `<rect>, <line>, <text>` elements on each graph to visualize certain metrics.
- This works and renders just fine, but results in a bloated DOM tree, where each shape is represented as separate nodes. 
  - Displaying all 50 graphs simultaneously on a web page results in 5, 951 DOM elements in total, which is far too many.
- This is not optimal for several reasons:
  - A large DOM increases memory usage, longer style calculations, and costly layout reflows.
  - It will increases the size of the file on the client side.
  - Lighthouse penalizes the performance and SEO scores.
  - Maintainability is a nightmare — even if we use a templating system — because there’s still a lot of cruft and repetition.
  - It doesn’t scale. Adding more graphs only exacerbates these issues.
- The solution? The SVG element.
  - The `<use>` element takes nodes from within the SVG document, and duplicates them somewhere else. 

    - The effect is the same as if the nodes were deeply cloned into a non-exposed DOM, then pasted where the `use` element is.
