---
title: lib-notebook-dataflow-unofficial-compiler
tags: [compiler, dataflow, notebook]
created: 2021-05-25T21:29:06.847Z
modified: 2021-05-25T21:29:41.301Z
---

# lib-notebook-dataflow-unofficial-compiler

# guide
- dataflow的compileNotebook()和runServer()都展示了如何使用unofficial-compiler编译ojs到esm格式的js
# api
- https://github.com/asg017/unofficial-observablehq-compiler/tree/beta
  - An unofficial compiler and interpreter for Observable notebooks (the glue between the Observable parser and runtime)
  - The Interpreter will interpret "Observable syntax" into "javascript syntax" live in a javascript environment. 
  - The Compiler will compile "Observable syntax" into javascript source code (as an ES module).

## `new Interpreter(params)`

- `Interpreter` is a class that encompasses all logic to interpret Observable js code.
- Keep in mind, there is no sandboxing done, so it has the same security implications as `eval()`.

- `params` is an optional object with the following allowed configuration
- `resolveImportPath(path, specifers)`
  - An async function that resolves to the `define` definition for a notebook. 
  - specifiers is a array of string if the imported cell name specifiers in the statement (cells inside import {...}). 
  - specifiers is useful when implementing tree-shaking. 
  - For example, import {chart as CHART} from "@d3/bar-chart" would supply path="@d3/bar-chart" and specifiers=["chart"].
- `resolveFileAttachments`
  - A function that, given the name of a FileAttachment, returns the URL that the FileAttachment will be fetched from
- `defineImportMarkdown`
  - whether to define a markdown description cell for imports in the notebook
- `observeViewofValues`
  - whether to pass in an observer for the value of viewof cells
- `module`
  - A default Observable runtime `module` that will be used in operations such as `.cell` and `.module`
- `observer`
  - A default Observable runtime observer that will be used in operations such as `.cell` and `.module`

- `interpret.cell(source [, module, observer])`
  - Parses the given string `source` with the Observable parser `.parseCell()` and interprets the source, passing it and the observer along to the Observable module. 
  - Returns a Promise that resolves to an array of runtime variables that were defined when interpreting the source. 
  - More than one variable can be defined with a single cell, like with `viewof`, `mutable`, and `import` cells. 
  - source can also be a pre-parsed cell instead of source code.

- `interpret.module(source [, module, observer])`
  - Parses the given string `source` with the Observable parser `.parseModule()` and interprets the source, passing it and the observer along to the Observable module. 
  - Returns a Promise that resolves to an array of an array of runtime variables that were defined when interpreting the source. 

- `interpret.notebook(source [, module, observer])`

## `new Compiler(params)`

- `Compiler` is a class that encompasses all logic to compile Observable javascript code into vanilla Javascript code, as an ES module. 
- `params` is an optional object with the following allowed configuration.
- `resolveImportPath(path, specifers)`
  - A function that returns a URL to where the notebook is defined.
- `resolveFileAttachments`
- `UNSAFE_allowJavascriptFileAttachments`
  - When `true`, the `resolveFileAttachments` function will resolve to raw JavaScript when calculating the value of a `FileAttachment` reference. 
  - This is useful if you need to use new URL or `import.meta.url` when determining where a FileAttachment url should resolve too. 
  - This is unsafe because the Compiler will not escape any quotes when including it in the compiled output, so do use with extreme caution when dealing with user input.
- `defineImportMarkdown`
- `observeViewofValues`
- `observeMutableValues`

- `compile.module(source)`
- `compile.notebook(source)`
# codebase
