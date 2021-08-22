---
title: thread-web-css-stars
tags: [css, thread, web]
created: '2021-07-25T12:48:41.836Z'
modified: '2021-07-25T12:49:10.410Z'
---

# thread-web-css-stars

# pieces

- ## 

- ## 

- ## 

- ## 

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
