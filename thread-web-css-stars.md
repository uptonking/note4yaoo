---
title: thread-web-css-stars
tags: [css, thread, web]
created: 2021-07-25T12:48:41.836Z
modified: 2021-07-25T12:49:10.410Z
---

# thread-web-css-stars

# guide

# discuss-stars
- ## 

- ## It looks like "position: sticky" is not implemented for ::before and ::after pseudo-elements in Chrome?
- https://x.com/fabiospampinato/status/1866299411216695470
  - That's why in some way CSS is harder than JS, in practice you can run the JS in your head fairly reliably, but you can't always do that with CSS, it's a spaghetti blob of hundreds of properties interacting with each other in sometimes unpredictable way, with a sauce of limitations and quirks that are just unpredictable, you need to run an experiment to see what happens, for each different engine.

- ## Found a neat CSS trick to automatically swap between black or white text based on any arbitrary background color
- https://x.com/devongovett/status/1863733091409461256
  - https://codepen.io/devongovett/pen/QwLbRrW
  - With relative color syntax, you can use calc to adjust the text color depending if the background is above or below 50% lightness in the LCH color space.
- I hope the `* infinity` trick doesn't yield whiter-than-white when browsers finally get around to supporting HDR colors. by the way, oklab would be better for avoiding black-on-blue and white-on-yellow edge cases.

- ## TL; DR: `content-visibility` property good, `F` value broken.
- https://x.com/fabiospampinato/status/1856032799892861070
  - Today's important learnings about the CSS `content-visibility` property:
  - Setting it to "auto" is broken in Chrome as far as I can see, it considers every block I have in this huge page as visible, even though I have correct "contain-intrinsic-size" properties set for each block. 
  - Setting it to "auto" is broken in Chrome as far as I can see, it considers every block I have in this huge page as visible, even though I have correct "contain-intrinsic-size" properties set for each block. 
- The best way that I've found to get this stuff to work:
  1. Add "content-visibility: auto" to all blocks, you need that compared to "hidden" to be able to search natively into the blocks that you can't see. (bug in Chrome presumably)
  2. Add "content-visibility: visible" to the blocks that are visible, you need that to unbreak the CSS custom highlights. (bug in Chrome presumably)

- ## There is a free performance improvement you can make right now to your CSS variable animations (if they're scoped to the current element).
- https://x.com/mattgperry/status/1853728564316680552
  - Register your CSS variable the `inherits: false` option. Depending on the size of the style recalcs this can be a huge saving.
  - I stumbled on this trying to figure out a more performant way to animate a layer that's too large for the GPU but setting `.style.transform` is triggering a ton of style recalculations. 
  - Normally I recommend against animating CSS variables but just goes to show.
  - That was the conclusion of https://web.dev/blog/at-property-performance . Also: Custom Properties animate on the Main Thread

- The problem with animating custom properties is that this happens on the main thread (unless this was fixed on Chrome?)
  - Yes but in this instance making this large element a GPU layer is crashing mobile browsers. There’s also non-accelerated values that would benefit from this approach.

- ## the things we do when styling HTML we don’t control… 🫠
- https://x.com/LeaVerou/status/1854658564423622882
  - `[style*="color:#000"]`

- This must be HTML 4. I can see you're styling the `<font>` tag 

- ## Create hover gallery effect using flex grow 
- https://twitter.com/davidm_ml/status/1778436043781341443
  - 卡片点击后会展开当前卡片，压缩其他卡片
  - https://github.com/atherosai/ui/tree/main/gallery-06

- ## PREVIOUSLY: separate rulesets for light and dark
- https://twitter.com/argyleink/status/1773387209925869752
  - NOW: one ruleset with `light-dark()` .
  - made with Shiki "magic move"

- https://twitter.com/devongovett/status/1773523822290846048
  - Want to use light-dark() today across all browsers? Use @lightningcss 

- ## Here's the ultimate z-index hack — `z-index: calc(infinity)` .
- https://twitter.com/stefanjudis/status/1763476475150286971
- Technically, you will still lose the z-index battle if someone plays the `!important` card. 

# discuss
- ## 

- ## 

- ## 

- ## if you have ::highlight() CSS rules that don't match anything they can still have a major performance impact on the rendering of the page, in Chrome.
- https://x.com/fabiospampinato/status/1866890002161860663
  - A lot of things around CSS Custom Highlights should be reviewed again because things are outright buggy (like a ::selection with a transparent background erasing custom highlights, which makes no sense, or custom highlights not being rendered after scrolling to blocks with "content-visibility: auto", unless you click somewhere, sometimes), and sometimes when they are not buggy they are not fully right either (how is an highlight rule with no registered ranges expensive).

- ## I wrote an interactive article about `display: contents` in CSS
- https://x.com/shadeed9/status/1832053021557321871
  - [CSS display contents _202409](https://ishadeed.com/article/display-contents/)
  - 可以通过css去掉父元素，然后子元素提升为父元素

- ## Use CSS relative color syntax to darken/lighten colors for borders, backgrounds, etc.
- https://twitter.com/jh3yy/status/1770948509933445269

```CSS
.success {
  --c: green;
}

aside {
  background: oklch(from var(--c) calc(l * 0.75) c h / 0.5);
  color: oklch(from var(--c) calc(l * 1.5) c h);
}
```

- ## CSS Tips: To get the maximum z-index, you can use calc(1 / 0) in addition to calc(Infinity).
- https://twitter.com/yisibl/status/1767531873742528698

- ## height and width precede inset (or trbl) in CSS; 
- https://twitter.com/steveruizok/status/1759351789705433163
  - so if you want to make something full parent size, it's gotta be: `inset: 0px; height: 100%; width: 100%;`

- ## Backdrop blurs are such a silent performance killer. 
- https://twitter.com/austin_malerba/status/1733921016978583992
  - If you notice weird artifacts and reduced framerate while scrolling, definitely look for backdrop blurs as a likely culprit. I've been bitten by this many times.

- ##  `isolation: isolate` 在CSS中被用作创建新的堆叠上下文，特别适用于局部 z-index 控制。
- https://twitter.com/lencx_/status/1719206813512704302
  - 当不想让子元素的 z-index 影响其他元素或被其他元素所影响时，可以通过为父元素设置此属性来实现，从而确保子元素的堆叠范围仅限于其父元素内部。
  - https://codepen.io/lencx/pen/BaMKvLE

- ## Atomic CSS is surprisingly effective performance wise (if done well) which is why I'm all about it lately. 
- https://twitter.com/sebmarkbage/status/1529622374575923206
  - It scales well by flattening out both in terms of number of rules and incrementally loading rules. 
  - It minimizes recalc of the whole documents. It allows for local scoping.
  - The surprising part is why is it better than inline styles? Set aside the things inline styles can't do without JS like hover/media queries. Why is a string like `class="width-100 height-100"` (AND more bytes elsewhere) better for perf than `style="width: 100px; height: 100px"` ?
  - It seems to me that it basically comes down to parsing and converting these rules to internal representations in the browser. This is also supported by similar data from React Native. It's surprisingly costly to convert these strings to the native representation of the platform.
  - We're effectively using CSS only as a hash map to look up cached parsed values. Maybe browsers should just do that with all inline styles? At least the ones that don't change frequently (like a JS animation). We're effectively using classes as hint that something will be reused.
- **It’s not parsing itself that’s slow - that can be super fast**. 
  - It’s all the stuff that happens afterward, eg computing inherited values for every element, variable substitution etc. 
  - Inline styles also use a lot more memory per element than pointers to matched rules.

- Might be missing something but is `http://el.style.background = "some css string"` the same as `eval`?
- https://twitter.com/markusparkus5/status/1529421308961890304

- ## In CSS you can use `display: contents` to omit the box of an element, which makes it behave like its child elements
- https://twitter.com/sobedominik/status/1441004416866213892

- ## Poll: Imagine your company has a component library that implements your design system. Should the components support custom restyling?
- https://twitter.com/housecor/status/1429426336695824384
  (1) Yes. Supporting restyling makes them more flexible.
  (2) No. Supporting restyling leads to inconsistency.
- Yes, allow restyling. It makes it easier to track the exceptions and detect patterns to latter evolve the components to support them out of the box.
  - [spotify: Customization vs. Configuration in Evolving Design Systems](https://engineering.atspotify.com/2021/04/28/customization-vs-configuration-in-evolving-design-systems/)
  - I agree with this approach. Much like other components, only abstract and make reusable when the need arises. 
  - Use CSS for variations, when more common consolidate and update the library itself as a standard config option.
- I think more important than allowing or disallowing restyling is allowing anything to be used as a child component.
  - I once worked with with a component lib that only allowed you to use the library-blessed `<Tr>` component as a table row. This made it impossible to create custom components per-row to add additional logic, like lazy loading data for one of cells in the row. Absolute nightmare.
- I see the component library as a tool to build UIs. It should give developers enough flexibility to do their job. Whether consumers of the library want to customize it is their decision.

- ## Inlining critical CSS can improve how quickly a page renders. 
- https://twitter.com/addyosmani/status/1419190681864658946
  - Now an opt-in feature in Next.js and the default in Angular
  - [Resource inlining in JavaScript frameworks](https://web.dev/aurora-resource-inlining/)
- I wrote https://github.com/addyosmani/critical for use-cases like static sites + gulp. 
  - For apps + webpack, https://github.com/GoogleChromeLabs/critters may be a better fit.
- Yes, sure, the problem is whether to inline CSS or not, and has nothing to do with the megabytes of JS and nothing being done server-side anymore because it’s too boring.
- using inline style will force us to protect from unsafe inline (CSP guidelines) which is an inconvenience
