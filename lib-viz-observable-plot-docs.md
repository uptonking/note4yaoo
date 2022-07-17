---
title: lib-viz-observable-plot-docs
tags: [docs, observable-plot]
created: 2021-05-05T07:42:17.542Z
modified: 2021-05-05T07:42:37.727Z
---

# lib-viz-observable-plot-docs

# guide

# concepts

## [marks](https://observablehq.com/@observablehq/plot-marks)

- Plot doesn’t have chart types.
- Instead, it has marks: geometric shapes such as bars, dots, and lines. 
  - Yet unlike a conventional graphics system, Plot marks are not positioned in pixels or colored literally. 
  - You draw with abstract data!
- A Plot mark is a template for generating shapes from data rather than a single shape.
- To make a plot, we bind columns of data to visual properties of marks. 
  - Since these visual properties encode abstract data, we call them **channels**. 
  - For example, we can encode the units column as the x-position and the fruit column as the y-position.
- Named columns are convenient for tabular data represented as an array of objects, but for greater flexibility we can use a function to feed abstract values to a channel. 
  - **Channel functions are repeatedly invoked for each element in the data**, being passed the datum (by convention d) and zero-based index (i). 
  - These functions can also perform data processing; 
- Named columns are also nice because they allow Plot to label the axes automatically, making the meaning of the plot more apparent. 
- An equivalent (and more efficient) way to specify channel values is with parallel arrays. 
  - Here it doesn’t really matter what’s in the data as long as each channel has an array of values of the same length as the data. 
  - This approach is well-suited to columnar data structures such as Arquero.
- Many marks provide default channel definitions for even more concise shorthand
- Plots can have multiple marks. 
  - Marks are layered such that the last mark is drawn on top. 
  - Each mark has its own data, channels, and options. 
  - However, marks share scales. 
  - Hence, multiple marks can be used to combine datasets: the scales’ domains are inferred from the union of associated data. 
  - For example, if you want to draw each dot using a separate mark, you can, though it’s less efficient and more verbose.
- Plot currently supports about a dozen mark types
  - Mark types do not just determine shape — they also determine which channels and options are supported, and what scales are associated with each channel, if any. 

## [Scales](https://observablehq.com/@observablehq/plot-scales)

- Scales map an abstract value such as time or temperature to a visual value such as x- or y-position or color. 
  - Scales define a plot’s coordinate system.
- In Plot, scales are named: 
  - x or y for position; fx or fy for facet position; r for radius; or color. 
  - A plot can have multiple scales but at most one scale of a given name.
- Mark channels are bound to scales; 
  - for example, a dot’s x channel is bound to the x scale. 
- The channel name and the scale name are often the same, but not always; 
  - for example, a bar’s y1 and y2 channels are both bound to the y scale.
- A scale is configured primarily by its input domain and output range: 
  - the domain is a set of abstract values typically derived from data, such as a time interval `[start, end]` or temperature interval `[cold, hot]`; 
  - the range is a set of visual values, such as an extent of the chart in pixels `[left, right]` or a color interval [blue, red].
- rather than you laboriously specifying everything, Plot can guess by inspecting the data so you don’t have to set the `type`, `domain`, and `range` (and for color, scheme) of scales explicitly. 
- But for Plot’s guesses to be accurate, your data must match Plot’s expectations.
- A scale’s type is most often inferred from associated marks’ channel values
- If a scale’s domain is specified explicitly, the scale’s type is inferred from the domain values rather than channels as described above.
- Finally, some marks declare the scale type for associated channels.
- scale.transform option allows you to apply a function to all values before they are passed through the scale.

## [Transforms](https://observablehq.com/@observablehq/plot-transforms)

- Transforms provide a convenient mechanism for deriving data while plotting. 
- All marks support the following basic transforms:
  - filter, sort, reserve
- The filter transform is similar to filtering the data with `array.filter`, except that it will preserve faceting and will not affect inferred scale domains; 
  - domains are inferred from the unfiltered channel values.
- Together the sort and reverse transforms allow control over z-order, which can be important when addressing overplotting.
- For greater control, you can also implement a custom transform function.

## [Facets](https://observablehq.com/@observablehq/plot-facets)

- The facet option produces horizontal or vertical small multiples to compare grouped data. 
- as with all ordinal scales in Plot, if the domain is not specified explicitly, it defaults to the union of values in natural order.
- To make room for the facet axes, you may need to specify the facet.marginTop/R/B/L
- When faceting, two additional band scales may be configured: fx and fy. 
  - These are driven by the facet.x and facet.y channels, respectively, which must be supplied strictly ordinal (i.e., discrete) values; 
  - each distinct value defines a facet. 
  - Quantitative data must be manually discretized for faceting, say by rounding or binning. 
  - Automatic binning for quantitative data may be added in the future.
- Only marks whose data is strictly equal to (===) the facet data will be filtered within each facet to show the current facet’s subset; 
  - other marks will be repeated across facets. 
