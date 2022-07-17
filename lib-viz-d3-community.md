---
title: lib-viz-d3-community
tags: [community, d3, viz]
created: 2021-05-29T21:05:33.951Z
modified: 2021-05-29T21:06:01.999Z
---

# lib-viz-d3-community

# pieces

- ## 

- ## 

- ## 

- ##  D3 and React can be tricky, because they both manipulate the DOM without reloading the whole page. 
- https://twitter.com/artistjaneadams/status/1397232666341163008
  - Left: D3's data join method; Right: React's Virtual DOM mechanic
- the more I thought about the longevity of our codebase, I decided to go the @plotlygraphs route.
  - [React Plotly.js in JavaScript](https://plotly.com/javascript/react/)
  - Much like other libraries like Vega/Altair, semantic encoding of functionality felt like an easier entry point for non-data-viz folks on our team.
- I still think D3 is wonderful for bespoke, 1-off visualizations, especially for unique formats beyond the standard line, bar, and scatter plots. 
  - But for @storywrangling , having simple, modular components of common graphs was more aligned with our use case.
  - So our back-end remains the same, but for v2 of Storywrangling (to be released in June), you'll see visualizations rendered using React and Plotly.

- ## What is your go-to method for D3 charts in React? An existing component library? Your own components?
- https://twitter.com/robhawkes/status/1393125636391284737
- I combined them by keeping them separate. React provides an empty DOM node and D3 does everything else. Makes for portable D3 code and a clear separation of responsibilities.
  - That makes sense; I'm not a massive fan of making everything React in any case (working with WebGL, etc). It's a tough balance but I like your example of how it keeps D3 logic transferrable to a non-React environment.
- Own components, with React doing all the DOM and rendering, and D3 for data manipulation, layouts, scales
- Own components, something like the screenshots. 'createChart' is fired on window resize and React useEffect/componentDidUpdate, and d3 operates over a DOM node ref provided by react Render. Transitions and D3 update & exit go out of the window in this model, though
  - I think I'd go for a custom setup like yours as you get so much more control over output.

- ## a quick performance test of different ways to combine React and d3:
- https://twitter.com/Wattenberger/status/1123413424678027265
  - A: d3 as util (for scales) and React for rendering elements
  - B: d3 as util and for rendering (within a React wrapper `<div>` )
  - Variant B (d3 for rendering) took ~4x as long as A. Only one sample ofc, I'll dig more
- I'd love to see other tests. Particularly animation. I didn't realize rendering the dom with react was so much faster. What if you have ten charts, like a dashboard? I'd also love tips on implementing this method.

- ## I wrote up a guide for combining React & d3
- https://twitter.com/Wattenberger/status/1375063666840772615
- [react + d3.js](https://wattenberger.com/blog/react-and-d3)
  - 提供了代码教程，后面还有超棒的示例
  - The crux of the issue is that they both want to handle the DOM.
- We've covered:
  - how to draw svg elements
  - how to draw many svg elements
  - how to replicate built-in d3 methods for drawing complex elements like axes
  - how to size our charts easily
  - how to draw maps!
- The rules(in the guide) definitely extend to all other Javascript frameworks. I've used very similar code many times, especially in Svelte 

- I'm curious: How well does React scale vs D3, for doing the rendering of many components? Could you take the "Creating Many D3 elements" example and scale it, add mutation and corresponding animation, and profile the render?
  - since every SVG element is a DOM element, there's a good amount of overhead and things can get slow, in my experience ~1000 elements. I'll often use SVG by default and switch to Canvas (imperative code, no mouse events) if I need better perf
- WRT React vs D3 for rendering: Both can output same DOM, but their approaches for manipulating/updating are different. I *suspect* React might be slower because it's creating a Component wrapper around each, but I also wonder if its DOM-diffing approach offsets(抵消、补偿) that overhead.
  - Yeah, it can be a bit slower, with all of the overhead. I'll sometimes go down the rabbit hole of perf checking and memoizing components, when a viz would still be snappy with vanilla js & d3. But I much prefer working with a js framework
  - Totally agree! Tho sometimes you don't have a choice. While React (or any framework) helps make things more readable and manageable (and testable!!), it's important to realize there might be tradeoffs as well.
- Very nice! I definitely advocated for this approach before, but I've found that both `react-spring` and `framer-motion` cause a lot of slowdowns when there are a lot of circles to animate (~500). Switching to `d3-transition` made it much smoother. Any thoughts on this?
  - there's definitely overhead with React that could require paying attention to perf, I'll always default to css animations when possible. but I'll take the tradeoffs for being able to use a framework any day

- Maybe I didn’t get it right but it seems that when you show “the React way”, d3 is no longer used. 
  - I see how you could come to that conclusion - a lot of people see d3 as a monolithic lib, but I prefer to think of it as a bag of really useful functions. You can use most of the API while not stepping on React's toes
  - She shows a few examples that are React only, but further down she brings in D3 as well. 
  - You are right, I didn't see it before because I was reading the code from my mobile phone. However, it's so minimal that the React code basically re-implements d3 features. Which makes sense to me because there is a lot of overlap between d3 SVG DOM manipulation and React.

- Based on your experience, which framework works better with d3 and which one is better for DataViz overall
  - definitely the one you're most comfortable with! 
