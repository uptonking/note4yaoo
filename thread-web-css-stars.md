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

- ## 
# discuss
- ## 

- ## 

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
