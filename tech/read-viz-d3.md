---
title: read-viz-d3
tags: [d3, read, viz]
created: '2021-05-27T19:54:19.960Z'
modified: '2021-05-27T19:54:31.731Z'
---

# read-viz-d3

# d3 for the impatient_201906
- notes
  - examples in d3 v5

## c1: d3 intro & conventions

- I believe that many of the difficulties experienced by new users are due to incorrect assumptions.
  - the new user is unpleasantly surprised at the verbosity required to set something as elementary as the color of an element
- The mistake here is that D3 is not a graphics library: 
  - instead, it is a JavaScript library to manipulate the DOM tree! 
  - Its basic building blocks are not circles and rectangles, but nodes and DOM elements; 
  - the typical activity does not involve the painting of a graphical shape on a canvas, but the styling of an element through attributes
- D3 is a web technology, and relies on a collection of other web technologies; 
  - D3 does make them easier to use, and it provides a considerable amount of unification and abstraction on top of them.
  - The only area where it is definitely not enough to “wing it” is SVG.
- **why d3**
  - D3 provides a convenient way to deliver graphics over the web
  - D3 makes it easy and convenient to create animated and interactive graphics
  - easy-to-learn, and easy-to-use framework for general-purpose DOM handling

- ### Conventions of the D3 API
- D3 is primarily an access layer to the DOM tree. 
  - As a rule, D3 makes no attempt to encapsulate underlying technologies, and instead provides convenient, but otherwise generic, handles on them. 
  - For example, D3 does not introduce “circle” or “rectangle” abstractions of its own, but instead gives the programmer direct access to the SVG facilities for creating graphical shapes. 
  - The advantage of this approach is that D3 is tremendously adaptable and not tied to one particular technology or version. 
  - The disadvantage is that programmers need to have knowledge of the underlying technologies, in addition to D3, since D3 itself does not provide a complete abstraction layer.
- Because JavaScript does not enforce formal function signatures, all function arguments are technically optional. 
  - Many D3 functions use the following idiom:
  - when called with appropriate arguments, these functions act as setters; 
  - when called without arguments, these functions act as getters
  - To entirely remove a property, call the appropriate setter while supplying `null` as argument.
- When called as setters, functions typically return a reference to the current object, thus enabling method chaining. 
  - (This idiom is so intuitive and consistent that it will rarely be mentioned explicitly again.)
- Instead of a value, many D3 setters can take an `accessor` function as argument, which is expected to return a value that will be used to set the property in question. 
  - The parameters expected by accessor functions are not the same across all of D3, but a set of related D3 functions will always call accessor functions in a uniform way. 
- Some important D3 facilities are implemented as function objects. 
  - They perform their primary task when called as a function, but they are also objects, with member functions and internal state (examples are scale objects; and generators and components). 
  - It is a common pattern to instantiate such an object, configure it using its member functions, and finally invoke it to complete its purpose. 
  - Frequently, the final invocation does not use explicit function-call syntax, but instead employs one of JavaScript’s methods for “synthetic” function calls: the function object is passed to another function (such as `call()`), which supplies the required arguments and finally evaluates the function object itself.

- ### Conventions for the API Reference Tables
- D3 functions are either called on the global `d3` object, or as member functions of some D3 object; 
  - some functions are available both ways. 
  - If a function is called through an object, this object is referred to as the `receiver` of the method call. 
  - Inside the member function, the `receiver` is the object pointed to by the `this` variable.
- Function signatures attempt to indicate the type of each argument, but many functions accept such a wide variety of different argument types that no unambiguous notation is practical. 
  - Where they are used, brackets indicate an array. 

- Naming conventions
- First-letter acronyms for individual objects: c for “circle, ” p for point, and so on. 
  - Append an “s” for collections: cs will be an array of circles
- Frequently occurring quantities have their own notation: 
  - pixels are denoted with px, scale objects with sc. 
  - Generators and components are function objects that “make” something and thus are called mkr.
- The letter d is used generically to indicate “the current thing” in anonymous functions. 
  - When working with D3 selections, d is usually an individual data point bound to a DOM element; 
  - when working with arrays, d is an array element (as in ds.map( d => +d )).
- Data sets are called data or ds.
- Selections representing either an `<svg>` or a `<g>` element are common and, when assigned to a variable, are denoted as svg or g.

## c2: examples

- Scales are function objects: you call them with a value from the domain and they return the scaled value.
- Both domain and range are specified as two-element arrays. 
- D3 tends to defer decisions in favor of “late binding”: 
  - for example, in the way that it is customary(习俗的，习惯的；典型的，独特的) to pass accessor functions as arguments, rather than requiring that the appropriate columns be extracted from the original data set before being passed to the rendering framework.
- Without scales or axes it is not possible to read quantitative information from the graph (or any graph, for that matter). 
  - We therefore need to add axes to the existing graph.
- Because the visual axis component consists of many individual SVG elements (for the tick marks and labels), it should always be created inside its own `<g>` container. 
  - all axes are initially located at the origin (the upper-left corner) and must be moved using the `transform` attribute to their desired location
- Functions that take a Selection as their first argument and then add elements to it are known as components and are an important mechanism for encapsulation and code reuse in D3. 
- a common D3 idiom: creating DOM elements is kept separate from configuring their appearance options!
- D3 assigns the active DOM element to `this` before invoking the callback, and so provides access to the current DOM element.

## c3: selections

- Selections are ordered collections of DOM elements
  - The Selection abstraction provides an API to query and modify the elements it contains.
- a Selection is a JavaScript wrapper around an ordered collection of DOM elements together with a set of methods to manipulate this collection. 
  - The API is declarative and supports method chaining, hence it is generally unnecessary to handle the elements of the collection explicitly.
- The `data()` method accepts an array of arbitrary values or objects 
  - and attempts to establish **a one-to-one correspondence** between the entries of this array and the elements in the current selection.
  - If a data point has been associated with a DOM element, the data point itself is stored in the `__data__` property of the selection element.
- The `data()` method **returns a new Selection object** containing those elements that were successfully bound to entries in the data set.
- The `exit()` method actually returns a Selection of DOM elements, but the `enter()` method only returns a collection of placeholder elements (by construction, there can be no actual nodes for surplus data points).
  - `enter()` returns the surplus data items
  - `exit()` returns the surplus DOM elements
- The `data()` method itself returns the Selection of DOM elements that were successfully bound to data points

- The General Update Pattern
- If an existing graph must be updated repeatedly with new data, the complete sequence of steps:
  1. Bind new data to an existing selection of elements. 
  2. Remove any surplus items that do not have matching data associated anymore (the `exit()` selection). 
  3. Create and configure all items associated with data points that did not exist before (the `enter()` selection). 
  4. Merge the remaining items from the original selection with the newly created items from the enter() selection.
  5. Update all items in the combined selection based on the current values of the bound data set.
- The exit selection contains an array having the same number of elements as the old data set, but with **only those entries populated for which there is no corresponding data point** in the new data set. 
  - Both enter and update selections contain arrays having an entry for each data point in the new data set, but with only those entries populated that are newly added or retained from previously, respectively. 
  - The `merge()` function combines these complementary arrays into one. 
  - If both arrays have a nonnull entry in the same position, one of them will be clobbered(打败；痛打). 
  - All of this is implemented using the JavaScript `Array` type, which allows for “holes” of unassigned, undefined values at arbitrary index positions. 
  - It is probably also best to consider all of this information as implementation detail and subject to change. 
  - Just remember the role of the `merge()` function as part of the General Update Pattern.

- The distinction between attributes and properties is subtle. 
  - Basically, an HTML element has attributes, a JavaScript Node object has properties. 
  - Most attributes map to properties and vice versa, but the names don’t always agree exactly
- The SVG specification distinguishes between properties as attributes that can be modified through CSS, in contrast to attributes in general, which cannot.
- Positions in pseudo-classes are evaluated at the time the pseudo-class is applied.
- `insert()` does not bind data; 
  - an explicit call to `datum()` is required to add data to elements added using insert().
- As a rule, methods that operate on individual elements of a selection return the current selection, whereas methods that operate on the entire selection return a new selection.
- there are some exceptions(functions that return new selection)
  - select(), selectAll()
  - data(), enter(), exit()
  - append(), insert(), remove()
  - merge(), filter(), sort()
  - create()

## c4: events & animation

- D3 treats event handling as part of the Selection abstraction
- If sel is a Selection instance, then you use the following member function to register a callback as event handler for the specified event type
  - Any DOM event type is permitted. 
  - If a handler was already registered for the event type via `on()`, it is removed before the new handler is registered. 
  - To register multiple handlers for the same event type, the type name may be followed by a period and an arbitrary tag (`click.formSubmit`)
- The actual event instance is not passed to the callback as an argument, but it is available in the variable `d3.event`
  - todo: ??? d3v6 has removed d3.event
- A behavior component is a component that installs required event callbacks in the DOM tree. 
  - it is also an object that has member functions itself.

- The Transition API allows you to change and remove elements, 
  - but it does not provide for the creation of elements as part of the transition.
- The Transition API replicates large parts of the Selection API.
- Technically, an easing is simply a mapping that is applied to the time parameter t before it is passed to the interpolator. 
  - This makes the distinction between the easing and the interpolator somewhat arbitrary. 
  - What if a custom interpolator itself mangles the time parameter in some nonlinear way?
- From a practical point of view, it seems best to **treat easings as a convenience feature** that adds “slow-in, slow- out” behavior to standard interpolators
  - D3 includes a confusingly large range of different easings, some of which considerably blur the distinction between an easing and what should be considered a custom interpolator
- A general problem with transitions is that they usually can’t be interrupted by the user
- D3 includes a special timer that will invoke a given callback once per animation frame, that is, every time the browser is about to repaint the screen. 
  - The time interval is not configurable because it is determined by the browser’s refresh rate
- 去除浮点数的小数部分 `d/n|0`

## c5: generator, layout, component

- SVG provides only a small set of built-in geometric shapes (like circles, rectangles, and lines)
  - Anything else has to be built up either from those basic shapes or by using the `<path>` element and its turtle(海龟) graphics command language
- To produce complex figures, D3 employs three different styles of helper functions. 
  - generators generate individual attributes, 
  - components create entire DOM elements, 
  - layouts determine the overall arrangement of the whole figure
- All of these helpers are implemented as function objects. 
  - They perform their primary task when invoked as a function. 
  - But they also have state and expose an API of member functions to modify and configure their behavior.
- D3 symbol generator uses an HTML5 `<canvas>` element for performance reasons, but there is no strict need to do so

## c6: file parser & formatter

## c7: scale & axes

## c8: color scales & heatmap

## c9: trees & networks

## c10: utilities: array, stats, datetime

# pro d3.js_201911

## c1: d3 intro

- why d3
  - thorough and complete control
  - built for web
  - good examples and large community
  - constantly improved

## c2: archetypal d3 chart

- The Margin Convention is a useful pattern that helps us avoid headaches when moving our SVG elements around. 
  - Once this pattern is arranged, the rest of the chart code can ignore margins altogether.

```JS
var g = svg.append("g").attr("transform", "translate(" + margin.left + "," + margin.top + ")");
```

## c3: d3 code encapsulation and comparison

- This abstraction should solve the problems we highlighted in the example code, namely: 
  - lack of clarity, configuration, reusability, composition, and testability. 
- there are so many coding flavors and levels of abstraction

- Object Oriented
  - plottable: many new

- Declarative
  - billboard: c3 fork, based on config object
  - vega: based on config json files
  - tell code what to do, but not how to do

- Functional
  - d3fc: like d3 methods
  - FP code avoids keeping global state, makes this state immutable, and favors the use of “pure functions.”
  - reusable and predictable. 

- Chained
  - britecharts、d3fc
  - A benefit is that they won’t need to create variables to store the results of each function call.
  - D3.js itself works in this way
  - Chained API (also named “Fluent Interface”)

- how to choose an api flavor
  - the most important goals: easy?customizable?fast?
  - developer bg

## c4: reusable api

- The Reusable API is a pattern to create modules that provides privacy and an interface based on getters and setters. 
  - It also allows us to group the creation of the charts' main building blocks. 
  - We do this by calling functions within the core of the pattern
- As a disclaimer, this version of the pattern and the following code evolved from the implementation in Developing a D3.js Edge and Mastering D3.js. 
  - These two great books were vital for the development of the Reusable API as we show it here
- we can create several charts with the same configuration and different data.

- benefits
  - simplicity with configurable api
  - modularity
  - reusability
  - composability
    - Accepting components as configuration
    - Hooking components to each other by using event handlers
  - testability

- drawbacks
  - Increased Complexity
    - There isn’t an escape from this. It is part of the tradeoff between the ease of use and the power of the abstraction. 
  - Inefficient Property Updates
    - One drawback of the Reusable API that developers mentioned is the need for re-calling the charts when updating some value
    - A proposed way of avoiding re-calling the chart would be to include an “updateWidth” accessor and call it when the width changes
    - Implementing “update functions” for all the chart properties won’t be scalable
    - we can throttle the call to “redrawChart”.
  - Boilerplate Code
    - This code includes the accessor functions, the logic for sizing the chart, labeling, and event handling
    - The solution is to generate the code of the accessors
    - If we want to avoid repetition in the chart-sizing logic and axes creation, we can extract their code
    - no base Class for Composition over Inheritance
    -  fine granularity of helpers gives us more flexibility

- The Reusable API covers a middle ground where the chart users need to use a bit of D3.js while the internals of the components are standard D3.js code. 
- We first read about the Reusable API pattern in Mike Bostock’s original post Towards Reusable Charts in 2012
  - It hasn’t changed a lot since then. 
  - Several libraries make use of this pattern, like nvd3
  - We also read about this pattern in books like Developing a D3.js Edge and Mastering D3.js.

### [Towards Reusable Charts_201202](https://bost.ocks.org/mike/chart/)

- ref
  - [time series d3.v3 example](https://bl.ocks.org/curran/66d926fe73211fd650ec)
  - [D3 Reusable Bar Chart Pattern(d3.v6)](https://observablehq.com/@john-guerra/d3-reusable-bar-chart-pattern)

- I’d like to propose a convention for encapsulating reusable charts in D3
- A function; the standard unit of code reuse!

- #### Configuration
- In truth we need a configurable function, since most charts require customization of their appearance or behavior. 
- A simple function is insufficient for highly-configurable charts. You could try a configuration object instead
- However, the caller must then manage both the chart function (assuming you have multiple types of charts to pick from) and the configuration object. 
- To bind the chart configuration to the chart function, we need a closure

```JS
function chart(config) {
  return function() {
    // generate chart here, using `config.width` and `config.height`
  };
}

var myChart = chart({ width: 720, height: 80 });
```

> A conventional object-oriented approach as `Chart.​proto­type.​render` would also work, but then you must manage the `this` context when calling the function.

- #### Reconfiguration
- what if you want to change the configuration after construction? Or if you want to inspect the configuration of an existing chart? 
- The configuration object is trapped by the closure and inaccessible to the outside world.
- Fortunately, JavaScript functions are objects, so we can store configuration properties on the function itself!
- The chart implementation changes slightly so that it can reference its configuration

- we can replace raw properties with getter-setter methods that allow method chaining.
- This gives the caller a more elegant way of constructing charts, and also allows the chart to manage side-effects when a configuration parameter changes
- The chart may also provide default configuration values. 

```JS
function chart() {
  var width = 720, // default width
    height = 80; // default height

  function my() {
    // generate chart here, using `width` and `height`
  }

  my.width = function(value) {
    if (!arguments.length) return width;
    width = value;
    return my;
  };

  my.height = function(value) {
    if (!arguments.length) return height;
    height = value;
    return my;
  };

  return my;
}

var myChart = chart().width(720).height(80);

// modify the existing chart
myChart.height(500);
myChart.height(); // 500
```

- To sum up: implement charts as closures with getter-setter methods
  - this is the same pattern used by D3’s other reusable objects, including scales, layouts, shapes, axes, etc.

- #### Implementation
- The chart can now be configured, but two essential ingredients are still missing: the DOM element into which to render the chart, and the data to display.
- These could be considered configuration, but D3 provides a more natural representation for data and elements: the `selection`.
- By taking a selection as input, charts have greater flexibility.
  - For example, you can render a chart into multiple elements simultaneously
  - You can control exactly when and how the chart gets updated when data or configuration changes
- The simplest way of invoking our chart function on a selection, then, is to pass the selection as an argument

```JS
myChart(selection);
// Or equivalently,
selection.call(myChart);
```

> The `call` operator is identical to invoking a function by hand; but it makes it easier to use method chaining.

- Internally, a `call`-based chart implementation looks something like this:

```JS
function my(selection) {
  selection.each(function(d, i) {
    // generate chart here; `d` is the data and `this` is the element
  });
}
```

- #### Examples
- A time series is a variable that changes over time. We can visualize this as an area chart

```JS
// 时间序列图表通用配置，简单示例
var chart = timeSeriesChart()
  .x(function(d) { return formatDate.parse(d.date); })
  .y(function(d) { return +d.price; });

var formatDate = d3.time.format("%b %Y");

// 数据和dom元素都在这里输入，开始执行绘制渲染
d3.csv("sp500.csv", function(data) {
  d3.select("#example")
    .datum(data)
    .call(chart);
});
```

- #### Further Considerations
- We now have a strawman convention for reusable visualization components
- Yet there is far more to cover as to what should be considered configuration or even a chart.
- Consider drawing inspiration from the Grammar of Graphics (see Polychart and ggplot2); there are more modular units for composition
- Even with traditional chart types, should you expose the underlying scales and axes, or encapsulate them with chart-specific representations? 
- animation, interaction, reactive...

## c5: make bar chart production-ready

## c6: britecharts

## c7: customize britecharts

## c8: extend a chart

## c9: test charts

## c10: build your library

## c11: creating documentation

## c12: use with react

# more-d3-books

## Integrating D3.js with React: Learn to Bring Data Visualization to Life /202106/src

- https://www.apress.com/gp/book/9781484270516 
- https://github.com/Apress/integrating-d3.js-with-react

- Set up your project with React, TypeScript and D3.js
- Create simple and advanced D3.js charts
- Work with complex charts such as world and force charts
- Integrate D3 data with **React state management**
- Improve the performance of your D3 components
- Deploy as a server or serverless app and debug test

## D3 Tips and Tricks v6.x: Interactive Data Visualization in a Web Browser /202102/free

- https://leanpub.com/d3-t-and-t-v6
- https://gist.github.com/d3noob

## Pro D3.js: Use D3.js to Create Maintainable, Modular, and Testable Charts /201911

- https://www.apress.com/gp/book/9781484252024
- https://github.com/Apress/pro-d3.js
- https://github.com/britecharts/britecharts
  - Client-side reusable Charting Library based on D3.js v5
  - https://github.com/britecharts/britecharts-react

- Create v5 D3.js charts with ES2016 and unit tests
- Develop modular, testable and extensible code with the Reusable API pattern
- Work with and extend Britecharts, a reusable charting library created at Eventbrite
- Use Webpack and npm to create and publish a charting library from your own chart collections
- Write reference documentation and build a documentation homepage for your library.

## Fullstack D3 and Data Visualization: Build beautiful data visualizations with D3 /201907

- https://www.newline.co/fullstack-d3
- https://github.com/TheRobBrennan/explore-data-visualization-with-D3

Chapter 0: Introduction When would you want to use D3.js?
Chapter 1: Making your first chart
Chapter 2: Making a scatterplot
Chapter 3: Making a bar chart
Chapter 4: Animations and Transitions
Chapter 5: Interactions
Chapter 6: Making a map
Chapter 7: Data Visualization Basics
Chapter 8: Common Charts
Chapter 9: Dashboard Design
Chapter 10: Advanced Visualization: Marginal Histogram
Chapter 11: Advanced Visualization: Radial Weather Chart
Chapter 12: Advanced Visualization: Animated Sankey Diagram
Chapter 13: D3 and React
Chapter 14: D3 and Angular

## D3 for the Impatient: Interactive Graphics for Programmers and Scientists /201905

- https://www.oreilly.com/library/view/d3-for-the/9781492046783/
- https://github.com/janert/d3-for-the-impatient

- Understand D3 selections, the library’s fundamental organizing principle
- Learn how to create data-driven documents with data binding
- Create animated graphs and interactive user interfaces
- Draw figures with curves, shapes, and colors
- Use the built-in facilities for heatmaps, tree graphs, and networks
- Simplify your work by writing your own reusable components
