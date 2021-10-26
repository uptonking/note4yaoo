---
title: page-web-what-forces-layout-reflow
tags: [copied, css, layout, web]
created: '2020-07-18T07:38:50.923Z'
modified: '2020-12-20T15:56:25.573Z'
---

# page-web-what-forces-layout-reflow

> copied from [What forces layout/reflow gist](https://gist.github.com/paulirish/5d52fb081b3570c81e3a)  

All of the below properties or methods, when requested/called in JavaScript, will trigger the browser to *synchronously calculate the style and layout*.   
This is also called reflow or [layout thrashing](http://www.kellegous.com/j/2013/01/26/layout-performance/), and is common performance bottleneck.

Generally, all APIs that synchronously provide layout metrics will trigger forced reflow / layout. Read on for additional cases and details.

### Element APIs

##### Getting box metrics

* `elem.offsetLeft` , `elem.offsetTop` , `elem.offsetWidth` , `elem.offsetHeight` , `elem.offsetParent`
* `elem.clientLeft` , `elem.clientTop` , `elem.clientWidth` , `elem.clientHeight`
* `elem.getClientRects()` , `elem.getBoundingClientRect()`

##### Scroll stuff

* `elem.scrollBy()` , `elem.scrollTo()`
* `elem.scrollIntoView()` , `elem.scrollIntoViewIfNeeded()`
* `elem.scrollWidth` , `elem.scrollHeight`
* `elem.scrollLeft` , `elem.scrollTop` also, setting them

##### Setting focus

* `elem.focus()` ([source](https://source.chromium.org/chromium/chromium/src/+/master:third_party/blink/renderer/core/dom/element.cc;l=4206-4225;drc=d685ea3c9ffcb18c781bc3a0bdbb92eb88842b1b))

##### Also…

* `elem.computedRole` , `elem.computedName`
* `elem.innerText` ([source](https://source.chromium.org/chromium/chromium/src/+/master:third_party/blink/renderer/core/editing/element_inner_text.cc;l=462-468;drc=d685ea3c9ffcb18c781bc3a0bdbb92eb88842b1b))

### Getting window dimensions

* `window.scrollX` , `window.scrollY`
* `window.innerHeight` , `window.innerWidth`
* window.visualViewport.height / width / offsetTop / offsetLeft ([source](https://source.chromium.org/chromium/chromium/src/+/master:third_party/blink/renderer/core/frame/visual_viewport.cc;l=435-461;drc=a3c165458e524bdc55db15d2a5714bb9a0c69c70?originalUrl=https:%2F%2Fcs.chromium.org%2F))

### document 

* `document.scrollingElement` only forces style
* `document.elementFromPoint`

### Forms: Setting selection + focus

* `inputElem.focus()`
* `inputElem.select()` , `textareaElem.select()`

### Mouse events: Reading offset data

* `mouseEvt.layerX` , `mouseEvt.layerY` , `mouseEvt.offsetX` , `mouseEvt.offsetY` ([source](https://source.chromium.org/chromium/chromium/src/+/master:third_party/blink/renderer/core/events/mouse_event.cc;l=476-487;drc=52fd700fb07a43b740d24595d42d8a6a57a43f81))

### Calling getComputedStyle()

`window.getComputedStyle()` will typically force style recalc.

`window.getComputedStyle()` will often force layout, as well.

<details>
<summary>Details of the conditions where gCS() forces layout</summary>

`window.getComputedStyle()` will force layout in one of 3 conditions:

1. The element is in a shadow tree
1. There are media queries (viewport-related ones). Specifically, one of the following: ([source](https://source.chromium.org/chromium/chromium/src/+/master:third_party/blink/renderer/core/css/media_query_exp.cc;l=240-256;drc=4c8db70889f2d2fae8338b16f553c646dd20bf78)

   * `min-width` , `min-height` , `max-width` , `max-height` , `width` , `height`
   * `aspect-ratio` , `min-aspect-ratio` , `max-aspect-ratio`
   * `device-pixel-ratio` , `resolution` , `orientation` , `min-device-pixel-ratio` , `max-device-pixel-ratio`
1. The property requested is one of the following:  ([source](https://source.chromium.org/chromium/chromium/src/+/master:third_party/blink/renderer/core/css/properties/css_property.h;l=69;drc=d685ea3c9ffcb18c781bc3a0bdbb92eb88842b1b))

   * `height` , `width`
   * `top` , `right` , `bottom` , `left`
   * `margin` [ `-top` , `-right` , `-bottom` , `-left` , or *shorthand*] only if the margin is fixed.
   * `padding` [ `-top` , `-right` , `-bottom` , `-left` , or *shorthand*] only if the padding is fixed.
   * `transform` , `transform-origin` , `perspective-origin`
   * `translate` , `rotate` , `scale`
   * `grid` , `grid-template` , `grid-template-columns` , `grid-template-rows`
   * `perspective-origin`
   * These items were previously in the list but appear to not be any longer (as of Feb 2018): `motion-path` , `motion-offset` , `motion-rotation` , `x` , `y` , `rx` , `ry`
</details>

### Getting `Range` dimensions

* `range.getClientRects()` , `range.getBoundingClientRect()`

### SVG

Quite a lot of properties/methods force, but I haven't made an exhaustive list. 
This list in incomplete:

* SVGLocatable: `computeCTM()` , `getBBox()`
* SVGTextContent: `getCharNumAtPosition()` , `getComputedTextLength()` , `getEndPositionOfChar()` , `getExtentOfChar()` , `getNumberOfChars()` , `getRotationOfChar()` , `getStartPositionOfChar()` , `getSubStringLength()` , `selectSubString()`
* SVGUse: `instanceRoot`
Use the "chromium source tree link" below to explore on your own!

### contenteditable

* Lots & lots of stuff, …including copying an image to clipboard ([source](https://source.chromium.org/search?q=UpdateStyleAndLayout%20-f:test&ss=chromium%2Fchromium%2Fsrc:third_party%2Fblink%2Frenderer%2Fcore%2Fediting%2F))

## * Appendix

* Reflow only has a cost if the document has changed and invalidated the style or layout. Typically, this is because the DOM was changed (classes modified, nodes added/removed, even adding a psuedo-class like :focus).
* If layout is forced, style must be recalculated first. So forced layout triggers both operations. Their costs are very dependent on the content/situation, but typically both operations are similar in cost.
* What should you do about all this? Well, the `More on forced layout` section below covers everything in more detail, but the short version is: 
  1. `for` loops that force layout & change the DOM are the worst, avoid them. 
  1. Use DevTools Performance Panel to see where this happens. You may be surprised to see how often your app code and library code hits this.
  1. Batch your writes & reads to the DOM (via [FastDOM](https://github.com/wilsonpage/fastdom) or a virtual DOM implementation). Read your metrics at the begininng of the frame (very very start of `rAF` , scroll handler, etc), when the numbers are still identical to the last time layout was done. 

<center>
<img src="https://cloud.githubusercontent.com/assets/39191/10144107/9fae0b48-65d0-11e5-8e87-c9a8e999b064.png">
 <i>Timeline trace of The Guardian. Outbrain is forcing layout repeatedly, probably in a loop.</i>
</center>

##### Cross-browser 

* The above data was built by reading the Blink source, so it's true for Chrome, Opera, Brave, Edge and most android browsers. You can browse them [yourself in the Chromium source tree](https://source.chromium.org/chromium/chromium/src/+/master:third_party/blink/renderer/core/dom/document.h;l=657-680;drc=d685ea3c9ffcb18c781bc3a0bdbb92eb88842b1b).
* [Tony Gentilcore's Layout Triggering List](http://gent.ilcore.com/2011/03/how-not-to-trigger-layout-in-webkit.html) was for 2011 WebKit and generally aligns with the above. 
* Modern WebKit's instances of forced layout are mostly consistent: [ `updateLayoutIgnorePendingStylesheets` - GitHub search - WebKit/WebKit ](https://github.com/WebKit/webkit/search?q=updateLayoutIgnorePendingStylesheets&utf8=%E2%9C%93)
* Gecko's reflow appears to be requested via FrameNeedsReflow. Results: [ `FrameNeedsReflow` - mozilla-central searchfox](https://searchfox.org/mozilla-central/search?q=FrameNeedsReflow&case=false&regexp=false&path=%5E%5B%5E%5C0%5D)
* No concrete data on IE or EdgeHTML, but they likely were roughly the same, as the return values for these properties are spec'd.

#### More on forced layout

* **[Avoiding layout thrashing — Web Fundamentals](https://developers.google.com/web/fundamentals/performance/rendering/avoid-large-complex-layouts-and-layout-thrashing)** The **best** resource on identifying and fixing this topic.
* [CSS Triggers](http://csstriggers.com/) - covers what operations are required as a result of setting/changing a given CSS value. The above list, however, are all about what forces the purple/green/darkgreen circles synchronously from JavaScript.
* [Fixing Layout thrashing in the real world | Matt Andrews](https://mattandre.ws/2014/05/really-fixing-layout-thrashing/)
* [Timeline demo: Diagnosing forced synchronous layouts - Google Chrome](https://developer.chrome.com/devtools/docs/demos/too-much-layout)
* [Preventing &apos; layout thrashing&apos; | Wilson Page](http://wilsonpage.co.uk/preventing-layout-thrashing/)
* [wilsonpage/fastdom](https://github.com/wilsonpage/fastdom)
* [Rendering: repaint, reflow/relayout, restyle / Stoyan](http://www.phpied.com/rendering-repaint-reflowrelayout-restyle/)
* [We spent a week making Trello boards load extremely fast. Here’s how we did it. - Fog Creek Blog](http://blog.fogcreek.com/we-spent-a-week-making-trello-boards-load-extremely-fast-heres-how-we-did-it/)
* [Minimizing browser reflow  |  PageSpeed Insights  |  Google Developers](https://developers.google.com/speed/articles/reflow?hl=en)
* [Optimizing Web Content in UIWebViews and Websites on iOS](https://developer.apple.com/videos/wwdc/2012/?id=601)
* [Accelerated Rendering in Chrome](http://www.html5rocks.com/en/tutorials/speed/layers/)
* [web performance for the curious](https://www.igvita.com/slides/2012/web-performance-for-the-curious/)
* [Jank Free](http://jankfree.org/)

-------------

Updated slightly April 2020. Codesearch links and a few changes to relevant element properties.
