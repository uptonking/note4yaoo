---
title: lib-viz-observable-plot-docs
tags: [docs, observable-plot]
created: '2021-05-05T07:42:17.542Z'
modified: '2021-05-05T07:42:37.727Z'
---

# lib-viz-observable-plot-docs

# guide

# [Introducing Observable Plot](https://observablehq.com/@observablehq/introducing-observable-plot)

- Observable’s mission is to help everyone make sense of the world with data. 
- With its concise and (hopefully) memorable API, Observable Plot lets you try out ideas quickly. 
  - You can make a meaningful chart with as little as one line of code. 
  - Yet Plot is still powerful and expressive when you need it. 
  - Plot is highly configurable and supports interaction with minimal fuss through Observable dataflow. 
  - And Plot is designed to be extended 
- **Plot’s aim is speed and convenience**. 
  - Our hope is you’ll spend less time reading the docs, searching for snippets, and debugging — and more time asking questions of data. 
  - With faster iteration, you can see more of your data and find more insights.
  - Plot not only has intuitive syntax but makes it incredibly easy to iterate through different chart types and faceting methods
- Plot is informed by ten years of maintaining D3 but does not replace it. 
  - We continue to support and develop D3, and recommend its low-level approach for bespoke explanatory visualizations and as a foundation for higher-level exploratory visualization tools. 
  - In fact, Plot is built on D3! 
  - Observable Plot is more akin(相似的) to Vega-Lite, another great tool for exploration. 
  - We designed Plot to pair beautifully with Observable: to leverage Observable dataflow for fluid exploration and interaction. 
  - However, Plot does not depend on Observable; use it wherever you like.

# [Observable Plot Overview](https://observablehq.com/@observablehq/plot)

- Observable Plot is a free, open-source JavaScript library to help you quickly visualize tabular data. 
- It has a concise and (hopefully) memorable API to foster fluency — and plenty of examples to learn from and copy-paste.
- Plot’s goal is to help you get a meaningful visualization quickly.

- Plot employs a layered grammar of graphics inspired by Vega-Lite, ggplot2, Wilkinson’s Grammar of Graphics, and Bertin’s Semiology of Graphics. 
- Plot rejects a chart typology in favor of marks, scales, and transforms. 
- Plot can be readily extended in JavaScript, whether to define a channel, a transform, or even a custom mark. 
- And Plot is compatible with Observable dataflow: use inputs to control charts, and views to read chart selections. 

- We created Plot to better support exploratory data analysis in reactive, JavaScript notebooks like Observable. 
- We continue to support D3 for bespoke explanatory visualization and recommend Vega-Lite for imperative, polyglot environments such as Jupyter. 
- Plot lets you see your ideas quickly, supports interaction with minimal fuss, is flexible with respect to data, and can be readily extended by the community. 

# [Plot for D3 Users](https://observablehq.com/@observablehq/plot-for-d3-users)

- Plot represents a chart in its own terms.
- D3 transforms the native DOM; 
  - it describes incremental changes to standard HTML or SVG elements and their attributes.
  - It has no notion of a “bar”, let alone a bar chart, 
  - but you can use it to append and transform an SVG `<rect>`, which serves the role of a bar.
- In contrast, Plot has its own vocabulary of building blocks on top of the DOM, 
  - like Plot.barY and Plot.barX for bar charts, which draw the `<rect>` for you. 
  - You use them to describe what the visualization should look like, not how to build it. 
  - Plot just takes one options object, with an array of marks, and returns a whole SVG.

- The scales are inferred.
  - In both D3 and Plot there’s a prominent function(d) that takes some data and returns… something. But they return different things
- The typical D3 pattern is to get the part of the data you want (here the date), and then pass it to a scale (here x) that turns it into an attribute value (here pixels). 
  - But in Plot, you just do the first part: specify how to get the data. The scales are inferred! Since that simplifies the function, you can also just write a string for the property of the data you want.

- You can take it apart or mash pieces together.
  - Most of our examples make a whole Plot in one expression, which can make it look like an imposing and indivisible block of code. 
  - But it’s just a plain JavaScript object with a plain JavaScript array for the marks. 
  - That means you can rearrange it more freely, without breakage, than a tangled thicket of D3. 

- Plot breaks less and shows more when it does.
  - While making a chart in D3, it’s common to get stuck with a bunch of code and nothing showing up at all. 
  - In Plot, so long as you don’t have a syntax error, you’re much more likely to see something. 
  - that partial broken chart can often help visualize what you’re doing wrong.

- You update a Plot by re-rendering the whole thing.
  - D3 involves managing a lot of state, like “this selection needs to update this when that changes”. 
  - But Plot declares the representation of a chart all at once, without an update pattern, 
  - which means the natural thing to do on Observable is to just use reactivity to throw it all away and re-render the whole thing whenever something it depends on changes. 
  - Yes, it’s inefficient; no, it doesn’t smoothly transition. 
  - But in my experience it has not been an issue, and it is possible to extend Plot to be more conscientious of this.

- Faceting is now so easy as to be worth doing.
  - D3 made transitions comparatively easy, so D3 charts have a lot of transitions. 
  - But it never made faceting easy. 
  - Faceting is a way to repeat the same chart several times for different parts of the data, like small multiples; Plot lets you facet in both x and y.

- We’re working on interactivity
  - Plot uses Observable’s reactivity for interactivity; it does not have a separate internal interaction system. 
  - But you could add a slider Input in one cell representing altitude, and have a Plot in another cell showing a 2D heatmap of air temperatures at a given altitude. 
  - Plot doesn’t re-implement reactivity internally because it grew up in a context in which reactivity is in the air all around.
  - However, we do plan to add brush and point interactions to Plot soon, so that charts can expose selections to the rest of the notebook.
  - Plot locates more of its dynamism on the notebook layer. 

- We’re working on plugins.
  - A mark has an initialize method and a render method, which you can implement to write your own.

- This doesn’t replace D3 for the stuff where D3 shines.
  - Someone at the recent Figma Config quoted Nikolas Klein saying, “The goal of a design tool is to find the 900 wrong ideas faster.” 
  - Analogously, one might say Plot doesn’t make better D3 charts; 
  - it lets you find which D3 chart you should be making, by making 900 wrong charts first.

- Try making a chart a minute.
  - With D3 I routinely spend a week on a single graphic; 
  - Plot encourages me to fling them around. 

# [Plot vs Vega-Lite](https://observablehq.com/@observablehq/plot-vega-lite)

lib              |   Observable Plot    |    Vega-Lite 
-----------------|----------------------|------------  
Language         |       JavaScript     | Vega Expressions
Data Transformations | Expressed as JavaScript functions | Built into the library
Data Types       |  Inferred from data  | Explicitly asserted
Interactivity    | Requires custom code | Built in
Package Maturity |      Brand new!      | Years of development and use

- ## Plot is just JavaScript
- Because Plot is just JavaScript, you can quickly replace built-in data processing methods with custom functions, utilizing anything within scope.
- This contrasts with using Vega Expressions which enable custom calculations in a safe and portable way across programming languages and environments. 
  - Because Vega (and Vega-Lite) are designed to be specified (and then compiled) the data processing functions need to be serializable. 
  - The trade-off is that you can safely render a Vega specified visualization in many environments, 
  - but you do need to learn the expression language to do so.
- One way Plot’s pure JavaScript approach can become important is when you want to use another JavaScript library to customize your aggregations. 
  - For example we can use d3-time to bin on Monday based weeks
  - We can do something very similar in Vega-Lite, but we’re constrained to Sunday-based weeks unless we were to transform the data ourselves before passing it to Vega-Lite.

- ## Data transformations
- In Plot, transforms are expressed explicitly as functions rather than built into the library.
- The decoupling of transforms and marks in Plot is intentional so that transforms can be more easily extensible. 
- This means that some types of aggregations and transforms may require slightly more typing than in Vega-Lite with the hope that Plot can be easier to extend with new and custom transforms.

- ## Data types
- The Vega-Lite API requires you to specify the type of your input data explicitly. 
- Plot scales infer data types from the data that is passed in. 
- This means it is important that data passed to plot is properly typed, if you want to work with time you should pass JavaScript dates. 
- You will also find that Plot marks can utilize scales to automatically derive certain graphical properties from the data.

- ## Plot is early and evolving
- While Plot is a new library, it is heavily informed by 10 years of experience developing and maintaining D3.js, as well as being inspired and informed by Vega and Vega-Lite’s evolution. 
- We also know there are some key features missing from Plot that are being planned for future releases, such as supporting interactivity and the easy creation of legends.
