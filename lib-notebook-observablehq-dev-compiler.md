---
title: lib-notebook-observablehq-dev-compiler
tags: [compiler, observablehq]
created: '2021-05-14T14:47:46.096Z'
modified: '2021-05-14T14:48:34.412Z'
---

# lib-notebook-observablehq-dev-compiler

# guide

# Unofficial ObservableHQ Compiler

# docs

## [AN OBSERVABLE NOTEBOOK compiled to js_202](http://www.tophtucker.com/observable-docco/index.js.html)

- When you download an Observable notebook, you get a compressed folder of files. 
- Several are basically the same for every notebook
- index.html 
  - loads everything else; 
  - it imports the notebook definition, Runtime, Standard Library, and Inspector. 
  - It does not hold the main content of your notebook; 
  - it is customized only with your title.
- package.json 
  - includes basic metadata about your notebook to make it an npm-installable package.
- runtime.js 
  - includes a copy of the Runtime, Standard Library, and Inspector, 
  - so that your tarball is self-contained and runs without an Internet connection.
- index.js 
  - is the default entry point for the notebook package, 
  - and just points to your main notebook definition.
- README.md 
  - includes a link to your notebook on observablehq.com 
  - and boilerplate information about how you can use the package.
- inspector.css 
  - styles the display of cells that return a JavaScript value (like an array or string), as opposed to a DOM node. 
  - It does not include the other styles (like fonts, colors, and tables) that you see when you render a cell on observablehq.com.

- notebook contents

- The content of each cell is wrapped in a function, 
  - and each function is passed to the runtime as a cell definition. 
  - In this context, each cell is called a variable. They’re basically the same thing; 
  - what you see as a cell in the frontend is defined as a variable for the runtime.

- I said earlier that cells and variables are basically the same thing. 
  - One exception is that there are built-in variables that aren’t represented by any cell. 
  - This last cell depends on one of them, `require`.
  - We saw three other examples above: `FileAttachment`, `md`, and `width`.

- That’s how a compiled Observable notebook is defined for the Runtime.
- For me, seeing the notebook in plain JavaScript clarified what the curly brace block syntax does; 
  - how reactive variables relate to the scope of a cell; 
  - and that asynchronous cells don’t look that scary. (One thing not shown here is a generator cell, with yield statements; maybe I should find a better example!) 
  - It also begins to demystify(使明白易懂；深入浅出地解释) the Runtime, which enables very intricate(复杂的；难理解的) interoperation. 
  - Finally, it helps understand how to copy and paste to port a notebook to a non-reactive setting (without the Runtime). 
  - If you pull out one of these functions, it’s plain JavaScript, and if you call it with the same arguments, you’ll get the same result.

## [v0.6.0 of the Unofficial ObservableHQ Compiler_202105](https://observablehq.com/@asg017/v0-6-0-of-the-unofficial-observablehq-compiler)

- The biggest change in v0.6.0 is the API change to distinguish between the library as a compiler and as an interpreter. 
  - Before, the entire thing was called a "compiler", but that wasn't really accurate.
  - in this library, the interpreter interprets (ie, executes) Observable JavaScript in a JavaScript environment, while the compiler compiles (ie, generates source code) Observable JavaScript into plain JavaScript as text. 
- The Interpreter takes Observable-style JavaScript and executes it. 
  - The Interpreter can be used in places like custom Observable notebook editors, 
  - or places that want to use Observable-style JavaScript and the Observable runtime.
- The compiler takes Observable JavaScript and compiles it to "plain" JavaScript, in the form of ES Modules. 
  - It's meant to make Observable source code more portable, since most other tools don't understand Observable JavaScript (but they can understand ES modules!).
- Tree-Shaking!
  - When compiling, you now have to option to tree-shake the compiled output on a cellular level. 
  - The compiler that observablehq.com uses doesn't have this feature

- [An Unofficial ObservableHQ Compiler_201909](https://observablehq.com/@asg017/an-unofficial-observablehq-compiler)
  - This notebook describes the old version of the compiler, v0.5.0, but the new version v0.6.0 is currently in beta.

- [pr: v0.6.0 Beta version: New Interpreter and Compiler APIs](https://github.com/asg017/unofficial-observablehq-compiler/pull/29)

# discuss

- ## [From raw notebook source to Observable runtime V1 modules_201903](https://observablehq.com/@bryangingechen/from-raw-notebook-source-to-observable-runtime-v1-modules)

- Update: Alex Garcia's Unofficial ObservableHQ Compiler lets you do much of the following for runtime V3 modules!
- 这里的compiler主要工作是将 手动编辑输入的字符串源码 编译成 js模块

- One of the great features of Observable notebooks is that the code for every cell is easily accessible – either displayed beneath every cell (if the cell is "pinned") or available after a click in the left sidebar. 
- Thus a cell can be represented as a JS Object containing a string for this displayed code string (let's call this the "raw source") and a boolean for the pin state. 
- An Observable notebook then can be stored in an array of such cell objects.
- This array contains the raw source of each cell, and is more or less what we interact with when we're writing and editing a notebook.

- How does the raw source get turned into a live-running cell? 
- In general, you can't copy and paste it directly into a standalone JS file or into a script tag in an HTML file.
- The solution, as given in the "Downloading and Embedding Notebooks" tutorial is to download a separate .js file which can be used with the Observable runtime library.
- Previously, such files defined modules in "Runtime version: 1" format, and I'll call them "runtime V1 modules" or "V1 modules" for short.
- These JS files are the second representation of Observable notebooks, and they are (closer to) what the browser sees when it "runs" the notebook.

- This notebook documents my attempt to bridge the gap and imitate roughly what the Observable servers do in generating the V1 module code. 
- In other words, this will be a demonstration of how raw notebook cell source (like what's stored in the JSON response) can be transformed into "module" code that the Observable runtime library can understand. 
- Along the way there'll be examples of the Observable runtime, inspector, and parser libraries in use.
- Edit (2019/09/27): Don't know why I didn't realize this when I wrote this notebook, but **what this notebook provides a COMPILER from notebook JSON files to runtime V1 modules**!

- The main function below, toV1, can take the notebook JSON object above and turn it into a string which is suitable for loading as a module and passing to an instance of the Observable runtime

- So, how exactly does toV1 work? How do we get from the raw source of each cell in the JSON to code for the V1 module?
- First, recall that each cell of a notebook is represented by an object in the JSON, and the part that we care about is just the value field, which is a string containing the source of that cell. On the other hand, the V1 module code consists of one or more runtime modules, which each contain an array of variables. Each cell of the notebook, roughly speaking, corresponds to one variable in the first module (called m0). The exceptions are import cells and viewof and mutable cells.
- To do this, we'll make use of the Observable parser library
- The Observable parser library's `parseCell` function takes as input the raw source and returns an abstract syntax tree of the cell, plus important meta info, including e.g. whether the cell is asynchronous, or a generator, as well as an array of dependencies of the cell
- If you dig through the parser output, you can see what goes into the name and inputs fields (hint: look in id and references), and then it's just a matter of trimming the cell source (using start and end) and wrapping it in another function call (or not) (this depends on whether the cell's type is parsed as "BlockStatement" or not). Ultimately, all this data and logic become embedded expressions in a big JS template literal.
- Cells which use viewof or mutable syntax are a tiny bit more complicated. Each viewof X cell becomes two variables, one for viewof X and one for X itself.
