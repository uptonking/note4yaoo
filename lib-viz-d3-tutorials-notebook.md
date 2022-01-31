---
title: lib-viz-d3-tutorials-notebook
tags: [d3, notebook, tutorials, viz]
created: '2021-05-18T08:48:48.865Z'
modified: '2021-05-18T08:49:58.244Z'
---

# lib-viz-d3-tutorials-notebook

# guide

- [D3 Charts: D3 examples as reusable functions! Ready for import or copy-paste.](https://observablehq.com/collection/@d3/charts)

# Learn D3

## introduction

- Why bother learning D3? And why learn here in Observable?
- For one, D3 is popular (80M downloads and 90K stars)
  - There are plenty of community-developed resources, including forkable examples, tutorials, videos, classes, and books.
- For another, D3 is flexible.
  - This flexibility stems from D3’s low-level approach, focusing on composable primitives such as shapes and scales rather than configurable charts.
- And D3 is renowned for animation and interaction.
  - Animation can be a powerful device for storytelling, while interaction allows active readers to explore.
  - This power, of course, comes at a cost. There’s much to learn: D3 has more than thirty modules and a thousand methods! 
- Observable is the ideal environment for learning D3 
  - because it simplifies code with dataflow, like a spreadsheet. 
  - As you edit, cells run automatically for rapid feedback.
  - You can add interaction or animation with almost no code! 
  - And Observable revolves around collaboration

## by example

- Say I hand you a set of numbers. What might you tell me about this data?
- `[d3.min(values), d3.median(values), d3.max(values)]`
- But we need something richer than a single number to get a sense of the distribution.
- We need a visualization. Specifically, a histogram.
- `import {chart as chart1} with {values as data} from "@d3/histogram"`
- we’re not limited to substituting data when we import. We can override any cell, say to customize the appearance of the x- or y-axis.
- `import {chart as chart2} with {values as data, height} from "@d3/histogram"`
- We didn’t need to rewrite the histogram to make it live because cells referencing mu, including imported cells, automatically run when mu changes thanks to dataflow.

## working with data

- Observable is akin to a spreadsheet: each cell defines a singular value.
- A subtle consideration when working with data in Observable is whether to put code in a single cell or separate cells. 
- A good rule of thumb is that a cell should either define a named value to be referenced by other cells, 
  - or it should display something informative to the reader (such as this prose, the chart above, or cells which inspect the data).
- A critical implication of this rule is that you should avoid implicit dependencies between cells: only depend on what you can name.
- Why? A notebook’s dataflow is built from its cell references. 
  - If a cell doesn’t have a name, it cannot be referenced and cells that implicitly depend on its effect may run before it. (Cells run in topological order, not top-to-bottom.) 
  - Implicit dependencies lead to nondeterministic behavior during development, and possible errors when the notebook is reloaded!

## scales

- scale maps an abstract dimension of data to a visual variable.
- an abstract dimension need not be spatial. 
  - It may be quantitative, such as the count of each fruit above. 
  - Or it may be nominal, such as a name.
- graphical marks such as points and lines can “represent differences (≠), similarities (≡), a  quantified order (Q), or a nonquantified order (O), 
  - and can express groups, hierarchies, or vertical movements” using position, size, color, and the like. 
  - These properties of graphical marks are our visual variables.
- Like many visualizations, the bar chart below maps two abstract dimensions to two visual variables
- D3 scales come in many types. 
  - Which you use depends on the abstract dimension (quantitative or nominal?) and the visual variable (position or color?). 
  - Each scale is configured by pairwise correspondences from abstract data (the domain) to visual variable (the range). 
- Scale methods can also be used to retrieve their associated values if you call them with no arguments.
- By convention, most D3 charts apply margins to inset scale ranges and make room for axes. 
  - Hence, x(0) is often not zero; it’s the size of the left margin.
- Another great reason to use scales is that D3 provides axes for explicitly showing a positional scale’s encoding, complete with nice, human-readable ticks

## shapes

- SVG and Canvas are intentionally generic; they allow for any type of graphic. 
- D3 meanwhile is intended for visualization, and so provides a specialized vocabulary of shapes which are functions that generate path data.
- A path’s shape is specified in the SVG path data language (or equivalent Canvas path methods), which is akin to commands you’d give an old-fashioned pen plotter. Such as:
  - Mx, y - move to the specified point [x, y]
  - Lx, y - draw a line to the specified point [x, y]
  - hx - draw a horizontal line of length x
  - vy - draw a vertical line of length y
  - z - close the current subpath
- To draw the line, we need path data that starts with `Mx,y` to move to the first point, followed repeatedly by `Lx,y` to draw a line to each subsequent point. 
  - We could do this by looping over the points to concatentate.
- But `d3.line` is more convenient. 
  - Calling `d3.line` returns a default line generator, 
  - and by calling `line.x` and l`ine.y` we can configure the line with functions to return the x- and y-position for a given data point d. 
  - These functions retrieve the desired abstract value (date or count) and convert it to visual position (by applying a scale).
- Passing the line generator the data returns the corresponding SVG path data string which can be used to set a path element’s `d` attribute.
- Lines and areas are designed to work together: you can derive the line corresponding to an area’s baseline or topline by calling area.lineY0 or area.lineY1, respectively.
- visualization is not just bars, lines, and areas.
- Another common shape is what D3 calls the `arc`, but what mathematicians would call an annulus(环状物；环带) sector(扇形). 
  - It features in pie charts, donut charts and sunbursts (but not, confusingly, arc diagrams).

## animation

- An animation is not a single graphic but a sequence of graphics over time. 
  - This sequence can be represented as a cell (or function) that returns the graphic for a given time t. 
  - For simplicity, we often use normalized time where `t = 0` is the start of the animation and `t = 1` is the end.
  - Our cell could theoretically return any graphic for a given time `t`, but often the graphic for time t is similar to the one for time `t + ϵ`
  - This similarity from frame to frame helps the viewer follow along
  - Hence, continuous animations are often defined by discrete keyframes with intermediate frames generated by interpolation, or tweening.
- To assist with animation (among other uses), D3 provides interpolators. 
- `d3.interpolate` accepts numbers, colors, strings-of-numbers, and even arrays and objects. 
  - Given a start and end value, d3.interpolate returns a function that takes a time `0 ≤ t ≤ 1` and returns the corresponding inbetween value.
- Animation is more than interpolation, however: it’s also timing. 
  - We need to redraw sixty times a second, 
  - and to compute the normalized time t based on real time and the desired start time and duration of the animation.
- We’ve seen two timing methods so far.
- The first relies on D3’s transitions, creating an initial graphic and then starting a transition to modify it (interpolating the stroke-dasharray).
- The second relies on Observable’s dataflow, recreating the graphic whenever the referenced `t` changes and relying on a `scrubber` for timing. 
  - This is less efficient than the previous method because the graphic is created from scratch each frame, but easier to write.
- Observable has another powerful tool for controlling animation: generators. 
  - When a generator cell yields a value, its execution is suspended until the next animation frame, up to sixty times per second.

- Given the variety of possible approaches to animation in Observable, which should you use? It depends!
  - If the graphic is simple enough that you can recreate it from scratch each frame—or if you don’t actually need animated transitions—then write the graphic declaratively.
    - Thanks to Observable’s dataflow, a “static” graphic can be made responsive, interactive, or animated without changing its code.
  - On other hand, for dynamic graphics of greater complexity—where performance necessitates efficient incremental updates—employ transitions or generators.
  - You can also combine approaches.

## joins/selections

- D3 selections fill a particular niche(功能；商机): fast, incremental updates of dynamic graphics. 
  - If your focus is on static graphics, or graphics that can be redrawn from scratch each frame, you may prefer a different abstraction. 
  - On the other hand, if you want animated transitions or to squeeze the best performance out of modern browsers, selections are for you.
- At heart, D3 selections specify transformation rather than representation. 
  - Instead of expressing the desired state of the graphic (the DOM), you specify the changes (insertions, updates, and deletions) needed to transform the current state into the desired state. 
  - This is sometimes tedious but allows you to animate transitions and to minimize changes to the DOM, improving performance.

- you want to apply the minimal set of updates to reflect the new data. 
  - `text` is a selection of text elements, initially empty, whose parent is the SVG element. 
  - This parent determines where entering text elements will be appended later.
  - By calling `selection.data`, text is bound to a new array of data, `letters`. 
  - This computes three disjoint subsets of the `text` selection: 
    - the `enter` selection representing new data for which there is no existing element; 
    - the `update` selection representing existing elements for which there is new data; 
    - and the `exit` selection representing existing elements for which there is no new data.
  - These selections are hidden in the code: `selection.data` returns the `update` selection, from which you can call `selection.enter` or `selection.exit` to access the others.
  - We could handle these three cases manually, but `selection.join` provides convenient defaults. 
  - The enter selection is appended; the exit selection is removed; and lastly the update and enter selections are merged, ordered and returned
- We can be even more efficient by observing that we don’t need to reassign some attributes and text content on updating elements as long as the association between letter and text element remains constant. 
  - To preserve this association, selection.data needs a key function; 
  - and for precise operations on enter, update, and exit, selection.join needs corresponding functions. 
- The key function passed to `selection.data` is used to compute a (string) key for each new datum and each selected element’s old datum, determining which datum is bound to which element: 
  - if an element and datum have the same key, that datum is bound to the element and the element is put in the update selection. 
  - Letters make good keys, so the identity function (d => d) is appropriate here.
  - If no key function is specified, data is bound by index: the first datum is bound to the first element, and so on. 
- Where selections really shine, though, are transitions!

## interaction

- There’s almost always too much information than can reasonably “fit” in a graphic.
  - Thus design is not just deciding how to show something, 
  - but what to show and what not to show based on what we think matters to the imagined reader.
- Interactivity allows the reader to surface more information
- if we seek to explore the unknown, then interaction can be faster than coding a new graphic
- A good guideline for interaction is Ben Shneiderman’s information-seeking mantra:
  - Overview first, 
  - zoom and filter, 
  - then details on demand.
- Details on demand allows the reader to extract exact values from the chart, rather than be limited to visual approximations. 
  - This can be as simple as tooltips.
- One approach to tooltips is to liberally sprinkle title elements into SVG. 
  - Mouseover (and wait briefly) to see
- A more general approach is a Voronoi overlay, where the closest data point to the mouse determines the tooltip.
- Native tooltips have several drawbacks: 
  - they can be sluggish(迟缓的) to appear; 
  -  mobile browsers don’t support them; 
  -  and it’s not always obvious which data point is associated with the tooltip, especially when using a Voronoi diagram.
- With a little more work, though, we can have custom tooltips.
- The ordering of elements here is important: SVG does not support z-order, so to draw the tooltip on top of the line and axes, it must be last.
- Whereas native tooltips appear automatically, custom tooltips typically require event listeners. 
- Observable’s HTML template literal does not currently support event listeners as attributes. 
  - Our newer hyperscript literal does support event listeners, so consider using that instead
- Tooltips triggered by `mouseover` events can be expensive: they require a separate element for each hoverable area of the chart. 
  - For complex charts, you may improve performance by calculating what is hovered on demand.
  - A particularly efficient approach for data sorted on one dimension, such as our time-series data here, is bisection on mousemove
- All the examples above demonstrate local interaction: interacting with the chart only affects the chart itself. 
- One of the most exciting aspects of Observable is that language-level reactivity makes it easy for interaction in one cell to ripple to any other cell in the notebook for global interaction!
- Most interactive controls in Observable are implemented as views. 
  - To make a view, define a `viewof` cell that returns an HTML input element. 
  - The input’s live current value will then be exposed to the rest of the notebook.
- These views involve generators, too: 
  - when you use the `viewof` operator, Observable implicitly creates an asynchronous input generator that yields a new value whenever you interact with the view.
- But views aren’t limited to HTML inputs—they can be anything! 
  - The only requirement is that the view exposes a `value` property and emits `input` events whenever that value changes.
  - Even charts can be views. The chart below dispatches synthetic input events when the mouse moves.
- Thanks to the Observable community, there are many custom inputs ready for reuse. 
  - See Jeremy’s inputs bazaar for a variety of useful options. 
  - Or for animation, consider a scrubber.

## further topics

- Clean data is a prerequisite for effective data visualization.
  - [Working with Wikipedia Data](https://observablehq.com/@mbostock/working-with-wikipedia-data)
  - Wikipedia has a fantastic array of tables on various subjects. 
  - Even better, Wikipedia has a CORS-accessible API! 
  - In this notebook, I’ll show how to load data directly from Wikipedia into an Observable notebook. 
- We limited ourselves to abstract tabular data, but D3 also works with other types of data
  - For networks, consider a chord diagram or force-directed graph. 
  - For hierarchical data, d3-hierarchy implements several popular algorithms, including treemaps and tidy trees. 
  - For cartography and geospatial visualization, see d3-geo. 
  - And for time-series data, see d3-time.
- d3-scale also provides numerous transformations
  - Your visualization will be more effective if you choose a transformation appropriate to your data
  - [Methods of Comparison, Compared](https://observablehq.com/@mbostock/methods-of-comparison-compared)
- For more control over how your data is presented, D3 provides low-level methods for formatting numbers and dates (in your desired locale). 
- For animation, explore D3’s easing methods, interpolators, and transitions
- for interaction, see D3’s reusable behaviors: brushing, zooming, and dragging.
- There’s a variety of Observable-specific topics you could tackle, too. 
  - promises, generators, and views.
- Thinking in visual variables will help you design better visualizations in D3, too. 
  - For labeling dense graphs, consider a Voronoi heuristic or iterative optimization. 
  - For showing color encodings, use a color legend.
