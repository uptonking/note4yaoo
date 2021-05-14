---
title: lib-notebook-observablehq-dev-compiler
tags: [compiler, observablehq]
created: '2021-05-14T14:47:46.096Z'
modified: '2021-05-14T14:48:34.412Z'
---

# lib-notebook-observablehq-dev-compiler

# guide

# Unofficial ObservableHQ Compiler

## docs

- ### [v0.6.0 of the Unofficial ObservableHQ Compiler_202105](https://observablehq.com/@asg017/v0-6-0-of-the-unofficial-observablehq-compiler)
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
