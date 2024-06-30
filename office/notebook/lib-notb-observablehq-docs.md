---
title: lib-notb-observablehq-docs
tags: [docs, observablehq]
created: 2021-05-14T18:00:13.935Z
modified: 2024-06-30T03:20:34.112Z
---

# lib-notb-observablehq-docs

# guide

- features
  - free private collaboration
  - realtime multiplayer editing
  - cell modes for MD, HTML & more

- [hands-on introductory tutorial series](https://observablehq.com/collection/@observablehq/introduction)

- ref
  - [Observable: The User Manual](https://observablehq.com/@observablehq/user-manual)
# A Taste of Observable
- A notebook is made up of a series of cells, and each cell is defined by its JavaScript source code.
- This reactivity is the heart of what makes Observable notebooks a special environment for exploration. 
  - Whenever you change anything, or anything changes by itself, the rest of the notebook instantly updates to reflect the latest information. 
  - In technical terms, this is called reactive, or dataflow programming. 
  - But in practical terms, it means that your notebooks never get stuck in a broken state, and that you never have to refresh the page. 
  - Reactivity gives you immediate feedback when you are exploring your data, sketching ideas in code, and collaborating with others.
- Observable makes it particularly easy to repurpose and remix other peoples’ D3 visualizations.
# [Why Observable?](https://observablehq.com/@observablehq/why-observable/2)
- Observable was born out of many years of creation in the world of data visualization and understanding developer productivity.
- You can explore data and create.
  - The notebook is a running environment with no compiling required.
  - Rather than track dependencies in your head, Observable re-evaluates cells whenever things change, like a spreadsheet.
- Observable offers thousands of visualizations to start from
  - charts with D3 and Vega-Lite, maps, art, and other components.
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
- observablehq特有的语法
  - A syntax error in one cell won’t prevent other cells from running.
  - cells run in topological order
  - auto re-evaluate
  - Cells implicitly await promises.
  - Cells implicitly iterate over generators.
  - named cells
  - Statements need curly braces, and return (or yield).
  - cells can be views
  - cells can be mutables
  - stdlib in runtime: lodash, d3, vl, Inputs, Plot, dot, htl
  - Cells can be imported from other notebooks.
  - Static ES imports are not supported; use dynamic imports.
  - require is AMD, not CommonJS. require uses jsdelivr

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
  - Since everything in Observable is inherently dynamic, there’s not really a need for static ES imports
  - we might add static ES imports support in the future
  - Note that only the most-recent browsers support dynamic imports, so you might consider using `require` for now.
- `require` is AMD, not CommonJS.
  - Observable’s `require` looks a lot like CommonJS because cells implicitly await promises. 
  - But under the hood it uses the Asynchronous Module Definition (AMD).
  - This convention will eventually be replaced with modern ES modules and imports
# Cells are Functions
- In Observable, each cell is a function; 
  - this function is called automatically by the runtime with the values of any other cell it references.
- Unlike promises, generators are automatically terminated on invalidation by the runtime.
- If you want to avoid a generator, you can do something similar using the invalidation promise and `Promise.race`: 
  - this will throw an error when the cell is invalidated, causing the loop to terminate. 
  - This error is never shown because the cell is immediately re-evaluated, giving it a new value.
# Notebook fundamentals

## Five-Minute Introduction

- An Observable notebook consists of cells.
- Each **cell** is a snippet of JavaScript. 
  - You can see (and edit!) the code for any cell by clicking the menu in the left margin
- Cells can have names.
  - This allows a cell’s value to be referenced by other cells.
  - A cell referencing another cell is re-evaluated automatically when the referenced value changes. 
- Cells can generate DOM (HTML, SVG, Canvas, WebGL, etc.). 
  - You can use the standard DOM API like `document.createElement`, or use the built-in `html` tagged template literal
  - There’s a Markdown tagged template literal, too
- DOM can be made reactive simply by referring to other cells.

- Sometimes you need to load data from a remote server, or compute something expensive in a web worker. 
  - For that, cells can be defined asynchronously using **promise**s
  - A cell that refers to a promise cell sees the value when it is resolved; 
  - this implicit await means that referencing cells don’t care whether the value is synchronous or not. 
- Promises are also useful for loading libraries from npm
  - `d3 = require("d3-fetch@1")`.
  - `require` returns a promise that resolves to the `d3-fetch` library
- If you prefer, you can use async and `await` explicitly

- Cells can be defined as **generator**s; 
  - Any cell that refers to a generator cell sees its current value; 
  - the referencing cell is re-evaluated whenever the generator yields a new value.
  - a generator can yield promises for async iteration; referencing cells see the current resolved value.

- Combining these primitives—promises, generators and DOM—you can build custom user interfaces.
- `Generators.input` returns a generator that yields promises. 
  - The promise resolves whenever the associated input element emits an input event. 
  - You don’t need to implement that generator by hand, though.
  - There’s a builtin `viewof` operator which exposes the current value of a given input element

- You can import cells from other notebooks.

## Introduction to Code

- Observable notebooks are written in JavaScript, the web’s native language, but with a few changes. 
- Cells come in two primary forms: expressions and blocks. 
  - Expression cells are the most concise and are intended for simple definitions, such as basic arithmetic(算术)
  - Blocks are surrounded by curly braces, `{ }`, and are intended for more complex definitions, such as ones involving local variables or loops
- Local variables can’t be referenced from other cells; 
  - trying to reference an unknown variable will throw a runtime error. 
  - However, this error is localized to the broken cell, allowing the rest of the notebook to run happily.
- If you want to define a cell as an object literal, you must wrap the literal in parenthesis to disambiguate it from a block
- To share code between cells without copying and pasting, define a function
- While local variables are not visible across cell boundaries, you can name cells to reference their values
  - This looks identical to a standard JavaScript assignment, but it’s not—it’s reactive!
- You needn’t define named cells before you reference them: order your cells however you like, 
  - and Observable will automatically execute them in topological order. 
- A cell that references other cells is re-evaluated automatically whenever the referenced values change.
  - This reactivity is similar to live reload, with an important difference: when a value changes, only referencing cells are re-evaluated, rather than the entire notebook.
- To understand reactivity, think of each cell as a function.
  - the runtime waits for the value of a and b to resolve and then invokes the sum function.
  - The runtime invokes sum again whenever a or b change.
- If a cell contains a `yield` statement, the runtime creates a generator function instead of a normal function.
  -  Likewise if the definition uses await, the runtime creates an `async` function.

## Introduction to HTML

- If a cell returns a DOM element, that DOM element is displayed as-is!
  - Or using the W3C DOM API directly (not that you should—it’s quite verbose)

```JS
html `<p>I am a <i>paragraph</i> element!</p>`

// 既可以使用 dom标签，也可以使用 dom js api

{
  const p = document.createElement("p");
  p.appendChild(document.createTextNode("I am also a "));
  p.appendChild(document.createTextNode(" element!"));
  return p;
}
```

- Even better, you can write Markdown
- Since all cells in Observable are JavaScript—a “Markdown cell” is just a JavaScript cell of a Markdown tagged template literal—Markdown and HTML cells can be dynamic: you can embed expressions `${…}` in template literals
  - Embedded expressions can also be DOM nodes. 
  - This lets you embed dynamic content, such as little charts in SVG or mathematical notation in LaTeX, within Markdown.
  - I like Markdown for prose, but katex for math.
- And of course, Markdown can be reactive, too! 
  - The `now` built-in from the Observable standard library is a reactive variable whose value is the current time.
  - So, embedding a reference to `now` causes the Markdown to re-evaluate continuously

- Another common type of dynamic content is Canvas.
  - The standard library method `DOM.context2d` returns a `CanvasRenderingContext2D` of the specified width and height (and automatic scaling for high-resolution displays). 
  - Draw to the context, and then return the canvas to display it in the notebook.

- Often you’ll use a helper library such as D3 to generate dynamic content
  - more succinctly as a single expression
- If your DOM is defined purely as a function of data—that is, if you don’t need D3’s data join to update and exit nodes, and instead you just create the DOM from scratch every time
  - then usually it’s simpler to stick with template literals. 
  - There’s an svg tagged template literal in the standard library that is useful for composing SVG fragments.
- For the mathematically inclined, you can write katex, either inline or as blocks
- you can read properties of a DOM element defined in another cell
  - But note that properties of a DOM element are not automatically reactive: 
  - a cell that references slider.value won’t be re-evaluated automatically when the slider changes. 
  - DOM elements are mutable, so be careful when referencing an element defined in another cell, and you should usually avoid mutating elements defined in other cells
- Cells share the same iframe, so you can use CSS to change styles globally.
- Use caution when applying global styles: if a style affects a cell’s height, the runtime may not notice unless the affected cell is re-evaluated.
  - You can explicitly tell the runtime to recompute cell heights by dispatching a load event, but it shouldn’t be necessary in most cases.
- A cell can return a DOM element that’s already being displayed somewhere else on the page. 
  - In this case, the value inspector is used, rather than showing the element inline.

## [Introduction to Views](https://observablehq.com/@observablehq/introduction-to-views)

- In Observable, a view is a user interface element that directly controls a value in the notebook. 
- A view consists of two parts:
  - The `view`, which is typically an interactive DOM element.
  - The `value`, which is any JavaScript value.
- See Observable Inputs for inputs that are more convenient and more usable than the native HTML inputs
- views aren’t limited to built-in HTML input types! 
  - A view can have any visual representation you desire, and any value, too.
  - A view could be a blank canvas for the user to draw a squiggle(写或画的弯弯曲曲的线条；潦草的笔迹)
- If there is a value you’d like the user to control in your notebook, represent that value as a view. 
- view’s value is exposed as `element.value`. 
- The `viewof` operator is just shorthand for defining the view and its value in the same cell. 
  - You can define them as separate cells if you prefer
- To trigger the re-evaluation of any cell that references a view’s value, the view must emit an input event
- the reason that HTML input elements work by default as views is that these elements have a `value` property and they emit `input` events when you interact with them. 
  - There is a little extra logic for dealing with idiosyncrasies; see the `Generators.input` source for details. 
  - And a view doesn’t need to be a DOM element; it only needs to support the `EventTarget` interface. 
  - For an example of a non-element view, see the Synchronized Inputs notebook.

## [Introduction to Mutable State](https://observablehq.com/@observablehq/introduction-to-mutable-state)

- Observable notebooks are made of cells. 
  - Each cell is defined by a bit of code and will react to updates in any other cells it references.
  - To take full advantage of this reactivity, we generally want to **avoid mutation** in our Observable code. 
  - Instead of reaching into the contents of other cells and setting values imperatively, each cell should usually return a new value when it runs. 
  - Any cells that reference that value will run every time the upstream cell recomputes.
- But you might run into a situation where this reactivity becomes a bit tricky to work with
  - What if I want to be able to set a cell’s value programmatically?
  - What if I want a cell to update some but not all of the times another cell’s value changes?
  - What if I want a long-running cell — like an animation loop — to use another cell’s value, but not reset itself when that value changes?
- In situations like these you have two main options:
  - Rewrite your code to use a functional style and avoid mutation (generally the best idea!)
  - Use Observable’s `mutable` keyword to define a cell with a mutable value — one that is meant to be changed by other cells.

- In Observable, a cell will automatically run each time any value it depends on changes.
- you can use Observable’s `mutable` keyword to define a cell with a mutable value — one that is meant to be changed by other cells.
- By using `mutable`, we can control the timing of when a downstream cell should be re-evaluated, by only setting its value at the appropriate moment. 
  - This can help cells share values without creating circular dependencies, and also prevent cells from updating more often than is needed — while allowing any cells that depend on them to continue receiving reactive updates as normal.

- Mutable values can be referenced either reactively, or non-reactively, as appropriate. 
  - To use the current value of a mutable without creating a dependency, use `mutable x`; 
  - to depend on it for re-evaluation, just use `x`.

## Introduction to Imports

- Observable lets you quickly reuse code by importing named cells from other notebooks.
- You could instead copy-paste the `ramp` function from that notebook into this one—it’s only a few lines of code.
- But imports have a few advantages.
- First, the cell you want to reuse may depend on other cells. 
  - If you import, the dependencies are loaded automatically, so you don’t have to think about it.
- Second, by importing, it’s easier to keep the reused code up-to-date.
  - Imports target the latest published version
  - The risk of importing the latest version is that your notebook may break if the imported notebook changes in a non-backwards-compatible way.
  - Observable also supports versioned imports, however version numbers aren’t currently exposed in the user interface, so for now you must specify the version manually.
  - In the future, imports will be pinned to the latest published version at the time you write the import statement, and can be re-pinned on-demand.
- Third, Observable imports let you inject dependencies using import-with!
  - As long as the new data conforms to the same shape as the old data, you can reuse the existing code
- Best of all, because Observable is reactive, you can even inject dynamic definitions into code that was previously static!

- Here are a few additional nuances(细微差别) of imports
- Like ES imports, Observable imports are live bindings. 
  - If you import a value that changes over time (a generator cell), the imported value will change over time, too
- You can only import named cells, 
  - and you must name each cell you want to import explicitly. 
  - No anonymous cells allowed; 
  - if a notebook uses side effects, as is sometimes common with anonymous cells, you must name and import the cells with side effects, too.
- Imported cells are lazily evaluated: 
  - if you import a cell but you don’t reference it anywhere, the code won’t run.
- Also like ES imports, only the cells you import are available (bound) in the local notebook, even if those cells depend on other cells. 
  - Those dependent cells are run—they’re just not exposed in the scope of the local notebook.
- You can use circular imports, but only if you don’t use the `with` clause when importing.
- You can import the same notebook multiple times and references will resolve exactly.
- If you find yourself using lots of imports in your notebooks, you might find our import visualizer helpful for debugging. 
- You can import from shared (non-public) notebooks, too
- You can even import from private notebooks
  - Don’t forget to share or publish your imports before you publish.

- Lastly, imports aren’t intended to replace libraries (like lodash or D3); 
  - if you want to design, build and support a reusable library, go for it and publish to npm! 
  - But if you want a lightweight way to reuse code across notebooks without resorting to copy-paste, reach for import.

## [Introduction to Data](https://observablehq.com/@observablehq/introduction-to-data)

- How do you get data into Observable for analysis and visualization?
  - inline - embedded in the notebook as code, for small amounts of data
  - files - attached to the notebook, for medium amounts of data (e.g., CSV, SQLite)
  - APIs - queried from a remote server, for programmatic access to data
  - databases - via an Observable database client, for accessing SQL databases
- For tiny datasets, you can inline JSON/CSV
- For medium-size datasets, you can attach files directly to your notebooks
  - To use a file, pass the file’s name to the built-in `FileAttachment` function from the Observable standard library 
  - then call the appropriate method depending on how you want to consume the file.
  - You can also fetch files uploaded and hosted on outside services such as GitHub Gist, as long as they support CORS.
- You can read local files in your notebooks too, without hosting
- A particularly powerful type of file for data analysis is a SQLite file, which you can query with arbitrary SQL, using SQL.js.
- There are myriad APIs available on the web, many of which are publicly accessible.
  - You can also use WebSockets to connect to realtime data streams!
  - If you want to access services that use API secret keys or passwords, you can use Observable secrets to store sensitive values securely, separately from code
- databases
  - To access PostgreSQL 8+, MySQL 5, or Google BigQuery databases, you can use an Observable database client.
  - For databases on private networks, use our self-hosted Observable database proxy. 

- You can also download generated data from notebooks.
- You can get data back out of notebooks as CSV or JSON by clicking on the cell menu.
  - This technique is especially useful for transforming (aggregating, filtering or reducing) data within a notebook, and then loading the transformed data in the future rather than transforming it on load. 
  - You can also download any attached files from the files pane.
- In addition to the built-in cell download menu items, you can download any file using `DOM.download`. 

## [Reading Local Files](https://observablehq.com/@mbostock/reading-local-files)

- As an alternative to attaching a file to your notebook, you can read files from your local file system in Observable using a file input
  - The initial value of a file input is `undefined`, so any cell that references this file will wait for the reader to choose a file before running. 
  - If you’d an initial value so that referencing cells run on load, wrap the input in a form and assign the form’s value. 
  - Or, import my reusable file input with initial value.
- A `File` is a `Blob`, so one way to read a file is to use `URL.createObjectURL`. 
  - This is useful, for example, with images. 
  - (Don’t forget to revoke your URLs, though, say using `Generators.disposable`.)
- This works with `require`, too
- You can also read a file using a `FileReader`. 
  - Observable’s standard library includes several convenience methods for reading files.
- If the file is text, use `Files.text` to obtain a promise to a String.
- For a binary file, use `Files.buffer` for a promise to an ArrayBuffer.

## Connecting to databases

- Observable database clients allow secure and convenient querying of SQL databases from private notebooks
- We currently support PostgreSQL 8+, MySQL 5, Google BigQuery, and Snowflake. 
- Create a DatabaseClient for a configured database, then use `client.query(sql, [parameters])` to issue a query, or `client.describe(table)` to inspect the schema.

## Introduction to Secrets

- we’re introducing Secrets, a new feature to make it easier to securely access private data and APIs on Observable.
- Secrets are name-value pairs, similar to environment variables, that you can can specify in your settings.
- Only your private notebooks (which are only readable by you) can access your secrets—that’s why they’re secret!
  -  If you share or publish a notebook, it won’t be able to access secrets: any cell that references the Secret function will error.
- You must explicitly grant permission for a notebook to access your secrets. 

## [Observable anti-patterns and code smells](https://observablehq.com/@tmcw/observable-anti-patterns-and-code-smells)

- Here are a few things that you might do a bunch in JavaScript ‘in general’ but are often more trouble than they're worth within in the context of Observable.

- Timers: use them sparingly, a lot of times there’s a better way
- Now timers will still ‘work’ in Observable
- cells are often re-evaluated, so it's important that everything a cell does can be cleaned up.

- Mutation: try to avoid it!
- Notebooks work better and are much more understandable if you keep mutation to a minimum. 
- Mutation being defined here as ‘changing a variable in-place’: not creating a new variable that’s some modification of an old one, but instead changing the original variable's value. 
- Some common sources of mutation in JavaScript are:
  - Array methods like .sort() and .splice() that modify arrays in-place
  - Similar methods on custom objects that modify them
  - Stateful regular expression methods
- One of my favorite things about Observable notebooks is that cell evaluation order doesn't matter. 
  - They don't run top-to-bottom, they simply run whenever values are needed or updated. 
  - Mutation really mucks that up.
- When you run into a method that works by default with mutation, you can make your code nice and ‘immutable’ instead by:
  - Using an alternative that doesn't mutate the data - for instance, using `Array#concat`, which returns a new Array, instead of `Array#push`, which modifies an array in-place
  - Making a copy of the data and mutating that: for instance, by using `Array#slice()`.
- If you have some object and then assign to some property of it, you have untracked mutation, which is usually bad.
  - the rule that if you want to get a modified object, it should be a new object, not a modification of the one you have. Spread syntax, noted as `...` in code, makes this great
- if you are dealing with modifying objects and arrays a lot, you may want to use something like `lodash`, which lets you avoid mutation by providing lots of useful functions.

- Generators: the return value doesn’t matter
- Don't use `return` in a generator that crosses cell boundaries.
- the return value of a generator is ignored, so don't return from a generator.
- This advice is all about generators that cross cell boundaries. 
  - In a JavaScript sense, you should think of cell boundaries as calling `generator.next()` and ignoring its value if `done` is true: that's what they do internally.

- Re-selecting elements: it's much better to reference elements in a notebook using variables than it is to reference them using class or tag names.
- Once you create an element, there are generally two ways to get a reference to it again in another cell:
  - Using the variable it was assigned to.
  - Selecting it again based on a class, id, or tag name - with `d3.select()`,  `document.querySelector()` .
- Note that this advice only applies for getting elements out of nowhere - you will still likely use sub-selectors to select within elements you already have references to. 
  - It also doesn't apply to using d3.select() with a variable as its argument, only with a string.
- Cells don't run top-down: they run in dependency order.
- And if two cells don't have a dependency relationship - one cell doesn't rely on the other's name - there's no guarantee that they'll run in any specific order. This is a good thing. 
- instead of selecting it based on the fact that it’s an svg element, or by its ID, we use the cell variable

## [Introduction to Embedding](https://observablehq.com/@observablehq/introduction-to-embedding)

- 还可以考虑嵌入动态的图片gif/mp4

- Embedding lets you put a working version of your notebooks inside another website.
- In many cases, you’re done with embedding `iframe`.
- But if you want more control or a deeper integration, you can try the other embedding methods, Runtime with JavaScript or Runtime with React, which generate code that uses the Runtime API to render your cells.
- The Runtime-based embedding methods are limited to environments where you can run your own scripts.
- But since the Iframe isolates that in a different document, it can go in more controlled WordPress blogs, content management systems like Gatsby, and note-taking software like Notion or Roam.
- If you want to pass data in and out of the cells, you’re still better off using `import`s

- Some sites like Medium and Reddit that don’t allow arbitrary HTML still “unfurl” certain links you paste to interactive versions, using a standard called [oEmbed](https://oembed.com/).
  - If the site uses Embedly, the Iframe can automatically resize to match the height of your content.
- It doesn’t help you embed in Slack, Facebook, Twitter, or LinkedIn, which don’t support arbitrary interactive embeds; we still use the notebook thumbnail for those. 

- let’s explore some ways to use embedded notebooks!

- ### Rendering cells
- The most obvious way to embed a notebook is to display its contents, live, in a web page
- It’s important to note that when you render a limited set of cells from your notebook, the cells that aren’t used — or depended on by those that are — won’t be run at all!
- If you want to run a cell with side effects in the background of your embedded notebook, you can return true instead of an inspector for those cells
- Note that CSS `<style>` cells don’t produce their side effects unless they are actually inserted into the DOM; they cannot be silently run in the background, and should instead be interpolated into a displayed HTML cell.

- ### Reading cell values
- An observer is an object that you define and implements optional methods to observe a cell’s live value. 
  - These methods are called repeatedly by the runtime
- Sometimes you just want the current value of a cell. 
  - For that, you don’t need a proper observer; 
  - instead, use `module.value` to get a promise to the current value of the cell with the given name.

- ### Overriding cell values
- your JavaScript program can assign reactive values, too, allowing bidirectional dataflow. 
- Then whenever you want to change the chart’s data, call `module.redefine`.
- Because Observable uses dataflow, the chart will update automatically in response to the new data, and the inspector will replace the contents 
- Another way to alter the behavior of your running notebook is to override Observable’s standard library.

- Notebooks as npm modules

- ### How to: Embed a Notebook in a React App

- [a notebook can embed itself](https://observablehq.com/@jashkenas/ouroboros-a-notebook-embeds-itself)
  - new Runtime().module(notebook).value("animation")

## Introduction to Promises

- A promise represents a value that is not yet known, but that will be known in the future. 
- This asynchronous design, essential for fluid interaction and parallel downloads, introduces complexity: 
  - code that depends on promised values must wait until the values are resolved rather than running immediately. 
  - Fortunately, JavaScript’s `Promise` API (and its companion `await` operator), make it easier to work with asynchronous values.
- Promises are often not created by you. Instead, an asynchronous library method might return a promise, and you need to wait for the promise to resolve (or reject)
- Observable implicitly awaits promises across cell boundaries
- Observable’s standard library has few built-in methods related to Promises.
- The implicit await of promises **only** happens across cell boundaries. 
  - So, if you create a promise and then refer to it within the same cell, you’ll see the `Promise` object and not the resolved value
  - You can use the `await` operator to pause the execution of code in the current cell while you wait for a promise to resolve
  - you can use `promise.then` to chain promises

```JS
// "[object Promise]world!"
{
  let promise = Promises.delay(3000, "Hello, ");
  return promise + "world!"; 
}

// "Hello, world!"
{
  let greeting = await Promises.delay(3000, "Hello, ");
  return greeting + "world!";
}

// "Hello, world!"
Promises.delay(3000, "Hello, ").then(greeting => greeting + "world!")
```

- Some libraries and methods use asynchronous callbacks. 
  - For example, the browser built-in `setTimeout` doesn’t return a promise like `Promises.delay`; 
  - instead it calls the specified callback function after the specified delay. 
  - To use callbacks in Observable, you should adapt to promises using the Promise constructor.

```JS
new Promise((resolve, reject) => {
  setTimeout(() => {
    resolve("Time’s up!");
  }, 5000);
})
```

## Introduction to Generators

- Observable uses generators to represent values that change over time. 
  - Generators enable interaction, animation, realtime data streaming, and all the other exciting, dynamic capabilities of Observable notebooks.
- The simplest generator is a cell that yields a single value.
  - This behaves no differently than a plain expression cell.
- When a yielded value resolves, referencing cells are automatically rerun, even if the new value is the same as the old one.
- Observable waits until the yielded value resolves before pulling the next value from the generator. 
  - The generator cell is magically suspended (paused) until Observable requests the the next value, at which point the cell resumes exactly where it left off. 
  - In effect, there’s an implicit await when you yield a promise.
- If a generator cell yields the same DOM element as it did previously, Observable doesn’t touch the DOM. 
  - This makes yielding an element repeatedly an efficient animation strategy.
- The previously-resolved value continues to be visible to other cells until the newly-yielded value resolves: 
  - in other words, a generator cell’s apparent value is the most-recently resolved value.
- Observable pulls at most one value per animation frame (sixty times per second) from the generator. 
  - To define a cell that counts sixty times per second, yield a resolved value rather than a pending promise.
- Per the iterator protocol, the `return` value of a generator is not considered part of the sequence of values; it is ignored.
- Use delegation (yield-star expressions) to yield the values of an iterable in order.

- Generators that yield promises are the basis for interactive views in Observable.
  - `Generators.observe` takes a push-based data source—code that invokes a callback function whenever there is new data—and converts it to a pull-based generator that yields promises. 
  - These promises resolve with the passed value when `next` is called.
- This pattern is based on JavaScript’s proposed Observable type.
- It’s tedious to add and remove event listeners to observe an input’s value, so the standard library provides `Generators.input` as a convenience method on top of `Generators.observe` for observing inputs. 
  - Yet you rarely need to use `Generators.input` directly: 
  - Observable’s `viewof` operator will do it for you! 
  - If you name a cell `viewof` value, Observable implicitly creates a second (hidden) cell named `value` using `Generators.input`.
- Many generators are infinite—they represent sequences of values that never end. 
  - Observable forcibly terminates the old generator when a generator cell is rerun by calling `generator.return` .
- you can define your own generator functions in notebooks, too.
- Calling a generator function returns a new generator object. 
  - This generator can then be consumed by the runtime, just like a generator cell.
- In addition to generator functions, the Observable standard library has several built-in reactive variables that are implemented with generators. 
  - There’s `width`, which represents the current page width and updates when the window resizes.

## Introduction to require

- Observable’s `require` lets you use thousands of open-source JavaScript modules in your notebooks. 
- require returns a promise with the module’s contents, or, if the module can’t be loaded, a promise rejection.
- Most of the time, you’ll use require in a cell of its own, so you won’t need to worry about the return value being asynchronous. 
  - But if you do want to use require in the context of other code, you’ll need to await the value of the promise it returns.
- By default, require uses modules published on npm
  - Because notebooks run in a web environment, we use another service, jsDelivr, that takes npm’s modules and makes them accessible to browsers.
  - For example, if we call require with the argument "d3@6", it resolves to "https://cdn.jsdelivr.net/npm/d3@6.7.0/dist/d3.min.js"
- The require function works with modules that include AMD distributions and that point to them in the jsdelivr, unpkg or main fields of their package.json files.
  - Unfortunately, not all modules are compatible: 
  - some rely on the built-in functions in Node.js that have no equivalent in the browser, 
  - and others don’t include an AMD file that require can use.
- require works with a subset of AMD modules that includes the vast majority of such modules: 
  - the strict specification is documented by `d3-require`, the module that powers Observable’s require.

- In addition to require, which uses the widely-supported AMD standard, we also support **dynamic import**, a new way of requiring modules that aims to replace custom module loaders such as require.
- It requires modules to be published in the ES6 module specification, which is still gaining adoption.

## [Introducing Visual Dataflow](https://observablehq.com/@observablehq/introducing-visual-dataflow)

- When a cell yields a new value, anything that references its name will be re-evaluated. 
  - That makes those variables “reactive”, different from normal JavaScript variables. 
- Now, we are explicitly showing reactive connections, both in the code editor and in a new minimap.
  - The little gray dots are the minimap. 
# [Observable for Jupyter users](https://observablehq.com/@observablehq/observable-for-jupyter-users)
- Observable, like Jupyter, is a computational notebook that’s great for doing data science and visualization, 
  - where “notebook” refers to a series of cells containing prose, code, and visualizations.

- Observable is reactive
  - This is the biggest difference between the evaluation model of Observable and Jupyter.
  - Like a spreadsheet, Observable keeps track of which cells depend on the output of other cells and recalculates results as necessary to keep everything up to date.
  - You can think of Observable keeping cells up to date as killing the kernel and rerunning the whole notebook each time you edit a cell, or you can think of it as rerunning just the cells that depend on the cell you’re editing (which is what’s actually happening).
  - This is a very different tradeoff than Jupyter makes! Observable’s approach is helpful for quickly iterating on visualizations or other outputs built up over multiple cells, and when a value is used in multiple places in a notebook. Not needing to remember to rerun the right cells is one less thing to worry about while focusing on a notebook’s contents.
  - These special, Notebook-level variables can only be defined once, and cannot be reassigned; cannot define a cell circularly
  - The upside is that user interactions and changes to code propagate instantly. 
- Observable runs a superset of JavaScript
  - You can also write some JavaScript in Jupyter that gets executed in the browser, 
  - but typically code in Jupyter notebooks is written in the kernel language and executed in a remote process running the kernel. 
  - Observable’s flavor of JavaScript is a little bit different, 
- Cell outputs are shown above the code
  - 类似预览组件的效果，上面是预览图，下面是源码
- You can show or hide the code
- Use shift-enter to run a cell, not alt+enter
- Cells produce only one value
  - Like function bodies in JavaScript, cells in Observable are either a single expression or a block of statements. 
  - only one expression is returned from a cell with multiple statements.
  - If no value is returned, similar to ending the last statement in Jupyter with a semicolon, the cell evaluates to undefined.
- Variables defined inside a block can only be accessed inside that block
  - Cell blocks are similar to bodies of functions in this way. 
- Cells can be named
  - Because every cell has just one return value, you should break up big cells into little, focused ones.
- Cells don’t run from top to bottom
- There’s only one kind of cell
  - Instead of Jupyter’s separate Markdown cells and code cells, all cells in Observable contain JavaScript code.
  - The result of evaluating this code is rendered based on its type.
  - Observable includes standard library functions that return DOM nodes, to make it easy to create rich documents with text and graphics.
- Notebooks live on the web
- Code runs in your browser
  - Observable code running in your browser’s JavaScript engine is different from Jupyter code running in a separate kernel process: for instance, you can use your browser’s dev tools to debug your code.
  - Respond to user interaction in milliseconds, without a client–server roundtrip
  - New web superpowers, with d3/webgl/video
  - You can’t get the current process ID in Observable. You can’t directly open a TCP socket, you can’t access the filesystem
- You can import cells from other notebooks
  - Importing a cell from another Observable notebook only runs the cells needed to produce the imported value, 
    - e.g. you can import just a file attachment from another notebook and know that data processing and animations in the notebook are not running in the background.

## Visualize a data frame with Observable, in Jupyter

- The most common reason for Jupyter users to use Observable is the creation and distribution of visualizations. 
- Anytime we have a dataframe like this in Jupyter we can package it up for Observable by exporting to csv
- Once you've got a CSV file with your data, the most direct way to get data into a notebook is to use a file attachment. 
- let's require d3-dsv, a library for parsing for CSVs.
- `irisData = d3.csvParse(await FileAttachment("iris_data.csv").text(), d3.autoType)`
- you can also view the data as a table.
- There's good news on the JavaScript-for-data-wrangling front: your browser's JavaScript runtime is fast.
- Making visualizations with web power
- Reusing cells wholesale
- Sharing your work
# [Interactivity in Observable](https://observablehq.com/@observablehq/interactivity-in-observable)
- Notebooks make arguments and explorations more reproducible by showing each step in code and encouraging the reader to run it themselves. 
- But viewing and modifying code isn't something all viewers are comfortable doing or something even the most technical viewers always have time for. 
- Interactive inputs make the acts of plugging in different data and questioning model assumptions available to everyone. 
- Interactive inputs in Observable, called views, are similar to IPythonWidgets in Jupyter, but tend to be
  - simpler to write
    - because they don't need to deal with crossing the Python/JavaScript border
  - quicker to respond to user changes
    - because they don't require server round-trips
  - more integrated with the notebook
    - because changing a value updates each of its references throughout a notebook, not just a single widget
- Adding a slider, a clickable map, a text box, or other input to modify a value used throughout a notebook works the same way as normal cross-cell communication: reactively.
- Visualizations in Observable are often created in multiple steps across multiple cells.
- In Jupyter, IPythonWidgets functionality like interact() and interactive() can be used to provide inputs which cause a Python function to be reexecuted when changed.
- In Observable, inputs modify variables which any other cells in the notebook are permitted to use. 
  - Cells that reference these variables will all change in sync with the input changing.
- IPythonWidgets allow other objects implementing the widget protocols to be linked on the JavaScript side, skipping the kernel, so the distinction between jslink and a trailets link is important. 
  - This distinction does not exist in Observable, because all code is linked in JavaScript (and links are implicit based on the cells referenced in code, not objects created in code).
- IPythonWidgets often use callbacks to hook up mutable objects, while Observable uses the reactive pattern of recreating objects based on the new values.
- Like IPythonWidgets, the state of a widget, such as which value is currently selected, is not part of the persisted notebook state.
  - If other people are viewing the same notebook, changes to the slider value are not shared between viewers and are not saved. 
- Part of getting used to the lack of client/server roundtrips in Observable is using animations more frequently. 
- Changing the value of a cell can be driven by a generator, a JavaScript language feature very similar to generators in Python.

- In review, for a Jupyter user to get comfortable with Observable it is helpful to:
  - know some JavaScript
  - understand differences from Jupyter, particularly reactivity
  - be able to import data, use a visualization tool, share notebooks and embed visualizations
