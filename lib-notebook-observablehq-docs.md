---
title: lib-notebook-observablehq-docs
tags: [docs, observablehq]
created: '2021-05-14T18:00:13.935Z'
modified: '2021-05-14T18:00:35.421Z'
---

# lib-notebook-observablehq-docs

# guide

- ref
  - [Observable: The User Manual](https://observablehq.com/@observablehq/user-manual)

# A Taste of Observable

- A notebook is made up of a series of cells, and each cell is defined by its JavaScript source code.
- Let’s make that forecast easier to read by taking the next few days of weather and turning it into a table
- This reactivity is the heart of what makes Observable notebooks a special environment for exploration. 
  - Whenever you change anything, or anything changes by itself, the rest of the notebook instantly updates to reflect the latest information. 
  - In technical terms, this is called reactive, or dataflow programming. 
  - But in practical terms, it means that your notebooks never get stuck in a broken state, and that you never have to refresh the page. 
  - Reactivity gives you immediate feedback when you are exploring your data, sketching ideas in code, and collaborating with others.
- Observable makes it particularly easy to repurpose and remix other peoples’ D3 visualizations.
  - Since the external notebook also happens to also render data in the Weather.gov forecast format, that’s not going to be too hard.

# [Why Observable?](https://observablehq.com/@observablehq/why-observable/2)

- Observable was born out of many years of creation in the world of data visualization and understanding developer productivity.
- The notebook is a running environment with no compiling required.
  -  Rather than track dependencies in your head, Observable re-evaluates cells whenever things change, like a spreadsheet.
- Observable offers thousands of visualizations to start from: charts with D3 and Vega-Lite, maps, art, and other components.
- You can share and collaborate with others

# [How Observable Runs](https://observablehq.com/@observablehq/how-observable-runs)

- If you’ve used other interactive notebooks before, you’re probably accustomed to code running from top to bottom. 
  - The first cell runs first, the second cell runs second and can reference values defined in the first cell, and so on down the page.
- Observable is different: it functions like a spreadsheet, where cells (like formulas) run **automatically** whenever their referenced values change. 
  - Observable runs cells independently of their order in the notebook, giving you the flexibility to arrange your cells in whatever order you prefer for literate programming.
- Observable uses **topological order** to run cells, as determined by cell references. 
  - Rather than a linear sequence of cells, an Observable notebook is a directed graph where values flow from top to bottom.
- We’ll consider the graph of a bar chart notebook as a whole later
  - To construct the y-scale, we need several values that are external to the cell: d3, data, margin (an object defining the chart’s margins in pixels), and height (the height of the chart, again in pixels).
  - before we can compute the maxValue, we need to have loaded the data, and so on.
- Observable identifies these external references by parsing the JavaScript and looking for variables that are not declared in scope. 
  - These variables are instead defined by other cells in the notebook. 
  - (Or if they are missing, Observable won’t compute the referencing cell: you’ll get a RuntimeError.)
  - Observable understands scoping, so you can define a local variable with the name of another cell, and this local variable will mask references to the cell.
- As above, we can think of a notebook as a directed graph representing the flow of data, 
  - where the nodes in the graph are cells and the directed edges go from a referenced cell to a referencing cell. 
  - A cell’s references are its incoming edges.
- Before we can compute the y-scale, then, we need the values of its incoming references: height, data, d3 and margin.
  - These may be defined asynchronously—for example, D3 needs to be loaded from unpkg and the data set needs to be loaded from GitHub. 
  - They may even be dynamic, as with a dataset that changes over time.
- We can also look at the outgoing edges from a cell: other cells that reference this cell’s value. 
  - If the y-scale changes, Observable recomputes the downstream cells: yAxis and chart.
  - We need the entire graph, as we’ll need to recompute the outgoing references of those cells, their outgoing references, and so on, until the notebook is up-to-date.

- There are a few interesting consequences of this design.
- First, the order of computation for cells at the same topological level is arbitrary!
  - For example, width, height and margin don’t reference any other cells, so Observable can compute them in any order. 
  - If the cells are defined asynchronously, such as a promise that fetches a dataset from a remote server, the cells will run concurrently.
  - Thus, be wary of side-effects and implicit dependencies on other cells (such as selecting from the DOM), as the order of computation is not guaranteed.
- Second, circular references are not allowed.
- The data flow graph also allows Observable to recompute a subset of the graph efficiently when something changes. 
- In March of 2020, we introduced visual dataflow so you can see how data flows through your notebook. 
  - For a more detailed view of your notebook’s graph, also see the notebook visualizer.

# [Observable’s not JavaScript](https://observablehq.com/@observablehq/observables-not-javascript)

- by building on the native language of the web, Observable is more familiar and you can use the libraries you know and love, such as D3, Three, and TensorFlow. 
  - Yet for (topological)dataflow, Observable needed to change JavaScript in a few ways.
- Here’s a quick overview of what’s different.
- Cells are separate scripts.
  - Each cell in a notebook is a separate script that runs independently. 
  - A syntax error in one cell won’t prevent other cells from running.
  - local variables are only visible to the cell that defines them.
- Cells run in topological order.
  - Observable runs like a spreadsheet, so you can define your cells in whatever order makes sense.
- Cells re-run when any referenced cell changes.
  - Only the referencing cells run, then their referencing cells, and so on—other cells are unaffected.
  - If a cell allocates resources that won’t be automatically cleaned up by the garbage collector, such as an animation loop or event listener, use the invalidation promise to dispose of these resources manually and avoid leaks.
- Cells implicitly await promises.
  - You can define a cell whose value is a promise.
  - If you reference such a cell, you don’t need to await; the referencing cell won’t run until the value resolves.
- Cells implicitly iterate over generators.
  - yields occur no more than once every animation frame: typically sixty times a second, which makes generators handy for animation. 
  - If you yield a DOM element, it will be added to the DOM before the generator resumes.
- Named cells are declarations, not assignments.
  - Cell names must also be unique.
  - cells can be defined in any order, so think of them as hoisted function declarations.
  - You can’t assign the value of another cell 
  - Observable doesn’t yet support destructuring assignment to declare multiple names
- Statements need curly braces, and return (or yield).
  - A cell body can be a simple expression, such as a number or string literal, or a function call. 
  - But sometimes you want statements, such as for loops. 
  - For that you’ll need curly braces, and a return statement to give the cell a value. 
  - Think of a cell as a function, except the function has no arguments.
  -  you’ll need to wrap object literals in parentheses, or use a block statement with a return.
- Cells can be views.
  - Observable has a special `viewof` operator which lets you define interactive values.
  - A view is a cell with two faces: its user interface, and its programmatic value.
- Cells can be mutables.
  - Observable has a special `mutable` operator so you can opt-in to mutable state: you can set the value of a mutable from another cell.
- Observable has a standard library.
  - a small standard library for essential features, such as Markdown tagged template literals and reactive width.
- Cells can be imported from other notebooks.
  - Observable imports are lazy: if you don’t use it, it won’t run.
- Static ES imports are not supported; use dynamic imports.
  - we might add static ES imports support in the future
  - Note that only the most-recent browsers support dynamic imports, so you might consider using require for now.
- require is AMD, not CommonJS.
  - Observable’s require looks a lot like CommonJS because cells implicitly await promises. 
  - But under the hood it uses the Asynchronous Module Definition (AMD).
  - This convention will eventually be replaced with modern ES modules and imports

# Notebook fundamentals
