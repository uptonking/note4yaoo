---
title: lib-viz-observable-plot-docs-api
tags: [api, docs, observable-plot]
created: 2021-05-05T07:47:02.322Z
modified: 2021-05-05T07:47:17.725Z
---

# lib-viz-observable-plot-docs-api

# guide

# options

## `Plot.plot(options)`

- Renders a new plot given the specified options 
- returns the corresponding SVG or HTML figure element.
- All options are optional

## marks options

- `marks` option specifies an array of marks to render. 
  - Each mark has its own data and options; 
  - see the respective mark type (e.g., bar or dot) for which mark options are supported.
- Each mark may be a nested array of marks, allowing composition. 
  - **Marks are drawn in z-order, last on top**. 
  - For example, here bars for the dataset alphabet are drawn on top of a single rule at y = 0.

```JS
Plot.plot({
  marks: [
    Plot.ruleY([0]),
    Plot.barY(alphabet, { x: "letter", y: "frequency" })
  ]
})
```

## layout options

- These options determine the overall layout of the plot; 
  - width, height, marginTop/Right/Bottom/Left
  - all are specified as numbers in pixels
- The default `width` is 640. 
- The default `height` is 396 if the plot has a y or fy scale; 
  - otherwise it is 90 if the plot has an fx scale, or 60 if it does not. 
  - (The default height will be getting smarter for ordinal domains; )
- The default margins depend on the plot’s axes
  - for example, marginTop and marginBottom are at least 30 if there is a corresponding top or bottom x axis, 
  - and marginLeft and marginRight are at least 40 if there is a corresponding left or right y axis. 
- For simplicity’s sake and for consistent layout across plots, **margins are not automatically sized to make room for tick labels**; 
  - instead, shorten your tick labels or increase the margins as needed. 
  - In the future, margins may be specified indirectly via a scale property to make it easier to reorient axes without adjusting margins; 
- The `style` option allows custom styles to override Plot’s defaults. 
  - By default, the returned plot has a white background, a max-width of 100%, and the system-ui font. 
  - Plot’s marks and axes default to `currentColor`, meaning that they will inherit the surrounding content’s color.
- If a `caption` is specified, Plot.plot wraps the generated SVG element in an HTML figure element with a figcaption, returning the figure.

## scale options

- x, y, r, color, opacity
- Plot passes data through scales as needed before rendering marks. 
- A scale maps abstract values such as time or temperature to visual values such as position or color. 
- **Within a given plot, marks share scales**. 
  - For example, if a plot has two Plot.line marks, both share the same x and y scales for a consistent representation of data. 
- Plot does not currently support dual-axis charts, which are not advised.
  - [Why not to use two axes, and what to use instead](https://blog.datawrapper.de/dualaxis/)
- Some scale types are for quantitative data — values that can be added or subtracted, such as temperature or time. 
- Other scale types are for ordinal or categorical data — unquantifiable values that can only be ordered, such as t-shirt sizes, or values with no inherent order that can only be tested for equality, such as types of fruit.
- You can set the scale type explicitly via the `scale.type` option, but **typically the scale type is inferred automatically from data**: 
  - strings and booleans imply an ordinal scale; 
  - dates imply a UTC scale; 
  - anything else is linear. 
- Unless they represent text, we recommend explicitly converting strings to more specific types when loading data (e.g., with `d3.autoType` or Observable’s `FileAttachment`). 
- For simplicity’s sake, Plot assumes that data is consistently typed; 
  - **type inference is based solely on the first non-null, non-undefined value**. 
- Certain mark types also imply a scale type; 
  - for example, the `Plot.barY` mark implies that the x scale is a band scale.
- For quantitative data (i.e. numbers), a mathematical transform may be applied to the data by changing the scale type:
  - linear, pow, sqrt, log, symlog
- The appropriate transform depends on the data’s distribution and what you wish to know. 
- For temporal data (i.e. dates), two variants of a linear scale are also supported
  - utc, time
- For ordinal data (e.g., strings), use the ordinal scale type or the point or band position scale types. 
  - The categorical scale type is also supported; 
  - it is equivalent to ordinal except as a color scale, where it provides a different default color scheme. 
  - (Since position is inherently ordinal or even quantitative, categorical data must be assigned an effective order when represented as position, and hence categorical and ordinal may be considered synonymous in context.)
- You can opt-out of a scale using the `identity` scale type
- A scale’s domain (the extent of its inputs, abstract values) and range (the extent of its outputs, visual values) are typically inferred automatically. You can set them explicitly using these options
  - domain, range, reverse
- For most quantitative scales, the default domain is the `[min, max]` of all values associated with the scale. 
  - For the radius and opacity scales, the default domain is `[0, max]` to ensure a meaningful value encoding. 
  - For ordinal scales, the default domain is the set of all distinct values associated with the scale in natural ascending order; 
  - set the domain explicitly for a different order. 
  - If a scale is reversed, it is equivalent to setting the domain as `[max, min]` instead of `[min, max]`.
- The default range depends on the scale: 
  - for position scales `(x, y, fx, and fy)`, the default range depends on the plot’s size and margins. 
  - For color scales, there are default color schemes for quantitative, ordinal, and categorical data. 
  - For opacity, the default range is [0, 1]. 
  - And for radius, the default range is designed to produce dots of “reasonable” size assuming a sqrt scale type for accurate area representation: zero maps to zero, the first quartile maps to a radius of three pixels, and other values are extrapolated. 
  - This convention for radius ensures that if the scale’s data values are all equal, dots have the default constant radius of three pixels, while if the data varies, dots will tend to be larger.
- Quantitative scales can be further customized with additional options
  - clamp, nice, zero, percent
- The `scale.transform` option allows you to apply a function to all values before they are passed through the scale. 

## position scale options

- The position scales (x, y, fx, and fy) support additional options
  - scale.inset, scale.round
- The scale.inset option can provide “breathing room” to separate marks from axes or the plot’s edge. 

## color options

- The normal scale types — linear, sqrt, pow, log, symlog, and ordinal — can be used to encode color.
- Plot supports special scale types for color:
  - sequential(linear), cyclical(linear-rainbow), diverging(linear-rdbu), categorical(ordinal-tableau10)

## facet options

- When faceting, two additional band scales may be configured:
  - fx - the horizontal position, a band scale
  - fy - the vertical position, a band scale
- Similar to marks, faceting requires specifying data and at least one of two optional channels:
  - facet.data - the data to be faceted
  - facet.x - the horizontal position; bound to the fx scale, which must be band
  - facet.y - the vertical position; bound to the fy scale, which must be band
- The facet.x and facet.y channels are strictly ordinal or categorical (i.e., discrete); 
  - each distinct channel value defines a facet. 
  - Quantitative data must be manually discretized for faceting, say by rounding or binning. 
  - Automatic binning for quantitative data may be added in the future. 
# marks
- Marks visualize data as geometric shapes such as bars, dots, and lines. 
- An single mark can generate multiple shapes: 
  - for example, passing a `Plot.barY` to `Plot.plot` will produce a bar for each element in the associated data. 
- Multiple marks can be layered into plots.
- Mark constructors take two arguments: data and options. 
  - Together these describe a tabular dataset and how to visualize it. 
- Options that are shared by all of a mark’s generated shapes are known as **constants**, while options that vary with the mark’s data are known as **channels**. 
- Channels are typically bound to scales and encode abstract values, such as time or temperature, as visual values, such as position or color.
- A mark’s data is most commonly an array of objects representing a tabular dataset, such as the result of loading a CSV file, while a mark’s options bind channels (such as x and y) to columns in the data (such as units and fruit).
- Channel functions are invoked for each datum (d) in the data and return the corresponding channel value. 
  - (This is similar to how D3’s `selection.attr` accepts functions, though note that Plot channel functions should return abstract values, not visual values.)
- Missing and invalid data are handled specifically for each mark type and channel. 
  - Plot.dot will not generate circles with null, undefined or negative radius, or null or undefined coordinates.
  - Similarly, Plot.line and Plot.area will stop the path before any invalid point and start again at the next valid point, thus creating interruptions

## area

- Draws regions formed by a baseline (x1, y1) and a topline (x2, y2) as in an area chart. 
  - Often the baseline represents y = 0. 
  - While not required, typically the x and y scales are both quantitative.
- By default, the data is assumed to represent a single series (a single value that varies over time, e.g.). 
  - If the z channel is specified, data is grouped by z to form separate series. 

## bar

- Draws rectangles where x is ordinal and y is quantitative (Plot.barY) or y is ordinal and x is quantitative (Plot.barX). 
- There is usually one ordinal value associated with each bar, such as a name, and two quantitative values defining a lower and upper bound. 
- The lower bound is often not specified explicitly because it defaults to zero as in a conventional bar chart.

## cell

- Draws rectangles where both x and y are ordinal, typically in conjunction with a fill channel to encode value. 
  - Cells are often used in conjunction with a group transform.

## rect

- Draws rectangles where both x and y are quantitative as in a histogram. 
- Both pairs of quantitative values represent lower and upper bounds, and often one of the lower bounds is implicitly zero. 
- If one of the dimensions is ordinal, use a **bar** instead; 
- if both dimensions are ordinal, use a **cell** instead. 
- Rects are often used in conjunction with a bin transform.

## dot

- Draws circles (and in the future, possibly other symbols) as in a scatterplot.
- Dots are drawn in input order, with the last data drawn on top. 
  - If sorting is needed, say to mitigate overplotting by drawing the smallest dots on top, consider a sort and reverse transform.

## line

- Draws two-dimensional lines as in a line chart.
- By default, the data is assumed to represent a single series (a single value that varies over time, e.g.). 
  - If the z channel is specified, data is grouped by z to form separate series. 
  - Typically z is a categorical value such as a series name. 
  - If z is not specified, it defaults to stroke if a channel, or fill if a channel.

## link

- Draws line segments (or curves) connecting pairs of points.
- The link mark supports curve options to control interpolation between points. 
- Since a link always has two points by definition, only the following curves (or a custom curve) are recommended: linear, step, step-after, step-before, bump-x, or bump-y. 
- Note that the linear curve is incapable of showing a fill since a straight line has zero area.

## rule

- Draws an orthogonal line at the given horizontal (Plot.ruleX) or vertical (Plot.ruleY) position, either across the entire plot (or facet) or bounded in the opposite dimension. 
- Rules are often used with hard-coded data to annotate special values such as y = 0, though they can also be used to visualize data as in a lollipop chart.

## text

- Draws a text label at the specified position.
- If text is not specified, it defaults to `[0, 1, 2, …]` so that something is visible by default. 
- Due to the design of SVG, each label is currently limited to one line; in the future we may support multiline text.

## tick

- Draws an orthogonal line at the given horizontal (Plot.tickX) or vertical (Plot.tickY) position, with an optional secondary position dimension along a band scale. 
  - (If the secondary dimension is quantitative instead of ordinal, use a rule.) 
  - Ticks are often used to visualize distributions as in a “barcode” plot.
# decorations
- Decorations are **static marks that do not represent data**. 
  - Currently this includes only `Plot.frame`, although internally Plot’s axes are implemented as decorations and may in the future be exposed here for more flexible configuration.

## frame

- Draws a simple frame around the entire plot (or facet).
- The frame mark supports the standard mark options, but does not accept any data or support channels. 
# transforms
- Plot’s transforms provide a convenient mechanism for transforming data as part of a plot specification. 
- All marks support the following basic transforms:
  - filter, sort, reverse

- The filter transform is similar to filtering the data with `array.filter`, except that it will preserve faceting and will not affect inferred scale domains; 
  - domains are inferred from the unfiltered channel values.
- Together the sort and reverse transforms allow control over z-order, which can be important when addressing overplotting. 
- For greater control, you can also implement a custom transform function:
  - `transform` - a function that returns transformed data and index
- The basic transforms are composable: 
  - the filter transform is applied first, then sort, reverse, and lastly the custom transform, if any. 
  - A custom transform is rarely specified directly; instead it is typically specified via one of an option transform.

## bin

- Aggregates continuous data — quantitative or temporal values such as temperatures or times — into discrete bins and then computes summary statistics for each bin such as a count or sum. 
  - The bin transform is like a continuous group transform and is often used to make histograms. 
  - There are separate transforms depending on which dimensions need binning: Plot.binX for x; Plot.binY for y; and Plot.bin for both x and y.
- Given input data = `[d₀, d₁, d₂, …]`, by default the resulting binned data is an array of arrays where each inner array is a subset of the input data `[[d₀₀, d₀₁, …], [d₁₀, d₁₁, …], [d₂₀, d₂₁, …], …]`. 
  - Each inner array is in input order. 
  - The outer array is in ascending order according to the associated dimension (x then y). 
  - Empty bins are skipped. 
- While it is possible to compute channel values on the binned data by defining channel values as a function, more commonly channel values are computed directly by the bin transform, either implicitly or explicitly.
- You can control whether a channel is computed before or after binning. 
- To control how the quantitative dimensions x and y are divided into bins, the following options are supported:
  - thresholds, domain, cumulative
- The bin transform supports grouping in addition to binning: you can subdivide bins by up to two additional ordinal or categorical dimensions (not including faceting).
- Lastly, the bin transform changes the default mark insets: rather than defaulting to zero, a pixel is reserved to separate adjacent bins. 

## group

- Aggregates ordinal or categorical data — such as names — into groups and then computes summary statistics for each group such as a count or sum. 
  - The **group transform is like a discrete bin transform**. 
- You can declare additional channels to aggregate by specifying the channel name and desired aggregation method in the outputs object which is the first argument to the transform. 
- Most aggregation methods require binding the output channel to an input channel; 

## map

- Groups data into series and then applies a mapping function to each series’ values, say to normalize them relative to some basis or to apply a moving average.
- The map transform derives new output channels from corresponding input channels. 
  - The output channels have strictly the same length as the input channels; 
  - the map transform does not affect the mark’s data or index. 
- The **map transform is akin to running `array.map`** on the input channel’s values with the given function. 
  - However, the map transform is series-aware: 
  - the data are first grouped into series using the z, fill, or stroke channel in the same fashion as the area and line marks so that series are processed independently.

## select

- Selects a value from each series, say to label a line or annotate extremes.
- The select transform derives a filtered mark index; 
  - it does not affect the mark’s data or channels. 
- **It is similar to the basic filter transform except** that provides convenient shorthand for pulling a single value out of each series. 
  - The data are grouped into series using the z, fill, or stroke channel in the same fashion as the area and line marks.

## stack

- Transforms a length channel into starting and ending position channels by “stacking” elements that share a given position, 
  - such as transforming the y input channel into y1 and y2 output channels after grouping on x as in a stacked area chart. 
  - The starting position of each element equals the ending position of the preceding element in the stack.
- The `reverse` option reverses the effective order.
# curves
- A curve defines how to turn a discrete representation of a line as a sequence of points `[[x₀, y₀], [x₁, y₁], [x₂, y₂], …]` into a continuous path; 
  - i.e., how to interpolate between points. 
- Curves are used by the line, area, and link mark, and are implemented by `d3-shape`.
- The supported curve options are:
  - curve - the curve method, either a string or a function
    - If curve is a function, it will be invoked with a given context in the same fashion as a D3 curve factory.
  - tension - the curve tension (for fine-tuning)
    - The tension option only has an effect on cardinal and Catmull–Rom splines (cardinal, cardinal-open, cardinal-closed, catmull-rom, catmull-rom-open, and catmull-rom-closed). 
    - For cardinal splines, it corresponds to tension; 
    - for Catmull–Rom splines, alpha.
# formats
- These helper functions are provided for use as a `scale.tickFormat` axis option, as the text option for `Plot.text`, or for general use. 
  - See also d3-time-format and JavaScript’s built-in date formatting and number formatting.
